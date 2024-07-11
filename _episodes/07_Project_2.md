---
title: "Quality control and taxonomic profiling"
teaching: 
exercises: 30
questions:
- "Quality control and taxonomic profiling of one virome"
objectives:
- "Install Fastp, kraken2 and use them"
keypoints:
- "Fastp, kraken2 using nf-core:taxoprofiler"
---

## 2. Taxonomic Profiling of One Virome
### Tools: Kraken2

### Perform taxonomic profiling using Kraken2
[Kraken2](https://ccb.jhu.edu/software/kraken2/) is a system for assigning taxonomic labels to short DNA sequences. [nf-core/taxprofiler](https://nf-co.re/taxprofiler/1.0.1/) is a bioinformatics best-practice analysis pipeline for taxonomic classification and profiling of shotgun metagenomic data. It allows for in-parallel taxonomic identification of reads or taxonomic abundance estimation with multiple classification and profiling tools against multiple databases and produces standardized output tables. 

### Step 1: Installation

**Method 1:**
Install [Nextflow](https://www.nextflow.io/docs/latest/install.html#installation) from the  (>=22.10.1).

**Method 2:**
Install [Docker Engine](https://docs.docker.com/engine/install/) using docker.

**Method 3:**
Create a new conda environment and install nextflow:
```
conda create -n workshop_nextflow -c bioconda nextflow 
conda activate workshop_nextflow`
```

For other installation methods, please check [nf-core website](https://nf-co.re/taxprofiler/1.0.1/)

### Step 2: Download taxoprofiler pipeline
Download taxoprofiler pipeline and test it on a minimal dataset with a single command:

In the following command, the name of the method used for the installation has been used as the "Profile" name. The profile name could be one of the docker, singularity, podman, shifter, charliecloud, and conda which instruct the pipeline to use the named tool for software management. For example if you used conda, ` -profile test,conda ` is the correct term.
```bash
# Update nextflow to make sure it is the latest version
nextflow self-update

# Chain multiple config profiles in a comma-separated string
nextflow run nf-core/taxprofiler -profile test,YOURPROFILE --outdir <OUTDIR>
```

### Step 3: Run the nf-core:taxoprofiler pipeline

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
# Run the nf-core:taxoprofiler pipeline
nextflow run nf-core/taxprofiler --input samplesheet.csv --databases database.csv --outdir <OUTDIR> --run_<TOOL1> --run_<TOOL1> -profile <docker/singularity/podman/shifter/charliecloud/conda/institute>

```

This pipeline automates the process, running Kraken2 and other tools as part of a streamlined workflow.

{% include links.md %}
