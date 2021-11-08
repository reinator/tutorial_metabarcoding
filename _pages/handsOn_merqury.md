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
  
  
  # Attention - number 2!
  
  Apart from having st, fn and ln, merqury is going to output 2 types of files, *asm* and *cn*. If the file contains *cn* its going to show you everything in terms of kmer counts, if it contains *asm* it is going to show you each kmer belonging to each assembly in the plot. Deep breath. You are going to get it! (Just takes time!).
  
  
  
  The *spectra* ones will show you only the kmers in that assembly. Example: 
 I recommned oppening the merqury folder, taking a deep breath and having a look at the manual here: https://github.com/marbl/merqury/wiki/2.-Overall-k-mer-evaluation
  
  What you need to do in the purging merqury results is:
  
  3-) Gather the spetrac plots for the primary purged assembly. They will be called purged.out.purged.spectra-cn*.png 
  4-) Gather the spetrac plots for the haplotigs purged assembly. It will be called purged.out.purged.htigs.spectra-cn*.png 
  5-) Gather the completeness results for the run. The file is called completeness.stats
  6-) Gather the QV results for the run. The file is called purged.out.qv
  
  
 
  By the time you finish gathering all of these results, its very likely that the merqury run for the Hicanu has finish. Please go and have a look at the same 3,4,5 and 6 for the total Hicnau run.
  
  Now that you have all the results organized, let's interprete them and discuss with your group while you make your collective presentation.
  
  - show the statistics for the total Hicanu assembly
  - show the busco short summary for the total Hicanu assembly
  - show the spectra plot for the total Hicanu assembly (one of the files st, ln or fn.
  
  
  
  
 
     1\. in your hicanu total merqury evaluation, in the plot \*spectra-asm.st.png, point in the presentation: (i) where are the assembly erroneous kmers, (ii) what is the heterozygous peak, (iii) what is the homozygoys peak.

     2\. Have a look at the completeness file and write down in your presentation the kmer completeness of this assembly. 

     3\. Have a look at the .qv file and write down in your presentation what is the QV for this assembly.

# Now

Let's have a look at another merqury folder where I have ran a merqury evaluation for your species after I had ran purge_dups on it. This means you are going to have plot files for the purged primary assembly, as well as for the haplotigs assembly. The results files of this run should be in `~/Share/Data/<your_species>/merqury/merqury_purged`.

Take your time and have a look at it all. Then dicuss with your team and answer in your presentation:

     4\. Open the \*.fl.png files (you can also open the \*.st.png or \*ln.png - they are the same result in diferent types of plots) for the purged, the haplotigs and the total hicanu you have produced. What is the biggest difference between those three plots?

     5\. Point on \*.fl.png for the purged and hapltoigs where the kmer errors are.

     6\. Point on \*.fl.png for the purged and hapltoigs where the heterozygous peak is, and where the homozygous peak is?

     7\. If you look at \*.fl.png you have generated for the total Hicanu output, in the heterozygous peak you don't see any kmers only present on the reads. On the other hand, if you look at \*.st.png for the purged results, the primary or the haplotigs, you see kmers present only on the reads and absent from the heterozygous peak. Why is that?

     8\. Look at the completeness file for the purged run I have produced: why is the completeness there different from the one you have generated for total hicanu?

     9\. Look at the .qv file for the purged run I have produced: why do you think the qvs are different from the one you have generated for the total hicanu?

Finally, we have discussed that another way of evaluating assemblies is at looking at BUSCO runs for the assemblies. I have generated BUSCO rans for the total Hicanu output, the primary purged assembly and the haplotigs purged assembly. You will find the BUSCO result folders in `~/Share/Data/<your_species>/BUSCO/`. You don't need to copy the whole busco folders, but I want you to go inside each BUSCO run and analyse the short_output*.txt file for each and answer:

     10\. Against which set of protein ortologs have I ran the BUSCO analysis? How many single copy ortholog genes were searched?

     11\. What is the general statistics for the total Hicanu BUSCO ran?

     12\. What is the general statistics for the total primary purged BUSCO ran?

     13\. What is the general statistics for the total haplotigs purged Hicanu BUSCO ran?

     14\. What is the biggest BUSCO difference between the total Hicanu run and the purged assembly?

Discuss all of this with your colleagues and make your presentation.

# Then

Finally, now we are going to look into merqury outpus for *Hemaris fuciformis* CLR assembly with FALCON and FALCON-Unzip. Remember that we have discussed that - unlike Hicanu - Falcon and Falcon Unzip will produce straigh away a primary and an alternate assembly. The primary is the most contiguous haplotype, while the haplotigs are only the phased blocks that differ in the second haplotype of the diploid species. I have also produced a merqury evaluation for the purged Falcon/Falcon-Unzip assembly of *H. fuciformis* and BUSCO runs for the Falcon/Falcon Unzip output, as well as the purged outputs. You will find all the files in `~/Shared/Data/h_fuciformis/`.

Look at all the files (take your time), discuss with your team and write down on your presentation:

- First plot a Illumina kmer profile distribution for your species. I have prepared the .histo file for you (OUTPUT.21.histo). Remember that with PacBio CLR reads you cannot plot kmer distributions because of the high error rate of the reads. But we have some linked chromium 10X reads (illumina) and I have produced the histogram file from them. What is the expected genome size, heterozygosity and repeat content? Analyse this plot and correlate it with the results you will look into in the next questions.

Also remember: the merqury analysis was done comparing kmers in the CLR assemblies with kmers in the Illumina reads (Chromium 10X).

Generate the asmstats for the Falcon/Falcon Unzip output assemblies. Primary and haplotigs are within the merqury_falcon folder and are called cns_p_ctg.fasta cns_h_ctg.fasta. Also, generate the asmstats for both after purging. The assemblies are within merqury_purged and are called purged.fa and purged.htigs.fa. Compare the statistics of the assemblies: what happened after purging? Present these results together with the following questions.

     15\. in the Falcon and Falcon Unzip merqury evaluation, look at the cns.p and cns.h \*.st.png plots. Point in the presentation: (i) where are the assembly erroneous kmers, (ii) what is the heterozygous peak, (iii) what is the homozygoys peak.

     16\. Have a look at the completeness file and write down in your presentation the kmer completness of the primary and alternate assemblies.

     17\. Have a look at the .qv file and write down in your presentation what is the QV for the primary and alternate assemblies.

Now, open the merqury run for the purged versions of *H. fuciformis* and answer the same questions as above.

Then, have a look at the BUSCO results for the Falcon and Falcon Unzip and the purging results and answer the same questions 10, 11, 12, 13 and 14 comparing the Falcon/Falcon Unzip BUSCO run with the purged BUSCO run.

## Finally

Now, I would like you to evaluate the difference in the merqury results for the Hicanu purged run for your species, and for the merqury run for the purged *H. fuciforms*. Of course they are different species, and therefore results will be different. But there is more. Evaluate kmer completeness, QVs, erroneous kmer levels, BUSCO outpus and answer:

     18\. Which assemblies seem to be better taking into consideration the different metrics? Explain.

     19\. Why error rates, QVs and completeness vary between these species assemblies?


# Well done.

You've got to the end of your 'Purging and assembly evaluation' Hands On. Now go back to the wider group with your presentation and let's discuss all the results together. 
