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

#### sample 1: soil sample (BioProject PRJNA646773)
Sample from project on characterization of viral communities associated with agricultural soils.

**Project description:**
The aim of [project PRJNA646773](https://www.ncbi.nlm.nih.gov/bioproject/?term=PRJNA646773) was to profile the viral diversity associated with agricultural fields. Plots treated with four different biochar treatments and two nitrogen fertilization regimes were sampled before and during a tomato growing season. Paired total metagenomes and viral-size metagenomes (viromes) were generated for each sample
 
To download the dataset from a BioProject there are [multiple tools](https://www.ncbi.nlm.nih.gov/home/tools/) including Entrez Direct and SRA Toolkit that need to be installed on your system. Alternatively, we used [SRA Explorer](https://sra-explorer.info/#) online tool to find the list of FastQ files belonging to this BioProject within SRA FTP server. 


<details>
<summary>⚠️ Warning: Download Requirements</summary>

To successfully download the required files, you need to have either `wget` or `curl` installed on your system. These tools are essential for fetching files from the internet.

**Using `wget`:**
- `wget` is a command-line utility for downloading files from the web. It supports HTTP, HTTPS, and FTP protocols.
- **Installation:**
  - **Linux (Debian/Ubuntu):**
    ```sh
    sudo apt-get install wget
    ```
  - **MacOS:**
    ```sh
    brew install wget
    ```
    (requires Homebrew)

**Using `curl`:**
- `curl` is a command-line tool for transferring data using various network protocols, including HTTP, HTTPS, and FTP.
- **Installation:**
  - **Linux (Debian/Ubuntu):**
    ```sh
    sudo apt-get install curl
    ```
  - **MacOS:**
    ```sh
    brew install curl
    ```
    (requires Homebrew)

**Example Usage:**

- **wget:**
  ```sh
  wget http://example.com/file.zip
  ```
 
- **curl:**
  ```sh
  curl -O http://example.com/file.zip
  ```

Ensure that you have one of these tools installed before proceeding with the download.
</details>

The list of the curl commands are stored in [PRJNA646773_fastq_download.sh](https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/f38c57fe435c149f8210d2e9c46cf1d34f85fd91/rawfiles/dataset/PRJNA646773_fastq_download.sh) bash script file. 


```bash
# Create a new directory "PRJNA646773" within "workshop" directory
mkdir workshop && cd workshop && mkdir PRJNA646773

# Download "PRJNA646773_fastq_download.sh" bash script file  
wget -O PRJNA646773_fastq_download.sh https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/f38c57fe435c149f8210d2e9c46cf1d34f85fd91/rawfiles/dataset/PRJNA646773_fastq_download.sh
curl -L https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/f38c57fe435c149f8210d2e9c46cf1d34f85fd91/rawfiles/dataset/PRJNA646773_fastq_download.sh -o PRJNA646773_fastq_download.sh
# Give the required permission to the script to be executed
chmod +x PRJNA646773_fastq_download.sh

# Execute the script that will download 39 Datasets in the current directory 
./PRJNA646773_fastq_download.sh
 
```

<div class="container mt-3">
    <ul class="nav nav-tabs" role="tablist">
        <li class="nav-item">
            <a class="nav-link active" id="wget-tab" data-toggle="tab" href="#shell-windows" role="tab">WGET</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" id="curl-tab" data-toggle="tab" href="#shell-macos" role="tab">CURL</a>
        </li>
    </ul>

    <div class="tab-content">
        <div class="tab-pane fade show active" id="shell-windows" role="tabpanel">
            <ol>
                <li>Download the Git for Windows <a href="https://gitforwindows.org/">installer</a>.</li>
                <li>Run the installer and follow the steps below:
                    <ol>
                        <li>Click on "Install".</li>
                        <li>Create a new directory "PRJNA646773" within the "workshop" directory:
                            <code>mkdir workshop && cd workshop && mkdir PRJNA646773</code>
                        </li>
                        <li>Click on "Finish" or "Next".</li>
                    </ol>
                </li>
            </ol>
        </div>
	<div class="tab-pane fade" id="shell-macos" role="tabpanel">
            <p>Here is a `bash` code example:</p>
            <pre><code class="bash">echo "This is a bash code example"</code></pre>
        </div>
    </div>
</div>

# x

<div class="tabs">
  <button class="tablink" onclick="openTab(event, 'wgetcode')">wget</button>
  <button class="tablink" onclick="openTab(event, 'curlcode')">curl</button>
</div>

<div id="wgetcode" class="tabcontent">
```bash
# Create a new directory "PRJNA646773" within "workshop" directory
mkir workshop && cd workshop && mkdir PRJNA646773

# Download "PRJNA646773_fastq_download.sh" bash script file
wget -O PRJNA646773_fastq_download.sh https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/f38c57fe435c149f8210d2e9c46cf1d34f85fd91/rawfiles/dataset/PRJNA646773_fastq_download.sh 

# Give the required permission to the script to be executed
chmod +x PRJNA646773_fastq_download.sh

# Execute the script that will download 39 Datasets in the current directory
./PRJNA646773_fastq_download.sh
```
</div>
<div id="curlcode" class="tabcontent">
```bash
# Create a new directory "PRJNA646773" within "workshop" directory
mkir workshop && cd workshop && mkdir PRJNA646773

# Download "PRJNA646773_fastq_download.sh" bash script file
curl -L https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/f38c57fe435c149f8210d2e9c46cf1d34f85fd91/rawfiles/dataset/PRJNA646773_fastq_download.sh -o PRJNA646773_fastq_download.sh

# Give the required permission to the script to be executed
chmod +x PRJNA646773_fastq_download.sh

# Execute the script that will download 39 Datasets in the current directory
./PRJNA646773_fastq_download.sh
```
</div>
<style>
/* Style the tab */
.tablink {
  background-color: #f1f1f1;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  font-size: 17px;
  transition: 0.3s;
}

/* Change background color of buttons on hover */
.tablink:hover {
  background-color: #ddd;
}

/* Style the tab content */
.tabcontent {
  display: none;
  padding: 20px;
  border: 1px solid #ddd;
  border-top: none;
}

/* Show the active tab content */
.tabcontent.active {
  display: block;
}
</style>
<script>
// Function to open the tab
function openTab(evt, tabName) {
  var i, tabcontent, tablinks;
  tabcontent = document.getElementsByClassName("tabcontent");
  for (i = 0; i < tabcontent.length; i++) {
    tabcontent[i].style.display = "none";
  }
  tablinks = document.getElementsByClassName("tablink");
  for (i = 0; i < tablinks.length; i++) {
    tablinks[i].className = tablinks[i].className.replace(" active", "");
  }
  document.getElementById(tabName).style.display = "block";
  evt.currentTarget.className += " active";
}

// Set default tab to open
document.addEventListener('DOMContentLoaded', (event) => {
  document.querySelector('.tablink').click();
});
</script>

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
