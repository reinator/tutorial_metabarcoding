---
title: "Hands On"
layout: archive
permalink: /mitohifi/
---  


Ok, so on the second day of our course you have assembled the mitogenome of your species with Hifiasm and Hicanu. Well, the contigs are the mitochondria, but they don't represent a final mitochondrial sequences we usually find on databases, right? Firts: for some of you, hifiasm or hicanu is likely to have outputed more than one contig, and second, the contig size if much larger than a mitogenom usually is. True! This happens because of the circular nature of the molecule, and because of how assemblies work! Basically the overlaps of the circular molecule makes the assemblers confused and they end up concatenating the circular molecule many times!

So I have written a pipeline that can finish the assembly of your mitochondria for you! It basically blasts your assembled Pacbio HiFi contigs to close-related species mitogenome, it does a series of parsings to be sure you have a contig that is only the mitogenome and not a NUMT, they it will circularise the contig, cut it and anotate it with MitoFinder.

For more information on MitoHifi, have a look here: [https://github.com/marcelauliano/MitoHiFi](https://github.com/marcelauliano/MitoHiFi)

Right, so in order to run MitoHifi, you have to have blast and MitoFi on your PATH. So have a look if you have it, if not, call Joāo or myself.

The other thing is to create a sym link to MitoHifi /scripts folder and one for the script run_MitoHifi.sh on your running directory.

Then, you need to find a close related species mitogenome on NCBI and need to download it in fasta and gb file. Upload them to your amazon user folder. 

To run MitoHiFi on your Hicanu contigs:

```console  
sh run_MitoHiFi.sh -c *contigs.fasta -f <NCBI_closerelatedSpecies>.fasta -g <NCBI_closerelatedSpecies>.gb -t 1-o 5' 
```  

To run MitoHiFi on your Hifiasm output, make a new mitogenome folder, and just replace the -c parameter above with your hifiasm contigs.

Once MitoHifi runs, your final mitogenome will be in a fine called mitogenome.fasta

We can discuss the intermediate results together. =)
