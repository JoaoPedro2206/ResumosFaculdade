### 1. Ponteiros

- E um apontador para um endereco de memoria
- Variavel que contem enderecos de memoria
- Sintaxe:
	`<tipo_ptr> *<nome_ptr>;`
	- Para criar um ponteiro
	`<nome_ptr> = &<nome_variavel>;`
- `*prt` : o apontado por, conteudo do endereco da variavel que ptr aponta
- `ptr` : o endereco da variavel
- `&prt`: o endereco de memoria do ponteiro

---
### 2. Ponteiros na memoria

|      | var  |      |      | ptr  |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|      | 15   |      |      | 8001 |      |      |
| 8000 | 8001 | 8002 | 8003 | 8004 | 8005 | 8006 |
###### A variavel var tem valor de 15 e foi salva no endereco de memoria 8001, o ponteiro ptr foi salvo no endereco de memoria 8004 e seu valor e o endereco de memoria da variavel var 8001.

###### No printf se colocar `*ptr` ele vai printar o valor do endereco de memoria que esta apontando, se printar direto o ptr ele vai retornar o endero de memoria que esta apontando.

---
### 3. Atualizando dados pelo ponteiro

- Se colocar `*<ponteiro> = <valor>;`, ele vai atualizar esse valor na variavel que ele esta apontando.

---
### 4. Ponteiros a Structs

```
int main(){
	struct horario{
		int hora;
		int minuto;
		int segundos;
	};

	struct horario agora, *depois; # cria um struct e um ponteiro de struct

	depois = &agora; # Aponta o ponteiro para a struct agora

	(*depois).hora = 20; # O ponteiro acessa a hora da struct agora e muda o valor
	(*depois).minutos = 20; 
	(*depois).segundo = 20;
}
```

- Para um ponteiro de um struct mudar o valor da struct que ele aponta, pode ser feito com:
	`(*<nome_ponteiro>).<dado da struct que quer alterar> = <valor_novo>`
	`<nome_ponteiro> -> <dado da struct que quer alterar> = <valor_novo>`

---
### 5. Ponteiros a Structs (Operacoes Matematicas)
```
int main(){
	struct horario{
		int hora;
		int minuto;
		int segundos;
	};

	struct horario agora, *depois; # cria um struct e um ponteiro de struct

	depois = &agora; # Aponta o ponteiro para a struct agora

	depois->hora = 20;
	depois->minuto = 30;
	depois->segundos = 50;

	int somatorio = 100;

	struct horario antes;
	antes.hora = somatorio + depois->segundo;
	antes.minuto = agora.hora + depois->minuto;
	antes.segundos = depois->minuto + depois->segundos;
	
```

- E possivel tambem acessar o dado da struct principal pelo ponteiro que esta apontando pra ela, da seguinte forma:
	`<ponteiro>-><variavel_struct>;`

---
### 6. Structs que contem ponteiros
```
int  main(){
	struct horario{
		int *pHora;
		int *pMinuto;
		int *pSegundo;
	}

	struct horario hoje;

	int hora = 200;
	int minuto = 300;
	int segundo = 400;

	hoje.pHora = &hora;
	hoje.pMinuto = &minuto;
	hoje.pSegundo = &segundo;

	printf("Hora - %i\n", *hoje.pHora);
	printf("Minuto - %i\n", *hoje.pMinuto);
	printf("Segundo - %i\n", *hoje.pSegundo);
}
```

- Para apontar o ponteiro da struct para alguma variavel:
	`<struct_ponteiros>.<nome_ponteiro> = &<variavel>`
- Para acessar o valor desse ponteiro:
	`*<struct_ponteiros>.<nome_ponteiro>`

---
### 7. Ponteiro como parametro de um funcao

```
int main(){

	void testeVariavel(int x);
	void testePonteiro(int *pX);
	int teste = 1; # Variavel com valor 1
	int *pTeste = &teste; # ponteiro que aponte para a variavel teste

	testeVariavel(teste);  # Nao altera o valor da variavel teste
	testePonteiro(pTeste); # Altera o valor da variavel teste

}

void testeVariavel(int x){
	#Altera o valor da variavel x apenas dentro dessa funcao, ou seja, nao vai    mudar o valor na funcao main;
	++x;
}

void testePonteiro(int *pX){
	#Nesse caso, a funcao vai mudar o valor da variavel da funcao main, pois esta recebendo o endereco de memoria dela e alterando o valor desse endereco;
	++*pX;
}

```

- Para uma funcao alterar o valor de uma variavel que esta contina na main, precisa-se passar um ponteiro como parametro, para que a funcao ao inves de criar outra variavel igual e mudar seu valor ele mude o valor da variavel que foi passado pelo endereco de memoria dela;
- `<tipo> <nome> (<ponteiro que aponta para a variavel>){...}`

---
### 8. Lista Concatenada
```
int main(){

	struct lista{
		int valor;
		struct lista *proximo; # Ponteiro que vai apontar para outro struct	
	};

	struct lista m1, m2, m3; # Cria as structs m1,m2 e m3
	struct lista *gancho = &m1; # Cria a cabeca da lista que aponta para &m1

	m1.valor = 10; 
	m2.valor = 20;
	m3.valor = 30;

	m1.proximo = &m2; # a struct m1 vai apontar para a m2
	m2.proximo = &m3; # a struct m2 vai apontar para a m3
	m3.proximo = (struct lista *)0; # a struct m3 vai apontar para null


	while(gancho != (struct lista *)0){ # Enquando o cabeca nao for null
		printf("%d\n", gancho->valor); # Vai printar o valor da struct
		gancho = gancho->proximo; # vai passar para o proximo
	}
}
```
![](../Imagens/StructEncadeada.png)


---
### 9. Lista concatenada e Funcao que retorna Ponteiro

```
struct lista{
	int valor;
	struct lista *proximo;
};

struct lista *procuraValor(struct lista *pLista, int valor){ 
	# Retorna um ponteiro de tipo struct lista
	while(pLista != (struct lista *)0){
		if(pLista->valor == valor){
			return (pLista);
		} else {
			pLista = pLista->proximo;			
		}
	}
	return NULL;

}

int main(){

	struct lista *procuraValor(struct lista *pLista, int valor);
	struct lista m1,m2,m3;
	struct lista *resultado, *gancho = &m1;
	int valor;

	m1.valor = 5;
	m2.valor = 10;
	m3.valor = 15;

	m1.proximo = &m2;
	m2.proximo = &m3;
	m3.proximo = NULL;

	printf("Digite um valor:\n")
	scanf("%d\n", &valor);

	resultado = procurarValor(gancho, valor);

	if (resultado == NULL){
		printf("Valor nao encontrado")
	} else {
		printf("Valor %d encontrado. \n", resultado->valor);
	}
}
```

- Funcoes que retornam ponteiros: `<tipo> *<nome> (<parametros>){...}`
- A funcao procuraValor e do tipo struct lista e retorna um ponteiro, ela recebe um ponteiro do tipo struct lista que e o cabeca da lista e um valor que vai ser procurado na lista.
- Em quanto o cabeca nao apontar para nulo ele vai verificar se o valor e o desejado se nao aponta para a proxima struct da lista

---
### 10. Ponteiros e Vetores

```
int main(){

	int vetor[3] = {1,2,3};
	int *ponteiro = vetor; # O ponteiro vai apontar para o indice 0 do array
	int *ponteiro = &vetor[i]; # aponta para o indice que quer

	int *ponteiro = &vetor[0];
	printf("%p\n", ponteiro);

	ponteiro = &vetor[1];
	printf("%p\n", ponteiro);

	ponteiro = &vetor[2];
	printf("%p\n", ponteiro);
----------------------------------------------------------------------------------
	int *ponteiro = vetor;

	++ponteiro;
	++ponteiro;
----------------------------------------------------------------------------------

	*(ponteiro+1) = 10;
}
```
- %p e o indentidicador para printar endereco de memoria
- Se somar 1 no endereco de memoria do ponteiro ele passa a apontar para o proximo indice da lista
---
### 11. Ponteiro, Vetores e Funcoes

```
int somarVetor(int vetor[], const int n){
	int soma = 0;
	int *ponteiro;
	int *const finalVetor = vetor + n;
	for(ponteiro = vetor; ponteiro < finalVetor; ponteiro++){
		soma += *ponteiro;
	}

	return soma;
}

int main(){

	int somarVetor(int vetor[], const int n);
	int vetor[10] = {5,5,5,5,5,5,5,5,5,5};

	printf("A soma dos membros do vetor = %d", somaVetor(vetor,10));
	
}

```

---

### 12. Copiar String utilizando Ponteiros

```
void copiarString(char *copiarDaqui, char *colarAqui){

	while(*copiarDaqui != '\0'){ # Enquando a string nao acabaar
		*colarAqui = *copiarDaqui;
		copiarDaqui++; # percorre a string
		colarAqui++;
	}

	*colarAqui = '\0'; # Caractere nulo para o print parar
}


int main(){

	void copiarString(char *copiarDaqui, char *colarAqui);

	char string1[] = "Pao com mortadela";
	char string2[20];

	copiarString(string1, string2);
	printf("%s\n", string2);

}
```

---

### 13. Ponteiros de Ponteiros

```
int main(){
	int = A

}
```