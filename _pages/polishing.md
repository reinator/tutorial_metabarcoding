---
title: "Hands On"
layout: archive
permalink: /polishing/
---  

# Polishing and last checks

Ok, so today you learned about the need to polish genomes, specially if they are produced with PacBio CLR reads, that can have up to 15% of errors. Now, you are going to investigate the impacts of polishing on the *H. fuciforms* genome, that was assembled with PacBio CLR reads.  


For such, you are going to compare some statistics for *H. fuciforms* before polishing, after polishing and after manual curation done by the [GRIT](https://www.sanger.ac.uk/group/genome-reference-informatics-team/) Team at the Sanger Institute. The stats I want you to compare are: 

i. Merqury completeness and QV  
    * Those files are located in the `merqury_before_polishing`, `after_polishing` and `after_manual_curation` directories, at `~/Share/Data/h_fuciforms/polishing/`
ii. general statistics  
    * For that you will need to run the `asmstats` script for the FASTA (\*.fasta or \*.fa) files located at each of the three directories mentioned in the previous step (`merqury_before_polishing`, `after_polishing` and `after_manual_curation`)
    * For before polishing, you should have two FASTAs:  
        * iHemFuc1.PB.asm1.purge2.scaff1_HiC.fasta - this is the primary assembly 
        * purged.htigs.fa - this is the haplotigs assembly  
    * For after polishing, you should also have two FASTAs:  
        * iHemFuc1.PB.asm1.purge2.scaff2.polish3.fa - this is the primary  
        * iHemFuc1.PB.asm1.purge2.scaff2.polish3.haplotigs.fa - this is the haplotigs  
    * Finally, for the manually curated, you should have only one FASTA file, because only the primary assembly has been curated:  
        * iHemFuc1_1.20200728.curated_primary.fa
iii. BUSCO  
    * BUSCO's results can be found at `~/Share/Data/h_fuciforms/BUSCO`, in the folders `run_before_polishing.busco`, `run_after_polishing.busco` and `run_manually_curated.busco` 


Not look at all the results and answer:

1. What were the general statistics (number of scaffolds, total assembled size, N50) for pre, post polishing and after curation?

2. Has the QVs improved with polishing?

3. Has QV improved with curation?

4. Has BUSCO changed pre, post-polishing and after curation?


# Finally

Considering the curated assembly, I would like you to count the size of each scaffold. You can use my python script for such.

First, copy both the script and the curated assembly to your working directory:  

```bash  
cp /home/ubuntu/softwares/scripts/fastaLength_1.py .  
cp ~/Share/Data/h_fuciforms/polishing/merqury_after_manual_curation/iHemFuc1_1.20200728.curated_primary.fa .
```

Now run the script:

```console  
python fastaLength_1.py iHemFuc1_1.20200728.curated_primary.fa iHemFuc1_1.20200728.curated_primary.sizes
```  

This script is going to output a 2 columns file, where the first column indicates the scaffold name, and the second column indicates the total size of that scaffold in base pairs. Now, sort this file by the second column to present scaffolds from the largest to the smallest:

```console  
sort -n -k2 -r iHemFuc1_1.20200728.curated_primary.sizes > iHemFuc1_1.20200728.curated_primary.sizes.sorted
```  

You can try the command bellow to have a look at what you have just ran above (what do `-r`, `-k2` and `-n` mean?)
```console  
sort --help
```


Ok, so now that you have the \*sizes file sorted, I would like you to calculate how much of the base pairs in this assembly are in the expected karyotype of the species. How to do that?

- search online to see if you find any research that has described the karyotype of *H. fuciforms*. If you find it, what is the expected karyotype?

Now, sum up the bases in the first largest scaffolds that correspod to the karyotype:   

     5\. How many assembled bases are inside the expected karyotype?      
    
     6\. How many bases were not asigned to chromosomes? 

     7\. Do you have any large scaffolds outside the expected number of chromosomes?
