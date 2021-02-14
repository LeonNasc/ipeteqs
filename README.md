ipeteqs
=======

Interpretador da pseudolinguagem PETEQS

A linguagem PETEQS é uma pseudolinguagem utilzada no aprendizado de lógica de programação em algumas faculdades.
Especificamente na UFF. Um problema para os iniciantes é que não há como executar códigos em PETEQS. Até agora...

Este é um interpretador da linguagem que funciona baseado em tradução para uma linguagem real e execução.
Ele é escrito em ruby, tanto o tradutor como a linguagem-destino.

## Ipeteqs em Javascript?

Visando a possibilidade de executar PETEQS em qualquer lugar, ipeteqs foi portado para Javascript. Assim como o interpretador original, ele traduz a linguagem PETEQS para uma linguagem real e a executa, sendo escrito  em Javascript ambos o tradutor e o código traduzido.

Sendo importado em uma página, recebe um string de código PETEQS e retorna a execução deste código.

## A linguagem PETEQS

A linguagem PETEQS todas as operações básicas. Em PETEQS, o operador de atribuição é `<-` :

    a <- 1                  // Atribuição
    a <- 2 + 2              // Soma
    a <- 2 - 1              // Subtração
    a <- a * 20             // Multiplicação
    a <- a mod 5            // Módulo

A exceção é a divisão. PETEQS trabalha normalmente com a divisão de inteiros, onde um número dividido sempre tera seu resultado como um inteiro.

    a <- 20 / 2             // a será 10
    a <- 20/3               // a será 6

Para fazer a divisão com um número real, deve-se incluir o ponto decimal.

    a <- 20.0 / 3           // a será 6.666..

A não ser que seja explicitamente declarado no momento da divisão, IPETEQS não consegue *por agora* determinar o tipo número em tempo de execução, então o código abaixo trabalharia com divisão de inteiros, exceto no caso em que o ponto está incluso na operação.

    a <- 15
    a <- a / 4              // a será 3
    
    b <- 15
    a <- b / 4.0            // b será 3.75

    a <- 15
    b <- 4
    a <- a/b                // a será 3, não é possível determinar tipo em tempo de execução.

IPETEQS possui também desvios condicionais, que atuam nos operadores lógicos `>`(maior que),`>=`(maior que ou igual),`<`(menor que),`<=`(menor que ou igual),`<>`(diferente de),`=`(igual à):

    SE a > 0 ENTÃO
      //Código aqui
    FIM SE

    SE b < 100 ENTÃO
      //Faça algo aqui
    SENÃO
      //Faça outra coisa aqui
    FIM SE  

    SE C = 2 ENTÃO
      imprimaln 'C é 2'
    SENÃO SE C <> 3
      imprimaln 'C não é 3'
    SENÃO
      imprima 'C é qualquer outro número'
    FIM SE

A linguagem também possui duas estruturas de repetição, os laços `para` e os laços `enquanto`, que tem a sintaxe abaixo:

    //Contador de ano novo
    PARA i<-10 ATÉ 1 FAÇA
      imprima i
    FIM PARA

    //De modo geral
    PARA Início ATÉ Final FAÇA
      //Ação
    FIM PARA


    saldo <- 100
    ENQUANTO saldo > 0 FAÇA
      saldo = saldo - 5
    FIM ENQUANTO

    //De modo geral
    ENQUANTO Condição FAÇA
      //Ação
    FIM ENQUANTO

IPETEQS, na implementação atual, estabelece um temporizador para um tempo máximo de execução de um loop. Isto garante que o loop não rode para sempre. Atualmente, este valor é de 30 segundos.

PETEQS também possui procedimentos e funções, que permitem a modularização do código. A diferença entre funções e procedimentos é que funções, assim como na matemática, mapeiam entradas de um conjunto A às saídas em um conjunto B. Procedimentos, por sua vez, não necessariamente retornam valores, mas realizam ações.

    FUNÇÃO É_PAR(entradas: num, saídas: é_impar)
    INÍCIO
       SE num mod 2 <> 0 ENTÃO 
         resultado <- Falso
       SENÃO
         resultado <- Verdadeiro
       FIM SE
    FIM

    PROCEDIMENTO ImprimePares
    INÍCIO
      PARA i<- 0 ATÉ 100 FAÇA
         SE É_PAR(i) ENTÃO
           imprimaln i
         FIM SE
      FIM PARA
    FIM

    ImprimePares()                  //Imprime todos os numeros pares

As funções de entrada e saída básicas de PETEQS são `leia`, `imprima` e `imprimaln`. Que leem a entrada de uma varíavel, imprime uma variavel na tela e imprime uma variavel na tela seguido de um caractere de nova linha, respectivamente. PETEQS também possui vetores, variaveis indexadas.

    //Em vez de fazer assim
    leia gato_1
    leia gato_2
    leia gato_3

    imprima gato_1
    imprima gato_2
    imprima gato_3

    //Com as funções de entrada PETEQS, com o uso de vetores podemos:
    PARA i<1 ATÉ 3 FAÇA
      leia gato[i]
      imprima gato[i]
    FIM PARA
