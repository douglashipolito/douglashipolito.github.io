---
published: false
title: Resumo BrazilJS 2014 - Primeiro Dia
layout: post
tags: [js, braziljs, events]
categories: [JS, Events]
---
Bom pessoal, pretendo passar um pouco do que eu vi de interessante no BrazilJS.

##Service Worker - [Renato Mangini](https://github.com/mangini) _Google_

A primeira palestra foi bem interessante, falou sobre o Network Service, que é uma das especificações do [Service Worker](https://github.com/slightlyoff/ServiceWorker/blob/master/explainer.md).

Basicamente, este serviço irá gerenciar todas requisições da rede, você terá controle do que será entregue ou não e poderá manipular este conteúdo. Ele funciona da seguinte forma, você determina em qual url o Service Worker deverá ser instalado, neste primeiro acesso, o Network Service não será utilizado, a partir do próximo acesso o Network Service será utilizado e com ele, será possível ter controle das requisições, cache, cabeçalhos.. ele funciona como um proxy, algo que é bem similar a ele é o [AppCache](http://www.html5rocks.com/en/tutorials/appcache/beginner/), porém o AppCache se proprõe a ter controle dos arquivos e não das requisições.

<!-- more -->

Um exemplo do uso de um Service Worker:

```html
<!DOCTYPE html>
<!-- Acessing http://www.mysite.com/test.html -->
<html>
  <head>
    <script>
      navigator.serviceWorker.register("meuworker.js").then(
        function(serviceWorker) {
          console.log("Service Worker has been installed!");
          serviceWorker.postMessage("Some message");
        },
        function(why) {
          console.error("Something is wrong, let's take a look:", why);
        });
    </script>

  </head>
  <body>
    <!-- Bunch of html elements -->
  </body>
</html>
```
Neste caso, o Service Worker será instalado nesta url e só será acessível no próximo acesso, no caso de querermos o acesso ao Service Worker de forma imediata, nós simplesmente podemos dar um reload na página, assim:

```js
window.location.reload();
```
Isso irá dar um reload e já caíremos na página utilizando o Service Work, neste caso, utilizaremos o Network Service para gerenciar as requisições.

Qual seria o propósito desta especificação? Bom, simplesmente ter um controle de fato sobre a rede, sobre o que é requisitado, sobre o que poderá ser acessado offline e assim, melhorando a usabilidade dos sites, principalmente quando acessados através de dispositivos mobile.

##Frontend at Scale - The Tumblr Story - [Chris Miller](https://github.com/ee99ee) _Tumblr_

Nesta talk, o Chris Miller basicamente explicou como funciona o workflow deles no Tumblr. Primeiro, eles utilizam algumas ferramentas para agilizar o processo de desenvolvimento, que são elas:

* [Backbone](http://backbonejs.org/)
* [Sass](http://sass-lang.com/)
* [Bourbon](http://bourbon.io/)
* [VelocityJS](http://julian.com/research/velocity/) - Para animações
* [Gulp](http://gulpjs.com/) - Para automação de processos, similar ao GruntJS

Eles possuem algumas regras e padrões que garantem a qualidade de entrega, entre elas: 

* Ter uma equipe pequena, de no máximo 5 pessoas, para que o processo de desenvolvimento seja ágil
*  Utilizar testes A/B para todas as funcionalidades
* Ter a validação de duas pessoas antes do código ser considerado pronto
* Além de ter um programa de Beta Testers

É interessante observar toda essa preocupação com a entrega sem deixar de lado a agilidade, mantendo qualidade e agilidade juntas.

##Intro to GFX: Raw WebGL - [Nick Desaulniers](https://github.com/nickdesaulniers) _Mozilla_

Esta foi uma palestra um pouco difícil de entender, pois tratou basicamente de como lidar com WebGL puro, sem utilizar o [three.js](http://threejs.org/), é algo complicado e como é dito no início, trabalhar com programação gráfica envolve muita física e muitas coisas que você aprendeu e nunca teve a change de utilizar, como Geometria, Trigonometria, Algebra Linear..

Ele demonstra o que envolve o WebGL e o que é possível fazer com o mesmo. Um exemplo muito bom que foi feito foi a utilização da câmera em um objecto triângulo em um espaço 3D com uma animação de rotação.

Para quem quiser ver a palestra dele em vídeo, tem esta no youtube:

[HTMLDevConf](https://www.youtube.com/watch?v=H4c8t6myAWU)

Mas como eu falei, é algo meio complexo.

##Effective jQuery - [Jörn Zaefferer - bassistance](https://github.com/jzaefferer) _JQuery_

Esta palestra basicamente reforçou os conceitos de um bom uso do JQuery e como utilizá-lo de uma forma mais performática. Como utilizar `.prevAll` ao invés de `.prev` para que o JS não deixe de funcionar caso ocorra alguma mudança no html, foi dado um exemplo também de como controlar as animações CSS por javascript utilizando o [Jquery.Transit](http://ricostacruz.com/jquery.transit/).

##Web Versus Native - [Chris Mills](https://github.com/chrisdavidmills) _Mozilla_

Bom, este é um assunto bastante discutido, desenvolver apps nativas ou web? Qual tem a melhor performance? Qual é a mais segura? Nesta talk algumas destas respostas foram dadas, como por exemplo, o medo do não acesso a recursos nativos, que hoje, já foi superado.. ou seja, é possível acessar praticamente todos os recursos nativos de um dispositivo utilizando somente tecnologia web sem ter que partir para uma solução nativa. O destaque da palestra foi a apresentação dos recursos disponíveis no FirefoxOS, onde foi apresentado o conceito básico do mesmo:

* Roda em cima da engine Gecko
* Gaia como UI
* Gonk é o Kernel do FirefoxOS

O FirefoxOS funciona totalmente com tecnologias web, a definição da app é feita por um arquivo de manifesto e é possível gerar um pacote, para ser enviado para um servidor ou mesmo enviar para a Mozilla Marketplace.

As permissões são todas gerenciadas através do arquivo de manifesto, onde é definido ao que a aplicação terá acesso no dispositivo.

Ele possuí diversos recursos de controle do dispositivo, como vibrar, controle de iluminação, identificar quando houve alteração na luminosidade, orientação, NFC.

Outra preocupação é o controle dos recursos offline, existe o IndexDB, LocalStorage, WebSQL, AppCache.. mas ainda existe um problema com relação ao controle da rede, então com aposta entram os Service Workers, como foi apresentado na palestra do Renato Mangini.

E quanto a performance, é possível utilizar Pointer Lock, Web Workers, Asm.js e Emscripten para que a performance seja melhorada.

##Limpando CSS gigantes com JS - [Mauricio Wolff](https://github.com/bitbonsais) _Booking.com_

Nesta palestra, foi demonstrado como podemos tratar aqueles projetos que possuem CSS muito gigantes, principalmente os projetos legados, automatizando com JS.

A solução encontrada neste caso para resolver este problema de CSS duplicado e em desuso foi utilizar o chamado [CSS Selector Scene Investigation(CSSI)](https://github.com/bitbonsai/cssi), que avalia todo o css e compara com os templates na base do git.

##Single Page Application Done Right - [Eduardo Lundgren](https://github.com/eduardolundgren) _Liferay_

Single Page Application(SPA) é algo que tem sido feito por um bom tempo, desde os anos 2000.. e ele se propõe a melhorar a usabilidade para usuário, como ele percebe a página fluindo, suas ações sendo executadas. Em uma SPA a execução da ação requerida pelo usuário é executada de uma forma mais rápida, pelo menos, na percepção de quem executou a ação porque a página não será toda recarregada novamente, somente parte da página. Um exemplo, em uma página com um cabeçalho, conteúdo e rodapé, normalmente só o conteúdo que é alterado ao clicar em um link, o restante da página continua igual. Em uma página comum, o clique em link dispara uma nova requisição para servidor que entrega um html inteiro para o browser que faz o reload novamente de tudo, mesmo que somente o conteúdo tenha mudado.. com SPA, será entregue somente a parte importante que deve ser recarregada.

Isso basicamente diz respeito a como a performance é percebida, existem diversas formas de percepção de performance, tempo de load de uma load pode ser uma métrica para performance, mas não necessariamente isso quer dizer que a página está tendo uma boa performance, a forma como o usuário percebe esta página que faz diferença. Como o Eduardo cita na palestra:

> "Performance is not just milliseconds and bytes. It's also how milliseconds and bytes translate to **how the user perceives the app**"
> 
> ilya grigorik - Developer Advocate, Google

A forma mais comum de utilizar SPA é com Ajax, mas antes mesmo do ajax, a técnica utilizada era com iframes, para ter esse comportamento, mas como é sabido, com iframes se perde a indexação, url específica para o conteúdo entre outros problemas. Neste caso, o melhor recurso é utilizar Ajax, porém existem algumas que foram levantados, vamos dar uma olhada nos métodos disponíveis de SPA:

###Ajax

Neste método, o conteúdo é carregado com base na requisição XHR, porém a url não é alterada e este é um grande problema pois vai contra o princípio da internet, que é linkar "coisas", linkar conteúdo, não existe uma forma de acessar o conteúdo com base na url.

###Hijax

Este método faz o mesmo que o anterior, porém, nele possuímos uma url para o conteúdo adicionando uma hash a url, como por exemplo, #contato. Neste caso, o problema com a url foi resolvida, mas só que isso não resolve o problema do conteúdo, o conteúdo será chamado por ajax, então, inicialmente ele será sempre o mesmo até que a requisição seja concluída, normalmente ficará com um load ou algo parecido e isso é ruim para SEO e compartilhamento. O ideal é que exista um conteúdo real para cada url, que não dependa somente da requisição ajax.

Outro problema que normalmente ocorre utilizando SPA é perder a referência do histórico de navegação no back e forward buttons, uma forma de manipular e corrigir esse problema é utilizando o History API, que proporciona um controle maior do histórico de navegação.

Outra questão é o controle do estado de onde o usuário estava, por exemplo, em um scroll infinito, caso o usuário já esteja na página 10 e ele queira voltar para página anterior através do back button e após voltar novamente para esta pagina, ele precisa ser posicionado exatamente onde ele estava antes, no caso na página 10 do infinite scroll.

Então, para resolver a maioria dos problemas com SPA, o Eduardo Lundgren lançou uma engine chamada [SENNA.JS](http://sennajs.com/) para single page applications que se propõe a resolver todos estes problemas de uma forma super simples e objetiva. Mas o interessante é antes de chegar nesta solução, eles procuraram bastante, mas nenhuma solução existente comportava o que eles queriam, que era transformar qualquer página em SPA. A idéia no futuro é fazer uma integração com web componente para que tenha mais performance ainda. 

Segundo os testes feitos por ele, uma página que carregava 1.3MB a cada load, passou a carregar somente 22.7KB, o que aumentou muito a percepção de performance.

Esta é uma engine que vale a pena dar uma olhada e deixo o link para os slides da apresentação abaixo.

https://speakerdeck.com/eduardolundgren/single-page-applications-done-right

##The 7 Principles of rich web applications - [Guillermo Rauch](https://github.com/guille) _LearnBoost/Cloudup_

Nesta palestra foi defendida a idéia de melhorar a experiência do usuário com JS. O que seria, não exibir uma página em branco para o usuário, gerenciar as requisições por js para que isso não ocorra. Controlar como o conteúdo está distribuído, utilizar uma CDN para que o conteúdo seja carregado de uma forma mais eficiente. 

Utilizar técnicas que indicam que o conteúdo está sendo carregado, como placeholders, loading spinners.. porém ele ressaltou que requisições com menos de 1 segundo eliminam a necessidade de loaders.

Controle da rede, identificando quando existe conexão e quando não existe, dando este feedback para usuário e também conseguindo sincronizar corretamente quando existir a conexão novamente, uma opção para controle da rede, novamente, o Service Worker. E outro ponto levantado foi conseguir sincronizar entre os diversos dispositivos de uma forma eficiente.

De uma forma geral, o primeiro dia trouxe boas idéias e tecnologias a serem estudadas, destacando [SENNA.JS](http://sennajs.com/)  e o [Service Worker](https://github.com/slightlyoff/ServiceWorker/blob/master/explainer.md).