---
title: "Submetendo jobs na fila do cluster"
layout: archive
permalink: /submitting_jobs/
---

Para mantermos organizado o ambiente computacional que compartilhamos com todo o Instituto, utilizamos o sistema [Torque PBS](https://hpc-wiki.info/hpc/Torque) 
Este sistema permite que todos os processos que precisam de recursos de processador e memória do cluster Superdome fiquem organizados em uma fila de processamento e de fácil monitoramento.

### Arquivo PBS
Todo comando que precise de recursos de processamento e memória não pode ser rodado diretamente do terminal. O comando precisa estar primeiramente dentro de um arquivo `.pbs`, cuja estrutura você pode verificar abaixo:

```shell
#PBS -l nodes=1:ppn=8
#PBS -N jellyfish
#PBS -o jellyfish.log
#PBS -e jellyfish.err

CORES=$[ `cat $PBS_NODEFILE | wc -l` ]
NODES=$[ `uniq $PBS_NODEFILE | wc -l` ]

printf "Inico: `date`\n";
TBEGIN=`echo "print time();" | perl`

printf "\n"
printf "> Executando demultiplexacao\n";
printf "> Rodando em $CORES nucleos, em $NODES nos\n"
cd $PBS_O_WORKDIR

##########INSIRA SEU COMANDO ABAIXO##########################
jellyfish count -C -m 31 -s 1000 -t 1 -o drUrtUren1.jf drUrtUren1.600.fasta
#############################################################

TEND=`echo "print time();" | perl`

printf "\n"
printf "Fim: `date`\n";
printf "Tempo decorrido (s): `expr $TEND - $TBEGIN`\n";
printf "Tempo decorrido (min): `expr $(( ($TEND - $TBEGIN)/60 ))`\n";
```

No exemplo acima, as primeiras linhas indicam os recursos que serão necessários para rodar o comando que você deseja executar.
Por exemplo, o programa `jellyfish` será executado usando `8` threads. Isso é definido na linha abaixo:
```shell
#PBS -l nodes=1:ppn=8
```

Nas três linhas seguintes, são definidos o nome do job, onde deverá ser salvo o log do comando e onde deverá ser salvo os erros dados no comando:
```shell
#PBS -N jellyfish
#PBS -o jellyfish.log
#PBS -e jellyfish.err
```

Toda vez que você for rodar um comando, deverá alterar a linha abaixo (talvez você tenha percebido pela sutil descrição no arquivo):
```shell
jellyfish count -C -m 31 -s 1000 -t 1 -o drUrtUren1.jf drUrtUren1.600.fasta
```

As outras linhas são apenas comandos de controle do job e não devem ser alteradas.


### Editando o arquivo PBS

Para editar o arquivo `.pbs`, você pode usar o comando `vim`. Com esse comando, você consegue editar o conteúdo do arquivo. 
```shell
vim job_jellyfish.pbs
```

Após executar o comando, você precisa apertar a tecla `i` (INSERT) pra poder editar o documento.
Ao terminar de fazer as edições necessárias, você precisa apertar a tecla `ESC`, para sair do modo de edição.
Em seguida, digite a tecla de dois pontos `:` e em seguida digite `wq!` para indicar que você deseja salvar o documento e sair da edição.

Toda vez que você for rodar um comando dos softwares apresentados neste tutorial, você vai precisar submeter o job do comando para a fila de jobs do cluster Superdome com as instruções mostradas anteriormente.

### Submetendo o arquivo PBS para a fila de jobs

Após ter editado o arquivo `.pbs` com o comando que você deseja executar, você precisa submeter o job para uma fila de processamento.
No total, o cluster Superdome apresenta um total de 768 núcleos, divididos em três filas:

`op1`: com 462 cores disponíveis;
`op2`: com 236 cores disponíveis;
`testes`: com 70 cores disponíveis;

Para submeter seu job para uma das filas acima, execute o comando `qsub` abaixo:
```shell
qsub -q <fila> <arquivo.pbs>
```

Onde o parâmetro `-q` indica a fila à qual o `<arquivo.pbs>` deve ser submetido, por exemplo:
```shell
qsub -q op1 job_jellyfish.pbs
```

Recomendamos que durante este curso você utilize a fila `op1`.

### Consultando a fila de jobs submetidos e deletando um job específico

Caso você queira saber quais jobs estão sendo executados, quem está executando, quanto de recurso computacional está sendo utilizado e há quanto tempo o processo está sendoe executado, basta usar o comando `qstat`:
```shell
qstat -a
```

Ao executar o comando acima, você vai ser capaz de verificar a fila de jobs submetidos até o momento e que estão rodando ou em pausa, como demonnstrado abaixo:

```shell
blmsvfhpc04.itv.local:
                                                            Req'd  Req'd   Elap
Job ID          Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
--------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
5444.blmsvfhpc* c0403    op1      snpArcher* 21701*   1  32  300gb   --  R 354:3
5606.blmsvfhpc* 81041448 op2      fst        35108*   1  20    --    --  R 214:5
5646.blmsvfhpc* c0430    op2      construct  24737*   1  20    --    --  R 117:0
5753.blmsvfhpc* c0403    op1      fastq2bam* 28126*   1  64    --    --  R 01:58
```

No resultado do comando `qstat -a`, podemos ter as seguintes informações:
`Job ID`: Identificador do job submetido. Esse identificador é importante caso queira deletar um job da fila;
`Username`: Matrícula do usuário que submeteu o job para a fila. Se você submeteu algum job, sua matrícula deve aparecer associada ao job submetido;
`Queue`: Fila onde o job está submetido;
`Jobname`: Nome do job que você configurou no arquivo `.pbs`





