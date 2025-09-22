## 1. Conceito

- No universo do desenvolvimento de software, a compreensão clara dos conceitos fundamentais é essencial para navegar pela multiplicidade de abordagens, ciclos de vida, processos e frameworks disponíveis.
![](ConceitosRequisitos.png)

---
### 1.1 Abordagens de Desenvolvimento de Software

- Filosofia geral do Desenvolvimento;
- Valores e principios que orientam como o softaware e desenvolvido;
- Molda a cultura e mentalidade da equipe, determina como as equipes interagem e trabalham juntas, e influenciam todas as praticas, decisoes e metodos utilizados no desenvolvimento;
- Ex: Abordadem **Dirigidas Por Plano, Ageis e Hibridas**

---
### 1.2 Ciclos de Vida de Desenvolvimento de Software

- Fases ou etapas pelas quais um produto de software passa, desde a concepcao ate a sua retirada de operacao.
- Fornece uma estrutura de alto nivel para a organizacao do processo de desenvolvimento.
- A abordagem escolhida direciona o tipo de ciclo de vida que sera adotado.
- Ex: **Sequencial, iterativo e incremental, espiral, agil**

---
### 1.3 Processos de Desenvolvimento de Software

- Sequencia detalhada de passos, atividades e praticas especificas realizadas durante o desenvolvimento de software.
- Cada processo e projetado para se alinhar com a abordagem e o ciclo de vida adotados.
- Detalha como os requisitos sao coletados, como o software e projetado, implementado, testados e mantido.
- Podem ser categorizados em:
	- **Processos abrangentes**: Definem detalhadamente atividades para todas as disciplinas de engenharia de software. EX: Cascata, Modelo V, RUP.
	- **Processos com foco em praticas tecnicas especificas**: Concentam-se em praticas especificas de engenharia, sem cobrir todo o ciclo de vida. EX: XP, FDD.
	- **Processo hibridos/adaptativos**: Combinam elementos de diferentes abordagens para equilibrar estrutura e flexibilidade. EX: DSDM, RAD, Espiral.

---
### 1.4 Frameworks de Gerenciamento

- Fornece umas **estrutura para organizar, planejar e coordenar** o trabalho em projetos de desenvolvimento. 
- Definem papeis, cerimonias, artefatos, regras que facilitam a organizacao do trabalho e a colaboracao da equipe.
- Nao especificam como realizar atividade tecnicas como design, codificacao ou teste.
- Sao frequentemente combinados com processos ou praticas tecnicas especificas para formar uma abordagem completa.
- Sao categorizados em:
	- **Frameworks de gerenciamento agil**: Focados na organizacao e coordenacao do trabalho seguindo principios ageis para equipes individuais. EX: Scrum, Kanban.
	- **Frameworks de escabilidade**: Fornecem estruturas abrangentes para coordenar multiplas equipes ageis em grandes organizacoes, combinando elementos de frameworks de gerenciamento com orientacoes sobre processos tecnicos e praticas organizacionais. EX: SAFe e LeSS.

---
### 1.5 Metodos e Ferramentas

- Sao **tecnicas** especificas utilizadas para realizar uma tarefa dentro de um processo, como programacao em pares ou desenvolvimento orientado a testes(TDD).
- Sao **recursos de software ou hardware** que apoiam os metodos e processos, como sistemas de controle de versao, frameworks de teste ou IDEs.

---
### 1.6 Relacionamento entre os Conceitos

- **A abordagem informa o Ciclo de Vida**, EX: Uma abordagem agil geralmente leva a adocao de um ciclo de vida iterativo e incremental, enquando uma abordagem dirigida por plano tende a favorecer ciclos de vida mais preditivos.
- **Ciclo de Vida Estrutura Processo e Frameworks**, EX: Um ciclo de vida preditivo estabelece fases sequenciais que estruturam os processos como o modelo Cascata, enquanto um ciclo de vida agil defini iteracoes curtas que estruturam a aplicacao de frameworks como o Scrum.
- **Processos Implementam Aspectos Tecnicos**: Os processos de desenvolvimento implementam as atividades técnicas específicas necessárias para criar o software, detalhando como os requisitos são coletados, como o design é realizado, como o código é escrito e testado, e como o sistema é implantado e mantido.
- **Frameworks Organizam e Coordenam o Trabalho**: Os frameworks de gerenciamento fornecem estruturas para organizar equipes, planejar o trabalho, e coordenar a execução das atividades de desenvolvimento.
- **Complementaridade entre Processos e Frameworks**: Processos e frameworks são complementares e frequentemente usados em conjunto. EX: Scrum e XP.
- **Processos e Frameworks Utilizam Métodos e Ferramentas**: Tanto os processos quanto os frameworks utilizam métodos (técnicas específicas) e ferramentas (recursos de software ou hardware) para realizar suas atividades.
- **Retroalimentacao e Evolucao Continua**: Existe uma retroalimentação continua entre todos os níveis conceituais.
- **Adaptabilidade Contextual**: Permeando todos estes relacionamentos, a adaptabilidade contextual representa a capacidade de selecionar e combinar elementos de diferentes abordagens, ciclos de vida, processos, frameworks, métodos e ferramentas conforme as necessidades específicas de cada projeto, considerando fatores como domínio de aplicação, tamanho e distribuição da equipe, criticidade do sistema, e cultura organizacional.

- Em resumo, as abordagens, os ciclos de vida, os processos de desenvolvimento, os frameworks de gerenciamento e os métodos e ferramentas estão intrinsecamente ligados e se influenciam mutuamente, formando a espinha dorsal da maneira como o software será desenvolvido, entregue e mantido. A escolha consciente e a adaptação desses elementos são cruciais para o sucesso de produtos de software.
--- 

### 1.7 Elementos Contextuais de adaptabilidade no Desenvolvimento de Software

#### 1.7.1 Paticularidade de Cada Projeto

- Caracteristicas e condicoes especificas que tornam um projeto de software unico e que influenciam diretamente as decisoes metodologicas.
- Elas incluem:
	- **Escala e Complexidade**: Tamanho do sistema, numero de usuarios esperados, volume de dados e a complexidade das interacoes;
	- **Criticidade e riscos**: Impacto potencial de falhas;
	- **Estabilidade dos requisitos**: Grau em que os requisitos sao conhecidos antecipadamente e a probabilidade de mudancas;
	- **Restricoes do projeto**: Limitacoes de recursos, tecnologias especificas que devem ser utilizadas;
	- **Distribuicao da equipe**: Localizacao geografica dos membros da equipe, comunicacao e colaboracao;
	- **Perfil dos stakeholders**: Nivel de entendimento dos stakeholders, disponibilidade para feedback continuo e familiaridade com processos de desenvolvimento de software.

#### 1.7.2 Dominio de Aplicacao

- Refere-se ao setor ou area especifica para a qual o software esta sendo desenvolvido, com seus requisitos e caracteristicas distintos;
- Aspecto relevantes incluem:
	- **Natureza do dominio**: Caracteristicas especificas de setores como financasl, saude, aeroespacial ou jogos.
	- **Maturidade tecnologica**: Nivel de estabelecimento e estabilidade das tecnologias e padroes no dominio especifico.
	- **Requisitos regulatorios**: Padroes, certificacoes e conformidades especificas do setor.
	- **Expectativas de qualidade**: Atributos de qualidade prioritários como desempenho, segurança, usabilidade, ou confiabilidade, que variam conforme o domínio.
	- **Ciclo de evolução**: Velocidade com que tecnologias e expectativas evoluem no domínio, influenciando a frequência necessária de atualizações e adaptações.
	- **Terminologia e conceitos**: Vocabulario especializado e modelos conceituais especificos que impactam a comunicacao e a modelagem do sistema.

#### 1.7.3 Cultura Organizacional

- Engloba os valores, crencas, comportamentos e praticas compartilhadas que caracterizam uma organizacao e influenciam como o  trabalho e realizado.
- Elementos relevantes incluem:
	- **Estrutura hierárquica**: O grau de hierarquia presente na organização e como as decisões são tomadas (centralizada vs. descentralizada). 
	- **Tolerância a riscos**: A disposição da organização para aceitar incertezas e experimentar novas abordagens ou tecnologias. 
	- **Autonomia das equipes**: O nível de liberdade que as equipes têm para tomar decisões sobre como realizar seu trabalho. 
	- **Maturidade em processos**: A experiência da organização com diferentes metodologias de desenvolvimento e sua capacidade de adaptação. 
	- **Comunicação**: Padrões e canais de comunicação estabelecidos, transparência de informações e abertura ao feedback. 
	- **Orientação a longo prazo**: O equilíbrio entre resultados rápidos e investimentos em qualidade e sustentabilidade a longo prazo. 
	- **Multidisciplinaridade**: A capacidade e disposição para integrar diferentes funções e especialidades em equipes colaborativas.

`A adaptabilidade contextual requer uma compreensao destes tres aspectos e a capacidade de calibrar as abordagens, ciclos de vida e processo para criar um alinhamento otimizado entre a metodologia de desenvolvimento e as realidades especificas do projeto, dominio e organizacao`.