# Lista de Comandos Assembly RISC-V

## 1. Instruções Aritméticas

### Operações com Registradores

- `add rd, rs1, rs2` - Soma: rd = rs1 + rs2
- `sub rd, rs1, rs2` - Subtração: rd = rs1 - rs2
- `mul rd, rs1, rs2` - Multiplicação: rd = rs1 * rs2
- `div rd, rs1, rs2` - Divisão: rd = rs1 / rs2
- `rem rd, rs1, rs2` - Resto da divisão: rd = rs1 % rs2
- `mulh rd, rs1, rs2` - Multiplicação (parte alta)
- `divu rd, rs1, rs2` - Divisão sem sinal
- `remu rd, rs1, rs2` - Resto sem sinal

### Operações com Imediatos

- `addi rd, rs1, imm` - Soma com imediato: rd = rs1 + imm
- `subi rd, rs1, imm` - Subtração com imediato: rd = rs1 - imm

## 2. Instruções Lógicas

### Operações com Registradores

- `and rd, rs1, rs2` - AND lógico: rd = rs1 & rs2
- `or rd, rs1, rs2` - OR lógico: rd = rs1 | rs2
- `xor rd, rs1, rs2` - XOR lógico: rd = rs1 ^ rs2
- `sll rd, rs1, rs2` - Shift left lógico
- `srl rd, rs1, rs2` - Shift right lógico
- `sra rd, rs1, rs2` - Shift right aritmético

### Operações com Imediatos

- `andi rd, rs1, imm` - AND com imediato
- `ori rd, rs1, imm` - OR com imediato
- `xori rd, rs1, imm` - XOR com imediato
- `slli rd, rs1, imm` - Shift left com imediato
- `srli rd, rs1, imm` - Shift right lógico com imediato
- `srai rd, rs1, imm` - Shift right aritmético com imediato

## 3. Instruções de Comparação

### Comparação com Registradores

- `slt rd, rs1, rs2` - Set less than: rd = (rs1 < rs2) ? 1 : 0
- `sltu rd, rs1, rs2` - Set less than unsigned
- `seq rd, rs1, rs2` - Set equal: rd = (rs1 == rs2) ? 1 : 0
- `sne rd, rs1, rs2` - Set not equal: rd = (rs1 != rs2) ? 1 : 0
- `sgt rd, rs1, rs2` - Set greater than: rd = (rs1 > rs2) ? 1 : 0
- `sge rd, rs1, rs2` - Set greater or equal: rd = (rs1 >= rs2) ? 1 : 0

### Comparação com Imediatos

- `slti rd, rs1, imm` - Set less than immediate
- `sltiu rd, rs1, imm` - Set less than immediate unsigned

## 4. Instruções de Desvio (Branch)

### Desvios Condicionais

- `beq rs1, rs2, label` - Branch if equal: se rs1 == rs2
- `bne rs1, rs2, label` - Branch if not equal: se rs1 != rs2
- `blt rs1, rs2, label` - Branch if less than: se rs1 < rs2
- `bge rs1, rs2, label` - Branch if greater or equal: se rs1 >= rs2
- `bltu rs1, rs2, label` - Branch if less than unsigned
- `bgeu rs1, rs2, label` - Branch if greater or equal unsigned
- `bgt rs1, rs2, label` - Branch if greater than: se rs1 > rs2
- `ble rs1, rs2, label` - Branch if less or equal: se rs1 <= rs2

### Desvios com Zero

- `beqz rs1, label` - Branch if equal zero: se rs1 == 0
- `bnez rs1, label` - Branch if not equal zero: se rs1 != 0
- `bltz rs1, label` - Branch if less than zero: se rs1 < 0
- `bgez rs1, label` - Branch if greater or equal zero: se rs1 >= 0
- `bgtz rs1, label` - Branch if greater than zero: se rs1 > 0
- `blez rs1, label` - Branch if less or equal zero: se rs1 <= 0

## 5. Instruções de Salto (Jump)

- `j label` - Jump incondicional para label
- `jal rd, label` - Jump and link: rd = PC+4, PC = label
- `jr rs1` - Jump register: PC = rs1
- `jalr rd, rs1, imm` - Jump and link register: rd = PC+4, PC = rs1 + imm

## 6. Instruções de Carga (Load)

- `lw rd, offset(rs1)` - Load word: rd = mem[rs1 + offset]
- `lh rd, offset(rs1)` - Load halfword (16 bits)
- `lhu rd, offset(rs1)` - Load halfword unsigned
- `lb rd, offset(rs1)` - Load byte (8 bits)
- `lbu rd, offset(rs1)` - Load byte unsigned
- `la rd, label` - Load address: rd = endereço do label
- `li rd, imm` - Load immediate: rd = imm

## 7. Instruções de Armazenamento (Store)

- `sw rs2, offset(rs1)` - Store word: mem[rs1 + offset] = rs2
- `sh rs2, offset(rs1)` - Store halfword
- `sb rs2, offset(rs1)` - Store byte

## 8. Instruções de Movimentação

- `mv rd, rs1` - Move: rd = rs1 (pseudoinstrução para addi rd, rs1, 0)
- `lui rd, imm` - Load upper immediate: rd = imm << 12
- `auipc rd, imm` - Add upper immediate to PC

## 9. Instruções de Sistema

- `ecall` - Environment call (syscall)
- `ebreak` - Environment break (breakpoint)
- `fence` - Memory fence
- `nop` - No operation (pseudoinstrução para addi x0, x0, 0)

## 10. Pseudoinstruções Úteis

- `not rd, rs1` - NOT lógico: rd = ~rs1
- `neg rd, rs1` - Negação: rd = -rs1
- `seqz rd, rs1` - Set equal zero: rd = (rs1 == 0) ? 1 : 0
- `snez rd, rs1` - Set not equal zero: rd = (rs1 != 0) ? 1 : 0
- `sltz rd, rs1` - Set less than zero: rd = (rs1 < 0) ? 1 : 0
- `sgtz rd, rs1` - Set greater than zero: rd = (rs1 > 0) ? 1 : 0

## 11. Registradores RISC-V

### Registradores de Uso Geral

- `x0` (zero) - Sempre zero
- `x1` (ra) - Return address
- `x2` (sp) - Stack pointer
- `x3` (gp) - Global pointer
- `x4` (tp) - Thread pointer
- `x5-x7` (t0-t2) - Temporários
- `x8` (s0/fp) - Saved register / Frame pointer
- `x9` (s1) - Saved register
- `x10-x11` (a0-a1) - Argumentos/valores de retorno
- `x12-x17` (a2-a7) - Argumentos
- `x18-x27` (s2-s11) - Saved registers
- `x28-x31` (t3-t6) - Temporários

## 12. Diretivas de Assembler

### Seções

- `.text` - Seção de código
- `.data` - Seção de dados inicializados
- `.bss` - Seção de dados não inicializados
- `.rodata` - Seção de dados somente leitura

### Declaração de Dados

- `.byte value` - Byte (8 bits)
- `.half value` - Halfword (16 bits)
- `.word value` - Word (32 bits)
- `.string "text"` - String
- `.ascii "text"` - String sem terminador nulo
- `.space n` - Reserva n bytes
- `.align n` - Alinha a n bytes

### Outras Diretivas

- `.globl label` - Torna label global
- `.equ name, value` - Define constante
- `label:` - Define um rótulo

## 13. Syscalls Comuns (Linux RISC-V)

- `a7 = 1` - print_int (a0 = valor)
- `a7 = 4` - print_string (a0 = endereço)
- `a7 = 5` - read_int (retorna em a0)
- `a7 = 8` - read_string (a0 = buffer, a1 = tamanho)
- `a7 = 10` - exit (a0 = código de saída)
- `a7 = 11` - print_char (a0 = caractere)
- `a7 = 12` - read_char (retorna em a0)
- `a7 = 93` - exit (a0 = código de saída)
- `a7 = 64` - write (a0 = fd, a1 = buffer, a2 = count)

## Exemplo de Programa Completo

```assembly
.data
    msg: .string "Hello, RISC-V!\n"
    num: .word 42

.text
.globl _start

_start:
    # Imprimir string
    li a7, 4
    la a0, msg
    ecall
    
    # Carregar e imprimir número
    lw a0, num
    li a7, 1
    ecall
    
    # Sair
    li a7, 10
    ecall
```