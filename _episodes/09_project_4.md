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
docker run -ti --rm -v "$(pwd):/app" antoniopcamargo/genomad end-to-end input.fna output genomad_db
```

**Usage:**

```bash
# Run geNomad for virus identification
geNomad identify --input PRJEB47625/illumina_sample_01_megahit.fa.gz --output genomad_output --threads 4
```

geNomad identifies viral sequences within the assembled contigs and provides annotations that are crucial for understanding the viral components of your virome.


{% include links.md %}
