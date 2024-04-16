---
layout: post
title: Otimizando Buscas no Active Record com ILIKE, Ignorando Case-Sensitive
---

O `PostgresSQL` tem uma função bem legal chamada `ILIKE`. Funciona como o `LIKE` porém, não é case-sensitive.

```ruby
@post = Post.where('title ILIKE ?', "%#{params['title']}%")
```
