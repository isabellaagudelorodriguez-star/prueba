# LMC Simulator en C – Suma de Números con Métricas de Rendimiento

##  Descripción

Este proyecto implementa un simulador del modelo computacional Little Man Computer (LMC) en lenguaje C.

El programa simula el funcionamiento básico de un procesador:

* Ciclo Fetch–Decode–Execute
* Uso de memoria y acumulador
* Instrucciones tipo máquina (ADD, SUB, LDA, STA, BRA, BRZ, OUT, HLT)

Tópicos que incluye:

* Métricas de rendimiento (IPC, throughput)
* Análisis de paralelismo a nivel de instrucciones (ILP)
* Ejecución de un programa que suma números almacenados en memoria

---

## Objetivo

Simular cómo funciona un computador simple a bajo nivel y analizar su rendimiento, usando conceptos vistos en clase:

* Operaciones de ALU
* Control de flujo
* Paralelismo (ILP)
* Medición de desempeño

---

## Estructura del Proyecto

El código se divide en los siguientes bloques:

### 1. Definición de constantes y opcodes

Se definen los códigos de operación del LMC:

* `ADD` → suma
* `SUB` → resta
* `LDA` → carga al acumulador
* `STA` → guarda en memoria
* `BRA` → salto incondicional
* `BRZ` → salto si el acumulador es cero
* `OUT` → salida
* `HLT` → detener ejecución

---

### 2. Estructura del computador (LMC)

```c
typedef struct {
    int memory[100];
    int acc;
    int pc;
    int halted;
} LMC;
```

Representa el estado del sistema:

* memory → memoria principal
* acc → acumulador (registro principal)
* pc → contador de programa
* halted → indica si el programa terminó

---

### 3. Métricas de rendimiento

Se almacenan estadísticas como:

* Número total de instrucciones
* Operaciones ALU
* Accesos a memoria
* Saltos (branches)
* ILP (Instruction-Level Parallelism)
* IPC (Instructions Per Cycle)
* Tiempo de ejecución

---

### 4. Unidad ALU

Funciones que realizan operaciones básicas:

```c
int alu_add(int a, int b);
int alu_sub(int a, int b);
```

Estas simulan la unidad aritmético-lógica del procesador.

---

### 5. Análisis de ILP

Se evalúa si dos instrucciones pueden ejecutarse en paralelo:

```c
ilp_are_independent(instr1, instr2);
```

Si no hay dependencia de datos (RAW), se concluye que se pueden usar simultáneamente.

---

### 6. Ciclo Fetch–Decode–Execute

Funciona como el núcleo de la simulación:

1. Fetch → se obtiene la instrucción desde memoria
2. Decode → se separa opcode y dirección
3. Execute → se ejecuta la operación

Ejemplo:

```text
522 → LDA 22
```

---

### 7. Carga de programa y datos

Funciones auxiliares:

* `load_program()` → carga instrucciones en memoria
* `load_data()` → carga datos (números a sumar)

---

## Programa de ejemplo

El sistema ejecuta un programa que suma una lista de números:

```c
int data[] = {7, 3, 12, 5, 9};
```

### Lógica del programa

```text
SUM = 0
IDX = cantidad de datos

while (IDX != 0):
    SUM = SUM + dato
    IDX = IDX - 1

imprimir SUM
```

---

## Resultado esperado

```text
7 + 3 + 12 + 5 + 9 = 36
```

---

## Métricas calculadas

Al finalizar la ejecución, el programa muestra:

* Total de instrucciones ejecutadas
* Operaciones ALU
* Accesos a memoria
* Saltos
* ILP detectado
* IPC estimado
* Tiempo de ejecución
* Throughput (instrucciones por segundo)

---

## Limitaciones

Debido a las características del LMC:

* No hay direccionamiento indirecto real
* El acceso a datos es simplificado
* No se implementa paralelismo real, solo análisis teórico (ILP)

---

## Requisitos

* Compilador de C (GCC recomendado)

---

## Compilación

En la terminal, ubícate en la carpeta del archivo y ejecuta:

```bash
gcc lmc_simulator.c -o lmc
```

---

## Ejecución

```bash
./lmc
```

En Windows:

```bash
lmc.exe
```

---

## Ejemplo de salida

```text
=== SUMA DE NUMEROS ALEATORIOS (LMC) ===
Datos: 7 3 12 5 9
[OUT] Resultado = 36

--- MÉTRICAS ---
Instrucciones: XX
ALU ops: XX
Mem ops: XX
Branches: XX
ILP slots: XX
IPC: X.XX
Tiempo (ns): XXXXX
```

---

## Conceptos aplicados

* Ciclo de instrucción
* ALU
* Control de flujo
* ILP (Instruction-Level Parallelism)
* IPC (Instructions Per Cycle)

---
