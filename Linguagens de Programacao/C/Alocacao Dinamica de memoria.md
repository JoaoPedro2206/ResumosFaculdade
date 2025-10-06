

### 1. `#include <stdlib.h>`
- Bliblioteca com as funcoes de alocacao de memoria

---
### 2. `malloc()`: 
- Funcao para alocar memoria
- Retorna um ponteiro para a regiao de memoria alocada 
- Retorna NULL se nao conseguir alocar a memoria
- Tem que passar o parametro do tamanho que quer alocar
- sizeof() para facilitar
```
int main(){
	int *x;

	x = malloc(sizeof(int));

	if(x){
		printf("Alocado com sucesso");
		printf("x = %d\n", *x);
		*x = 50;
		printf("x = %d\n", *x);
	} else {
		printf("ERRO ao alocar memoria");
	}
}
```
---
### 3. `calloc()`:
- A unica diferenca para a funcao `malloc()` e a quantidade de parametros;
- 2 Parametros: `callor(<num de elemetos alocados>,<tam elemento alocado>)`
```
int main(){
	int *x;

	x = calloc(1,sizeof(int));

	if(x){
		printf("Alocado com sucesso");
		printf("x = %d\n", *x);
		*x = 50;
		printf("x = %d\n", *x);
	} else {
		printf("ERRO ao alocar memoria");
	}
}
```
---
### 4. Alocar vetor dinamico
- Alocacao de um vetor do tamanho que o usuario quiser
- Evita erros se o vetor for muito grande
```
int main(){
	int tam, *vet;

	printf("Digite o tamanho do vetor: ")
	scanf("%d", &tam);
	srand(time(NULL));

	vet = malloc(sizeof(int) * tam);
	ou 
	vet = calloc(tam, sizeof(int));

	if(vet){
		for(int i = 0; i<tam; i++){
			*(vet + 1) = rand() % 100;			
		}

		for(int i = 0; i<tam; i++){
			printf("%d ", *(vet + 1));
		}
	} else{
		printf("ERRO")
	}


}
```
---
### 5. `Realloc()`

- Retorna um ponteiro para a nova regiao de memoria
- Se o ponteiro for nulo ela aloca memoria
- se o novo tamanho for 0 a memoria e liberada
- Se nao houver memoria suficiente retorna NULL
- Recebe dois paramentros `realloc(<ptr alocado anteriormente>,<novo_tamanho>)`
```
int main(){
	int tam, *vet;

	printf("Digite o tamanho do vetor: ")
	scanf("%d", &tam);
	srand(time(NULL));

	vet = malloc(sizeof(int) * tam);
	ou 
	vet = calloc(tam, sizeof(int));

	if(vet){
		for(int i = 0; i<tam; i++){
			*(vet + 1) = rand() % 100;			
		}

		for(int i = 0; i<tam; i++){
			printf("%d ", *(vet + 1));
		}

		printf("Digite o novo tamanho do vetor: ")
		scanf("%d", &tam);

		vet = realloc(vet,tam);
		
	} else{
		printf("ERRO")
	}


}
```

---
### 6. `free()`

- Libera a memoria alocado pelo malloc()
- Se alocou memoria dinamicamente e necessario liberar essa memoria, para evitar erros
- Recebe 1 parametro: `free(<memoria que quer liberar(ptr)>)` 

```
int main(){
	int tam, *vet;

	printf("Digite o tamanho do vetor: ")
	scanf("%d", &tam);
	srand(time(NULL));

	vet = malloc(sizeof(int) * tam);
	ou 
	vet = calloc(tam, sizeof(int));

	if(vet){
		for(int i = 0; i<tam; i++){
			*(vet + 1) = rand() % 100;			
		}

		for(int i = 0; i<tam; i++){
			printf("%d ", *(vet + 1));
		}

		printf("Digite o novo tamanho do vetor: ")
		scanf("%d", &tam);	

		free(vet);
	} else{
		printf("ERRO")
	}
	


}
```

---
### 7. Diferenca entre malloc() e calloc()

- Com a `malloc()`, quando alocar a memoria pode vir com lixo de memoria;
- Ja com a funcao `calloc()`, a alocacao vem sem nada apenas com 0;
