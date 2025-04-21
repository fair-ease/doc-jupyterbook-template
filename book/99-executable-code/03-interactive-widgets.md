---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: '0.8'
    jupytext_version: 1.4.1+dev
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Interactive Widgets

## Leaflet

Including Jupyter Widgets within a Quarto document is as easy as including a plot. For example, here is how we embed a Leaflet map:

```{code-cell}
from ipyleaflet import Map, Marker

center = (48.866667, 2.333333)
map = Map(center=center, zoom=12)

# Add a draggable marker to the map
# Dragging the marker updates the marker.location value in Python
marker = Marker(location=center, draggable=True)
map.add_control(marker)

display(map)
```

## Plotly

Plotly is an interactive graphics library that can also be used with the Jupyter engine. Here’s an example of using Plotly:

```{code-cell}
import plotly.express as px
df = px.data.election()
fig = px.scatter_3d(df, x="Joly", y="Coderre", z="Bergeron", color="winner", size="total", hover_name="district",symbol="result", color_discrete_map = {"Joly": "blue", "Bergeron": "green", "Coderre":"red"})

fig.show()
```