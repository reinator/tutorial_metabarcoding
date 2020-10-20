---
title: "Hands On"
layout: archive
permalink: /handsOn_2/
---  

# Assembling genomes

Right, so here we are! Let’s assemble the species you have chosen. You are going to run two assemblers for Pacbio HiFi data: Hicanu and Hifiasm.

Have a look at their websites:


[Hicanu](https://github.com/marbl/canu/releases/tag/v2.1)

[Hifiasm](https://github.com/chhylp123/hifiasm)

Now let’s run the assembly on our subsamples:

Let’s create a folder for each assembly we are going to run, as both assemblers create a lot of different outputs:

```console  
mkdir hicanu
mkdir hifiasm
```  

Now let’s change to the hicanu folder, let’s copy our data there and run our assembly. 
But… before you run these 3 steps, let’s just call canu in your command line:


```console  
canu
```  

This will print you all the parameters that one can use to run canu. So have a look at the parameters in your screen and compare with the ones below on the command you will run:


```console  
cd hicanu
cp data/<species>.fasta .
canu -d <species_subset> -p <species_id> genomeSize=16000 -pacbio-hifi <species>.fasta useGrid=false

```  
  
  ### Attention :grey_exclamation: 

For the copy line you need to give the whole path to the ‘data’ folder. I just wrote *data/\<species>\.fasta* to make it short. If you are unsure about the whole PATH to 'data', go back to ‘data’ and run **pwd** on your commandline. This will print you the whole path for the folder you are currently at. Then copy this PATH and go back to the folder ‘hicanu’. And now type your command: *cp whole_path_of_data/\<species>\.fasta .* This line basically means: I’m copying the \<species>\.fasta file all the way from the data folder to here (here is represented by the dot).


Right, so let’s wait for Hicanu to run. While we do that, let’s put hifiasm to run!

In a second tab, let’s change to the hifiasm folder and copy our data there:

```console  
cd hifiasm
cp data/<species>.fasta .

```

Note: because we have a small dataset, we can copy the reads file to different folders. But if you had a large file, it would be better to create a [symbolic link](https://kb.iu.edu/d/abbe) or give the assemblers the whole PATH to the files.

Now let’s call hifiasm and have a look at the parameters it prints:


```console  
hifiasm

```
And this is the line we will run:


```console  
hifiasm -t1 -o <species>.hifiasm <species.fasta>

```

Let’s wait a few minutes for both assemblers to run.

## Interpreting our results

Each assembler will output different intermediate files together with the final assembly result. 

1-) Hifiasm

Let’s look at the Hifiasm result first:


```console  
pwd
ls -ltrh
```

Am I in the hifiasm folder? If not, then I need to change there

Among the results hifiasm produced, you will find the **.p_ctg.gpa** file. This is our assembly output file. Hifiasm gives us the [assembly graph](http://gfa-spec.github.io/GFA-spec/GFA1.html) as an output. This means we need to  convert the graph into a fasta file. For that, we have a awk script:


```console  
gfa2fa *.p_ctg.gpa > *.p_ctg.fa

```

Right. So now, what to do with the assembly file?
Well, first we should have a look at the statistics for this assembly. Let’s run out asmstats script on it

```console  
asmstats *.p_ctg.fa > *.p_ctg.fa.stats

```

2-) Hicanu

Now, let’s move to the hicanu folder and let’s have a look at the results.


```console  
pwd
ls -ltrh

```

Differently than Hifiasm, Hicanu is going to give you a fasta file at the end. It’s called * *.contigs.fasta.* So, go on and generate the statistics for this result:

```console  

asmstats *.contigs.fasta > *.contigs.fasta.stats

```

## WELL DONE!
You have just done eukaryotic genome assembly using PacBio HiFi reads and two different assemblers! **That is fantastic!**

Before you go back to the group, I want you to gather the statistics results of different files:

1-) The statistics of the raw reads you have used as input for your assembly.

a- How many reads are there?

b- What is their average length?

OBS: remember you already have these results as we have generated them in the previous Hands On session.

2-) The statistics of Hicanu and Hifiasm assembled files.

a-) Have both assemblers assembled exactly the same number of contigs?

b-) What are the assembly statistics: N50, total assembled size, contig counts ...


# BEFORE YOU GO BACK TO THE GROUP

As you know, because of time and computer resources, we have assembled only a subset of reads for the species you have chosen. But I have generated previous assemblies for the complete set of reads, and I would like you to generate assembly statistics for those assemblies. The files will be on the species folder and will be called <species>.hicanu.total.contigs.fasta and <species>.hifiasm.total.fasta. Copy the files to your directory and run asmstats on them. Then answer:
  
  1-) What is the assembled size, number of contigs and N50 for the hicanu assembly? 
  1a-) Is the Hicanu result close to the estimated genome size? Why?
  
  2-) Hifiasm generates two files, *p*.contigs.fasta and *a*.contigs.fasta. Why? What are the assembly metrics for these two files?
  


Now gather all these results, let’s go to the larger group and let’s discuss them together!



