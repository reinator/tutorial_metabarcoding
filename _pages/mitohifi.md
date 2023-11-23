---
title: "Hands On"
layout: archive
permalink: /mitohifi/
---  

## Background

Ok, so on the second day of our course you have assembled the mitogenome of your species with Hifiasm and Hicanu. Well, the contigs are the mitochondria, but they don't represent a final mitochondrial sequences we usually find on databases, right? Firts: for some of you, hifiasm or hicanu is likely to have outputed more than one contig, and second, the contig size if much larger than a mitogenom usually is. True! This happens because of the circular nature of the molecule, and because of how assemblies work! Basically the overlaps of the circular molecule makes the assemblers confused and they end up concatenating the circular molecule many times!

So we have written a pipeline that can finish the assembly of your mitochondria for you! It basically blasts your assembled Pacbio HiFi contigs to close-related species mitogenome, it does a series of parsings to be sure you have a contig that is only the mitogenome and not a NUMT, they it will circularise the contig, cut it and anotate it with MitoFinder.

For more information on MitoHifi, have a look here: [https://github.com/marcelauliano/MitoHiFi](https://github.com/marcelauliano/MitoHiFi)

## Setting up the environment for running MitoHiFi  
At your home directory, create 3 directories to work on MitoHiFi today and move to it:  

```console  
mkdir ~/mitohifi_ilDeiPorc1/
mkdir ~/mitohifi_bCygCol1/
mkdir ~/mitohifi_cbCliDend2/
```
Copy specific data to the respective folders. Data is here: ```/mnt/gen/temp/workshop_montagem_gbb/data/MitoHiFi ```

We are going to run this session together with Marcela. The commands we are going to run are bellow:

Let's assemble something pink
```
findMitoReference.py --species "Deilephila porcellus" --outfolder . --min_length 14000

mitohifi.py -r ilDeiPorc1.reads.100.fa -f NC_079697.1.fasta -g NC_079697.1.gb -t 1 -o 5
```

Let's do a bird

```
findMitoReference.py --species "Cygnus columbianus" --outfolder . --min_length 14000

mitohifi.py -c bCygCol1.hifiasm.contigs.fa -f NC_007691.1.fasta -g NC_007691.1.gb -o 2 -t 3
```

Let's do a plant

```
findMitoReference.py --species "Climacium dendroides" --outfolder . --min_length 50000

mitohifi.py -c cbCliDend2.hicanu.contigs.fa -f NC_053886.1.fasta -g NC_053886.1.gb -t 6 -o 1 -a plant
```

Questions:  
1) What's the meaning of each parameter used to run MitoHiFi? Hint: if in doubt, run `python mitohifi.py -h` and/or check the official MitoHiFi documentation at [github](https://github.com/marcelauliano/MitoHiFi).    
2) Has MitoHiFi succeded creating final mitogenome fasta/genbank files? What are the names of those files?  
3) Open the final mitogenome genbank file and answer: i) what's the total length of the mitogenome?; ii) what's the first gene in that mitogenome?  
4) Go to BLAST [webserver](https://blast.ncbi.nlm.nih.gov/Blast.cgi) and do a blastn of the final mitogenome fasta file (`final_mitogenome.fasta`) against the Nucleotide collection (nr/nt). What's the first hit you get from the alignment? What species does that hit come from? Click on the hit accession number hyperlink. You should be redirected to a new page. Go to the `COMMENT` section and answer: how was this sequence assembled?    
5) Open the `contigs_stats.tsv` file and answer: is there another mitogenome assembly besides the final_mitogenome? 
 
We can discuss the results together. =)
