---
title: "Hands On"
layout: archive
permalink: /handsOn_plotReadSize/
---  

it would be nice to check one more thing: the size distribution of our reads!

**Imagine if we have a good genome coverage but our reads are all small? It would not be very useful to assemble across repeats**

So let’s plot the size distribution of our <species>.total.fasta file then:


```console  
python plot_fasta_length.py <species>.total.fasta <species>.total.fasta.length.png
```
This might take a bit of time…

Note: my script plot_reads_length.py and also Shane’s script asmstats are two of many options you can use to plot fasta lengths and generate statistics. Remember, internet is on your side in this journey. While you wait the script to run, have a look at other options: [like this one](https://bioinformatics.stackexchange.com/questions/45/read-length-distribution-from-fasta-file) or the stats from [BBMap](https://github.com/BioInfoTools/BBMap)

Once you have plotted the reads length distribution, download it to your local computer and have a look.
g- How does the reads distribution look like?
h- Which length most of the reads have?

Now, gather all the results you have so far and let’s discuss them as a group!!
