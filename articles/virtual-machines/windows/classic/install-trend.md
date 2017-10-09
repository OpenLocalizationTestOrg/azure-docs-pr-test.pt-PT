---
title: "aaaInstall tendência Micro segurança profunda numa VM | Microsoft Docs"
description: "Este artigo descreve como tooinstall e configurar a segurança de tendência Micro numa VM criada com o modelo de implementação clássica Olá no Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>Como tooinstall e configurar a segurança avançada do tendência Micro como um serviço numa VM do Windows
> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

Este artigo mostra como tooinstall e configurar a segurança avançada do tendência Micro como um serviço numa nova ou existente máquina virtual (VM) com o Windows Server. Segurança avançada, como um serviço inclui proteção antimalware, uma firewall, um sistema de prevenção de intrusões e monitorização de integridade.

Olá é instalado como uma extensão de segurança através de Olá agente da VM. Uma nova máquina virtual, instale Olá profunda de segurança de agente, como Olá que agente da VM é automaticamente criada pelo Olá portal do Azure.

VM existente criada utilizando o portal clássico Olá, Olá Azure CLI ou PowerShell poderá não ter um agente VM. Para uma máquina virtual existente que não tem Olá agente da VM, tem de toodownload e instale-o primeiro. Este artigo abrange ambas as situações.

Se tiver uma subscrição atual de tendência Micro para uma solução no local, pode utilizá-lo toohelp proteger as máquinas virtuais do Azure. Se ainda não estiver um cliente, pode inscrever-se para uma subscrição de avaliação. Para obter mais informações sobre esta solução, consulte a mensagem de blogue de tendência Micro de Olá [Microsoft Azure VM extensão para a segurança do agente](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Instalar uma nova VM Olá profunda de segurança de agente

Olá [portal do Azure](http://portal.azure.com) permite-lhe instalar extensão de segurança de tendência Micro Olá quando utiliza uma imagem de Olá **Marketplace** toocreate Olá máquina. Se estiver a criar uma máquina virtual individual, através do portal Olá é uma proteção de tooadd de forma fácil de tendência Micro.

Através de uma entrada de Olá **Marketplace** abre um assistente que o ajuda a configurar a máquina virtual de Olá. Utilizar Olá **definições** painel, o painel de terceiro Olá do Assistente de Olá, tooinstall Olá extensão de segurança de tendência Micro.  Para instruções gerais, consulte [criar uma máquina virtual com o Windows hello portal do Azure](tutorial.md).

Quando obtiver toohello **definições** Olá painel do Assistente de Olá, os seguintes passos:

1. Clique em **extensões**, em seguida, clique em **Adicionar extensão** no painel seguinte Olá.

   ![Começar a adicionar a extensão de Olá][1]

2. Selecione **profunda de segurança de agente** no Olá **novo recurso** painel. No painel de agente de segurança avançada de Olá, clique em **criar**.

   ![Identificar o agente de segurança avançada][2]

3. Introduza Olá **identificador de inquilino** e **palavra-passe de ativação de inquilino** para extensão Olá. Opcionalmente, pode introduzir um **identificador de política de segurança**. Em seguida, clique em **OK** cliente de Olá tooadd.

   ![Forneça detalhes de extensão][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Instalar Olá profunda de segurança de agente numa VM existente
agente de Olá tooinstall numa VM existente, terá de Olá seguintes itens:

* módulo do Azure PowerShell Olá, versão 0.8.2 ou mais recente, instalada no seu computador local. Pode verificar a versão de Olá do Azure PowerShell que tenha instalado utilizando Olá **azure Get-Module | versão de formato tabela** comando. Para obter instruções e uma versão mais recente do toohello de ligação, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Inicie sessão com a subscrição do Azure tooyour `Add-AzureAccount`.
* Olá agente da VM instalado na máquina de virtual de destino Olá.

Em primeiro lugar, certifique-se que Olá que agente da VM já se encontra instalado. Preencha o nome do serviço de nuvem de Olá e nome da máquina virtual em seguida, execute Olá os seguintes comandos uma linha de comandos do PowerShell do Azure de nível de administrador. Substitua tudo dentro de aspas Olá, incluindo Olá < e > carateres.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Se não souber o serviço em nuvem Olá e nome da máquina virtual, execute **Get-AzureVM** toodisplay que informações para todos os Olá máquinas virtuais na sua subscrição atual.

Se hello **escrita anfitrião** comando devolve **verdadeiro**, Olá agente VM está instalado. Se devolver **falso**, consulte as instruções de Olá e toohello uma hiperligação Transferir Olá mensagem de blogue do Azure [extensões - parte 2 e o agente da VM](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Se Olá agente VM está instalado, execute estes comandos.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Passos seguintes
Demora alguns minutos para Olá toostart de agente em execução quando é instalado. Depois disso, terá de tooactivate segurança profunda na máquina virtual de Olá, para que possa ser gerido por um Gestor de segurança avançada. Olá seguintes artigos para obter instruções adicionais, consulte:

* Artigo da tendência sobre esta solução, [Instant-On Cloud Security para o Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)
* A [script do Windows PowerShell de exemplo](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure Olá máquina
* [Instruções](http://go.microsoft.com/fwlink/?LinkId=404099) de exemplo de Olá

## <a name="additional-resources"></a>Recursos adicionais
[Como toolog na máquina de virtual tooa com o Windows Server]

[Extensões de VM do Azure e funcionalidades]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Como toolog na máquina de virtual tooa com o Windows Server]:connect-logon.md
[Extensões de VM do Azure e funcionalidades]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
