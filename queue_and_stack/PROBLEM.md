# Modern times

## EN

A production line receives different items to be processed. Each item has a unique identifier `X` (sequential integer 0,1,2...) and a processing time `T` (positive integer), which corresponds to the amount of work required for the item to be fully processed. New items (`X`, `T`) (identifier, processing time) are brought to the line by a **loader** `L` and admitted into an **input queue** `I` (FIFO). The items are then progressively added by a **scheduler** `S` to a **circular work queue** `W` to be processed by a **processor** `P`. After being completely processed, the items are removed from the circular work queue by the scheduler and placed in an **output stack** `O` (LIFO), from where they are finally removed by an **unloader** `U`.

The layout of the production line is illustrated below. Note that the Processor `P` and the Scheduler `S` have access to consecutive positions in the circular queue (which, in the diagram, "rotates" counterclockwise). The scheduler's access point comes immediately after (in the direction of the queue) the processor's access point.

```
                                                                    Processor
                                                                 +-------------+           
                                                                 |      P      |
  Loader                                        Scheduler        +------------ +
+----------+                                    +-------+               |
|    L     |      I: Input Queue (FIFO):        |   S   |               v          
|          | ---> (X15, T15)   (X14, T14) -----------.  |            (X8, T8)  .  (X9, T9)       
+----------+                                    |    '-------.      .                     .  
                                                |       |      (X7, T7)                  (X10, T10)    
+----------+       O: Output Stack (LIFO):       |    .-------'   .         W: Circular         .  
|          | <---------------.  .--------------------'  |       .          Work Queue           .     
|    U     |                 |  |               |       |        .           (CCW)             .  
+----------+                 |  v               +-------+       (X6, T6)                 (X11, T11)     
 Unloader                    (X4)                                   .                       .  
                             (X1)                                    (X13, T13) .  (X12, T12)  
                             (X5)  
                             (X2)  
```

The work of the line occurs in a synchronized manner in **processing cycles** of `K` time units. Each cycle, the following events occur, in this order:

1. The scheduler checks if the item at its access position is fully processed, i.e., if its remaining processing time is zero (see item 3 below). If so, it is removed from the circular work queue `W` and placed in the output stack `O`.

2. The scheduler checks if any new item is present in the input queue `I`. If so, it removes **one** item from the front of the queue `I` and inserts it into the work queue `W` at the access position. That is, this new item will occupy the position immediately after the processor's position (in the direction of `W`).

3. The processor works for `K` time units on the item (`X`,`T`) at its position, after which the remaining processing time `T` is decreased by `K` units (limited to zero). Then, the circular queue "advances" by one position. To illustrate, suppose `T7=0` in the above diagram (item X7 is fully processed). After completing one cycle, we would have the following situation:

```
                                                                    Processor
                                                                 +-------------+           
                                                                 |      P      |
  Loader                                        Scheduler        +------------ +
+----------+                                    +-------+               |
|    L     |      I: Input Queue (FIFO):        |   S   |               v          
|          | --->              (X15, T15) -----------.  |            (X9, T9)  .  (X10, T10)       
+----------+                                    |    '-------.      .                     .  
                                                |       |      (X8, T8'=T8-K)             (X11, T11)    
+----------+       O: Output Stack (LIFO):       |    .-------'   .           W: Circular       .  
|          | <---------------.  .--------------------'  |       .             Work Queue         .     
|    U     |                 |  |               |       |        .              (CCW)           .  
+----------+                 |  v               +-------+       (X14, T14)                 (X12, T12)     
 Unloader                    (X7)                                   .                       .  
                             (X4)                                     (X6, T6) .  (X13, T13)  
                             (X1)  
                             (X5)  
                             (X2)  
```

Between successive cycles, new items can be loaded into `I` and items can be unloaded from stack `O`.

#### Important

If there is nothing in the work queue, the processor does nothing. If there is only one item, that item is processed by `P` and the advancement of the circular queue `W` will place that item back at the processing position. Thus, for example, at the beginning, in the cycle when the first item is placed in `W` (step 2), in the same cycle it is processed for `K` time units (step 3). At the start of the next cycle, only this item will be in `W`. Thus, in step 1, the scheduler will check if it should be removed. If not, it will again be the item processed since, even if a new item is inserted into `W`, it would be "behind" this item.

### Input Specification

The input begins with a line containing an integer
```
K
```
corresponding to the duration of a processing cycle. Then, we have several lines in one of the following forms, each corresponding to an event:

* `LOAD X T` : indicates that a new item with identifier X and remaining processing time T has been loaded into the input queue (initially empty)

* `UNLD` : indicates that an item has been unloaded from the output stack O

* `PROC` : indicates the occurrence of a processing cycle (steps 1-3 described above)

The input ends with a line
```
END
```

### Output Specification

For each `UNLD` line in the input, the program should print a line
```
UNLD X
```
where `X` is the identifier of the item unloaded from the output stack `O`.

For each `PROC`, the program should print a line
```
PROC X T
```
where `X` is the identifier of the item processed in that cycle, and `T` indicates the remaining processing time of the item **at the end** of that cycle (after step 3). If the work queue is empty, it should print `PROC -1 -1`.


## PT-BR

Uma linha de montagem recebe diferentes itens para serem processados. Cada item tem um identificador único `X` (inteiro sequencial 0,1,2...) e um tempo de processamento `T` (inteiro positivo), que corresponde ao tempo de trabalho sobre esse item necessário para que ele esteja completamente pronto. Novos itens (`X`, `T`) (identificador, tempo de processamento) são trazidos à linha por um **carregador** `L` e admitidos numa **fila de entrada** `I` (FIFO). Os itens são então progressivamente adicionados por um **escalonador** `S` a uma **fila de trabalho circular** `W` para serem processados por um **processador** `P`. Após serem completamente processados, os itens são retirados da fila circular de trabalho pelo escalonador e colocados numa **pilha de saída** `O` (LIFO), de onde são finalmente retirados por um **descarregador** `U`.

O layout da linha de montagem está ilustrado a seguir. Repare que o Processador `P` e o Escalonador `S` têm acesso a posições consecutivas da fila circular (que, no diagrama, "roda" no sentido anti-horário). O ponto de acesso do escalonador vem imediatamente após (no sentido da fila) ao ponto de acesso do processador.

```
                                                                    Processor
                                                                 +-------------+           
                                                                 |      P      |
  Loader                                        Scheduler        +------------ +
+----------+                                    +-------+               |
|    L     |      I: Input Queue (FIFO):        |   S   |               v          
|          | ---> (X15, T15)   (X14, T14) -----------.  |            (X8, T8)  .  (X9, T9)       
+----------+                                    |    '-------.      .                     .
                                                |       |      (X7, T7)                  (X10, T10)    
+----------+       O: Ouput Stack (LIFO):       |    .-------'   .         W: Circular         .
|          | <---------------.  .--------------------'  |       .          Work Queue           .     
|    U     |                 |  |               |       |        .           (CCW)             .  
+----------+                 |  v               +-------+       (X6, T6)                 (X11, T11)     
 Unloader                    (X4)                                   .                       . 
                             (X1)                                    (X13, T13) .  (X12, T12)
                             (X5)
                             (X2)  
```

O trabalho da linha ocorre de forma sincronizada em **ciclos de processamento** de `K` unidades de tempo. A cada ciclo, os seguintes eventos ocorrem, nesta ordem:

1. O escalonador verifica se o item na sua posição de acesso está totalmente processado, ou seja, se o seu tempo restante de processamento é zero (ver item 3 abaixo). Em caso positivo, ele é retirado da fila circular de trabalho `W` e colocado na pilha de saída `O`.

2. O escalonador verifica se algum novo item está presente na fila de entrada `I`. Em caso positivo, ele retira **um** item da frente da fila `I` e o insere na fila de trabalho `W` na posição de acesso. Ou seja, esse novo item ocupará a posição imediatamente após a posição do processador (no sentido de `W`)

3. O processador trabalha por `K` unidades de tempo no item (`X`,`T`) da sua posição, após o que o tempo restante de processamento `T` é decrescido de `K` unidades (limitado a zero). Em seguida, a fila circular "avança" uma posição.
Para exemplificar, suponha que `T7=0` no diagrama acima (o item X7 está totalmente processado). Após a execução de um ciclo, teríamos a seguinte situação:

```
                                                                    Processor
                                                                 +-------------+           
                                                                 |      P      |
  Loader                                        Scheduler        +------------ +
+----------+                                    +-------+               |
|    L     |      I: Input Queue (FIFO):        |   S   |               v          
|          | --->              (X15, T15) -----------.  |            (X9, T9)  .  (X10, T10)       
+----------+                                    |    '-------.      .                     .
                                                |       |      (X8, T8'=T8-K)             (X11, T11)    
+----------+       O: Ouput Stack (LIFO):       |    .-------'   .           W: Circular       .
|          | <---------------.  .--------------------'  |       .             Work Queue         .     
|    U     |                 |  |               |       |        .              (CCW)           .  
+----------+                 |  v               +-------+       (X14, T14)                 (X12, T12)     
 Unloader                    (X7)                                   .                       . 
                             (X4)                                     (X6, T6) .  (X13, T13)
                             (X1)
                             (X5)  
                             (X2)
```

Entre dois ciclos sucessivos, novos itens podem ser carregados em `I` assim como itens podem ser descarregados da pilha `O`.

#### Importante

Caso não haja nada na fila de trabalho, o processador não realiza tarefa alguma. Caso haja apenas um item, esse item é processado por `P` e o avanço da fila circular `W` colocará esse item novamente na posição de processamento. Assim, por exemplo, no início, no ciclo em que o primeiro item é colocado em `W` (passo 2), nesse mesmo ciclo ele é processado por `K` unidades de tempo (passo 3). No início do próximo ciclo, apenas esse item estará em `W`. Logo, no passo 1 o escalonador verificará se ele deve ser retirado. Caso negativo, ele será novamente o item processado pois, ainda que um novo item seja inserido em `W`, seria "atrás" desse item.

### Especificação da Entrada

A entrada inicia com uma linha contendo um inteiro
```
K
```
correspondente à duração de um ciclo de processamento. Em seguida, temos várias linhas numa das formas a seguir, cada uma correspondendo a um evento:

* `LOAD X T` : indica que um novo item com identificador X e tempo restante de processamento T foi carregado na fila de entrada (inicialmente vazia)

* `UNLD` : indica que um item foi descarregado da pilha de saída O

* `PROC` : indica a ocorrência de um ciclo de processamento (passos 1-3 descritos acima)

A entrada termina com uma linha
```
END
```

### Especificação da Saída

Para cada linha `UNLD` da entrada, o programa deve imprimir uma linha
```
UNLD X
```

onde `X` é o identificador do item descarregado da pilha de saída `O`.

Para cada linha `PROC`, o programa deve imprimir uma linha
```
PROC X T
```

onde `X` é o identificador do item processado nesse ciclo, e `T` indica o tempo restante de processamento do item **ao final** desse ciclo (após o passo 3). Caso a fila de trabalho esteja vazia, deve ser impresso `PROC -1 -1`.