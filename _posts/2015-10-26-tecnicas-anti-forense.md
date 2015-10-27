---
author: OntheFrontLine
layout: post
title: "Forensic - Conheça algumas técnicas Anti-Forense"
date: 2015-10-26 00:00
comments: true
category : Forensic
tags:
- Security
- Anti-Forensic
---


Conheça algumas técnicas básicas Anti-Forense.  

[<img src="{{ site.url }}/images/anti-forense.jpg" style="height: 75%;width: 75%;"/>]({{ site.url }}/images/anti-forense.jpg "Técnicas Anti-Forense")


## Anti-Forense ##

A Ciência Forense é responsável pela preservação, identificação, extração, documentação e interpretação de uma prova.  Ao contrário dela, existem as técnicas Anti-Forenses, são métodos de remoção, ocultação e obstrução de evidências com o objetivo de mitigar os resultados de análises forenses. 

## Técnicas de destruição da informação ##

Com o objetivo de impossibilitar a recuperação de evidências ou simplesmente proteger dados confidenciais, técnicas de destruição da informação podem ser necessárias. 

"A todo momento, um usuário normal, cria e exclui vários arquivos no disco. Mas, na maioria dos sistemas computacionais, as informações excluídas permanecem intactas no disco. Isso ocorre porque o arquivo não é fisicamente excluído, e sim uma operação de exclusão lógica."

Alguns softwares se baseiam no Método de Gutmann, segundo Gutmann, para eliminação segura dos dados, é necessário sobrescrever um bloco no disco várias vezes, com alternância de padrões em diferentes frequências. O algoritmo trabalha com 35 passos de sobrescrita no disco.



## Técnicas de Ocultação da informação ##

O objectivo principal deste método é o de tornar invisível a evidência para o analista. Deste modo, os atacantes conseguem ocultar mensagens ou objetos dentro de arquivos (por ex: imagens dentro de arquivos .mp3), de forma que não haja nenhum sinal de sua existência.

Esta técnica, chamada esteganografia, pode ser muito eficaz se bem executada, mas traz muitos riscos para o atacante. Caso não seja alterado os elementos necessários e a técnica identificada, poderá ser mais acréscimo para uma investigação, resultando em mais uma acusação.


## Técnicas de Alteração da informação (meta dados) ##

O principal objetivo da técnica é criar provas falsas para cobrir o verdadeiro autor, incriminar outrém, e portanto, desviar a investigação.

Se o analista descobre quando um invasor teve acesso a um sistema, seja ele Windows, Mac ou Unix, muitas vezes é possível determinar quais arquivos ou pastas ele acessou. 

Utilizando uma linha do tempo é possível fazer uma ordem cronológica das ações, o analista teria uma reconstituição do que aconteceu no sistema. Embora um invasor possa excluir o conteúdo dos logs (arquivos com os registros), esta ação poderia atrair ainda mais atenção.

Uma estratégia muito utilizada é quando um atacante esconde seus passos, substituindo seus próprios tempos de acesso (sejam data, hora..etc), para que o cronograma não possa ser construído de forma confiável.

Existem inúmeras ferramentas para este fim, por exemplo o ExifTool, que permitem apagar ou alterar esses parâmetros.

As técnicas não necessariamente têm objetivos maliciosos. É possível, por exemplo, ocultar informações, alterando os atributos, porque é muito improvável que um atacante que tenha acessado um sistema, vá acessar arquivos antigos, especialmente se ele não foi aberto e/ou foi criado há alguns anos.


## Programas Úteis ##

 
+ Wipe ([Linux](http://sourceforge.net/projects/wipe/files/wipe/ "Download Wipe para Linux") - apt-get install wipe)

+ BitKiller ([Windows](http://sourceforge.net/projects/bitkiller/ "Download BitKiller para Windows"))

+ ExifTool ([Linux e Windows](http://sourceforge.net/projects/exiftool/ "Download ExifTool"))
