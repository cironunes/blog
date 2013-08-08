---
layout: post
title: "Os poderes do box-sizing"
date: 2013-06-05 23:40
comments: true
categories: [css, tips]
published: false
---

Durante anos os Desenvolvedores e Web Designers tiveram a difícil tarefa de lhe dar com o ```box-model``` que é a área ocupada em pixels (```width/height``` + ```padding``` + ```border```) por cada elemento na tela. Montar um layout fluido com CSS era fatalmente frustrante para iniciantes pela facilidade de se perder nos calculos.

Felizmente, com a "nova" propriedade ```box-sizing``` do CSS3, podemos ajustar o ```box-model``` para trabalhar de uma maneira mais conveniente. Existem 3 valores possíveis para esta propriedade: ```content-box```, ```padding-box(experimental)``` e ```border-box```


### Selects e textareas 100%
Sabe aquele textarea chato que você coloca ```width: 100%;``` e ele sempre fica 20px "pra fora" à direita?

### Suporte
Caso você não precise dar suporte a IE abaixo do 8, use sem preoucupações