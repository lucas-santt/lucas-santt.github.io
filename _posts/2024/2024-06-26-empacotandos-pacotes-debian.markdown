---
layout: post
title:  "Empacotando pacotes para o debian"
date:   2024-06-26 22:32:14 -0300
categories: IME-USP MAC0470-Software_Livre
published: false
---
Este artigo é uma exploração da minha experiência empacotando pacotes para o debian, necessária para um projeto na disciplina de [Desenvolvimento de Software Livre (MAC0470)][MAC0470], realizado em conjunto com [Bruno Levi][bruno-blog].

Ainda no tema de software livre, vamos realizar o empacotamento de bibliotecas em Perl para o debian, seguindo dois tutoriais feitos por Joenio Marques da Costa
 
## Primeiro tutorial - Aprendendo com o Hello World
Para o nosso primeiro empacotamento, seguimos o [primeiro tutorial do Joenio][primeiro-tut], onde empacotamos um pacote HelloWorld de exemplo.

#### Utilizando docker

Como eu não possuo nenhum computador com debian, tive que aprender a utilizar [docker][docker] para """simular""" um sistema operacional debian, foi a minha primeira vez utilizando o docker. Como apenas havia experiência com máquinas virtuais, achava que criar e rodar containers via docker seria tão complicado quando, porém, tendo ajuda de um pequeno tutorial, consegui rodar o container sem nenhum erro e com total entendimento do processo bem rápido.

Assim, fiquei mais motivado para estudar e utilizar mais o docker no futuro

#### Editando o pacote

Apenas tive que alterar as coisas mais simples do pacote, como o ano do copyright e sua licensa, a versão do gerenciador de pacotes e a descrição e sinopse do pacote.

Como era um pacote exemplo, apenas construi o pacote em um `.deb` e testei utilizando o comando `dpkg`.

## Segundo tutorial - Caso real e erros

Agora é hora de empacotar um pacote real que ainda não foi empacotado no debian. Seguindo o [segundo tutorial do Joenio][segundo-tut], escolhi empacotar o pacote [Git::CPAN::Patch][cpan-patch] de acordo com o [debian bug #733922][debian-bug], tal bug sugerido no próprio tutorial.

Esse pacote realiza uma série de comandos para facilitar o processo de pegar qualquer distribuição CPAN, guardar em um repositório git e enviar patches de volta para os mantenedores.

Consegui realizar as modificações necessárias do pacote e fazer os seus respectivos commits de maneira bem simples e sem erros significantes. Porém, após construir o pacote, faltava apenas testa-lo, eu me deparei com o seguinte erro:

```bash
    ERROR: testbed failure: unexpected eof from the testbed
```

Não conseguindo entender o motivo do erro, procurei no google e achei um [caso bem parecido com o meu][docker-bug] e descobri que é um bug que ocorre especificamente quando tentamos rodar testes com `autopkgtest` dentro de um container docker. Desse modo, fiquei impossibilitado de continuar o tutorial pois não conseguia testar o pacote (e eu não vou enviar o pacote sem testa-lo); 

## Conclusão

Embora não tenha conseguido enviar o pacote Git::CPAN::Patch, aprendi muito seguindo os dois tutoriais do Joenio: Consegui entender o processo de gerenciamento de pacotes dos sistemas operacionais/linguagens (apt install aparentemente não é nenhuma magia, como eu acreditava antes) e me motivei o suficiente para me aprofundar no uso de docker, já que achei muita mais fácil do que montar e rodar uma máquina virtual em casos de uso simples.

[MAC0470]: https://uspdigital.usp.br/jupiterweb/obterDisciplina?nomdis=&sgldis=MAC0470
[bruno-blog]: https://brunorlevi.github.io/
[primeiro-tut]: https://joenio.me/tutorial-pacote-debian-parte1/
[docker]: https://www.docker.com/
[segundo-tut]: https://joenio.me/tutorial-pacote-debian-parte2/
[cpan-patch]: https://metacpan.org/pod/Git::CPAN::Patch
[debian-bug]: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=733922
[docker-bug]: https://www.die-welt.net/2023/04/running-autopkgtest-with-docker-inside-docker/