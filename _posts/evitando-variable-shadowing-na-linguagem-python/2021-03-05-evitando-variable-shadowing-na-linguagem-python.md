---
layout: post
title: Evitando Variable Shadowing na linguagem Python 🐍
date: 2021-03-05 22:23 -03:00
modified: 2021-03-06 11:34 -03:00
description: Shell adalah sebuah command-line interpreter; program yang berperan sebagai penerjemah perintah yang diinputkan oleh User yang melalui terminal, sehingga perintah tersebut bisa dimengerti oleh si Kernel.
tag: [python dicas]
image: "https://images.unsplash.com/photo-1614680889612-d82e69f49ea2?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=634&q=80"
---

Variable Shadowing (sombreamento de variável) é um problema que ocorre quando há tentativa de *redeclaração* de variáveis em escopos diferentes.

Veja o exemplo a seguir utilizando a linguagem **Python**:

```python
numero = 10

def alterar():
    numero = 20
    print(a) # saída 20

alterar()
print(numero) # saída 10
```

Esse é um pequeno código feito em Python que inicializa a variável `numero` na linha `1` com um valor inicial de `10`. Na linha `4` dentro da nossa função `alterar()` redeclaramos a variável `numero` repassando um novo valor para ela, `20`.

Perceba que o operador `=` em `Python` serve tanto para declarar ou reatribuir valores de  variáveis de forma dinâmica. 

> Como previsto, os valores mostrados são diferentes.

Isso ocorre, porquê a variável `numero` dentro da função `alterar` só é válida enquanto a função estiver sendo executada. A partir do momento que o **Python** termina de executar a função, a variável `numero` que está dentro da função morrerá.

Imagina que isso pode causar bugs em seu programa? 😁😁 

Pois, você faz uma modificação em seu código, achando que está alterando o valor da variável do top level, quando na verdade, está declarando um variável local dentro da função. E o interpretador do `Python` não identifica isso como bug. Pois, essa é uma operação normal.


## Resolvendo

Para resolver este problema, iremos matar a *redeclaração* da variável `numero` dentro da função `alterar`; ao invés disso, passamos ela como parâmetro e devolvemos o novo valor atribuído. Veja:

```python
numero = 10

def alterar(numero):
    numero = 20
    print(numero) # saída 20
    return numero

resultado = alterar(numero)
print(resultado) # saída 20
```

Sinceramente? Eu evito declarar variáveis no escopo global em meu código, a não ser que haja extrema necessidade. Ao invés disso, declararia a variável dentro da função `alterar` e retornaria:

```python
def alterar():
    numero = 20 * 10
    return numero

resultado = alterar()
print(resultado) # saída 200
```

Se preferir, pode matar o uso da variável número **(neste caso específico)** e retornar a operação de uma só vez.

```python
def alterar():
    return  20 * 10

resultado = alterar()
print(resultado) # saída 200
```

Uma outra forma de causar **variable shadowing**, é substituir um comportamento de um objeto já declarado pela linguagem, vejamos o seguinte exemplo:

```python
sum = 4 + 6
print(sum) # 10
```

Até ai não parece nada demais correto? Apenas declaramos uma variável chamada `sum` e delegamos para ela um valor, que é a soma de dois números. OK 😎!

Mas você sabia que a palavra `sum` é reservada pela linguagem python? Não acredita em mim? Então veja o exemplo abaixo:

```python
>>> sum([1,2,3])
6
```

Ou seja, usamos a função `sum` passando uma lista de números que gostariamos de somar. E ela entregou o resultado `6` pra gente. Porém se eu *redeclaro* o objeto `sum`, como no exemplo anterior, onde eu digo que `sum = 4 + 6`. Não será mais possível, utilizar o `sum` como uma função, pois isso me causaria um erro, veja:

```python
>>> sum = 4 + 6
>>> sum([1,2,3])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not callable
>>>
```

Agora que vocês já sabem como lhe dar com problema de **variable shadowing**, fiquem ligados para não cometer esses erros, que podem dá dor de cabeça no futuro. Principalmente, porque são dificeis de debugar e pode te levar algumas horas até você encontrar a falha.