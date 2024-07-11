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
mkir workshop && cd workshop && mkdir PRJNA646773

# Download "PRJNA646773_fastq_download.sh" bash script file  
wget -O PRJNA646773_fastq_download.sh https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/f38c57fe435c149f8210d2e9c46cf1d34f85fd91/rawfiles/dataset/PRJNA646773_fastq_download.sh
curl -L https://raw.githubusercontent.com/VirJenDB/2024-07-12-leipzig-viromics-workshop/f38c57fe435c149f8210d2e9c46cf1d34f85fd91/rawfiles/dataset/PRJNA646773_fastq_download.sh -o PRJNA646773_fastq_download.sh
# Give the required permission to the script to be executed
chmod +x PRJNA646773_fastq_download.sh

# Execute the script that will download 39 Datasets in the current directory 
./PRJNA646773_fastq_download.sh
 
```

<div>
    <ul class="nav nav-tabs" role="tablist">
      <li role="presentation" class=""><a data-os="windows" href="#shell-windows" aria-controls="Windows" role="tab" data-toggle="tab">Windows</a></li>
      <li role="presentation" class=""><a data-os="macos" href="#shell-macos" aria-controls="MacOS" role="tab" data-toggle="tab">MacOS</a></li>
      <li role="presentation" class="active"><a data-os="linux" href="#shell-linux" aria-controls="Linux" role="tab" data-toggle="tab">Linux</a></li>
    </ul>

    <div class="tab-content">
      <article role="tabpanel" class="tab-pane" id="shell-windows">
        <ol>
          <li>Download the Git for Windows <a href="https://gitforwindows.org/">installer</a>.</li>
          <li>Run the installer and follow the steps below:
            <ol>
              
              <li>
                Click on "Next" four times (two times if you've previously
                installed Git).  You don't need to change anything
                in the Information, location, components, and start menu screens.
              </li>
              <li>
                <strong>
                  From the dropdown menu, "Choosing the default editor used by Git", select "Use the Nano editor by default" (NOTE: you will need to scroll <emph>up</emph> to find it) and click on "Next".
                </strong>
              </li>
              
              <li>
                On the page that says "Adjusting the name of the initial branch in new repositories", ensure that
		"Let Git decide" is selected. This will ensure the highest level of compatibility for our lessons.
		     
              </li>
              
              <li>
                Ensure that "Git from the command line and also from 3rd-party software" is selected and
                click on "Next". (If you don't do this Git Bash will not work properly, requiring you to
                remove the Git Bash installation, re-run the installer and to select the "Git from the
                command line and also from 3rd-party software" option.)
              </li>
              
 	      <li>
	      Select "Use bundled OpenSSH".
	      </li>
              
              <li>
		Ensure that "Use the native Windows Secure Channel Library" is selected and click on "Next".
	      </li>
              
              
              <li>
                Ensure that "Checkout Windows-style, commit Unix-style line endings" is selected and click on "Next".
              </li>
              
              <li>
                <strong>
                  Ensure that "Use Windows' default console window" is selected and click on "Next".
                </strong>
              </li>
              
              <li>
		Ensure that "Default (fast-forward or merge) is selected and click "Next"
              </li>
              <li>
		Ensure that "Git Credential Manager" is selected and click on "Next".
              </li>
              <li>
		Ensure that "Enable file system caching" is selected and click on "Next".
              </li>
              
              <li>Click on "Install".</li>
              
              
              
              <li>Click on "Finish" or "Next".</li>
            </ol>
          </li>
          <li>
            If your "HOME" environment variable is not set (or you don't know what this is):
            <ol>
              <li>Open command prompt (Open Start Menu then type <code>cmd</code> and press <kbd>Enter</kbd>)</li>
              <li>
                Type the following line into the command prompt window exactly as shown:
                <p><code>setx HOME "%USERPROFILE%"</code></p>
              </li>
              <li>Press <kbd>Enter</kbd>, you should see <code>SUCCESS: Specified value was saved.</code></li>
              <li>Quit command prompt by typing <code>exit</code> then pressing <kbd>Enter</kbd></li>
            </ol>
	  </li>
        </ol>
        <p>This will provide you with both Git and Bash in the Git Bash program.</p>
        <h4 id="video-tutorial">Video Tutorial<a class="anchorjs-link " aria-label="Anchor" data-anchorjs-icon="" href="#video-tutorial" style="font: 1em / 1 anchorjs-icons; padding-left: 0.375em;"></a></h4>
        <div class="yt-wrapper2">
        <div class="yt-wrapper">
        <p>Looks like your adblocker blocked the registration window. Please navigate to <a href="https://www.eventbrite.com/tickets-external?eid=&amp;ref=etckt">https://www.eventbrite.com/tickets-external?eid=&amp;ref=etckt</a> to register.</p><iframe type="text/html" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" src="https://www.youtube-nocookie.com/embed/339AEqk9c-8?modestbranding=1&amp;playsinline=1&amp;iv_load_policy=3&amp;rel=0" class="yt-frame" allowfullscreen=""></iframe>
        </div>
        </div>
      </article>
      <article role="tabpanel" class="tab-pane" id="shell-macos">
        <p>
          The default shell in Mac OS X Ventura and newer versions is Zsh, but
	  Bash is available in all versions, so no need to install anything.
	  You access Bash from the Terminal (found in
	  <code>/Applications/Utilities</code>).
          See the Git installation <a href="#shell-macos-video-tutorial">video tutorial</a>
          for an example on how to open the Terminal.
          You may want to keep Terminal in your dock for this workshop.
        </p>
        <p>
            To see if your default shell is Bash type <code>echo $SHELL</code>
            in Terminal and press the <kbd>Return</kbd> key. If the message
            printed does not end with '/bash' then your default is something
            else, you can change your current shell to Bash by typing
            <code>bash</code> and then pressing  <kbd>Return</kbd>. To check
            your current shell type <code>echo $0</code> and press <kbd>Return</kbd>.
        </p>
        <p>
          To change your default shell to Bash type <code>chsh -s /bin/bash</code> and
          press the <kbd>Return</kbd> key, then reboot for the change to take effect. To
          change your default back to Zsh, type <code>chsh -s /bin/zsh</code>, press the
          <kbd>Return</kbd> key and reboot.  To check available shells, type
          <code>cat /etc/shells</code>.
        </p>
        <h4 id="shell-macos-video-tutorial">Video Tutorial<a class="anchorjs-link " aria-label="Anchor" data-anchorjs-icon="" href="#shell-macos-video-tutorial" style="font: 1em / 1 anchorjs-icons; padding-left: 0.375em;"></a></h4>
        <div class="yt-wrapper2">
        <div class="yt-wrapper">
        <p>Looks like your adblocker blocked the registration window. Please navigate to <a href="https://www.eventbrite.com/tickets-external?eid=&amp;ref=etckt">https://www.eventbrite.com/tickets-external?eid=&amp;ref=etckt</a> to register.</p><iframe type="text/html" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" src="https://www.youtube-nocookie.com/embed/9LQhwETCdwY?modestbranding=1&amp;playsinline=1&amp;iv_load_policy=3&amp;rel=0" class="yt-frame" allowfullscreen=""></iframe>
        </div>
        </div>
      </article>
      <article role="tabpanel" class="tab-pane active" id="shell-linux">
        <p>
          The default shell is usually Bash and there is usually no need to
          install anything.
        </p>
        <p>
            To see if your default shell is Bash type <code>echo $SHELL</code>
            in Terminal and press the <kbd>Return</kbd> key. If the message
            printed does not end with '/bash' then your default is something
            else, you can change your current shell to Bash by typing
            <code>bash</code> and then pressing  <kbd>Return</kbd>. To check
            your current shell type <code>echo $0</code> and press <kbd>Return</kbd>.
        </p>
        <p>
          To change your default shell to Bash type <code>chsh -s /bin/bash</code> and
          press the <kbd>Return</kbd> key, then reboot for the change to take effect. To
          change your default back to Zsh, type <code>chsh -s /bin/zsh</code>, press the
          <kbd>Return</kbd> key and reboot.  To check available shells, type
          <code>cat /etc/shells</code>.
        </p>
      </article>
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
