# Pandemia

## EN

A major pandemic is occurring. The Ministry of Health (MH) needs to implement a resource distribution system that aims to prioritize hospitals with the highest number of active cases of the disease.

The proposed system must be able to:

1. Register all existing hospitals in the system;
2. Register new field hospitals in the system;
3. Remove a hospital from the system;
4. Update the number of cases for an existing hospital;
5. Distribute resources.

### Input Specification

The input begins with a line with 1 integer `N` followed by `N` integers on the next line
```
N
C[0] C[1] ... C[N-1]
```

where `N` represents the initial number of registered hospitals and `C[i]` represents the initial number of cases for hospital `i`. Hospitals are identified sequentially by integers `0..N-1`.

This is followed by several events of the form:

* `EW H C`: registers a new hospital with id `H` (sequential) and `C` initial cases.
* `DEL H`: removes the hospital with id `H`.
* `IN H C`: increments the number of cases of hospital `H` by `C` units.
* `OUT H C`: decrements the number of cases of hospital `H` by `C` units.
* `PAY R`: triggers a distribution round of a total `R` resources to the hospitals.

The input ends with a line
```
END
```

A distribution round of an amount `R` in resources occurs as follows:

* The MH assigns one unit of resources at a time, always to the hospital with the highest number of active cases. In case of a tie, the hospital with the highest id has higher priority.
* Each unit of resource is sufficient to attend to one active case. Upon receiving it, the hospital immediately deducts one active case from its total.
* The distribution round ends after all `R` units are assigned or if there are no more hospitals with active cases. In this case, the remaining balance is returned to the MH and allocated to other pandemic control efforts, not carried over to the next round.

### Output Specification

For `NEW H C` and `DEL H` operations, print a line
```
H0 C0
```
where `H0` and `C0` represent, respectively, the ID and number of cases of the hospital with the highest priority at the end of the operation. If there are no hospitals left, print a line
```
-1 -1
```

For `IN H C` and `OUT H C` operations, print a line
```
Cnew
```
where `Cnew` represents the new number of cases for hospital `H` after the operation.

For the `PAY R` operation, print a line
```
P
```
where `P <= R` represents the total resources effectively distributed in that round.

At the end, i.e., after `END`, print a line
```
T
```
where `T` represents the total sum of active cases of all remaining open hospitals.

## PT-BR

Uma grande pandemia está acontecendo. O Ministério da Saúde (MS) precisa implementar um sistema de distribuição de recursos que visa a atender, prioritariamente, os hospitais mais casos ativos da doença.

O sistema proposto deve ser capaz de:

1. Cadastrar todos os hospitais existentes no sistema;
2. Cadastrar novos hospitais de campanha no sistema;
3. Remover um hospital do sistema;
4. Atualizar o número de casos de um hospital existente;
5. Fazer a distribuição de recursos.

### Especificação da Entrada

A entrada começa com uma linha com 1 inteiro `N` seguida de `N` inteiros na linha seguinte
```
N
C[0] C[1] ... C[N-1]
```

onde `N` representa o número inicial de hospitais cadastrados e `C[i]` representa o número inicial de casos do hospital `i`. Os hospitais são identificados sequencialmente por inteiros `0..N-1`.

Seguem-se vários eventos da forma:

* `EW H C`: cadastra de um um novo hospital com id `H` (sequencial) e `C` casos iniciais.
* `DEL H`: remove o hospital com id H.
* `IN H C`: incrementa o número de casos do hospital `H` em `C` unidades.
* `OUT H C`: decrementa o número de casos do hospital `H` em `C` unidades.
* `PAY R`: dispara uma rodada de distribuição de uma quantidade total `R` em recursos para os hospitais.

A entrada termina com uma linha
```
END
```

Uma rodada de distribuição de um valor R em recursos dá-se da seguinte forma:

* O MS atribui uma unidade de recursos por vez, sempre ao hospital com maior número de casos ativos. Em caso de empate, o hospital com maior id tem maior prioridade.
* Cada unidade de recursos é o suficiente para atender um caso ativo. Ao recebê-la, o hospital deduz imediatamente um caso ativo do seu total.
* A rodada de distribuição acaba após todas as R unidades serem atribuídas ou caso não haja mais nenhum hospital com casos ativos. Neste caso, o saldo restante é devolvido ao MS e destinado a outras frentes de combate à pandemia, não sendo acumulado para a próxima rodada.

### Especificação da Saída

Para as operações `NEW H C` e `DEL H` deve ser impressa uma linha
```
H0 C0
```

em que `H0` e `C0` representam, respectivamente o ID e número de casos do hospital com maior prioridade ao término da operação. Caso não haja mais nenhum hospital, deve ser impressa uma linha
```
-1 -1
```

Para as operações `IN H C` e `OUT H C` deve ser impressa uma linha
```
Cnew
```

em que `Cnew` representa o novo número de casos do hospital `H` após a operação.

Para a operação `PAY R` deve ser impressa uma linha
```
P
```

onde `P <= R` representa o total de recursos efetivamente pagos nessa rodada.

Ao final, ou seja, após o `END`, deve ser impressa uma linha
```
T
```

onde `T` representa a soma total dos casos ativos de todos os hospitais ainda abertos juntos.