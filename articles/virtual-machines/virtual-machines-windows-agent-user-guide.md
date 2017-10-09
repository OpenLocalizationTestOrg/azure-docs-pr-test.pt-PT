---
title: "Descrição geral do agente de Máquina Virtual de aaaAzure | Microsoft Docs"
description: "Descrição geral do agente de Máquina Virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Descrição geral do agente da Máquina Virtual do Azure

Olá agente de Máquina Virtual do Microsoft Azure (agente da VM) é um processo seguro e simples que gere a interação de VM com Olá controlador de recursos do Azure. Olá agente da VM tem uma função primária em ativar e executar as extensões de máquina virtual do Azure. Ativar as extensões de VM após a configuração de implementação de máquinas virtuais, tais como instalar e configurar o software. Extensões de máquina virtual também ativar as funcionalidades de recuperação, tal como repor Olá palavra-passe administrativa de uma máquina virtual. Sem Olá agente da VM do Azure, não não possível executar as extensões de máquina virtual.

Este documento fornece detalhes sobre a instalação, a deteção e a remoção de Olá agente da Máquina Virtual do Azure.

## <a name="install-hello-vm-agent"></a>Instalar Olá agente da VM

### <a name="azure-gallery-image"></a>Imagem da galeria do Azure

Olá agente da VM do Azure está instalado por predefinição em qualquer máquina virtual do Windows implementada a partir de uma imagem de galeria do Azure. Quando implementar uma imagem de galeria do Azure a partir de Olá Portal, o PowerShell, Interface de linha de comandos ou um modelo Azure Resource Manager, Olá que agente da VM do Azure é também instalada. 

### <a name="manual-installation"></a>Instalação manual

agente de VM do Windows Hello pode de ser instalado manualmente utilizando um pacote de instalador do Windows. Instalação manual pode ser necessária quando criar uma imagem de máquina virtual personalizada que será implementado no Azure. toomanually Olá de instalar o agente de VM do Windows, transferir o instalador do agente de VM de Olá partir desta localização [transferir de agente do Windows Azure VM](http://go.microsoft.com/fwlink/?LinkID=394789). 

Olá agente da VM pode ser instalado fazendo duplo clique em ficheiro de instalador do windows hello. Para uma instalação automatizada ou automática do agente da VM Olá, execute Olá os seguintes comandos.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Detetar Olá agente da VM

### <a name="powershell"></a>PowerShell

módulo do Azure Resource Manager PowerShell de Olá pode ser utilizados tooretrieve informações sobre máquinas virtuais do Azure. Executar `Get-AzureRmVM` devolve bastantes bits de informações, incluindo Olá para Olá agente da VM do Azure, o estado de aprovisionamento.

```PowerShell
Get-AzureRmVM
```

Olá segue-se apenas um subconjunto de Olá `Get-AzureRmVM` saída. Olá aviso `ProvisionVMAgent` propriedade aninhada `OSProfile`, esta propriedade pode ser utilizado toodetermine se o agente da VM Olá foi implementado toohello máquina.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

Olá script a seguir pode ser utilizado tooreturn concisa obter uma lista de nomes de máquina virtual e o estado de Olá de Olá agente da VM.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>Deteção manual

Quando tem sessão iniciada no tooa VM do Windows Azure, o Gestor de tarefas pode ser utilizado tooexamine processos em execução. toocheck para Olá agente da VM do Azure, abra o Gestor de tarefas > clique separador de detalhes de Olá e procure um nome de processo `WindowsAzureGuestAgent.exe`. presença de Olá deste processo indica que o agente VM Olá está instalado.

## <a name="upgrade-hello-vm-agent"></a>Atualizar Olá agente da VM

Olá Azure VM agente para o Windows é atualizado automaticamente. As novas máquinas virtuais implementada tooAzure, estes recebem agente da VM Olá mais recente. Imagens VM personalizadas devem ser agente da VM nova Olá tooinclude atualizadas manualmente.
