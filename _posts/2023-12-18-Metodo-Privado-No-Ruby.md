---
layout: post
title: 🕵️‍♀️ Método privado no Ruby
---
Em Ruby métodos privados podem ser definidos através do modificador de acesso private.

```ruby
class Dog
  def loud
    barking.upcase
  end

  private

  def barking
    'au au'
  end
end
```

```shell
irb(main):014:0> dog = Dog.new
=> #

irb(main):015:0> dog.barking
(irb):15:in: private method `barking' called for # (NoMethodError)

irb(main):016:0> dog.loud
=> "AU AU"
```

Como esperado, o método privado barking não pode ser acessado através da referência da instância definida. 😌
