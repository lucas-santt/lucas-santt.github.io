---
layout: post
title:  "Segunda contribuição para o kworkflow"
date:   2024-06-26 21:56:55 -0300
categories: IME-USP MAC0470-Software_Livre
published: false
---
Este artigo é uma exploração da minha experiência contribuindo ao [kworflow][kw-git], necessária para um projeto na disciplina de [Desenvolvimento de Software Livre (MAC0470)][MAC0470], realizado em conjunto com [Bruno Levi][bruno-blog].

Após a minha [primeira contribuição para o kworkflow (kw)][first-kw-post], ainda queria realizar mais contribuições. Agora, demos uma olhada nos issues abertos dentro do repositório git do kw e decidimos resolver o [issue #1014][issue-1014].
 
## Problema a resolver
Quando rodamos testes para o kw, a própria ferramenta cria imagens de containers para realizar os testes. Porém, como podem ser um pouco pesadas (podem ocupar alguns gigas), é de bom gosto avisar o usuário as imagens criadas e o seu espaço ocupado.

Essa foi a sugestão dada por [João Paulo][jppaulo06-git] e por [Rodrigo Siqueira][siqueira-git] no [issue][issue-1014] e, desse modo, realizamos a correção do código para avisar o usuário.

## Contribuição
Como é um erro simples, tivemos apenas que alterar o arquivo de testes de integração (`tests/integration/utils.sh`), adicionando uma verificação do tamanho e o id do container criado, as modificações do código estão disponíveis no nosso [commit][pr-commit].

## Conclusão

Depois alterar o código, realizamos um [pull request][pull-request], que foi aceito após alguns dias.

[kw-git]: https://github.com/kworkflow/kworkflow
[MAC0470]: https://uspdigital.usp.br/jupiterweb/obterDisciplina?nomdis=&sgldis=MAC0470
[bruno-blog]: https://brunorlevi.github.io/
[first-kw-post]: https://luccaaxx.github.io/posts/primeira-contribuicao-software-livre/
[issue-1014]: https://github.com/kworkflow/kworkflow/issues/1014
[jppaulo06-git]: https://github.com/jppaulo06
[siqueira-git]: https://github.com/rodrigosiqueira
[pr-commit]: https://github.com/BrunoRLevi/kworkflow/commit/cf35f113b0ee1b604a13e31d5a7211f36b7dbf2b
[pull-request]: https://github.com/kworkflow/kworkflow/pull/1112
