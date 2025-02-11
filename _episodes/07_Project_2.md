---
title: "Quality control and taxonomic profiling"
teaching: 
exercises: 30
questions:
- "Quality control and taxonomic profiling of one virome"
objectives:
- "Install Fastp, kraken2 and use them"
keypoints:
- "Fastp, kraken2 using nf-core:taxprofiler"
tips:
- yeseri tip
---

## 2. Taxonomic Profiling of One Virome
### Tools: Kraken2

### Perform taxonomic profiling using Kraken2
[Kraken2](https://ccb.jhu.edu/software/kraken2/) is a system for assigning taxonomic labels to short DNA sequences. [nf-core/taxprofiler](https://nf-co.re/taxprofiler/1.0.1/) is a bioinformatics best-practice analysis pipeline for taxonomic classification and profiling of shotgun metagenomic data. It allows for in-parallel taxonomic identification of reads or taxonomic abundance estimation with multiple classification and profiling tools against multiple databases and produces standardized output tables. 

### Step 1: Installation

**Method 1:**
Install [Nextflow](https://www.nextflow.io/docs/latest/install.html#installation) from the  (>=22.10.1).

**Method 2: (recommended)**
Install nextflow using [Docker Engine](https://docs.docker.com/engine/install/). The Docker engine installation procedure is described at the end of the page.

```
# Install Java as a dependency 
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java 11.0.11.hs-adpt

curl -s https://get.nextflow.io | bash
mv nextflow /usr/local/bin/
```

If your user is not a sudoer, try a users local bin folder and add it to the PATH variable
```
# Create ~/bin Directory if It Does Not Exist
mkdir -p ~/bin

# Move the Nextflow Executable to ~/bin
mv nextflow ~/bin/

# Add ~/bin to Your PATH
export PATH=$HOME/bin:$PATH

# Then, reload your shell configuration:
source ~/.bashrc
```

Test the installation of Nextflow using `nextflow -version`

**Method 3:**
Create a new conda environment and install nextflow:
```
conda create -n workshop_nextflow -c bioconda nextflow 
conda activate workshop_nextflow
```

For other installation methods, please check [nf-core website](https://nf-co.re/taxprofiler/1.0.1/)

### Step 2: Download taxprofiler pipeline
Download taxprofiler pipeline and test it on a minimal dataset with a single command:

In the following command, the name of the method used for the installation has been used as the "Profile" name. The profile name could be one of the docker, singularity, podman, shifter, charliecloud, and conda which instruct the pipeline to use the named tool for software management. For example if you used conda, ` -profile test,conda ` is the correct term.
```bash
# Update nextflow to make sure it is the latest version if it is needed
nextflow self-update

# return to workshop_day5 folder
cd workshop_day5

# Chain multiple config profiles in a comma-separated string
nextflow run nf-core/taxprofiler -profile test,YOURPROFILE --outdir nextflow
```

### Step 3: Run the nf-core:taxprofiler pipeline

execution of the pipeline required [multiple input files](https://nf-co.re/taxprofiler/1.0.1/docs/usage/) including samplesheet.csv and database.csv files.
```
# Create samplesheet.csv by listing the fastq files processed by fastp
echo "sample,run_accession,instrument_platform,fastq_1,fastq_2,fasta\nERR6797441,run1,ILLUMINA,PRJEB47625/ERR6797441_1.fastq.gz,PRJEB47625/ERR6797441_2.fastq.gz," > samplesheet.csv

echo -e "tool,db_name,db_path\nkraken2,kraken2,kraken2_db/kraken2_db/" > database.csv

```

---

## nf-core/taxprofiler Pipeline Parameters

| Parameter               | Description                                                                                   |
|-------------------------|-----------------------------------------------------------------------------------------------|
| `--input` `samplesheet.csv` | Specifies the CSV file with your sample information.                                         |
| `--databases` `database.csv` | Specifies the CSV file with the list of databases.                                           |
| `--outdir` `<OUTDIR>`   | The directory where the output files will be saved.                                           |
| `--run_<TOOL1>`         | Include any specific tools or modules you want to run. Replace `<TOOL1>` with the actual tool names (e.g., `--run_blast`). |
| `--run_<TOOL2>`         | Optionally include additional tools or modules.                                               |
| `-profile` `<profile>`  | Specifies the execution profile (e.g., `docker`, `singularity`, `conda`, etc.).              |

```


# Run the nf-core:taxprofiler pipeline
nextflow run nf-core/taxprofiler --input samplesheet.csv --databases database.csv --outdir nextflow_output -profile docker
```

This pipeline automates the process, running Kraken2 and other tools as part of a streamlined workflow.

after the completion of the pipeline execution, the nextflow_output folder will contain fastqc, multiqc, and pipeline_info folders. 

---

### Install Docker Engine on Ubuntu if it is needed (Sudo privilege is required)
```
#Update the Package Index
sudo apt-get update

# Install Required Packages
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release

# Add Docker’s Official GPG Key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Set Up the Repository
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update the Package Index Again
sudo apt-get update

# Install the latest version of Docker Engine and containerd.io:
sudo apt-get install docker-ce docker-ce-cli containerd.io

#Verify Docker Installation
sudo docker run hello-world
```

### Create a Kraken2 Database
```
# Get back to the workshop folder
cd workshop_day5

# Download and install Kraken2
wget https://github.com/DerrickWood/kraken2/archive/v2.1.2.tar.gz
tar -xvzf v2.1.2.tar.gz
cd kraken2-2.1.2
./install_kraken2.sh .
export PATH=$PATH:$PWD
cd .. && rm v2.1.2.tar.gz

# Create a directory for the database
mkdir -p kraken2_db
cd kraken2_db

# Download RefSeq viruses as a kraken2 database
kraken2-build --download-library viral --db kraken2_db

```

### Install with conda directly
```
conda install bioconda::kraken2
kraken2-build --download-taxonomy --db kraken2_db
kraken2-build --download-library viral --db kraken2_db
```

### download the ready kraken database for viruses
```
wget  -c "https://genome-idx.s3.amazonaws.com/kraken/k2_viral_20240605.tar.gz"
mkdir kraken_db
tar -xvzf k2_viral_20240605.tar.gz -C kraken_db
```

{% include links.md %}
