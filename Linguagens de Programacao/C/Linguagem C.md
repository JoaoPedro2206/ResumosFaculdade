
## 1 Introdução

### 1.1 Comentarios

// -> Comentario de uma linha
/* Mensagem */ -> Comentario de um bloco de texto

### 1.2 Bibliotecas

###### Biblioteca padrão de entrada e saída
```
#include <stdio.h>

-> Funcoes
printf() # Exibi mensagens no terminal
scanf() # Pega a entrada do usuario
fopen() # Abre algum arquivo
fclose() # Fecha algum arquivo
```

###### Biblioteca padrão do C
```
#include <stdlib.h>

-> Funcoes
malloc() # Aloca memoria
free() # desaloca a memoria
realloc() # realoca a memoria
atoi() # Converte para Int
atof() # Converte para Float
qsort() # Ordena um vetor
bsearch() # Busca em um vetor
system() # Funcoes do Sistema
```

###### Biblioteca para manipulação de cadeias de caracteres
```
#include <string.h>

-> Funcoes
strcpy() # Copia Strings
strcat() # Concatena Strings
strlen() # Mede o tamanho de um String
strcmp() # compara uma String
```

###### Biblioteca para funções matemáticas fundamentais
```
#include <math.h>

-> Funcoes
sin() # Seno
cos() # Cosseno
tan() # Tangente
sqrt() # Raiz
pow() # Potenciacao
log() # Logaritmo
```

###### Biblioteca para classificação e conversão de caracteres
```
#include <ctype.h>

-> Funcoes
isalpha() # Verifica alphanum
isdigit() # Verifica se e digito
toupper() # Converte para maiusculas
tolower() # Converte para minusculas
```

###### Biblioteca para lidar com data e hora
```
#include <time.h>

-> Funcoes
time() # tempo
clock() # medir tempo
localtime() # formatar data e horarios
```


### 1.3 Tipos de Variaveis

###### Endereco de memoria
- Quando quer acessar o endereco de memoria de uma variavel usa-se o simbolo `&` e o nome da variavel.
- Quando quer acessar o dado da variavel usa apenas o nome dela.
###### Tamanho e Tipo dos dados:
- `Int` -> Dado do tipo inteiro (4 bytes)
- `short` -> Dado do tipo inteiro (2 bytes)
- `long` -> Dado do tipo inteiro (8 bytes)
- `float` -> Dado do tipo decimal (4 bytes)
- `double` -> Dado do tipo decimal (8 bytes)
- `char` -> Dado do tipo caractere (1 byte)
- `bool` -> dado do tipo true or false
- `unsigned` -> A variavel so poder ser positiva

###### Para criar uma variavel com algum tipo desse dados é necessario:
```
(Tipo de dado da variavel) (Nome da Variavel);
(Tipo de dado da variavel) (Nome da Variavel) = (Valor inicial da Variavel);

Ex:
-> Variavel sem valor inicial
int x; # x e o nome da variavel e ela e do tipo inteira.

-> Variavel com valor incial
int x = 2; # x e o nome da variavel, ela e inteira e tem valor 2
```

###### Para criar um variavel constante usa-se o #define. O define geralmente vem no inicio do codigo, pois o compilador ja identifica antes de executar o resto do codigo. Uma variavel constante nao pode ter seu valor alterado.
```
#define NOME valor 
ou
const TIPO NOME = VALOR

Ex:
#define PI 3.14159 # Definiu a variavel PI com o valor de 3.14159
```

###### Especificadores do Printf e do Scanf
- `%d` → Inteiro
- `%f` → Número de ponto flutuante  
- `%lf` → double
- `%s` → String    
- `%c` → Char
- `%i` → Bool
- `%%` → Imprime o próprio `%`

###### Escopo das Variaveis: Uma variavel so pode ser acessada dentro da funcao que ela foi criada, ou seja, um variavel criada dentro da main, so pode ser acessada dentro da main. Variaveis criadas fora da funcao main sao chamadas de Variaveis Globais, ou seja, podem ser acessadas em qualquer lugar do codigo.
```
-> Ex de Variavel global
#include <stdio.h>
int x = 10;

int soma(){

}
int main(){

}

# Nesse caso a variavel X pode ser acessada tanto pela funcao soma tanto pela funcao main.

-> Ex de variavel normal
#include <stdio.h>

int soma(){
	int x = 10;
}
int main(){

}

# Nesse caso a variavel x so pode ser acessada pela funcao soma, se a funcao main tentar acessar a variavel x o codigo retornara um erro dizendo que a variavel nao esta definida.
```

### 1.4 Função Main

###### Função principal, onde o compilador começa a executar o codigo.
```
int main(){
  # Comandos que serao executados primeiro
}
```

### 1.5 Função Printf

###### A função printf exibi dados no console. O printf analisa a string de formatação caractere por caratere. Quando encontra um `%`, ela entra em modo de interpretação do especificador. Para cada especificador, **printf** converte o argumento correspondente para uma sequência de caracteres de acordo com as regras definidas (por exemplo, números são convertidos para sua representação decimal ou em outro formato, dependendo do especificador).

```

-> Printar uma String simples
printf("Hello Word") # Printa a string que esta dentro das aspas no console

-> Printar quando e uma variavel
printf("%d", x) # Dentro das aspas vai o tipo de dado que vai printar(%d -> inteiro) e depois da virgula a variavel que quer printar

-> Outras Funcoes:
/n # Quebra de Linha
\\ # Imprime o caractere da barra invertida
\' # Aspas Simples
\" # Aspas duplas
%.2f -> Duas casas decimais (para float)
%.3lf -> Três casas decimais (para double)
```

### 1.6 Função Scanf

###### A funcao Scanf() le dados digitados pelo usuario e armazena-os em variáveis.
```
scanf("Tipo do dado", &variavel); 
# O primeiro argumento indica os tipos de dados esperados e o segundo argumento sao os enderecoes de memoria das variaveis onde os valores lidos serao armazenados.


-> O scanf pode ler varios valores de um vez, se estiverem na mesma linha
int x, y;
scanf("%d %d", &x, &y);

```

###### Scanf com char e String: como uma string e um array de chars, nao precisa usar o &, pois arrays ja representam enderecos de memoria
```
char letra;
char nome[50];

scanf(" %c", &letra);  // espaço antes de %c ajuda a ignorar '\n' anterior
scanf("%s", nome);     // não precisa de & pois nome é um array
```

###### Scanf para validacao de entreda: o scanf tenta ler o tipo de dados especifico, se ele conseguir ele retorna o valor 1, se nao conseguir ele retorna 0
```
#include <stdio.h>

int main() {
    int idade;
    int resultado;

    printf("Digite sua idade: ");
    resultado = scanf("%d", &idade);

    if (resultado != 1) {
        printf("Entrada inválida. Por favor, digite um número inteiro.\n");
        return 1; // encerra o programa com erro
    }

    printf("Idade válida: %d anos\n", idade);
    return 0;
}


# Exemplo com repeticao ate digitar certo:

int main(){
	int numero;
	int sucesso;
	do {
        printf("Digite um número inteiro: ");
        sucesso = scanf("%d", &numero);

        if (sucesso != 1) {
            printf("Entrada inválida. Tente novamente.\n");

            // Limpa o buffer do teclado
            while (getchar() != '\n'); // descarta até a nova linha
        }
    } while (sucesso != 1);

    printf("Você digitou: %d\n", numero);
    return 0;
}

Quando o `scanf` falha, ele **não consome os caracteres inválidos** do buffer (como letras), o que causaria um **loop infinito**. O `while (getchar() != '\n')` serve para **limpar o buffer** até o final da linha.

```


### 1.7 Operadores Aritméticos:

- + → Soma
- - → Subtracao
- * → Multiplicacao
- / → Divisao
- % → Resto da Divisao
- ++ → Incremento
- -- → Decremento

### 1.8 Operadores Logicos:

- == → Igual
- != → Diferente
- > → Maior
- < → Menor
- >= → Maior igual
- <= → Menor igual
- && → And
- || → Or
- ! → Not

### 1.9 Operadores Condicionais:

###### IF, ELSE IF, ELSE
```
if(condicao 1){ # Se a condicao for verdadeira ele executa esse bloco
	# Comandos
} else if(condicao 2) { # se a condicao 1 for falsa e a 2 for verdaderia ele executa esse bloco de codigo

} else { # Se todas as outras condicoes forem falsas executa esse bloco

}

if -> SE
else if -> Senao se
else -> Senao
```

###### Switch Case:
```
switch(variavel){ # Olha para o valor de um variavel especifica
	case 1: # se o valor dela for igual ao valor do case, ele executa o bloco
		comando no caso 1
		break;
	case 2: # se o valor dela for igual ao valor do case, ele executa o bloco
		comando no caso 2
		break
	default: # se nao for igual a nenhum case ele executa o default
		comando no caso default
		break;
}
```

###### IF Ternario:
```
(condicao) ? valor se for verdade : valor se for false

EX

int x = 10
int y = 100

x > y ? "X e maior" : "X e menor"

```
### 1.10 Laços de Repetição:

- FOR -> Para
```
for(variavel de incial; condicao de parada; incremento ou decremento){

}

EX:
int main(){
	int num = 10;
	for(int i = 0; i < num; i++){ 
	# Vai executar esse bloco 10 vezes, pois a condicao de para e que o i tem que      ser menor que o num 
	}
	return 0
}
```

- While -> Enquanto
```
while(condicao){
# Verifica a condicao, se for verdade ele executa esse bloco ate a condicao ficar falsa.
}
```

- do While -> Faca enquanto
```
do{
# Primeiro executa o bloco de codigo, e depois verifica se a condicao e verdadeira, se for ele continua executando.
} while(condicao)
```
- break: Quebra o laco
- continue: Pula para a proxima iteracao
- while(1){}: Laca infinito

### 1.11 Arrays ou Vetores:

###### Para criar um array e necessario primeiro declara o tipo de dados do array, o nome dele e o tamanho dele.
```
int numero[10]; # Array de inteiros com tamanho 10

numero[0] = 1; # Atribui o valor 1 na posicao 0 do array

printf("%i", numero[0]) # printa o valor da posicao 0 do array

# Como o array comeca em 0, a ultima posicao que pode ser acessa e tamanho do array - 1.
```

###### Manipulacao de array
```
int main() {
	int vetor[5] = {4, 2} # Coloca os valores das chaves dentro do array
}

float numeros[100] = {0} # Inicializa o vetor com todas as posicoes com valor 0

# Usa o scanf com o for para colocar os elementos dentro do array
for(int i = 0; i < 5; i++){
	scanf("%f", &numeros[i])
}

```

###### Array de Char
```
# Um Array de Char e uma String

char nome[] = "Joao"; # equivalente a {'J','o','ã','o','\0'}

char nome[10];
scanf("%s", nome); # Nao valida o tamanho e pode dar erro

sprintf(NOME do array, STRING que quer colocar);

NOME do array[posicao depois da ultima letra da string] = '\0'; -> Indica o final da string

strlen(NOME do array) # Tamanho da String

size_t -> Tipo de variavel para tamanho de array
```

### 1.12 Matrizes:

###### Matrizes sao representadas com arrays dentro de arrays
```
TIPO NOME[3 LINHAS][3 COLUNAS]; # Matriz com 3 de largura e 3 de comprimento
[[x x x]
[x x x]
[x x x]] 

# Para acessar um item da matriz e necessario colocas a posicao dele
matriz[0][0] # Item na linha 0 e coluna 0
```

###### Manipulacao de Matriz:
```
# Para printar a matriz
for(int m = 0; m < 5; m++){
	for(int n = 0; n < 5; n++){
		printf("%i", matriz[m][n])
	}
	printf("/n")
}
```

### 1.13 Ponteiros
