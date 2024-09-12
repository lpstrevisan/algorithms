# Teorema Fundamental das Rotações

## EN

The *Fundamental Theorem of Rotations* states that a BST `S` can be transformed into a BST `T`, with the same values, through an appropriate number of rotations. This can be verified through the following procedure:

Step 1.  Transform `S` into a "left spine" `E`, which means a BST where no node has a right child.

Step 2. Transform `E` into `T`.

The step 1 is achieved by performing left rotations on the root of the tree until it no longer has a right child. Once this occurs, repeat the process on the left subtree, and so on, until we have a tree with only a left spine.

The diagram below illustrates this step. The nodes where left rotations occur are marked with a \*.
```
S =    3*              5*            6             6     E =   6    
     /   \           /   \          /             /           /
    1     5         3     6        5             5           5
     \   / \       / \            /             /           /
      2 4   6     1   4          3*            4           4
                   \            / \           /           /
                    2          1   4         3           3    
                                \           /           /
                                 2         1*          2
                                            \         /
                                             2       1
```

In Step 2, we initially perform *right* rotations at the root of the spine `E` until it has the same value at the root as `T`. At this point, the left and right subtrees of the root of `E` also have the same values as the respective left and right subtrees of the root of `T`. Moreover, the left subtree of the root of `E` is a left spine and therefore the same procedure from Step 2 can be applied to this subtree to transform it into the left subtree of the root of `T`. On the other hand, the right subtree of the root of `E` is a right spine, and therefore, initially, Step 2 cannot be applied directly. However, we can easily modify this Step to apply equally to a right spine. We simply need to perform right or left rotations at the root of `E`, depending on whether it is a left or right spine, respectively, until the root has the same value as the root of `T`. Then, we solve the problem recursively using the same algorithm on the left and right sides of the root.

For example, consider converting the above spine into the BST `T` as follows.
```
         4 
T =    /   \
      2     6
     /\    /
    1  3  5
```

Performing two right rotations at the root of `E`, we will have
```
        4   
      /   \
     3     5
    /       \
   2         6 
  /
 1
```

Next, we need to transform the left subtree by performing a right rotation at the node `3`, resulting in
```
        4   
      /   \
     2     5
    / \     \
   1   3     6 
```

Finally, we need to perform a left rotation at the root of the right subtree (`5`), resulting in the target tree.

### Input Specification

The input consists of several cases, each corresponding to a pair of BSTs, S (source) and T (target), in the following format:
```
N
S[0] S[1] ... S[N-1]
T[0] T[1] ... T[N-1]
//blank line
```

where

*   `N` is the number of vertices in the trees, with values ranging from `0..N-1`.
*   Tree `S` is the BST resulting from the successive insertion of the values `S[0]..S[N-1]` in that order.
*   Tree `T` is the BST where the nodes are enumerated in *pre-order* as `T[0] T[1] ... T[N-1]`.


### Output Specification

For each case in the input, a corresponding output should be printed in the form:
```
L R
T[0] T[1] ... T[N-1]
A
//blank line
``` 
where

*   L and R correspond to the numbers of left and right rotations, respectively, needed to transform L into R according to the algorithm described above
*   T[0] T[1] ... T[N-1] corresponds to the enumeration of the nodes of the BST T in *post-order*
*   A is a boolean "true" or "false" indicating whether the BST T is an AVL.

## PT-BR

O *Teorema Fundamental das Rotações* propõe que uma BST `S` pode ser transformada numa BST `T`, com os mesmos valores, apenas através de uma quantidade apropriada de rotações. Isso pode ser verificado através do procedimento a seguir.

Etapa 1. Transforma `S` numa "espinha à esquerda" `E`, ou seja, uma BST sem nenhum nó à direita do seu pai. Etapa 2. Transforma `E` em `T`

A Etapa 1 é realizada efetuando-se rotações à esquerda na raiz na árvore até que ela não tenha mais filho à direita. Assim que isso ocorrer, repete-se o processo na subárvore à esquerda, e assim sucessivamente que tenhamos apenas um ramo à esquerda.

O diagrama abaixo ilustra essa Etapa. Os nós nos quais ocorrem as rotações à esquerda são sinalizados por um \*.
```
S =    3*              5*            6             6     E =   6    
     /   \           /   \          /             /           /
    1     5         3     6        5             5           5
     \   / \       / \            /             /           /
      2 4   6     1   4          3*            4           4
                   \            / \           /           /
                    2          1   4         3           3    
                                \           /           /
                                 2         1*          2
                                            \         /
                                             2       1
```

Na Etapa 2, inicialmente efetuamos rotações à *direita* na raiz da espinha `E` até que ela tenha o mesmo valor na raiz que `T`. Nesse momento, as subárvores à esquerda e à direita da raiz de `E` também possuem os mesmos valores que as respectivas subárvores à esquerda e à direita da raiz de `T`. Mais ainda, a subárvore à esquerda da raiz de `E` é uma espinha à esquerda e, portanto, o mesmo procedimento da Etapa 2 pode ser aplicado a essa subárvore para transformá-la na subàrvore à esquerda da raiz de `T`. Já a subárvore à direita da raiz de `E` é uma espinha à direita, e portanto, a princípio, a Etapa 2 não pode ser aplicada diretamente. Porém, podemos modificar facilmente essa Etapa para se aplicar igualmente a uma espinha à direita. Basta que, incialmente, efetuemos rotações à direita ou à esquerda na raiz de `E`, conforme ela seja uma espinha à esquerda ou à direita, respectivamente, até que a raiz tenha o mesmo valor que a raiz de `T`. Em seguida, resolvemos o problema recursivamente pelo mesmo algoritmo à esquerda e à direita da raiz.

Por exemplo, considere a conversão da espinha acima na BST `T` a seguir.
```
         4 
T =    /   \
      2     6
     /\    /
    1  3  5
```  

Efetuando duas rotações à direita na raiz de `E`, teremos
```
        4   
      /   \
     3     5
    /       \
   2         6 
  /
 1
```  

Em seguida, precisamos transformar a subárvore à esquerda efetuando uma rotação à direita no nó `3`, obtendo
```
        4   
      /   \
     2     5
    / \     \
   1   3     6 
```

Finalmente, precisamos de uma rotação à esquerda na raiz da subárvore à direita (`5`), obtendo a árvore destino.

### Especificação da Entrada

A entrada consiste de vários casos, cada um correspondente a um par de BSTs S (source) e T (target) na forma
```
N
S[0] S[1] ... S[N-1]
T[0] T[1] ... T[N-1]
//linha em branco
```  

onde

*   `N` é o número de vértices das árvores, com valores `0..N-1`
*   A Árvore `S` é a BST resultante da inserção sucessiva dos valores `S[0]..S[N-1]` nessa ordem
*   B é a BST cujos nós enumerados em *pré-ordem* são `T[0] T[1] ... T[N-1]`

### Especificação da Saída

Para cada caso da entrada, deve ser impressa uma saída correspondente na forma
```
L R
T[0] T[1] ... T[N-1]
A
//linha em branco
```  

onde

*   `L` e `R` correspondem aos números de rotações à esquerda e à direita, respectivamente, necessárias para transformar `L` em `R` de acordo com o algoritmo descrito acima
*   `T[0] T[1] ... T[N-1]` corresponde à enumeração dos nós da BST `T` em *pós-ordem*
*   A é um booleano "true" ou "false" que indica se a BST `T` é uma AVL.