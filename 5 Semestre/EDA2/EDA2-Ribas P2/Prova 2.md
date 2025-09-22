## 1 - 
- Em um grafo não-dirigido, um ciclo é um caminho que começa e termina no mesmo vértice, onde todos os outros vértices visitados ao longo do caminho são distintos entre si e diferentes do vértice inicial/final (exceto no ponto de retorno).
- Uma única aresta, por si só, conecta dois vértices (ou um único vértice a si mesmo, no caso de um laço). Embora um laço (uma aresta que conecta um vértice a si mesmo) possa ser considerado um ciclo de comprimento 1 em algumas definições mais amplas, a definição padrão de ciclo em muitos contextos de algoritmos em grafos, especialmente ao discutir ciclos simples, implica um caminho com pelo menos três vértices.
```
// Estrutura de lista encadeada para representar vizinhos (adjacência)
typedef struct No{
	int valor;
	struct No* proximo;
} No;

// Grafo como array de listas de adjacência
typedef struct grafo{
	int numVertices;
	No **adj; // ponteiro para array de ponteiros Node*
}Grafo;

// Cria um novo nó de adjacência
No* criarNo(int dest){
	No *novoNo = (No*)malloc(sizeof(No));
	novoNo->valor = dest;
	novoNo->proximo = NULL;
	return novoNo;
}

// // Cria um grafo com V vértices
Grafo* criarGrafo(int numVertices){
	Grafo *gr = (Grafo*)malloc(numVertices * sizeof(Grafo));
	gr->numVertices = numVertices;
	gr->adj = (No**)malloc(numVertices * sizeof(No*));
	for(int i = 0; i < numVertices; i++){
		gr->adj[i] = NULL;
	}
	return gr;
}

// // Adiciona aresta não-direcionada entre u e v

void adicionarAresta(Grafo *gr, int u, int v){
	No *novoNo = criarNo(v);
	novoNo->proximo = gr->adj[u];
	gr->adj[u] = nodeNo;

	No *novoNo = criarNo(u);
	novoNo->proximo = gr->adj[v];
	gr->adj[v] = nodeNo;
}

// Função auxiliar DFS que detecta ciclo
int dfsCiclo(Grafo *gr, int v, int visited[], int parent){
	visited[v] = 1;

    // Percorre todos os vizinhos de v
	for(No *ptr = gr->adj[v]; ptr != NULL; ptr = ptr->proximo){
		int u = ptr->valor;

		// Se vizinho não visitado, recuse
		if(!visited[u]){
			if(dfsCiclo(gr, u, visited, v)){
				return 1;
			}
		}

		// // Se vizinho visitado e não for pai, ciclo detectado
		else if(u != parent){
			return 1;
		}
	}
	return 0;
}

// Detecta ciclo em todo o grafo
int eh_Ciclo(Grafo *gr){
	int V = gr->numVertices;
	int* visited = (int*)malloc(V * sizeof(int));
	for(int i = 0; i < V; i++){
		visited[i] = 0;
	}

 // Chama DFS para cada componente conexo
	 for(int v = 0; v < V; v++){
		 if(!visited[v]){
			 if(dfsCiclo(gr, v, visited, -1)){
				 free(visited);
				 return 1;
			 }
		 }
	 }
	 free(visited);
	 return 0;
}
```

## 2-
### A)

- Eu usaria listra de adjacencia, pois :
- 1 - Economia de espaço:
	- Lista de adjacência: armazena apenas as arestas existentes, ocupando `O(V + E)` memoria, onde V e o numero de pontos e E o numero de conexoes
	- Matriz de adjacência: ocupa `O(V^2)`, mesmo que muitos pares de pontos não estejam conectados.
- 2 - Eficiência nas operações típicas
	- Percorrer todos os vizinhos de um ponto (por exemplo, para busca em largura ou profundidade) custa `O(deg⁡(v))`, que é ideal quando deg⁡(v) é bem menor do que V.
	- Inserir uma nova conexão (arestas) em lista de adjacência é `O(1)` amortizado (basta acrescentar à lista do vértice).
- 3 - Custo de verificar existência de uma aresta
	- **Lista de adjacência:** para saber se existe a aresta (u,v), percorremos a lista de vizinhos de u até encontrar v (ou esgotar). Isso custa `O(deg(u))`
	- **Matriz de adjacência:** bastaria acessar diretamente o elemento `M[u][v]`, em O(1). Contudo, esse ganho de tempo compensa o custo muito maior de memória apenas em grafos muito densos ou quando V é pequeno.
- Resumo: Em um grafo esparso como o de pontos de onibus e metro no DF, optamos por lista de adjacencia. A checagem "Existe conexao entre u e v" tem complexidade `O(deg(u))`, o que na pratica, e eficiente dado que cada estacao se conecta a poucas outras.

### B) 
Como linhas de onibus e metro nao vao e voltar pela mesma linha, estamos tratando de um grafo dirigido, assim basta apenas fazer uma alcancabilidade desse grafo atras de BFS
```
// Retorna 1 se o Ponto B for alcancavel a partir de Ponto A
int alcancavel(Grafo *gr, int A, int B){

	// cria vetor de visitados, inicializado com zeros (não visitado)
	int *visitado = calloc(gr->numVertices, sizeof(int));

	// fila para BFS
	int *fila = malloc(gr->numVertices * sizeof(int));
	int inicio = 0; fim = 0;

	// Marca o vertice de partida como Visitado
	visitado[A] = 1;
	// Enfilera o vertice V1
	fila[fim++] = A;

	// Enquanto houver elementos na fila
	while (inicio < fim){
		// Desenfilera o proximo vertice
		int u = fila[inicio++];
		// Se chegamos no Ponto B, liberamos memoria e retorna verdadeiro
		if (B == u){
			free(visitado);
			free(fila);
			return 1;
		}
		
		// Percorre todos os vizinhos de u
		for(No *p = gr->adj[u]; p != NULL; p = p->proximo){
			// se o vizinho ainda nao foi visitado
			if(!visitado[v]){
				// Marca como visitado
				visitado[v] = 1;
				// Coloca no final da fila
				fila[fim++] = v;
			}
		}
	}

	// Se esgotamos a fila sem encontrar t, nao e alcancavel
	free(visitado);
	free(fila);
	return 0;
}
```

- Escolhi o algoritmo BFS porque ele explora todos os nós vizinhos antes de seguir para os próximos níveis, garantindo que se encontrar um caminho, será o mais curto em termos de número de conexões.
- Este é um fator importante em um cenário de transporte, onde Mojinho deseja minimizar o número de transferências.
- Complexidade: `O(V + E)`, onde V é o número de vértices (pontos de transporte) e E é o número de arestas (conexões).
- No pior caso, pode ser necessário visitar todos os vértices e percorrer todas as arestas uma vez.

### C) Para descobrir se existe volta do Ponto B para o Ponto A, basta apenas inverter os pontos na entrada da funcao; EX:

- Para verificar se é possível ir de um ponto a outro e depois retornar, precisamos simplesmente verificar a alcançabilidade em ambas as direções.
```
int temVolta(Grafo *gr, int A, int B){

	if(alcancavel(gr, A, B) == 1){
		printf("Existe o caminho de IDA");
	} 
	
 // Se não é possível ir, não é possível fazer ida e volta

    if (!ida)
        return false;

	if(alcancavel(gr, B, A) == 1){
		printf("Existe o caminho de Volta");
	}
	
}
```

- A solução é direta: verificamos se existe um caminho de A para B e, em seguida, se existe um caminho de B para A.
- Só consideramos possível fazer o trajeto completo se ambos os caminhos existirem.
- Complexidade: O(V + E) + O(V + E) = O(V + E), já que executamos o mesmo algoritmo duas vezes.
- Este é um caso em que precisamos avaliar a alcançabilidade em ambas as direções, então não há como otimizar além disso sem comprometer a solução.

### D) 
- Um ponto está completamente isolado se não tem nenhuma conexão de entrada nem de saída, ou seja, não é possível alcançá-lo a partir de nenhum outro ponto e nem sair dele para chegar a outros pontos.
```
// Função para encontrar pontos de transporte isolados
void encontrarPontosIsolados(Grafo* grafo) {
    // Arrays para marcar vértices com arestas de saída e entrada
    int* temArestaSaida = (int*) calloc(grafo->numVertices, sizeof(int));
    int* temArestaEntrada = (int*) calloc(grafo->numVertices, sizeof(int));
    
    // Percorrer o grafo para encontrar todas as conexões
    for (int i = 0; i < grafo->numVertices; i++) {
        No* temp = grafo->lista[i].cabeca;
        
        // Se este vértice tem pelo menos uma aresta saindo
        if (temp != NULL)
            temArestaSaida[i] = 1;
            
        // Marcar todos os vértices que têm arestas chegando
        while (temp) {
            temArestaEntrada[temp->vertice] = 1;
            temp = temp->proximo;
        }
    }
    
    // Imprimir os pontos isolados
    printf("Pontos de transporte isolados:\n");
    int contador = 0;
    
    for (int i = 0; i < grafo->numVertices; i++) {
        if (!temArestaSaida[i] && !temArestaEntrada[i]) {
            printf("Ponto %d\n", i);
            contador++;
        }
    }
    
    if (contador == 0)
        printf("Não há pontos isolados no sistema.\n");
    else
        printf("Total: %d pontos isolados\n", contador);
    
    // Limpar memória
    free(temArestaSaida);
    free(temArestaEntrada);
}
```

- Um ponto isolado não tem conexões de entrada nem de saída.
- Percorremos todo o grafo uma vez para identificar quais vértices têm conexões saindo deles e quais têm conexões chegando neles.
- Os pontos que não têm nenhuma das duas são considerados isolados.
- Complexidade: `O(V + E)` para percorrer o grafo inteiro e verificar todas as conexões.
- O(V) adicional para verificar quais vértices estão isolados.
- Portanto, o custo total é O(V + E).