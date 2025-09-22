### 1. Ordenacao topologica

- Uma **ordenação topológica** é, em essência, uma **extensão linear** de uma **ordem parcial** imposta pelas arestas de um DAG. Em outras palavras, é uma forma de “linearizar” os vértices de um grafo dirigido acíclico, de modo que todas as precedências sejam respeitadas: se há uma aresta u->v, então u aparece **antes** de v na sequência.
- Por que fazemos ordenacao topologica?
	- **Modelagem de dependencias**.
	- **Deteccao de Ciclos**.
	- **Planejamento e Otimizacao**.
---
### 2. Propriedades
- É um **permutation** (reordenação) de todos os V vértices.
- Para cada aresta u->v, o indice de u na lista e **menor** que o de v.
- Num DAG, s**empre** existe pelo menos uma ordenação topológica. (Em contraste, grafos com ciclo não têm.)
Porém, **não é única**—quando dois vértices não têm relação de precedência direta (nem indireta), você pode colocá-los em qualquer ordem relativa.
---
### 3. Dois algoritmos classicos

#### 3.1 Kahn (grau de entrada + fila)
- **Intuicao**:
	- Vertices sem nenhum pre-requisito (grau de entrada 0) podem vir primeiro.
	- Retire-os, "de baixa" nas arestas que saem deles, e revele novos vertices de grau 0.
- **Passos**:
	- 1. Calcule o grau de entrada `indeg[v]` para cada vertice v.
	- 2. Enfileire todos os vertices com `indeg[v] == 0`.
	- 3. Enquanto a fila nao estiver vazia:
		- 3.1 Remova (`u = dequeue`) e adicione u ao resultado.
		- 3.2 Para cada aresta u->v:
			- Decremente `indeg[v]` em 1.
			- Se `indeg[v]` chegar a 0, enfileire v.
	- 4. Se voce processou todos os vertices (tamanho do resultado = V), tem uma ordenacao valida; caso contrario, havia ciclo.
- **Complexidade:**
	- Tempo: `O(V+E)`
	- Espaco: `O(V)` (vetor de graus, fila e vetor de saida).
- **Implementacao**:
```
int* topo_kahn(Grafo* g) {
    int V = g->V;
    int* indeg = calloc(V, sizeof(int));
    int* fila  = malloc(V * sizeof(int));
    int front = 0, back = 0;
    int* ordem = malloc(V * sizeof(int));
    int idx = 0;

    // calcula grau de entrada
    for (int u = 0; u < V; u++) {
        for (No* p = g->adj[u]; p; p = p->prox) {
            indeg[p->v]++;
        }
    }
    // enfileira vértices de indeg == 0
    for (int u = 0; u < V; u++) {
        if (indeg[u] == 0) {
            fila[back++] = u;
        }
    }
    // processa
    while (front < back) {
        int u = fila[front++];
        ordem[idx++] = u;
        for (No* p = g->adj[u]; p; p = p->prox) {
            int v = p->v;
            if (--indeg[v] == 0) {
                fila[back++] = v;
            }
        }
    }

    free(indeg);
    free(fila);

    // se não processou todos, há ciclo
    if (idx != V) {
        free(ordem);
        return NULL;
    }
    return ordem;
}
```

#### 3.2 DFS pos-visita (pilha)
- **Intuicao**:
	- Faca uma DFS normal, mas empilhe cada vertice apos explorar todos os seus vizinhos (isto e, momento de "backtrack").
	- Quando a DFS terminar, voce tera uma pilha onde o topo e o "ultimo" vertice a ser finalizado(isto e, aquele que nao depende de mais ninguem). E so retirar todos da pilha em sequencia.
- **Passos**:
	- 1. Marque todos os vertices como nao visitados.
	- 2. Para cada vertice u nao visitado, chame `dfs(u)`, recursivamente.
	- 3. Apos todas as chamadas, pop da pilha em ordem produz a ordenacao topologica.
- **Complexidade**:
	- Tempo: `O(V+E)`
	- Espaco: `O(V)`
- **Implementacao**
```
void dfs_post(Grafo* g, int u, int* vis, int* stack, int* top) {
    vis[u] = 1;
    for (No* p = g->adj[u]; p; p = p->prox) {
        if (!vis[p->v]) {
            dfs_post(g, p->v, vis, stack, top);
        }
    }
    // pós-visita: empilha u
    stack[(*top)++] = u;
}
```
```
// Retorna um array de tamanho V com ordenação topológica, ou NULL se detectar ciclo (opcional: aqui assume DAG).
int* topo_dfs(Grafo* g) {
    int V = g->V;
    int* vis   = calloc(V, sizeof(int));
    int* stack = malloc(V * sizeof(int));
    int  top   = 0;

    // roda DFS em cada componente
    for (int u = 0; u < V; u++) {
        if (!vis[u]) {
            dfs_post(g, u, vis, stack, &top);
        }
    }
    free(vis);

    // stack[0..top-1] contém pós-visita; inverter para ordem topo
    int* ordem = malloc(V * sizeof(int));
    for (int i = 0; i < V; i++) {
        ordem[i] = stack[V - 1 - i];
    }
    free(stack);
    return ordem;
}
```
---
### 4. Consideracoes Praticas

- **Escolha do algoritmo**:
	- **Kahn**: mais intuitivo quando voce ja tem ou precisa do grau de entrada; facil detectar ciclo (fila esvazia antes de processar todos).
	- **DFS**: integra bem quando voce ja faz outras DFS, mas cuidado com profundidade de recursao em grafos muito grandes.
- **Não-única**
	- Em muitos casos há várias ordenações válidas; dependendo da ordem de inserção na fila ou da ordem em que você visita vizinhos no DFS, o resultado varia.
- **Validação de DAG**
	- Qualquer tentativa que retorne **menos** de V vértices (no caso de Kahn) ou encontre uma chamada recursiva a um nó “cinza” (no caso do DFS com marcação tríplice) indica que há ciclo e, portanto, **não** existe ordenação topológica.
---
### 5. Resumo Final
##### 1. **O que é:** uma sequência linear dos vértices de um DAG respeitando todas as arestas.
##### 2. **Por que:** para ordenar tarefas com dependências, detectar ciclos, planejar execuções.
##### 3. **Como**:
- **Kahn**: removendo vértices de grau de entrada zero em ordem.
- **DFS-pós-visita**: empilhando ao sair da recursão.
##### 4. **Complexidade**: `O(V+E)` em ambos os casos.
##### 5. **Resultado**: não-único, mas garante que todo u→v apareça com u antes de v.


