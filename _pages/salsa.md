---
title: "Part 5 - SALSA2 Scaffolding"
layout: archive
permalink: /salsa/
---


# SALSA2 Scaffolding

Right, so now you have learned about Chromosome conformation capture and scaffolding genomes with the Hi-C technology. Today you will start one of the softwares that is used to scaffold genomes with Hi-C that is called SALSA2. You can have a look [here](https://github.com/marbl/SALSA) on what we will be running. 

First you need to activate our SALSA environment:

```console
conda activate salsa_env  
```

Then run:

```console  
run_pipeline.py -h
``` 

See the help message? Nice! 

Now let's create a `scaff` subdirectory in your species home directory so that we can work on scaffolding from there:

```console  
mkdir ~/<species_folder>/scaff/
cd ~/<species_folder>/scaff/  
```

To run SALSA2 you need first to symlink 3 files to your working directory. All files will be inside the shared species directory, in a subdirectory called `HiC` (`~/Share/<species_id>_data/HiC/`). The files are `<species_id>_hicanu.purged.polish.fa`, `<species_id>_hicanu.purged.polish.fa.fai` and `merge.mkdup.bed`. Once you have symlinked all files, run:

```console  
run_pipeline.py -a <species_id>_hicanu.purged.polish.fa -l <species_id>_hicanu.purged.polish.fa.fai -b merge.mkdup.bed -e GATC,GANTC -i 5 -p yes -o out
``` 

Attention :exclamation:  
Remember to replace `<species_id>` with the ID of your species. For instance, for *Vanessa atalanta* that would be `ilVanAtal1`.

Right, SALSA2 will start running. However, since SALSA2 run should take a long time, we'll **stop SALSA2 run** now with `Ctr+C`. From this point on we'll be using SALSA2 results generated in advance by your instructors. Those files can be found under `~/Share/<species_id>_data/HiC/out.break.salsa/` directory. 

Now let's generate assembly statistics for the genome prior Hi-C scaffolding, and after Hi-C scaffolding. 

First let's add the folder that contains `asmstats` script to our `PATH`:  

```bash  
export PATH=$PATH:~/Share/scripts
```

And make sure our conda environment is activated:  
```  
conda activate eukaryotic_genome_assembly  
```

Then symlink the file from the genome after Hi-C scaffolding to your working directory:  
```bash  
ln -s ~/Share/<species_id>_data/HiC/out.break.salsa/scaffolds_FINAL.fasta .
```

Now we can run `asmstats` for both the genome prior Hi-C scaffolding (`<species_id>_hicanu.purged.polish.fa`) and after Hi-C scaffolding (`scaffolds_FINAL.fasta`):

```console  
asmstats <species_id>_hicanu.purged.polish.fa > <species_id>_hicanu.purged.polish.fa.stats
asmstats scaffolds_FINAL.fasta > scaffolds_FINAL.fasta.stats
``` 

Now I want you to download to your local machine the assembly Hi-C heatmaps for (i) prior and (ii) after scaffolding. 

1-) Opening the Hi-C heatmap at pretextview of your species contigs **before** they were scaffolded with Salsa2

The pre-scaffolding is a file that ends with \*.pretext and it is located in your species shared directory at `~/Share/<species_id>_data/HiC/<species_id>.preScaf.pretext`. Also, the assembly pre-scaffolding will be in the same folder and is called <species_id>_hicanu.purged.polish.fa. 

2-) Opening the Hi-C heatmap with Juicebox of your species scaffolds **after** the contigs were scaffolded with Salsa2

The post-scaffolding will be in the `out.break.salsa` directory (`~/Share/<species_id>_data/HiC/out.break.salsa/`) and it is a file that ends in \*.hic. The scaffolded assembly file is in the same folder and is called `scaffolds_FINAL.fasta`. Recapping: the .hic file and the `scaffolds_FINAL.fasta` are the same thing: just that the .hic file is the heatmap imaging representation of the multifasta file `scaffolds_FINAL.fasta`.

Once you download the two files to your local computer, you are going to use the [pretextView](https://github.com/wtsi-hpag/PretextView/releases/tag/0.1.3) program to open the pre-scaffolding (\*.pretext) heatmap, and the [JuiceBox](https://www.aidenlab.org/juicebox/) program to open the post-scaffolding (\*.hic) heatmap.   

Now, analyze all the results, discuss with your team and answer the questions in your presentation:

1. What are the assembly statistics before scaffolding?
2. What are the assembly statistics after scaffolding?
3. Looking at the final agp file (maybe you wan to read a little about the AGP format [here](https://www.ncbi.nlm.nih.gov/assembly/agp/AGP_Specification/)): what scaffolds were scaffolded with more than one component (a contig of a piece of a contig)? And what scaffolds are unchanged in relation to the contigs?
4. How do the Hi-C maps look prior and after scaffolding?
5. Do you think you see a sex chromosome on the Hi-C heatmap? If so, point to it in your presentation.

After that, come back to the wider group.
