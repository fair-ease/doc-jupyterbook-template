# FAIRE-EASE Jupyterbook on Marine Omics pilot

Go directly to the deployed [book](https://lab.fairease.eu/doc-jupyterbook-mgo/).

## Install the project

```bash
# install jupyterbook
pip install -r requirements.txt

# install libraries needed to execute your code  
pip install -r .binder/requirements.txt
```

## How to use

Run a local server:

```bash
cd book/

# preferrably use mystd, since it is used for deployment.
mystd start --execute

# using jupyter
jupyter book start --execute
```
