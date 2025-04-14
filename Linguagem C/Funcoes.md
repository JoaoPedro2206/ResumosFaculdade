
### 1. Funcoes e modularizacao de codigo

- **Funcoes**: Resolver problemas complexos atraves da combinacao de solucoes menores
- **Sintaxe** de definicao:
```
<tipo> <nome_da_funcao>(<parametros>){
	<bloco de comandos>
	return <informacoes>;
}
```

---
### 2. Detalhes de uma funcao
- **Identificador**: mesma regra de variaveis
- Tipo de retorno:
	- Retorno nao e obrigatorio em C;
- Parametros de entrada:
	- Nenhum, um ou varios;

---

### 3. Exemplos de implementacao

```
#include <stdio.h>

float maior(float num1, float num2){
	if(num1>num2){
		return num1;
	} else {
		return num2;
	}
}

int main(){
	float x,y,m;

	printf("Insira um valor:\n");
	scanf("%f", &x);
	printf("Insira mais um valor:\n");
	scanf("%f", &y);
	m = maior(x,y);
	printf("Maior: %.2f\n", m);

}
```

---
### 4. Parametros de funcao distintos
- **Sintaxe** para parametros struct:
	`<tipo> <funcao> (<tipo_struct> <param>) {...}`
- **Sintaxes** para vetores/matrizes como parametro
	`<tipo> <funcao> (<tipo> <vet>[], int tam) {...}`
	`<tipo> <funcao> (<tipo> <vet>[<tam>] {...}`
	`<tipo> <funcao> (<tipo> *<vet>, int tam) {...}`
	`<tipo> <funcao> (<tipo> m[] [<tam2>], int tam1) {...}`
```
void imprime1(int v[], int n){
	for(int i = 0; i<n;i++){
		printf("%d ", v[i]);
	}
}

void imprime2(int v[5]){
	for(int i = 0; i<n;i++){
		printf("%d ", v[i]);
	}
}

void imprime3(int *v, int n){
	for (int i = 0;i<n;i++){
		printf("%d ", v[i]);
	}
}
```

---
### 5. Escopo
- **Escopo de variaveis**: local vs global
- Declaracao de um funcao em C:
	- Deve aparecer antes do main()
	- Sintaxe de um prototipo de funcao
	 `<tipo> <nome_da_funcao>(<parametros>);`