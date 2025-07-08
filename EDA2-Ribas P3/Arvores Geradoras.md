- **Árvore Geradora**: subgrafo de um grafo não‑dirigido G que (i) é conexo, (ii) não tem ciclos e (iii) inclui todos os vértices de G.
- Toda árvore geradora em um grafo com V vértices tem exatamente V−1 arestas.
- Métodos para obter uma árvore geradora de um grafo conexo:
    - **Busca em Profundidade** (DFS)    
    - **Busca em Largura** (BFS)

## Leques e Cortes

- **Leque** (δ(X)\delta(X)δ(X)) de um conjunto de vértices XXX: todas as arestas com uma ponta em XXX e outra em seu complemento X‾\overline XX
- **Corte**: leque de um subconjunto **não-trivial** XXX (X≠∅,  X≠VX\neq\emptyset,\;X\neq VX=∅,X=V).
    
- Cada corte é identificado pelas suas duas “margens” XXX e X‾\overline XX.
    
- **Importância**: cortes caracterizam conexidade e formam a base da “Propriedade do Corte” em MST.