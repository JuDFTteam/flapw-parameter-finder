# FLAPW Parameter finder app

Use this app to browse interactive visualizations of FLAPW sets generated for the atomic structure set form the [Open Quantum Materials Database (OQMD)](http://www.oqmd.org/). The set represents the default choice of the FLEUR input generator (Version MAX1, 2018) with close to touching Muffin-tin radii (which may or may not be resonable). Feel free to use this parameter set to choose resonable FLAPW parameters for your calculations, especially for HTC runs.

## Features

 * interactive scatter plots via [bokeh server](https://bokeh.pydata.org/en/1.0.4/)
 * interactive structure visualization via [jsmol](https://chemapps.stolaf.edu/jmol/docs/)
 * simple input: provide CIF/XYZ files with structures and CSV file with their properties
 * simple deployment on [materialscloud.org](https://www.materialscloud.org/discover/menu) through [Docker containers](http://docker.com)
 * driven by database backend:
   1. [sqlite](https://www.sqlite.org/index.html) database (default)


## Getting started

### Prerequisites

 * [git](https://git-scm.com/)
 * [python](https://www.python.org/)
 * [nodejs](https://nodejs.org/en/) >= 6

### Installation

```
git clone https://github.com/JuDFTteam/FLAPW_parameter_finder.git
cd FLAPW_parameter_finder
pip install -e .     # install python dependencies
./prepare.sh         # download test data (run only once)
```

### Running the app

```
bokeh serve --show figure detail select-figure   # run app
```

## Customizing the app

### Input data
 * a set of structures in `data/structures`
   * Allowed file extensions: `cif`, `xyz`
 * a CSV file `data/properties.csv` with their properties
   * has a column `name` whose value `<name>` links each row to a file in `structures/<name>.<extension>`.
 * adapt `import_db.py` accordingly and run it to create the database

### Plots

The plots can be configured using a few YAML files in `figure/static`:
 * `columns.yml`: defines metadata for columns of CSV file
 * `filters.yml`: defines filters available in plot
 * `presets.yml`: defines presets for axis + filter settings

## Docker deployment

```
pip install -e .
./prepare.sh
docker-compose build
docker-compose up
# open http://localhost:3245/cofs/select-figure
```
