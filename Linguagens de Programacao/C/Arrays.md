
### 1. Estrutura de dados unidimensionais

**Vetores**:
- Estruturas de dados unidimensionais
- Indice unico controla as posicoes
- Sintaxa de declaracao:
  `<tipo> <nome> [<Tamanho>]`

---
### 2. Vetores em memoria

A memoria do computador e organizada da seguinte forma:
![](MemoriaVetor.png)

---
### 3. Manipulando Vetores

Acesso a uma posicao:
- Nao e possivel acessar um vetor todos;
- Sintaxe:
     `<nome> [<indice>]`

Lista de inicializacao: preenche um vetor todo, de uma vez so
`<tipo> <nome> [<tam.> = {<v1>, <v2>, ..., <vN>}`

---
### 4. Exemplo de implementacao:

```
int main(){
	int v[5]; # Declarou um vetor de inteiros do tamanho 5

	float m;
	
	v[0] = 50; # Coloca o valor 50 no indice 0 do vetor
	v[1] = 40; # Coloca o valor 40 no indice 1 do vetor
	v[2] = 30; # Coloca o valor 30 no indice 2 do vetor
	v[3] = 20; # Coloca o valor 20 no indice 3 do vetor
	v[4] = 10; # Coloca o valor 10 no indice 4 do vetor

	m = (v[0] + v[1] + v[2] + v[3] + v[4]) / 5;
	# Pega os valores dentro do vetor soma e divide por 5;

	printf("Resultado: %f\n", m);
}
```

```
int main(){
	int v[5] = {10, 20, 30, 40, 50}; # Declara e vetor e ja colocar valores inciais
	int i;
	float s = 0;

	for(i=0;i<5;i++){ # Usa o laco for para percorrer o vetor
		s += v[i]; 
	}

	printf("Resultado: %f\n", s/5);
}
```

---
### 5. Extrapolando o tamanho do vetor

Cuidado, pois a linguagem C e permissiva com relacao aos indices de um vetor

| 0   | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
|     |     |     |     |     |
Se o progama tentar acessar indices que nao estam declarados pelo vetor, nao vai retornar um erro de compilacao so que gerara erros futuros, como o erro na impressao desses valores fora do vetor.