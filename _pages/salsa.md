---
title: "Part 5 - SALSA2 Scaffolding"
layout: archive
permalink: /salsa/
---


# SALSA2 Scaffolding

Right, so now you have learned about Chromosome conformation capture and scaffolding genomes with the Hi-C technology. Today you will start one of the softwares that is used to scaffold genomes with Hi-C that is called SALSA2. You can have a look [here](https://github.com/marbl/SALSA) on what we will be running. 

First try:


```console  
run_pipeline.py -h
``` 

See the help message? Nice! To run SALSA2 you need to copy 2 files to your working directory first. Both files will be inside your species folder, in a folder called `salsa` (`~/Share/Data/<your_species>/salsa`). The files are `ref.fa` and `ref.fa.fai`. Once you have copied the files over, run:

```console  
run_pipeline.py -a ref.fa -l ref.fa.fai -b ~/Share/Data/<your_species>/salsa/merge.mkdup.bed -e GATC,GANTC -i 5 -p yes -o out
``` 

Attention :exclamation:  
Remember to replace `<your_species>` with the name of your species. For instance, for *Vanessa atalanta* that would be `v_atalanta`. Otherwise the command will fail to find the `merge.mkdup.bed` file.

Right, SALSA2 will start running. However, since SALSA2 run should take a long time, we'll **stop SALSA2 run** now with `Ctr+C`. From this point on we'll be using SALSA2 results generated in advance by your instructors. Those files can be found under `~/Share/Data/<your_species>/salsa/out.break.salsa` directory. 


Now let's generate assembly statistics for the genome prior Hi-C scaffolding, and after Hi-C scaffolding. 

First let's add the folder that contains `asmstats` script to our `PATH`:  

```bash  
export PATH=$PATH:/home/ubuntu/softwares/scripts
```

And make sure our conda environment is activated:  
```  
conda activate eukaryotic_genome_assembly  
```

Then copy the file from the genome after Hi-C scaffolding to your working directory:  
```bash  
cp ~/Share/Data/<your_species>/salsa/out.break.salsa/scaffolds_FINAL.fasta .
```

Now we can run `asmstats` for both the genome prior Hi-C scaffolding (`ref.fa`) and after Hi-C scaffolding (`scaffolds_FINAL.fasta`):

```console  
asmstats ref.fa > ref.fa.stats
asmstats scaffolds_FINAL.fasta > scaffolds_FINAL.fasta.stats
``` 

Now I want you to download to your local machine the assembly Hi-C heatmaps for prior and after scaffolding. 

The pre-scaffolding is a file that ends with \*.pretext and it is located in your species folder inside `before_salsa` directory (`~/Share/Data/<your_species>/salsa/before_salsa`). Also, the assembly pre-scaffolding will be in the same folder and is called ref.fa. 

The post-scaffolding will be in the `out.break.salsa` directory (`~/Share/Data/<your_species>/salsa/out.break.salsa`) and it is a file that ends in \*.hic. The scaffolded assembly file is in the same folder and is called `scaffolds_FINAL.fasta`. Recapping: the .hic file and the `scaffolds_FINAL.fasta` are the same thing: just that the .hic file is the heatmap imaging representation of the multifasta file `scaffolds_FINAL.fasta`.

Once you download the two files to your local computer, you are going to use the [pretextView](https://github.com/wtsi-hpag/PretextView/releases/tag/0.1.3) program to open the pre-scaffolding (\*.pretext) heatmap, and the [JuiceBox](https://www.aidenlab.org/juicebox/) program to open the post-scaffolding (\*.hic) heatmap.   

Now, analyze all the results, discuss with your team and answer the questions in your presentation:

1. What are the assembly statistics before scaffolding?
2. What are the assembly statistics after scaffolding?
3. Looking at the final agp file (maybe you wan to read a little about the AGP format [here](https://www.ncbi.nlm.nih.gov/assembly/agp/AGP_Specification/)): what scaffolds were scaffolded with more than one component (a contig of a piece of a contig)? And what scaffolds are unchanged in relation to the contigs?
4. How do the Hi-C maps look prior and after scaffolding?
5. Do you think you see a sex chromosome on the Hi-C heatmap? If so, point to it in your presentation.

After that, come back to the wider group.
