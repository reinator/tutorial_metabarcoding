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

