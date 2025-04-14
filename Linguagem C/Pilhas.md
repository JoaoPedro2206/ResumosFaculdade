### 1. Oque e
- As operacoes sao feitas no topo da pilhas (Insercao ou remocao);
- Funciona como uma pilha normal
- Apenas duas operacoes: `PUSH() e POP()`;
- Os Nos ficam espalhados na memoria, nao ficam em ordem;
- Estrutura do tipo LIFO: `LAST-IN FIRST-OUT`;
- O ultimo a entrar e o primeiro a sair;
---
### 2. Estrutura de um No
```
-> No com variaveis normais
typedef struct no{
	<tipo_dado> dado;
	struct no *<nome_ptr>;
}No;

-> No com vetor
typedef struct no{
	<tipo_dado> dado[10];
	struct no *<nome_ptr>;
}No;

-> No com structs
typedef struct no{
	<nome_struct> dado;
	struct no *<nome_ptr>;
}No;
```
---
### 3. `push()` 
- Ponteiro apontando para o topo da lista;
- `NULL <- *Topo`, se a pilha estiver vazia;
- `*Topo -> <Dado 1 e Ponteiro NULL>`;
- Composta por varios Nos, ou seja, structs;
- Cada No armazena um dado do tipo que quiser e uma ponteiro;
- Ao fazer uma insercao o ponteiro do No anterior ira apontar para o No inserido na pilha;
```
#include <stdio.h>
#include <stdlib.h>

typedef struct no{
	int valor;
	struct no *proximo;
}No;

// Funcao para a operacao push
void push(No **topo, int valor){
	No *novo = (No *)malloc(sizeof(No));
	
	if(novo){
		printf("Alocacao feita com sucesso");
		novo->dado = dado;
		novo->proximo = *topo;
		*topo = novo;
	} else {
		printf("ERRO na alocacao");
	}

}

int main(){

	No *topo = NULL;
	topo = empilhar(topo);

}
```
---
### 4. pop()
- Ao remover e necessario fazer 3 passos:
	- 1. Criar um ponteiro auxiliar que ira apontar para o No do topo da pilha
	- 2. O ponteiro Topo tera que apontar para o No que esta sendo apontando pelo No retirado da pilha;
	- 3. Remover o No `free(remover)`
```
#include <stdio.h>
#include <stdlib.h>

typedef struct no{
	int valor;
	struct no *proximo;
}No;

// Funcao para a operacao pop
int pop(No **topo){
	if(*topo == NULL){
		printf("Erro: Pilha vazia.\n");
		exit(1);
	}
	No *remover = *topo;
	int valor = remover->valor;
	*topo = remover-prox;
	free(remover);
	return valor;
}


int main(){

	No *topo = NULL;
	topo = empilhar(topo);

}
```
---
### 5. peek()
- Apenas retornar o valor no topo da pilha sem remover
```
int peek(No *topo){
	if(topo == NULL){
		printf("ERRO: Pilha Vazia");
		exit(1);
	}

	return topo->valor;
}
```

---
### 6. Outra estrutura de Pilha
```
#include <stdio.h>
#include <stdlib.h>

typedef struct{
	int dia,mes,ano;
}Data;

typedef struct{
	char nome[50]
	Data data;
}Pessoa;

typedef struct no{
	Pessoa p;
	struct no *proximo;
}No;

Pessoa ler_pessoa(){

	Pessoa p;

	printf("\nDigite nome e data de nascimento dd mm aaaa:\n");
	scanf("%49[^\n]%d%d%d", p.nome, &p.dado.dia, &p.dado.mes, &p.dado.ano);
	return p;
}

void imprimir_pessoa(Pessoa p){
	printf("\nNome: %dData: %2d/%2d/%4d\n", p.nome, p.data.dia, p.data.mes, p.data.ano);
}

// Opcao para empilhar
No* push(No *topo)}{
	 No *novo = malloc(sizeof(No));

	if(novo){
		novo->p = ler_pessoa();
		novo->proximo = topo;
		return novo;
	} else {
		printf("ERRO")
	}
	return NULL;
 }


// FUncao para desempilhar
No* pop(No **topo){
	if(*topo != NULL){
		No *remover = *topo;
		*topo = remover->proximo;
		return remover;
	} else {
		printf("Pilha Vazia")
	}
	return NULL;
}


int main(){

	No *remover, *topo = NULL;
	int opcao;

	do{
		printf("\n0 - Sair\n1 - Empilhar\n2 - Desemiplhar\n 3 - Imprimir\n");
		scanf("%d", &opcao);
		getchar();

		switch(opcao){
		case 1:
			topo = empilhar(topo);
			break;
		case 2:
			remover = desempilhar(&topo);
			if(remover){
				printf("Elemento removido com sucesso");
				imprimir_pessoa(remover);
			} else {
				printf("Sem no a remover")
			}
			break;
		case 3:
			break;
		default:
			if(opcao != 0){
				printf("Opcao invalida")
			}
		}	
	} while(opcao != 0);

	return 0;
}

```

```
#include <stdio.h>
#include <stdlib.h>

typedef struct{
	int dia,mes,ano;
}Data;

typedef struct{
	char nome[50]
	Data data;
}Pessoa;

typedef struct no{
	Pessoa p;
	struct no *proximo;
}No;

typedef struct{
	No *topo;
	int tam;
}Pilha;

void criar_pilha(Pilha *p){
	p->topo = NULL;
	p->tam = 0;
}


Pessoa ler_pessoa(){

	Pessoa p;

	printf("\nDigite nome e data de nascimento dd mm aaaa:\n");
	scanf("%49[^\n]%d%d%d", p.nome, &p.dado.dia, &p.dado.mes, &p.dado.ano);
	return p;
}

void imprimir_pessoa(Pessoa p){
	printf("\nNome: %dData: %2d/%2d/%4d\n", p.nome, p.data.dia, p.data.mes, p.data.ano);
}

// Opcao para empilhar
void push(Pilha *p)}{
	 No *novo = malloc(sizeof(No));

	if(novo){
		novo->p = ler_pessoa();
		novo->proximo = p->topo;
		p->topo;
	} else {
		printf("ERRO")
	}
 }


// FUncao para desempilhar
No* pop(Pilha *p){
	if(p->topo){
		No *remover = p->topo;
		p->topo = remover->proximo;
		return remover;
	} else {
		printf("Pilha Vazia")
	}
	return NULL;
}


int main(){

	No *remover, *topo = NULL;
	int opcao;

	do{
		printf("\n0 - Sair\n1 - Empilhar\n2 - Desemiplhar\n 3 - Imprimir\n");
		scanf("%d", &opcao);
		getchar();

		switch(opcao){
		case 1:
			topo = empilhar(topo);
			break;
		case 2:
			remover = desempilhar(&topo);
			if(remover){
				printf("Elemento removido com sucesso");
				imprimir_pessoa(remover);
			} else {
				printf("Sem no a remover")
			}
			break;
		case 3:
			break;
		default:
			if(opcao != 0){
				printf("Opcao invalida")
			}
		}	
	} while(opcao != 0);

	return 0;
}
```

```
celula *pi;

void criapilha (void) {
   pi = malloc (sizeof (celula)); // cabeça
   pi->prox = NULL; 
}

void empilha (char y) { 
   celula *nova;
   nova = malloc (sizeof (celula));
   nova->conteudo = y;
   nova->prox  = pi->prox;
   pi->prox = nova; 
}

char desempilha (void) {
   celula *p;
   p = pi->prox;
   char x = p->conteudo;
   pi->prox = p->prox;
   free (p);
   return x; 
}
```