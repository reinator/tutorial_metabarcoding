---
title: "Part 5 - SALSA2 Scaffolding"
layout: archive
permalink: /salsa/
---


# SALSA2 Scaffolding

Right, so now you have learned about Chromosome conformation capture and scaffolding genomes with the Hi-C technology. Today you will start one of the softwares that is used to scaffold genomes with Hi-C that is called SALSA2. You can have a look here on what we will be running: https://github.com/marbl/SALSA

First try:


```console  
python run_pipeline.py -h
``` 

See the help message? Nice! To run SALSA2 you need to copy 2 files to your working directory first. Both files will be inside your species folder, in a folder called `salsa` (`~Share/Data/<your_species>/salsa`). The files are the `ref.fa` and a `merge.mkdup.bed` file. Once you have copied the files over, run:

```console  
python run_pipeline.py -a ref.fa -l ref.fa.fai -b merge.mkdup.bed -e GATC,GANTC -i 5 -p yes -o out
``` 

Right, SALSA2 will start running. However, since SALSA2 running should take a long time, we'll **stop SALSA2 run** now with `Ctr+C`. From this point on we'll be using data SALSA2 results generated in advance by your instructors. Those files can be found under `~Share/Data/<your_species>/salsa/out.break.salsa` directory. 


Now let's generate assembly statistics for the genome prior Hi-C scaffolding, and after Hi-C scaffolding (again, make sure `eukaryotic_genome_assembly` environment is activated so that you can use the `asmstats` command):

```console  
asmstats ref.fa > ref.fa.stats
asmstats scaffolds_FINAL.fasta > scaffolds_FINAL.fasta.stats
``` 

Also, now I want you to copy the assembly Hi-C heatmaps for prior and after scaffolding. You are going to use two different softwares to visualize these heatmaps: [pretextView](https://github.com/wtsi-hpag/PretextView/releases/tag/0.1.3) and [JuiceBox](https://www.aidenlab.org/juicebox/)

Ok, so you have to download both heatmaps to your local computer, and then you open the pre-scaffolding heeatmap on pretextView and the post-scaffolding on Juicebox. The pre-scaffolding is a file called \*.pretext located in your species folder inside `before_salsa` directory (`~Share/Data/<your_species>/salsa/before_salsa`) and should be open with pretextView. The post-scaffolding will be in the `out.break.salsa` directory (`~Share/Data/<your_species>/salsa/out.break.salsa`) and it is a file that ends in \*.hic and should be opened with JuiceBox.

Now, analyze all the results, discuss with your team and answer the questions in your presentation:

1-) What are the assembly statistics before scaffolding?

2-) What are the assembly statistics after scaffolding?

3-) Looking at the final agp file: what scaffolds were scaffolded with more than one component (a contig of a piece of a contig)? And what scaffolds are unchanged in relation to the contigs?

4-) How do the Hi-C maps look prior and after scaffolding?

5-) Do you think you see a sex chromosome on the Hi-C heatmap? If so, point to it in your presentation.

After that, come back to the wider group.
