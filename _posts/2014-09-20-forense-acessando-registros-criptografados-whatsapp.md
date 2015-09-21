---
author: OntheFrontLine
layout: post
title: "Forensic - Acessando registros de conversas do Whatsapp"
date: 2014-09-21 00:00
comments: true
category : forensic
tags:
- whatsapp
- criptografia
- dorks
---

Forensic - Acessando registros de conversas criptografados do Whatsapp

## Mas afinal, o que é Ciência Forense? ##

A Ciência Forense é responsável pela preservação, identificação, extração, documentação e interpretação de uma prova.

O objetivo da computação forense é recuperar o registros e mensagens de dados existente em um computador, de modo a que toda a informação digital, pode ser usado como
prova. 


## Estudo de Caso ##

Vamos partir do pressuposto que já possuímos o arquivo da base de dados do WhatsApp: **msgstore.db.crypt**

A Localização deste arquivo no Dispositivo móvel é geralmente: ***/sdcard/WhatsApp/Databases***

Recentemente foi [descoberta uma nova Dork](https://www.exploit-db.com/ghdb/4073/ "Dork - WhatsApp Databases ") ¹, para busca destes arquivos online:

{% highlight bash%}
intitle:"Index of" "WhatsApp Databases" 
{%endhighlight%}

*¹ Dork ou Google Dork, é uma seqüência de pesquisa, que utiliza operadores para encontrar a informação que não está prontamente disponível em um site. *

## Ferramentas ##

+ Python ([Windows](https://www.python.org/downloads/ "Download Python for Windows")) (apt-get install idle-python3.4)
+ Whatsapp Mapper by SixP4ck3r ([Download 1](http://www.mediafire.com/download/1ubi67d67rddaf6/WhatsAppMapper.zip "Download Opção 1") ou [Download 2](http://www.mediafire.com/download/ayuxmixmg4avc16/WhatsAppMapper.zip "Download WhatsApp Mapper"))

## Utilização ##

+ Após o download do arquivo, vamos descompactá-lo e executá-lo:
{% highlight bash%}
sudo su
cd Downloads
unzip WhatsAppMapper.zip
cd WhatsAppMapper
{%endhighlight%}

+ Colocaremos o arquivo msgstore.db.crypt está na mesma pasta do WhatsAppMapper e então executaremos:

[<img src="{{ site.url }}/images/whatsappmapper-folder.jpg" style="height: 75%;width: 75%;"/>]({{ site.url }}/images/whatsappmapper-folder.jpg)

{% highlight bash%}
./WhatsAppMapper msgstore.db.crypt arquivo-log
{%endhighlight%}

<img src="{{ site.url }}/images/whatsappmapper-cmd.jpg" style="height: 75%;width: 75%;"/>

+ Após a execução, ele salvará o log na pasta ***out/*** abra no seu navegador, conforme a imagem:

<img src="{{ site.url }}/images/whatsappmapper-log.jpg" style="height: 75%;width: 75%;"/>

Como vocês podem observar na imagem acima, o LOG gerou um HTML com um Menu com todos os números dos contatos do WhatsApp, basta clicar em cada número para ler as mensagens.

Good Luck...
