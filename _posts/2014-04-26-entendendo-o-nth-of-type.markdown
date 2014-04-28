---
published: true
title: Entendendo o :nth-of-type
layout: post
tags: [css tricks tutorial]
categories: [CSS]
---
No momento em que estamos hoje é muito provável que você já tenha ouvido falar
na pseudo-classe **:nth-of-type** ou mesmo no **:nth-child**, porém eu gostaria de
abordar o funcionamento desta pseudo-classe de uma forma mais simples e talvez esclarecer
algumas dúvida que você ainda possa ter.

##Conceito

Pretendo explicar de uma forma simples como funciona esta pseudo-classe, existe
a documentação oficial do [:nth-of-type](http://www.w3.org/TR/css3-selectors/#nth-of-type-pseudo),
mas ela pode ser um tanto confusa e podendo até gerar mais dúvidas..

Bom, para começar, **:nth-of-type** basicamente trabalha com um ramo matemático
chamado [sequências](http://pt.wikipedia.org/wiki/Sequ%C3%AAncia_matem%C3%A1tica).
Vamos ver um exemplo prático utilizando a pseudo-classe:

{% highlight css %}
p:nth-of-type(5n+3)
{% endhighlight %}

<!-- more -->
