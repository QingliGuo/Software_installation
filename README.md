# Installation instructions
This repo will record instructions for software installation either on Apocrita or UCL COLCC, or both.
## 1. [Octopus](https://github.com/luntergroup/octopus)
The installation is supported by Ben Talbot.

The following commands would help to install Octopus_0.6.3 on Apocrita:

```
module load anaconda3/2020.02
conda create --name oct-env
conda activate oct-env
conda install -c conda-forge -c bioconda octopus
```

To install older version Octopus_0.5.2 on Apocrita (seems not working anymore):

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
conda create --name oct-env
conda activate oct-env
conda install -c bioconda/label/cf201901 octopus
```

For a newer version [0.7.4](https://anaconda.org/bioconda/octopus) on COLCC:
```
source /share/apps/miniconda3/etc/profile.d/conda.sh
conda create --name oct-env-0.7.4
conda activate oct-env-0.7.4
conda install -c bioconda octopus
```

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
## 3. [ANNOVAR](https://annovar.openbioinformatics.org/en/latest/user-guide/download/)

The downloader need to sign via a form [here](https://www.openbioinformatics.org/annovar/annovar_download_form.php); and the download link will be sent via email by the author.

```
## login the cluster, make/find a folder where you want to store the data:
wget http:PATH-SENT-VIA-EMAIL/annovar.latest.tar.gz
tar -zxvf annovar.latest.tar.gz
```

Annovar is made of several perl scripts. So once uncompressed the file, we already have it. To use it to annotate or filter variants, we also need to download databases, e.g. the 1000genome data:

```
cd /PATH-TO-ANNOVAR/annovar
## -downdb "1000g2015aug" is the database+version we would like to download; humandb is a pre-exisiting folder which contains to-be-downloaded data; -buildver hg19 tells the script which version of genome you want to download

perl annotate_variation.pl -downdb 1000g2015aug humandb -buildver hg19

## e.g. to download gnomad30_genome for hg38
perl annotate_variation.pl -downdb -webfrom annovar -build hg38 gnomad30_genome humandb/
```
More database for Annovar can be found [here](https://annovar.openbioinformatics.org/en/latest/user-guide/download/)
## 4. [Samtools; htslib](http://www.htslib.org/download/)(1.2) and [bcftools](http://samtools.github.io/bcftools/howtos/install.html)1.2;

```
wget https://github.com/samtools/samtools/releases/download/1.12/samtools-1.12.tar.bz2
tar xjf samtools-1.12.tar.bz2
cd samtools-1.12
./configure --prefix=/where/to/install
make
make install
export PATH=/where/to/install/bin:$PATH  ## for samtools
```
Same installation methods for htslib.

For bcftools:
```
git clone --recurse-submodules git://github.com/samtools/htslib.git
git clone git://github.com/samtools/bcftools.git
cd bcftools
make
export BCFTOOLS_PLUGINS=/path/to/bcftools/plugins ## set enviromental variables; IMPORTANT!
```

# New MacOS set up

+ Change the repeating & deleting speed "System preferences" -> keybord -> select "FAST"
+ Change the terminal color setting
Add the following to ~/.bash_profile file, save and source it.
```
export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]\$ "
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad
alias ls='ls -GFh'
```

+ Homebrew on MacOS

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
```

+ Install Python
```
## python version manager
brew install pyenv

## 3.9.2 is my current version, could be any
pyenv install 3.9.2

## confirgure the enviromental file
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
pyenv local 3.9.2
brew install jupyter
```

+ Anaconda
```
brew install --cask anaconda
echo "export PATH=$PATH:/opt/homebrew/anaconda3/bin/" >> ~/.bash_profile
source ~/.bash_profile

## to install packages in certain environment (e.g. an environment called tf).
conda install -n tf lightgbm
```
