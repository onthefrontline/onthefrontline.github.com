---
author: OntheFrontLine
layout: post
title: "Sniffing - Detectando anomalias na rede"
date: 2014-09-24 00:50
comments: true
category : sniffing
tags:
- nmap
- detect_sniffer6
---

Sniffing - Detectando e Defendendo-se de "cães farejadores" na rede.

Dentre muitas ferramentas para exploração de redes, destaco dois softwares que auxiliam no processo de detecção de anomalias na rede.
 
## NMAP - Uma ferramenta poderosa ##

NMAP ou Networking Mapper é um scanner de rede de gratuito e de código aberto que permite explorar sistemas e serviços na rede, seja local ou na internet. A ferramenta foi desenvolvida para auxiliar na descoberta de vulnerabilidades em redes.  


## Detect Sniffer 6 ##

Como o próprio nome diz, ela detecta farejadores na rede local. 

## Ferramentas ##

+ Nmap ([Windows](https://nmap.org/download.html#windows "Download Nmap for Windows")) (sudo apt-get install nmap)
+ Detect_sniffer6 (Disponível na Distribuição KALI)



## Detectando os cães ##

Via **detect_sniffer6**

Sintaxe: 
{% highlight bash%}
detect_sniffer6 interface 
{%endhighlight%}

Exemplo:
{% highlight bash%}
detect_sniffer6 eth0 
{%endhighlight%}

Output:
{% highlight bash%}
root@root:~# detect_sniffer6 eth0
Sending sniffer detection packets to ff02:1
 Snffing host detected: xxxx:xxxx:xxxx:xxxx:xxxx
1 sniffing host detected 
{%endhighlight%}

O Software detectou 1 farejador no Link-Local-IPV6:
xxxx:xxxx:xxxx:xxxx.

OBS: Caso não saiba qual interface você esta utilizando, digite:

{% highlight bash%}
ifconfig 
{%endhighlight%}

ou 

{% highlight bash%}
iwconfig
{%endhighlight%}



Via **NMAP**

Sintaxe: 
{% highlight bash%}
nmap -sV --script=sniffer-detect ip-address 
{%endhighlight%}

Exemplo:
{% highlight bash%}
nmap -sV --script=sniffer-detect 192.168.0.2 
{%endhighlight%}

Output:
{% highlight bash%}
nmap -sV --script=sniffer-detect 192.168.0.2

Starting Nmap 6.47 ( http://nmap.org ) at 2015-09-24 23:33 BRT
Nmap scan report for 192.168.0.2
Host is up (0.0049s latency).
Not shown: 996 filtered ports
PORT     STATE  SERVICE    VERSION
23/tcp   closed telnet
80/tcp   open   tcpwrapped
1900/tcp closed upnp
8080/tcp closed http-proxy
MAC Address: xx:xx:xx:xx:xx:xx (Arris Group)

Host script results:
|_sniffer-detect: Likely in promiscuous mode  (tests: "11111111")
{%endhighlight%}

O atributo -sV traz ao resultado a lista de portas que estão rodando atualmente sobre a máquina. Consulte a lista completa de atributos na [Wiki](http://wiki.ubuntu-br.org/Nmap "Wiki do NMAP").

Como resultado ele nos trouxe "11111111", isso quer dizer que uma máquina está executando o modo promíscuo...alguém está farejando.

*"[Modo promíscuo](https://pt.wikipedia.org/wiki/Modo_prom%C3%ADscuo "Definição de modo promíscuo") (ou ainda comunicação promíscua), é um tipo de configuração de recepção na qual todos os pacotes que trafegam pelo segmento de rede ao qual o receptor está conectado são recebidos pelo mesmo, não recebendo apenas os pacotes endereçados ao próprio."* 

Alguns sistemas operacionais podem trazer a informação de outras formas como: 

Windows: 11_1__11 ou 111___1_
Linux: 11111111 

Caso o script não retorne nada, é porque não há execução.

Caso não saiba qual o ip utilizar você pode basear-se no gateway, por exemplo, 192.168.0.1 (gateway), você pode utilizar como ip: 192.168.0.1/255 

Isto faz com que o NMAP faça a varredura em todas os ips da faixa de 1 a 255. 

Lembrando que o NMAP pode demorar um pouco para scannear uma grande faixa.

## Defendenda-se! ##

Algumas dicas para proteger-se:

+ Utilize VPN (Virtual Private Network) para encriptar as comunicações. 
+ 
	+ [FrootVPN](http://frootvpn.com/ "FrootVPN")
	+ [Sumrando](https://www2.sumrando.com/pricing.aspx "Sumrando")

+ Conheça alguns softwares que ajudam a gerenciar e proteger a tabela ARP:

	+ [XArp](http://www.chrismc.de/development/xarp/ "XArp")
	+ [Arpwatch](http://www.vivaolinux.com.br/artigo/Arpwatch-Detecte-em-sua-rede-ataques-de-Arp-Spoofing-Arp-Poisoning "Guia do ArpWatch")
	+ [ArpON](http://arpon.sourceforge.net/download.html "ArpON Download")
	+ [Antidote](http://sourceforge.net/projects/antidote/ "Antidote on SourceForge")
	


## Conclusão ##

Neste breve post foi possível detectar farejadores na rede de modo simples, muitos anti-virus/securitys não detectam estas atividades na rede. 

Lembre-se segurança e prevenção nunca é demais. 

Já fez algumas varreduras de segurança em sua rede?
Analisou quais serviços estão rodando?
Esses serviços são realmente necessários? 

Quanto aos softwares de terceiros, são confiáveis?

Lembre-se de mantê-los atualizados, a cada dia milhares de novos exploits nascem, de nada adianta ter um bom servidor atualizado com aplicações vulneráveis, elas podem comprometer completamente o seu sistema. 




