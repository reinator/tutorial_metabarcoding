---
title: "Hands On"
layout: archive
permalink: /handsOn_1/
---  

# Kmer analysis: running jellyfish <a name="where-are-we?"></a> 

Right, so today you have heard about how to analyse kmer composition of your genome sequenced reads! Now you are going to put Hands On and will yourself count and analyse kmers.
You have to chose between the species: (i) *Vanessa atalanta*, (ii) *Pieris rapae* and (iii) *Notonda dromedarius* and you will analyse the reads and genome of your chosen species until the end of the week. Once you have chosen it, create a folder where you will run your analysis. My suggestion would be to create a folder with your species name and inside it, a series of other folders to structure your analysis. For example:

v_atalanta/
  kmers/
  assembly/
  
 The above basically means you have created a folder called 'v_atanta' (if you chose vanessa atalanta as your working species) and inside it you have created two other folders side by side called 'kmers' and 'assembly'. If you would like to do that, then do:
 
 ```console  
mkdir <species_folder>
cd <species_folder>
mkdir kmers
mkdir assembly
```  
 
Great, now you need to go and copy the working data for your species. The data will be inside /home/ubuntu/Data

```console  
cd /home/ubuntu/Data
ls -ltr
```  
Do you see the 3 species folder? if you do, then copy the 


This way, everytime you have to use your species data, you refer to the folder data. 

Now that you have all your data in place, try to call Jellyfish:

```console  
jellyfish
``` 

Do you see the help message? Great! (If not, call Joāo!)

Jellyfish has many steps. The first one we want to run is the *count* to count our genome reads kmers. The kmer size we are going to use is 31. 

1-) Jellyfish count

So here comes the command:

```console  
jellyfish count -C -m 31 -s 1000 -t 1 -o <species>.jf <species>.fasta
``` 


### Attention :grey_exclamation: 

In the command line above you see \<species\>.fasta. This needs to be replaced by the fasta file of the species you have chosen. This is just a generic way to point out that a fasta file must be imputed in that position in the command line above. The same with the \<species\>.jf. If your species is Vanessa atalanta, you can choose to have the output (-o) called v_atalanta.jf and this will be your output name.

### More

Please try 

```console  
jellyfish count --help 
```

on your command line to understand what are the parameters you have imputed in the above line. Help messages are a useful way for you to understand what you are running, and to see if you would like to add any other parameter for your specific analysis case. Also remember that beyond this course, the internet is always on your side. If you google ‘jellyfish user guide’, for example, you will find [JellyfishUserGuide]( http://www.genome.umd.edu/docs/JellyfishUserGuide.pdf)

### Back

2-) Jellyfish histo

Now that you have counted our 31 letters kmers, we want to transform it to a histogram file so we can plot it. Then we have our second command:


```console  
jellyfish histo <species>.jf > <species>.jf.histo

```

### Attention :grey_exclamation: 

Note in the command above we have used the symbol “>” before the output. This is a command line symbol that will redirect your output to a file instead of printing it to the screen.

Note that the input for your command **jellyfish histo** is the output from your previous command, which was **jellyfish count**. Now you have the necessary result to plot a histogram on genomescope and have a look at the distribution of your genome kmers. But before you plot this result, I want you to plot a genomescope plot for another file FIRST!! 

In the data folder for the species you have chosen, you are going to find two files called:

```console  
<species>.total.fasta
<species>.total.histo
```

Download the file \<species\>.total.histo to your local machine (as you learned yesterday), go to the [Genomescope]http://qb.cshl.edu/genomescope/ page and upload the file there. You should change the **Description** to the name of your species, and the **kmer** to 31. Then plot.

Save the image of both versions of the plot - normal and log scale - somewhere in your computer.

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

d- Taking into consideration the estimated genome size, and the statistics of the total reads you have just generated, how much reads coverage you have to assemble this genome?


Now, 

I want you to go back to the *.histo* file you have generated today, download it to your local machine and plot it on genomescope. Also, I want you to run asmstats on the fasta file (the 600 subset) you imputed to jellyfish. 

e- What genomescope tells you when you try to plot a kmer histogram for just a handful of sequences? 
f- Looking at the asmstats result for this smaller file, how much coverage of the genome you have in this file giving the estimated genome size?

Great. Now let’s look at it all together: considering the kmer plot of the total file and its statistics, we can have a good look at the kmer composition of the DNA in the genome. How does it look? Discuss with your partners and then later in the big group.  


