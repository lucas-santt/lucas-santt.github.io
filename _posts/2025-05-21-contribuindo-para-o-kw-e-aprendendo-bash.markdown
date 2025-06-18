---
layout: post
title:  "Contribuindo para o kw e aprendendo bash"
date:   2025-06-18 12:47:44 -0300
categories: IME-USP MAC0470-Software_Livre
---
Como parte da disciplina de [Desenvolvimento de Software Livre (MAC0470)][MAC0470], vou contribuir para o projeto do [kworkflow][kw]. Portanto, tive que escolher uma *issue* para trabalhar e realizar uma contribuição.

# Escolha da primeira *issue*

Para começar, escolhi a [*issue* #1211][*issue*-1211] para trabalhar. Acreditava que não seria muito díficil de resolver, dado que eu já tinha uma ideia da resolução. Porém, embora seja fácil de resolver, testar não seria tão fácil, já que eu teria que rodar `kw deploy` várias vezes na máquina virtual, processo cujo não tinha ideia de como realizar.

Desse modo, fui em busca de outro *issue* que eu conseguia testar localmente. Assim, me deparei com o [*issue* #1212][*issue*-1212], cujo não parecia muito difícil de arrumar. O *issue* se tratava de, quando você utiliza `kw deploy --uninstall`, o kworkflow cria várias imagens *initramfs* inúteis, já que estamos desisntalando o kerne utilizado.

Inicialmente, a *issue* pedia para diminuir o número de imagens criadas, já que o kw criava diversas imagens iguais. Porém, o mantenedor [Rodrigo Siqueira][siqueira] respondeu falando que, na realidade, é desnecessário cria qualquer imagem. Desse modo, eu fiquei com um objetivo claro e fácil de ser resolver, bastava apenas testar.

Como o próprio ploblema diz, para testar o `--uninstall` eu tenho que dar *deploy* no kernel, algo que eu não sabia realizar e o motivo de abandonar a primeira *issue*

# Aprendendo a dar *deploy*

Assim, chamei o monitor da disciplina para pedir uma ajuda e ele realmente explicou tudo passo a passo deixando o processo bem claro. Tive que remontar a mesma máquina virtual que criei ao [preparar o ambiente para contribuição no kernel linux][artigo-ambiente-kernel] e dar um *deploy* remotamente da minha máquina (que vai enviar o comando) para a máquina virtual (vai receber o comando e desinstalar o kernel).

Desse modo, consegui testar o kworkflow com o código modificado por mim mesmo. Após tudo isso, estava na hora de modificar o código para resolver a *issue*

# Botando a mão na massa - modificando o código

Percebi que o kworkflow possuía uma pasta de *plugins* que estava meio "abandonada" com o código meio cru. Fui olhar e percebi que este era o lugar onde eu deveria modificar o código para resolver a *issue*. Desse modo, abri o arquivo *uninstall.sh* dentro da pasta *plugins/kernel_install* e notei que, toda vez que o kw atualiza o *bootloader* (normalmente o *grub*) para atualizar a lista de kernels instalados, ele cria uma cópia *initramfs* da imagem de cada kernel instalado.

Pensei em simplesmente apagar a chamada da função *update_bootloader* de dentro da função de desinstalar, porém não posso fazer isso pois ainda queremos que o bootloader atualize, apenas queremos que ele não crie nenhuma imagem. Então, quase adicionei um parâmetro na função *update_bootloader* do arquivo *src/plugins/kernel_install/bootloader.sh*  para saber se ela deveria ou não criar a imagem.

Foi desse jeito que percebi que a função *update_bootloader* já testava se um parâmetro `@root_file_system` foi passado ou não, caso não tenha sido passado, ela não criava a imagem. Dei uma estudada a mais e percebi que esse parâmetro possuía apenas essa função de apenas ser utilizada para a criação da imagem e, portanto, bastava não passar esse parâmetro para a imagem ser criada e o *bootloader* ainda ser criado.

Dessa forma, modifiquei a seguinte linha:

```bash
update_bootloader "$flag" "$kernel" "$target" "$kernel_image_name" '' "$path_prefix" '' "$force"
```

para:

```bash
update_bootloader "$flag" "$kernel" "$target" "$kernel_image_name" '' '' '' "$force"
```

# Realizando a contriubuição - *pull request*

Portanto, o último passo era dar um commit para a minha branch e abrir um *pull request* no kworkflow citando a *issue* escolhida. Dessa maneira, criei um [*pull request* #1216][pull-request] explicando as mudança e os seus porquês. Decidi nem comentar na *issue*, apenas citá-la no *pull request*.

# Resposta dos mantenedores

Cerca de uma semana e meia depois, o mantenedor [Rodrigo Siqueira][siqueira] me respondeu falando que já havia implementado uma solução para a issue, apenas não tinha dado pull request ainda.
Desse modo, pediu para que eu alterasse o pull request para a seguinte solução dele:

```bash
   # Each distro script should implement update_bootloader
-  if [[ "$update_grub" -gt 0 ]]; then
-    #printf '%s\n' "update_bootloader $kernel $target $flag"
-    update_bootloader "$flag" "$kernel" "$target" "$kernel_image_name" '' "$path_prefix" '' "$force"
-
+  if [[ "$reboot" == '1' ]]; then
     # Reboot
     reboot_machine "$reboot" "$target" "$flag"
   fi
```

Desse modo, não atualizamos o bootloader e adicionamos uma opção apenas para rebootar a máquina

# Conclusão do Pull Request

Após 3 dias da resposta, fui implementar o que ele havia pedido e me deparei com outra mensagem do mesmo mantenedor avisando que já havia implementado em outro pull request que ele estava desenvolvendo, o que era um grande bloco de mudanças, incluindo essa. Portanto, ele fechou o Pull Request, visto que a implementação já teria sido feita na pull request dele.

# O que fazer agora?

Mesmo que não consegui implementar o meu pull request, fiquei feliz com o resultado pois, para implementar tal solução, obtive um aprendizado forte sobre gerenciamento de máquinas virtuais, área que eu possuía um gap de conhecimento.

Agora, fui a procura de outra issue para resolver, ainda no kw, e reparei com a [*issue* #1182][*issue*-1182] que é sobre refatoração e UX, coisas que me interessam para realizar a contribuição.

[MAC0470]: https://uspdigital.usp.br/jupiterweb/obterDisciplina?nomdis=&sgldis=MAC0470
[kw]: https://github.com/kworkflow/kworkflow
[*issue*-1211]: https://github.com/kworkflow/kworkflow/*issue*s/1211
[*issue*-1212]: https://github.com/kworkflow/kworkflow/*issue*s/1212
[siqueira]: https://github.com/rodrigosiqueira
[artigo-ambiente-kernel]: https://lucas-santt.github.io/posts/ambiente-kernel/
[pull-request]: https://github.com/kworkflow/kworkflow/pull/1216
[*issue*-1182]: https://github.com/kworkflow/kworkflow/issues/1182
