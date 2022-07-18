![](docs/_include/images/aviary_logo.png)

# Aviary
An easy to use for wrapper for a robust snakemake pipeline for metagenomic hybrid assembly, binning, and annotation. 
The pipeline currently includes a step-down iterative 
hybrid assembler, an isolate hybrid assembler, a quality control module and a 
comprehensive binning pipeline. Each module can be run independently or as a single pipeline depending on provided input.

[Please refer to the full docs here](https://rhysnewell.github.io/aviary)

# Quick Installation

Your conda channels should be configured ideally in this order with strict channel priority order
turned on:
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```

Your resulting `.condarc` file should look something like:
```
channels:
  - conda-forge
  - bioconda
  - defaults
channel_priority: strict
```

Initial requirements for aviary can be downloaded using the `aviary.yml`:
```
git clone https://github.com/rhysnewell/aviary.git
cd aviary
conda env create -n aviary -f aviary.yml
conda activate aviary
pip install .
aviary --help
```

The resulting output should contain a list of the available aviary modules:
```
                    ......:::::: AVIARY ::::::......

           A comprehensive metagenomics bioinformatics pipeline

Metagenome assembly, binning, and annotation:
        assemble  - Perform hybrid assembly using short and long reads, 
                    or assembly using only short reads
        recover   - Recover MAGs from provided assembly using a variety 
                    of binning algorithms 
        annotate  - Annotate MAGs using EggNOG and GTBD-tk
        genotype  - Perform strain diversity analysis of MAGs using Lorikeet
        complete  - Runs each stage of the pipeline: assemble, recover, 
                    annotate, genotype in that order.
        cluster   - Combines and dereplicates the MAGs from multiple Aviary runs
                    using Galah

Isolate assembly, binning, and annotation:
        isolate   - Perform isolate assembly **PARTIALLY COMPLETED**
        
Utility modules:
        configure - Set or overwrite the environment variables for future runs.

```

Upon first running aviary you will be prompted to input the location for where you would like
your conda environments to be stored, the GTDB release installed on your system, the location of your
EnrichM database, and the location of your BUSCO database. These locations will be stored as environment
variables, but for aviary to be able to use those environment variables you will have to either source your .bashrc
or reactivate your conda environment depending on whether you installed aviary within a conda environment or not:

```
conda deactivate; conda activate aviary

OR

source ~/.bashrc
```

These environment variables can be reset using `aviary configure`

## Requirements

Your conda channels should be configured ideally in this order with strict channel priority order
turned on:
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```

Your resulting `.condarc` file should look something like:
```
channels:
  - conda-forge
  - bioconda
  - defaults
channel_priority: strict
```

Initial requirements for aviary can be downloaded using the `aviary.yml`:
```
conda env create -n aviary -f aviary.yml
```

## Databases

Aviary uses programs which require access to locally stored databases. These databases can be quite large, as such we recommend setting up one instance of Aviary and these databases per machine or machine cluster.

The **required** databases are as follows:
* [GTDB](https://gtdb.ecogenomic.org/downloads) Required for taxonomic annotation

The **optional** databases are as follows:
* [EggNog](https://github.com/eggnogdb/eggnog-mapper/wiki/eggNOG-mapper-v2.1.5-to-v2.1.7#setup).

**If you do not have the optional databases installed, then when aviary asks you to specify these database when configuring just press enter and specify no path.**

### Environment variables

Upon first running Aviary, you will be prompted to input the location for several database folders if
they haven't already been provided. If at any point the location of these folders change you can
use the the `aviary configure` module to update the environment variables used by aviary.

These environment variables can also be configured manually, just set the following variables in your `.bashrc` file:
```
export GTDBTK_DATA_PATH=/path/to/gtdb/gtdb_release207/db/ # https://gtdb.ecogenomic.org/downloads
export EGGNOG_DATA_DIR=/path/to/eggnog-mapper/2.1.7/ # https://github.com/eggnogdb/eggnog-mapper/wiki/eggNOG-mapper-v2.1.5-to-v2.1.7#setup
export CONDA_ENV_PATH=/path/to/conda/envs/
```

# Workflow
The current complete workflow for aviary. This is constantly being updated and will eventually include and assembly stage and
post binning analysis of MAGs
![Aviary workflow](figures/aviary_workflow.png)


# Citations
If you use aviary then please be aware that you are using a great number of other programs and aviary wrapping around them.
You should cite all of these tools as well, or whichever tools you know that you are using. To make this easy for you
we have provided the following list of citations for you to use in alphabetical order. This list will be updated as new
modules are added to aviary.

A constantly updating list of citations can be found in the [Citations document](https://rhysnewell.github.io/aviary/citations).

# License

Code is [GPL-3.0](LICENSE)
