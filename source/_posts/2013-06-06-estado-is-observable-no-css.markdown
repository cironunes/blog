---
layout: post
title: "Estado is-observable no CSS"
date: 2013-06-06 22:08
comments: true
categories: [smacss, oocss, bem, abstraction]
published: false
---

Se você é familiar com OOCSS, provavelmente conhece o objecto ```.media```que te poupa de escrevar **milhares de linhas de código**. O estado ```.is-observable``` também vai te livrar de bastante esforço repetitivo (DRY).

No SMACSS, uma das categorias para organizar o código é a de **estado** que segue o **open/closed principle** do **solid**. O estado ```.ìs-observable``` fará parte do seu arquivo ```state.css``` ou algo do tipo.

## mostrar/esconder no :hover

A idéia é criar de uma maneira bem declarativa, uma forma de mostrar/esconder elementos no ```:hover```.

### CSS
```
// is-observable
// --------------------
.is-hidden {
	display: none;
}
.is-observable:hover > .is-hidden {
	display: block;
}

.is-hidden--floated {
	position: absolute;
	visibility: hidden;
}

.is-observable:hover > .is-hidden--floatead {
	visibility: visible;
}
```

Caso esteja usando o Compass, esta versão vem com uma animação legal em CSS3 :)

### SCSS (Compass)

```
// is-observable
// --------------------
.is-observable:hover {
  .is-hidden {
    display: block;
  }
  .is-hidden--floated {
    visibility: visible;
    @include opacity(1);
  }
}

.is-hidden {
  display: none;
}
.is-hidden--floated {
  visibility: hidden;
  @include opacity(0);
  @include transition-property(opacity);
  @include transition-duration(.3s);
}
```

