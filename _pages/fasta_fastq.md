---
title: "Fasta and Fastq sequences"
layout: archive
permalink: /fasta_fastq/
---  

# Fasta format

Right, now that you have learn the basic of linux, let's also look at some sequence formats to represent sequenced reads or assembled genome, transcriptome and translated protein data.

The first format we are going to talk about is the fasta format.

![Figure 1](/images/fasta.png)



In the image about you see two DNA sequences in a multifasta file. A fasta sequence is basically a text file where first you see the symbol '>' followed by the ID of the sequence. Then, on the next line you see the nucleotide sequence. If the file is a multifasta file - like in this case - the next line will the symbol '>' again followed by the ID of the second nucleotide sequence, and so on. Fasta sequences can also represent protein sequences, such as bellow. 
