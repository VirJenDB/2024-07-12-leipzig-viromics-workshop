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

### Create abundance_counts file
```
# Index the contig file (conda install bioconda::bwa)
bwa index PRJEB47625/illumina_sample_01_megahit.fa.gz

# Align reads to contigs
bwa mem PRJEB47625/illumina_sample_01_megahit.fa.gz PRJEB47625/ERR6797441_1.fastq.gz PRJEB47625/ERR6797441_2.fastq.gz > aligned_reads.sam

# Convert SAM to BAM (conda install bioconda::samtools)
samtools view -bS aligned_reads.sam > aligned_reads.bam

# Sort BAM file
samtools sort aligned_reads.bam -o sorted_reads.bam

# Index BAM file
samtools index sorted_reads.bam

bedtools bamtobed -i sorted_reads.bam > intervals.bed

# Count reads mapped to each contig (conda install bioconda::bedtools)
bedtools coverage -a intervals.bed -b sorted_reads.bam > abundance_counts.txt
```

## 3. Bin virus genomes
### Tools: MaxBin2, CheckV

In this section, we start with the [assembled contig file](https://zenodo.org/records/10650983) belonging to the same [project](https://www.biorxiv.org/content/10.1101/2023.11.24.568560v1) to save time and focus on binning and evaluation. By starting with a pre-assembled contig file, you streamline the process and focus on binning and quality evaluation, ensuring efficient and effective analysis of your viromics data.

### Step 1: Bin virus genomes from the assembly file using MaxBin2
[MaxBin2](https://kbase.us/applist/apps/kb_maxbin/run_maxbin2/release) is a tool designed to bin metagenomic contigs into individual genomes, including viral genomes. Follow [website](https://github.com/assemblerflow/flowcraft/blob/master/docs/user/components/maxbin2.rst) instructions or use `conda install bioconda::maxbin2` to install maxbin2 via conda.

**Usage:**

```bash
cd workshop_day5
wget -c https://zenodo.org/records/10650983/files/illumina_sample_01_megahit.fa.gz -O PRJEB47625/illumina_sample_01_megahit.fa.gz

# Run MaxBin2 for binning
run_MaxBin.pl -contig PRJEB47625/illumina_sample_01_megahit.fa.gz -out bins_directory
```

MaxBin2 will generate bins of contigs, each representing a putative genome, including viral genomes.

### Step 2: Evaluate bins using CheckV
[CheckV](https://bitbucket.org/berkeleylab/checkv/src/master/) is used to assess the quality of viral genomes from metagenomic assemblies. Conda installation command is `conda install bioconda::checkv`
**Usage:**

```bash
# Run CheckV on the binned data
checkv end_to_end bins_directory checkv_output -t 4
```

CheckV evaluates the completeness and contamination of viral bins, providing quality metrics that help in refining and validating your viral genomes.

{% include links.md %}
