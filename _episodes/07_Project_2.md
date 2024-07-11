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

## 2. Quality Control and Taxonomic Profiling of One Virome
### Tools: Fastp, Kraken2

### Step 1: Perform quality control using Fastp
[Fastp](https://github.com/OpenGene/fastp?tab=readme-ov-file) is a fast all-in-one preprocessing tool for FASTQ files. Install the tool from [download page](https://github.com/OpenGene/fastp?tab=readme-ov-file#or-download-the-latest-prebuilt-binary-for-linux-users).

**Usage:**

```bash
# Perform quality control on the input FASTQ file
fastp -i input.fastq -o cleaned_output.fastq -h report.html -j report.json
```

Fastp not only performs quality filtering but also removes adapters and low-quality reads, producing a cleaned dataset ready for downstream analysis.

### Perform taxonomic profiling using Kraken2
[Kraken2]() is a system for assigning taxonomic labels to short DNA sequences. [nf-core/taxprofiler](https://nf-co.re/taxprofiler/1.0.1/) is a bioinformatics best-practice analysis pipeline for taxonomic classification and profiling of shotgun metagenomic data. It allows for in-parallel taxonomic identification of reads or taxonomic abundance estimation with multiple classification and profiling tools against multiple databases, produces standardised output tables. 


**Usage:**

Install [Nextflow](https://www.nextflow.io/docs/latest/install.html#installation) (>=22.10.1).

Install [Docker Engine](https://docs.docker.com/engine/install/) 

Download the pipeline and test it on a minimal dataset with a single command:

```bash
# Chain multiple config profiles in a comma-separated string
nextflow run nf-core/taxprofiler -profile test,YOURPROFILE --outdir <OUTDIR>

# Run the nf-core:taxoprofiler pipeline
nextflow run nf-core/taxprofiler --input samplesheet.csv --databases database.csv --outdir <OUTDIR> --run_<TOOL1> --run_<TOOL1> -profile <docker/singularity/podman/shifter/charliecloud/conda/institute>

```

This pipeline automates the process, running Kraken2 and other tools as part of a streamlined workflow.

{% include links.md %}
