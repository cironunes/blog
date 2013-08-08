---
layout: post
title: "AngularJS: Melhores práticas - Parte I: Iniciando projetos"
date: 2013-03-10 16:01
comments: true
categories: [angularjs, yeoman, workflow, best pratices]
---

{% img center /images/posts/cover-bestpratices-bootstrap.jpg %}

Melhores práticas são como fórmulas mágicas para ajudar na organização do seu projeto, documentadas por desenvolvedores que tiveram sucesso usando elas em diversas situações.

Nesta série vou compartilhar algumas técnicas que tornam meu trabalho cada vez mais simples e divertido.

Essas práticas foram baseadas [neste vídeo](http://www.youtube.com/watch?v=ZhfUv0spHCY&feature=g-user-u) e nas minhas experiências diárias.

<!-- more -->

## Por que eu preciso organizar meu projeto?
- **Facilitar a manutenção**
- **Aumentar a velocidade de desenvolvimento**
- **Identificar problemas antecipadamente**

## Navegue pela série
- [Parte I - Iniciando um projeto e a estrutura de diretórios](/angularjs-melhores-praticas-parte-I-bootstrap)
- [Parte II - Carregamento de scripts](/angularjs-melhores-praticas-parte-II-carregamento)
- Parte III - Dicas e truques
- Parte IV - MVC

## Iniciar um projeto e a estrutura de diretórios
Esta é a etapa mais importante, e pode definir o sucesso ou fracasso do nosso projeto. Aqui surgem várias dúvidas e teremos bastante trabalho:

- Como organizar a estrutura de diretórios? (Criar os diretórios manualmente)
- Quais serão as dependências? (Baixar cada uma e adicionar manualmente no projeto)
- Como vou preparar pacotes para produção? (Instalar ferramenta de build e configurá-la manualmente)

Não reinvente a roda! Existem vários "bootstraps" para fazer estas coisas de forma automatizada, padronizada e seguindo as boas práticas:

## [Angular Seed](http://github.com/angular/angular-seed) e variações ([Express + Socket.IO](http://github.com/btford/angular-socket-io-seed/), [Express](http://github.com/btford/angular-express-seed))*
Mantidos pelos próprios membros do time do Angular, os 'seeds' são repositórios que você simplesmente clona:

```
$ git clone git@github.com:angular/angular-seed.git
```

apaga as referências para o repositório original:

```
$ rm -rf .git
```

E está pronto para começar seu projeto com:

- **Estrutura de diretórios bem organizada e padronizada**: o que facilita encontrar as coisas até mesmo se for a primeira vez que alguem esteja vendo seu projeto.
- **Suites de testes unitários e [e2e](http://docs.angularjs.org/guide/dev_guide.e2e-testing)**
- **Scripts para rodar os testes inclusive de forma contínua.**

**Os seeds de Express e Socket.IO não vem com a suite de testes, mas é só você copiar do seed principal :)*

Incrível! Mas pode ser ainda melhor, atualmente o time do Angular recomanda o uso do Yeoman.

## Yeoman
{% img center /images/posts/logo-yeoman.png %}
O [Yeoman](http://yeoman.io) é uma ferramenta para facilitar nosso workflow, independente das libraries e frameworks Front-end que vamos usar. Ele utiliza de outras ferramentas incríveis: [Grunt](http://gruntjs.com/) e [Bower](http://twitter.github.com/bower/), para te ajudar a:

- **Inicializar projetos**: criar toda a estrutura de diretórios e configurar a suite de testes
- **Gerencias dependencias**: adicionar, remover e atualizar recursos
- **Criar pacotes**: preparar seus releases para testes ou para produção
- **Executar testes automatizados**
- **Manter recursos do framework**: no caso do AngularJS, criar controllers, views, rotas, etc.

Depois de instalar o Yeoman (veja como instalar no [site oficial](http://yeoman.io)), instale os generators para o Angular:

```
$ npm install generator-angular generator-testacular
```

Inicie um novo projeto:

```
$ yo angular [nome-da-app]
```

O Yeoman vai te perguntar se você deseja usar o Twitter Bootstrap. Se sim, prefere uma versão com o Compass? (Eu particularmente prefiro). Depois se quer incluir os módulos: [```angular-resource```](http://docs.angularjs.org/api/ngResource.$resource), [```angular-cookies```](http://docs.angularjs.org/api/ngCookies.$cookies), [```angular-sanitize```](http://docs.angularjs.org/api/ngSanitize.$sanitize). Recomendo que responda sim para todos, mas você pode incluí-los a qualquer momento usando o Bower.


Feito isso, instale as depencias:

```
$ npm install && bower install --dev
```

Instale o ```angular-mocks``` para os testes funcionarem corretamente:

```
$ bower install angular-mocks
```

Então você já pode rodar seus testes:

```
$ grunt test
```

Rodar sua aplicação em ambiente local:

```
$ grunt server
```

E gerar um pacote para produção:

```
$ grunt
```

Além disso você pode usar os geradores para criar seus controllers, views, services, directives, filters e routes:

```
$ yo angular:controller myCtrl
$ yo angular:view myView
$ yo angular:service myService
...
```
O mais interessante é que além de criar os arquivos e incluí-los no meu HTML automaticamente com os nomes e lugares corretos, ele já cria a ```spec```correspondente na minha suite de testes, incentivando sempre a fazer [TDD](http://en.wikipedia.org/wiki/Test_Driven_Development).

Dúvidas? Não concorda com algo? Mande um [e-mail](mailto:ciroanunes@gmail.com) ou deixe um comentário, só não deixe de me notificar! :)

Por hoje é só!