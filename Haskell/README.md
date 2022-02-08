## Grupo:
Gabriel da Silva Cardoso - 20100524

Julio Gonçalves Ramos - 19203165

## Links:
Repositório Git com o código: https://github.com/Cardoz-0/Suguru-Solver

Apresentação: https://youtu.be/UKXcL7VkfnI

# SUGURU SOLVER

## O problema

Suguru é um quebra cabeça onde o tabuleiro é dividido em grupos ou regiões que devem ser preenchidos com números de acordo com as regras do jogo.

Existem duas regras para como os números podem ser postos no tabuleiro, que é onde a complexidade do puzzle é criada: 
1. um número não pode ser posto nas oito casas em torno de um igual.
2. as regiões devem ser completadas obedecendo a regra acima, com números de 1 a N, onde N é o tamanho da região.

## Solução
Parte da dificuldade de realizar um algoritmo para o resolver sugarus é que vários caminhos para a solução são sem saída e é preciso checar por esses casos e voltar o quanto for necessário para resolver o problema.

Para isso, é utiliado a estratégia de backtracking, assim, várias soluções são testadas em sequência e caso ela não seja adequada, é descartada. Isso é feito até chegar na solução de fato.

## Entrada e saída
A entrada dos tabuleiros de jogo é feita diretamente no código. A função tabuleiro que recebe o tamanho do tabuleiro desejado e retorna um tabuleiro (inserido pelo usuário) em forma de matriz (lista de listas). Espaços vazios são representados pelo número 0.

Também é necessário uma matriz para especificar as regiões do tabuleiro, também inserida pelo usuário. Cada região é representada por um grupo de elementos com o mesmo valor adjacentes um ao outro. Ao contrário do tabuleiro, 0 é utilizado como índice.

Para adicionar um novo puzzle de suguru basta ir em tabuleiros.hs e adicionar as duas matrizes necessárias. A primeira precisa das regiões da matriz, estas são representadas por números. Já a segunda basta adicionar os valores na sua posição na matriz, sendo que o zero significas um valor vazio
```
{-
    region
    Função complementar ao tabuleiro
    Números iguais representam uma mesma região
    Parametros:
        Tamanho do tabuleiro
    Retorno = Matriz de regiões
-}
region::Int -> [[Int]]
region 7 = [
    [0,0,0,0,1,1,1],
    [0,2,2,2,3,1,1],
    [4,2,2,3,3,3,5],
    [4,4,4,6,3,5,5],
    [4,8,6,6,6,5,5],
    [7,8,8,6,9,9,9],
    [7,8,8,9,9,10,10]]

{-
    tabuleiro
    Entrada do programa contendo os números presentes no tabuleiro
    Espaços vazios são representados por zeros
    Parametros:
        Tamanho do tabuleiro desejado
    Retorno = Matriz Tabuleiro
-}
tabuleiro::Int -> [[Int]]
tabuleiro 7 = [
    [3,0,2,0,0,1,2],
    [0,0,0,0,0,0,0],
    [0,0,0,0,0,0,5],
    [0,0,0,0,0,0,1],
    [0,0,0,0,1,0,0],
    [0,0,0,0,0,0,4],
    [0,4,0,0,0,0,0]]
```

![matriz](https://i.imgur.com/xWQDVhM.png)

Para compilar basta rodar :
```
ghc main.hs -o suguru 
```
Para executar:
```
./suguru
```
Após ser executado o programa printa a matriz do tabuleiro resolvido
```
[3,4,2,1,5,1,2]
[5,1,5,3,4,3,4]
[2,4,2,1,5,2,5]
[3,1,5,4,3,4,1]
[4,2,3,2,1,2,3]
[1,5,1,5,3,5,4]
[2,4,3,2,1,2,1]
```

![matriz](https://i.imgur.com/UpMl6af.png)


## Implementação
Uma grande parte do código serve para implementar funções para operar matrizes em Haskell, que não tem suporte nativo para isso.

É gerado um vetor de tamanhos, que contém um número com o tamanho de cada região.

O algoritmo principal primeiro checa se o número esta dentro dos limites da matriz e se ele se encaixa como solução.

A partir daí, existem vários casos de teste dependendo da condição do número testado e do tabuleiro, por exemplo:
- Checar nova linha (backtrackingTestNextColumn)
- Checar nova coluna (backtrackingTestNextLine)
- Testar próximo número (backtrackingTestNewNumber)
- Achar próxima posição para tentar um número (backtrackingFindNextPos)
- Validar uma posição proposta (backtrackingValidate)
- Entre outros.

## Separação de tarefas
As tarefas do trabalho foram separadas entre os integrantes do grupo:
Um dos integrantes ficou com a documentação, a modularização, a implementação das funções de matrizes.
O outro trabalhou com os algoritmos do suguru em si, incluindo as varias funções do jogo e testagem.
Ao final, os integrantes revisaram o trabalho como um todo em conjunto, proporcionando assim que todos interagissem com todas as partes do trabalho.

## Dificuldades
A maior dificuldade encontrada pelo grupo foi a própria línguagem Haskell. A falta de implementação nativa para operações com matrizes e a síntaxe que para certas situações foi pouco intuitiva e confusa.

Também houve dificuldade para testar as várias situações de jogo, que o algoritmo de backtracking teve que levar em conta na hora de propor uma solução.
