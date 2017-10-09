---
title: "aaaAzure início rápido - criar Portal de VM do Windows | Microsoft Docs"
description: "Guia de Introdução do Azure - Criar Portal da VM do Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a>Criar uma máquina virtual do Windows com Olá portal do Azure

Máquinas virtuais do Azure podem ser criadas através de Olá portal do Azure. Este método fornece uma interface de utilizador baseada no browser para criar e configurar máquinas virtuais e todos os recursos relacionados. Este passos de início rápido através da criação de uma máquina virtual e instalar um servidor Web num Olá VM.

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="log-in-tooazure"></a>Inicie sessão no tooAzure

Inicie sessão no toohello do portal do Azure em http://portal.azure.com.

## <a name="create-virtual-machine"></a>Criar a máquina virtual

1. Clique em Olá **novo** botão encontrado no canto esquerda superior Olá de Olá portal do Azure.

2. Selecione **Computação** e, em seguida, selecione **Windows Server 2016 Datacenter**. 

3. Introduza as informações da máquina virtual Olá. nome de utilizador Olá e a palavra-passe introduzida aqui é toolog utilizado na máquina virtual de toohello. Quando terminar, clique em **OK**.

    ![Introduza as informações básicas sobre a VM no painel de portal Olá](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. Selecione um tamanho de Olá VM. toosee mais tamanhos, selecione **ver todos os** ou alterar Olá **suportada de tipo de disco** filtro. 

    ![Captura de ecrã que mostra os tamanhos de VM](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. No painel de definições de Olá, mantenha as predefinições de Olá e clique em **OK**.

6. Na página de resumo de Olá, clique em **Ok** implementação da máquina virtual toostart Olá.

7. Olá VM será afixado toohello dashboard do portal do Azure. Depois de concluída a implementação de Olá, o painel de resumo de VM de Olá é aberto automaticamente.


## <a name="connect-toovirtual-machine"></a>Ligue toovirtual máquina

Crie uma máquina de virtual de toohello de ligação de ambiente de trabalho remoto.

1. Clique em Olá **Connect** botão de propriedades da máquina virtual Olá. É criado e transferido um ficheiro do Protocolo do Ambiente de Trabalho Remoto (ficheiro .rdp).

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. tooconnect tooyour VM, abra Olá transferido o ficheiro RDP. Se lhe for solicitado, clique em **Ligar**. No Mac, terá de um cliente RDP como esta [cliente de ambiente de trabalho remoto](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) de Olá Mac App Store.

3. Introduza o nome de utilizador de Olá e a palavra-passe que especificou ao criar a máquina virtual de Olá, em seguida, clique em **Ok**.

4. Poderá receber um aviso de certificado durante o processo de início de sessão Olá. Clique em **Sim** ou **continuar** tooproceed com ligação Olá.


## <a name="install-iis-using-powershell"></a>Instalar o IIS com o PowerShell

Na máquina virtual de Olá, inicie uma sessão do PowerShell e execute Olá os seguintes comandos tooinstall IIS.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Quando terminar, saia da sessão do RDP Olá e devolver propriedades VM Olá Olá portal do Azure.

## <a name="open-port-80-for-web-traffic"></a>Abrir a porta 80 para o tráfego da Web 

Um Grupo de segurança de rede (NSG) protege os tráfegos de entrada e de saída. Quando é criada uma VM de Olá portal do Azure, é criada uma regra de entrada na porta 3389 para ligações RDP. Porque esta VM aloja um servidor Web, uma regra NSG tem toobe criado para a porta 80.

1. Na máquina virtual de Olá, clique no nome de Olá de Olá **grupo de recursos**.
2. Selecione Olá **grupo de segurança de rede**. Olá NSG pode ser identificado utilizando Olá **tipo** coluna. 
3. No menu da esquerda Olá, em definições, clique em **regras de segurança de entrada**.
4. Clique em **Adicionar**.
5. Em **Nome**, escreva **http**. Certifique-se **intervalo de porta** está definido too80 e **ação** estiver definido demasiado**permitir**. 
6. Clique em **OK**.


## <a name="view-hello-iis-welcome-page"></a>Olá vista página de boas-vindas do IIS

Com o IIS instalado e a porta 80 abra tooyour VM, agora pode ser acedido Olá webserver de Olá internet. Abra um browser e introduza o endereço IP público de Olá do Olá VM. endereço IP público Olá pode ser encontrado no painel VM Olá no Olá portal do Azure.

![Site predefinido do IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpar recursos

Quando já não é necessário, elimine o grupo de recursos de Olá, a máquina virtual e todos os recursos relacionados. toodo por isso, selecione o grupo de recursos de Olá a partir do painel da máquina virtual de Olá e clique em **eliminar**.

## <a name="next-steps"></a>Passos seguintes

Neste guia de introdução, implementou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web. toolearn mais informações sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.

> [!div class="nextstepaction"]
> [Tutoriais de máquinas virtuais do Windows do Azure](./tutorial-manage-vm.md)
