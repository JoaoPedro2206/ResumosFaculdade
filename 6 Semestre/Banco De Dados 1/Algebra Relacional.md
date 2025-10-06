
1 - Liste o código dos Projetos e os dados das Pessoas que estão alocadas a esses Projetos. Para o Projeto aparecer na listagem é necessário ter pelo menos uma Pessoa alocada:
- `π Projeto_Codigo,CPF,Nome,Sexo,Idade,Gerente_CPF(Projeto⨝Aloca⨝Pessoa)`

2 - Liste os dados dos projetos que alocam a Pessoa com CPF = 123:
- `π Projeto_Codigo,Descricao(σCPF = 123 (Pessoa⨝Aloca⨝Projeto))`

3 - Liste o CPF das pessoas que não participam de nenhum projeto:
- `π CPF (Pessoa⟕Aloca) - π CPF (Pessoa⨝Aloca)`

4 - Liste os dados das Pessoas que estão alocadas ao Projeto 3344 ou Projeto 5566
- `π CPF,Nome,Sexo,Idade,Gerente_CPF(σProjeto_Codigo = 3344 ∨ Projeto_Codigo = 5566(Projeto⨝Aloca⨝Pessoa))`

5 - Liste os dados das Pessoas que estão alocadas ao Projeto 3344 e ao Projeto 5566
- `π CPF,Nome,Sexo,Idade,Gerente_CPF(σProjeto_Codigo = 3344(Projeto⨝Aloca⨝Pessoa)) ∩ π CPF,Nome,Sexo,Idade,Gerente_CPF(σProjeto_Codigo = 5566(Projeto⨝Aloca⨝Pessoa))`

6 - Liste os dados das Pessoas que estão alocadas ao Projeto 3344, mas não estão alocadas ao Projeto 5566:
```
π CPF,Nome,Sexo,Idade,Gerente_CPF((σProjeto_Codigo = 3344(Pessoa⨝Aloca⨝Projeto)) - (σProjeto_Codigo = 5566(Pessoa⨝Aloca⨝Projeto)))
```

7 - Liste os dados dos Projetos, de Aloca e das Pessoas que estão alocadas a esses Projetos:

- `πProjeto_Codigo,Descricao,CPF,Nome,Sexo,Idade,Gerente_CPF(Projeto⨝Aloca⨝Pessoa)`
- `Projeto⋈Aloca⋈Pessoa`

8 - Liste a descrição dos Projetos e o nome das Pessoas que estão alocadas a esses Projetos:
- `π Descricao,Nome(Projeto⨝Aloca⨝Pessoa)`

9 - Liste o nome de todas as Pessoas, independente delas estarem alocadas a projetos, e a descrição do projeto a qual está alocada, quando houver:

- `π Nome,Descricao(Pessoa⟕Aloca⟕Projeto)`

10 - Liste o código dos projetos que não tem participantes:
- `π Projeto_Codigo(σCPF = null(Projeto⟕Aloca))`



# Lista 2

1- Encontrar o nome de todos os alunos matriculados em 2024.:
- `π NomeAluno(σ Ano = 2024 (Aluno⨝Matriculas))`

2- Encontrar o nome dos cursos que possuem alunos matriculados em 2024.:
- `π NomeCurso(σ Ano = 2024 (Curso⨝Matriculas))`

3- Encontrar o nome dos cursos que possuem alunos matriculados em 2024 e que são oferecidos pelo departamento de Exatas.
- `π NomeCurso(σ Ano = 2024 ∧ NomeDepto = 'Exatas' (Curso⨝Matriculas⨝Depto))`

4- Encontrar o nome de todos os alunos matriculados no curso de 'Matemática' em 2024.
- `π NomeAluno(σ IdCurso = 101 ∧ Ano=2024 (Aluno⋈Matriculas))`

5 - Encontrar o nome dos cursos que não possuem nenhum aluno matriculado em 2024:
- `π NomeCurso(σ IdAluno = null (Curso⟕Matriculas))`

6 - Encontrar o nome dos alunos que se matricularam tanto em ‘Matemática’ quanto em ‘História’ em 2023:
- `π NomeAluno (((π IdAluno(σ Ano = 2023 (Matriculas) ⨝ σ IdCurso = 101 (Curso))) ∩ (π IdAluno(σ Ano = 2023 (Matriculas) ⨝ σ IdCurso = 103 (Curso)))) ⨝ Aluno)`

7 - Listar o nome dos alunos, o nome de seus cursos matriculados em 2023 e o nome dos departamentos de seus cursos, mesmo aqueles que não se matricularam em nenhum curso em 2023.

- `π NomeAluno,NomeCurso,NomeDepto (Aluno ⟕ π NomeCurso,NomeDepto,IdAluno(Depto ⨝ (Curso ⨝ σ Ano = 2023(Matriculas))))`

8 - Mostrar o nome dos professores e o nome dos departamentos aos quais eles pertencem, incluindo aqueles professores que não pertencem a nenhum departamento.
- `π NomeProf, NomeDepto (Professor ⟕ (Depto))`

9 - Listar o nome de todos os cursos e o nome de seus respectivos alunos matriculados em 2024, incluindo aqueles cursos que não têm alunos matriculados em 2024.
- `π NomeCurso, NomeAluno (Curso ⟕ π IdCurso, NomeAluno(Aluno ⨝ (σ Ano = 2023 (Matriculas))))`

10 - Encontrar cursos sem alunos matriculados em 2024.
- `π NomeCurso(σ IdAluno = null (Curso ⟕ σ Ano = 2023(Matriculas)))`

11 - Verificar se os cursos de 'Matemática' e 'Química' são oferecidos pelo mesmo departamento.
- `π NomeCurso, NomeDepto (σ IdCurso = 101 ∨ IdCurso = 104 (Curso⨝Depto))`