<h1>Redes Geradoras Adversariais na Criação de Jogos Digitais</h1>

<p align="justify">Resolvi tentar treinar meu computador para criar gráficos de jogos ao estilo anos 80/90 sozinho e para isso utilizei um conceito criado não faz nem 10 anos: Redes Neurais Adversariais ou simplesmente GAN!</p>

<h3>Para criar precisa-se conhecer</h3>

<p align="justify">Quando é dada uma foto de um quarto a um ser humano, este consegue assimilar rapidamente os objetos na foto, observando o piso, cor da parede, cama, portas, janelas, e até consegue reproduzir o desenho de um novo quarto. Já para um computador essa imagem é apenas uma matriz de números, o computador não consegue compreender a imagem na fotografia, muito menos criar novos quartos.</p>

<p align="justify">Os avanços tecnológicos dos últimos anos, que tornaram possível o processamento e a análise semântica de grandes bancos de dados, impulsionaram o desenvolvimento rápido de diversos modelos de visão computacional, em especial modelos que utilizam o aprendizado de máquina para a geração de conteúdo, os chamados modelos geradores. Um dos mais reconhecidos atualmente foi publicado em 2014, por Ian Goodfellow, que propôs um modelo chamado de <a href="https://papers.nips.cc/paper/5423-generative-adversarial-nets.pdf">Generative Adversarial Networks</a> (GANs). Esse modelo foi o pioneiro em utilizar uma iteração inteligente entre duas redes neurais profundas que competem entre si para gerar conteúdo, utilizando uma base de dados pré-estabelecida.</p>

<p align="justify">As GANs surgiram como meio de treinar computadores a entenderem conceitos sem que seja explicitamente ensinado o significado desses conceitos, o tornando mais eficiente que os métodos tradicionais que dependem de humanos pré-rotulando dados, e desde então, tem ganhado destaque dentre os pesquisadores pois sua capacidade de assimilar dados brutos o torna um poderoso método de inteligência artificial. Voltando ao exemplo anterior, agora utilizando GANs o computador pode, depois de exposto a milhares de fotos de quartos, gerar novos quartos por conta própria, ou seja, o computador conseguiu assimilar o conceito de quarto e produzir imagens sem a intervenção de um ser humano.</p>

<p align="justify">Na imagem abaixo temos quartos criados por um computador:</p>

<img  src=ImagensReadme/DCGAN-quartos.png> 

<p align="justify">E na área de jogos digitais, é indiscutível a importância da geração automática de conteúdo, em particular na <a href="https://www.worldscientific.com/doi/abs/10.1142/S0218213017600193">geração procedural de fases dos jogos</a>, mas também no <a href="https://www.springer.com/la/book/9783319427140>conteúdo visual</a>. Ao gerar conteúdo automaticamente é possível auxiliar os designers e artistas a criar conteúdo com maior variedade e em menos tempo.</p>

<h3>Nossa missão</h3>

<p align="justify">Nos anos de 1980, os gráficos para jogos NES eram baseados em blocos de imagens de 16×16 pixels e as telas eram formadas por matrizes desse blocos, porém como a capacidade de memória daquela época era muito baixa, a variedade era limitada, por exemplo, nas figuras abaixo podemos notar que a quantidade de blocos que compõem todo o jogo Super Mario Bros é inferior a 80 e como a tela inicial usa a repetição de muitos desses blocos para compor seu cenário.</p>

<img width="300" heigth="200" src=ImagensReadme/tilesmario.png> <img width="300" heigth="200" src=ImagensReadme/firstscreenmario.png>

<p align="justify"> A missão das GANs para esse projeto é conseguir reproduzir alguns blocos de 16×16 pixels suficientemente bons para construir um cenário, como pisos, árvores, água, pedras, etc. Mesmo se conseguirmos poucos blocos já será possível gerar uma fase, além disso o tamanho dos tiles permite que eles não sejam complexos.</p>

<h3>Mas pera, o que são redes neurais???</h3>
<p align="justify">Redes neurais são modelos computacionais inspirados no sistema nervoso central de animais, onde diversas camadas de neurônios se conectam entre si. O comportamento inteligente vem da capacidade de aprendizado da rede, que utiliza a interação entre seus neurônios, processando sinais e adaptando suas variáveis a fim de otimizar uma solução, que normalmente envolve reconhecer padrões.

Essa adaptação torna as redes neurais independentes em seu aprendizado, cabendo ao ser humano apenas orientar os dados de entrada e a saída esperada para o treinamento. Assim, uma única rede pode ser usada para compreender a fala humana ou reconhecer objetos visualmente sem quase nenhum apoio humano.</p>

<p>Link úteis para entender como uma rede neural aprende:</p>
<ul>
<li><a href="http://www.dsc.ufcg.edu.br/~joseana/IAPos_NA15_Complementar.pdf">Slides Prof.a Joseana Fechine UFCG</a>
</li>

<li><a href="http://redesneuraisartificiais.blogspot.com/2010/10/o-primeiro-modelo-de-um-neuronio-criado.html">Explicação modelo de neurônio</a></li>

<li><a href="https://www.youtube.com/watch?v=vbf4IzvXvuM&t=2s">Vídeo explicativo sobre redes neurais artificiais</a></li>

<li><a href="https://www.youtube.com/watch?v=DXnyuUZcAAI&t=2474s">Vídeo explicativo sobre redes neurais profundas</a></li>

<li><a href="http://www.deeplearningbook.org/">Deep Learning Book</a></li>
</ul>

<h3>E essas GANs aí, como funcionam?</h3>
<p align="justify">GANs são formadas por duas redes neurais profundas (Deep Learning), que através da teoria dos jogos, competem entre si, e no processo se tornam mais eficientes a cada iteração. Essa competição permite treinar modelos capazes de gerar conteúdo artificial aproximando a distribuição de dados reais.</p>

<p align="justify"> Podemos comparar uma das redes à uma policial que está sendo treinado para identificar dinheiro falso, checando cada imagem e avaliando se é real, chamamos essa rede de Discriminadora. A segunda rede pode ser comparada à um falsificador que está aprendendo a criar imagens de dinheiro falso, chamada também de Geradora.</p>

<p align="justify"> No início as duas redes são horríveis em suas funções, o Gerador(falsificador) não faz idéia de como criar dinheiro falso e o Discriminador(policial) não sabe distinguir qual imagem é verdadeira e qual é falsa. </p>

<img  width="400" heigth="300" src=ImagensReadme/1it.png> 

<p align="justify">Então, para ajudar o Discriminador é passada juntamente com as imagens falsas algumas verdadeiras e depois de avalidas é dado um gabarito com as respostas. Isso irá ajudar o Discriminador a procurar por detalhes que o possam ajudar a identificar melhor as imagens, por exemplo: notas verdadeiras possuem números.</p>

<img  width="400" heigth="300" src=ImagensReadme/3it.png> 

<p align="justify">O Gerador, ao perceber que suas criações estão sendo decifradas, tenta encontrar algum detalhes para enganar o Discriminador.</p>

<img  width="400" heigth="300" src=ImagensReadme/2it.png> 

<p align="justify">E essa disputa continua por muitas vezes até que ambos se tornem especialistas e, assim, podemos utilizar uma rede geradora treinada para realizar a função que quisermos, pode ser criar notas falsas ou para no caso desse projeto, criar imagens pixel-art para jogos.</p>

<h3>Implementações e banco de imagens utilizados</h3>

<p align="justify">Muitas implementações de GANs de código aberto existem na internet para serem testadas, então escolhi duas delas: a DCGAN feita pelo Taehoon Kim (<a href="https://github.com/carpedm20/DCGAN-tensorflow">github</a>), e a WGAN do Cameron Fabbri (<a href="https://github.com/cameronfabbri/Wasserstein-GAN-Tensorflow#wasserstein-gan-tensorflow">github</a>). Ambas implementadas na linguagem Python e utilizando a biblioteca Tensorflow para criação de redes neurais.</p>

<p align="justify">A base de imagens utilizada para alimentar as redes adversárias foi baixada do site <a href="http://www.vgmuseum.com/">VG Museum</a>, que conta com mais de 10.000 screenshots de centenas de jogos entre as décadas de 80 e 90 para o console Super Nintendo e Nintendo. As imagens possuem resolução de 224×256 pixels.</p>

<img src=ImagensReadme/snesgames.png> 

<h3>Rodando as GANs com a base de imagens</h3>

<p align="justify">No início, a saída dos dois geradores consistia em apenas ruídos mas a medida que as iterações iam sendo processadas, formas começaram a surgir.</p>

<p>DCGAN com 100 rodadas:</p>
<img src=ImagensReadme/dcgan-100epocas.png> 

<p>WGAN com 5 rodadas:</p>
<img src=ImagensReadme/wgan-5epocas.png> 

<p>Depois de um determinado número de iterações, blocos começaram a aparecer em ambas as redes. Tijolos, arbustos, água e padrões que poderiam ser usadas como o céu foram selecionados, e utilizando a ferramenta <a href="https://www.mapeditor.org/">Tiled Map Editor</a>, foram montados alguns cenários artificiais.</p>

<p>DCGAN 18000 rodadas:</p>
<img src=ImagensReadme/dcgan-resultados-finais.png> 

<p>Evolução da DCGAN:</p>
<img src=ImagensReadme/dcgan-resultados.png> 

<p>WGAN 8000 rodadas:</p>
<img src=ImagensReadme/WGAN-8000iterações.png> 

<p>Alguns tiles selecionados:</p>
<img src=tiles/tiles-usados.png>

<img src=tiles/tiles-variados.png> 

<p>Com o intuito de tornar a imagem mais parecida com a captura de tela de um jogo verdadeiro, foi adicionado alguns elementos característicos de jogos da plataforma, como personagens e pontuação.</p>

<h3>Imagens geradas</h3>

<img src=jogosCriados/todas.png>

<p align="justify">Com as imagens geradas resolvi aplicar um questionário simples misturando essas imagens com imagens reais de jogos de NES e Super Nintendo, depois perguntei às pessoas o que elas achavam de cada imagem, com a resposta podendo variar entre 1 a 4, sendo 1 = "provavelmente falso" e 4 = "provavelmente verdadeiro". Colocado no grupo da faculdade tive a resposta de 205 pessoas.</p>

<p align="justify">Primeiro perguntei o quão familiarizado com jogos de Super Nintendo a pessoa é, considerando 1="nunca joguei"e 4="jogo/joguei muito", as respostas foram: </p>

<table style="border: 1px solid black;">
  <tr border>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
  </tr>
  <tr>
    <td>3(1.5%)</td>
    <td>48(23.4%) </td>
    <td>72(35.1%) </td>
    <td>82(40%)</td>
  </tr>
</table>

<p align="justify">Considerando a ordem das imagens geradas a cima da esquerda para direita, com respostas variando entre 1="provavelmente falso"e 4="provavelmente verdadeiro", o resultado da classificação de cada imagem artificial foi: </p>

<table style="border: 1px solid black;">
  <tr>
    <th> </th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
  </tr>
  <tr>
    <td>Imagem 1</td>
    <td>23(11.2%) </td>
    <td>43(21.1%)  </td>
    <td>59(28.9%) </td>
    <td>79(38.7%) </td>
  </tr>
    <tr>
    <td>Imagem 2</td>
    <td>6(2.9%) </td>
    <td>13(6.3%)  </td>
    <td>40(19.5%) </td>
    <td>146(71.2%) </td>
  </tr>
    <tr>
    <td>Imagem 3</td>
    <td>15(7.3%) </td>
    <td>21(10.2%) </td>
    <td>51(24.9%) </td>
    <td>118(57.6%) </td>
  </tr>
    <tr>
    <td>Imagem 4</td>
    <td>9(4.4%)  </td>
    <td>26(12.7%) </td>
    <td>46(22.5%) </td>
    <td>123(60.3%) </td>
  </tr>
</table>

<h3> Como cada rede se saiu?</h3>

<p align="justify">Ambas as redes neurais utilizadas conseguiram gerar imagens que puderam ser aproveitadas. Em comparativo, pode-se dizer que a WGAN conseguiu melhores resultados mesmo com o tempo de aprendizado semelhante a DCGAN. Observando os gráficos dos cálculos dos erros das duas redes com o passar das iterações é possível notar o motivo: a WGAN conseguiu estabilizar o aprendizado das duas redes e assim conseguiram aprender de forma equilibrada e contínua até o fim das iterações, já o DCGAN sofreu com o chamado Mode Collapse, onde o discriminador acabou se tornando rapidamente mais eficiente que o Gerador, impedindo o seu desenvolvimento correto. (obs: clique no gráfico para ver ele maior)</p>

<img width="250" heigth="400" src=Graficos/dcgan.png> <img width="250" heigth="400" src=Graficos/wgan.png>


<h3>Conclusão: GANs funcionam! Mas calma lá.</h3>

<p align="justify">Considerando que as imagens falsas conseguiram enganar bem as pessoas acho que podemos dizer que as GANs são um método promissor de gerador de conteúdos, tanto a DCGAN quanto a WGAN conseguiram gerar imagens que puderam ser aproveitadas para a
construção de novos cenários para os jogos.

<p align="justify">As imagens geradas artificialmente praticamente possuem qualidade equivalente às produzidas por humanos, o que prova o potencial das GANs para a produção criativa de conteúdos ligados a jogos, apesar de serem difícieis de treinar e ainda produzem imagens limitadas, onde tive que eu mesmo garimpar os bons tiles.</p>

<p align="justify">Também devemos observar que não há garantias que as imagens são totalmente originais, pois em diversos exemplos, pode-se notar partes de texto, pontuação ou até partes conhecidas de jogos que foram simplesmente copiadas de imagens existentes no banco.</p>

<p align="justify">Contudo, essa tecnologia vem ganhando muitas pesquisas que já possuem uma enorme importância para as áreas de visão computacional de inteligência artificial. Sua capacidade de assimilar detalhes e produzir conteúdos é notável e a indústria de entretenimento tem apostado a fundo seu potencial. Considerando os avanços feitos em espaço tão curto de existência, já não é exagero esperar daqui alguns anos produções artísticas inteiras feitas digitalmente. Filmes, jogos e músicas gerados completamente por computadores já podem ser considerados uma provável realidade.</p>
