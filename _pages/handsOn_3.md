---
title: "Hands On"
layout: archive
permalink: /handsOn_3/
---  

# BLAST (Basic Local Alignment Search Tool)

Last but not least!

I know you have chosen a specific species and you have assembled a partial set of Pacbio HiFi reads for it. Do you think you have just assembled some portions of you species nuclear genome? Or something special? Aren’t you curious? Well, the parameter ‘genomeSize=’ you have used for Hicanu already gives you a hint about what you have assembled. 

But we will do something even more fun to find out. Let’s do a stand-alone BLAST of our assembled contigs (choose one or run for both, as you wish!).

We already have BLAST installed in our server. Try it.

```console  
blast -h
```  

Right. So now we want to BLAST our contigs to find out what they are. This means we need to blast them against a database of sequences we must think are present in our assembly. I have already created a database for you. It’s called <DB.fasta>. So all you have to do to use it is to create this database in the format blast understands and uses it. So you do:


```console  
cp <path/to/database/DB.fasta yourfolder
makeblastdb -in DB.fasta -dtype nucl
```  

Now, list your directory. Have a look. Do you see different files with the database name but with specific blast file extensions?

```console  
ls -ltrh
```  

Now that we have formated our database, let’s run our blast. Blast has many parameters. We are going to run it twice to produce two types of output files. First run to generate a standard output:


```console  
blastn -query *.contigs.fasta -db DB.fasta -out *.contigs.DB.blastn -evalue 1e-05 
```  

Now run it with a output format 6:

```console  
blastn -query *.contigs.fasta -db DB.fasta -out *.contigs.DB.blastn6 -evalue 1e-05 -outfmt 6
``` 

### Attention :grey_exclamation: 

The blast database files and the contigs must be in the same folder. If they aren’t you have some options: (i) you can give absolute paths to specific files, (ii) you can copy files (assembly or database) to the same folder, (ii) you can symlink files. If you get stuck let us know.

# Good! 

So now let’s have a look at our outputs!
1-) Based on your blast results, what have you assembled? (If you don't understand the subject ID, search it on NCBI).
2-) Let’s inspect the differences between the two outputs
3-) What each columns on the output *.contigs.DB.blastn6 mean? (Internet is your friend!)

Discuss this with your colleages and then let's discuss this as a group!

