---
title: "Hands On"
layout: archive
permalink: /handsOn_4/
---  

# Mapping and IGV

Mapping and dealing with samtools and IGV.

Right, so yesterday we have generated statistics for our raw data, have assembled it with two different assemblers and have even done a BLAST search to try to identify what we have assembled. Those are all good metrics to check our assembly. Another metric commonly used is to map all the reads back to our assembly and determine the percentage of mapping. As this was the data we inputted to assemble the contigs, we want that most of the reads mapped back to it, if not, it raises a red flag to us about the sanity of our assembly. So let’s learn how to use two new tools: minimap2 and samtools.

Choose one of your two assembly results (or run for both) and go to your folder.
Identify the raw reads you have used to produce that assembly
Identify the assembly file
And let’s run minimap2 (remember, the internet is your friend). Try:

  
```console  
minimap2
```  

See the help message? Then let’s run it:

```console  
minimap2 -t 1 --secondary=no -ax map-pb your_contigs.here.fasta raw.reads.here.fasta -o outputname_you_chose.sam
```  

Right. As soon as it finishes, we are going to use a tool called samtools to manipulate the output file:

```console  
samtools view -h -Sb outputname_you_chose.sam -o outputname_you_chose.bam
samtools sort outputname_you_chose.bam -o outputname_you_chose.sorted.bam
Samtools index outputname_you_chose.sorted.bam
``` 
Right. What we did above was to convert the output mapped file from the format sam to bam, then we sorted this file and created an index for it. This will be a standard procedure most of the time that you will be producing and visualizing a mapping: samtools view, sort and index.
To know more about samtools: https://samtools.github.io

Now, we want to visualize one contig with the reads mapped to back to it. So we need to extract one contig from the \*.sorted.bam file that contains mappings for all contigs assembled. To use IGV we need to visualize one contig at a time. The steps are:

1-) Extract a bam file for one contig from outputname_you_chose.sorted.bam and make a samtools index for it
2-) Extract the fasta file for the contig you chosen and make a samtools faidx for it

Bellow you see the steps detailed:

Let's get the fasta first:
So let’s select the pattern common to a fasta file “>” and list the name of our contigs

```console  
grep “>” your_contigs.here.fasta 
```  

This will print to the screen the names of all your assembled contigs. Choose one and create a file with it's ID. Let’s say my grep result looks like this:

\>Contig1

\>Contig2

So here I’ll choose ‘Contig1’. To create a text file with this ID. I can use nano. I need a text file with the ID because the next script we are going to use to extract the contig needs this as an input. 

```console  
nano contig_id
```  

Nano will open a empty file for you. Inside it type the name of the contig you have chosen, in my case this will be Contig1. Then to close and save the file in a Mac you do Control + O Control + X (control O control X).

Now, let’s run our script that will extract that contig from our assembly result:

```console  
python filterfasta.py -i contig_id your_contigs.here.fasta > *ID.fasta
```  

Right. Now give a less to the file *ID.fasta

```console  
less *ID.fasta
``` 
And let's create an index for our fasta as well

```console  
samtools faidx *ID.fasta
``` 

If you list your directory now, do you see a \*ID.fasta.fai file there as well? Great!

Extract a bam file only for this contig and create a index for it

```console  
samtools view -b -h outputname_you_chose.sorted.bam “*ID.fasta” > *ID.fasta.bam
samtools index *ID.fasta.bam
``` 

Now you have four files you must download to your local machine to open them on IGV

Your contig fasta file
Your contig fasta.fai file
Your contig bam file
Your contig bam.bai file

Take your time…

On IGV, on the top, click ‘Genomes’ and add your fasta file. Then on ‘File’, “Learn from file’ include your bam file. And… you are done!!!

Let’s discuss IGV as a group. 

# Further

But, how can I see how many reads have mapped to all my contigs? 
A few ways.
Minimap2 would have printed you some log files containing that info
You can also run samtools flagstat.

```console  
samtools flagstat outputname_you_chose.sorted.bam
samtools flagstat *ID.fasta.bam
``` 

# GOOD!


Now that you know all about how to open bam files on IGV, I would like you to open another contig. This is a bam file for the mitogenome of another Lepidoptera, but it was produced with PacBio CLR data. Download to your local computer:

iHemFuc1_MT_16012020.fa
iHemFuc1_MT_16012020.fa.fai
iHemFuc1_MT.sorted.bam
iHemFuc1_MT.sorted.bam.bai

Now open it on IGV

What do you see? What is the mean difference in the IGV plots of your PacBio HiFi assembled contig and the CLR assembled contig?

Let’s discuss it!

