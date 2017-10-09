---
title: "aaaAzure discos de dados ligados à máquina Virtual escala conjuntos | Microsoft Docs"
description: "Saiba como toouse ligado a discos de dados com conjuntos de dimensionamento de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Conjuntos de dimensionamento de VMs do Azure e discos de dados anexados
Agora, os [conjuntos de dimensionamento de máquinas virtuais](/azure/virtual-machine-scale-sets/) do Azure suportam máquinas virtuais com discos de dados anexados. Os discos de dados podem ser definidos no perfil de armazenamento Olá para conjuntos de dimensionamento que foram criadas com discos gerida do Azure. Anteriormente hello apenas ligado diretamente as opções de armazenamento disponíveis com as VMs em conjuntos de dimensionamento foram unidade Olá SO e unidades temporários.

> [!NOTE]
>  Quando cria um conjunto com discos de dados anexados definidos de dimensionamento, terá ainda de toomount e Olá formato discos de dentro de uma VM toouse-los (apenas como autónomo VMs do Azure). Uma forma conveniente toodo trata toouse uma extensão de script personalizado que chama um script padrão toopartition e formatar a todos os discos de dados de Olá numa VM.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Criar um conjunto de dimensionamento com discos de dados anexados
Toocreate uma forma simples definir com discos ligados a uma escala é toouse Olá [CLI do Azure](https://github.com/Azure/azure-cli) _vmss criar_ comando. Olá seguinte exemplo cria um grupo de recursos do Azure e um conjunto de dimensionamento VM de 10 Ubuntu VMs, cada um com discos de dados anexados 2, de 50 GB e 100 GB, respetivamente.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Tenha em atenção que Olá _vmss criar_ comando predefinições determinados valores de configuração se não especificá-los. toosee Olá opções disponíveis que pode substituir tente:
```bash
az vmss create --help
```
Outra forma toocreate, um conjunto com discos de dados anexados de dimensionamento é toodefine uma escala definida num modelo Azure Resource Manager, incluir uma _dataDisks_ secção Olá _storageProfile_e implementar Olá modelo. Olá 50 GB e 100 GB disco exemplo acima deverá ser definido como esta no modelo de Olá:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
Pode ver um exemplo de toodeploy concluída, pronto de um modelo de conjunto de dimensionamento com um disco ligado definido aqui: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Adicionar uma escala existentes do disco tooan de dados definido
> [!NOTE]
>  Apenas pode anexar dados discos tooa conjunto de dimensionamento da que foi criado com [Azure geridos discos](./virtual-machine-scale-sets-managed-disks.md).

Pode adicionar um dados disco tooa dimensionamento definido utilizando a CLI do Azure _anexar o disco de vmss az_ comando. Certifique-se de que especifica um lun que não esteja já em utilização. Olá seguinte CLI exemplo adiciona uma toolun de unidade de 50 GB 3:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

Olá seguinte o exemplo do PowerShell adiciona um toolun de unidade de 50 GB 3:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Tamanhos VM diferentes têm limites diferentes em números de Olá de unidades anexados suportam. Verifique Olá [características de tamanho de máquina virtual](../virtual-machines/windows/sizes.md) antes de adicionar um novo disco.

Também pode adicionar um disco ao adicionar um novo toohello de entrada _dataDisks_ propriedade no Olá _storageProfile_ de escala definido a definição e aplicar a alteração de Olá. tootest, encontrar uma definição de conjunto de dimensionamento existente no Olá [Explorador de recursos do Azure](https://resources.azure.com/). Selecione _editar_ e adicione uma nova lista de toohello de disco de discos de dados. Por exemplo, utilizar o exemplo de Olá acima:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

Em seguida, selecione _colocar_ tooapply Olá altera o conjunto de dimensionamento tooyour. Este exemplo funciona desde que utilize um tamanho de VM que suporte mais do que dois discos de dados anexados.

> [!NOTE]
> Quando efetuar o conjunto de dimensionamento de tooa uma alteração da definição de como adicionar ou remover um disco de dados, que aplica-se as VMs de tooall recentemente criado, mas apenas se aplica tooexisting VMs se hello _upgradePolicy_ propriedade está definida demasiado "automática". Se estiver definido demasiado "Manual", precisa de toomanually aplicar Olá novo modelo tooexisting VMs. Pode fazer isto no portal de Olá, utilizando Olá _atualização AzureRmVmssInstance_ PowerShell comandos ou utilizando Olá _az vmss update-instâncias_ comando da CLI.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Adicionar conjunto de dimensionamento existente do tooan de discos de dados pré-preenchidos 
> Ao adicionar discos tooan existente conjunto de dimensionamento de modelo, por predefinição, o disco de Olá será sempre criado vazio. Este cenário também inclui novas instâncias criadas pelo conjunto de dimensionamento de Olá. Este comportamento é porque a definição de scaleset Olá tem um disco de dados vazio. Na ordem toocreate dados pré-preenchidos unidades para um modelo de conjunto de dimensionamento existente, pode escolher uma das junto duas opções:

* Copie dados de discos de dados do Olá instância 0 VM toohello no Olá outras VMs, executando um script personalizado.
* Criar uma imagem gerida com o disco de SO de Olá plus disco de dados (com dados Olá necessário) e crie um novo scaleset com imagem Olá. Desta forma, cada nova VM criada terá dados de um disco que é fornecido na definição de Olá de Olá scaleset. Uma vez que esta definição irá referir-se a imagem de tooan com um disco de dados que tenha personalizado dados, cada máquina virtual no Olá scaleset será pensar automaticamente com estas alterações.

> Olá toocreate de forma uma imagem personalizada pode ser encontrada aqui: [criar uma imagem gerida de uma VM generalizada no Azure](/azure/virtual-machines/windows/capture-image-resource/) 

> Olá utilizador precisa de toocapture Olá instância 0 VM que tenha Olá dados necessários e, em seguida, utilizar essa vhd para a definição de imagem de Olá.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Remover um disco de dados de um conjunto de dimensionamento
Pode remover um disco de dados de um conjunto de dimensionamento de VM com o comando _az vmss disk detach_ da CLI do Azure. Por exemplo Olá seguinte comando remove o Olá disco definido no lun 2:
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
Da mesma forma, pode também remover um disco de um conjunto ao remover uma entrada de Olá de dimensionamento _dataDisks_ propriedade no Olá _storageProfile_ e aplicar a alteração de Olá. 

## <a name="additional-notes"></a>Notas adicionais
Suporte para discos gerida do Azure e o dimensionamento definido discos de dados anexados está disponível numa versão de API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) ou posterior do Olá Microsoft. Compute API.

Na implementação inicial de Olá do suporte de disco ligado para conjuntos de dimensionamento, não é possível anexar ou desanexar os discos de dados do VMs individuais num conjunto de dimensionamento.

O suporte do portal do Azure para discos de dados anexados em conjuntos de dimensionamento é limitado inicialmente. Dependendo dos requisitos, que pode utilizar os modelos do Azure, CLI, do PowerShell, SDKs e REST API toomanage discos ligados.


