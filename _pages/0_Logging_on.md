---
title: "Fazendo login no cluster"
layout: archive
permalink: /logging_on/
---

Normalmente, ao trabalhar com bioinformática, nós nos conectamos a um cluster computacional, como o que preparamos para este curso. Esses clusters fornecem recursos computacionais muito mais poderosos do que os computadores pessoais médios, permitindo-nos executar tarefas computacionais altamente complexas exigidas por algumas análises de bioinformática. Como podemos fazer o login no cluster disponibilizado para este curso?

### Cluster computacional Superdome Flex

O Cluster computacional que iremos utilizar para o curso será o Superdome Flex. Ele apresenta 1 Blade com 768 Núcleos Intel(R) Xeon(R) Gold 6252 CPU @ 2.10GHz e 3 TB RAM. O endereço IP do cluster é `172.16.111.35` e deverá ser utilizado ao se fazer o login.

![](/gbb_montagem_workshop/images/superdome.svg)

### Usuários de Mac OS X e Linux

#### Fazendo o login

Se você estiver usando Mac OS ou Linux, você vai precisar primeiramente abrir um `terminal` e então digite `ssh`.

`ssh` significa [secure shell](https://en.wikipedia.org/wiki/Secure_Shell) e é o comando que permite interagir com servidores e computadores de forma remota. Você também deve ter recebido o seu nome de usuário no cluster `nome_de_usuario`
Você vai logar no cluster usando o seguinte comando:

```shell
ssh nome_de_usuario@172.16.111.35
```  

Após isso, você precisará digitar sua senha (também fornecida via email).
Talvez você também preciso aceitar uma chave RSA, para fins de segurança. Nesse caso, apenas digite `yes` e você terá logado no nosso cluster Superdome Flex!

#### Diretório para a parte prática do Workshop
Todas as nossas atividades serão feitas no diretório `/mnt/gen/temp/workshop_montagem_gbb/`. Então assim que você fizer o login, vá para o diretório mencionado anteriormente e liste o conteúdo:

```shell
cd /mnt/gen/temp/workshop_montagem_gbb/
ls
```  
Dê uma olhada nas subpastas presentes. Viu que tem uma pasta chamada `alunos`? Entre nela e em seguida crie uma pasta com o seu nome:

```shell
cd /mnt/gen/temp/workshop_montagem_gbb/alunos
mkdir <seu_nome>
```

Pronto! É nessa pasta que todas as suas análises devem ser feitas. Vamos considerar que essa pasta que você criou seja o seu "home".

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
