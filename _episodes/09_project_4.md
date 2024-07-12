---
title: "Virus identification using geNomad"
teaching: 
exercises: 30
questions:
- "How to use geNomad?"
objectives:
- "Install geNomad"
- "Run and interpret its result"
keypoints:
- "geNomad"
---

## 4. Virus Identification and annotation by geNomad
### Tools: geNomad

[geNomad](https://portal.nersc.gov/genomad/index.html) is a tool for identifying and annotating viral sequences in metagenomic data.

### Installation
using conda
```
conda create -n genomad -c conda-forge -c bioconda genomad
conda activate genomad
genomad download-database .
```

using docker
```
docker pull antoniopcamargo/genomad
docker run -ti --rm -v "$(pwd):/app" antoniopcamargo/genomad download-database .
docker run -ti --rm -v "$(pwd):/app" antoniopcamargo/genomad end-to-end PRJEB47625/illumina_sample_01_megahit.fa.gz output genomad_db
```

## Pipeline Options

| Option       | Description                                           |
|--------------|-------------------------------------------------------|
| end-to-end   | Executes the full pipeline                            |
| --cleanup    | Force geNomad to delete intermediate files            |
| --splits 8   | To make it possible to run this example in a notebook |

**Usage:**

```bash
# Run the full geNomad pipeline (end-to-end command), taking a nucleotide FASTA file (illumina_sample_01_megahit.fa.gz) and the database (genomad_db) as input and produce output in genomad_output
genomad end-to-end --cleanup --splits 8 PRJEB47625/illumina_sample_01_megahit.fa.gz genomad_output genomad_db
```

geNomad identifies viral sequences within the assembled contigs and provides annotations that are crucial for understanding the viral components of your virome.


{% include links.md %}
