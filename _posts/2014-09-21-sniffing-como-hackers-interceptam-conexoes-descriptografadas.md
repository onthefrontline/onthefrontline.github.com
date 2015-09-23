---
author: OntheFrontLine
layout: post
title: "Sniffing - Como hackers interceptam conexões descriptografadas"
date: 2014-09-22 00:50
comments: true
category : sniffing
tags:
- criptografia
- ettercap
---

Farejando e interceptando logins e senhas através de redes não seguras. 

## O que é Sniffing? ##
É a técnica de capturar as informações de uma determinada máquina ou o tráfego de uma rede sem autorização, com o objetivo de coletar dados, senhas e comportamentos do usuário.

Os programas geralmente capturam tudo o que passa e depois utilizam filtros para que possa facilitar a vida do 'farejador'. 

Existem sniffers específicos para cada protocolo.

## Man in the Middle (MITM) ##

Conhecido como o Ataque do Homem do Meio. É um dos ataques no qual uma terceira pessoa consegue "ficar no caminho" de uma comunicação de dois computadores.

Não há qualquer interrupção do tráfego, pois a terceira pessoa redireciona os pacotes de dados ao computador destino, técnica chamada de ARP-Poisoning / ARP-Spoofing.

*Em uma **explicação básica** seria como se você postasse nos Correios uma carta, o carteiro olhasse o conteúdo e depois  entregasse a carta a você.*

## Ferramentas ##

+ Ettercap ([Windows - Binários não oficiais](http://sourceforge.net/projects/ettercap/files/unofficial%20binaries/windows/ "Versões Binárias Não Oficiais")) ([Site Oficial do Código Fonte](https://ettercap.github.io/ettercap/downloads.html "Download do Ettercap"))

Caso esteja utilizando alguma distribuição Linux:

{% highlight bash%}
sudo apt-get install zlib1g zlib1g-dev
sudo apt-get install build-essential
sudo apt-get install ettercap
{%endhighlight%}



## O Cenário ##

**1 - Atacante**

Nesse tutorial utilizamos uma máquina virtual (Virtual BOX) com o Sistema Operacional Kali e com a ferramenta Ettercap instalada.


**2 - Alvo**

Usuário(s) da rede utilizando algum serviço com conexão não segura na rede ou internet.


**3 - Objetivo**

Coletar informações aleatórias de algum usuário conectado na rede.




## Utilização ##

+ O software Ettercap pode ser executado através da interface gráfica ou simplesmente pela linha de comando, utilizaremos a Interface Gráfica para maior percepção sobre a ferramenta:

[<img src="{{ site.url }}/images/snifffing-ettercap-1.png" style="height: 75%;width: 75%;"/>]({{ site.url }}/images/snifffing-ettercap-1.png "Interface do Programa")


+ Com o programa aberto, iremos configurá-lo:

Ative o modo promíscuo 
{% highlight bash%}
Options -> Promisc mode
{%endhighlight%}

O Modo Promíscuo permite examinar dados destinados a outros endereços MAC da sua rede.

+ Também configuramos a interface de rede a qual utilizaremos:
{% highlight bash%}
Sniff -> Unified Sniffing...
{%endhighlight%}

[<img src="{{ site.url }}/images/snifffing-ettercap-interface.png" style="height: 75%;width: 75%;"/>]({{ site.url }}/images/snifffing-ettercap-interface.png "Lista de Alvos")

No nosso caso, utilizaremos a interface **eth0**, caso não saiba qual você está utilizando abra o terminal e digite:


Para conexão cabeada:

{% highlight bash%}
ifconfig
{%endhighlight%}
 
ou para Wireless

{% highlight bash%}
iwconfig
{%endhighlight%}

+ Após isto, vamos configurar a lista de alvos 
[<img src="{{ site.url }}/images/snifffing-ettercap-host.png" style="height: 75%;width: 75%;"/>]({{ site.url }}/images/snifffing-ettercap-host.png "Lista de Alvos")

{% highlight bash%}
Hosts > Scan for Hosts
{%endhighlight%}

Uma Lista de endereços IP e Macs será exibida, selecione o alvo e clique em **Add to Target 1**

+ O próximo passo é ativar o "Ataque do Homem do Meio" (MITM)

{% highlight bash%}
Mitm > Arp Poisoning
{%endhighlight%}

Assim que abrir a caixa marque as opções:

{% highlight bash%}
[x] Sniff remote Connections
[x] Only poison one-way
{%endhighlight%}

Aperte no Botão OK.

+ Agora vamos ativar o farejador:

{% highlight bash%}
Start > Start Sniffing
{%endhighlight%}

+ Pronto, o programa está na escuta. Agora é só aguardar algum usuário realizar alguma requisição.

## Alvo ##

+ Para prosseguir com o cenário, a vítima, neste tutorial se chamará: "Moleque Maroto", ele está se cadastrando em uma Loja Virtual Online para realizar suas compras.


[<img src="{{ site.url }}/images/sniffing-ettercap-alvo-formulario.jpg" style="height: 75%;width: 75%;"/>]({{ site.url }}/images/sniffing-ettercap-alvo-formulario.jpg "Moleque Maroto se cadastrando")

+ Assim que ele enviar o formulário de cadastro, o ettercap irá extrair os dados da requisição, conforme imagem:

[<img src="{{ site.url }}/images/snifffing-ettercap-dados.png" style="height: 75%;width: 75%;"/>]({{ site.url }}/images/snifffing-ettercap-dados.png "Moleque Maroto se cadastrando")

Ele exibiu todos os detalhes preenchidos no formulário de cadastro. 


## Conclusão ##

+ Para finalizar as tarefas:

{% highlight bash%}
Mitm > Stop mitm attack(s)
{%endhighlight%}

e

{% highlight bash%}
Start > Stop Sniffing
{%endhighlight%}

Viu como você muitas vezes está exposto? Compreende a importância  de comprar / utilizar serviços de site com Criptografia de dados? 

Já imaginou quantos sites você acessa em Lan Houses, Universidades e Pontos de Acesso sem criptografia?



**A Internet pode até ser grátis, ou o vizinho pode ser bacana em compartilhar a internet com você, mas a maior moeda são seus dados pessoais.**


Lembramos que nem toda criptografia é 100% segura e que muitas conexões HTTPS também poderão ser quebradas.

Caso você queira saber como se proteger destes ataques, aguarde o próximo post.

Good Luck...
