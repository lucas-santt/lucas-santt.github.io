---
layout: post
title:  "Primeira contribuição para um software livre"
date:   2024-05-06 20:21:03 -0300
categories: IME-USP MAC0470-Software_Livre
published: false
---
Este artigo é uma exploração da minha primeira experiência contribuindo ao [kworflow][kw-git], necessária para um projeto na disciplina de [Desenvolvimento de Software Livre (MAC0470)][MAC0470], realizado em conjunto com [Bruno Levi][bruno-blog].

Após [contribuir para o kernel linux][kernel-post], queria realizar uma contribuição para um software livre que possuía um ambiente mais familiar. Como o grupo FLUSP, do IME-USP, é bem ativo no desenvolvimento da ferramenta [kworflow (kw)][kw-git], utilizada para o de auxílio no desenvolvimento do kernel linux, decidimos contribuir para essa ferramenta, já que teríamos apenas que utilizar o github, bem mais fácil do que basear a contribuição por emails que nem no kernel linux.

## Objetivos do projeto
O objetivo é realizar uma contribuição simples, dentro das sugestões dadas pelos monitores da disciplina.

Meu objetivo pessoal com este projeto continua o mesmo da minha contribuição para o kernel linux, aprender e entender o processo de contribuição para qualquer software livre.

## Contribuição
Decidimos alterar pequenos erros de *coding style*, porém em grande quantidades.

Desse modo, documentamos as funções que podem possívelmente retornar erros, comentando esses erros para maior clareza no entendimento do código, sempre seguindo o padrão de código errno.

## Modificação do código

No total, modificamos 16 arquivos e documentamos 19 erros, abaixo mostrarei um exemplo de um erro que documentamos no arquivo `setup.sh`:

```bash
    else
        warning "setup could not find $config_file_template"
        return 2
    fi
```

para

```bash
    else
        warning "setup could not find $config_file_template"
        return 2 # ENOENT
    fi
```

Alguns dos arquivos alterados:
- `kw`
- `src/lib/kwlib.sh`
- `src/lib/remotre.sh`
- `src/pomodoro.sh`

Com tudo pronto, enviamos um [pull request][pull-request] para o repositório do kw.

## Conclusão

Após alguns dias e algumas alterações, o nosso pull request finalmente foi [aceito!][pr-commit]

[kw-git]: https://github.com/kworkflow/kworkflow
[MAC0470]: https://uspdigital.usp.br/jupiterweb/obterDisciplina?nomdis=&sgldis=MAC0470
[bruno-blog]: https://brunorlevi.github.io/
[kernel-post]: https://luccaaxx.github.io/posts/primeira-contribuicao-kernel/
[pull-request]: https://github.com/kworkflow/kworkflow/pull/1112
[pr-commit]: https://github.com/kworkflow/kworkflow/pull/1112/commits/74ab399c5f6da35ca222f3ebf59ee72a88cd1c1d
