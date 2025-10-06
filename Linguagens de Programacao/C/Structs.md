### 1. Structs
- Definindo novo tipo
	- `typedef`
- Declarando variaveis do novo tipo
- Acessando membros de uma variavel `struct`
---
### 2. Tipos de dados compostos
- Structs(registros)
	- Sintaxe de definicao
```
struct <novo_tipo>{
	<tipo1> <campo1>;
	<tipo2> <campo2>;
	...
	<tipoN> <campoN>;
};
```

---
### 3. Declarando variaveis do novo tipo
- Comando typedef: renomeia um identificador
	- Sintaxe:
	 `typedef <tipo> <novo_nome>;`
	- Sintaxes de declaracao de variavel `struct`:
	 `struct <novo_tipo> <nome_variavel>;`
	 `<novo_nome> <nome_variavel>;`

---
### 4. Acessando os membros de uma struct
- Antes de mais nada, e preciso haver uma variavel desse tipo declarada
	- Sintaxe:
	 `<variavel>.<campo>`

- Fato: E comum misturar vetores e structs!

--- 
### 5. Exemplos de Implementacao
```
#define TAM 50

struct tipo_pessoa{
	int idade;
	float peso;
	char nome[TAM];
}

typedef struct tipo_pessoa tipo_pessoa;

int main(){
	// Criando e inicialicando
	tipo_pessoa pes = {0, 0.0, "Teste"};

	printf("Inicio:\n")
	printf("pes.idade: %d\n", pes.idade);
	printf("pes.peso: %.2f\n", pes.peso);
	printf("pes.nome: %s\n", pes.nome);

	// Atribuindo valores aos campos
	pes.idade = 10;
	pes.peso = 99.99;
	strcpy(pes.nome, "Texto");

	printf("\nAlterando os campos via codigo:\n")
	printf("pes.idade: %d\n", pes.idade);
	printf("pes.peso: %.2f\n", pes.peso);
	printf("pes.nome: %s\n", pes.nome);

	// Solicitando insercoes via teclado
	printf("\nInsira um numero inteiro:\n");
	scanf("%d", &pes.idade);
	printf("\nInsira um numero real:\n");
	scanf("%f", &pes.peso);
	fflush(stdin);
	printf("\nInsira uma palavra:\n");
	scanf("%s", &pes.nome);

	printf("\nAlterando os campos via teclado:\n")
	printf("pes.idade: %d\n", pes.idade);
	printf("pes.peso: %.2f\n", pes.peso);
	printf("pes.nome: %s\n", pes.nome);
}
```

```
#define TAM 3

struct tipo_pessoa{
	int idade;
	float peso;
	char nome[50];
};

typedef struct tipo_pessoa tipo_pessoa;

int main(){
	tipo_pessoa lista[TAM]

	for (int i = 0; i<TAM;i++){
		printf("Insira os dados (%d):\n", i+1);
		puts("Nome: ");
		scanf("%50[^\n]s", &lista[i].nome);
		fflush(stdin);

		puts("Idade: ");
		scanf("%d", &lista[i].idade);
		fflush(stdin);

		puts("Peso: ");
		scanf("%f", &lista[i].peso);
		fflush(stdin);
	}
	system("cls");

	puts("Seus dados:\n");
	for(int i=0; i<TAM; i++){
		printf("Pessoa %d", i+1);
		printf("\tNome: %s\n", lista[i].nome);
		printf("\tIdade: %d\n", lista[i].idade);
		printf("\tPeso: %.2f\n", lista[i].peso);
		
	}
	
}
```