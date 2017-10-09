---
title: aaaCapture uma imagem de uma VM com Linux | Microsoft Docs
description: "Saiba como toocapture uma imagem de uma baseado em Linux máquina virtual do Azure (VM) é criado com o modelo de implementação clássica Olá."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>Como toocapture uma máquina virtual de Linux clássica como uma imagem
> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Saiba como demasiado[executar estes passos, utilizando o modelo do Resource Manager Olá](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este artigo mostra como toocapture clássica do Azure máquinas virtuais (VMS) com o Linux como um toocreate imagem outras máquinas virtuais. Esta imagem inclui o disco do SO Olá e discos de dados ligada toohello VM. Não inclui a configuração de rede, por isso terá de tooconfigure que quando cria Olá outro VM da imagem de Olá.

Arquivos de Azure Olá imagem em **imagens**, juntamente com quaisquer imagens carregar. Para obter mais informações sobre imagens, consulte [sobre imagens de Máquina Virtual no Azure][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Antes de começar
Estes passos partem do princípio de que já criou uma VM do Azure utilizando o modelo de implementação clássica Olá e sistema de operativo Olá configurada, incluindo anexar qualquer discos de dados. Se precisar de toocreate uma VM, leia [como tooCreate uma Máquina Virtual Linux][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Capturar a máquina virtual de Olá
1. [Ligar toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) utilizando um cliente SSH à sua escolha.
2. Na janela SSH Olá, escreva Olá os seguintes comandos. o resultado da Olá `waagent` pode variar devido às ligeiramente dependendo da versão de Olá deste utilitário:

    ```bash
    sudo waagent -deprovision+user
    ```

    Olá comando anterior tentativas de sistema de Olá tooclean e torná-lo adequado para reprovisioning. Esta operação efetua Olá seguintes tarefas:

   * Remove as chaves de anfitrião do SSH (se Provisioning.RegenerateSshHostKeyPair 'y' no ficheiro de configuração de Olá)
   * Limpa configuração nameserver /etc/resolv.conf
   * Remove Olá `root` palavra-passe de utilizador do etc/sombra de volumes (se Provisioning.DeleteRootPassword 'y' no ficheiro de configuração de Olá)
   * Remove as concessões de cliente DHCP em cache
   * Reposições toolocalhost.localdomain de nome de anfitrião
   * Elimina Olá último aprovisionado conta de utilizador (obtida /var/lib/waagent) **e dados associados**.

     > [!NOTE]
     > Desaprovisionamento elimina os ficheiros e dados demasiado "generalize" Olá imagem. Apenas execute este comando numa VM que pretende toocapture como um novo modelo de imagem. Garante dessa imagem Olá é limpa de todas as informações confidenciais ou é adequada para as partes de toothird redistribuição.

3. Tipo **y** toocontinue. Pode adicionar Olá `-force` parâmetro tooavoid este passo de confirmação.
4. Tipo **saída** cliente do tooclose Olá SSH.

   > [!NOTE]
   > Olá restantes passos partem do princípio que já tem [instalado Olá CLI do Azure](../../../cli-install-nodejs.md) no computador cliente. Também pode ser feito Olá todos os seguintes passos no Olá [portal do Azure](http://portal.azure.com).

5. A partir do computador cliente, abra CLI do Azure e o início de sessão tooyour subscrição do Azure. Para obter mais informações, leia o artigo [ligar tooan subscrição do Azure a partir de Olá CLI do Azure](../../../xplat-cli-connect.md).

   > [!NOTE]
   > No portal do Azure Olá, inicie sessão no portal de toohello.

6. Certifique-se de que estejam no modo de gestão do serviço:

    ```azurecli
    azure config mode asm
    ```

7. Encerre Olá VM que já está a ser desaprovisionada. Olá exemplo seguinte encerra Olá VM com o nome `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   Se for necessário, pode ver uma lista Olá todas as VMs criados na sua subscrição através da utilização`azure vm list`

   > [!NOTE]
   > Se estiver a utilizar Olá portal do Azure, selecione Olá VM e clique em **parar** encerrar Olá VM.

8. Quando Olá VM estiver parada, capture a imagem de Olá. Olá seguintes capturas do exemplo Olá VM com o nome `myVM` e cria uma imagem generalizada com o nome `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Olá `-t` subcomando eliminações Olá máquina virtual original.

    > [!NOTE]
    > No portal do Azure Olá, pode capturar uma imagem selecionando **imagem** a partir do menu do hub de Olá. Terá de Olá toosupply seguintes informações para a imagem de Olá: nome, grupo de recursos, localização, tipo de sistema operativo e caminho do blob de armazenamento.

9. nova imagem de Olá está agora disponível na lista de Olá de imagens que pode ser tooconfigure de utilizada qualquer nova VM. Pode vê-la com o comando de Olá:

   ```azurecli
   azure vm image list
   ```

   No Olá [portal do Azure](http://portal.azure.com), nova imagem de Olá aparece no Olá **imagens da VM (clássica)** que pertence toohello **computação** serviços. Pode aceder ao **imagens da VM (clássica)** clicando _mais serviços_ na parte inferior de Olá de Olá Azure service lista e, em seguida, procura no Olá **computação** serviços.   

   ![Captura de imagens com êxito](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Passos seguintes
imagem de Olá está pronto toobe utilizado toocreate VMs. Pode utilizar o comando da CLI do Azure de Olá `azure vm create` e nome da imagem de alimentação Olá que criou. Para obter mais informações, consulte [Using Olá CLI do Azure com o modelo de implementação clássica](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

Em alternativa, utilize Olá [portal do Azure](http://portal.azure.com) toocreate uma VM personalizada utilizando Olá **imagem** método e Olá a seleção da imagem que criou. Para obter mais informações, consulte [como tooCreate uma VM personalizada][How tooCreate a Custom Virtual Machine].

**Consulte também:** [guia de utilizador do agente Linux do Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
