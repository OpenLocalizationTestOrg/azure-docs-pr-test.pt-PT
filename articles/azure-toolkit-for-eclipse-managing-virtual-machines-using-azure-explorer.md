---
title: "máquinas virtuais de aaaManage utilizando Olá Explorador do Azure para o Eclipse | Microsoft Docs"
description: "Saiba como toomanage as máquinas virtuais do Azure utilizando Olá Explorador do Azure para o Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a>Gerir máquinas virtuais utilizando Olá Explorador do Azure para Eclipse

Olá Explorador do Azure, o que faz parte do Olá Toolkit do Azure para o Eclipse, fornece aos programadores de Java com uma solução fácil de utilizar para gerir máquinas virtuais da conta do Azure a partir da ambiente de desenvolvimento integrado do Olá Eclipse (IDE).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Criar uma máquina virtual no Eclipse

toocreate uma máquina virtual utilizando o Explorador do Azure, de Olá Olá seguintes:

1. Inicie sessão tooyour conta do Azure utilizando Olá [instruções de início de sessão para Olá Toolkit do Azure para o Eclipse].

2. No Olá **Explorador do Azure** ver, expanda Olá **Azure** nó, clique com botão direito **máquinas virtuais**e, em seguida, clique em **criar VM**.

   ![Olá comando Criar VM][CR01]  
   Olá **Criar Nova Máquina Virtual** é aberto o assistente.

3. No Olá **escolha uma subscrição** janela, selecione a sua subscrição e, em seguida, clique em **seguinte**.

   ![Olá, escolha uma janela de subscrição][CR02]

4. No Olá **selecionar uma imagem de Máquina Virtual** janela, introduza Olá seguintes informações:

   * **Localização**: Especifica onde será criada a máquina virtual (por exemplo, *EUA oeste*).

   * **Publicador**: Especifica o publicador de Olá que criou a imagem de Olá utilizará toocreate a máquina virtual (por exemplo, *Microsoft*).

   * **Oferecer**: Especifica a máquina virtual de Olá oferta toouse do publicador selecionado Olá (por exemplo, *JDK*).

   * **SKU**: Especifica Olá stockkeeping unidade (SKU) toouse da oferta selecionado Olá (por exemplo, *JDK_8*).

   * **Versão #**: Especifica a versão de Olá selecionado SKU toouse.

    ![Olá, selecione um período de imagem de Máquina Virtual][CR03]

5. Clique em **Seguinte**.

6. No Olá **definições básicas de Máquina Virtual** janela, introduza Olá seguintes informações:

   * **Nome da máquina virtual**: Especifica o nome de Olá para a nova máquina virtual, que tem de começar com uma letra e conter apenas letras, números e hífenes.

   * **Tamanho**: Especifica o número de Olá de núcleos e tooallocate de memória para a máquina virtual.

   * **Nome de utilizador**: Especifica Olá toocreate de conta de administrador para gerir a sua máquina virtual.

   * **Palavra-passe** e **confirmar**: Especifica Olá palavra-passe da sua conta de administrador.

    ![janela de definições da Máquina Virtual básico Olá][CR04]

7. Clique em **Seguinte**.

8. No Olá **criar nova conta do Storage** janela, introduza Olá seguintes informações:

   * **Grupo de recursos**: Especifica o grupo de recursos de Olá para a máquina virtual. Selecione uma das seguintes opções de Olá:
      * **Criar um novo**: Especifica que pretende toocreate um novo grupo de recursos.
      * **Utilizar existentes**: Especifica que pretende tooselect um grupo de recursos que já está associado a sua conta do Azure.

      ![caixa de diálogo Criar nova conta do Storage Olá][CR05]

   * **Conta de armazenamento**: Especifica Olá toouse de conta de armazenamento para armazenar a máquina virtual. Pode utilizar uma conta de armazenamento existente ou crie uma nova conta.

   * **Rede virtual** e **sub-rede**: Especifica a rede virtual Olá e a sub-rede que a máquina virtual ligará. Pode utilizar uma rede existente e sub-rede ou pode criar uma nova rede e sub-rede. Se selecionar **criar nova**, Olá seguintes da caixa de diálogo é apresentada:

      ![caixa de diálogo Criar nova rede Virtual Olá][CR06]

9. No Olá **recursos associados** janela, introduza Olá seguintes informações:

   * **Endereço IP público**: Especifica um endereço IP de acesso externo para a máquina virtual. Pode escolher toocreate um novo endereço IP ou, se a máquina virtual não tiver um endereço IP público, pode selecionar **(nenhum)**.

   * **Grupo de segurança de rede**: Especifica uma firewall de rede opcional para a máquina virtual. Pode selecionar uma firewall existente ou, se a máquina virtual não utilizará uma firewall de rede, pode selecionar **(nenhum)**.

   * **Conjunto de disponibilidade**: Especifica um opcional conjunto de disponibilidade que a máquina virtual podem pertencer a. Pode selecionar um conjunto de disponibilidade existente ou criar um novo conjunto de disponibilidade ou, se a máquina virtual não irão pertencer tooan conjunto de disponibilidade, pode selecionar **(nenhum)**.

   ![janela de recursos associados Olá][CR07]

9. Clique em **Concluir**.  
  A nova máquina virtual é apresentada na janela de ferramenta Olá Explorador do Azure.

   ![Nova Máquina Virtual][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Reiniciar uma máquina virtual no Eclipse

toorestart uma máquina virtual utilizando Olá Explorador do Azure no Eclipse, Olá seguintes:

1. No Olá **Explorador do Azure** ver, faça duplo clique Olá máquina e, em seguida, selecione **reiniciar**.

   ![Olá comandos de reinício de máquinas virtuais][RE01]

2. Na janela de confirmação de Olá, clique em **Sim**.

   ![janela de confirmação de reinício de Olá][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Encerrar uma máquina virtual no Eclipse

tooshut para baixo de uma máquina virtual em execução utilizando Olá Explorador do Azure no Eclipse, Olá seguintes:

1. No Olá **Explorador do Azure** ver, faça duplo clique Olá máquina e, em seguida, selecione **encerramento**.

   ![Olá comandos de encerramento da máquina virtual][SH01]

2. Na janela de confirmação de Olá, clique em **Sim**.

   ![janela de confirmação de encerramento da máquina virtual de Olá][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Eliminar uma máquina virtual no Eclipse

toodelete uma máquina virtual utilizando Olá Explorador do Azure no Eclipse, Olá seguintes:

1. No Olá **Explorador do Azure** ver, faça duplo clique Olá máquina e, em seguida, selecione **eliminar**.

   ![Olá comando de eliminação da máquina virtual][DE01]

2. Na janela de confirmação de Olá, clique em **Sim**.

   ![janela de confirmação de eliminação da máquina virtual de Olá][DE02]

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre os tamanhos de máquina virtual do Azure e preços, consulte Olá os seguintes recursos:

* Tamanhos de máquina virtual do Azure
  * [Tamanhos de máquinas virtuais do Windows no Azure]
  * [Tamanhos de máquinas virtuais do Linux no Azure]
* Preços de máquina virtual do Azure
  * [Preços de máquina virtual do Windows]
  * [Preços de máquina virtual do Linux]

Para mais informações sobre Olá Toolkits do Azure para Java IDEs, consulte Olá os seguintes recursos:

* [Toolkit do Azure do Eclipse]
  * [Novidades no Olá Toolkit de Azure do Eclipse]
  * [Instalar Olá Toolkit de Azure do Eclipse]
  * [instruções de início de sessão para Olá Toolkit do Azure para o Eclipse]
  * [Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]
* [Azure Toolkit para IntelliJ]
  * [Novidades no Olá Toolkit do Azure para o IntelliJ]
  * [Instalar Olá Toolkit do Azure para o IntelliJ]
  * [Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ]
  * [Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]

Para obter mais informações sobre como utilizar o Azure com Java, consulte [Centro de programadores Java do Azure] e [ferramentas de Java para Visual Studio Team Services].

<!-- URL List -->

[Toolkit do Azure do Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalar Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instruções de início de sessão para Olá Toolkit do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de programadores Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Tamanhos de máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos de máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços de máquina virtual do Windows]: /pricing/details/virtual-machines/windows/
[Preços de máquina virtual do Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
