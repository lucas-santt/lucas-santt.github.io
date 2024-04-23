---
layout: post
title:  "Criação de um ambiente para o desenvolvimento de um kernel"
date:   2024-04-20 19:48:32 -0300
categories: IME-USP MAC0470-Software_Livre
---
Para o desenvolvimento de qualquer kernel, é importante criar um ambiente para evitar possíveis defeitos permanentes no seu computador. Desse modo, tive que criar um ambiente estável para realizar projetos da disciplina de Desenvolvimento de Software (MAC0470) que envolvem o desenvolvimento do kernel linux.

## Tutorias do FLUSP

Utilizei como base os tutoriais elaborados pelo Rodrigo Siqueira no site do Flusp para [criar a máquiva virtual][qemu-kernel], [compilar e instalar o kernel linux][compilar-kernel] e [entender e instalar módulos][entender-modulos].

Embora tenha encontrado vários problemas e erros ao longo do caminho, os tutoriais foram de grande ajuda para o entendimento dos passos realizados pois explicam cada tópico com bastante clareza.

## Criando a máquina virtual

Como essa parte incial é a mais simples, quase não tive erros graves ou difíceis de se resolver.

#### Criando a imagem e bootando a VM

Para a criação da máquina virtual, utilizei o qemu para emular e gerenciar a imagem da vm.

Inicialmente, criei uma imagem de 15G e formato qcow2 e tentei instalar Debian Linux, porém a instalação e boot do Debian demorou mais do que eu esperava e não consegui realizar em um tempo razoável.

Desse modo, desisti de instalar o debian e baixei a ISO do linux Ubuntu 22.04, conseguindo instalar e bootar de maneira mais rápida e prática do que o Debian

#### Configurando a chave SSH

Para facilitar o uso da VM, podemos logar e deslogar da VM utilizando apenas a senha do seu usuário principal. Assim, apenas tive que criar uma chave RSA na máquina host e permitir que a VM aceite conexões ssh via o pacote `openssh`.

Após isso, consegui acessar o shell da VM via o shell da máquina host com um comando apenas.

#### Diretórios compartilhados

Outra funcionalidade importante de se ter em uma máquina virtual é o compartilhamento de diretórios entre a máquina host e a virtual.

Para criar um diretório compartilhado, tive que instalar o pacote `samba cifs-utils`, alterar o arquivo `/etc/fstab` para implementar o caminho do diretórios e criar uma arquivo `.cifs` que armazena o login do usuário da vm.

O único problema que tive foi alterar o arquivo `fstab`devido às suas restritas permissões, porém não foi nada difícil de arrumar.

Após esse processo, consegui um diretório com arquivos compartilhados entre a VM e a máquina host.

## Instalar e compilar o kernel linux

Para essa etapa, tive que clonar o diretório Torvalds linux

#### Arquivo config

Para compilar o kernel, tive que conseguir um arquivo `.config` direto do diretório `/boot` da VM. Após isso, trouxe o arquivo config para a máquina host via o diretório compartilhado criado anteriormente

Consegui customizar o arquivo .config pelo comando `menuconfig` presente no repositório clonado, apenas alterando o nome do kernel. Assim, basta mover para a compilação do kernel.

Não vou mentir, gastei uma quantia de tempo considerável batendo a cabeça e tentando resolver um erro que não encontrava o comando `menuconfig`, porém bastava estar dentro do diretório git clonado para o shell achar o comando.

#### Compilando!

Após o config estar pronto, basta compilar e instalar o kernel. Na compilação tive que escolher a quantidade de threads focadas na compilação antes de compilar, demorou um pouco mas a compilação deu certo.

Para a instalação eu redobrei a atenção pois é muito fácil fazer um erro fatal, instalei os módulos e rebootei a vm com o novo kernel, parte em que eu fiquei mais tenso. Porém tudo deu certo e meu computador não explodiu

O tutorial ainda fala sobre remover versões antigas do Kernel para organizar e liberar espaço, porém decidi não realizar tal passo.

## Os erros

Durante o passo de conseguir o arquivo config, por algum motivo a VM ficou sem espaço, provavelmente por lixo. Ao invés de eu tentar liberar algum espaço, decidi, por impulso, aumentar o tamanho de armazenamento da imagem pelo comando `virt-resize`, porém tal comando conseguiu praticamente estragar com a imagem e a VM não conseguia mais dar boot.

Eu segui esse erro fatal com outro erro fatal, decidi apagar a imagem e reiniciar o processo todo do zero. Mesmo que eu já sabia os passos que eu deveria fazer até essa parte, consegui atrasar a data de entrega do projeto.

Portanto, aprendi que se deve analisar muito bem os erros que me depara ao invés de realizar decisões fatais diretas antes de se aprofundar no motivo do erro e suas possíveis soluções.

## Conclusão

Mesmo que tenha sido trabalhoso e com bastantes erros frustantes, criar um ambiente para o desenvolvimento do kernel e compilar/instalar um kernel linux foi uma ótima experiência para aprender mais afundo o kernel linux.

Os erros que eu me deparei ao longo dessa jornada me ajudaram a entender mais a fundo os comandos que eu estava realizando e como eles funcionam.

Após essa experiência, me sinto mais confiante e motivado para, além de emular uma VM com mais conhecimento, desenvolver em algumas partes do sistema onde eu tinha medo por serem críticas ou importantes.



[qemu-kernel]: https://flusp.ime.usp.br/kernel/use-qemu-to-play-with-linux/
[compilar-kernel]: https://flusp.ime.usp.br/kernel/Kernel-compilation-and-installation/
[entender-modulos]: https://flusp.ime.usp.br/kernel/play_with_modules/