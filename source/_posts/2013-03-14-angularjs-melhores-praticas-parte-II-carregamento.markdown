---
layout: post
title: "AngularJS: Melhores práticas - Parte II: Carregamento de scripts"
date: 2013-03-14 21:30
comments: true
categories: [angularjs, workflow, best pratices, requirejs]
published: true
---

{% img center /images/posts/cover-bestpratices-loading.jpg %}

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

{% codeblock lang:js %}
<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.0.4/angular.min.js"></script>
{% endcodeblock %}

Recomendo ter o arquivo no projeto também, para poder trabalhar offline e se aventurar pelo código! :)

## Bônus: Carregue seus scripts de forma assíncrona e gerencie suas dependencias

{% img center /images/posts/logo-requirejs.png %}

Caso prefira, saiba mais sobre os [benefícios de fazê-lo](https://gist.github.com/desandro/4686136) antes de continuar.

Este [demo](https://github.com/cironunes/ng-require) será usado para facilitar a explicação. É indispensável cloná-lo e navegar pelo código para entender como funciona.

Para conseguirmos fazer o carregamento assíncrono dos nossos scripts, primeiro precisamos entender como funcionar o “startup” do Angular.

## Angular startup

Sua aplicação pode ser iniciada de duas formas:

**Automaticamente:** via ```ng-app```

{% gist 5229926 %}

você pode passar também um nome opicional para o módulo

{% gist 5229865 %}

- **manualmente:** via ```angular.bootstrap```

{% gist 5229948 %}

Essa flexibilidade, nos possibilita carregar nossos recursos como bem entendermos, e quando estivermos prontos (callback) fazer o Angular [ler nosso HTML](http://docs.angularjs.org/api/ng.$compile) e dar vida as nossas diretivas.

**Atenção:** Para que possamos carregar nossos scripts em qualquer ordem, é necessário incluir o script a seguir, antes do carregamento do nosso módulo principal do RequireJS.

{% gist 5431503 %}

Depois basta fazer a chamada principal

```javascript
<script data-main="js/main.js" src="js/libs/require.js"></script>
```

O arquivo ```main.js``` deve se parecer com este:

```javascript
requirejs.config({
    baseUrl: 'js/libs',
    paths: {
        app: '../'
    }
});

requirejs([
    'angular',
    'app/app',
    'app/controllers',
    'app/filters',
    'app/services',
    'app/directives'
    ], function() {
        angular.bootstrap(document, ['myApp']);
});
```

Onde carregamos nossas dependências de forma assíncrona, e depois de tudo pronto, usamos o ``angular.bootstrap`` para fazer o startup manual.

Mais uma vez, recomendo fortemente dar uma olhada no código do [demo](https://github.com/cironunes/ng-require) para um entendimento mais claro.

Dúvidas? Não concorda com algo? Mande um e-mail ou deixe um comentário, só não deixe de me notificar! :)