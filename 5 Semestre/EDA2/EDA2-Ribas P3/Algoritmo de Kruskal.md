
O **Algoritmo de Kruskal** é um algoritmo guloso (greedy) usado para encontrar a **Árvore Geradora Mínima (MST - Minimum Spanning Tree)** de um grafo conectado e ponderado. Desenvolvido por Joseph Kruskal em 1956, é um dos algoritmos mais eficientes para resolver este problema.

## Conceito Fundamental

Uma Árvore Geradora Mínima é um subgrafo que:

- Conecta todos os vértices do grafo original
- É uma árvore (não possui ciclos)
- Tem o menor peso total possível entre todas as árvores geradoras

## Como Funciona

O algoritmo segue uma estratégia gulosa simples:

1. **Ordenação**: Ordena todas as arestas do grafo em ordem crescente de peso
2. **Seleção**: Examina cada aresta na ordem ordenada
3. **Verificação**: Para cada aresta, verifica se sua adição criará um ciclo
4. **Decisão**: Se não criar ciclo, adiciona a aresta à MST; caso contrário, descarta

## Estrutura de Dados Chave

O algoritmo utiliza a estrutura **Union-Find (Disjoint Set)** para:

- Detectar ciclos eficientemente
- Gerenciar conjuntos disjuntos de vértices
- Operações principais: `Find()` e `Union()`

## Pseudocódigo

```
KRUSKAL(G):
    A = ∅  // conjunto de arestas da MST
    Para cada vértice v em G:
        MAKE-SET(v)
    
    Ordenar arestas de G por peso crescente
    
    Para cada aresta (u,v) em ordem:
        Se FIND-SET(u) ≠ FIND-SET(v):
            A = A ∪ {(u,v)}
            UNION(u,v)
    
    Retornar A
```

## Complexidade

- **Tempo**: O(E log E) onde E é o número de arestas
    - Ordenação das arestas: O(E log E)
    - Operações Union-Find: O(α(V)) por operação, onde α é a função de Ackermann inversa
- **Espaço**: O(V) para a estrutura Union-Find

## Vantagens

- **Simplicidade**: Fácil de entender e implementar
- **Eficiência**: Bom desempenho para grafos esparsos
- **Garantia**: Sempre encontra a MST ótima
- **Flexibilidade**: Funciona bem com diferentes representações de grafos

## Desvantagens

- **Ordenação**: Requer ordenação prévia das arestas
- **Grafos Densos**: Menos eficiente que Prim para grafos muito densos
- **Memória**: Precisa armazenar todas as arestas

## Exemplo Prático

Para um grafo com vértices A, B, C, D e arestas:

- (A,B) peso 1
- (B,C) peso 2
- (C,D) peso 3
- (A,D) peso 4
- (B,D) peso 5

O algoritmo:

1. Ordena: (A,B)=1, (B,C)=2, (C,D)=3, (A,D)=4, (B,D)=5
2. Adiciona (A,B) - não há ciclo
3. Adiciona (B,C) - não há ciclo
4. Adiciona (C,D) - não há ciclo
5. Ignora (A,D) e (B,D) - criariam ciclos

**Resultado**: MST com arestas (A,B), (B,C), (C,D) e peso total = 6

## Aplicações

- **Redes**: Projeto de redes de comunicação com custo mínimo
- **Transporte**: Planejamento de rotas e infraestrutura
- **Clustering**: Análise de agrupamentos em dados
- **Circuitos**: Design de circuitos eletrônicos
- **Aproximação**: Base para algoritmos de aproximação em problemas NP-difíceis

O algoritmo de Kruskal é fundamental em teoria dos grafos e tem aplicações práticas em diversas áreas da computação e engenharia, sendo especialmente útil quando se precisa conectar elementos com o menor custo total possível.

---

```
#include <stdio.h>
#include <stdlib.h>

// Estrutura para representar uma aresta
typedef struct {
    int src, dest, weight;
} Edge;

// Estrutura para representar um grafo
typedef struct {
    int V, E;      // V = número de vértices, E = número de arestas
    Edge* edges;   // Array de arestas
} Graph;

// Estrutura para Union-Find (Disjoint Set)
typedef struct {
    int parent;
    int rank;
} Subset;

// ==================== FUNÇÕES AUXILIARES ====================

// Função para criar um grafo com V vértices e E arestas
Graph* createGraph(int V, int E) {
    Graph* graph = (Graph*)malloc(sizeof(Graph));
    graph->V = V;
    graph->E = E;
    graph->edges = (Edge*)malloc(E * sizeof(Edge));
    return graph;
}

// Função para adicionar uma aresta ao grafo
void addEdge(Graph* graph, int index, int src, int dest, int weight) {
    graph->edges[index].src = src;
    graph->edges[index].dest = dest;
    graph->edges[index].weight = weight;
}

// ==================== UNION-FIND OPERATIONS ====================

// Função para encontrar o conjunto de um elemento (com compressão de caminho)
int find(Subset subsets[], int i) {
    // Compressão de caminho: faz o nó apontar diretamente para a raiz
    if (subsets[i].parent != i) {
        subsets[i].parent = find(subsets, subsets[i].parent);
    }
    return subsets[i].parent;
}

// Função para unir dois conjuntos por rank
void Union(Subset subsets[], int x, int y) {
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);
    
    // Une pela rank - árvore menor vira subárvore da maior
    if (subsets[xroot].rank < subsets[yroot].rank) {
        subsets[xroot].parent = yroot;
    }
    else if (subsets[xroot].rank > subsets[yroot].rank) {
        subsets[yroot].parent = xroot;
    }
    else {
        // Se ranks são iguais, escolhe um como raiz e incrementa rank
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

// ==================== ALGORITMO DE ORDENAÇÃO ====================

// Função de comparação para qsort (ordena arestas por peso)
int compare(const void* a, const void* b) {
    Edge* edgeA = (Edge*)a;
    Edge* edgeB = (Edge*)b;
    return edgeA->weight - edgeB->weight;
}

// ==================== ALGORITMO DE KRUSKAL ====================

void KruskalMST(Graph* graph) {
    int V = graph->V;
    Edge result[V];  // Array para armazenar a MST
    int e = 0;       // Índice para result[]
    int i = 0;       // Índice para arestas ordenadas
    
    printf("\n=== ALGORITMO DE KRUSKAL ===\n");
    
    // PASSO 1: Ordenar todas as arestas por peso
    printf("\nPasso 1: Ordenando arestas por peso...\n");
    qsort(graph->edges, graph->E, sizeof(graph->edges[0]), compare);
    
    printf("Arestas ordenadas:\n");
    for (int j = 0; j < graph->E; j++) {
        printf("  (%d-%d): %d\n", 
               graph->edges[j].src, 
               graph->edges[j].dest, 
               graph->edges[j].weight);
    }
    
    // PASSO 2: Criar subconjuntos para Union-Find
    printf("\nPasso 2: Inicializando Union-Find...\n");
    Subset* subsets = (Subset*)malloc(V * sizeof(Subset));
    
    // Inicializar cada vértice como seu próprio conjunto
    for (int v = 0; v < V; v++) {
        subsets[v].parent = v;
        subsets[v].rank = 0;
        printf("  Vértice %d: parent=%d, rank=%d\n", v, v, 0);
    }
    
    // PASSO 3: Processar arestas uma por uma
    printf("\nPasso 3: Processando arestas...\n");
    
    while (e < V - 1 && i < graph->E) {
        // Próxima aresta com menor peso
        Edge next_edge = graph->edges[i++];
        
        // Encontrar conjuntos dos vértices da aresta
        int x = find(subsets, next_edge.src);
        int y = find(subsets, next_edge.dest);
        
        printf("\nAnalisando aresta (%d-%d) peso %d:\n", 
               next_edge.src, next_edge.dest, next_edge.weight);
        printf("  Conjunto do vértice %d: %d\n", next_edge.src, x);
        printf("  Conjunto do vértice %d: %d\n", next_edge.dest, y);
        
        // Se os vértices pertencem a conjuntos diferentes, não forma ciclo
        if (x != y) {
            printf("  ✓ Não forma ciclo - ACEITA\n");
            result[e++] = next_edge;
            Union(subsets, x, y);
        }
        else {
            printf("  ✗ Forma ciclo - REJEITA\n");
        }
    }
    
    // PASSO 4: Mostrar resultado
    printf("\n=== RESULTADO - ÁRVORE GERADORA MÍNIMA ===\n");
    int totalWeight = 0;
    
    for (i = 0; i < e; i++) {
        printf("Aresta %d: (%d-%d) peso %d\n", 
               i+1, result[i].src, result[i].dest, result[i].weight);
        totalWeight += result[i].weight;
    }
    
    printf("\nPeso total da MST: %d\n", totalWeight);
    
    // Liberar memória
    free(subsets);
}

// ==================== FUNÇÕES DE DEMONSTRAÇÃO ====================

// Função para imprimir o grafo
void printGraph(Graph* graph) {
    printf("\n=== GRAFO ORIGINAL ===\n");
    printf("Vértices: %d, Arestas: %d\n", graph->V, graph->E);
    printf("Lista de arestas:\n");
    
    for (int i = 0; i < graph->E; i++) {
        printf("  %d: (%d-%d) peso %d\n", 
               i+1, 
               graph->edges[i].src, 
               graph->edges[i].dest, 
               graph->edges[i].weight);
    }
}

// Função para demonstrar Union-Find isoladamente
void demonstrateUnionFind(int V) {
    printf("\n=== DEMONSTRAÇÃO UNION-FIND ===\n");
    
    Subset* subsets = (Subset*)malloc(V * sizeof(Subset));
    
    // Inicializar
    printf("Inicializando %d elementos:\n", V);
    for (int i = 0; i < V; i++) {
        subsets[i].parent = i;
        subsets[i].rank = 0;
        printf("  Elemento %d: parent=%d, rank=%d\n", i, i, 0);
    }
    
    // Demonstrar operações
    printf("\nOperações:\n");
    
    // União de 0 e 1
    printf("Union(0, 1):\n");
    Union(subsets, 0, 1);
    printf("  Elemento 0: parent=%d, rank=%d\n", subsets[0].parent, subsets[0].rank);
    printf("  Elemento 1: parent=%d, rank=%d\n", subsets[1].parent, subsets[1].rank);
    
    // União de 2 e 3
    printf("Union(2, 3):\n");
    Union(subsets, 2, 3);
    printf("  Elemento 2: parent=%d, rank=%d\n", subsets[2].parent, subsets[2].rank);
    printf("  Elemento 3: parent=%d, rank=%d\n", subsets[3].parent, subsets[3].rank);
    
    // Find operations
    printf("\nOperações Find:\n");
    for (int i = 0; i < V; i++) {
        int root = find(subsets, i);
        printf("  Find(%d) = %d\n", i, root);
    }
    
    free(subsets);
}

// ==================== FUNÇÃO PRINCIPAL ====================

int main() {
    printf("=== IMPLEMENTAÇÃO DO ALGORITMO DE KRUSKAL ===\n");
    
    // Demonstrar Union-Find primeiro
    demonstrateUnionFind(4);
    
    // Exemplo 1: Grafo simples
    printf("\n\n=== EXEMPLO 1: GRAFO SIMPLES ===\n");
    Graph* graph1 = createGraph(4, 5);
    
    // Adicionar arestas (src, dest, weight)
    addEdge(graph1, 0, 0, 1, 1);  // A-B peso 1
    addEdge(graph1, 1, 1, 2, 2);  // B-C peso 2
    addEdge(graph1, 2, 2, 3, 3);  // C-D peso 3
    addEdge(graph1, 3, 0, 3, 4);  // A-D peso 4
    addEdge(graph1, 4, 1, 3, 5);  // B-D peso 5
    
    printGraph(graph1);
    KruskalMST(graph1);
    
    // Exemplo 2: Grafo mais complexo
    printf("\n\n=== EXEMPLO 2: GRAFO MAIS COMPLEXO ===\n");
    Graph* graph2 = createGraph(6, 9);
    
    // Grafo com 6 vértices (0-5) e 9 arestas
    addEdge(graph2, 0, 0, 1, 4);
    addEdge(graph2, 1, 0, 2, 3);
    addEdge(graph2, 2, 1, 2, 1);
    addEdge(graph2, 3, 1, 3, 2);
    addEdge(graph2, 4, 2, 3, 4);
    addEdge(graph2, 5, 3, 4, 2);
    addEdge(graph2, 6, 3, 5, 6);
    addEdge(graph2, 7, 4, 5, 1);
    addEdge(graph2, 8, 2, 5, 5);
    
    printGraph(graph2);
    KruskalMST(graph2);
    
    // Análise de complexidade
    printf("\n=== ANÁLISE DE COMPLEXIDADE ===\n");
    printf("Complexidade de tempo: O(E log E)\n");
    printf("  - Ordenação das arestas: O(E log E)\n");
    printf("  - %d operações Union-Find: O(E α(V))\n", graph2->E);
    printf("Complexidade de espaço: O(V) para Union-Find\n");
    
    // Liberar memória
    free(graph1->edges);
    free(graph1);
    free(graph2->edges);
    free(graph2);
    
    return 0;
}
```