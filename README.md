# Classificador de imagens

Este projeto é uma continuação do projeto [Criando um dataset e classificando com uma rede yolov5](https://github.com/JoaoPedroMoro/dio-formacao-machine-learning-specialist/tree/main/cria%C3%A7%C3%A3o%20de%20um%20dataset%20e%20classifica%C3%A7%C3%A3o%20com%20rede%20yolov5) realizando anteriormente como prática e aprendizado.

O objetivo deste projeto é aumentar a base de dados, que inicialmente é própria para conseguir treinar o classificador de maneira eficaz e correta, visto que no projeto dito anteriormente o objetivo era entender como funcionava a rede [YoloV5](https://github.com/ultralytics/yolov5) e devido a isso o resultado não foi dos melhores.

O projeto foi/é desenvolvido utilizando um notebook no [Google Colab](https://colab.research.google.com/) devido aos limites computacionais da minha máquina. E devido a isso, existem limites de utilização, já que estou usando a versão gratuita. Devido a isso, o projeto não terá um desenvolvimento contínuo, sendo realizado em várias partes e em vários dias diferentes.

De começo, existem duas classes para serem classificadas: 0 - dog e 1 - cat.

# Fase 1
## Parte 1
Dando continuidade ao projeto realizado anterior, é necessário entender que o classificador teve um problema relacionado a classificação errada das duas classes. Uma taxa de confiabilidade alta retornava pouquíssimas classificações e uma taxa de confiança baixa retornava classificações incorretas. Diante disso, vou separar a fase 1 em duas partes: a classificação de mais imagens e vídeos para a classe gato e para a classe cachorro.

Para isso, foi criado os datasets test_gato e train_gato, localizados na pasta "Parte 1" dos dados.

Foram rodados 6 treinamentos (experimentos) iniciais, onde eram conjuntos de 3 épocas (número de iterações de treinamento) para 2 batch sizes (número de amostras processadas em uma iteração) diferentes, 16 e 32, com 50 épocas, 100 épocas e 200 épocas. O limiar de confiança para a classificação de cada um desses treinamentos foi 0.4. O comando para tal classificação é: 

```!python detect.py --weights /content/yolov5/runs/train/exp/weights/best.pt --img 640 --conf 0.40 --source /content/data_test/ --data /content/yolov5/data/custom_data.yaml --save-txt --save-conf```

onde o parâmetros --weights indica qual treinamento utilizar, --img a proporção das imagens, --conf o nível de confiança, --data qual arquivo .yaml de dados usar, --save-txt e --save-conf para salvar as projeções .txt da classificação das imagens e o limiar de confiança.

Estes experimentos podem ser encontrados no diretório yolov5/runs/detect e vão ter de exp até exp5, indicando qual classificação foi. O treinamento exp resultou na detecção exp, o exp2 na exp2 e por ai vai.

Para visualização e análise dos resultados dessas 6 runs, experimentos, onde a run 1 é o exp, a run 2 é o exp2, até a run 6 que é o exp6, foi observado todas as saídas e construído uma tabela. As classificações corretas são aquelas em que a área demarcada do gato é aceitável, as classificações incorretas são aquelas em que ou não encontrou gato, ou o número de gatos encontrados não é correto, podendo ter o algoritmo classificado mais ou menos gatos do que há na imagem, e as classificações desproporcionais são aquelas em que é correto o número de gatos classificados mas a área demarcada de classificação está incorreta, muitas vezes classificando apenas o rosto e ignorando o corpo do gato.

|Run|Corretas|Incorretas|Desproporcionais|
|---|---|---|---|
| 1 | 27 | 20 | 14 |
| 2 | 26 | 28 | 7 |
| 3 | 35 | 6 | 20 |
| 4 | 32 | 12 | 17 |
| 5 | 29 | 16 | 16 |
| 6 | 30 | 16 | 15 |

Quase em todas as comparações de 16 com 32 de batch size, a de 16 teve um menor número de classificações incorretas e um maior número de classificações desproporcionais, o que indica que ela está classificando mais as imagens porém com um quadrado maior do que o que deveria.

A propósito de estudos, vou realizar para 8, 16 e 32 de batch size com 400 épocas. Respectivamente serão exp7, exp8 e exp9.

|Run|Corretas|Incorretas|Desproporcionais|
|---|---|---|---|
| 7 | 44 | 8 | 9 |
| 8 | 40 | 11 | 10 |
| 9 | 35 | 13 | 13 |

Conforme podemos visualizar, o batch size 8 com 400 épocas teve o melhor desempenho, porém é válido ressaltar que a run 8 obteve boas classificações em fotos com mais de 1 gato, que não tinham sido tão boas em nenhuma outra run.

Com as imagens classificadas nas 9 runs feitas, irei realizar uma separação de imagens, na qual as que foram melhor classificadas vão ir para o treinamento e as que não foram tão bem classificadas ou não foram classificadas permanecerão no teste. A descrição melhor dessa escolha estará na parte 2.

# Referências
Nesta seção estão os links que foram utilizados neste projeto em algum momento, seja tanto para o desenvolvimento do código quanto a descrição deste relatório.
- https://www.deeplearningbook.com.br/o-efeito-do-batch-size-no-treinamento-de-redes-neurais-artificiais/
- https://machinelearningmastery.com/difference-between-a-batch-and-an-epoch/