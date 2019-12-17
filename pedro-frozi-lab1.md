# Laboratório 01- Algoritmo de Classificação de k Vizinhos Mais Próximos

## I. Avaliando a fronteira de decisão do Algoritmo

1. **Qual o efeito prático na forma/complexidade da pronteira de decisão, conforme se aumenta o numero de vizinhos?**  
   Conforme aumentamos a quantidade de vizinho que serão considerados para a classificação, menos complexa fica a superfície de decisão. Por outro lado, intuitivamente, parece que mais dados conhecidos começam a ter a predição incorreta. Por exemplo, para k=1 a fronteira fica super-ajustada para os dados conhecidos, com uma superfície de decisão extremamente complexa, enquanto para k=20 a fronteira fica mais "relaxada", parecendo errar a predição de dados conhecidos.

2. **Intuitivamente, para quais valores de vizinhos (baixos, intermédios, altos) você acha que o algoritmo provavelmente iria conseguir classificar corretamente novas instâncias? Por que?**  
   Para valores altos de K a fronteira de decisão ficará menos complexa, mais uniforme, parecendo ter uma predição mais assertiva para próximas instâncias que são desconhecidas em relação aos dados utilizados para o treinamento. Entretanto, K's muito altos tendem à extinguir a fronteira de decisão, transformado-a em um espaço uniforme (podemos dizer que todos os vizinhos do espaço de dados conhecido são próximos).

## II. Entendendo a importância da normalização dos atributos

3. **Por que você acha que os vizinhos mais próximos da instância não estão dispostos em um círculo ao seu redor (como seria de se esperar), e sim uma linha horizontal (isto é, para os lados) da instância?**  
   Como os dados não estão normalizados, a textura por ser uma grandeza maior acaba impactando de forma negativa na distância entre os pontos, fazendo com que a distância em relacão ao raio sempre acabe sendo mais relevante quanto à proximidade. Como o raio é o eixo X, os pontos que estão em uma mesma linha horizontal em relação à este eixo acabam sendo considerados "próximos".

**_Configure k_neighbors = 3 e responda:_**

> _knn_parametros.exibe_conjunto_de_teste = True. Não esqueça de desabilitar a opção para destacar os vizinhos mais próximos (isto é, configure o parâmetro destacar_vizinhos_mais_proximos para False);_

4. **Quantas instâncias novas de teste (marcadas como estrelas) foram incorretamente classificadas pelo algoritmo?**  
   3 instâncias rotuladas como "Com_Câncer" foram classificadas incorretamente como "Sem_Câncer". Aqui podemos notar uma grande proximidade horizontal com instâncias da base de treinamento rotuladas como "Sem_Câncer" que, devido à não normalização dos dados, explica o erro na classificação.

5. **Agora acione a opção para normalização de atributos. Para fazer isso, altere o valor do parâmetro correspondente: knn_parametros.normalizacao = True. Quantas instâncias novas/de teste foram incorretamente classificadas, agora? Por que você acha que isso aconteceu?**  
   1 instância rotulada como "Com_Câncer" e 1 instância rotulada como "Sem_Câncer" foram classificadas erroneamente. Em ambos os casos, as instâncias de teste estão muito próximas das instâncias de treinamento com classificação contrária. Podemos dizer que,1 instância rotulada como "Com_Câncer" foi classificada como "Sem_Câncer" por estar "rodeada" de instâncias "Sem_Câncer", e como estamos utilizando k=3 ela recebe a classificação destas instâncias (neste caso o método de votação não influenciaria).

## III. Otimizando o Algoritmo

6. **Quando normalização de atributos não é utilizada, a taxa de erros fica aceitável para algum valor de número de vizinhos? Por que?**  
   Para nenhum valor de K a taxa de erro se mostrou aceitável. A menor taxa de erros quando os atributos não estão normalizados ocorreu para k=1, temos uma taxa de erro de 33%, ou 75% de erro para instâncias classificadas como "Sem_Câncer" e rotuladas como "Com_Câncer". Neste caso, uma proximidade vertical, mesmo de pontos distantes horizontalmente, mostrará uma proximidade que não é válida para o algoritmo, classificando errado as instâncias de teste.

7. **Quando normalização de atributos é utilizada, qual padrão que você percebe entre a taxa de erros do algoritmo em instâncias novas, e o número de vizinhos utilizados? Em particular, como o erro se comporta para valores baixos, intermediários, e altos de vizinhos? Por que você acha que isso aconteceu? Dica: relembre a sua resposta para as questões (1) e (2).**
   A menor taxa de erro é apresentada para valores intermediários de K. Para valores baixos, a fronteira de decisão fica extremamente complexa e assertiva em relação à base de treinamento utilizada, contudo existe um erro maior na classificação das instâncias de teste utilizadas em relação aos erros encontrados com valores intermediários de K. Para K's muito altos, acontece o que foi previsto em (2): A fronteira de decisão simplesmente "some", e a classificação em diferentes classes se torna impossível (erro de 40%, ou 100% das instâncias "Com_Câncer").
