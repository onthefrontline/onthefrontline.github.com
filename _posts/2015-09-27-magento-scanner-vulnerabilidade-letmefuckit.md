---
author: OntheFrontLine
layout: post
title: "Magento - Verificação de vulnerabilidade com o Scanner LetMeFuckIt"
date: 2015-09-27 23:00
comments: true
category : magento
tags:
- letmefuckit
- python
- scanner
---

Magento - Detectando e explorando falha SQLi Vulnerability (1.9.1.0 CE).
 
Scanner and Exploit Magento 

## O Problema##

O SQLi (SQL Injection) permite que atacantes injetem dados não confiáveis ​​ no banco de dados do alvo. Com este tipo de vulnerabilidade explorada no Magento, o atacante pode executar determinadas ações no banco de dados como a adição de um cupom para obter um desconto sobre um determinado produto ou mesmo adicionando uma conta de administrador para obter acesso administrativo no site.

O Magento é um dos principais distribuidores de CMS para o comércio eletrônico. Ele atualmente mantém duas versões de sua aplicação, uma edição para comunidade e uma edição Enterprise.

## O Scanner ##

O Scanner explora a vulnerabilidade **SQLi Vulnerability (1.9.1.0 CE)** do Magento.

A vulnerabilidade foi corrigida no **Patch SUPEE-5344**, entretanto, o scanner serve para localizar e testar os sitemas que não aplicaram o patch de segurança. 

O **LetMeFuckIt** foi escrito em Python e utiliza as seguintes bibliotecas:

*pygoogle, argparse, urllib2, requests, base64*

## Uso: ##
    letmefuckit.py --dork <dork> --pages <number> --user <user> --pwd <pass>

## Exemplo: ##
    letmefuckit.py --dork "inurl:customer/account/login/ site:com.br" --pages 4 --user adm --pwd pass

## Opções ##

--dork < dork >


--user < user >

--pwd < password >

--pages < number >

--help 

## Dorks Recomendadas##

"inurl:/customer/account/login site:com.br"

"inurl:/checkout/onepage/ site:com.br"

 
## Informações ##

Através da dork inserida, é feita uma varredura no Google, as urls são salvas no arquivo urls.txt, que posteriormente são automaticamente testadas.

Os usuários fornecidos na execução são adicionados automaticamente como administradores nos sites vulneráveis.


## Screenshots ##

[![](http://i.imgur.com/6lJtrv1.jpg)](http://i.imgur.com/6lJtrv1.jpg)

[![](http://i.imgur.com/KuK3S95.png)](http://i.imgur.com/KuK3S95.png)

[![](http://i.imgur.com/DSVEoSz.jpg)](http://i.imgur.com/DSVEoSz.jpg)


## Ferramenta ##

+ Python 2.7 ([Python](https://www.python.org/download/releases/2.7/ "Download Python 2.7"))

+ LetMeFuckIt ([Python](https://github.com/onthefrontline/LetMeFuckIt-Scanner "Download"))


## Possíveis erros ##

Caso você se depare com o erro abaixo, é porque o scanner utiliza a biblioteca pygoogle, a biblioteca está desatualizada com o novo sistema de API's do Google, pois agora é necessário uma Key para utilizar a api.

    pygoogle ERROR __search__| responseDetails : Suspected Terms of Service Abuse. Please see http://code.google.com/apis/errors

Se o erro aparecer, apenas aguarde 1 minuto ou 2. O Scanner voltará ao normal.


## Defendenda-se! ##

Instale agora o PATCH 5344 ou superior no [site oficial do Magento](https://www.magentocommerce.com/download "Download do Patch de Segurança") 


-------------



Referências: 

[0] https://www.pandoralabs.net/sample-sqli-exploits-magento-1-9-1-0-ce/

[1] http://blog.checkpoint.com/2015/04/20/analyzing-magento-vulnerability/

[2] https://blog.sucuri.net/2015/04/magento-shoplift-supee-5344-exploits-in-the-wild.html


