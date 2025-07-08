
Uma **árvore geradora mínima** (do inglês _Minimum Spanning Tree_, MST) de um grafo conexo e ponderado é um subgrafo que:
1. **É uma árvore** — conecta todos os vértices sem formar ciclos.
2. **Espalha** sobre todos os vértices do grafo original (ou seja, contém exatamente V–1 arestas, onde V é o número de vértices).
3. **Minimiza** o peso total, isto é, a soma dos pesos de suas arestas é a menor possível dentre todas as árvores geradoras.
---
## Propriedades Fundamentais

- **Uniqueness (Unicidade)**
    - Se todos os pesos das arestas são distintos, a MST é única.
    - Caso haja pesos repetidos, podem existir várias MSTs diferentes com igual peso total.
- **Corte (Cut) e Ciclo (Cycle)**
    - **Propriedade do Corte**: Sejam dois grupos quaisquer de vértices, digamos A e B, que juntos formam todo o conjunto de vértices do grafo e não têm nenhum elemento em comum. Considere todas as arestas que ligam um vértice de A a um vértice de B. A aresta de menor peso entre essas é garantidamente parte de alguma árvore geradora mínima.
    - **Propriedade do Ciclo**: Em qualquer ciclo do grafo, a aresta de maior peso não faz parte de nenhuma MST.
Essas propriedades são a base para provar a correção dos algoritmos gulosos (Greedy) para MST.

---

## Algoritmos Clássicos

- 1. **Kruskal**
    - Ordena todas as arestas em ordem crescente de peso.
    - Itera em cada aresta, adicionando-a ao forest (conjunto de componentes) apenas se ela não criar ciclo (verificado por _Union‑Find_ / Disjoint Set Union).
    - Continua até ter V–1 arestas.
    - **Complexidade**:
        - Ordenação: O(E log E)
        - Union‑Find: quase O(1) amortizado por operação
        - **Total**: O(E log E) ≃ O(E log V)
- 2. **Prim**
    - Inicia em um vértice qualquer, constrói iterativamente a MST adicionando sempre a aresta de menor peso que conecta o conjunto “já gerado” ao restante do grafo.   
    - Implementação com **heap** (fila de prioridade):
        - Cada aresta incidente num vértice maduro entra na fila; ao extrair, se o vértice alvo ainda não está maduro, é adicionado.
        - Complexidade: O((V + E) log V) ≃ O(E log V)
    - Com **fila de prioridade linear** (array simples), dá O(V² + E) — bom para grafos densos.

---
## Complexidade e Escolha de Algoritmo

- Para **grafos esparsos** (E ≪ V²), o custo dominante é O(E log V). Kruskal e Prim com heap são preferidos.
- Para **grafos muito densos** (E ≈ V²), Prim com implementação em array (O(V²)) pode ser mais rápido.
---
## Aplicações Comuns

- **Redes de Comunicação**: construir backbones de mínima latência ou custo.
- **Projetos de Infraestrutura**: redes de distribuição de água, eletricidade ou estradas com custo mínimo.
- **Clustering em Aprendizado de Máquina**: definir agrupamentos mínimo‑cobertos.
- **Algoritmos de Imagem**: segmentação via grafos, onde MSTs ajudam a detectar fronteiras.
---
## Resumo das Etapas de Kruskal

- **1. Ordenar** todas as arestas.
- **2. Para** cada aresta na ordem crescente:
    - Se conectar duas componentes distintas, **adicionar** à MST (e unir componentes).    
- **3. Fim** quando MST tiver V–1 arestas.

---
## Resumo das Etapas de Prim

- **1. Escolher** vértice inicial, marcá‑lo como “maduro”.
- **2. Repetir** V–1 vezes:
    - Selecionar a **menor** aresta que liga um vértice maduro a um não‑maduro.
    - **Marcar** o novo vértice como maduro e **incluir** essa aresta na MST.
- **3. Fim** quando todos os vértices estiverem maduros.