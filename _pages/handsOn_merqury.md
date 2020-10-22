---
title: "Hands On"
layout: archive
permalink: /handsOn_merqury/
---  

# Merqury - evaluating purging and assembly quality

Ok, today you have heard of Purge Dups and purging assemblies. You also have learned that Hicanu outputs an assembly that is double the expected haploid genome size, and then you have to use a tool such as Purge Dups to separated the haplotips of the assembly. Later, you learned about how to evaluated assembly completeness and quality having a look at the shared kmers between the kmers present in the assembly, and kmer in high-quality reads - such as Illumina. Now you are going to run merqury to evaluate assemblies for your species!!

All right, then the first step is to copy the output of Hicanu for the species you have chosen to your folder (you can make a folder for this analysis to organize your data).

```console  
cp /home/unbuntu/Results/purge_dups/<your_species>/*contigs.fasta .

```  

Right, now that you need to copy the meryl database for the Illumina reads of your species. I have made that database for you, you just need to copy the folder with several files to your folder.

```console  
cp -vrn /home/unbuntu/Data/merylDB/<your_species>/

```  
