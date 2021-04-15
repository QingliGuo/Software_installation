# Software_installation
This repo will record instructions for software installation on the current cluster (Apocrita, QMUL)I am working on.
## Octopus
The installation is supported by Ben Talbot.

+ Version 0.6.3

The following commands would help to install Octopus_0.6.3:

```
module load anaconda3/2020.02
conda create --name oct-env
conda activate oct-env
conda install -c conda-forge -c bioconda octopus
```

+ Version 0.5.2

To install older version Octopus_0.5.2:

```
module load anaconda3/2020.02
conda create --name oct-env
conda activate oct-env
conda install libboost=1.67.0
conda install octopus
```