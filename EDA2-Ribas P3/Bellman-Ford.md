
### 1. Bellman-Ford

### 1. Implementacao

#### 1.1 Funcao
```
bool GRAPHcptBF(Graph G, int inicial, int *pa, int *dist){
```
- **Objetivo**: calcular caminhos mínimos num grafo possivelmente com arestas de peso negativo, detectando ciclos negativos.
- `G` é o grafo, `inicial` é o vértice‑fonte, `pa[v]` vai guardar o predecessor de `v` e `dist[v]` a distância mínima até `v`.
#### 1.2 Inicialização dos vetores:
```
bool onqueue[1000];
for(int v = 0; v < G->V; v++){
    pa[v] = -1;
    dist[v] = INT_MAX;
    onqueue[v] = false;
}

pa[inicial]   = inicial;
dist[inicial] = 0;

```
- 1. **`pa[v] = -1`**: nenhum predecessor definido ainda.
- 2. **`dist[v] = INT_MAX`**: distância “infinita” no começo.
- 3. **`onqueue[v] = false`**: flags que dizem se `v` já está na fila de espera para processamento.
- 4. Para o vértice‑fonte `inicial`, dizemos que `pa[inicial] = inicial` (convencional) e `dist[inicial] = 0`.

#### 1.3 Preparação da fila e sentinel
```
Queueinit(G->E);
Queueput(inicial);
onqueue[inicial] = true;

// Sentinela para contar “rodadas” completas
Queueput(G->V);
int K = 0;
```
- 1. **`Queueinit(G->E)`**: inicializa uma fila capaz de comportar até `G->E`+ elementos.
- 2. **`Queueput(inicial)`**: enfileira o vértice‑fonte para começar a relaxar suas arestas.
- 3. **`onqueue[inicial] = true`**: marca que `inicial` já está na fila (evita duplicatas).
- 4. **`Queueput(G->V)`**: insere um “marcador” com valor igual a `G->V` (fora do range `[0..G->V-1]`).
	- Serve para **contar quantas vezes** já processamos todos os vértices ativos (cada vez que esse marcador reaparece, incrementamos `K`).
	- Usuário típico: após `K > V−1`, sabemos que há ciclo de peso negativo e podemos abortar.

#### 1.4 Loop principal
```
while (1) {
    int v = Queueget();
```
- **`Queueget()`**: retira o próximo elemento da fila (FIFO).
- O loop só termina por `return` interno (não mostrado), por `break` ao detectar ciclo negativo, ou por fila vazia.

#### 1.5 Tratamento de vértice vs. sentinela:
```
    if (v < G->V) {
        // É um vértice real: relaxe suas arestas
        for (link a = G->adj[v]; a != NULL; a = a->next) {
            if (dist[v] + a->c < dist[a->v]) {
                dist[a->v] = dist[v] + a->c;
                pa[a->v]   = v;
                if (!onqueue[a->v]) {
                    Queueput(a->v);
                    onqueue[a->v] = true;
                }
            }
        }
    }
    // else seria o caso v == G->V (sentinela)
    // aí faríamos: K++; 
    //          if (K > G->V - 1) return false;   // ciclo negativo detectado
    //          Queueput(G->V);                  // re-enfileira sentinela
}
```
- 1. Quando `v < G->V` (vértice real)
	- **Percorre lista de adjacência** de `v`.
	- **Teste de relaxamento**: se `dist[v] + peso < dist[w]`, então encontramos caminho mais curto até `w = a->v`.
	- **Atualiza**
		- `dist[w] = dist[v] + a->c`
		- `pa[w] = v`
	- **Fila**: se `w` ainda não estava `onqueue`, enfileira `w` para processar suas arestas mais tarde e marca `onqueue[w] = true`.
- 2. Quando `v == G->V` (sentinela):
	- **Significado**: chegamos ao final de uma “rodada” completa de relaxamentos.
	- **Incrementar contador**: `K++`.
	- **Teste de término**: se `K > G->V - 1`, executamos `return false;` indicando que há ciclo de peso negativo e não existe solução de caminhos mínimos.
	- **Recolocar sentinela**: para a próxima rodada, faz `Queueput(G->V);` novamente, garantindo que continuemos contando.
#### 1.6 Término e retorno
- Se a fila esvaziar **sem** que `K > V−1`, significa que relaxamos todas as arestas suficientes vezes e não há ciclo negativo.
- Então retornamos `true`, indicando sucesso e com `dist[]` e `pa[]` preenchidos com os menores caminhos.
---
### 2. Implementacao completa
```
bool GRAPHcptBF(Graph G, int inicial, int *pa, int *dist){

	bool onqueue[1000];
	for(int v = 0; v < G->V; v++){
		pa[v] = -1;
		dist[v] = INT_MAX;
		onqueue[v] = false;
	}

	pa[inicial] = inicial;
	dist[inicial] = 0;
	Queueinit(G->E);
	Queueput(inicial);
	onqueue[inicial] = true;

	Queueput(G->V);
	int K = 0;

	while(1){
		int v = Queueget();
		if(v < G->V){
			for(link a = G->adj[v]; a != NULL; a = a->next){
				if(dist[v] + a->c < dist[a->v]){
					dist[a->v] = dist[v] + a->c;
					pa[a->v] = v;
					if(onqueue[a->v] == false){
						Queueput(a->v);
						onqueue[a->v] = true;
					}
					
				
				}
			}
		}
	
	
	}



}
```

---
### 3. Complexidade

#### Tempo
- 1. **Pior caso**
    - Cada aresta pode ser relaxada até **V–1** vezes (igual ao Bellman–Ford clássico).
    - Para cada relaxamento bem‑sucedido, você enfileira o vértice e mais tarde processa suas adjacências.
    - Portanto, no pior caso, você faz até **O(V·E)** operações de relaxamento.
    - Além disso, cada operação de fila (enqueue/dequeue) é O(1), mas pode ocorrer uma vez para cada relaxamento bem‑sucedido.
    - **Resultado**: _O(V·E)_ no pior caso e detecção de ciclo negativo logo após V rodas.
- 2. **Caso médio (prático)**
	- Em grafos “bem comportados” (sem pesos muito negativos em sequência), muitas arestas não precisam ser re-relaxadas repetidamente.
	- Em benchmarks, costuma dar próximo de _O(E)_ ou _O(k·E)_ com k muito menor que V, às vezes k≈log V.
	- Porém **não há garantia teórica** forte de sub‑quadrático.
- 3. **Comparação com Bellman–Ford clássico**
    - Bellman–Ford puro sempre executa exatamente V–1 iterações sobre **todas** as arestas: O(V·E).
    - SPFA faz “rodadas” dinâmicas apenas enquanto houver melhora, e ignora vértices cujas distâncias não mudaram.
    - **Na prática** SPFA costuma superar Bellman–Ford em grafos esparsos e sem muitos ciclos negativos.

#### Espaco

- **Vetor de distâncias** `dist[V]`: O(V)
- **Vetor de predecessores** `pa[V]`: O(V)
- **Flag de fila** `onqueue[V]`: O(V)
- **Fila** com até O(E) elementos no pior caso: O(E)
Total: **O(V + E)** em memória.

#### Resumo
- **Pior caso:** O(V·E) tempo
- **Caso prático:** geralmente entre O(E) e O(V·E), muitas vezes perto de O(E)
- **Espaço:** O(V + E)