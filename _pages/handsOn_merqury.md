---
title: "Hands On"
layout: archive
permalink: /handsOn_merqury/
---  

# Part 5 - Merqury - evaluating purging and assembly quality

Ok, today you leanerd about Purge Dups and purging assemblies. You also learned that Hicanu outputs an assembly that is the double of the expected haploid genome size, and that you have to use a tool such as Purge Dups to separate the haplotypes of the assembly. Later, you learned how to evaluate assembly completeness and quality having a look at the shared kmers between the assembly and high-quality reads kmers, such as Illumina. Now you are going to run merqury to evaluate assemblies for your species!

All right, remember yesterday you have assembled a subset of reads for your species, but you have generated statistics for a total-assembly run I have generated previously? This is the file you are going to work on; the total assembly of Hincanu for your species, it will be called something like \*\.hicanu.total.contigs.fasta inside <your_species>/assembly/hicanu.total/. So I would like you to create a folder called merqury_hicanu_eval and copy or sym link your \*\.hicanu.total.contigs.fasta there. Such as:

```console  
mkdir merqury_hicanu_eval
cp <path_to_file>/*.hicanu.total.contigs.fasta merqury_hicanu_eval

```  

Right, so in order to run merqury, you need a meryl datase of the reads you want to compare kmers with the kmers in your assembly. In our case, I have created meryl databases for 10X reads (illumina linked-reads) for your species, and you just need to copy the meryl db folder to your execution folder. So you do:

```console  
cp -vrn /home/unbuntu/Data/merylDB/<your_species>/*OUTPUT.21.meryl merqury_hicanu_eval

```  

It will take a few minutes to copy the database...

Once it's copied, let's run merqury! For that, you need to start our conda enviroment:

```console  
source activate eukaryotic_genome_assembly

```  

Right, as soon as you see it's activated, try:

```console  
./merqury.sh
```  

The help message should show you that in order to run merqury, you need (i) the meryl database (ii) your assembly (one or two, if you have primary and haplotigs. In our case its only one) and (iii) an output name. So inside your merqury_hicanu_eval directory, you will do:

```console  
./merqury.sh *OUTPUT.21.meryl *.hicanu.total.contigs.fasta outHicanu
```  

Great!!

This will take a while to run, so we will go back to the wider group, run another Hands On first, and then you will come back here to finish analysing your merqury outputs.

.... Go back to the group! :) Say "Merqury is running for me!!"

(...) One hour later...

Hello back here!


Right, once you are back here merqury should have finished. If merqury finished succesfully, you should have a variety of files produced in your folder: (i) different plot (.png) files, a <outname>.completeness.stats file and a <outputname>.qv file. I want you to analyse all these files and discuss with your partners. We have seen the theory of merqury kmer analysis in our class today. But it can be a lot to take at the first time. So, in order to investigate your results and answer the exercise questions, have a look here on points 1, 2 and 3 of the reference free QV estimation https://github.com/marbl/merqury/wiki/2.-Overall-k-mer-evaluation.
  
  
Take your time and then produce a presentation with your team showing and explaning: 
 
 
1-) in your hicanu total merqury evaluation, in the plot \*\spectra-asm.st.png, point in the presentation: (i) where are the assembly erroneous kmers, (ii) what is the heterozygous peak, (iii) what is the homozygoys peak.

2-) Have a look at the completeness file and write down in your presentation the kmer completeness of this assembly. 

3-) Have a look at the .qv file and write down in your presentation what is the QV for this assembly.

# Now

Let's have a look at another merqury folder where I have ran a merqury evaluation for your species but after I ran purge_dups on it. This means you are going to have plot files for the purged primary assembly, and for the haplotigs assembly. The results file of this run should be in /home/unbuntu/Data/<your_species>/merqury_purged

Take your time and have a look at it all. Then dicuss with your team and answer in your presentation:

4-) Open the files \*spectra-asm.st.png for the purged, the haplotigs and the total hicanu you have produced. What is the biggest difference between those three plots?

5-) Point on \*spectra-asm.st.png for the purged and hapltoigs where the kmer errors are.

6-) Point on \*spectra-asm.st.png for the purged and hapltoigs where the heterozygous peak is, and where the homozygous peak is?

7-) If you look at \*spectra-asm.st.png you have generated for the total Hicanu output, in the heterozygous peak you don't see any kmers only present on the reads. On the other hand, if you look at \*\spectra-asm.st.png for the primary and the haplotigs you see kmers present only on the reads and absent from the heterozygous peak. Why is that?

8-) Look at the completeness file for the purged ran I have produced: why is the completeness there different from the one you have generated for total hicanu?

9-) Look at the .qv file for the purged ran I have produced: why do you think the qvs are different from the one you have generated for the total hicanu?

Finally, we have discussed that another way of evaluating assemblies is at looking at BUSCO runs for the assemblies. I have generated BUSCO rans for the total Hicanu output, the primary purged assembly and the haplotigs purged assembly. You will find the BUSCO result folders in /home/unbuntu/Data/<your_species>/BUSCO_runs . You don't need to copy the whole busco folders, but I want you to go inside each BUSCO run and analyse the short_output*.txt file for each and answer:

10-) Against which set of protein ortologs have I ran the BUSCO analysis? How many single copy ortholog genes were searched?

11-) What is the general statistics for the total Hicanu BUSCO ran?

12-) What is the general statistics for the total primary purged BUSCO ran?

13-) What is the general statistics for the total haplotigs purged Hicanu BUSCO ran?

14-) What is the biggest BUSCO difference between the total Hicanu run and the purged assembly?

Discuss all of this with your colleagues and make your presentation.

# Then

Finally, now we are going to look into merqury outpus for *Hemaris fuciformis* CLR assembly with falcon. Remember that we have discussed that - unlike Hicanu - Falcon and Falcon Unzip will produce straigh away a primary and an alternate assembly. The primary is the most contiguous haplotype, while the haplotigs are only the phased blocks that differ in the second haplotype of the diploid species. I have also produced a merqury evaluation for the purged Falcon/Falcon-Unzip assembly of *H. fuciformis* and BUSCO runs for the Falcon/Falcon Unzip output, as well as the purged outputs. You will find all the files in /home/unbuntu/Data/H_fuciformis/merqury and /home/unbuntu/Data/H_fuciformis/BUSCO.

Look at all the files (take your time), discuss with your team and write down on your presentation:

- First plot a Illumina kmer profile distribution for your species. I have prepared the .histo file for you. Remember that with PacBio CLR reads you cannot plot kmer distributions because of the high error rate of the reads. But we have some linked chromium 10X reads (illumina) and I have produced the histogram file from them. What is the expected genome size, heterozygosity and repeat content? Analyse this plot and correlate it with the results you will look into in the next questions.

15a-) in the Falcon and Falcon Unzip merqury evaluation, look at the cns.p and cns.h \*\spectra-asm.st.png plots. Point in the presentation: (i) where are the assembly erroneous kmers, (ii) what is the heterozygous peak, (iii) what is the homozygoys peak.

16a-) Have a look at the completeness file and write down in your presentation the kmer completness of the primary and alternate assemblies.

17b-) Have a look at the .qv file and write down in your presentation what is the QV for the primary and alternate assemblies.

Now, open the merqury run for the purged versions of *H. fuciformis* and answer the same questions as above:

15b)

16b)

17b)

Then, have a look at the BUSCO results for the Falcon and Falcon Unzip and the purging results and answer the same questions 10, 11, 12, 13 and 14 comparing the Falcon/Falcon Unzip BUSCO run with the purged BUSCO run.

## Finally

Now, I would like you to evaluate the difference in the merqury results for the Hicanu purged run for your species, and for the merqury run for the purged *H. fuciforms*. Of course they are different species, and therefore results will be different. But there is more. Evaluate kmer completeness, QVs, erroneous kmer levels, BUSCO outpus and answer:

18-) Which assemblies seem to be better taking into consideration the different metrics?

19-) Why error rates, QVs and completeness vary between these species assemblies?


# Well done.

You've got to the end of your Purging and assembly evaluatiom Hands On. Now go back to the wider group with your presentation and let's discuss all the results together. 



