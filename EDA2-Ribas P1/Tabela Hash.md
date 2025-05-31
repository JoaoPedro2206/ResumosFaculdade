### 1. Oque e uma Tabela Hash
- Estrutura de dados utilizada para tornar o processo de busca mais eficiente;
- E basicamente um vetor em que os indices sao hashs de um elemento
- Parecido com dicionario do python;
- Cada elemento da tabela possui uma chave unica, e essa chave e o indice do vetor que o elemento se encontra;
- Usa os ultimos dois digitos das chaves para verificar o indice no vetor, isso faz com que evite desperdicio de memoria;
	- `chave % 100` Funcao hash ou funcao de espalhamento;
- As chaves hash sao unicas;
- ![Descrição da imagem](../Imagens/TabelaHash.png)

---
### 2. Funcao Hash
- Pega o elemento que quer inserir e pega o resto da divisao com alguma numero;
- O resto sera a chave Hash, ou seja, o indice que o elemento vai ser inserido no vetor
- `Chave % <tam_tabelaHash>`
- ![Descrição da imagem](../Imagens/Espalhamento.png)

---
### 3. Tratamento de colisoes

- Para evitar colisoes crie um tabela hash com tamanho primo
- Para descobrir esse primo, olhe para a quantidade de dados que tem que inserir e multiplique por 2, e depois pegue o numero primo mais proximo do resultado;
- EX: `M = 2 * <num_elemento> = (Primo mais proximo)`
- Fator de  carga: divida o numero de elementos pelo tamanho da tabela, para descobrir a porcentagem da tabela que sera ocupada;
- O fator de carga vai de 0 a 1, se for muito perto de 0 a tabela nao esta sendo usada corretamente havendo despedicio de memoria, se for muito perto de 1 a tabela estara muito cheia prejudicando na busca de um elemento;
- Existem 3 formas principais para tratar colisoes:
	- **Enderecamento Fechado:** Cada indice do vetor sera uma lista encadeado, se houver colisoes o elemento vai para a lista encadeada;
	- **Enderecamento Aberto:** Quando houver colisao, cheque o numero do hash + 1, ou seja, procure a proxima posicao vaga;
	- **Double Hash:** Se calcular a hash e houver colisao, ele calcula uma segunda hash para descobrir o indice que o elemento vai ficar;
---
### 4. Tabela Hash com Lista encadeada
- Cada posicao do vetor e composta por uma lista encadeada
- Ao inserir o indice do vetor apontara para um lista encadeada com o valor inserido
- se houver colisao, coloca o numero como o proximo da lista encadeada;
- Usa muita memoria, devido a cada indice do vetor ser uma lista encadeada.
- ![Descrição da imagem](../Imagens/Colisoes.png)

---
### 5. Encadeamento Aberto:

- Vetor de M posicoes;
- Se o houver uma colisao, ele vai para a proxima posicao livre do vetor e coloca insere o elemento;
- Se a tabela Hash tiver o quase o mesmo tamanho da quantidade de numeros que serao inseridos havera muitas colisoes, ocasionando em uma busca linear perdendo desempenho.
- Para evitar isso, deve aumentar o tamanho da tabela Hash.
- O problema de aumentar o tamanho da tabela Hash sera a mudanca de posicao de alguns elementos, pois a funcao hash ira mudar.
---
### 6. Hash Universal - Para Strings

- Defini valores fixos para A e B;
- Calcula o Hash com base em A, B e a representacao em inteiro do char.
- **Problema**: O custo dessa funcao hash comeca a ficar caro.
```
int hashU(char *v, int M){
	int h, a = 31415, b = 27183;
	for(h=0; *v!= '\0'; v++){
		a = a*b % (M-1);
		h = (a*h + *v) % M;
	}

	return h;
}
```
---
### 7. Conceitos essenciais
- `TAMANHO`: Quantidade maxima de elementos na tabela
- `FUNCAO HASH`: Funcao que gera um codigo a ser utilizado como indice de acesso na tabela;
- `COLISOES`: Ocorre uma colisao quando a funcao de hash gera o mesmo codigo para chaves diferentes;
- `FATOR DE CARGA`: Quantidade de elementos dividido pelo Tamanho da Tabela;
---
### 8. Implementacao da Tabela Hash linear ou Enderecamento Aberto:
```
#include <stdio.h>
#include <stdlib.h>
#define TAM  31 # Tamanho da tabela Hash

# Inicializa o vetor com todas os valores 0;
void inicializarTabela(int t[]){
		for(int i = 0; i < TAM; i++)
		t[i] = 0;
}

# Funcao para descobrir o indice que vai ser inserido
int hash(int chave){ 
	return chave % TAM
}

# Funcao para inserir um valor na tabela
void inserir(int t[], int valor){
	int id = hash(valor);
	while(t[id] != 0){
		id = hash(id + 1);
	}
	t[id] = valor;
}

#Funcao que busca um valor na tabela
int busca(int t[], int chave){
	int id = hash(chave);
	while(t[id] != 0){
		if(t[id] == chave){
			return t[id];
		} else {
			id = hash(id+1);
		}
	return 0;
}

#Funcao para imprimir a tabela
void imprimir(int t[]){
	for(int i = 0; i < TAM; i++){
		printf("%d = %d\n", i, t[i]);
	}

}


}
int main(){

	int opcao, tabela[TAM]; # Vetor da tabela hash
	return 0;

}
```
---
### 9. Tabela Hash com Lista Encadeada ou Encadeamento Separado: 

- Cada indice do vetor sera composto por uma lista encadeada;
- Evita colisoes, pois mesmo se houver colisoes o elemento ficara no msm indice, ou seja, ficara na lista encadeada presente no indice do Hash;
- `Implementacao:`
```
#include <stdio.h>
#include <stdlib.h>
#define TAM  31 # Tamanho da tabela Hash

# Struct do No da lista encadeada
typedef struct no{
	int chave;
	struct no *proximo;
}No;

# Estrutura da lista encadeada
typedef struct{
	No *inicio;
	int tam;
}Lista;

# Inicializa a Lista encadeada vazia
void inicializar_Lista(Lista *l){
	l->inicio = NULL;
	l->tam = 0;
}

# Funcao para inserir itens na lista;
void inserir_Lista(Lista *l, int valor){
	No *novo = malloc(sizeof(No));
	
	if(novo){
		novo->chave = valor;
		novo->proximo = l->inicio;
		l->inicio = novo;
	} else {
		printf("Erro")
	}
}

#Buscar um elemento na lista encadeada
int buscar_Lista(Lista *l, int valor){
	No *aux = l->inicio;
	while(aux && aux->chave != valor){
		aux = aux->proximo;
	}

	if(aux){
		return aux->chave;
	}
	return -1;
}

# Funcao para imprimir a lista
void imprimir_Lista(Lista *l){
	No *aux = l->inicio;
	printf("Tam: %d: ", l->tam);
	while(aux){
		printf("%d ", aux->chave);
		aux = aux->proximo;
	}
}

# Inicializa o vetor com todas os valores 0;
void inicializarTabela(Lista t[]){		
	for(int i = 0; i < TAM; i++){
		inicializar_Lista(&t[i]);
	}
}

# Funcao para descobrir o indice que vai ser inserido
int hash(int chave){ 
	return chave % TAM
}

# Funcao para inserir um valor na tabela
void inserir(Lista t[], int valor){
	int id = hash(valor);
	inserir_Lista(&t[id], valor);
}

#Funcao que busca um valor na tabela
int busca(Lista t[], int chave){
	int id = hash(chave);
	return buscar_Lista(&t[id], chave);
}

#Funcao para imprimir a tabela
void imprimir(Lista t[]){
	for(int i = 0; i < TAM; i++){
		printf("%2d = ", i);
		imprimir_Lista(&t[i]);
		printf("\n")
	}

}
}
int main(){

	int opcao, tabela[TAM]; # Vetor da tabela hash
	return 0;

}
```

---
### 10. Tabela Hash com varias Structs

- Estrutura Pessoa
```
typedef struct P{
	char nome[50];
	int cpf;
}Pessoa;
```
- Funcao para incializar a tabela:
```
void init(Pessoa t[]){
	int i;
	for(i = 0; i < TAM; i++)
		t[i].cpf = 0;
}
```
- Funcao Hash
```
int hash(int chave){
	return chave % TAM;
}
```
- Funcao inserir
```
void inserir(Pessoa t[], Pessoa p){
	int id = hash(p.cpf);
	while(t[id].cpf != 0){
		id = hash(id + 1);
	}
	t[id] = p;
}
```
- Funcao Busca
```
Pessoa* busca(Pessoa t[], int chave){

	int id = hash(chave);
	while(t[id].cpf != 0){
		if(t[id].cpf == chave){
			return &t[id];
		} else {
			id = hash(id+1);
		}
	}
	return NULL;
}
```

---
### 11. Double Hash
``
```
typedef struct Item{
	int chave;
	long e1, e2;
	long elemento;
}Item; Item NULLITEM = {0,0,0,0}
```
```
#define Key(x) (x.chave);
#define null(A) ((Key(ht[A])) == Key(NULLITEM))
```
```
int hash(int v, int M){
	return v%M;
}

int hashTwo(int v, int M){
	return (v%97)+1
}
```
- Funcao de insercao
```
void HTinsert(Item item){
	Key v = Key(item);
	int i = hash(v,M);
	int k = hashTwo(v,M);
	while(!null(i)){
		i = (i+k) % M;
	} 
	ht[i] = item;
	n++;
}
```
- Funcao de Busca
```
Item HTSearch(Key v){
	int i = hash(v,M);
	int k = hashTwo(v,M);
	while(!null(i)) {
		if(v == key(ht[i])) return ht[i];
		else i = (i+k) % M;
	}
	return NULLITEM;

}
```
---
### 12. Tabela Hash Dinamica

```
void expand(){
	int i;
	Item *t = ht;
	ht = malloc(sizeof(Item) * M * 2);
	M = M * 2;
	for(i = 0; i<M/2; i++){
		if(Key(t[i]) != key(NULLITEM)){
			S Tinsert(t[i]);
		}
	}
	free(t);

}
```
```
void HTinsert(Item item){
	Key v = Key(item);
	int i = hash(v,M);
	int k = hashTwo(v,M);
	while(!null(i)) i = (i+k) % M;
	ht[i] = item;
	n++;
	if(n >= M/2) 
		expand();
}
```