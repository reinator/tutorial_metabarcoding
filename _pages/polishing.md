---
title: "Hands On"
layout: archive
permalink: /polishing/
---  

# Polishing CLR assembly

Ok, we have talked a little about polishing and how much polishing is still vital if you are working with PacBio CLR reads, that can have up to 15% of errors. Now, you are going to investigate the impacts of polishing on the *H. fuciforms* genome, that was assembled with PacBio CLR reads as part of the [25 Genomes Project of the Sanger Institute](https://www.sanger.ac.uk/collaboration/25-genomes-for-25-years/)  


For such, you are going to compare some statistics for *H. fuciforms* before polishing, after polishing and after manual curation done by the [GRIT](https://www.sanger.ac.uk/group/genome-reference-informatics-team/) Team at the Sanger Institute. The stats I want you to compare are: 

* Merqury completeness and QV    
    * Those files are located in the `merqury_before_polishing`, `merqury_after_polishing` at  `~/Share/Data/h_fuciforms/polishing/`
* General statistics  
    * For that you will need to run the `asmstats` script for the FASTA (\*.fasta or \*.fa) files located at each of the three merqury directories (`merqury_before_polishing`, `after_polishing` and `after_manual_curation`)  
    * For before polishing, you should have two FASTAs:    
        * iHemFuc1.primary.BF.fa.gz - this is the primary assembly before polishing (BF)
        * iHemFuc1.htigs.BF.fa.gz - this is the haplotigs assembly before polishing (BF)
    * For after polishing, you should also have two FASTAs:    
        * iHemFuc1.prim.polished.fa.gz - this is the primary  
        * iHemFuc1.htigs.polished.fa.gz - this is the haplotigs  
    
* BUSCO  
    * BUSCO's results can be found at `~/Share/Data/h_fuciforms/BUSCO`, in the folders `run_before_polishing.busco`, `run_after_polishing.busco` 


Not look at all the results and answer:

1. What were the general statistics (number of scaffolds, total assembled size, N50) for before and after polishing?

2. Has the QVs improved with polishing?

3. Has BUSCO changed before and after-polishing?

Make one slide with all the information you have analysed here.


