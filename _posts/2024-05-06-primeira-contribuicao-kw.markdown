---
layout: post
title:  "Primeira contribuição para o kworkflow"
date:   2024-05-06 20:21:03 -0300
categories: IME-USP MAC0470-Software_Livre
---
Este artigo é uma exploração da minha primeira experiência contribuindo à ferramenta kworkflow, necessária para um projeto na disciplina de Desenvolvimento de Software Livre (MAC0470), realizado em conjunto com Bruno Levi.

## Objetivos do projeto
O objetivo é realizar uma contribuição para a ferramenta kworkflow, necessária para auxílio no desenvolvimento Linux, com sugestões de contribuições dadas pelos monitores da disciplina.

Meu objetivo pessoal com este projeto continua o mesmo da minha contribuição para o kernel linux, aprender e entender o processo de contribuição para qualquer software livre.

## Contribuição
Na minha primeira contribuição para o kernel linux, editei apenas um bloco de comentário para entender como enviar o patch. Agora, minha dupla e eu decidimos continuar alterar pequenos erros de *coding style*, porém em grande quantidades.

Desse modo, documentamos as funções que podem possívelmente retornar erros, comentando esses erros para maior clareza no entendimento do código, sempre seguindo o padrão de código errno.

## Modificação do código

No total, modificamos 16 arquivos e documentamos 19 erros, abaixo mostrarei um exemplo de um erro que documentamos no arquivo `setup.sh`:

{% highlight c %}
    else
        warning "setup could not find $config_file_template"
        return 2
    fi
{% endhighlight %}

para

{% highlight c %}
    else
        warning "setup could not find $config_file_template"
        return 2 # ENOENT
    fi
{% endhighlight %}

Alguns dos arquivos alterados:
- `kw`
- `src/lib/kwlib.sh`
- `src/lib/remotre.sh`
- `src/pomodoro.sh`

## Finalização

Como o kworkflow utiliza um repositório do github para as contribuições, demos um [pull request][pull-request] no repositório para garantir a contribuição.

[pull-request]: https://github.com/kworkflow/kworkflow/pull/1112
