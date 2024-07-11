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
---

## 2. Taxonomic Profiling of One Virome
### Tools: Kraken2

### Perform taxonomic profiling using Kraken2
[Kraken2](https://ccb.jhu.edu/software/kraken2/) is a system for assigning taxonomic labels to short DNA sequences. [nf-core/taxprofiler](https://nf-co.re/taxprofiler/1.0.1/) is a bioinformatics best-practice analysis pipeline for taxonomic classification and profiling of shotgun metagenomic data. It allows for in-parallel taxonomic identification of reads or taxonomic abundance estimation with multiple classification and profiling tools against multiple databases and produces standardized output tables. 

### Step 1: Installation

**Method 1:**
Install [Nextflow](https://www.nextflow.io/docs/latest/install.html#installation) from the  (>=22.10.1).

**Method 2: (recommended)**
Install [Docker Engine](https://docs.docker.com/engine/install/) using docker.

```
curl -s https://get.nextflow.io | bash
sudo mv nextflow /usr/local/bin/
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
conda activate workshop_nextflow`
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

execution of the pipeline required multiple input files including samplesheet.csv and database.csv files.
```
# Create samplesheet.csv by listing the fastq files processed by fastp
echo "sample,fastq_1,fastq_2" > samplesheet.csv && for f in fastp_output/*_1.fastq.gz; do base=$(basename $f _1.fastq.gz); echo "$base,fastp_output/${base}_1.fastq.gz,fastp_output/${base}_2.fastq.gz"; done >> samplesheet.csv
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
nextflow run nf-core/taxprofiler --input samplesheet.csv --databases database.csv --outdir <OUTDIR> --run_<TOOL1> --run_<TOOL1> -profile <docker/singularity/podman/shifter/charliecloud/conda/institute>

```

This pipeline automates the process, running Kraken2 and other tools as part of a streamlined workflow.

> ## prerequisites
> To successfully download the required files, you need to have either `wget` or `curl` installed on your system. These tools are essential for fetching files from the internet.
>
> **Using `wget`:**
> `wget` is a command-line utility for downloading files from the web. It supports HTTP, HTTPS, and FTP protocols.
> - **Installation:**
>   - **Linux (Debian/Ubuntu):**
>   ```sh
>   sudo apt-get install wget
>   ```
> Install Docker Engine on Ubuntu (Sudo privilege is required)
> Update the Package Index
> `sudo apt-get update`
> Install Required Packages
> `sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release`
> Add Docker’s Official GPG Key
> `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`
> Set Up the Repository
> `echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`
> Update the Package Index Again
> `sudo apt-get update`
> Install the latest version of Docker Engine and containerd.io:
> `sudo apt-get install docker-ce docker-ce-cli containerd.io`
> Verify Docker Installation
> `sudo docker run hello-world`

{% include links.md %}
