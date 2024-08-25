# Classificador de imagens

Este projeto é uma continuação do projeto [Criando um dataset e classificando com uma rede yolov5](https://github.com/JoaoPedroMoro/dio-formacao-machine-learning-specialist/tree/main/cria%C3%A7%C3%A3o%20de%20um%20dataset%20e%20classifica%C3%A7%C3%A3o%20com%20rede%20yolov5) realizando anteriormente como prática e aprendizado.

O objetivo deste projeto é aumentar a base de dados, que inicialmente é própria para conseguir treinar o classificador de maneira eficaz e correta, visto que no projeto dito anteriormente o objetivo era entender como funcionava a rede [YoloV5](https://github.com/ultralytics/yolov5) e devido a isso o resultado não foi dos melhores.

O projeto foi/é desenvolvido utilizando um notebook no [Google Colab](https://colab.research.google.com/) devido aos limites computacionais da minha máquina. E devido a isso, existem limites de utilização, já que estou usando a versão gratuita. Devido a isso, o projeto não terá um desenvolvimento contínuo, sendo realizado em várias partes e em vários dias diferentes.

De começo, existem duas classes para serem classificadas: 0 - dog e 1 - cat.

# Fase 1
Dando continuidade ao projeto realizado anterior, é necessário entender que o classificador teve um problema relacionado a classificação errada das duas classes. Uma taxa de confiabilidade alta retornava pouquíssimas classificações e uma taxa de confiança baixa retornava classificações incorretas. Diante disso, vou separar a fase 1 em duas partes: a classificação de mais imagens e vídeos para a classe gato e para a classe cachorro.

Para isso, foi criado os datasets test_gato e train_gato, localizados na pasta "Parte 1" dos dados.