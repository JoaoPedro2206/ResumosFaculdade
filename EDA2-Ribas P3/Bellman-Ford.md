
### 1. Bellman-Ford

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
