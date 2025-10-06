
### 1. Strings sao vetores de Char

##### Em linguagem C:
- Dados de texto sao algo um pouco abstrato
- E preciso entender como os dados estao dispostos em memoria
- Operacoes sobre caracteres individuais

| 0   | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
| O   | L   | A   | !   | \0  |

**O caractere \0 representao o final da string**

---
### 2. Strings: entrada e saida

##### scanf():
- Limitacoes: sintaxe rebuscada
- Especificador de formato: %s
- Sintaxe geral: 
	`scanf("%s", <str>`);  
	- Esse scanf nao le entradas com espacos
	- O scanf pode extrapolar tambem o tamanho do vetor de char, podendo causa erros
- Sintaxe aprimorada
	`scanf("%<tam.-1>[^\n]s", <str>);`
	- `<tam.-1>` Representa o tamanho da string que vai ser inserida
	- `[^\n]` Consegue ler espacos, vai ler tudo ate o usuario der enter
- Note: Nao precisa do &

##### printf():
- Especificador de formato: %s
- Sintaxe:
	`printf("<texto>", <str1>, <str2>, ..., <strN>);`

--- 
### 3. Exemplo de implementacao

```
int main(){

	char s[10]; # Array de char que pode armazenar uma string de ate 9 chars

	printf("Digite algo (scanf converncional):\n");
	scanf("%s", s);
	fflush(stdin); 

	printf("Resultado: %s\n\n", s);
}
```

```
int main(){

	char s[10]; # Array de char que pode armazenar uma string de ate 9 chars

	printf("Digite algo (scanf aprimorado):\n");
	scanf("%10[^\n]s", s);
	fflush(stdin); 

	printf("Resultado: %s\n\n", s);
```

---
### 4. Strings: Outras funcoes de entrada e saida

##### gets()
- Limitacoes: estouro do limite do vetor;
- Sintaxe:
	`gets(<string>)`
```
int main(){

	char s[10];

	printf("digite algo (leitura pelo gets): \n");
	gets(s);
	fflush(stdin);
}
```
##### fgets()
- Ultimo caractere sempre fica reservado ao '\0'
- Entrada padrao: stdin
- Sintaxe:
	`fgets(<string>, <tam>, stdin)`
	- Pega a entrada de dados padrao do teclado com stdin com o tamanho definido, coloca o \0 na ultima posicao e coloca dentro do array de char definido.
```
int main(){

	char s[10];

	printf("digite algo (leitura pelo fgets): \n");
	fgets(s, 10, stdin);
	fflush(stdin);
}
```
##### puts()
- Imprime uma string diretamente na tela
- Nao admite variaveis de outro tipos
- Sintaxe:
	`puts(<string>);`
```
int main(){

	char s[10];

	printf("digite algo (leitura pelo gets): \n");
	gets(s);
	fflush(stdin);

	puts("Resultado:");
	puts(s);
	puts("");
}
```
##### fflush(stdin)
- Chamar sempre depois de uma entrada
- Zera o buffer de memoria de entrada, evitando erros na entrada de dados

---
### 5. Biblioteca string.h

- Sintaxes de funcoes importantes:
	- `strcpy(<destino>, <origem>);` //  Usado para alterar o conteudo de uma string
	- `strcat(<destino>, <origem>);` // Juntar duas strings concatenar
	- `strlen(<string>);` // Comprimento da string
	- `strcmp(<string1>, <string2>);` // Compara se as strings sao iguais, se forem iguais retorna 0, se nao retorna outro valor.
 
- Biblioteca locale.h:
	- `setlocale(LC_ALL, "Portuguese");` // Permite acentos