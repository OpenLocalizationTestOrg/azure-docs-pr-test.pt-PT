---
title: "aaaReset Olá palavra-passe ou a configuração de ambiente de trabalho remoto numa VM do Windows no Azure | Microsoft Docs"
description: "Saiba como tooreset uma palavra-passe de conta ou serviços de ambiente de trabalho remoto numa VM do Windows criada utilizando Olá clássico implementação modelo utilizando Olá portal do Azure ou do Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Como o serviço de ambiente de trabalho remoto de Olá tooreset ou a palavra-passe de início de sessão numa Windows VM criados utilizando o modelo de implementação clássica Olá
> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Também pode [executar estes passos para VMs criadas com o modelo de implementação do Resource Manager Olá](../reset-rdp.md).

Se não conseguir ligar a máquina virtual (VM) do tooa Windows, pode repor a palavra-passe de administrador local do Olá ou reponha Olá configuração do serviço de ambiente de trabalho remoto. Pode utilizar qualquer um dos Olá extensão de acesso de VM do Azure portal ou Olá na palavra-passe do Azure PowerShell tooreset Olá.

## <a name="ways-tooreset-configuration-or-credentials"></a>Configuração de tooreset formas ou credenciais
Pode repor os serviços de ambiente de trabalho remoto e as credenciais de diversas formas, consoante as suas necessidades:

- [Repor utilizando Olá portal do Azure](#azure-portal)
- [Repor com o Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Portal do Azure
Pode utilizar Olá [portal do Azure](https://portal.azure.com) tooreset Olá serviço de ambiente de trabalho remoto. menu do portal Olá tooexpand, clique em barras Olá três no canto superior esquerdo Olá e, em seguida, clique em **máquinas virtuais (clássicas)**:

![Navegue para a VM do Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

Selecione a máquina virtual do Windows e, em seguida, clique em **repor remoto...** . hello seguinte caixa de diálogo é apresentada a configuração de ambiente de trabalho remoto de Olá tooreset:

![Página de configuração reposição RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

Pode também repô Olá nome de utilizador e palavra-passe da conta de administrador local Olá. A VM, clique em **suporte + resolução de problemas** > **Repor palavra-passe**. é apresentado o painel de reposição de palavra-passe Olá:

![Página de reposição de palavra-passe](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Depois de introduzir Olá novo nome de utilizador e a palavra-passe, clique em **guardar**.

## <a name="vmaccess-extension-and-powershell"></a>Extensão VMAccess e PowerShell
Certifique-se de que Olá que agente VM está instalado na máquina virtual de Olá. Olá extensão VMAccess não necessita de toobe instalado para poder utilizá-lo, desde que Olá agente VM está disponível. Certifique-se de que Olá que agente da VM já estiver instalado utilizando Olá os seguintes comandos. (Substituir "myCloudService" e "myVM" por nomes de Olá do seu serviço em nuvem e a VM, respetivamente. Pode obter estes nomes executando `Get-AzureVM` sem quaisquer parâmetros.)

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Se hello **escrita anfitrião** comando apresenta **verdadeiro**, Olá agente VM está instalado. Se apresenta **falso**, consulte as instruções de Olá e toohello uma hiperligação Transferir Olá [extensões - parte 2 e o agente da VM](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) mensagem de blogue do Azure.

Se criou a máquina virtual de Olá através do portal Olá, verifique se `$vm.GetInstance().ProvisionGuestAgent` devolve **verdadeiro**. Caso contrário, pode configurá-lo ao utilizar este comando:

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

Este comando impede Olá seguinte erro ao executar o Olá **conjunto AzureVMExtension** comando nos passos seguintes Olá: "Aprovisionar o agente convidado deve ser ativado no objeto VM Olá antes de definir a extensão de acesso de VM do IaaS."

### <a name="reset-hello-local-administrator-account-password"></a>**Repor palavra-passe de conta de administrador local Olá**
Criar uma credencial de início de sessão com o nome de conta de administrador local Olá atual e uma palavra-passe nova e, em seguida, execute Olá `Set-AzureVMAccessExtension` da seguinte forma.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Se escrever um nome diferente conta atual de Olá, Olá extensão VMAccess muda o nome de conta de administrador local Olá, atribui a conta de toothat Olá palavras-passe e emite um ambiente de trabalho remoto fim de sessão. Se a conta de administrador local Olá estiver desativada, Olá extensão VMAccess ativa o mesmo.

Estes comandos também repor a configuração do serviço de ambiente de trabalho remoto de Olá.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Repor a configuração do serviço de ambiente de trabalho remoto de Olá**
tooreset Olá ambiente de trabalho remoto a configuração do serviço, executar Olá os seguintes comandos:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Olá extensão VMAccess executa dois comandos na máquina virtual de Olá:

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

Este comando activa grupo Firewall do Windows incorporado Olá que permita o tráfego recebido do ambiente de trabalho remoto, que utiliza a porta TCP 3389.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

Este comando define Olá fDenyTSConnections registo valor too0, ativação de ligações de ambiente de trabalho remoto.

## <a name="next-steps"></a>Passos seguintes
Se não responde Olá extensão de acesso de VM do Azure e são palavra-passe do tooreset não é possível Olá, pode [reposição Olá Windows palavra-passe local offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Este método é um processo mais avançado e requer que tooconnect Olá disco rígido virtual Olá problemática VM tooanother VM. Siga os passos de Olá documentados neste artigo pela primeira vez e apenas a tentativa de método de reposição de palavra-passe offline Olá como último recurso.

[Extensões VM do Azure e funcionalidades](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Ligar tooan máquina virtual do Azure com RDP ou SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Resolver problemas de ambiente de trabalho remoto ligações tooa baseados em Windows máquina virtual do Azure](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

