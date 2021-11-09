---
title: "Hands On"
layout: archive
permalink: /mitohifi/
---  

## Background

Ok, so on the second day of our course you have assembled the mitogenome of your species with Hifiasm and Hicanu. Well, the contigs are the mitochondria, but they don't represent a final mitochondrial sequences we usually find on databases, right? Firts: for some of you, hifiasm or hicanu is likely to have outputed more than one contig, and second, the contig size if much larger than a mitogenom usually is. True! This happens because of the circular nature of the molecule, and because of how assemblies work! Basically the overlaps of the circular molecule makes the assemblers confused and they end up concatenating the circular molecule many times!

So I have written a pipeline that can finish the assembly of your mitochondria for you! It basically blasts your assembled Pacbio HiFi contigs to close-related species mitogenome, it does a series of parsings to be sure you have a contig that is only the mitogenome and not a NUMT, they it will circularise the contig, cut it and anotate it with MitoFinder.

For more information on MitoHifi, have a look here: [https://github.com/marcelauliano/MitoHiFi](https://github.com/marcelauliano/MitoHiFi)

## Running MitoHiFi with an example dataset

Let's run MitoHiFi using an example dataset. The first thing you will need to do is activate the MitoHiFi conda environment, which has been set up in advance by your instructors and contains some software dependencies used by MitoHiF:

```console  
conda activate mitohifi_env  
```

Now, create a directory that you'll use to run the MitoHiFi analysis (e.g. `mitohifi_test_01`) and move to it.

```console
mkdir mitohifi_test_01
cd mitohifi_test_01/
```

Add MitoFinder to your PATH (this is another software dependency used by MitoHiFi):

```console
export PATH=$PATH:/home/ubuntu/softwares/MitoFinder/  
```

(Optional) You can test if `mitofinder` has been successfully added to your PATH by running the following command and checking if it returns a help message explaining how the mitofinder program is supposed to be run:  

```console
mitofinder -h
```

Add a symbolic link (symlink) to the MitoHiFi script in your current diretory:

```console  
ln -s /home/ubuntu/softwares/MitoHiFi/mitohifi_v2.py  
```

(Optional) You can test if mitohifi symlink has been successfully set by running the help command:  

```console  
python mitohifi_v2.py -h
```  

Copy the `exampleFiles` directory to your current directory. `exampleFiles` contains all input files you'll need to run MitoHiFi.

```console  
cp -r /home/ubuntu/softwares/MitoHiFi/exampleFiles/ .
```

Finally, run MitoHiFi: 

```console  
python mitohifi_v2.py -c exampleFiles/test.fa -f exampleFiles/NC_016067.1.fasta -g exampleFiles/NC_016067.1.gb -t 1 -o 5
```

The pipeline will probably take a few minutes to run. Once it's done, it will output a message saying `Pipeline finished!`.

Questions:
1) What's the meaning of each parameter used to run MitoHiFi? Hint: if in doubt, run `python mitohifi_v2.py -h` and/or check the official MitoHiFi documentation at [github](https://github.com/marcelauliano/MitoHiFi).  
2) Has MitoHiFi succeded creating final mitogenome fasta/genbank files? What are the names of those files?
3) Open the final mitogenome genbank file and answer: i) what's the total length of the mitogenome?; ii) what's the first gene in that mitogenome?
4) Open the `contigs_stats.tsv` file and answer: is there another mitogenome assembly besides the final_mitogenome? What's its ID?
5) Open the other(s) mitogenome assembled and compare it with the final_mitogenome: i) what's its size? ii) what's its first gene? 
 
We can discuss the intermediate results together. =)
