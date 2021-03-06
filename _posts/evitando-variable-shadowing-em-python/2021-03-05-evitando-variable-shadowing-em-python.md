---
layout: post
title: Evitando Variable Shadowing em Python 🐍
date: 2021-03-05 22:23 +07:00
modified: 2021-03-05 22:23 +07:00
description: Neste tutorial pretendo mostrar como evitar o problema de **variable shadowing**.
tag:
  - python
  - dicas
image: /evitando-variable-shadowing-em-python/shadow.jpg
---

Variable Shadowing (sombreamento de variável) é um problema que as vezes podemos cometer por falta de atenção. Esse problema está ligado a *redeclaração* de variáveis em escopos diferentes.

Veja o exemplo a seguir utilizando a linguagem **Python**:

```python
numero = 10

def alterar():
    numero = 20
    print(a) # saída 20

alterar()
print(numero) # saída 10
```

Esse é um pequeno código em Python que inicializa a variável `numero` na linha `1` com um valor inicial de `10`. Na linha `4` dentro da nossa função `alterar()` redeclaramos a variável `numero` repassando um novo valor para ela, `20`.

Perceba que o operador `=` em `Python` serve tanto para declarar ou reatribuir valores de  variáveis de forma dinâmica. 

> Como previsto, os valores mostrados são diferentes.

Isso ocorre, porquê a variável `numero` dentro da função `alterar` só é válida enquanto a função estiver sendo executada. A partir do momento que o **Python** termina de executar a função, a variável `numero` morre. Isso é o que chamamos de variável que pertence ao escopo de uma função!

Imagina o que isso pode causar de bugs em seu programa? 😁😁 Você está esperando que o interpretador do `Python` identifique e te ajude a eliminar este problema? Pode tirar seu cavalinho 🐴 da chuva ☔, isso não vai acontecer!


## Resolvendo

Para resolver este problema, iremos matar a redeclaração da variável `numero` dentro da função `alterar`, ao invés disso, passamos ela como parâmetro e devolvemos o novo valor atribuído, veja:

```python
numero = 10

def alterar(numero):
    numero = 20
    print(numero) # saída 20
    return numero

resultado = alterar(numero)
print(resultado) # saída 20
```

Sinceramente? Eu evito declarar variáveis no escopo global do meu código, a não ser que haja extrema necessidade. Ao invés disso, eu somente iria declarar a variável dentro da função `alterar` e retornaria o valor declarado:

```python
def alterar():
    numero = 20
    return numero

resultado = alterar(numero)
print(resultado)
```

Com certeza isso iria me livrar de problemas futuros 😎.