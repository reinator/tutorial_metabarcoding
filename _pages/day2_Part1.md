---
title: "Linux: navigating the system"
layout: archive
permalink: /day2_1/
---  

## Kmer analysis: running jellyfish <a name="where-are-we?"></a> 

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


So here comes the command:

```console  
jellyfish histo -C -m 31 -s 1000 -t 1 -o <species>.jf <species>.fasta
``` 


### Attention :grey_exclamation: 

In the command line above you see \<\species\>\.fasta. This needs to be replaced by the fasta file of the species you have chosen. This is just a generic way to point out that a fasta file must be imputed in that position in that command line above. The same with the <species>.jf. If your species is Vanessa atalanta, you can choose to have the output (-o) called v_atalanta.jf and this will be your output name. .
