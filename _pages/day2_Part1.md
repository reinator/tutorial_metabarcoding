---
title: "Linux: navigating the system"
layout: archive
permalink: /day2_1/
---  

# Kmer analysis: running jellyfish <a name="where-are-we?"></a> 

Go to the folder with the data you have chosen to assemble
  
```console  
ls -ltrh
```  
Do you see all your files there? Great! Now call Jellyfish:

```console  
jellyfish
``` 

Do you see the help message? Great! If not, call Joāo!

Jellyfish has many steps. The first one we want to run is the *count* to count our genome reads kmers. The kmer size we are going to use is 31. 

1-) Jellyfish count

So here comes the command:

```console  
jellyfish count -C -m 31 -s 1000 -t 1 -o <species>.jf <species>.fasta
``` 


### Attention :grey_exclamation: 

In the command line above you see \<species\>.fasta. This needs to be replaced by the fasta file of the species you have chosen. This is just a generic way to point out that a fasta file must be imputed in that position in that command line above. The same with the \<species\>.jf. If your species is Vanessa atalanta, you can choose to have the output (-o) called v_atalanta.jf and this will be your output name.

### More

Please try 

```console  
jellyfish count --help 
```

on your command line to understand what are the parameters we have imputed in the above line. Help messages are a useful way for you to understand what you are running, and to see if you would like to add any other parameter for your specific case. Also remember that beyond this course, the internet is always on your side. If you google ‘jellyfish user guide’, for example, you will find [JellyfishUserGuide]( http://www.genome.umd.edu/docs/JellyfishUserGuide.pdf)

### Back

2-) Jellyfish histo

Now that we have counted our 31 letters kmers, we want to transform it to a histogram file so we can plot it. Then we have our second command:


```console  
jellyfish histo <species>.jf > <species>.jf.histo

```

### Attention :grey_exclamation: 

Note in the command above we have used the symbol “>” before the output. This is a command line symbol that will redirect your output to a file instead of printing it to the screen.

Note that the input for your command **jellyfish histo** is the output from your previous command, which was **jellyfish count**. Now you have the necessary result  to plot a histogram on genomescope and have a look at the distribution of your genome kmers. But before you plot this result, I want you to plot a genomescope plot for another file. 

In the data folder for the species you have chosen, you are going to find two files called:

```console  
<species>.total.fasta
<species>.total.histo
```

Download the file \<species\>.total.histo to your local machine (as Joāo has shown us yesterday), go to the [Genomescope]http://qb.cshl.edu/genomescope/ page and upload the file there. You should change the **Description** to the name of your species, and the **kmer** to 31. Then plot.

Sabe the image of both versions of the plot - normal and log scale - somewhere in your computer.

Cool, you have plotted the kmer distribution of the \<species\>.total.histo file, and the model of genome scope has calculated for your (i) the estimated genome size, (ii) the heterozygosity and (iii) the percentage of repeats of your genome. 

Now, take the file \<species\>.total.fasta and run the command:


```console  
asmstats <species>.total.fasta > <species>.total.fasta.stats
```

Note: We are calling your output file \<species\>.total.fasta.stats

Once the command finishes to run, have a look at the output:

```console  
less <species>.total.fasta.stats
```

You have now generated the kmer plot and reads statistics for your complete PacBio HiFi read set. Which conclusions can you now draw from these results?


a- What is the expected genome size?

b- What is the estimated heterozygosity?

c- What is the estimated repeat content?

d- How much coverage -  in base pairs (bp) - we have taken into consideration to estimate the genome size and the reads statistics?


Now, 

I want you to go back to the *.histo* file you have generated today, download it to your local machine and plot it on genomescope. Also, I want you to run asmstats on the fasta file you used to count kmers. 

e- What genomescope tells you when you try to plot a kmer histogram for just a handful of sequences? 
f- Looking at the asmstats result for this smaller file, how much coverage of the genome you have in this file giving the estimated genome size?

Great. Now let’s look at it all together: considering the kmer plot of the large file and its statistics, we can have a good look at the kmer composition of the genome and we can see that our two peak diploid distribution seems regular. It seems like we have a good data set for assembly!!

Well, 

it would be nice to check one more thing: the size distribution of our reads!

••Imagine if we have a good genome coverage but our reads are all small? It would not be very useful to assemble across repeats.•• 
