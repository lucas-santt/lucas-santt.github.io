---
layout: post
title:  "Preparando o ambiente para contribuir para o kernel linux"
date:   2025-04-23 14:20:32 -0300
categories: IME-USP MAC0470-Software_Livre
---
Para contribuir para o kernel linux, é necessário realizar alguns passos anteriores para configurar um ambiente propício para o desenvolvimento kernel Linux. Para isso, obtive ajuda de tutorias realizados pelo [FLUSP (FLOSS at USP)][flusp] onde explicam, de maneira fácil e intuitiva, como preparar esse ambiente dentro do linux debian (ubuntu).

## Objetivo

Desenvolver uma máquina virtual para a aplicação do kernel a ser desenvolvido e testado, utilizando a ferramenta [kworkflow][kw] para facilitar esse desenvolvimento e, por último, aprender e entender o subsistema IIO (Industrial Input/Output) no qual irei contribuir futuramente.

## Criação da Máquina Virtual

O [primeiro tutorial][tutorial-um] que segui for para criar e configurar uma máquina virtual via qemu. Isso é necessário pois não quero explodir a minha máquina testando o kernel desenvolvido nela.

Esse tutorial não foi difícil, apenas fiquei preso ao configurar o ssh pois a máquina virtual não é criada com a biblioteca ssh instalada, porém foi apenas instalar via apt install que o problema foi embora. 

Tenho que admitir que fui barrado algumas partes pois sempre esqueco de desligar a vm e, por isso, não conseguia realizar algumas partes pois a vm estava ativa.

## Desenvolvendo um novo kernel

Após, criar a máquina virtual, segui o [segundo tutorial][tutorial-dois] para criar e bootar um novo kernel na máquina virtual.

Para facilitar o procesos, utilizei a ferramenta [kworkflow][kw] para o desenvolvimento do novo kernel. Apenas para testar, só modifiquei o nome da versão do kernel, adicionando um -VM-LUCAS no final. Após instalar a imagem do kernel na máquina virtual, foi possível visualizar o novo nome do kernel, ou seja, o processo deu certo.

Aproveitando a oprotunidade, segui o [terceiro][tutorial-tres] e o [quarto][tutorial-quatro] tutorial para aprender sobre como os módulos do linux funcionam e como adicionar um novo módulo na imagem do novo kernel que criei. Obviamente utilizei o [kworkflow][kw] para facilitar o processo

[flusp]: https://flusp.ime.usp.br/about/
[kw]: https://kworkflow.org/
[tutorial-um]: https://flusp.ime.usp.br/kernel/qemu-libvirt-setup/
[tutorial-dois]: https://flusp.ime.usp.br/kernel/build-linux-for-arm-kw/
[tutorial-tres]: https://flusp.ime.usp.br/kernel/modules-intro/
[tutorial-quatro]: https://flusp.ime.usp.br/kernel/char-drivers-intro/
[tutorial-cinco]: https://flusp.ime.usp.br/iio/iio-dummy-anatomy/
[tutorial-seis]: https://flusp.ime.usp.br/iio/experiment-one-iio-dummy/