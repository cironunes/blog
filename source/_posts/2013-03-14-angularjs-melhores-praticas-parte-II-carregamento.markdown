---
layout: post
title: "AngularJS: Melhores práticas - Parte II: Carregamento de scripts"
date: 2013-03-14 21:30
comments: true
categories: [angularjs, workflow, best pratices, requirejs]
published: false
---

{% img center /images/posts/cover-bestpratices.jpg %}

Baixar recursos (HTML, CSS, scripts, imagens) tem um custo alto em termos de performance das aplicações. Principalmente scripts, que podem parar completamente o carregamento da página enquanto são baixados e executados pela engine de JavaScript do browser.

Nesta parte vamos focar em estratégias para carregá-los e como a flexibilidade do Angular nos possibilita fazê-lo de forma performática.

<!-- more -->

## Navegue pela série
- [Parte I - Iniciando um projeto e a estrutura de diretórios](/angularjs-melhores-praticas-parte-I-bootstrap)
- [Parte II - Carregamento de scripts](/angularjs-melhores-praticas-parte-II-carregamento)
- Parte III - Dicas e truques
- Parte IV - MVC

## Regra nº 1: Coloque seus scripts no rodapé

Desta maneira você evita que o carregamento da página seja bloqueado enquanto eles são baixados, "parseados" e executados. [Saiba mais](http://developer.yahoo.com/performance/rules.html#js_bottom)

## Regra nº 2: Use um CDN em produção

Fazendo isso, não otimizamos apenas nossa aplicação, mas a de todos que fizerem o mesmo. [Saiba mais](http://developer.yahoo.com/performance/rules.html#cdn)

O Angular está hospedado no [CDN do Google](https://developers.google.com/speed/libraries/devguide?hl=pt-PT#angularjs), basta incluí-lo no projeto, sempre no rodapé] e estaremos prontos para começar.

```
<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.0.4/angular.min.js"></script>
```

Recomendo ter o arquivo no projeto também, para poder trabalhar offline e se aventurar pelo código! :)

## Carregue seus scripts de forma assíncrona e gerencie suas dependencias

{% img center /images/posts/logo-requirejs.png %}

Caso prefira, saiba mais sobre os [benefícios de fazê-lo](https://gist.github.com/desandro/4686136) antes de continuar.

Para conseguirmos fazer o carregamento assíncrono dos nossos scripts, primeiro precisamos entender como funcionar o "startup" do Angular.

## Angular startup

Sua aplicação pode ser iniciada de duas formas:

**Automaticamente:** via ```ng-app```

{% gist 5229926 %}

você pode passar também um nome opicional para o módulo

{% gist 5229865 %}

- **manualmente:** via ```angular.bootstrap```

{% gist 5229948 %}