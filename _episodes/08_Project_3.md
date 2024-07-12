---
title: "Virome Assembly and Bin Evaluation"
teaching: 
exercises: 30
questions:
- "How to bin virus genomes from the assembly file"
- "How to evaluate binning results"
objectives:
- ""
keypoints:
- "MaxBin2, CheckV"
---

## 1. 
### Tools: MaxBin2, CheckV

In this section, we start with the [assembled contig file](https://zenodo.org/records/10650983) belonging to the same [project](https://www.biorxiv.org/content/10.1101/2023.11.24.568560v1) to save time and focus on binning and evaluation. By starting with a pre-assembled contig file, you streamline the process and focus on binning and quality evaluation, ensuring efficient and effective analysis of your viromics data.

### Step 1: Bin virus genomes from the assembly file using MaxBin2
[MaxBin2](https://kbase.us/applist/apps/kb_maxbin/run_maxbin2/release) is a tool designed to bin metagenomic contigs into individual genomes, including viral genomes.

**Usage:**

```bash
# Run MaxBin2 for binning
run_MaxBin.pl -contig assembly_output/contigs.fasta -out bins_directory
```

MaxBin2 will generate bins of contigs, each representing a putative genome, including viral genomes.

### Step 2: Evaluate bins using CheckV
[CheckV](https://bitbucket.org/berkeleylab/checkv/src/master/) is used to assess the quality of viral genomes from metagenomic assemblies.

**Usage:**

```bash
# Run CheckV on the binned data
checkv end_to_end bins_directory checkv_output -t 4
```

CheckV evaluates the completeness and contamination of viral bins, providing quality metrics that help in refining and validating your viral genomes.

{% include links.md %}
