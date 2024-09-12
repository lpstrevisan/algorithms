# Hashify

## EN

A streaming service offers its users unlimited access to music and a variety of services. One of these services allows users to check how much time they have spent listening to any song in their playlist. To track this time, the streaming service uses a table to store the duration and playtime of each song in the playlist, increasing the latter value every time the song is played.

The table is implemented as a closed hashtable, which uses linear probing to handle collisions. The hash function is:
```
H(C, i) = (H0(C) + i) mod M
```

Where

*  `C` is a numeric key calculated from the song name;

*  `M` is the current maximum capacity of the table;

*  `H0` is the initial position calculated for the key `C`;

*  `i` is the insertion attempt number;

The initial position `H0` is calculated using the division heuristic `H0(C) = (C mod M)`.

The key `C` used in the hash function is calculated from the song name as the sum of the ASCII codes of each letter in the name, each multiplied by its respective position.

Example: the song named `S = "abcd"` has the key
```
C = a*0 + b*1 + c*2 + d*3 = 97*0 + 98*1 + 99*2 + 100*3 = 596
```

If the table's load factor reaches 50%, rehashing is necessary, increasing the table size to `2*M + 1`. **This check should be done immediately before each insertion.**

### Input Specification

The input starts with a line indicating the initial size `M` of the hashtable. It is followed by several lines, each containing one of three possible operations:

1.  `ADD s t`: Adds the song named **s** with duration **t** to the table (playlist).

2.  `PLAY s`: Finds the song named **s** in the table and increments its total playtime by its duration.

3.  `TIME s`: Finds the song named **s** in the table and reports its total playtime up to the current moment.

The input ends with a line
```
END
```

### Output Specification

For each `ADD s t` operation, the program should print a line with the name of the song added to the playlist and the position in the table where the song was inserted.

For each `PLAY s` and `TIME s` operation, the program should print a line with the name of the song and its total playtime up to the current moment.

#### Notes

When a song is added to the playlist, it has a total playtime of zero, as it has not been played yet.

## PT-BR

Um serviço de streaming oferece a seus usuários acesso ilimitado a músicas e à uma série de serviços. Um desses serviços permite que o usuário possa consultar quanto tempo ele passou ouvindo qualquer uma das músicas de sua playlist. Para contabilizar esse tempo, esse serviço de streaming utiliza uma tabela para armazenar a duração e o tempo de reprodução de cada uma das músicas da playlist, aumentando esse último valor todas as vezes em que a música for escutada.

A tabela é implementada como uma hashtable fechada, que utiliza sondagem linear para tratar as colisões. Dessa forma, a sua função de dispersão é:

```
H(C, i) = (H0(C) + i) mod M
```

Em que

*  `C` é uma chave numérica calculada a partir do nome da música;

*  `M` é a capacidade máxima atual da tabela;

*  `H0` é a posição inicial calculada para a chave `C`;

*  `i` é o número da tentativa de inserção;

A posição inicial `H0` é calculada a partir da aplicação da heurística da divisão `H0(C) = (C mod M)`.

A chave `C`usada na função de dispersão é calculada a partir do nome da música como o somatório do código ASCII de cada uma das letras desse nome multiplicada pela sua respectiva posição.

Ex.: a música de nome `S = "abcd"` tem chave
```
C = a*0 + b*1 + c*2 + d*3 = 97*0 + 98*1 + 99*2 + 100*3 = 596
```

Caso a taxa de ocupação (fator de carga) da tabela chegue a 50%, é necessário fazer rehashing, aumentando o tamanho da tabela para `2*M + 1`. **Essa verificação deve ser feita imediatamente antes de cada inserção.**

### Especificação da Entrada

A entrada inicia com uma linha indicando o tamanho inicial `M` da hashtable. Em seguida, temos várias linhas, cada uma contendo uma de três tipos possíveis de operação:

1.  `ADD s t`: Adiciona a música de nome **s** com duração **t** à tabela (playlist).

2.  `PLAY s`: Busca a música de nome **s** na tabela e incrementa o tempo total de reprodução de acordo com sua duração.

3.  `TIME s`: Busca a música de nome **s** na tabela e informa o tempo total de reprodução de **s** até o momento atual.

A entrada termina com uma linha
```
END
```

### Especificação da Saída

Para cada operação `ADD s t` o programa deve imprimir uma linha com o nome da música adicionada à playlist e a posição da tabela onde a música ela foi inserida.

Para cada operação `PLAY s` e `TIME s` o programa deve imprimir uma linha com o nome da música e o tempo total de reprodução dela até o momento.

#### Notas

Quando uma música é adicionada à playlist, ela tem tempo total de reprodução nulo, pois ainda não foi reproduzida.