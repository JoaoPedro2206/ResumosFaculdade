- A primeira implementação do algoritmo de Dijkstra começa cada iteração examinando os vértices imaturos, um por um, à procura de algum que minimize `dist[]`. Para acelerar esse processo, a implementação que examinaremos a seguir mantém os vértices imaturos em uma fila priorizada "de mínimo" (= _min priority queue_). (Seria suficiente manter na fila priorizada os vértices imaturos que pertencem a T, mas é mais simples colocar na fila todos os vértices imaturos, mesmo os que estão fora de T.)
### 1. Implementacao:

#### 1.1 Funcao
```
void GRAPHcptD2(Graph G, int s, int *pa, int *dist){
```
- **Objetivo**: calcular distâncias mínimas de um vértice‑fonte `s` até todos os demais vértices de `G`, armazenando em `dist[]`, e manter o predecessor de cada vértice em `pa[]` para reconstruir caminhos.
#### 1.2 Declarações e Inicialização Básica:
```
   bool mature[1000];
   for (int v = 0; v < G->V; v++)
      pa[v] = -1;
      mature[v] = false;
      dist[v] = INT_MAX;
   
   pa[s] = s;
   dist[s] = 0;
```

- 1. **`mature[1000]`** – marca quais vértices já tiveram sua distância definitiva.
- 2. **Loop de inicialização**
    - `pa[v] = -1` → nenhum predecessor definido.
    - `mature[v] = false` → nenhum vértice foi processado.
    - `dist[v] = INT_MAX` → distância “infinita” (desconhecida) inicialmente.    
- 3. **Configuração do vértice‑fonte `s`**
    - `pa[s] = s` → convenção de predecessor.
    - `dist[s] = 0` → distância de `s` até si mesmo é zero.

#### 1.3 Inicialização da Fila de Prioridade:
```
   PQinit(G->V);
   for (int v = 0; v < G->V; v++)
      PQinsert(v, dist);
```
- **`PQinit(n)`** – prepara uma estrutura de dados (tipicamente um heap mínimo) capaz de armazenar até `n` elementos, indexados por vértice.
- **`PQinsert(v, dist)`** – insere cada vértice `v` na fila, com chave inicial `dist[v]`. No início, só `s` tem chave 0; todos os outros têm `INT_MAX`.
#### 1.4 Loop Principal: Extração e Relaxamento:
```
   while (!PQempty()) {
      int y = PQdelmin(dist);
      if (dist[y] == INT_MAX) break;
```
- 1. **`!PQempty()`** – continua enquanto houver vértices na fila.
- 2. **`y = PQdelmin(dist)`** – remove e retorna o vértice de menor chave (menor `dist[]`) da fila de prioridade.
- 3. **Condição de parada**
	- Se o menor valor ainda for `INT_MAX`, então todos os vértices restantes são inacessíveis a partir de `s`. O loop encerra.

#### 1.5 Relaxamento de Arestas de Saída de `y`:
```
      for (link a = G->adj[y]; a != NULL; a = a->next) {
         if (mature[a->v]) {
	         continue;
         } 

         if (dist[y] + a->c < dist[a->v]) {
            dist[a->v] = dist[y] + a->c;
            PQdec(a->v, dist);
            pa[a->v] = y;
         }
      }

```

- **Para cada aresta `a` de `y` para `a->v com custo `a->c`:**
- 1. **Ignorar vértices já maduros** (`if (mature[a->v]) continue;`).
- 2. **Teste de relaxamento:**
	- Se `dist[y] + a->c < dist[a->v]`, encontramos um caminho mais curto até `a->v` passando por `y`.
	- **Atualização**:
		- `dist[a->v] = dist[y] + a->c`
		- `pa[a->v] = y`
- 3. `PQdec(a->v, dist)`
	- Informa à fila de prioridade que a chave (distância) do vértice `a->v` diminuiu, ajustando sua posição no heap para manter a propriedade de min‑heap.

#### 1.6 Marcar `y` como “Maduro” e Repetir:
```
      mature[y] = true;
   }
```
- Depois de processar todas as arestas de `y`, sua distância é definitivamente a menor possível; marcamos `mature[y] = true` e voltamos ao `while` para extrair o próximo vértice de menor distância.

#### 1.7 Liberação de Recursos:
```
   PQfree();
}
```
- **`PQfree()`** – limpa a memória ou estruturas internas usadas pela fila de prioridade.


### 2. Implementacao Completa:
```
void GRAPHcptD2(Graph G, int s, int *pa, int *dist){

	bool mature[1000];
	for(int v = 0; v < G->V; v++){
		pa[v] = -1;
		mature[v] = false;
		dist[v] = INT_MAX;
	}

	pa[s] = s;
	dist[s] = 0;

	PQinit(G->V);
	for(int v = 0; v < G->V; v++){
		PQinsert(v, dist);
	}

	while(!PQempty()){
		int y = PQdelmin(dist);
		if(dist[y] == INT_MAX){
			break;
		}
		for(link a = G->adj[y]; a != NULL; a = a->next){
			if(mature[a->v]){
				continue;
			}
			if(dist[y] + a->c < dist[a->v]){
				dist[a->v] = dist[y] + a->c;
				PQdec(a->v, dist);
				pa[a->v] = y;
			}
		}
		mature[y] = true;
	}
	PQfree();
}

```
### 3. Visão Geral da Estrutura de Dados de Prioridade
- A fila de prioridade (`PQ*`) fornece três operações essenciais para Dijkstra eficiente:
	- 1. **Insert**: insere todos os vértices no início (custo `O(n)` para heapify ou `O(nlog⁡n)` em inserções separadas).
	- 2. **Delete‑Min**: extrai em `O(logn)` o vértice de menor distância.
	- 3. **Decrease‑Key**: atualiza a posição de um vértice cujo custo diminuiu, em `O(logn)`.
Isso reduz a complexidade total do algoritmo para `O((V + E) log V)`, muito melhor que `O(V^2)` da versão sem heap, especialmente para grafos esparsos.

### 4. Execucacao Passo a Passo

![](D10.png)
![](D11.png)

- Iteracao 1
![](D12.png)
- Iteracao 2:
![](D13.png)
- Iteracao 3:
![](D17.png)
- Iteracao 4:
![](D16.png)
- Iteracao 5: 
![](D15.png)
- Iteracao 6
![](D14.png)