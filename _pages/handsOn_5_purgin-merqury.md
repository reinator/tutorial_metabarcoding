---
title: "Hands On"
layout: archive
permalink: /handsOn_5_purgin-merqury/
---  

# Part 3 - Purging and Merqury evaluation

Ok, today you learned about [Purge Dups](https://github.com/dfguan/purge_dups) and purging assemblies. You also learned that Hicanu outputs an assembly that is double of the expected haploid genome size and that you have to use a tool such as Purge Dups to separate the haplotypes of the assembly. Later, you learned how to evaluate assembly completeness and quality by looking at the shared kmers between the assembly and high-quality reads kmers, such as Illumina or Hifi. Now you are going to run merqury to evaluate assemblies for your species!

All right, earlier today you assembled a subset of reads for your species, but you have generated statistics for a total-assembly run I have generated previously. This total assembly is the file you are going to work on: the total assembly of Hicanu for your species, this is called  `<your_species>.hicanu.total.contigs.fasta.gz`. So I would like you to create a directory called `merqury_hicanu_eval` inside your home species directory (`~/<species_folder>/`), go there and create a symlink to the Hicanu assembly file: `<your_species>.hicanu.total.contigs.fasta.gz` there:

```console  
mkdir ~/<species_folder>/merqury_hicanu_eval/
cd ~/<species_folder>/merqury_hicanu_eval/
ln -s /mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/<species_id>.hicanu.total.contigs.fasta.gz
```  

PS: Remember to replace `<species_id>` with the ID of your species! :)

Right, so in order to run merqury, you need a meryl database of the reads you want to compare kmers with the kmers in your assembly. I have created meryl databases for 10X reads (illumina linked-reads) for your species, and you just need to symlink the meryl db folder to your execution folder. So you do:

```console  
ln -s /mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/<species_id>.10X.21.meryl/
```

Now, let's run merqury! For that, you need to activate the merqury enviroment:

```console  
conda activate merqury_env
```  

Right, as soon as you see it's activated, try:

```console  
merqury.sh
```  

The help message should show you that in order to run merqury, you need (i) the meryl database (ii) your assembly (one or two, if you have primary and haplotigs. For HiCanu its only one) and (iii) an output name. So inside your merqury_hicanu_eval directory, you will create a `.pbs` file with the following command (or just copy it from `/mnt/gen/temp/workshop_montagem_gbb/pbs/job_merqury.pbs`:

```console  
merqury.sh <your_species>.10X.21.meryl <your_species>.hicanu.total.contigs.fasta.gz outHicanu
```  

Great!! 

### Remember ❗
You have to run some commands with `.pbs` file. Everytime we mention it in the text, you have to do so.

## This will take a while to run. During this time...

You are going to gather the results and evaluate the purged version of your species Hicanu assembly. We don't have time to run [Purge_dups](https://github.com/dfguan/purge_dups) here, but the **most important** thing is to learn how to interpret the results after purge_dups is done. So, I have generated for you the (i) purged assemblies, (ii) the merqury, and (iii) the BUSCO results.

1-) First thing you need to do is to symlink the purged assemblies and calculate the general statistics for the primary and haplotigs files. Let's create a new directory to save the purged results and create the symlinks there:

```console  
mkdir ~/<your_species>/purged/
cd ~/<your_species>/purged/
ln -s /mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/purged/purged.fa.gz
ln -s /mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/purged/purged.htigs.fa.gz
```  

Now activate our main conda environment:

```console
conda activate eukaryotic_genome_assembly
```

And then run the `asmstats` script for each file (put the commands below in a `.pbs` file or copy from `/mnt/gen/temp/workshop_montagem_gbb/pbs/job_asmstats.pbs` and replace the commands:

```console
asmstats purged.fa.gz > purged.fa.gz.stats
asmstats purged.htigs.fa.gz > purged.htigs.fa.gz.stats
```

Then, submit the job to the op1 queue:
```console
qsub -q op1 job_asmstats.pbs
```

Great!

2-) Now, I want you to take a look and take notes of the BUSCO results **before** and **after** purging for the Hicanu assembly. The short summaries are the files you should look at. You can do that by using the `less` command:

before purging:

```
less /mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/run_<species_id>.contigs.insecta.busco/short_summary.txt
```

after purging:  

primary:
```
less /mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/run_purged.insecta.busco/short_summary.txt
```

htigs:
```
less /mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/run_purged.htigs.insecta.busco/short_summary.txt
```

Right, now let's have a look at the merqury results.
If the one your group is running for the Hicanu assembly is not done yet, we can start having a look at the purged results.

The merqury results for the purged assemblies are located in this directory: `/mnt/gen/temp/workshop_montagem_gbb/data/<species_id>_data/purged/merqury_purged_eval/` (you don't need to copy anything yet). 

Merqury is going to create a lot of different files: (i) different plot (.png) files, (ii) a <outname>.completeness.stats file and (iii) a <outputname>.qv file.  
    

  
# About the Merqury output files
 
For the plot files, you will have 3 types: st (stacked), ln (line) and fl (filled). 
### These three graphs will represent the same data
they are just a different way of plotting the (same) data. For further information, I recommend having a look at the manual [here](https://github.com/marbl/merqury/wiki/2.-Overall-k-mer-evaluation).
   
# Attention
Apart from having st, fl and ln, merqury is going to output 2 types of files, *asm* and *cn*. If the file contains *cn* it's going to show you all kmer counts of primary + haplotigs in the plot, without distinguishing them. If it contains *asm* it is going to show you kmers belonging to each assembly in different colours. 

DEEP BREATH. 

You are going to get it! (It just takes time!). 

Didn't get it yet? Discuss it with your group!
     
Now I want you to take a look at some relevant Merqury files. The text files can be opened with the `less` command, while you will need to download the plot files (*.png) to your local machine in order to actually open them. 
(Take a look [here](https://itvgenomics.github.io/gbb_montagem_workshop/logging_on/) to remember how to copy files from Superdome to your local machine)
  
  3-) Gather the spectra plots for the primary purged assembly. They will be called `purged.out.purged.spectra-cn*.png` (notice that the `*` represents the different files we have: `st`, `ln` and `fl`)
  
  4-) Gather the spectra plots for the haplotigs purged assembly. It will be called `purged.out.purged.htigs.spectra-cn*.png`
  
  5-) Gather the completeness results for the run. The file is called `completeness.stats`
  
  6-) Gather the QV results for the run. The file is called `purged.out.qv`
  
By the time you finish gathering all of these results, it's very likely that the merqury run for the Hicanu has finished. Please go and have a look at the same 3,4,5 and 6 questions for the total Hicnau run.
  
Now that you have all the results organized, let's interpret them and discuss with your group while you make your group presentation.
  
  - show the statistics for the total Hicanu assembly
  - show the busco short summary for the total Hicanu assembly
  - show the spectra plot for the total Hicanu assembly (one of the files st, ln or fl)
  - show the completeness for the total assembly
  - show the QV for the total assembly.
  
  Go and do the same for the primary purged assembly:
  
  - show the statistics for the purged assembly
  - show the busco short summary for the purged assembly
  - show the spectra plot for the purged assembly (one of the files st, ln or fl)
  - show the completeness for the purged assembly
  - show the QV for the purged assembly.
  
  
  Go and do the same for the htigs purged assembly:
  
   - show the statistics for the purged.htigs assembly
  - show the busco short summary for the purged.htigs assembly
  - show the spectra plot for the purged.htigs assembly (one of the files st, ln or fl)
  - show the completeness for the purged.htigs assembly
  - show the QV for the purged.htigs assembly.
  
  
# Attention!
  
For the purged run, the qv and completeness result for the purged and htigs assembly will be in the same files. Understand what each column of the files qv and completeness mean by reading the manual again:  https://github.com/marbl/merqury/wiki/2.-Overall-k-mer-evaluation
  
 # Now  
  
  I don't know if you realized, but you have for now (i) ran kmer analyses to understand the DNA composition of your reads, (ii) you have ran two genome assemblers and you are learning how to (iii) interprete the BUSCO run results and how to run (iv) and interpret (v) kmer assembly evaluation results with merqury! THIS IS A LOT FOR THREE DAYS! Really well done! Now its time to gather all of the results and answer the following questions with your team and later on we will go through them together as a group.
  
  
  a-) What has happened with the assembly general statistics after it was purged?
  
  b-) Why the HiCanu statistics before purging shows a larger than estimated genome size?
  
  c-) After purging, what the files purged and htigs mean?
  
  d-) How is the BUSCO duplication before purging?
  
  e-) How is the busco duplication in the purged assembly after purging? Why has it changed?
  
  f-) What are all the QVs of the assemblies? Are they good QVs? 
  
  h-) What a QV of 50 means?
  
  Well done! Let's come back to the group all together now!
 
  
