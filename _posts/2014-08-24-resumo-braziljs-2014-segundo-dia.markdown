---
published: false
title: Resumo BrazilJS 2014 - Segundo Dia
layout: post
tags: [js, braziljs, events]
categories: [JS, Events]
---
Continuando o resumo sobre o BrazilJS de 2014, vou passar o que achei de mais interessante neste dia.

##From commit to prod in 5 minutes - [Jacob Page](https://github.com/DullReferenceException) _GoDaddy_

Nesta palestra, Jacob abordou como eles utilizavam o git na GoDaddy, mais focado em como eram tratadas as novas funcionalidades, através de branchs, porém isto este processo era bastante demorado e cansativo.

O primeiro passo para melhorar o fluxo na GoDaddy foi implementar Continuous Integration(CI), Continuous Delivery(CD) e implementar um fluxo do github de pull requests, onde eram feitos testes e validações do código.

<!-- more -->

Eles passaram a utilizar diversos recursos e ferramentas que agilizaram todo o processo de implementação e controle.

Algumas ferramentas citadas:

* [Jira](https://www.atlassian.com/software/jira) - Gerenciamento dos projetos
* [New Relic](http://newrelic.com/) - Monitoramento
* [Slack](https://slack.com/) - Comunicação
* [Github](github.com) - Versionamento de código

Frameworks e libs utilizados:

* [Mocha](http://visionmedia.github.io/mocha) - Testes
* [Chai.js](http://chaijs.com/) - Assertion
* [Selenium](http://www.seleniumhq.org/) - Automatização
* [Istanbul](http://gotwarlost.github.io/istanbul) - Cobertura de testes

E legal ver como todas estas ferramentas, bibliotecas se integraram para gerar um ótimo fluxo de publicação de novas funcionalidades.

##Frontend was always my favorite color - [Ricardo Tomasi](https://github.com/ricardobeat) _Booking.com_

O Ricardo apresentou quais foram as lições aprendidas na vida em desenvolvimento de projetos.

A primeira coisa que ele fala é, não tenha medo de compartilhar código, idéias, compartilhe sempre, não tenha medo de receber um não, de ser criticado, sempre compartilhe com as pessoas, isso vai fazer com que você evolua como desenvolvedor e como pessoa, aprendendo com os outros e com os seus próprios erros. E tenha em mente que o código nunca será perfeito, sempre terá alguém que achará ruim e que irá querer melhora-lo, então tenha em mente que o código é orgânico, ele tem um tempo de vida, em pouco tempo irá surgir alguma lib melhor do que a sua. Então a questão é, desenvolva, compartilhe, e não tenha medo de ser criticado e não tente desenvolver o código perfeito, pois você só irá perder tempo, se preocupe em desenvolver aos poucos e ir melhorando o código.

Outra ponto importante que ele levantou, é importante aprender Ciências da computação, porque ele mesmo não é formado em nenhuma área relacionada a TI e teve que aprender boa parte dos conceitos de Ciência da Computação. Boa parte dos fundamentos serve para qualquer desenvolvedor, que ajudam desenvolver um código conciso.

E por último, lembre que estamos trabalhando com pessoas, precisamos saber lidar com elas, trabalhar em equipe, não ficar discutindo por coisas que não agregam ao projeto, tentar sempre chegar em um acordo.

##Mastering IE’s updated F12 tools - [Jonathan Sampson](https://github.com/jonathansampson) _Microsoft_

Nesta palestra Jonathan veio apresentar como a Microsoft tem se esforçado para transformar o IE em uma ótima ferramenta para os desenvolvedores, e realmente, o IE está evoluindo mesmo.

Basicamente ele apresentou as melhorias no Developer Tools do IE, ela possuí varios recursos para debug, como perfil do consumo de memória, breakpoints no JS, e outros recursos já conhecidos no Firefox e Chrome.

##The Web Component Ecosystem - [Rob Dodson](https://github.com/robdodson) _Google_

Nesta palestra, Rob Dodson mostrou como funciona o ecosistema dos web components.

Iniciou dando exemplos de como funcionam os componentes hoje na web, onde normalmente, digamos, quando precisamos de tabs, procuramos por algum biblioteca JS e olhamos no README para entender como devo proceder para que ela funcione corretamente no meu projeto, ok, sem grande dificuldades, o grande problema é que este "componente" não fica encapsulado e basicamente são varias tags html sem uma semântica clara que identifique que aquele conjunto de elementos seria um componente de tabs, e também, cada implementação de um componente de tab é diferente do outro, não existe um padrão. Os Web Componentes vieram para isso, padronizar, encapsular componentes e facilitar o reuso.

Os Web Components ainda não possuem um bom suporte em todos os browsers, então, para isso, foi criado o [Polymer](http://www.polymer-project.org/) que permite que utilizemos os Web Componentes com os browsers existentes.

Foi apresentado componentes do [Material Design](http://www.google.com/design/spec/material-design/introduction.html), chamados de [Paper Elements](http://www.polymer-project.org/docs/elements/paper-elements.html) que facilitam o reuso de componentes com o conceito do Material Design, além do [Core Elements](http://www.polymer-project.org/docs/elements/core-elements.html) do polymer que possui diversos custom elements visuais e não visuais. 

Algo que foi repetido varias vezes é que, isso não é a google que está fazendo, somos todos nós, ou seja, ele basicamente falou para experimentar, testar, contribuir para fazer com que os Web Components evoluam e façam da web algo mais simples de se trabalhar e mais organizada.

##Data-binding [R]evolution - [Leonardo Balter](https://github.com/leobalter) _Bocoup_

Leo Balter apresentou como está ocorrendo a evolução do Data-binding. Data-binding é o processo que indica a relação entre os dados e a aplicação, mas precisamente com a interface da aplicação.

Algo que foi apresentado bem interessante é uma especificação do ES6 chamada _proxies_ que consiste em permitir que objetos possam ser monitorados, por exemplo, quando o valor de uma propriedade for alterada.

##AST, CST e Ferramentas Incríveis - [Miller Medeiros](https://github.com/millermedeiros) _Mozilla_

Nesta palestra foi apresentada de uma forma simples, qual seria a utilidade de um AST e CST em projetos javascript.

AST é uma representação do código de uma forma abstrata ou em formato de árvore e que será alterado, ele é utilizado para descrever a estrutura original do programa antes que seja convertido.

E a utilidade de utilizar AST, é entender como os parsers funcionam, como por exemplo: 

* lint/validação
* minificação
* formatação
* refactoring
* compilers

O parser mais conhecido de javascript é o [Esprima](http://esprima.org/), a execução dele retorna um objeto JSON com a análise léxica do código.

Já o CST é a representação concreta do código, porém não existe nenhum padrão de CST para javascript, porém o palestrante desenvolveu sua própria lib para formatar códigos javascript chamada [Esformatter](https://github.com/millermedeiros/esformatter). Além de outra contribuição chamada [Nodify](https://github.com/millermedeiros/nodefy) que converte padrão de módulos AMD para Node.js.

##A Day in the Life of an Ember Developer - [Yehuda Katz](https://github.com/wycats) _Tilde Inc._

O foco da palestra foi em cima de como o Ember trabalha com data-binding.

Ele mostrou diversas formas de trabalhar com data-binding, mostrando como é possível alterar o template, a informação contida no template assim que os dados são alterados.

##Making 3D Graphics Accesible - [Ricardo Cabello (Mr. Doob)](https://github.com/mrdoob)

Ricardo Cabello é criador da biblioteca [three.js](http://threejs.org/) que pode ser considerada como o JQuery para computação gráfica, porque com está biblioteca, o desenvolvimento de aplicações 3D ficou simplificado.

Antes do HTML5, a unica forma de exibir uma animação 3D era com Flash Player e com a entrada do HTML5 isso acabou.

Nesta palestra, Ricardo apresentou um série de exemplos, demonstrações do uso do three.js e realmente, existem muitas funcionalidades, muito potencial e só depende do desenvolvedor utilizá-las. Ele apresentou também uma para edição de frames em 3D no próprio browser.

A palestra dele impressionou muitas pessoas, foi muito aplaudido no final por seu empenho neste projeto que provavelmente irá substituir as ferramentas desktop de edição 3D ou pelo menos será uma ótima opção para grande maioria das empresas.

