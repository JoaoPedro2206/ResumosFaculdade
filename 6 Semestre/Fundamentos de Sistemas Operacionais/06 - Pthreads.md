#### **1. Motivação: Por que Usar Threads?**

A era de ganhos de desempenho automáticos a cada nova geração de CPUs acabou por volta de 2003, devido a limitações físicas como consumo de energia e dissipação de calor. Em vez de aumentar a velocidade do clock de um único núcleo, a indústria de processadores mudou o paradigma para aumentar o número de núcleos (cores) em um único chip.

Um programa sequencial tradicional só consegue utilizar um desses núcleos, deixando os outros ociosos. Para aproveitar o poder de processamento dos computadores modernos, é necessário escrever software paralelo, e as **threads** são a principal forma de alcançar isso.

**Pthreads** (POSIX Threads) é um padrão (IEEE) que define uma API na linguagem C para criar e sincronizar threads, garantindo que o código seja portável entre diferentes sistemas operacionais.

---

#### **2. Gerenciamento Básico de Threads com Pthreads**

##### **Criação e Término**

- **`pthread_create()`**: É a função usada para criar uma nova thread. Ela recebe quatro argumentos: um ponteiro para a variável que armazenará o ID da thread, atributos (geralmente `NULL`), o nome da função que a thread executará e um argumento para essa função.
- Uma thread pode terminar sua execução de várias maneiras:
    - Chamando `pthread_exit()` explicitamente.
    - Retornando da função principal que foi passada para `pthread_create()`.
    - Sendo cancelada por outra thread.
    - Se qualquer thread do processo chamar `exit()` ou se a função `main()` do programa terminar.

##### **Aguardando o Término de Threads**

- **`pthread_join()`**: Esta função é usada para fazer uma thread esperar pelo término de outra. A thread que chama `pthread_join()` fica bloqueada até que a thread alvo finalize sua execução. Após o retorno bem-sucedido desta função, é garantido que a thread alvo terminou. É o principal mecanismo para a thread principal aguardar a conclusão de suas threads de trabalho.

##### **Passando Argumentos**

- Argumentos podem ser passados para uma thread através do último parâmetro da função `pthread_create()`, que é um `void *`. Uma prática comum é usar uma `struct` para agrupar múltiplos valores e passar um ponteiro para essa `struct`.

---

#### **3. Sincronização em Pthreads**

Para evitar condições de corrida e gerenciar o acesso a recursos compartilhados, Pthreads oferece primitivas de sincronização.

##### **Mutex (Exclusão Mútua)**

- Mutexes são usados para proteger regiões críticas, garantindo que apenas uma thread possa executar um trecho de código por vez.
- **Funções Principais**:
    - **Inicialização**: `pthread_mutex_init()` ou a macro `PTHREAD_MUTEX_INITIALIZER`.
    - **Bloqueio**: `pthread_mutex_lock()` adquire o mutex. Se ele já estiver bloqueado, a thread que fez a chamada fica em espera.
    - **Desbloqueio**: `pthread_mutex_unlock()` libera o mutex, permitindo que outra thread o adquira.
    - **Destruição**: `pthread_mutex_destroy()` libera os recursos associados ao mutex.

##### **Variáveis de Condição**

- Variáveis de condição são usadas para sincronizar threads com base em condições específicas, permitindo que uma thread espere (durma) até que um evento ocorra. Elas devem ser sempre usadas em conjunto com um mutex.
- **Funções Principais**:
    - **`pthread_cond_wait()`**: Libera atomicamente o mutex associado e bloqueia a thread até que a condição seja sinalizada. Ao ser "acordada", a thread re-adquire o mutex antes de continuar.
    - **`pthread_cond_signal()`**: "Acorda" pelo menos uma das threads que estão esperando na variável de condição.
    - **`pthread_cond_broadcast()`**: "Acorda" todas as threads que estão esperando na variável de condição.

- **Uso Correto e _Spurious Wakeups_**: O padrão Pthreads alerta que uma thread pode acordar de um `pthread_cond_wait()` de forma "espúria" (sem ter sido sinalizada). Por isso, a boa prática de programação exige que a chamada a `pthread_cond_wait()` esteja **sempre dentro de um loop `while`** que re-verifica a condição, e não dentro de um `if`.

---

#### **4. Escrevendo Código Seguro para Threads (Thread-Safe)**

Uma função é considerada **thread-safe** se puder ser chamada simultaneamente por múltiplas threads sem causar problemas de concorrência.

- **Problemas Comuns**:
    
    - **Dados Estáticos e Globais**: Funções que usam variáveis estáticas ou globais sem proteção não são seguras. Um exemplo clássico é a função `inet_ntoa`. O acesso a esses dados deve ser protegido por mutexes.
    - **`errno`**: Para evitar conflitos, o padrão Pthreads exige que cada thread tenha sua própria variável `errno`.
    - **Locks de Arquivo**: Locks de arquivo tradicionais operam a nível de processo. Pthreads oferece funções específicas (como `flockfile`) para sincronização de acesso a arquivos por threads.

É fundamental sempre verificar a documentação para saber se uma função é "thread-safe" antes de usá-la em um programa multithread. Por exemplo, a função `signal()` tem comportamento indefinido em programas com múltiplas threads.