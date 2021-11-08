---
title: "Hands On"
layout: archive
permalink: /handsOn_merqury/
---  

# Part 3 - Purging and Merqury evaluation

Ok, today you leanerd about Purge Dups and purging assemblies. You also learned that Hicanu outputs an assembly that is the double of the expected haploid genome size, and that you have to use a tool such as Purge Dups to separate the haplotypes of the assembly. Later, you learned how to evaluate assembly completeness and quality having a look at the shared kmers between the assembly and high-quality reads kmers, such as Illumina or Hifi. Now you are going to run merqury to evaluate assemblies for your species!

All right, earlier today you have assembled a subset of reads for your species, but you have generated statistics for a total-assembly run I have generated previously. This total assembly is the file you are going to work on: the total assembly of Hicanu for your species, this is called  <your_species>.hicanu.total.contigs.fasta inside <your_species>/assembly/hicanu.total/. So I would like you to create a folder called merqury_hicanu_eval and  sym link your \*.hicanu.total.contigs.fasta there. Such as:

```console  
mkdir merqury_hicanu_eval
cp <path_to_file>/<your_species>.hicanu.total.contigs.fasta merqury_hicanu_eval
```  

PS: Remember to replace `<your_species>` with the ID of your species! :)

Right, so in order to run merqury, you need a meryl datase of the reads you want to compare kmers with the kmers in your assembly. In our case, I have created meryl databases for 10X reads (illumina linked-reads) for your species, and you just need to symlink the meryl db folder to your execution folder. So you do:

```console  
ln -s ~/Share/Data/<your_species>/merqury/<species_ID>.10X.21.meryl merqury_hicanu_eval
```  


Now, let's run merqury! For that, you need to start our conda enviroment (if not yet started):

```console  
conda activate eukaryotic_genome_assembly
```  

Right, as soon as you see it's activated, try:

```console  
merqury.sh
```  

The help message should show you that in order to run merqury, you need (i) the meryl database (ii) your assembly (one or two, if you have primary and haplotigs. In our case its only one) and (iii) an output name. So inside your merqury_hicanu_eval directory, you will do:

```console  
merqury.sh <your_species>.21.meryl <your_species>.hicanu.total.contigs.fasta outHicanu
```  

Great!!

This will take a while to run. During this time, we are going to gather results and evaluate the purged version of your species Hicanu assembly. We don't have time to run Purge_dups here, but the most important thing is to learn how to interprete the results after purge_dups is done. So, Joao and I have generated for you the purged results, the merqury and the BUSCO results.

1-) First thing you need to do is to copy (or symlink) the purged assemblies and generate the general statistics for the p and hitgs files. 


```console  
./asmstats purged.fa.gz > purged.fa.gz.stats
./asmstats purged.htigs.fa.gz > purged.htigs.fa.gz.stats

```  

Great!

2-) Now, I want you to take a look and take notes of the BUSCO results before and after purging for the Hicanu assembly.

Jao, uma vez que as pastas do BUSCO estao copiadas, colocar aqui o caminha e um less 


Right, now let's have a look at the merqury results. If the one your group is running for the Hicanu assembly is not done yet, we can start having a look at the purged results. Merqury is going to create a lot of different files:  (i) different plot (.png) files, (ii) a <outname>.completeness.stats file and (iii) a <outputname>.qv file.  
  
  
  The merqury results for the purged assembleis are here:
  
  
  
  joao.....
  
  
 #  Attention!
  
  
  For the plot files, you will have 3 types: st (stacked), fn (line) and ln (filled). For each spectra these three graphs will represent the same data, they just present a different way to plot the data.
  
  I recommned oppening the merqury folder, taking a deep breath and having a look at the manual here: https://github.com/marbl/merqury/wiki/2.-Overall-k-mer-evaluation
  
  
  # Attention - number 2!
  
  Apart from having st, fn and ln, merqury is going to output 2 types of files, *asm* and *cn*. If the file contains *cn* its going to show you everything in terms of kmer counts without accounting for which kmer is present in which assembly, if it contains *asm* it is going to show you each kmer belonging to each assembly in the plot. Deep breath. You are going to get it! (Just takes time!). Didn't understand, discuss this with your group on zoom!
   
  
  What you need to do with the purging merqury results is:
  
  3-) Gather the spetrac plots for the primary purged assembly. They will be called purged.out.purged.spectra-cn*.png 
  4-) Gather the spetrac plots for the haplotigs purged assembly. It will be called purged.out.purged.htigs.spectra-cn*.png 
  5-) Gather the completeness results for the run. The file is called completeness.stats
  6-) Gather the QV results for the run. The file is called purged.out.qv
  
  
 
  By the time you finish gathering all of these results, its very likely that the merqury run for the Hicanu has finish. Please go and have a look at the same 3,4,5 and 6 questions for the total Hicnau run.
  
  Now that you have all the results organized, let's interprete them and discuss with your group while you make your collective presentation.
  
  - show the statistics for the total Hicanu assembly
  - show the busco short summary for the total Hicanu assembly
  - show the spectra plot for the total Hicanu assembly (one of the files st, ln or fn)
  - show the completeness for the total assembly
  - show the QV for the total assembly.
  
  Go and to the same for the primary purged assembly:
  
   - show the statistics for the purged assembly
  - show the busco short summary for the purged assembly
  - show the spectra plot for the purged assembly (one of the files st, ln or fn)
  - show the completeness for the purged assembly
  - show the QV for the purged assembly.
  
  
  Go and to the same for the htigs purged assembly:
  
   - show the statistics for the purged.htigs assembly
  - show the busco short summary for the purged.htigs assembly
  - show the spectra plot for the purged.htigs assembly (one of the files st, ln or fn)
  - show the completeness for the purged.htigs assembly
  - show the QV for the purged.htigs assembly.
  
  
  # Attention - number 3!
  
  For the purged run, the qv and completeness result for the purged and htigs assembly will be in the same files. Understand what each column of the files qv and completeness mean by reading the manual again:  https://github.com/marbl/merqury/wiki/2.-Overall-k-mer-evaluation
  
  # NOW
  
  I don't know if you realised, but you have for now (i) ran kmer analyses to understand the DNA composition of your reads, (ii) you have ran two genome assemblers and you are learning how to (iii) interprete the BUSCO run results and how to run (iv) and interprete (v) kmer assembly evaluation results with merqury! THIS IS A LOT FOR THREE DAYS! Really well done! Now its time to gather all of the results and answer the following questions with your team and later on we will go through them together as a group.
  
  
  a-) What has happened with the assembly general statistics after it was purged?
  b-) Why the hicanu statistics before purging shows a larger than estimated genome size?
  c-) After purging, what files purged and htigs mean?
  d-) How is the BUSCO duplication before purging?
  e-) How is the busco duplication in the purged assembly after purging? Why has it changed?
  f-) What are all the QVs of the assemblies? Are they good QVs? 
  h-) What a QV of 50 means?
  
  
  
  Well done! Let's come back to the group all together now!
 
  
