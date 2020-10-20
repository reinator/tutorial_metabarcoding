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
