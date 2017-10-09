---
title: "aaaCopy uma gerida do Azure em disco para Back cópias de segurança | Microsoft Docs"
description: "Saiba como toocreate emite uma cópia de um toouse de disco gerida do Azure para o disco voltar se ou a resolução de problemas."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Criar uma cópia de um VHD armazenado como um disco gerida do Azure, utilizando instantâneos de gerido
Tirar um instantâneo de um disco de gerido para cópia de segurança ou criar um disco gerido a partir do instantâneo Olá e anexe-tootroubleshoot de máquina virtual de teste tooa. Um instantâneo gerido é uma cópia completa ponto no tempo de um disco de geridos de VM. Cria uma cópia só de leitura do seu VHD e, por predefinição, armazena-lo como um disco gerido Standard. 

Para obter informações sobre preços, consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Utilize o Olá tootake de 2.0 do Azure CLI do Azure portal ou Olá um instantâneo de Olá disco gerida.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Utilizar o Azure CLI 2.0 tootake um instantâneo

> [!NOTE] 
> Olá seguinte exemplo requer Olá Azure CLI 2.0 instalado e registado na sua conta do Azure.

Olá passos seguintes mostram como tooobtain e tirar um instantâneo de um SO gerido disco Olá `az snapshot create` comando com Olá `--source-disk` parâmetro. Olá seguinte exemplo assume que há uma VM chamada `myVM` criado com um disco de SO gerido no Olá `myResourceGroup` grupo de recursos.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

saída de Olá deverá ter um aspeto semelhante ao seguinte:

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Utilizar tootake do portal do Azure, um instantâneo 

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. A partir de Olá canto superior esquerdo, clique em **novo** e procure **instantâneo**.
3. No painel de instantâneo Olá, clique em **criar**.
4. Introduza um **nome** para instantâneo Olá.
5. Selecione um existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de Olá de tipo para um novo. 
6. Selecione um localização do datacenter do Azure.  
7. Para **disco de origem**, selecione Olá toosnapshot de disco gerido.
8. Selecione Olá **tipo de conta** instantâneo de Olá toouse toostore. Recomendamos **Standard_LRS** , a menos que o ficheiro necessário armazenados num disco elevado desempenho.
9. Clique em **Criar**.

Se planear toouse Olá instantâneo toocreate um disco gerido e ligá-lo uma VM que necessita de toobe elevado desempenho, utilize o parâmetro de Olá `--sku Premium_LRS` com Olá `az snapshot create` comando. Esta ação cria o instantâneo de Olá, para que esta está armazenada como um disco de gerido para Premium. Os discos Premium geridos melhor efetuar porque são unidades de estado sólido (SSDs), mas custo mais do que os discos padrão (HDDs).


