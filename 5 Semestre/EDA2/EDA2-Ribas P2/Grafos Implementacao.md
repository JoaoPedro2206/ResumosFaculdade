### 1. Lista de Adjacencia 

- Estrutura para um No da lista de adjacencia
```
typedef struct No {

    int vertice;         // Vértice de destino

    struct No* proximo;  // Ponteiro para o próximo nó

} No;
```

- Estrutura para um No com peso (grafos Ponderados) da lista de adjacencia:
```
typedef struct No {

    int vertice;         // Vértice de destino

    int peso;            // Peso da aresta

    struct No* proximo;  // Ponteiro para o próximo nó

} No;
```

- Estrutura para uma lista de adjacencia
```
typedef struct Lista {

    No* cabeca;          // Ponteiro para o primeiro nó da lista

} Lista;
```

- Estrutura para o Grafo:
```
typedef struct Grafo {

    int numVertices;     // Número de vértices no grafo

    Lista* listaAdj;     // Array de listas de adjacência

    int* visitado;       // Array para controle de vértices visitados em buscas

} Grafo;
```

- Funcao para criar o No
```
No* criarNo(int v) { // Recebe o numero do vertice que vai se ligar

    No* novoNo = (No*)malloc(sizeof(No)); // Aloca o No

    novoNo->vertice = v; // Coloca o valor

    novoNo->peso = 1;  // Coloca o Peso da aresta, Padrao 1

    novoNo->proximo = NULL; // Aponta o proximo para NULL

    return novoNo; // Retorna o No

}
```

- Funcao para criar um grafo
```
Grafo* criarGrafo(int numVertices) {

    Grafo* grafo = (Grafo*)malloc(sizeof(Grafo)); // Aloca o grafo

    grafo->numVertices = numVertices; // coloca o numero de vertices do grafo

    // Criar um array de listas de adjacência

    grafo->listaAdj = (Lista*)malloc(numVertices * sizeof(Lista));

    // Inicializar cada lista de adjacência como vazia

    for (int i = 0; i < numVertices; i++) {

        grafo->listaAdj[i].cabeca = NULL;

    }

    // Criar array para controle de vértices visitados

    grafo->visitado = (int*)malloc(numVertices * sizeof(int));

    return grafo;

}
```

- Funcao para liberar/excluir um grafo:
```
void liberarGrafo(Grafo* grafo) {

    if (grafo) {
        if (grafo->listaAdj) {
            // Liberar cada lista de adjacência
            for (int v = 0; v < grafo->numVertices; v++) {
                No* atual = grafo->listaAdj[v].cabeca;
                while (atual) {
                    No* temp = atual;
                    atual = atual->proximo;
                    free(temp);
                }
            }
            free(grafo->listaAdj);
        }
        if (grafo->visitado) {
            free(grafo->visitado);
        }
        free(grafo);
    }
}
```

- Funcao que Adiciona uma Aresta ao grafo nao direcionado:
```
int adicionarAresta(Grafo* grafo, int origem, int destino) {

	// Verifica se existe o grafo
    if(gr == NULL)
        return 0;

    // Verifica de o Vertice existse
    if(orig < 0 || orig >= gr->num_vertices)
        return 0;
    if(dest < 0 || dest >= gr->num_vertices)
        return 0;
        

    // Adicionar aresta de origem para destino
    No* novoNo = criarNo(destino); // Cria o No com o vertice de destino

	// Faz o novoNo apontar para o No no inicio da lista
    novoNo->proximo = grafo->listaAdj[origem].cabeca; 

	// Atualiza o ponteiro da cabeca da lista para apontar para o novoNo
    grafo->listaAdj[origem].cabeca = novoNo;

    // Para grafo não direcionado, adicionar também de destino para origem
    novoNo = criarNo(origem);
    novoNo->proximo = grafo->listaAdj[destino].cabeca;
    grafo->listaAdj[destino].cabeca = novoNo;
}
```

- Funcao que Adiciona um Aresta com Peso:
```
void adicionarArestaComPeso(Grafo* grafo, int origem, int destino, int peso) {

    // Adicionar aresta de origem para destino
    No* novoNo = criarNoComPeso(destino, peso);
    novoNo->proximo = grafo->listaAdj[origem].cabeca;
    grafo->listaAdj[origem].cabeca = novoNo;

    // Para grafo não direcionado, adicionar também de destino para origem
    novoNo = criarNoComPeso(origem, peso);
    novoNo->proximo = grafo->listaAdj[destino].cabeca;
    grafo->listaAdj[destino].cabeca = novoNo;
}
```

- Funcao para remover uma aresta de um Grafo:
```
void removerAresta(Grafo* grafo, int origem, int destino) {

    // Inicializa dois ponteiro
    // Aponta para o primeiro No da lista de adjacencia do vertice origem
    No* atual = grafo->listaAdj[origem].cabeca; 
    // Comeca como NULL pois ainda nao temos No anterior ao primeiro
    No* anterior = NULL;

	// Percorre a lista do vertice de origem ate achar a aresta
    while (atual != NULL) {
        if (atual->vertice == destino) {
        
	        // Se o que vai ser removido for o cabeca da lista
            if (anterior == NULL) {
	            // O no cabeca vai apontar para o proximo da lista
                grafo->listaAdj[origem].cabeca = atual->proximo;
            } else {
	            // O No anterior aponta para o proximo do atual
                anterior->proximo = atual->proximo;
            }
            // Libera o No, assim excluindo a aresta
            free(atual);

			// Quebra o loop
            break;
        }

		// Se nao encontrar o No
		// Anterior passa a apontar para o no Atual
        anterior = atual;

		// atual avanca para o proximo No da lista
        atual = atual->proximo;
    }

    // Para grafo não direcionado, remover também de destino para origem
    atual = grafo->listaAdj[destino].cabeca;
    anterior = NULL;
    while (atual != NULL) {
        if (atual->vertice == origem) {
            if (anterior == NULL) {
                grafo->listaAdj[destino].cabeca = atual->proximo;
            } else {
                anterior->proximo = atual->proximo;
            }
            free(atual);
            break;
        }
        anterior = atual;
        atual = atual->proximo;
    }

}
```

- Funcao para imprimir o Grafo
```
void imprimirGrafo(Grafo* grafo) {

    for (int v = 0; v < grafo->numVertices; v++) {

        No* temp = grafo->listaAdj[v].cabeca;

        printf("\nLista de adjacência do vértice %d:\n%d", v, v);

        while (temp) {

            printf(" -> %d", temp->vertice);

            temp = temp->proximo;

        }

        printf("\n");

    }

}
```

---

### 2. Matriz de Adjacencia

- Estrutura para um grafo com matriz
```
typedef struct Grafo {

    int numVertices;     // Número de vértices no grafo

    int** matriz;        // Matriz de adjacência

    int* visitado;       // Array para controle de vértices visitados em buscas

} Grafo;
```

- Funcao para criar um grafo com V vertices
```
Grafo* criarGrafo(int V) {

    Grafo* grafo = (Grafo*)malloc(sizeof(Grafo));

    grafo->numVertices = V;

    // Criar array para controle de vértices visitados

    grafo->visitado = (int*)malloc(V * sizeof(int));

    // Alocar memória para a matriz de adjacência

    grafo->matriz = (int**)malloc(V * sizeof(int*));

    for (int i = 0; i < V; i++) {

        grafo->matriz[i] = (int*)malloc(V * sizeof(int));

        // Inicializar todos os valores da matriz como 0 (sem arestas)

        for (int j = 0; j < V; j++) {

            grafo->matriz[i][j] = 0;

        }

    }

    return grafo;

}
```

- Funcao para liberar/excluir o grafo:
```
void liberarGrafo(Grafo* grafo) {

    if (grafo) {

        // Liberar a matriz de adjacência

        if (grafo->matriz) {

            for (int i = 0; i < grafo->numVertices; i++) {

                if (grafo->matriz[i]) {

                    free(grafo->matriz[i]);

                }

            }

            free(grafo->matriz);

        }

        // Liberar o array de visitados

        if (grafo->visitado) {

            free(grafo->visitado);

        }

        // Liberar a estrutura do grafo

        free(grafo);

    }

}
```

- Funcao para adicionar uma aresta:
```
void adicionarAresta(Grafo* grafo, int origem, int destino) {

	// Verifica se os vertices sao validos
   if (origem >= 0 && origem < grafo->numVertices && 
        destino >= 0 && destino < grafo->numVertices) {
        // Adiciona aresta de origem para destino
        grafo->matriz[origem][destino] = 1;
        
        // Para grafo não direcionado, adiciona também de destino para origem
        grafo->matriz[destino][origem] = 1;
    }

}
```

- Funcao para adicionar uma aresta com peso:
```
void adicionarArestaComPeso(Grafo* grafo, int origem, int destino, int peso) {

	// Verifica se os vertices sao validos
   if (origem >= 0 && origem < grafo->numVertices && 
        destino >= 0 && destino < grafo->numVertices) {
        // Adiciona aresta de origem para destino
        grafo->matriz[origem][destino] = peso;
        
        // Para grafo não direcionado, adiciona também de destino para origem
        grafo->matriz[destino][origem] = peso;
    }

}
```

- Funcao para excluir uma aresta do grafo:
```
// Função para remover uma aresta de um grafo não direcionado
void removerAresta(Grafo* grafo, int origem, int destino) {
    // Verificar se os vértices são válidos
    if (origem >= 0 && origem < grafo->numVertices && 
        destino >= 0 && destino < grafo->numVertices) {
        // Remover aresta de origem para destino
        grafo->matriz[origem][destino] = 0;
        
        // Para grafo não direcionado, remover também de destino para origem
        grafo->matriz[destino][origem] = 0;
    }
}
```

- Funcao para imprimir o Grafo
```
void imprimirGrafo(Grafo* grafo) {

    printf("\nMatriz de Adjacência:\n");

    printf("   ");

    for (int i = 0; i < grafo->numVertices; i++) {

        printf("%d ", i);

    }

    printf("\n");

    for (int i = 0; i < grafo->numVertices; i++) {

        printf("%d: ", i);

        for (int j = 0; j < grafo->numVertices; j++) {

            printf("%d ", grafo->matriz[i][j]);

        }

        printf("\n");

    }

}
```

--- 