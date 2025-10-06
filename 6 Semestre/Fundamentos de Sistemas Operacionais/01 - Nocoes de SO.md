Sistema Operacional é um programa ou conjunto de programas.
- Visão Geral de um Sistema Computacional:
![[Pasted image 20251006163342.png]]
**Modo Protegido não é modo administrador ou modo usuário. Ele é ainda mais forte e restrito.**

- **Tanenbaum:** a maioria dos SOs possuem dois modos de operação: modo protegido (kernel) e modo usuário.
- Algumas instruções são utilizadas para controlar o hardware, como instruções de entrada e saída, que fazem modificação no disco rígido, por exemplo.
- No modo usuário, algumas instruções são proibidas de executar( instruções privilegiadas).
---
## Definição:

- O SO é a parte fundamental de software que executa em modo protegido, onde possui acesso a todo hardware e pode executar qualquer instrução que a máquina é capaz de executar.
- Um SO não é executado de forma linear como na maioria das aplicações, como início, meio e fim.
- Suas rotinas são executadas concorrentemente em função de eventos assíncronos(que podem ocorrer a qualquer momento).
---
## Qual a função de um SO

- O SO é o gerenciador de recursos da máquina.
- O SO fornece ao usuário uma visão de sua interface com a máquina.
- Um SO possui duas grandes funções: 
	- Criar para o usuário uma **abstração do hardware**.
	- **Gerenciar os recursos** da máquina.
---
## Máquina Estendida

- O sistema operacional apresenta ao usuario uma maquina estendida, mais simples de programar que a maquina real.
	- Tambem chamada de maquina abstrata, ela é equivalente ao hardware, mas mais simples de manipular.
- Leitura de arquivo em disco.
- *Hardware*: verificar a rotação do HD, posicionar o cabeçote na trilha correta, realizar operação de leitura e escrita, etc.
- Máquina estendida: aceita chamadas
	- `fp = fopen(...)`;
	- `fread(fp,...)`;
- Além disso, existem dezenas de informações que influenciam: sistemas de arquivos(ext4, NTFS).
- Se o programador tivesse que se preocupar com todos esses detalhes, existiriam pouquissimos programas portáteis.
- A função do sistema operacional de máquina estendida esconde tal complexidade do hardware, protegendo programadores e usuários.
---
## Gerenciador de Recursos

- O computador é um conjunto de recursos que serão compartilhados:
	- Físicos: Processadores, memorias, discos, rede, ...
	- Abstratos: processos, arquivos, ...
- O SO deve proteger esses recursos, especialmente em ambientes com múltiplos usuários, de forma que não interfiram uns nos outros.
- Exemplos típicos de gerenciador de recursos:
	- Uso de CPU: um programa pode usar a CPU durante um tempo, porém após um determinado período o SO deve permitir que outro programa execute.
	- Uso de memória: um programa deve ser terminado caso altere uma região de memória que não lhe pertence.
- Para todos recurso, o SO deve:
	- Manter informações sobre o recurso(endereço, estado, etc);
	- Decidir quem pode acessar o recurso;
	- Alocar e liberar o recurso;
- É desejável no gerenciamento de recursos:
	- Ser eficiente, maximizando a utilização de recursos
	- Possuir um tempo de resposta previsível;
---
## História Dos Sistemas Operacionais

- A evolução dos SOs está intimamente ligada à evolução dos computadores e suas principais formas de uso.
- A evolução dos computadores é separada em décadas
	- **Máquina Analítica:** 
		- Foi o primeiro computador digital projetado por Charles Babbage, nunca foi implementados pois ela era puramente mecânica e a tecnologia da epoca não permitia a criação de mecanismos precisos.
	- **Primeira Geração** (1945-1955): 
		- Computadores a válvula. 
		- O primeiro funcional foi criado na Universidade de Iowa com 300 válvulas. 
		- Eram muito primitivos. 
		- Toda programação era feita em codigo de maquina absoluta, ou ligando diretamente circuitos elétricos. 
		- Não havia conceito de linguagem de programação, nem sistemas operacionais.
	- **Segunda Geração** (1955-1965): 
		- Substituição das válvulas por transistores.
		- Diferenciação dos papéis dos projetistas, construtores, operadores, programadores e manutenção.
		- Eram máquinas de grande porte (mainframes) e ficavam isolados em grandes salas climatizadas.
		- Apenas grandes corporações e governos tinham acesso à essas máquinas.
		- Para executar uma tarefa, um programador escrevia o programa em um papel e perfurava cartões.
		- Ele levava os cartões a um operador e então aguardava o resultado(Podia demorar muito).
		- Quando o computador terminava, o operador ia até a impressora e pegava o resultado, armazenando-o em uma das salas para que o programador pudesse pegá-la.
		- Surgiu os sistemas de lote (batch) para economizar recursos e diminuir o tempo.
		- Reunir em um lote de tarefas na sala de entrada e então passa-lo para uma fita magnética. usando um computador pequeno e relativamente barato.
		- A computação real era utilizando um computador mais caro e completo.
		- Essa fita magnética era carregada em um programa que lia a primeira tarefa da fita e então a executava, armazenando a saída em uma segunda fita.
		- O sistema operacional era responsável por ler a tarefa das fitas, executar, e ao término da tarefa ler a próxima tarefa da lista.
		- Dessa forma, as tarefas eram executadas sequencialmente.
		- Esses grandes computadores da segunda Geração foram amplamente utilizados para cálculos científicos e de engenharia.
	- **Terceira Geração** (1965-1980):
		- No inicio da década de 1960, existiam duas linhas de computadores: 
			- Computadores de grande porte, científicos de grande escala, orientados a palavras.
			- Computadores comerciais, orientados a caracteres e impressão de fitas, utilizados por bancos e companhias de seguros.
		- A IBM inovou o mercado com o System/360: uma série de máquinas com software compatíveis.
			- Essas maquinas possuíam uma diferença de preço e desempenho considerável.
			- Todas tinham a mesma arquitetura e conjunto de instrução.
			- A primeira linha utilizou circuitos integrados.
			- O sistema operacional OS/360 funcionava em todos os modelos.
			- Houve um problema para criar software e SOs pois os software tinham que ser compatíveis com todos os modelos, e eram máquinas muito distintas e de diferentes escalas.
		- Os SOs de terceira geração também introduziram um conceito fundamental em todos os sistemas operacionais modernos: a **multiprogramação**.
		- Nessa geração, existia dois processos ativos concorrentemente no sistema operacional.
		- Mas a concorrência era muito primitiva: quando uma tarefa atual fazia uma pausar para esperar uma fita ou outra operação de E/S, a CPU ficava ociosa até o término da E/S.
		- A solução encontrada foi dividir a memória em várias partes, com uma tarefa diferente em cada partição:
			- ![[Pasted image 20251006172613.png]]
			- Enquanto uma tarefa aguardava uma operação de E/S a outra poderia avançar.
			- Para isso, foram necessária modificações no hardware para proteger partições contra transgressões ou bugs das outras.
		- Outro aspecto adicionado a essa geração foi a capacidade de transferir tarefas de cartões para discos.
		- Sempre que uma tarefa sendo executava terminava, o sistema operacional podia carregá-la do disco para memória e executá-la.
		- Essa técnica é chamada de **spooling**.
		- O spooling é uma técnica que permite acesso para dispositivos muito lentos, armazenando temporiamente dados em uma memória secundária.
		- Hoje em dia, essa técnica ainda é utilizada nas impressoras.
		- Surgiu tambem o conceito de **timesharing**: os usuários poderiam compartilhar a CPU e recursos, sendo que cada um deles tinha direito a usar uma fatia de tempo.
		- Sistema MULTICS teve sucesso com essa técnica.
	- **Quarta Geração** (1980-Atual):
		- Desenvolvimento de circuitos em larga escala (LSI);
		- Popularização dos computadores pessoais;
		- IBM entrou no mercado de microcomputadores pessoais;
		- Intel virou grande referência;
		- Surgiu as primeiras interfaces gráficas como o Windows;
		- Surgiram sistemas operacionais de rede e distribuídos, são SOs que estão conscientes da existência de mais de uma máquina.
		- Primeiros Telefones Moveis;
		- A era dos smartphones (computadores portáteis) com iOS e Android classificaram uma nova geração de sistemas operacionais.
		- Melhora nos sistemas operacionais embarcados como o iOS, Android, BlackBerry OS e Symbiam OS.
		- A maioria dos conceitos fundamentais de SO não foram alterados por essa nova geração
---
## Classificações de sistemas operacionais

- Os SOs podem ser classificados em três categorias:
	- Sistemas Monoprogramáveis / Monotarefa;
	- Sistemas Multiprogramáveis / Multitarefa;
	- Sistemas com Múltiplos Processadores;

### Sistemas Monoprogramáveis

- SOs voltados à execução de um único programa;
- Processador, memória, periféricos permanecem dedicados à um único programa;
- Possuem a raiz nos computadores da década de 60;
- Ex: MS-DOS da Microsoft;
- 
