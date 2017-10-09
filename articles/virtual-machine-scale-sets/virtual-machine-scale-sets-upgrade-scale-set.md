---
title: "conjunto de um dimensionamento de máquina virtual do Azure aaaUpgrade | Microsoft Docs"
description: "Atualizar um conjunto de dimensionamento da máquina virtual do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Atualizar um conjunto de dimensionamento de máquina virtual
Este artigo descreve como pode implementar um SO atualização tooan máquina virtual do Azure conjunto de dimensionamento sem qualquer período de inatividade. Neste contexto, uma atualização de SO envolve alterar versão Olá ou SKU do Olá SO ou alterar Olá URI de uma imagem personalizada. A atualização sem meios de período de indisponibilidade atualizar máquinas virtuais uma a uma hora ou em grupos (por exemplo, um domínio de falhas numa altura) em vez de ao mesmo tempo. Ao fazê-lo, pode manter executar quaisquer máquinas virtuais que não estão a ser atualizadas.

tooavoid ambiguidade, vamos distinguir quatro tipos de atualização de SO poderá tooperform:

* Alterar a versão de Olá ou SKU de uma imagem de plataforma. Por exemplo, a alteração Ubuntu versão 14.04.2-LTS de 14.04.201506100 too14.04.201507060 ou alterar Olá Ubuntu 15.10/mais recente SKU too16.04.0-LTS/latest. Este cenário é descrito neste artigo.
* A alteração Olá URI que aponta tooa nova versão de uma imagem personalizada que criou (**propriedades** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **imagem** > **uri**). Este cenário é descrito neste artigo.
* A alteração Olá a referência da imagem de um conjunto de dimensionamento que foi criada utilizando discos de gerida do Azure.
* Aplicação de patches Olá SO a partir de uma máquina virtual (exemplos deste incluem a instalação de um patch de segurança e executar o Windows Update). Este cenário é suportado, mas não abrangido neste artigo.

Conjuntos de dimensionamento de máquina virtual que são implementados como parte de um [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster não são abrangidos aqui. Consulte [Patch de SO de Windows no seu cluster do Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) para obter mais informações sobre a aplicação de patches de Service Fabric.

Olá básico Olá de sequência de tarefas para alterar versão de SO/SKU de uma imagem de plataforma ou Olá URI de uma imagem personalizada procura da seguinte forma:

1. Obter o modelo de conjunto de dimensionamento de máquina virtual de Olá.
2. Alterar versão do Olá, SKU, a referência da imagem ou o valor no modelo de Olá URI.
3. Atualize o modelo de Olá.
4. Fazer uma *manualUpgrade* chamar Olá máquinas de virtuais num conjunto de dimensionamento de Olá. Este passo só é relevante se *upgradePolicy* estiver definido demasiado**Manual** no seu dimensionamento definido. Se estiver definido demasiado**automática**, todas as máquinas de virtuais Olá sejam atualizadas em simultâneo, fazendo com que um período de indisponibilidade.

Com estas informações em mente, vamos ver como foi possível atualizar a versão de Olá de um conjunto no PowerShell e utilizando Olá REST API de dimensionamento. Estes exemplos abrangem Olá maiúsculas e minúsculas de uma imagem de plataforma, mas este artigo fornece informações suficientes para lhe tooadapt esta imagem personalizada do tooa de processo.

## <a name="powershell"></a>PowerShell
Neste exemplo de atualizações de um conjunto de dimensionamento de máquina virtual do Windows (criar toohello nova versão 4.0.20160229. Depois de atualizar o modelo de Olá, faz uma instância de máquina virtual de um de atualização de cada vez.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

Se estiver a atualizar o Olá URI para uma imagem personalizada em vez de alterar uma versão de imagem de plataforma, substitua Olá "Definir Olá nova versão" Olá, linha com um comando que irá atualizar a imagem de origem URI. Por exemplo, se o conjunto de dimensionamento de Olá foi criado sem utilizar discos gerida do Azure, atualização Olá seria este aspeto:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Se uma imagem personalizada baseada em conjunto de dimensionamento foi criada utilizando discos gerida do Azure, em seguida, a referência da imagem Olá seria atualizada. Por exemplo:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Olá REST API
Seguem-se alguns exemplos de Python que utilizam a API REST da Azure de Olá tooroll fora de uma atualização de versão do SO. Utilizam ambos lightweight Olá [azurerm](https://pypi.python.org/pypi/azurerm) biblioteca de API REST da Azure wrapper funções toodo uma ação obter numa escala de Olá definir modelo, seguido de um PUT com um modelo atualizado. Podem também ver vistas de instâncias de máquina virtual tooidentify Olá máquinas virtuais por domínio de atualização.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) é um script de Python que tenha utilizado tooroll terminar um tooa de atualização de SO em execução de dimensionamento da máquina virtual definir um domínio de atualização de cada vez.

![Script de Vmssupgrade para escolher um domínio de atualização ou máquinas virtuais](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Este script permite-lhe escolher tooupdate de máquinas virtuais específicas ou especificar um domínio de atualização. Suporta a alteração de uma versão de imagem de plataforma ou alterar Olá URI de uma imagem personalizada.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) é um editor para fins gerais para conjuntos de dimensionamento de máquina virtual que mostra a virtual máquina de estado como um heatmap em que uma linha representa um domínio de atualização. Entre outras coisas, pode atualizar o modelo de Olá para um conjunto de dimensionamento com uma nova versão, o SKU ou o URI de imagem personalizada e, em seguida, escolha tooupgrade de domínios de falhas. Ao fazê-lo, todas as máquinas de virtuais Olá nesse domínio de atualização são toohello atualizado novo modelo. Em alternativa, pode efetuar uma atualização sem interrupção, com base no tamanho do lote Olá à sua escolha.  

Olá seguinte captura de ecrã mostra um modelo de um conjunto para Ubuntu 14.04-2LTS versão 14.04.201507060 de dimensionamento. Muitas mais opções foram adicionadas toothis ferramenta desde que foi tirada nesta captura de ecrã.

![Modelo de Vmsseditor de um conjunto para Ubuntu 14.04-2LTS de dimensionamento](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

Depois de clicar em **atualizar** e, em seguida, **obter detalhes**, máquinas virtuais no UD 0 Iniciar tooupdate.

![Vmsseditor que mostra atualização em curso](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

