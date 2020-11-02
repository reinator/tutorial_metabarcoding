---
title: "Hands On"
layout: archive
permalink: /curated/
---

# Final results

Right guys, so here we are. I don't know if you realize you have come a long way this week. You have learned:

(i) how to count and plot Kmers to understand genome composition (heterozygosity, genome size, repeat content)

(ii) you have assembled your genome with 2 different softwares

(iii) you have learned about purging genomes to (i) separated haplotypes or (ii) exclude retained haplotypes

(iv) you have learned how to evaluate genome quality with (i) kmers (Merqury, (ii) mapping (samtools, IGV) , (iii) general statistics and (iv) busco

(v) you have learned how to scaffold genomes with Hi-C data and SALSA2

(vi) you have heard of genome polishing and curation

(vii) you have learned how to run stand alone BLAST

Look at that? Thats is A LOT! WELL DONE!

This material will be always here for you to come back to it and consolidate your knowlegde, and you can ALWAYS email me with questions; it will be lovely to hear from you.

# Now,

It's time for you and your team to gather all the results and make a final presentation. I have some extra results for your species: it's the final curated primary assembly and its haplotypes (not curated). So you have the curated results, a merqury and BUSCO ran for it and the final curated Hi-C heatmap. So I want you to gather ALL the results for your species and make a final presentation answering all the questions bellow:

1-) What is the name of your species? And what else have you learned online for it (do a small search to find a picture and maybe some interesting evolutionary facts about it)?

2-) What is the genomescope plot for the total Pacbio Hifi reads histogram? What is the expected genome size? What is the expected heterozygosity? What is the repeat content?

3-) How does the reads plot length distribution looks like? What is the average read length that was inputted to assembly?

4-) What are the statistics for the Hicanu total reads output? How do the merqury plots look like? What is the qv? The completeness? How does busco looks like?

5-) What are the statistics for the purged results for primary and haplotigs? How do the merqury plots look like? What are the qvs? Completeness? How does busco looks like for the primary assembly?

Now, let's go to the scaffolding part. One note: in the official Darwin Tree of Life Pipeline, we have ran one round of Illumina polishing after purging the assembly and before running salsa on it. This is why maybe you are going to find a slightly different number of bases in the statistics of the assembly after purging, and just before salsa (which is file ref.fa).

6-) What is the primary genone statistics just before salsa scaffolding? How does the Hi-C heat map looks like?

7-) What is the primary genone statistics after salsa scaffolding? How does the Hi-C heat map looks like?

8-) What is the primary genone statistics after manual curation? How does the Hi-C heat map looks like? Has BUSCO changed at all?

9- What is the QV diference of the primary genome after purging and the version just before salsa scaffolding?

10-) For the subset of reads you have assembled for your species. Which kind of reads were they? What have you assembled there?

11-) What were the mapping statiscs when you mapped the 600 reads back to the assembly?

WELL DONE!

You have a robust knowlegde and skill set to perform eukaryotic genome assembly using Pacbio HiFi and Hi-C. Looking at kmer profiles and Hi-C heatmaps takes practice and time. So, just keep doing it and you will become more confident with time. 


# Right, 

So during this week you have also evaluated a genome what was assembled with Pacbio CLR reads. We also have a curated version of this assembly, a merqury, a BUSCO ran and a Hi-C heat map for it. Produce a presentation with all these results - including the final curated results - answering all the questions abobe also for *H. fuciforms*. You have a lot of these results already done from the previous hands on.


