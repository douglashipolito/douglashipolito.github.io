---
published: true
title: Entendendo o :nth-of-type
layout: post
tags: [css, tricks, tutorial]
categories: [CSS]
---
No momento em que estamos hoje, é muito provável que você já tenha ouvido falar ou utilizado
a pseudo-classe **:nth-of-type(n)** ou mesmo o **:nth-child(n)**, porém eu gostaria de
abordar o funcionamento desta pseudo-classe de uma forma mais simples e talvez esclarecer
algumas dúvida que você ainda possa ter.

Pretendo detalhar seu funcionamento, explicando com exemplos das expressões e abordar as expressões
matemáticas envolvidas.

##Conceito

Bom, para começar, o **:nth-of-type** trabalha basicamente com um ramo da matemática
chamado [sequências](http://pt.wikipedia.org/wiki/Sequ%C3%AAncia_matem%C3%A1tica).

<!-- more -->

> Uma sequência ou sucessão é qualquer conjunto organizado de objectos, números ou eventos de qualquer natureza. Para representar uma sucessão escrevem-se os seus elementos numa lista pela sua ordem bem determinada entre parêntesis. Frequentemente nos deparamos com situações em que enumeramos elementos de um conjunto seguindo uma determinada ordenação:
>
  1. Da sucessão dos presidentes de um país;
  2. Da sequência dos episódios de uma minissérie de televisão;

Ou seja, sequência é todo grupo ou conjunto no qual seus elementos estão definidos em uma determinada ordem e é nisto que esta pseudo-classe se baseia.

##nth-of-type(N)

O argumento `N` pode ser um inteiro, uma palavra-chave ou uma expressão de (an+b).

###Expressão (an+b)###

Está expressão é bem simples e entendendo ela, você poderá fazer qualquer combinação(dentro das restrições) e entender complementamente o que está acontecendo.

Explicando melhor:

###an - iterações###

O `a` representa o valor de iteração, ou seja, basicamente o número de grupo de elementos. Um exemplo, `5n`:

(5 x 0) + 0 = 0<br />
(5 x 1) + 0 = 5<br />
(5 x 2) + 0 = 10<br />
(5 x 3) + 0 = 15<br />
(5 x 4) + 0 = 20<br />

Esta regra fica mais ou menos assim, a cada 5 elementos + o deslocamento inicial(b), selecione o elemento cujo índice seja igual ao resultado desta expressão.

Neste caso, os elementos com índices `5`, `10`, `15` e `20` serão selecionados, o primeiro resultado, o `0` será ignorado pois os elementos devem ser selecionados com índices começados em 1 e 0 não é um índice válido neste caso.

Como é possível perceber, a fórmula ficou (a x n) + **0**, este zero foi adicionado devido a omissão do valor de deslocamento inicial(`b`), se ele for omitido, este valor será considerado como 0.

###b - deslocamento inicial###

O `b` representa o valor de deslocamento inicial, ou seja, o índice pelo qual a busca será iniciada dentro do grupo. Seu valor pode ser tanto positivo, negativo ou zero.

Considere o seguinte exemplo:

{% highlight css %}
p:nth-of-type(5n+2)
{% endhighlight %}

Neste exemplo possuímos uma regra para iterar a cada 5 elementos e iniciar pelo elemento de índice 2 com base na iteração atual dentro do loop, por exemplo, considerando que estamos no terceiro loop desta iteração, no caso, no índice 2:

5 x 0 = 0<br />
5 x 1 = 5<br />
**5 x 2 = 10**<br />

O resultado será `10`, mas possuímos o `b` para processar ainda, então o resultado da iteração + `b` será o índice do elemento que procuramos nesta sequência, que seria 10 + 2 = **12**, logo, o elemento de índice `12` seria selecionado.

Um exemplo em forma matemática:

(5 x 0) + 2 = 2<br />
(5 x 1) + 2 = 7<br />
(5 x 2) + 2 = 12<br />
(5 x 3) + 2 = 17<br />

Agora em um exemplo real aplicado ao css:

<p data-height="300" data-theme-id="5971" data-slug-hash="CpfcH" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/douglashipolito/pen/CpfcH/'>nth-of-type - 5n+2</a> by Douglas Hipolito (<a href='http://codepen.io/douglashipolito'>@douglashipolito</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>
<small>* pressione o botão "unselect elements" para desfazer a seleção dos elementos</small>

Neste exemplo possuímos 8 elementos, uma lista com 10 LIs e para facilitar, o conteúdo de cada LI está sendo representado de forma numérica. Os elementos que possuem como conteúdo os valores "2" e "7" foram selecionados, confirmando a expressão, ou seja, se mais dois elementos fossem adicionados, o elemento com conteúdo "12" seria selecionado e assim sucessivamente.

##Expressões com valores negativos

É possível utilizar valores negativos nas expressões, porém é necessário sempre ter um valor positivo ou para o `an` ou para o `b`.

###Valores negativos para o deslocamento inicial(b)###

Ao utilizar um valor negativo para o deslocamento inicial, indicamos que após obter o resultado de (a x n), desejamos que o índíce do elemento que será selecionado deverá ser igual ao resultado de (a x n) - o deslocamento inicial(b), sendo assim, ao invés de ir da esquerda para direita, iremos da direita para esquerda.

Um exemplo `5n-2`:

(5 x 0) - 2 = -2<br />
(5 x 1) - 2 = 3<br />
(5 x 2) - 2 = 8<br />
(5 x 3) - 2 = 13<br />

Por consequência da subtração de 2 do resultado (a x n), o deslocamento iniciou-se da direita para esquerda. Esta é uma forma bem útil de inverter a expressão e começar pelos últimos elementos de cada grupo, sendo mais ou menos como dizer algo parecido com: "selecione os dois últimos elementos a cada 5 elementos começando em zero".

Este detalhe:

> selecione os dois últimos elementos a cada 5 elementos começando em **zero**

Este **zero** deve ser levado em consideração, nesta caso, se for contar de trás para frente em cada grupo, a contagem deverá começar em zero e não em um, por exemplo:

<table>
  <thead>
    <tr>
      <th>Elemento</th>
      <th>Índice</th>
      <th>Selecionado</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>5</td>
      <td>0</td>
      <td>não</td>
    </tr>
    <tr>
      <td>4</td>
      <td>1</td>
      <td>não</td>
    </tr>
    <tr>
      <td>3</td>
      <td>2</td>
      <td><strong>sim</strong></td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>não</td>
    </tr>
    <tr>
      <td>1</td>
      <td>4</td>
      <td>não</td>
    </tr>
  </tbody>
</table>

Veja como ficou a seleção em um exemplo real:

<p data-height="300" data-theme-id="5971" data-slug-hash="fIzEG" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/douglashipolito/pen/fIzEG/'>nth-of-type - 5n+2</a> by Douglas Hipolito (<a href='http://codepen.io/douglashipolito'>@douglashipolito</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

#####Omissão de valores#####

Se `an` for omitido ele será considerado como `0n`, seguindo o mesmo exemplo `5n-2`, mas o omitindo o `5n`, teriamos o seguinte resultado:

(0 x 0) - 2 = -2<br />
(0 x 1) - 2 = -2<br />
(0 x 2) - 2 = -2<br />

Ou seja, neste caso, não é permitido a omissão do `an` pois o resultado será sempre negativo, só é permitido com valores positivos.

###Valores negativos para iteração(an)###

Ao passar um valor negativo para o valor de iteração você estará dizendo que quer iterar sobre -n elementos, parece não funcionar, mas como precisamos somar com o `b`, este valor volta a ser positivo conforme os loops. Vamos ver melhor isso.

Vejamos este exemplo: `-1n+2`

Representando matematicamente:

((-1) x 0) + 2 = 2<br />
((-1) x 1) + 2 = 1<br />
((-1) x 2) + 2 = 0<br />

Assim, teremos o resultado de selecionar os elementos em ordem até um certo limite, neste caso, selecionar até o segundo elemento, veja como ficou o exemplo real:

<p data-height="300" data-theme-id="5971" data-slug-hash="kmczu" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/douglashipolito/pen/kmczu/'>nth-of-type - 5n+2</a> by Douglas Hipolito (<a href='http://codepen.io/douglashipolito'>@douglashipolito</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

Outro exemplo, selecionando até o oitavo elemento:

<p data-height="300" data-theme-id="5971" data-slug-hash="erhKc" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/douglashipolito/pen/erhKc/'>nth-of-type - 5n+2</a> by Douglas Hipolito (<a href='http://codepen.io/douglashipolito'>@douglashipolito</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

Foi utilizado `-1n`, mas não é necessário expressar o `-1`, se um valor númerico não for passado, será assumido o `1` como valor.

Como é possível perceber, está expressão é bem útil, de uma forma bem simples selecionamos varios elementos ao mesmo tempo com um limite definido, `-n+2`, neste caso, até o segundo elemento.

#####Omissão de valores#####

Assim como para o deslocamento inicial(b), não é permitido a omissão do deslocamento inicial quando o valor de iteração for negativo ou mesmo valores negativos no deslocamento inicial.

##Seleção de elementos entre faixas

Tanto o :nth-of-type quanto o :nth-child e seus derivados são excelentes, ajudam muito e são muito bem feitos, além de terem estas seleções mais simples, é possível também fazer seleções mais complexas, como por exemplo, selecionar entre faixas, vamos ver alguns exemplos.

Considerando um exemplo como: "Queremos selecionar todos elementos entre 3 e 8".

Para que isso seja possível, devemos utilizar duas vezes o :nth-of-type, assim:

{% highlight css %}
p:nth-of-type(n+3):nth-of-child(-n+8)
{% endhighlight %}

Desta forma vamos conseguir selecionar entre a faixa especificada, mas vejamos como isto ficaria visto de forma matemática:

(1 x 0) + 3 = 3<br />
(1 x 1) + 3 = 4<br />
(1 x 2) + 3 = 5<br />
 +<br />
((-1) x 0) + 8 = 8<br />
((-1) x 1) + 8 = 7<br />
((-1) x 2) + 8 = 6<br />
((-1) x 3) + 8 = 5<br />
((-1) x 4) + 8 = 4<br />
((-1) x 5) + 8 = 3<br />
((-1) x 6) + 8 = 2<br />
((-1) x 7) + 8 = 1<br />
((-1) x 8) + 8 = 0<br />

É possível ver claramente como será o resultado, no primeiro caso será selecionado a partir do terceiro elemento e deveria seguir até o fim, ou seja, selecionar todos elementos a partir do terceiro elemento, mas devido a segunda regra aplicada, será selecionado do oitavo elemento até primeiro e juntando as duas regras, ficará de 3 até 8 ou de 8 até 3.

Vamos ver o exemplo real:

<p data-height="300" data-theme-id="5971" data-slug-hash="ijdEg" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/douglashipolito/pen/ijdEg/'>nth-of-type - 5n+2</a> by Douglas Hipolito (<a href='http://codepen.io/douglashipolito'>@douglashipolito</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

Sabendo disso, é possível fazer diversas combinações, criar diversos ranges. Só ter em menter qual será a regra matemática aplicada nesta pseudo-classe.

Bom, agora eu já falei bastante sobre a expressão (an+b), vamos ver agora sobre os outros dois valores do argumento N, as palavras-chaves e os valores numéricos.

##Palavras-chaves

Existem duas palavras-chaves que são na verdade atalhos para uma expressão.

###odd###

A palavra-chave `odd` serve para selecionar elementos ímpares e sua sintaxe é assim:

{% highlight css %}
p:nth-of-type(odd)
{% endhighlight %}

Isto é um atalho para `2n+1`, onde sua representação matemática fica assim:

(2 x 0) + 1 = 1<br />
(2 x 1) + 1 = 3<br />
(2 x 2) + 1 = 5<br />
(2 x 3) + 1 = 7<br />

Vejamos o exemplo real:

<p data-height="300" data-theme-id="5971" data-slug-hash="noLjH" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/douglashipolito/pen/noLjH/'>nth-of-type - 5n+2</a> by Douglas Hipolito (<a href='http://codepen.io/douglashipolito'>@douglashipolito</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

###even###

A palavra-chave `even` serve para selecionar elementos pares e sua sintaxe é assim:

{% highlight css %}
p:nth-of-type(even)
{% endhighlight %}

Isto, assim como `odd`, é um atalho também, mas só que para expressão `2n+2`, onde sua representação matemática fica assim:

(2 x 0) + 2 = 2<br />
(2 x 1) + 2 = 4<br />
(2 x 2) + 2 = 6<br />
(2 x 3) + 2 = 8<br />

Vejamos o exemplo real:

<p data-height="300" data-theme-id="5971" data-slug-hash="GrzFo" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/douglashipolito/pen/GrzFo/'>nth-of-type - 5n+2</a> by Douglas Hipolito (<a href='http://codepen.io/douglashipolito'>@douglashipolito</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

##Valores numéricos

Os valores numéricos representam basicamente a posição exata do elemento que se deseja selecionar, como por exemplo:

{% highlight css %}
p:nth-of-type(2)
{% endhighlight %}

Isto irá selecionar exatamente o segundo elemento.

<p data-height="300" data-theme-id="5971" data-slug-hash="bJgwx" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/douglashipolito/pen/bJgwx/'>nth-of-type - 5n+2</a> by Douglas Hipolito (<a href='http://codepen.io/douglashipolito'>@douglashipolito</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

Isto tem o mesmo efeito que `0n+2`, pois, estamos omitindo o `an` e quando ele é omitido automaticamente o valor `0n` é assumido, e quando omitimos o `an` somos obrigados a fornecer um valor positivo, sendo assim o `2` já fica subentendido como positivo.

##Finalização

Bom, espero que este artigo tenha sido útil para esclarecer qualquer dúvida com relação esta pseudo-classe e a lógica por trás do nth.

O artigo ficou meio extenso, mas acredito que ficou de uma forma simples e de fácil entendimento. Espero que ele tenha sido útil para você se aventurar mais nos nth-*.

Qualquer dúvida, só perguntar :)

###Referências e materiais para estudo

  * [w3c - css3-selectors](http://www.w3.org/TR/css3-selectors/#nth-child-pseudo)
  * [css-tricks](http://css-tricks.com/how-nth-child-works/)
  * [site-point](http://reference.sitepoint.com/css/understandingnthchildexpressions)
  * [nth-master](http://nthmaster.com/)
