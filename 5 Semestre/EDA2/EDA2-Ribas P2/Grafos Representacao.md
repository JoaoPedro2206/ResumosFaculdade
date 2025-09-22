### 1. Representacao de Grafos
- Duas abordagens sao muito utilizadas:
	- **Matriz de Adjacencia**
	- **Lista de Adjacencia**a
- Qual e a representacao que deve ser utilizada?
	- Depende da aplicacao!
	- Grafos muito esparsos melhor usar lista de adjacencia.
	- Grafos muito conectados melhor usar matriz de adjacencia.
---
### 2. Matriz de Adjacencia
- Uma matriz N x N e utilizada para armazenar o grafo, onde N e o numero de vertices.
	- Alto custo computacional, `O(N^2)`.
- Uma aresta e representada por uma *marca* na posicao (i, j) da matriz.
	- Aresta liga o vertice i ao j.
![](G20.png)
---
### 3. Lista de Adjacencia

![](G21.png)
 - Cada vertice guarda a informacao de com quem esta se ligando e um ponteiro.
 - Para cada aresta criada sera criado um novo ponteiro e um valor indicando a proximo vertice.
 - A partir de um certo numero de conexoes nao vale a pena, pois torna computacionalmente complicado.
![](G22.png)
---
### 4. Lista X Matriz

#### 4.1 Lista de Adjacencia
##### 4.1.1 Vantagens
- **Economia de memoria em grafos esparsos**
	- Usa espaco `O(V+E)`: Voce aloca um vetor de V listas e, para cada aresta, armazena apenas um no (ou dois, em grafo nao-direcionado).
- **Iteracao eficiente sobre vizinho**
	- Para percorrer vizinhos de um vertice u, basta varrer sua lista - custo `O(deg(u))`.
- **Insercao de aresta barata**
	- Insere no inicio (ou fim) da lista em `O(1)` (alocacao dinamica incluida).
##### 4.1.2 Desvantagens
- **Acesso aleatorio mais lento**
	- Testar se existe aresta(u,v) pode custar `O(deg(u))`, pois potencialmente exige varrer toda a lista.
- **Mais complexo para implementacao em C**
	- Precisa gerenciar alocacao e estruturas de no.
- **Overhead de ponteiros**
	- Cada No carrega um ponteiro extra (next), consumindo memoria adicional.
##### 4.1.3 Cenarios Ideais
- **Grafos esparsos**: (E < V^2), por exemplo: redes de estradas, arvores de grande porte, grafos de redes sociais pouco conectados.
- **Algoritmos BFS/DFS** e outras travessias que exploram principalmente vizinhanca imediata.

#### 4.2 Matriz de Adjacencia
##### 4.2.1 Vantagens
- **Teste de existencia de aresta em `O(1)`**
	- Basta checar `mat[u][v]`
- **Implementacao simples**
	- Uma `int mat[v][v]`)(ou alocacao dinamica unica com malloc) e dois loops aninhados sao suficientes.
- **Boas para grafos densos**
	- Quando `E = V^2`, o espaco `O(V^2)` ja esta dominando mesmo que nao ocupe todo.
##### 4.2.2 Desvantagens
- **Alto consumo de memoria em grafos esparsos**
	- Usa sempre `O(V^2)`, mesmo se tiver poucas arestas. Em C, para V = 10 000, sao 100 milhoes de celulas - *Impraticavel*.
- **Ineficiencia em listagem de vizinhos**
	- Para achar todos os vizinhos de u, e preciso varrer V entradas, ou seja, O(V) por vertice.
- **Dificuldade de redimensionamento**
	- Se quiser crescer o grafo, precisa realocar a matriz inteira.
##### 4.2.3 Cenarios Ideais
- **Grafos densos** `(E = V^2)`, por exemplo: Grafos de fluxo de custo, simulacoes onde quase todo vertice esta conectado a quase todos.
- **Algoritmos de matriz** como Floyd-Warshall(todos-pares), onde o acesso O(1) e crucial e percorre toda a matriz varias vezes.
#### 4.3 Complexidade de Operacoes

| **Operacao**                | **Lista de Adjacencia** | **Matriz de Adjacencia** |
| --------------------------- | ----------------------- | ------------------------ |
| Inserir Aresta              | `O(1)`                  | `O(1)`                   |
| Remover Aresta              | `O(deg(u))`             | `O(1)`                   |
| Testar existencia de aresta | `O(deg(u))`             | `O(1)`                   |
| Iterar sobre vizinhos de u  | `O(deg(u))`             | `O(V)`                   |
| Espaco                      | `O(V+E)`                | `O(V^2)`                 |
- **deg(u)**: Numero de arestas saindo de (ou chegando em) u.
- **O(deg(u))**: custo assintotico exatamente proporcional a esse numero de aresta.
#### 4.4 Resumo
- **Lista de adjacencia**: Grafo grande e esparso, foco em travessias (BFS/DFS), economia de memoria.
- **Matriz de adjacencia**: Grafo moderadamente pequeno ou denso, necessidade de teste rapido de existencia, algoritmos de caminho todos-a-todos.
---