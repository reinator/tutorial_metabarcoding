---
title: "Hands On"
layout: archive
permalink: /handsOn_merqury/
---  

# Merqury - evaluating purging and assembly quality

Ok, today you have heard of Purge Dups and purging assemblies. You also have learned that Hicanu outputs an assembly that is double the expected haploid genome size, and then you have to use a tool such as Purge Dups to separated the haplotips of the assembly. Later, you learned about how to evaluated assembly completeness and quality having a look at the shared kmers between the kmers present in the assembly, and kmers in high-quality reads - such as Illumina. Now you are going to run merqury to evaluate assemblies for your species!!

All right, remember yesterday you have assembled a subset of reads for your species, but you have generated statistics for a total-assembly run I have generated previously? This is the file you are going to work on, the total assembly of Hincanu for your species, it will be called something like \*\.hicanu.total.contigs.fasta. So I would like you to create a folder called merqury_hicanu_eval and copy or sym link your \*\.hicanu.total.contigs.fasta total contigs there. Such as:

```console  
mkdir merqury_hicanu_eval
cp <path_to_file>/*.hicanu.total.contigs.fasta merqury_hicanu_eval

```  

Right, so in order to run merqury, you need a meryl datase of the reads you want to compare kmers with kmers in your assembly. In our case, I have created meryl databases for 10X reads (illumina linked-reads) for your species, and you just need to copy the meryl db folder to your execution folder. So you do:

```console  
cp -vrn /home/unbuntu/Data/merylDB/<your_species>/*OUTPUT.21.meryl merqury_hicanu_eval

```  

It will take a few minutes to copy the database...

Once it's copied, let's run merqury! For that, you need to start our conda enviroment:

```console  
source activate eukaryotic_genome_assembly

```  

Right, as soon as see it's activated, try:

```console  
./merqury.sh
```  

The help message should show you that to run merqury, you need (i) the meryl databse (ii) your assembly (iii) an output name. So inside your merqury_hicanu_eval directory, you will do:

```console  
./merqury.sh *OUTPUT.21.meryl *.hicanu.total.contigs.fasta outHicanu
```  

Great!!

This will take a while to run, so we will go back to the wider group, run another Hands On first, and then you will come back here to finish analysing our outputs.

.... Go back to the group! :) Say "Merqury is running for me!!"

(...) One hour later...

Hello back here!


Right, once you are back here merqury should have finished. If merqury finished succesfully, you should have a variety of files produced in your folder: (i) different plots (.png) files, a completeness.stats file and a file that will have the output name you gave (in the example above it was outHicanu) followed by .qv. I want you to analyse all these files and discuss with your partners. Take your time and then produce a presentation with your team showing:

1-) in the hicanu total merqury evaluation, in the plot \*\spectra-asm.st.png, point in the presentation (i) where are the errouneous kmers, (ii) what is the heterozygous peak, (iii) what is the homozygoys peak).
2-) Have a look at the completeness file and right down in your presentation the kmer completness of this assembly
3-) Have a look at the .qv file and right down in your presentation what is the QV for this assembly

# Now

Let's have a look at another merqury folder where I have ran and outputed a merqury evaluation for your species but after I ran purge_dups on it. This means you are going to have plot files for the purged primary assembly, and for the haplotigs assembly. The results file of this run should be in /home/unbuntu/Data/<your_species>/merqury_purge

Take your time and have a look at it all. Then dicuss with your team and answer in your presentation:

1-) Open the files  \*spectra-asm.st.png for the purged, the haplotigs and the total hicanu you have produced. What is the biggest difference between those three plots?

2-) Point on \*spectra-asm.st.png for the purged and hapltoigs where the kmer errors are.

3-) Point on \*spectra-asm.st.png for the purged and hapltoigs where the heterozygous peak is, and where the homzygous peak is?

4-) If you look at \*spectra-asm.st.png you have generated for the total Hicanu output, in the heterozygous peak you don't see any kmers only present on the reads. On the other hand, if you look at \*\spectra-asm.st.png for the primary and the haplotigs you see kmers present only on the reads and absent from the heterozygous peak. Why is that?

5-) Look at the completeness file for the purged ran I have produced: why is the completeness there different from the one you have generated?
6-) Look at the .qv file for the purged ran I have produced: why do you think the qvs are different than the one you have generated?

Discuss all of this with your colleagues and make your presentation.

# Then

Finally, now we are going to look into some CLR assemblies merqury outputs. 
