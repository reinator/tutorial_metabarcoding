---
title: "Hands On"
layout: archive
permalink: /day2_2/
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
