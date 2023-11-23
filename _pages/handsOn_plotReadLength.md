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

Isso pode levar um pouco de tempo. Portanto, se preferir, você pode usar ferramentas como [`nohup`](https://www.ibm.com/docs/en/aix/7.2?topic=n-nohup-command) ou [`tmux`](https://www.redhat.com/sysadmin/introduction-tmux-linux) para executar o processo em segundo plano (por exemplo, `nohup <command> &`).

> Obs: 
> Meu script `plot_fasta_length.py` e também o script `asmstats` do Shane são duas das muitas opções que você pode usar para plotar comprimentos de sequências em arquivos fasta e gerar estatísticas. Lembre-se de que a Internet está ao seu lado nessa jornada. Enquanto espera o script ser executado, dê uma olhada em outras opções: [como esta] (https://bioinformatics.stackexchange.com/questions/45/read-length-distribution-from-fasta-file) ou as estatísticas do [BBMap] (https://github.com/BioInfoTools/BBMap)  

Depois de obter a distribuição do comprimento das leituras, faça o download para o seu computador local (se não lembrar como fazer isso, siga este [tutorial](https://itvgenomics.github.io/gbb_montagem_workshop/logging_on/)) e dê uma olhada.  
a- Qual é a aparência da distribuição de leituras?  
b- Qual é o comprimento da maioria das leituras?  

Agora, reúna todos os resultados que você obteve até agora e vamos discuti-los em grupo!
