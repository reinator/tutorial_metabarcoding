---
title: "Hands On"
layout: archive
permalink: /handsOn_plotReadLength/
---  

Em nosso tutorial anterior, geramos uma distribuição de kmer k=31 para um subconjunto de leituras e analisamos a mesma distribuição de kmer k=31 para o total de leituras sequenciadas para a espécie escolhida. Com o GenomeScope de nossos resultados totais, estimamos o tamanho do genoma, a heterozigosidade e o conteúdo de repetição. Agora, estamos prontos para montar essas leituras. 

Antes disso, seria bom verificar mais uma coisa: a distribuição de tamanho de nossas leituras!

**Imagine se tivermos uma boa cobertura do genoma, mas nossas leituras forem todas pequenas? Não seria muito útil fazer a montagem entre as repetições**

Portanto, vamos plotar a distribuição de tamanho do nosso arquivo <species>.css.total.fasta usando um script python chamado `plot_fasta_length.py`. 
Coloque o comando abaixo em um arquivo `.pbs`, ou copie o seguinte arquivo para o seu diretório `/mnt/gen/temp/workshop_montagem_gbb/pbs/job_plot_fasta_length.pbs`
```console  
python /mnt/gen/temp/workshop_montagem_gbb/scripts/plot_fasta_length.py <species>.ccs.total.fasta.gz <species>.ccs.total.fasta.length.png
```

Em seguida, submeta o arquivo `.pbs` para a fila op1.
```console  
qsub -q op1 job_plot_fasta_length.pbs
```

This might take a bit of time. So if you prefer, you can use tools such as `nohup` or `screen` to run the process in the background (e.g. `nohup <command> &`).

> Note: 
> My script `plot_fasta_length.py` and also Shane’s script `asmstats` are two of many options you can use to plot fasta lengths and generate statistics. Remember, internet is on your side in this journey. While you wait the script to run, have a look at other options: [like this one](https://bioinformatics.stackexchange.com/questions/45/read-length-distribution-from-fasta-file) or the stats from [BBMap](https://github.com/BioInfoTools/BBMap)  

Once you have plotted the reads length distribution, download it to your local computer and have a look.  
a- How does the reads distribution look like?  
b- Which length most of the reads have?  

Now, gather all the results you have so far and let’s discuss them as a group!!
