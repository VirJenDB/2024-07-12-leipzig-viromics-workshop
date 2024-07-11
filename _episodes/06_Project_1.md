---
title: "Exploring viromics resources and files"
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

## 1. Download viromes and generate a summary report
### Tools: Seqtk, FastQC, Fastp

### Step 1: Exploring Viromics Resources and Files

#### sample 1:  sample (BioProject PRJEB47625)
Sample from [project](https://www.ebi.ac.uk/ena/browser/view/PRJEB47625) on characterizing viral communities associated with human faecal virome.

**Project description:**
The raw sequencing reads were derived from the human faecal virome (BioProject PRJEB47625). Total VLP DNA isolated from [faecal](https://www.ncbi.nlm.nih.gov/bioproject/?term=PRJEB47625) samples provided by three donors were subjected to whole-genome shotgun metagenomic sequencing using Illumina HiSeq X Ten platform. In this study, we compared the use of PCR and PCR-free methods for sequence library construction to assess the impact of PCR amplification bias on the human faecal virome.
 
To download the dataset from a BioProject there are [multiple tools](https://www.ncbi.nlm.nih.gov/home/tools/) including Entrez Direct and SRA Toolkit that need to be installed on your system. Alternatively, we used [SRA Explorer](https://sra-explorer.info/#) online tool to find the list of FastQ files belonging to this BioProject within SRA FTP server. 


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
>
>   - **MacOS (requires Homebrew):**
>   ```sh
>   brew install wget
>   ```
>
>   - **Conda environment:**
>   ```sh
>   conda install anaconda::wget
>   ```
>
> **Using `curl`:**
> `curl` is a command-line tool for transferring data using various network protocols, including HTTP, HTTPS, and FTP.
> - **Installation:**
>   - **Linux (Debian/Ubuntu):**
>   ```sh
>   sudo apt-get install curl
>   ```
>
>   - **MacOS (requires Homebrew):**
>   ```sh
>   brew install curl
>   ```
>
>   - **Conda environment:**
>   ```sh
>   conda install conda-forge::curl
>   ```
>
> Ensure that you have one of these tools installed before proceeding with the download.
{: .discussion}

The list of the curl commands are stored in [PRJEB47625_fastq_download.sh](https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/6db885443ca210ba51c07345717a0bed9abf707a/rawfiles/dataset/PRJEB47625_fastq_download.sh) bash script file. 


```bash
# Create a new directory "PRJEB47625" within "workshop" directory
mkdir workshop_day5 && mkdir workshop_day5/PRJEB47625

# Download "PRJEB47625_fastq_download.sh" bash script file, if you are using wget  
wget -O workshop_day5/PRJEB47625/PRJEB47625_fastq_download.sh https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/1e984f29c4c7e4559493ae26453c6d9122763353/rawfiles/dataset/PRJEB47625_fastq_download_wget.sh

# Download "PRJEB47625_fastq_download.sh" bash script file, if you are using curl
curl -L https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/6db885443ca210ba51c07345717a0bed9abf707a/rawfiles/dataset/PRJEB47625_fastq_download.sh -o workshop_day5/PRJEB47625/PRJEB47625_fastq_download.sh

# Give the required permission to the script to be executed
chmod +x workshop_day5/PRJEB47625/PRJEB47625_fastq_download.sh

# Execute the script that will download 39 Datasets in the current directory 
./workshop_day5/PRJEB47625/PRJEB47625_fastq_download.sh
```

### Step 2: Perform quality control using Fastp
[Fastp](https://github.com/OpenGene/fastp?tab=readme-ov-file) is a fast all-in-one preprocessing tool for FASTQ files. Install the tool from [download page](https://github.com/OpenGene/fastp?tab=readme-ov-file#or-download-the-latest-prebuilt-binary-for-linux-users).
Alternatively, you can install Fastp tool using conda `conda install bioconda::fastp`

---
## Explanation of Main Fastp Options

| Option            | Description                                     |
|-------------------|-------------------------------------------------|
| `-i`              | Input file for read 1 (can be gzipped).         |
| `-I`              | Input file for read 2 (paired-end, can be gzipped). |
| `-o`              | Output file for read 1 (can be gzipped).        |
| `-O`              | Output file for read 2 (paired-end, can be gzipped). |
| `--html`          | Generate an HTML report.                        |
| `--json`          | Generate a JSON report.                         |
| `--thread`        | Number of threads to use.                       |
| `--length_required` | Minimum length of reads to keep.             |

**Usage:**

```bash
# Enter to the workshop day 5 folder
cd workshop_day5 && mkdir fastp_report fastp_output
# Perform quality control on the input FASTQ file
fastp -i PRJEB47625/ERR6797441_1.fastq.gz -I PRJEB47625/ERR6797441_2.fastq.gz -o fastp_output/ERR6797441_1.fastq.gz -O fastp_output/ERR6797441_2.fastq.gz --html fastp_report/report.html --json fastp_report/report.json
```

Fastp not only performs quality filtering but also removes adapters and low-quality reads, producing a cleaned dataset ready for downstream analysis.

**Check the outputs:**

```bash
# If the FastP run finished successfully, there should be two report files in the fastp_report folder and two FASTQ files within the "fastp_output" folder. FASTQ files will be used in the next step.
ls fastp_output/
ls fastp_report/ 

# To see FASTQ content, use zcat as they are compressed files
zcat fastp_output/ERR6797441_1.fastq.gz | head -n 10
 
# To see the report, either use a web browser to open fastp_report/report.html or use the head to read the first 26 lines of json file
head -n 26 fastp_report/report.json
```

### Step 3: Assess the quality of the sequencing data using FastQC
[FastQC](https://github.com/s-andrews/FastQC) provides a simple way to perform quality control checks on raw sequence data. Check the [download](https://www.bioinformatics.babraham.ac.uk/projects/download.html#fastqc) page to download and install it or install it in the conda environment `conda install bioconda::fastqc`.

**Usage:**

```bash
# create a directory for FastQC output
mkdir fastqc_report 
# Run FastQC on the input FASTQ file
fastqc PRJEB47625/ERR6797441_1.fastq.gz -o fastqc_report
```

FastQC generates a detailed report on the quality of the sequencing data, including information on read length distribution, GC content, and the presence of adapters, which helps in identifying any potential issues before further analysis.

**Let's take a look at the statistics generated by FastQC:**

```bash
unzip fastqc_report/ERR6797441_1_fastqc.zip -d fastqc_report
head fastqc_report/ERR6797441_1_fastqc/fastqc_data.txt -n 20
```

### Step 4: Create small files for use in the next steps using Seqtk
Seqtk is a fast and lightweight tool for processing sequences in the FASTA/FASTQ format. Check the GitHub page of [Seqtk](https://github.com/lh3/seqtk) to install the tool. Alternatively, use `conda install bioconda::seqtk` to install Seqtk as a conda package.

**Usage:**

```bash
# Extract the first 1000 reads from a FASTQ file
seqtk sample -s100 fastp_output/ERR6797441_1.fastq.gz 1000 > read1.fastq
seqtk sample -s100 fastp_output/ERR6797441_2.fastq.gz 1000 > read2.fastq
```

In this step, we use Seqtk to create a smaller subset of the data for initial exploration, which helps in quickly assessing the quality and content of the dataset without processing the entire file.

{% include links.md %}
