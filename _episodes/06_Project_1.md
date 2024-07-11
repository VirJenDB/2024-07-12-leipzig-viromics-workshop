---
title: "Practical session part 1"
teaching: 
exercises: 30
questions:
- "What are the data sources in viromics"
objectives:
- "Exploring viromics resources and files"
keypoints:
- "Seqtk"
- "fastqc"
- "Fastp"
---

## 1. Exploring Viromics Resources and Files
### Tools: Seqtk, FastQC, Fastp

### Step 1: Download viromes and generate a summary report

```bash
# Example command to download a virome dataset
wget -O virome_dataset.fastq.gz [URL]

# Unzip the downloaded dataset
gunzip virome_dataset.fastq.gz
```

### Step 2: Perform quality control using Fastp
[Fastp](https://github.com/OpenGene/fastp?tab=readme-ov-file) is a fast all-in-one preprocessing tool for FASTQ files. Install the tool from [download page](https://github.com/OpenGene/fastp?tab=readme-ov-file#or-download-the-latest-prebuilt-binary-for-linux-users).

**Usage:**

```bash
# Perform quality control on the input FASTQ file
fastp -i input.fastq -o cleaned_output.fastq -h report.html -j report.json
```

Fastp not only performs quality filtering but also removes adapters and low-quality reads, producing a cleaned dataset ready for downstream analysis.

### Step 3: Assess the quality of the sequencing data using FastQC
[FastQC](https://github.com/s-andrews/FastQC) provides a simple way to perform quality control checks on raw sequence data. Check the [download](https://www.bioinformatics.babraham.ac.uk/projects/download.html#fastqc) page to download and install it.

**Usage:**

```bash
# Run FastQC on the input FASTQ file
fastqc input.fastq -o output_directory
```

FastQC generates a detailed report on the quality of the sequencing data, including information on read length distribution, GC content, and the presence of adapters, which helps in identifying any potential issues before further analysis.

### Step 4: Create small files for use in the next steps using Seqtk
Seqtk is a fast and lightweight tool for processing sequences in the FASTA/FASTQ format. Check the github page of [Seqtk](https://github.com/lh3/seqtk) to install of the tool.

**Usage:**

```bash
# Extract the first 1000 reads from a FASTQ file
seqtk sample -s100 input.fastq 1000 > subset.fastq
```

In this step, we use Seqtk to create a smaller subset of the data for initial exploration, which helps in quickly assessing the quality and content of the dataset without processing the entire file.

{% include links.md %}
