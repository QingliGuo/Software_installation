# Installation instructions
This repo will record instructions for software installation.
## 1. [Octopus](https://github.com/luntergroup/octopus)
The installation is supported by Ben Talbot.

The following commands would help to install Octopus_0.6.3 on Apocrita:

```
module load anaconda3/2020.02
conda create --name oct-env
conda activate oct-env
conda install -c conda-forge -c bioconda octopus
```

To install older version Octopus_0.5.2 on Apocrita:

```
module load anaconda3/2020.02
conda create --name oct-env
conda activate oct-env
conda install libboost=1.67.0
conda install octopus
```

To install older version Octopus_0.5.2 on UCL COLCC:

```
## open an interactive node for installation as it takes quite long time:
qrsh -l tmem=10G, h_rt=01:00:0
## source miniconda from /shared/apps/ folder
source /share/apps/miniconda3/etc/profile.d/conda.sh

## then install octopus as what we did before

conda create --name oct-env
conda activate oct-env
conda install libboost=1.67.0
conda install octopus
```
In UCL COLCC, the installed package is in ~/.conda/envs/oct-env/bin/octopus

## 2. [SigProfilerMatrixGenerator](https://github.com/AlexandrovLab/SigProfilerMatrixGenerator)

The package installed using pip3.8 on UCL COLCC:

```
## open an interactive node for installation as it takes quite long time:
qrsh -l tmem=10G, h_rt=01:00:0

## source a new python3 version, I used 3.8
source /share/apps/source_files/python/python-3.8.5.source

pip3.8 install SigProfilerMatrixGenerator --user

## after installatin using pip3.8, open python3.8 to install reference genome from the command line
python3.8
>>> from SigProfilerMatrixGenerator import install as genInstall
>>> genInstall.install('GRCh37', rsync=False, bash=True)
## when this is done, quit the session
>>> quit()
```
