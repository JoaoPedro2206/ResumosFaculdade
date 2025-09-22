### 1. Definicao

##### 1.1 Grafos
- É um modelo matemático que representa relações entre objeto
- Utilizados na definição e/ou resolucao de problemas de diversas areas
##### 1.2 Em computacao
- E uma forma de solucionar problemas computaveis.
- buscam o desenvolvimento de algoritmos mais eficiente.
##### 1.3 Exemplos
- Qual a melhor rota da minha casa ate um restaurante?
- Duas pessoas tem algum amigo em comum?
##### 1.4 Representacao
- E definido como um conjunto de vertices e um conjunto de arestas que conectam qualquer par de vertices.
- `G = (V, A)`
	- V e o conjunto de vertices (nao vazio).
	- A e o conjunto de arestas.
##### 1.5 Vertice
- E cada uma das entidades representadas em um grafo.
- Depende da natureza do problema. Podem ser pessoas, casas, etc.
- Dois vertices sao **adjacentes** se existir uma aresta ligando eles.
##### 1.6 Aresta
- Tambem chamada de **arco**.
- Esta associada a dois vertices (v1, v2).
- Faz a ligacao entre eles, ou seja, diz qual a relacao entre eles.
- 
---
### 2. Propriedades

##### 2.1 Direcao das Arestas
- **Grafos direcionados** ou **Digrafos**:
	- Existe uma orientacao quanto ao sentido da aresta.
	- Se uma aresta liga *A* e *B*, podemos ir de *A* para *B*, mas nao o contrario.
- **Grafos Nao Direcionados**:
	- Nao existe nenhuma orientacao quanto ao sentido da aresta. Podemos ir de *A* para *B* ou de *B* para *A*.

##### 2.2 Grau de um Vertice
- E o numero de arestas que chegam ou partem dele.
- No caso dos **grafos direcionados**, temos:
	- *Grau de entrada*: Arestas que chegam ao vertice.
	- *Grau de saida*: Arestas que partem do vertice
![](G1.png)

##### 2.3 Laco
- Uma aresta e chamada de *Laco* se seu vertice de partida e o mesmo que o de chegada, ou seja, a aresta conecta o vertice com ele mesmo (v, v).
 ![](G2.png)
##### 2.4 Caminho
- E uma sequencia de vertices de modo que existe sempre uma aresta ligando o vertice anterior com o seguinte.
- **Caminho Simples**:
	- Nenhum dos vertives no caminho se repete.
- **Comprimento do Caminho**:
	- E o numero de arestas que o caminho usa.
![](G3.png)

##### 2.5 Ciclo
- E um caminho que comeca e termina no mesmo vertice.
- Um **Laco** e um ciclo de comprimento 1.
- **Grafo Aciclico**:
	- Nao contem *ciclos simples* (onde cada vertice aparece apenas uma vez cada).
![](G4.png)
##### 2.6 Arestas Multiplas
- Tambem chamado **Multigrafo**.
- E um grafo que permite mais de uma aresta conectando o mesmo par de vertices.
- Nesse caso, as arestas sao ditas *paralelas*.
![](G5.png)
---
### 3. Tipos de Grafos

##### 3.1 Grafo Trivial
- E um grafo com um unico vertice e sem arestas.
![](G6.png)

##### 3.2 Grafo Simples
- E um grafo nao direcionado, sem lacos e sem arestas paralelas.
![](G7.png)

##### 3.3 Grafo Completo
- E um grafo simples onde cada vertice se conecta a todos os outros vertices.
![](G9.png)

##### 3.4 Grafo Regular
- E um grafo onde todos os vertices possuem o mesmo grau.
- E um tipo de grafo completo.
- O exemplo do grafo com grau 3 e um grafo regular mas nao e um grafo completo, pois os seus vertices nao se conectar com todos os outros vertices.
![](G10.png)
##### 3.5 SubGrafo
- Um grafo `Gs(Vs, As)` e chamado de *subgrafo* de `G(V, S)` se :
	- *Vs* esta contido em *V*.
	- *As* esta contido em *A*.
![](G11.png)

##### 3.6 Grafo Bipartido
- E um grafo cujos vertices podem ser divididos em dois conjunto.
- Nesse caso, as arestas ligam os vertices que estao em conjunto diferentes, nunca ligando vertices do mesmo conjunto.
![](G12.png)

##### 3.7 Grafo Conexo
- Existe um caminho partindo qualquer vertice ate qualquer outro vertice do grafo.
![](G13.png)

##### 3.8 Grafo Desconexo
- Nao existe um caminho ligando dois vertices selecionados.
![](G14.png)

##### 3.9 Grafos Isomorfos 
- Dois grafos, `G1(V1, A1)` e `G2(V2, A2)`, sao ditos **isomorfos** se existe uma funcao que faca o mapeamento de vertices e arestas de modo que os dois grafos se tornem coincidentes.
![](G15.png)

##### 3.10 Grafos Ponderados
- E o grafo que possui **pesos** associados a cada uma de suas arestas.
![](G16.png)

##### 3.11 Grafos Hamiltonianos
- E o grafo que possui um caminho que visita cada *vertice* apenas uma vez.
	- Sua deteccao e uma tarefa extremamente ardua.
- Um **ciclo hamiltoniano** e o ciclo que visita cada *vertice* apenas uma vez.
![](G17.png)

##### 3.12 Grafos Eulerianos
- E o grafo que possui um *ciclo* que visita cada *aresta* apenas uma vez.
![](G18.png)

##### 3.13 Grafos Semi-Eulerianos
- E o grafo que possui um *caminho* que visita cada aresta apenas uma vez.
![](G19.png)
---
