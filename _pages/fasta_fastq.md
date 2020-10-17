---
title: "Fasta and Fastq sequences"
layout: archive
permalink: /fasta_fastq/
---  

# Fasta format

Right, now that you have learn the basic of linux, let's also look at some sequence formats to represent sequenced reads or assembled genome, transcriptome and translated protein data.

The first format we are going to talk about is the fasta format.

![Figure 1](/images/fasta.png)



In the image about you see two DNA sequences in a multifasta file. A fasta sequence is basically a text file where first you see the symbol '>' followed by the ID of the sequence. Then, on the next line you see the nucleotide sequence. If the file is a multifasta file - like in this case - the next line will the symbol '>' again followed by the ID of the second nucleotide sequence, and so on. Fasta sequences can also represent protein sequences. 


# Fastq format

A fastq sequence starts with an ID line that starts with "@". 




### Attention :grey_exclamation: 

Fasta and fastq IDs can be as long as you like. But be careful with length: many algorithms crash with long-read-IDs. Secondly, differently than the image above tha ilustrates a fasta sequence, you should avoid spaces in IDs before you have a unique pattern in the ID. We will see examples of why.


![Figure 2](/images/fastq.jpg)


