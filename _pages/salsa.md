---
title: "Part 5 - SALSA2 Scaffolding"
layout: archive
permalink: /further_reading/
---


# SALSA2 Scaffolding

Right, so now you have heard of Chromosomo conformation capture and scaffolding genomes with the Hi-C technology. Today you will start one of the softwares that is used to scaffold genomes with Hi-C data which is called SALSA2. You can have a look here on what we will be running: https://github.com/marbl/SALSA

First try:


```console  
python run_pipeline.py -h
``` 

See the help message? Nice! To run SALSA2 you need to copy 2 files to your working directory first. Both files will be inside your species folder, in a folder called "HiC". The files are the 'ref.fa' and a merge.mkdup.bed file. Once you have copied the files over, run:

```console  
python run_pipeline.py -a ref.fa -l ref.fa.fai -b merge.mkdup.bed -e GATC,GANTC -i 5 -p yes -o out
``` 

Right, SALSA2 will run overnight.


Once SALSA2 is done. I want you to investigate the output files:









