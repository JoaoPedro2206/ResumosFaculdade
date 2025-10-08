#### **1. O que é um Processo?**

Um processo é a unidade fundamental de execução em um sistema operacional. Ele é mais do que apenas um código; é um **programa em execução**. A principal diferença entre um programa e um processo é que o programa é uma entidade passiva (como uma receita de bolo), enquanto o processo é uma entidade ativa (o ato de fazer o bolo).

Um processo é composto por duas partes principais:

- **Ambiente**: Inclui o espaço de endereçamento, arquivos abertos, processos filhos e sinais.
- **Execução**: Refere-se ao estado do hardware, incluindo o contador de programa (PC), o apontador de pilha e os valores nos registradores da CPU.
- 
Os processos são classificados como **Heavyweight** (processos tradicionais, com alto custo de troca de contexto) e **Lightweight** (threads).

---

#### **2. Ciclo de Vida de um Processo**

**Criação de Processos:** Os processos podem ser criados em quatro momentos principais:

1. **Início do sistema**: Processos de primeiro plano (que interagem com o usuário) e de segundo plano (daemons) são criados.
2. **Chamada de sistema**: Um processo em execução pode criar outro.
3. **Requisição do usuário**: O usuário solicita a execução de um programa.
4. **Início de um job em lote**.

Em sistemas como o **Unix**, a criação ocorre por clonagem, usando a chamada de sistema `fork()`. Já no **Windows**, a função `CreateProcess` é usada para criar e carregar um novo processo. Sistemas Unix organizam processos em uma hierarquia (árvore), o que não ocorre no Windows.

**Término de Processos:** Um processo pode terminar de quatro maneiras:

- **Saída Normal (Voluntária)**: O processo conclui sua tarefa.
- **Saída por Erro (Voluntária)**: O processo encontra um erro que ele mesmo trata e encerra.
- **Erro Fatal (Involuntário)**: O processo causa um erro que não pode ser tratado.
- **Cancelamento por outro processo (Involuntário)**.

---

#### **3. Estados de um Processo**

Um processo pode estar em um dos três estados principais:

1. **Rodando (Running)**: O processo está atualmente utilizando a CPU.
2. **Pronto (Ready)**: O processo está apto a executar, mas aguarda a sua vez de usar a CPU.
3. **Bloqueado (Blocked)**: O processo está esperando por um evento externo, como uma operação de entrada/saída (E/S) ou um sinal, e não pode executar mesmo que a CPU esteja livre.

As transições entre os estados ocorrem da seguinte forma:

- Um processo **rodando** passa para **bloqueado** ao solicitar uma operação de E/S.
- Um processo **bloqueado** passa para **pronto** quando o evento que aguardava ocorre.
- Um processo **rodando** passa para **pronto** quando seu tempo de uso da CPU (quantum) se esgota.
- Um processo **pronto** passa para **rodando** quando o escalonador o seleciona para executar.

**Processos CPU-Bound vs. I/O-Bound:**

- **CPU-bound**: Passam a maior parte do tempo executando cálculos, nos estados "rodando" ou "pronto".
- **I/O-bound**: Passam a maior parte do tempo esperando por operações de E/S, no estado "bloqueado".

---

#### **4. Implementação e Escalonamento de Processos**

O Sistema Operacional (SO) gerencia os processos através da **Tabela de Processos** (ou Bloco de Controle de Processo - PCB). Cada entrada na tabela armazena todas as informações de um processo, como seu PID (ID do processo), registradores, estado, prioridade e ponteiros para seus segmentos de memória.

A **troca de contexto** é a operação fundamental da multiprogramação, onde o SO salva o estado de um processo e carrega o de outro, permitindo que múltiplos processos compartilhem uma única CPU.

O **escalonador (scheduler)** é a parte do SO que decide qual processo no estado "pronto" deve ser executado. Ele utiliza um **algoritmo de escalonamento** para tomar essa decisão.

**Tipos de Escalonadores:**

- **Não-Preemptivo**: Uma vez que um processo recebe a CPU, ele a utiliza até terminar ou se bloquear voluntariamente. É simples, mas pode ser monopolizado por um processo longo.
- **Preemptivo**: Um processo executa por um intervalo de tempo (quantum). Se o tempo acabar, o SO o interrompe e passa a CPU para outro processo. É mais justo e usado na maioria dos sistemas modernos.

**Critérios de Escalonamento:** Um bom algoritmo busca balancear os seguintes objetivos, que são muitas vezes conflitantes:

- **Justiça**: Todos os processos têm chance de executar.
- **Eficiência**: Manter a CPU ocupada o máximo de tempo possível.
- **Minimizar o tempo de resposta**: Para usuários interativos.
- **Minimizar o turnaround**: Tempo total desde a criação até o término do processo.
- **Maximizar o throughput**: Número de tarefas concluídas por unidade de tempo.

---

#### **5. Algoritmos de Escalonamento Clássicos**

1. **First-Come, First-Served (FCFS)**:

	- **Como funciona**: Os processos são executados na ordem em que chegam. É um algoritmo não-preemptivo.
    - **Vantagens**: Simples de implementar.
    - **Desvantagens**: Um processo longo (CPU-bound) pode atrasar todos os outros, resultando em um tempo médio de espera alto.
2. **Round-Robin (RR)**:
    
    - **Como funciona**: Um algoritmo preemptivo onde cada processo recebe um pequeno intervalo de tempo (quantum) para rodar. Se não terminar, volta para o final da fila de prontos.
    - **Vantagens**: É justo, garantindo que todos os processos recebam atenção da CPU.
    - **Desvantagens**: A escolha do quantum é crítica. Um quantum muito grande se assemelha ao FCFS, e um muito pequeno aumenta a sobrecarga com trocas de contexto.
    
3. **Escalonamento por Prioridades**:
    
    - **Como funciona**: Cada processo tem uma prioridade, e o escalonador sempre escolhe o processo de maior prioridade para executar.
    - **Tipos**: As prioridades podem ser **estáticas** (fixas) ou **dinâmicas** (ajustadas pelo SO com base no comportamento do processo, como favorecer processos I/O-bound).
    
4. **Shortest Job First (SJF)**:
    
    - **Como funciona**: O escalonador seleciona o processo que tem o menor tempo de execução estimado.
    - **Vantagens**: É ótimo para minimizar o tempo de turnaround médio, ideal para sistemas de lote (batch).
    - **Desvantagens**: O principal desafio é saber o tempo de execução de um processo antes de ele começar, o que na prática é muito difícil de prever.