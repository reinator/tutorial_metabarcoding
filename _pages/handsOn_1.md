---
title: "Hands On"
layout: archive
permalink: /handsOn_1/
---  

# Kmer analysis: running jellyfish <a name="where-are-we?"></a> 

Certo, hoje você aprendeu como analisar a composição kmer das leituras sequenciadas do seu genoma! Agora você vai colocar suas habilidades em prática e irá, você mesmo, contar e analisar kmers. Você deve escolher entre as espécies: (i) Vanessa atalanta, (ii) Urtica urens e (iii) Notonda dromedarius para trabalhar até o final da semana. Depois de escolher, crie uma pasta onde fará suas análises. Minha sugestão é criar uma pasta com o nome da sua espécie em seu diretório home (`/<species_name>/`) e dentro dela, criar uma série de outras pastas para estruturar suas análises. Por exemplo:

u_urens/
u_urens/kmers/
u_urens/assembly/
  
O exposto acima basicamente significa que você criou uma pasta chamada 'u_urens' (se você escolher U. urens como sua espécie de trabalho) e dentro dela você criou duas outras pastas lado a lado chamadas 'kmers' e 'assembly'. Se você quiser fazer isso, faça:
 
 ```console  
mkdir <species_folder>
cd <species_folder>
mkdir kmers
mkdir assembly
```  
 
Ótimo, agora você precisa copiar os dados da sua espécie. Os dados estāo dentro de `/mnt/gen/temp/workshop_montagem_gbb/data/`

```console  
cd /mnt/gen/temp/workshop_montagem_gbb/data/
ls -ltr
```  
Você vê as pastas das 3 espécies? Se sim, copie o arquivo <species-code>.600.fasta (veja abaixo a nota de atenção, que explica sobre os códigos das espécies) para o diretório `kmers` que você criou e volte para o diretório `kmers`. Um exemplo:

```console  
cp drUrtUren1_data/drUrtUren1.600.fasta <Path_to_your_folder>/u_urens/kmers/
cd <Path_to_your_folder>/u_urens/kmers/ 
ls -ltr
```

PS: se você seguiu nossa recomendação e criou a pasta de espécies no diretório inicial, `<Path_to_your_folder>` deve ser seu diretório inicial, então `user2` agora deve estar localizado em `/home/user2/<species_name>/kmers/ ` (lembre-se que você pode verificar seu diretório de trabalho atual com o comando `pwd`). 

### Atenção: grey_exclamation:

Os dados de cada espécie terão um código em seu nome representando cada uma das 4 espécies que trabalharemos durante esta semana, este é o código que eles possuem no Projeto Darwin Tree of Life. Os códigos são:

* ilVanAtal1 - *Vanessa atalanta*

* drUrtUren1 - *Urtica urens*

* ilNotDrom1 - *Notodonta dromedarius*

* iHemFuc1 - *Hemaris fuciformis* (não vamos usar esta espécie na análise atual)


Lembre-se desses códigos, pois os arquivos via de regra vāo possuir esse código.

Agora você precisa configurar o `conda` para o seu usuário. Siga [este tutorial](https://eukaryotic-genome-assembly.github.io/conda_setup/) para fazer isso.

Agora, verifique se o ambiente conda `eukaryotic_genome_assembly` está ativo. Seu prompt deve ser semelhante a:

```bash
(eukaryotic_genome_assembly) userX@IP-address:working_directory$
```

Se o seu prompt for semelhante a:

```bash
(base) userX@endereço IP:working_directory$
```

você só precisa executar `conda activate eukaryotic_genome_assembly`. Caso contrário (ou seja, se não houver `(base)` nem `(eukaryotic_genome_assembly)`, então provavelmente você não configurou o conda corretamente. Volte ao tutorial ou peça a ajuda do Renato.
 
Com o ambiente `eukaryotic_genome_assembly` ativo, tente chamar Jellyfish:

```console
jellyfish --help
```

Você vê help message? Ótimo! (Se não, chame o Renato!)

Jellyfish tem muitos passos. O primeiro que queremos executar é o *count* para contar as leituras de kmers do nosso genoma. O tamanho do kmer que usaremos é 31.

1-) Jellyfish count

Então aí vem o comando:

```console
jellyfish count -C -m 31 -s 1000 -t 1 -o <espécie>.jf <espécie>.600.fasta
```


### Atenção: grey_exclamation:

Na linha de comando acima você vê \<species\>.600.fasta. Este precisa ser substituído pelo arquivo fasta da espécie que você escolheu. Esta é apenas uma forma genérica de apontar que um arquivo fasta deve ser imputado naquela posição na linha de comando acima. O mesmo acontece com \<species\>.jf. Se sua espécie for Vanessa atalanta, você pode optar por ter um output chamado (-o) chamada v_atalanta.jf .

### Mais

Tente por favor:

```console
jellyfish count --help
```

na sua linha de comando para entender quais são os parâmetros que você imputou na linha anterior. As mensagens de ajuda são uma forma útil de entender o que você está executando e de ver se gostaria de adicionar algum outro parâmetro para seu caso de análise específico. Lembre-se também que além deste curso a internet estará sempre do seu lado. Se você pesquisar no Google ‘how to use jellyfish’, por exemplo, encontrará [JellyfishUserGuide]( http://www.genome.umd.edu/docs/JellyfishUserGuide.pdf)

### Voltemos!

2-) jellyfish histo

Agora que você contou seus kmers de 31 letras, queremos transformá-los em um arquivo de histograma para que você possa plotá-los. Então temos o segundo comando:

```console
jellyfish histo <espécie>.jf > <espécie>.histo
```
### Atenção: grey_exclamation:

Observe que no comando acima usamos o símbolo “>” antes do outpus. Este é um símbolo de linha de comando que redirecionará sua saída para um arquivo em vez de imprimir o resultado na tela.

Observe que o arquivo de entrada para o seu comando **jellyfish histo** é a saída do seu comando anterior, que era **jellyfish count**. Agora você tem o resultado necessário para plotar um histograma no genomescope e dar uma olhada na distribuição dos seus kmers do genoma.

# MAS PARE!

# PARA PARA!

...

Antes de plotar este resultado, quero que você plote um gráfico do genomescope para outro arquivo PRIMEIRO!!

Dentro do diretório compartilhado para sua espécie (`/mnt/gen/temp/workshop_montagem_gbb/data/<species-Code>_data/`), você encontrará dois arquivos chamados:

```console  
<species>.ccs.total.fasta.gz
<species>.total.histo
```

Baixe o arquivo \<species\>.total.histo para sua máquina local (se precisar de ajuda para isso, temos instruções sobre como fazer download/upload de arquivos [neste](https://eukaryotic-genome-assembly.github.io /logging_on/) tutorial), vá para a página [Genomescope](http://qb.cshl.edu/genomescope/) e carregue o arquivo lá. Você deve alterar a **Descrição** para o nome da sua espécie, e o **kmer** para 31. Em seguida, plote. Pessoas que trabalham com drUrtUren1 também precisam definir a contagem máxima de kmer para 10.000.

Salve a imagem de ambas as versões do gráfico - normal e escala logarítmica - em algum lugar do seu computador.

Legal, você traçou a distribuição kmer do arquivo \<species\>.total.histo, e o genomascope calculou para (i) o tamanho estimado do genoma, (ii) a heterozigosidade e (iii) a porcentagem de repetições do seu genoma da espécie.

O histograma que você acabou de traçar é para uma contagem de águas-vivas do **total** leituras do PacBio HiFi sequenciadas para montar sua espécie. Nós o geramos para você porque leva tempo. No entanto, quando você voltar à vida real e precisar executá-lo para sua amostra, você executará os mesmos comandos executados para a subamostra (`*600.fasta`) como acabou de fazer! =) Yeah!!

## Agora

Gostaria que você gerasse algumas estatísticas gerais para as leituras de \*.ccs.total.fasta.gz. Eu tenho um script para você fazer isso. É chamado de `asmstats`.

Antes de executar o asmstats, vá para o diretório de espécies e crie um link virtual para o arquivo \*.ccs.total.fasta.gz:

```bash
cd <Caminho_para_sua_pasta_de_espécie>/
ln -s /home/ubuntu/Share/<código-espécie>_data/<código-espécie>.ccs.total.fasta.gz
```

Você pode verificar se o link virtual está funcionando imprimindo as duas primeiras linhas do arquivo. Se as duas primeiras linhas forem retornadas, o link foi criado com sucesso:

```bash
zcat <código-espécie>.ccs.total.fasta.gz | head -2
```
 
Agora você precisa adicionar o diretório onde o script `asmstats` está localizado (`/home/ubuntu/Share/scripts/asmstats`) à sua variável de ambiente:

```bash
exportar PATH=$PATH:/home/ubuntu/Share/scripts/
```

Em seguida, verifique se o diretório foi adicionado à sua variável de ambiente:

```bash
echo $PATH
```

Se você puder ver `/home/ubuntu/Share/scripts/` na saída do comando anterior, você deve estar pronto para executar o script asmstats (mas primeiro verifique se o ambiente conda `eukaryotic_genome_assembly` está ativo):

```console
asmstats <espécie>.ccs.total.fasta.gz > <espécie>.total.fasta.stats
```

Observação: estamos chamando seu arquivo de saída \<species\>.total.fasta.stats

Assim que a execução do comando terminar (pode levar alguns minutos), dê uma olhada na saída:

```console
menos <espécie>.total.fasta.stats
```

Além disso: use este tutorial para traçar a distribuição do comprimento de suas leituras: [Plot reads](https://eukaryotic-genome-assembly.github.io/handsOn_plotReadLength/)

Agora você gerou o gráfico kmer, lê as estatísticas e lê a distribuição do gráfico para seu conjunto completo de leitura PacBio HiFi. Que conclusões você pode tirar agora desses resultados?


a- Qual é o tamanho esperado do genoma?

b- Qual é a heterozigosidade estimada?

c- Qual é o conteúdo repetido estimado?

d- Levando em consideração o tamanho estimado do genoma e as estatísticas do total de leituras que você acabou de gerar, quanta cobertura de leitura você tem para montar esse genoma?

# Agora,

Quero que você volte ao arquivo *.histo* que você gerou hoje (para sua subamostra), baixe-o para sua máquina local e plote-o no genomascópio. Além disso, quero que você execute asmstats no arquivo fasta (o subconjunto 600) que você imputou à água-viva.

e- O que o genomascópio lhe diz quando você tenta traçar um histograma kmer para apenas algumas sequências?

f- Olhando o resultado do asmstats para este arquivo menor, quanta cobertura do genoma você tem neste arquivo, dando o tamanho estimado do genoma?

Ótimo. Agora vamos analisar tudo juntos: considerando o gráfico kmer do arquivo total e suas estatísticas, podemos dar uma boa olhada na composição kmer do DNA no genoma. Como se parece? Discuta com seus parceiros e depois com o grande grupo.  


