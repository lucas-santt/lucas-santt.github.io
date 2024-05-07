---
layout: post
title:  "Primeira contribuição para o kworkflow"
date:   2024-05-06 21:54:15 -0300
categories: IME-USP MAC0470-Software_Livre
---
Este artigo é uma exploração da minha primeira experiência contribuindo à ferramenta kworkflow, necessária para um projeto na disciplina de Desenvolvimento de Software Livre (MAC0470), realizado em conjunto com Bruno Levi.

## Objetivos do projeto
O objetivo é realizar uma contribuição para a ferramenta kworkflow, necessária para auxilio no desenvolvimento para Linux, com sugestões de contribuições dadas pelos monitores da disciplina.

Meu objetivo pessoal com este projeto continua o mesmo da minha contribuição para o kernel linux, aprender e entender o processo de contribuição para qualquer software livre.

## Contribuição
Na minha primeira contribuição para o kernel linux, editei apenas um bloco de comentário para entender como enviar o patch. Agora, minha dupla e eu decidimos continuar alterar pequenos erros de *coding style*, porém em grande quantidades.

Desse modo, alteramos, em sua maioria, o uso de comandos echo para printf, já que o comando echo não é consistente através de várias plataformas e sistemas.

## Modificação do código

No total, modificamos 4 arquivos corrigindo 10 erros de *coding style*, abaixo mostrarei um exemplo de um comando echo que substituímos para printf:

{% highlight c %}
    -action_parameters=$(echo "$options" | sed 's/.*--//')
{% endhighlight %}

para

{% highlight c %}
    -action_parameters=$(printf "%s\n" "$options" | sed 's/.*--//')
{% endhighlight %}

Alguns dos arquivos alterados:
- `src/kwremote.sh`
- `src/plugins/kernel_install/remote_deploy.h`
- `src/plugins/kernel_install/utils.sh`

## Finalização

Enviamos o patch via `git send-email` para os monitores da disciplina para uma eventual revisão. Conseguimos juntar todos patchs em apenas um e-mail com todas as suas informações, algo que tivemos dificuldade na nossa contribuição para o kernel linux mas agora já possuímos experiência e conseguimos realizar com mais facilidade
