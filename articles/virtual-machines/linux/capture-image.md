---
title: aaaCapture uma imagem de uma VM com Linux no Azure utilizando o CLI 2.0 | Microsoft Docs
description: "Capture uma imagem de toouse uma VM do Azure para implementações em massa com Olá Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>Como toocreate uma imagem de uma máquina virtual ou o VHD

<!-- generalize, image - extended version of hello tutorial-->

toocreate várias cópias dos toouse máquina virtual (VM) no Azure, capturar uma imagem de Olá VM ou Olá VHD de SO. toocreate uma imagem, tem de remover as informações de conta pessoal que torna mais segura toodeploy várias vezes. Olá os seguintes passos desaprovisionar uma VM existente, Desalocação e criar uma imagem. Pode utilizar esta imagem toocreate VMs em qualquer grupo de recursos na sua subscrição.

Se pretende toocreate uma cópia da sua VM do Linux existente para cópia de segurança ou de depuração ou carregar um VHD de Linux especializado de uma VM no local, consulte [carregar e criar uma VM com Linux a partir da imagem de disco personalizado](upload-vhd.md).  

Também pode utilizar **Packer** toocreate a configuração personalizada. Para obter mais informações sobre como utilizar Packer, consulte [como imagens de máquina virtual do toouse Packer toocreate Linux no Azure](build-image-with-packer.md).


## <a name="before-you-begin"></a>Antes de começar
Certifique-se de que cumpre Olá os seguintes pré-requisitos:

* Precisa de uma VM do Azure criados no modelo de implementação Resource Manager Olá utilizando discos geridos. Se ainda não criou uma VM com Linux, pode utilizar Olá [portal](quick-create-portal.md), Olá [CLI do Azure](quick-create-cli.md), ou [modelos do Resource Manager](create-ssh-secured-vm-from-template.md). Configure Olá VM conforme necessário. Por exemplo, [adicionar discos de dados](add-disk.md), aplicar atualizações e instalar aplicações. 

* Também precisa de toohave Olá mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e de ter sessão iniciada utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).

## <a name="quick-commands"></a>Comandos rápidos

Para uma versão simplificada neste tópico, para fins de teste, avaliar ou a saber mais sobre as VMs do Azure, consulte o artigo [criar uma imagem personalizada da VM do Azure utilizando Olá CLI](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>Passo 1: Desaprovisionar Olá VM
Desaprovisionar Olá VM, com o agente da VM do Azure de Olá, dados e ficheiros específicos do toodelete máquina. Olá utilize `waagent` comando com Olá *-deprovision + utilizador* parâmetro na sua origem de VM com Linux. Para obter mais informações, consulte Olá [guia de utilizador do agente Linux do Azure](../windows/agent-user-guide.md).

1. Ligar tooyour VM com Linux utilizando um cliente SSH.
2. Na janela SSH Olá, escreva Olá os seguintes comandos:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Apenas execute este comando numa VM que pretende toocapture como uma imagem. Garante dessa imagem Olá é limpa de todas as informações confidenciais ou é adequada para a redistribuição. Olá *+ utilizador* parâmetro também remove a última conta de utilizador aprovisionado Olá. Se pretender que as credenciais da conta tookeep no Olá VM, utilize apenas *-deprovision* conta de utilizador de Olá tooleave no local.
 
3. Tipo **y** toocontinue. Pode adicionar Olá **-forçar** parâmetro tooavoid este passo de confirmação.
4. Após a conclusão do comando de Olá, escreva **sair**. Este passo se fechar o cliente SSH Olá.

## <a name="step-2-create-vm-image"></a>Passo 2: Criar a imagem de VM
Utilize Olá de toomark Olá Azure CLI 2.0 VM como generalizado e capturar a imagem de Olá. No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes dos parâmetros de exemplo incluem *myResourceGroup*, *myVnet*, e *myVM*.

1. Desalocar Olá VM desaprovisionada com [az vm desalocar](/cli//azure/vm#deallocate). Olá exemplo seguinte deallocates Olá VM com o nome *myVM* no grupo de recursos de Olá designado *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. Olá marca VM como generalizado com [az vm Generalizar](/cli//azure/vm#generalize). Olá seguintes Olá Olá marcas de exemplo com o nome de VM *myVM* no grupo de recursos de Olá designado *myResourceGroup* como generalizado:
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Agora criar uma imagem de recurso VM Olá com [criar imagem az](/cli//azure/image#create). Olá exemplo seguinte cria uma imagem com o nome *myImage* no grupo de recursos de Olá designado *myResourceGroup* com recurso VM de Olá designado *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Olá imagem é criada na Olá mesmo grupo de recursos como a VM de origem. Pode criar VMs em qualquer grupo de recursos na sua subscrição a partir desta imagem. Numa perspetiva de gestão, pode ser útil toocreate um grupo de recursos específicos para os recursos da VM e imagens.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Passo 3: Criar uma VM da imagem de Olá capturada
Criar uma VM utilizando a imagem de Olá que criou com [az vm criar](/cli/azure/vm#create). Olá exemplo seguinte cria uma VM chamada *myVMDeployed* imagem Olá com o nome do *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Criar Olá VM noutro grupo de recursos 

Pode criar VMs a partir de uma imagem em qualquer grupo de recursos na sua subscrição. toocreate uma VM de um grupo de recursos diferente que imagem Olá, especifique a imagem de tooyour de ID de recurso completo de Olá. Utilize [lista de imagens az](/cli/azure/image#list) tooview uma lista de imagens. Olá de saída é semelhante toohello seguinte exemplo:

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Olá exemplo seguinte utiliza [az vm criar](/cli/azure/vm#create) toocreate uma VM de um grupo de recursos diferente a imagem de origem Olá, especificando o ID de recurso de imagem de Olá:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Passo 4: Verificar a implementação de Olá

Agora SSH toohello máquina virtual é criada a implementação de Olá tooverify e utilizar o início Olá nova VM. tooconnect através de SSH, localizar o endereço IP Olá ou o FQDN da sua VM com [mostrar de vm az](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Passos seguintes
Pode criar várias VMs a partir da imagem de VM de origem. Se precisar de imagem de tooyour toomake alterações: 

- Crie uma VM a partir da imagem.
- Fazer quaisquer atualizações ou alterações de configuração.
- Siga Olá novamente passos toodeprovision, desalocar, generalize e criar uma imagem.
- Utilize esta nova imagem para implementações futuras. Se assim o desejar, elimine a imagem original Olá.

Para obter mais informações sobre gerir as VMs com Olá CLI, consulte [Azure CLI 2.0](/cli/azure/overview).
