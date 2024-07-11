---
title: "Project Explanation"
teaching: 30
exercises: 
questions:
- ""
objectives:
- ""

---

### Hands-on Workshop: Viromics
Description

Metagenomics

The emergence of Next Generation Sequencing (NGS) has facilitated the development of metagenomics. In metagenomic studies, DNA from all the organisms in a mixed sample is sequenced in a massively parallel way (or RNA in case of metatranscriptomics). The goal of these studies is usually to identify certain microbes in a sample, or to taxonomically or functionally characterize a microbial community. There are different ways to process and analyze metagenomes, such as the targeted amplification and sequencing of the 16S ribosomal RNA gene (amplicon sequencing, used for taxonomic profiling) or shotgun sequencing of the complete genomes in the sample.

After primary processing of the NGS data (which we will not perform in this exercise), a common approach is to compare the metagenomic sequencing reads to reference databases composed of genome sequences of known organisms. Sequence similarity indicates that the microbes in the sample are genomically related to the organisms in the database. By counting the sequencing reads that are related to certain taxa, or that encode certain functions, we can get an idea of the ecology and functioning of the sampled metagenome.

When the sample is composed mostly of viruses we talk of metaviromics. Viruses are the most abundant entities on earth and the majority of them are yet to be discovered. This means that the fraction of viruses that are described in the databases is a small representation of the actual viral diversity. Because of this, a high percentage of the sequencing data in metaviromic studies show no similarity with any sequence in the databases. We sometimes call this unknown, or at least uncharacterizable fraction as viral dark matter. As additional viruses are discovered and described and we expand our view of the Virosphere, we will increasingly be able to understand the role of viruses in microbial ecosystems. 

In this hands-on portion of the workshop, we will go through key steps in viromics.

## 0. Setup and choosing a dataset

Conda enables us to create multiple separate environments on our computer, where different programs can be installed without affecting our global virtual environment.

Why is this useful? Most of the time, tools rely on other programs to be able to run correctly - these programs are the tool's dependencies. For example: you cannot run a tool that is coded in Python 3 on a machine that only has Python 2 installed (or no Python at all!).

So, why not just install everything into one big global environment that can run everything? We will focus on two reasons: compatibility and findability. The issue with findability is that sometimes, a tool will not "find" its dependency even though it is installed. To reuse the Python example: If you try to run a tool that requires Python 2, but your global environment's default Python version is Python 3.7, then the tool will not run properly, even if Python 2 is technically installed. In that case, you would have to manually change the Python version anytime you decide to run a different tool, which is tedious and messy. The issue with compatibility is that some tools will just plain uninstall versions of programs or packages that are incompatible with them, and then reinstall the versions that work for them, thereby "breaking" another tool (this might or might not have happened during the preparation of this course ;) ). To summarize: keeping tools in separate conda environments will can save you a lot of pain.

## 1. Exploring Viromes
### Tools: Seqtk, FastQC

- **Seqtk**: Extract subsets of your data.
- **FastQC**: Generate summary reports.

Choose a dataset and explore it.

Describe fastq and fasta file formats
- What information is contained in sequencing files?
- How many sequences are in your files?
Print the first 10 and last 10 lines of your files in terminal
- Describe these lines
- What is different between the paired end files? What is the same?
What is the GC content of your files?

## 2. Quality Control and Taxonomic Profiling
### Tools: Fastp, Kraken2 (using nf-core:taxoprofiler)

- **Fastp**: Clean your data by removing low-quality reads and adapters, ensuring high-quality input for downstream analyses.
- **Kraken2**: Assign taxonomic labels to your sequences, providing insights into the diversity of your virome.
- **nf-core:taxoprofiler**: An integrated pipeline that automates the taxonomic profiling process, improving efficiency and reproducibility.

Sequencing Quality Questions

Why do we need quality control?
- adapters and/or primers
- low quality ends
What is the impact of including low quality reads in downstream analyses?
What are the metrics for assessing sequencing quality for Illumina reads?
-- phred scores
-- read quality disribution

## 3. Binning and Evaluation
### Tools: MaxBin2, CheckV

- **MaxBin2**: Organize contigs into bins representing individual genomes, facilitating genome-centric analyses.
- **CheckV**: Evaluate the quality of your viral bins to ensure completeness and minimize contamination, enhancing the reliability of your results.

Questions
How many viral contigs are there in the assembly?
How many bins were found by the tool?
How many high-quality bins do you find?

## 4. Virus Identification
### Tool: geNomad

- **geNomad**: Identify and annotate viral sequences within your assembled contigs, providing crucial insights into the viral components of your sample.

## Additional Considerations

1. **Data Management and Storage**: Ensure you have adequate storage and a robust data management plan in place, as viromics data can be extensive. Here we use a tiny dataset to accelerate the preparation part. 
2. **Computational Resources**: Some of these tools require significant computational resources. Ensure you have access to high-performance computing facilities if necessary.
3. **Documentation and Reproducibility**: Keep detailed records of your commands, parameters, and tool versions to enhance process reproducibility.
4. **Visualization and Interpretation**: Post-analysis, use visualization tools like Krona for taxonomic profiles or Bandage for assembly graphs to better interpret the results.

By following these steps and leveraging the described tools, you will be able to perform an accurate analysis of a viromics dataset. 

{% include links.md %}
