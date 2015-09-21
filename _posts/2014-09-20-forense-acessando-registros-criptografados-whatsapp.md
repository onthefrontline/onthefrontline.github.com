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

<img src="{{ site.url }}/images/whatsappmapper-folder.jpg" style="height: 50%%;width: 50%;"/>

{% highlight bash%}
./WhatsAppMapper msgstore.db.crypt arquivo-log
{%endhighlight%}

<img src="{{ site.url }}/images/whatsappmapper-cmd.jpg" style="height: 50%%;width: 50%;"/>

+ Após a execução, ele salvará o log na pasta ***out/*** abra no seu navegador, conforme a imagem:

<img src="{{ site.url }}/images/whatsappmapper-log.jpg" style="height: 50%%;width: 50%;"/>



Now try below commands to make sure you are connected to machine.

{% highlight bash%}
amey@amey-xps:~$ adb devices -l
List of devices attached 
0202dc7rh2934b2a    device usb:3-2 product:occam model:Nexus_4 device:mako
{%endhighlight%}

+ Now unlock bootloader 
Turn off your Nexus 4.
Press and hold Volume Down and Power to enter the Fastboot menu.
Connect the Nexus 4 to your computer via USB cable.

{% highlight bash%}
fastboot oem unlock
{%endhighlight%}
Press the Volume Up button on the Nexus 4 to accept the command and press the Power button to confirm. The bootloader will now be unlocked, you will loss all data with this.

+ Download the factory image from [Google](https://developers.google.com/android/nexus/images), OR direct download clicking [HERE](https://dl.google.com/dl/android/aosp/occam-lrx21t-factory-51cee750.tgz).
unzip it

{% highlight bash%}
tar -xf occam-lrx21t-factory-51cee750.tgz
cd occam-lrx21t
{%endhighlight%}
+ Now the final step to Flash and install new lollipop image to your Nexus 4

{% highlight bash%}
adb reboot-bootloader
sleep 15
sudo ./flash-all.sh
{%endhighlight%}

This command will  generate following logs on your terminal, put your password if prompted, your phone may be rebooted few times.

<img style="height: 25%;width: 25%;" src="{{ site.url }}/images/nxs3.jpg"/>

{% highlight bash%}
amey@amey-xps:~/Downloads/occam-lrx21t$ sudo ./flash-all.sh
Password:
sending 'bootloader' (2264 KB)...

{%endhighlight%}

If your phone missbehave after finishing, just hard reboot it pressing power button for few seconds.

Happy coding ..... :)
