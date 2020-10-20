---
title: "Hands On"
layout: archive
permalink: /handsOn_4/
---  

# Mapping and IGV

Mapping and dealing with samtools and IGV.

Right, so yesterday we have generated statistics for our raw data, have assembled it with two different assemblies and have even done a BLAST search to try to identify what we have assembled. Those are all good metrics to check our assembly. Another metric commonly used is to map all the reads back to our assembly and determine the percentage of reads mapping back to it. As this was the data we used to assemble the contigs, we want that most of it is mapped back, if not, it raises a red flag to us about the sanity of our assembly. So let’s learn how to use two new tools: minimap2 and samtools.

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

Right. As soon as it finishes, we are going to use a tools called samtools to manipulate the output file

```console  
samtools view -h -Sb outputname_you_chose.sam -o outputname_you_chose.bam
samtools sort outputname_you_chose.bam -o outputname_you_chose.sorted.bam
Samtools index outputname_you_chose.sorted.bam
``` 
Right. So what we did above was to convert the output mapped file from the format sam to bam, then we sorted this file and then we created an index for this file. This will be a standard procedure most of the time that you will be producing a mapping. 
To know more about samtools: https://samtools.github.io

Now, we want to visualize one contig with the reads mapped to back to it. So we need to extract one contig from the *.sorted.bam file which contains all contigs assembled. 

So let’s select the pattern common to a fasta file “>” and list the name of our contigs

```console  
grep “>” your_contigs.here.fasta 
```  

This will print to the screen the names of all your assembled contigs. Choose one and create a file with this ID. Let’s say my grep result looks like this:

>Contig1
>Contig2

So here I’ll choose ‘Contig1’. To create a file with this ID I can use nano.

```console  
nano contig_id
```  

Nano will open a black file for you. Inside it type the name of the contig you have chosen, if my case this will be Contig1. Then to close and save the file in a Mac you do Control + O Control + X (control O control X). 

Now, let’s run our script which will extract that contig from our assembly result:

```console  
python filterfasta.py -i contig_id your_contigs.here.fasta > *ID.fasta
```  

