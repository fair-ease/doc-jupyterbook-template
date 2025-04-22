---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# GECCO analysis over time (EXAMPLE)

This is far from perfect example, but the point being that that treating the EMO-BON samplings as *complex networks*, ie. graphs provides advantages on how to compare the results over time and space.

Every sequencing event is represented as a graph. Graphs can be constructed on both *taxonomy* [1](https://doi.org/10.1093/bib/bbaa005) and *functional* tables. Depending on the question at hand, different graphs represent the sequencing result [rK communities](https://www.nature.com/articles/s41598-021-03018-z).

Here I create graphs from the secondary analysis (GECCO) runs to identify *Biosynthetic Gene Clusters* (BGCs).

::::{note} Pilot demos allow to submit and receive GECCO jobs run on Galaxy. If interested, start [here](https://github.com/emo-bon/momics-demos?tab=readme-ov-file#wf3-biosynthetic-gene-clusters-bgcs)
:class: dropdown
::::

## Setup

I ran GECCO locally on the assembled contigs from the metaGOflow for one single station (Ria Formosa). 16 total sequencing analyses in batch 1 and batch 2 are distributed into *replicates*, *soft sediment* and *water column samplings* and *3 collection dates*, which results in overall limited time series of maximum 3 time-points, but sufices for demonstration purposes.

```bash
gecco -v run --genome XXX.fa
```

GECCO version 0.9.10, default parameters.

## Loading data and metadata

```{code-cell}
:label: import-load
:class: dropdown
import pandas as pd
from momics.loader import bytes_to_df
import matplotlib.pyplot as plt
import networkx as nx

from momics.metadata import get_metadata, enhance_metadata, filter_metadata_table, filter_data

def bgc_tables_dict(tsv_names: list):
    """
    Combine multiple BGC tables into a single DataFrame.

    Args:
        tvs_files (list): List of file paths to the TVS files.

    Returns:
        pd.DataFrame: Combined DataFrame with all BGC data.
    """
    tables_dict = {}
    for name in tsv_names:
        try:
            url = f"https://raw.githubusercontent.com/fair-ease/doc-jupyterbook-mgo/refs/heads/main/book/assets/data/gecco_clusters/{name}_final.contigs.clusters.tsv"
            df = pd.read_csv(url, sep="\t", header=0, index_col=0)
            tables_dict[name] = df
        except Exception as e:
            print(f"Error reading file {name}: {e}")
            continue
    return tables_dict


# TODO: I need to add metadata somehow
## method to merge tracker and shipments data
def merge_tracker_metadata(df_tracker):
    BATCH1_RUN_INFO_PATH = (
        "https://raw.githubusercontent.com/emo-bon/sequencing-data/main/shipment/"
        "batch-001/run-information-batch-001.csv"
    )
    BATCH2_RUN_INFO_PATH = (
        "https://raw.githubusercontent.com/emo-bon/sequencing-data/main/shipment/"
        "batch-002/run-information-batch-002.csv"
    )
    df = pd.read_csv(BATCH1_RUN_INFO_PATH)
    df1 = pd.read_csv(BATCH2_RUN_INFO_PATH)
    df = pd.concat([df, df1])
    print(len(df))

    # select only batch 1 and 2 from tracker data
    df_tracker = df_tracker[df_tracker['batch'].isin(['001', '002'])]

    # merge with tracker data on ref_code
    df = pd.merge(df, df_tracker, on='ref_code', how='inner')

    # split the sequenced tables
    df_discarded = df[df['lib_reads_seqd'].isnull()]
    df1 = df[~df['lib_reads_seqd'].isnull()]

    # deliver only filters and sediment samples, no blanks
    df_to_deliver = df1[df1['sample_type'].isin(['filters', 'sediment'])].reset_index(drop=True)
    #drop columns
    df_to_deliver.drop(columns='reads_name_y', inplace=True)
    df_to_deliver.rename(columns={'reads_name_x': 'reads_name'}, inplace=True)
    return df_to_deliver, df_discarded

def combine_metadata():
    url_metadata = "https://raw.githubusercontent.com/emo-bon/emo-bon-data-validation/refs/heads/main/validated-data/Batch1and2_combined_logsheets_2024-11-12.csv"
    url_tracker = "https://raw.githubusercontent.com/emo-bon/momics-demos/refs/heads/main/wf0_landing_page/emobon_sequencing_master.csv"

    df_metadata = pd.read_csv(url_metadata ,index_col=0)
    df_tracker = pd.read_csv(url_tracker ,index_col=0)
    df_to_deliver, _ = merge_tracker_metadata(df_tracker)
    assert len(df_to_deliver) == 181, "Number of samples in the metadata is not correct"

    mapper = df_to_deliver[['ref_code', 'source_mat_id', 'reads_name']]
    mapper['reads_name_short'] = mapper['reads_name'].str.split('_').str[-1]

    df_full = mapper.merge(df_metadata, on='ref_code', how='inner')
    assert len(df_full) == 181, "Number of samples in the metadata is not correct"
    return df_full

df_metadata = combine_metadata()

## validation DF
url_valid = "https://raw.githubusercontent.com/emo-bon/momics-demos/refs/heads/main/data/shipment_b1b2_181.csv"
df_valid = pd.read_csv(url_valid)

## enhance metadata
df_metadata = enhance_metadata(df_metadata, df_valid)
```


Batch 1+2 contain 181 valid samples, which should be the first value. The second value is number of metadata columns available for each samplling. Note that not all are obligatory, therefore the table contains many missing values.

```{code-cell}
assert df_metadata.shape[0] == 181

print(df_metadata.shape)
```

Here I hardcode list of names for which GECCO was run, plus a color hash for the BGC coloring. Note that BGCs are colored, domains will be in grey, which are inherently different nodes. Each cluster is composed from 1 to many nodes, which can be shared between the BGCs and therefore I use them as nodes to connect the BGCs with edges.

```{code-cell}
data_list = [
    "HCFCYDSX5.UDI129", 
    "HVWGWDSX5.UDI102",
    "HCFCYDSX5.UDI130",
    "HVWGWDSX5.UDI103",
    "HCFCYDSX5.UDI131",
    "HVWGWDSX5.UDI115",
    "HCFCYDSX5.UDI132",
    "HVWGWDSX5.UDI127",
    "HMNJKDSX3.UDI234",
    "HVWGWDSX5.UDI150",
    "HMNJKDSX3.UDI236",
    "HVWGWDSX5.UDI162",
    "HMNJKDSX3.UDI246",
    "HVWGWDSX5.UDI174",
    "HMNJKDSX3.UDI250",
    "HVWGWDSX5.UDI186",
]

color_hash = {
    'NRP': 'red',
    'PKS': 'blue',
    'RiPPs': 'darkgreen',
    'Terpene': 'brown',
    'Unknown': 'black',
    'Polyketide': 'purple',
    'NRP;Polyketide': 'orange',
    'RiPP': 'darkblue',
    'Saccharide': 'darkred',
    'domain': 'lightgrey',
}

tables = bgc_tables_dict(data_list)
```

Below are methods I use to construct the network using `networkx` package.

```{code-cell}
:class: dropdown

def graph_nodes_edges(df, color_hash):
    nodes = []
    for i, row in df.iterrows():
        nodes.append(
            (
                row['cluster_id'],
                {'type': row['type'],
                'color': color_hash[row['type']],
                }
            ),
        )
    print(f"Number of nodes: {len(nodes)}")

    nodes_domains = []
    already_seen = set()
    for i, row in df.iterrows():
        domains = row['domains'].strip().split(';')
        for domain in domains:
            if domain not in already_seen:
                already_seen.add(domain)
                nodes_domains.append(
                    (
                        domain,
                        {'type': "domain_node",
                        'color': "grey",
                        }
                    ),
                )
            else:
                pass 

    assert len(nodes_domains) == len(already_seen), f"Number of nodes is not correct, {len(nodes_domains)} != {len(already_seen)}"
    print(f"Number of nodes from domains: {len(nodes_domains)}")

    edges = []

    for i, row in df.iterrows():
        lst_domains = list(set(row['domains'].strip().split(';')))
        assert len(lst_domains) == len(set(lst_domains)), f"Number of domains is not correct, {len(lst_domains)} != {len(set(lst_domains))}"
        for j in range(len(lst_domains)):
            # connect cluster ids to domains
            edges.append((row['cluster_id'], lst_domains[j]))

    print(f"Number of edges: {len(edges)}")
    return nodes, nodes_domains, edges

def generate_graph(nodes, nodes_domains, edges, collection_date):
    import networkx as nx
    G = nx.Graph(
        date = collection_date,
    )

    G.add_nodes_from(nodes)
    G.add_nodes_from(nodes_domains)
    G.add_edges_from(edges)

    print(f"Number of nodes: {G.number_of_nodes()}")
    print(f"Number of edges: {G.number_of_edges()}")
    return G


def plot_graph(G, color_hash):
    colors = [k[1]['color'] for k in G.nodes(data=True)]

    # drawing nodes and edges separately so we can capture collection for colobar
    pos = nx.spring_layout(G, k=0.2)
    # pos = nx.kamada_kawai_layout(G)
    # pos = nx.spiral_layout(G)
    ec = nx.draw_networkx_edges(G, pos, alpha=0.2)
    nc = nx.draw_networkx_nodes(G, pos, nodelist=G.nodes, node_color=colors,
                                node_size=15,
                                alpha=0.5,
                                cmap=plt.cm.jet)
    # plt.colorbar(color_hash)
    plt.axis('off')
    plt.legend(
        handles=[plt.Line2D([0], [0], marker='o', color='w', label=k, markerfacecolor=v)
                for k, v in color_hash.items()],
        loc='upper left',
        bbox_to_anchor=(1, 1),
        title="BGC type",
    )
    plt.title(f"Sample info: {G.graph['date']}")
    plt.show()

from collections import Counter
def count_multiple_edges(edges):
    """
    Count appearances of the second position in the edge tuple and filter those with more than one occurrence.

    Args:
        edges (list): List of edge tuples.

    Returns:
        tuple: A tuple containing:
            - cnt_full (Counter): Full count of appearances.
            - cnt_multiple (dict): Filtered counts with more than one occurrence.
    """
    edge_counter = [e[1] for e in edges]
    cnt_full = Counter(edge_counter)

    # Filter those which have more than 1
    cnt_multiple = {k: v for k, v in cnt_full.items() if v > 1}
    cnt_multiple = dict(sorted(cnt_multiple.items(), key=lambda item: item[1], reverse=True))

    return cnt_full, cnt_multiple


def plot_domain_edges_counts(counts, title: str = "Domain counts"):
    # barplot
    plt.figure(figsize=(10, 5))
    plt.bar(counts.keys(), counts.values())
    plt.xticks(rotation=90)
    plt.xlabel('Domain')
    plt.ylabel('Count')
    plt.title('Domain Counts')
    plt.tight_layout()
    plt.title(title, )
    plt.show()


def create_graph_id(df_metadata: pd.DataFrame, name: str):
    graph_id = df_metadata[df_metadata['reads_name_short'] == name]['replicate_info'].values.tolist()[0]
    return graph_id
```

Example of a resulting graph can look like this one

```{code-cell}
# over all
nodes, nodes_domains, edges = graph_nodes_edges(df, color_hash)

# contitutes date nad replicate number to make it unique
graph_id = create_graph_id(df_metadata, table_names[0])
G = generate_graph(nodes, nodes_domains, edges, graph_id)
plot_graph(G, color_hash)
```

