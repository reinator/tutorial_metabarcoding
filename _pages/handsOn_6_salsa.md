---
title: "Part 4 - SALSA2 Scaffolding"
layout: archive
permalink: /handsOn_6_salsa/
---


# SALSA2 Scaffolding

Right, so now you have learned about Chromosome conformation capture and scaffolding genomes with the Hi-C technology. Today you will start one of the softwares that is used to scaffold genomes with Hi-C that is called SALSA2. You can have a look [here](https://github.com/marbl/SALSA) on what we will be running. 

First you need to activate our SALSA environment:

```console
conda activate salsa  
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

To run SALSA2 you need first to symlink 3 files to your working directory. All files are inside `<species>_data` directory, in a subdirectory called `HiC` (`/mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/HiC/`). The files are `<species_id>_*purged.polish.fa`, `<species_id>_*purged.polish.fa.fai` and `<species_id>.merge.mkdup.bed`. 

If the file `<species_id>_*purged.polish.fa.fai` does not exist, once you symlink the fasta file, just run the following command in the console:
```console  
samtools faidx <species_id>_*purged.polish.fa
```


Once you have symlinked all files, put the commands below in a `.pbs` file (or just copy it from `/mnt/gen/temp/workshop_montagem_gbb/pbs/job_salsa.pbs`) :

```console
source /bio_temp/share_bio/softwares/miniconda3/etc/profile.d/conda.sh
conda activate salsa
run_pipeline.py -a <species_id>_*purged.polish.fa -l <species_id>_*purged.polish.fa.fai -b <species_id>.merge.mkdup.bed -e GATC,GANTC -i 5 -p yes -o out
``` 

> Attention :exclamation:  
> Remember to replace `<species_id>` with the ID of your species. For instance, for *Vanessa atalanta* that would be `ilVanAtal1`.


> **What exactly are you scaffolding?**
> You will notice that the contigs you are scaffolding are called polish. In fact, if/when you run a summary statistics for them you will see that they have a different number of bases compared with the purged assembly you analyzed. Why is that? That is because at Darwin Tree of Life we used to polish the purged genomes before scaffolding (remember I showed you this in the lecture?). We have dropped polishing now, but you are working with data that was polished. :) 

Right, SALSA2 will start running. However, since SALSA2 run should take a long time, we'll **stop SALSA2 run** now with `qdel`. From this point on we'll be using SALSA2 results generated in advance by your instructors. Those files can be found under `/mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/HiC/out.break.salsa/` directory. 

Now let's generate assembly statistics for the genome prior Hi-C scaffolding, and after Hi-C scaffolding. 

Make sure our conda environment is activated:  
```  
conda activate eukaryotic_genome_assembly  
```

Then symlink the file from the genome after Hi-C scaffolding to your working directory:  
```bash  
ln -s /mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/HiC/out.break.salsa/scaffolds_FINAL.fasta.gz .
```

Now we can run `asmstats` for both the genome prior Hi-C scaffolding (`<species_id>_hicanu.purged.polish.fa`) and after Hi-C scaffolding (`scaffolds_FINAL.fasta`):

Put the commands below in a `.pbs` file:
```console  
asmstats <species_id>*.purged.polish.fa > <species_id>*.purged.polish.fa.stats
asmstats scaffolds_FINAL.fasta > scaffolds_FINAL.fasta.stats
``` 

Now I want you to download to your local machine the assembly Hi-C heatmaps for (i) prior and (ii) after scaffolding.
Instructions on how to download files to your local machine can be found [here](https://itvgenomics.github.io/gbb_montagem_workshop/logging_on/)

1-) Hi-C heatmap of your species contigs **before** they were scaffolded with SALSA2

If you are working with ilNotDrom1 or ilVanAtal1, the pre-scaffolding is a file that ends with \*.pretext and it is located in your species shared directory (`/mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/HiC/<species_id>.preScaf.pretext`). 

The pre-scaffolding file for drUrtUren1 ends with \*.hic and it is located in your species' shared directory (`/mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/HiC/drUrtUren1.preScaf.hic`). This is to be open at Juicer.

2-) Hi-C heatmap of your species scaffolds **after** the contigs were scaffolded with SALSA2

The post-scaffolding will be in the `out.break.salsa` directory (`/mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/HiC/out.break.salsa/`) and it is a file that ends in \*.hic. This file is a heatmap image representing the final scaffolded assembly (`scaffolds_FINAL.fasta`).

Once you download the two files (pre and after scaffolding) to your local computer, you are going to use the PretextView program to open the pre-scaffolding heatmap, and the JuiceBox program to open the post-scaffolding heatmap. You should already have PretextView installed on your local computer. If not, follow [this link](https://itvgenomics.github.io/gbb_montagem_workshop/pretextView_installation/) to install it. You can run Juicebox using its [website](https://www.aidenlab.org/juicebox/) or (optionally) you can also run it locally. If you choose to run Juicebox locally, you will need to access [this link](https://github.com/aidenlab/Juicebox/wiki/Download) to download the executable for Juicebox compatible with your operating system, and after you download it, just double click on the executable file to open Juicebox.

### Using Juicebox  
##### Using the webserver
Go to the Juicebox's [website](https://www.aidenlab.org/juicebox/). Click on `Load Map > Local File` and locate your downloaded \*.hic file.

##### Using locally installed Juicebox (optional)
Once you open Juicebox, click on `File > Open`. A new window will open, then you should click on the `Local...` button. Now you are ready to select the downloaded \*.hic file. Once you do it, the heatmap should be plotted. 

### Using PretextView
After opening PretextView, click on the `Load Map` button and then select the downloaded \*.pretext file.

## Now 
Analyze all the results, discuss them with your team, and answer the questions in your presentation:

1. What are the assembly statistics before scaffolding?
2. What are the assembly statistics after scaffolding?
3. Looking at the final agp file (`/mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/HiC/out.break.salsa/scaffolds_FINAL.agp`) (maybe you want to read a little about the AGP format [here](https://www.ncbi.nlm.nih.gov/assembly/agp/AGP_Specification/)): what scaffolds were scaffolded with more than one component (a contig of a piece of a contig)? And what scaffolds are unchanged in relation to the contigs?
4. How do the Hi-C maps look prior and after scaffolding?
5. Do you think you see a sex chromosome on the Hi-C heatmap? If so, point to it in your presentation.

After that, let's discuss the results together!
