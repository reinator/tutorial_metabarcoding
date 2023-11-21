---
title: "Submetendo jobs na fila do cluster"
layout: archive
permalink: /submitting_jobs/
---

Para mantermos organizado o ambiente computacional que compartilhamos com todo o Instituto, utilizamos o sistema [Torque PBS](https://hpc-wiki.info/hpc/Torque) 
Este sistema permite que todos os processos que precisam de recursos de processador e memória do cluster Superdome fiquem organizados em uma fila de processamento e de fácil monitoramento.

### Arquivo PBS
Todo comando que precise de recursos de processamento e memória não pode ser rodado diretamente do terminal. O comando precisa estar primeiramente dentro de um arquivo `.pbs`, cuja estrutura você pode verificar abaixo:

```shell=
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
Por exemplo, o programa `jellyfish` será executado usando `8` threads


#### Fazendo o login

Se você estiver usando Mac OS ou Linux, você vai precisar primeiramente abrir um `terminal` e então digite `ssh`.

`ssh` significa [secure shell](https://en.wikipedia.org/wiki/Secure_Shell) e é o comando que permite interagir com servidores e computadores de forma remota. Você também deve ter recebido o seu nome de usuário no cluster `nome_de_usuario`
Você vai logar no cluster usando o seguinte comando:

```shell
ssh nome_de_usuario@172.16.111.35
```  

Após isso, você precisará digitar sua senha (também fornecida via email).
Talvez você também preciso aceitar uma chave RSA, para fins de segurança. Nesse caso, apenas digite `yes` e você terá logado no nosso cluster Superdome Flex!

#### Baixando e subindo arquivos para o cluster com o comando scp

Ocasionalmente, precisaremos transferir arquivos entre o cluster e nossos computadores locais. Para fazer isso, podemos usar um comando chamado `scp` ou [secure copy](https://en.wikipedia.org/wiki/Secure_copy). Ele funciona de forma semelhante ao `ssh`. Vamos tentar criar um arquivo fictício em nosso diretório pessoal local e, em seguida, carregá-lo em nosso diretório pessoal no cluster.

```shell
# crie um arquivo fictício
touch arquivo_teste
# faça o upload para o custer
scp arquivo_teste <nome_de_usuario>@<172.16.111.35>:~/
```

No comando acima, nós simplesmente estamos copiando um arquivo (`arquivo_teste`) para o cluster. Após o símbolo `:`, estamos especificando para onde no cluster estamos copiando o arquivo. No comando nós utililzamos `~/` para especificar o diretório `home` do usuário.

A cópia de arquivos de volta para o computador local também é simples. Se quisermos copiar o arquivo que acabamos de carregar no servidor de volta para o computador local, precisaremos executar o mesmo comando `scp`, mas agora trocando a ordem dos diretórios local e do servidor:

```shell
# download `test_file` from server to local current working directory (.)
scp <nome_de_usuario>@<172.16.111.35>:~/arquivo_teste ./
```

### Usuários Windows

#### Fazendo o login

Se estiver usando um computador Windows, será necessário fazer login usando o [MobaXterm](http://mobaxterm.mobatek.net), pois ainda não há um cliente `ssh` nativo. Depois de instalá-lo, abra o MobaXterm e:

1. Inicie um novo terminal SSH (1 e 2);
2. Adicione o endereço do host (3) - que é o endereço IP `172.16.111.35` - e seu nome de usuário (4);
3. Depois de adicionar as informações anteriores, pressione "OK" para se conectar ao servidor.

![](/gbb_montagem_workshop/images/mobaxterm_tutorial.PNG)

#### Baixando e subindo arquivos para o cluster com o Filezilla

O [Filezilla](https://filezilla-project.org/) é um software útil para mover arquivos de um servidor remoto.

Abra o Filezilla, digite o endereço IP `172.16.111.35` e o nome de usuário. Quando você pressionar Enter, ele deverá conectá-lo. Da próxima vez, você poderá usar o menu suspenso "Conexão rápida", desde que o endereço IP não tenha sido alterado nesse meio tempo.

![](/gbb_montagem_workshop/images/putty/fig12.png)

Agora você verá o sistema de diretório de arquivos (pastas) no seu computador local à esquerda e as pastas no cluster Superdome à direita. Agora você pode simplesmente arrastar e soltar arquivos de um lado para o outro. 
