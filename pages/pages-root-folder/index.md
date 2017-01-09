---
#
# Use the widgets beneath and the content will be
# inserted automagically in the webpage. To make
# this work, you have to use › layout: frontpage
#
layout: homejm1
header:
  image_fullwidth: homeheader.fw.png
widget1:
  title: ""
  url: 'http://www.jorgecast.com.br/'
  image: jorgecast.png
  text: 'O JorgeCast é um PodCast com uma assinatura própria, focado em Internet das Coisas e Produtos, não deixa de lado as raízes de desenvolvedor que tenho, e a vontade de mudar o mundo, sempre com muita diversão, tento trazer novidades, eventos, minha experiência e aprendizados do dia a dia.'
widget2:
  title: ""
  #url: 'http://phlow.github.io/feeling-responsive/info/'
  image: ctgTV.png
  text: 'Um canal recentemente criado, acompanhando a linha dos CrazyTechGuys, para quem ainda não conhece recomendo escutar os podcasts, neste canal vamos trazer tecnologia, aprendizados e muita diversão. '
  #video: '<a href="#" data-reveal-id="videoModal"><img #src="http://phlow.github.io/feeling-responsive/images/start-video-feeling-responsive-302x182.jpg" width="302" #height="182" alt=""/></a>'
widget3:
  title: ""
  #url: 'https://github.com/Phlow/feeling-responsive'
  image: transamerica.png
  text: 'Toda quarta-feira, além de muita informação sob o comando do Daniel Zukko do canal Minha Brasília, eu sou colunista no Transnotícias, ao meio dia em ponto no horário de Brasília. Um quadro sobre as novidades no mercado de tecnologia e discussões sobre o que foi pauta na semana. '
#
# Use the call for action to show a button on the frontpage
#
# To make internal links, just use a permalink like this
# url: /getting-started/
#
# To style the button in different colors, use no value
# to use the main color or success, alert or secondary.
# To change colors see sass/_01_settings_colors.scss
#
callforaction:
  url: https://tinyletter.com/feeling-responsive
  text: Inform me about new updates and features ›
  style: alert
permalink: /index.html
#
# This is a nasty hack to make the navigation highlight
# this page as active in the topbar navigation
#
homepage: true
---

<div id="videoModal" class="reveal-modal large" data-reveal="">
  <div class="flex-video widescreen vimeo" style="display: block;">
    <iframe width="1280" height="720" src="https://www.youtube.com/embed/3b5zCFSmVvU" frameborder="0" allowfullscreen></iframe>
  </div>
  <a class="close-reveal-modal">&#215;</a>
</div>
