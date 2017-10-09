---
title: "listas de controlo de aaaManage acesso de ponto final do Azure | PowerShell | Clássico | Microsoft Docs"
description: Saiba como toomanage ACLs com o PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Gerir listas de controlo de acesso de ponto final com o PowerShell no modelo de implementação clássica Olá
Pode criar e gerir o controlo de acesso de rede lista (ACLs) para pontos finais utilizando o Azure PowerShell ou na Olá Portal de gestão. Neste tópico, encontrará procedimentos para tarefas comuns de ACL que pode realizar com o PowerShell. Para obter lista de Olá do Azure PowerShell cmdlets consulte [Cmdlets de gestão do Azure](http://go.microsoft.com/fwlink/?LinkId=317721). Para obter mais informações sobre as ACLs, consulte [o que é uma lista de controlo de acesso de rede (ACL)?](virtual-networks-acl.md). Se pretender toomanage as ACLs utilizando o Portal de gestão de Olá, veja [como tooSet pontos finais de cópia de segurança tooa Máquina Virtual](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Gerir ACLs de rede utilizando o Azure PowerShell
Pode utilizar o Azure PowerShell cmdlets toocreate, remova e configure (conjunto) rede acesso as listas de controlo (ACLs). Iremos tiver incluído alguns exemplos de algumas formas de Olá que pode configurar uma ACL com o PowerShell.

tooretrieve uma lista completa dos cmdlets do PowerShell de ACL de Olá, pode utilizar qualquer um dos seguintes Olá:

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Criar uma ACL de rede com regras que permitem o acesso a partir de uma sub-rede remota
exemplo de Olá abaixo ilustra uma toocreate de forma uma que contém as regras de ACL de novo. Em seguida, é aplicada esta ACL de ponto final de máquina virtual tooa. regras de ACL de Olá no exemplo Olá abaixo permitirá o acesso a partir de uma sub-rede remota. toocreate uma ACL de rede nova com regras de autorização para uma sub-rede remota, abra uma ISE do PowerShell do Azure. Copie e cole o script Olá abaixo, configurando o script de Olá com os seus próprios valores e, em seguida, execute o script de Olá.

1. Crie Olá novo objeto de ACL de rede.
   
        $acl1 = New-AzureAclConfig
2. Defina uma regra que permite acesso de sub-rede remota. Exemplo de Olá abaixo, definir regra *100* (que tem prioridade sobre regra 200 e superior) sub-rede remota de Olá tooallow *10.0.0.0/8* aceder ao ponto final de máquina virtual toohello. Substitua os valores de Olá os seus requisitos de configuração. o nome de Olá "Configuração de ACL de SharePoint" deve ser substituído com o nome amigável Olá que pretende toocall esta regra.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Para as regras adicionais, repita o cmdlet Olá, substituindo os valores de Olá com os seus próprios requisitos de configuração. Ser se toochange Olá regra número Order tooreflect Olá ordem em que pretende Olá regras toobe aplicada. número de regra inferior Olá tem precedência sobre o número mais alto Olá.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. Em seguida, pode criar um novo ponto final (Add) ou definir Olá ACL para um ponto final existente (conjunto). Neste exemplo, iremos adicionar que um novo ponto final da máquina virtual denominada "web" e a atualização Olá máquina virtual ponto final com Olá as definições de ACL.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. Em seguida, combinar cmdlets Olá e execute o script de Olá. Para este exemplo Olá cmdlets combinados seria este aspeto:
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Remover uma regra de ACL de rede que permite acesso de sub-rede remota
exemplo de Olá abaixo ilustra uma tooremove de forma uma regra ACL de rede.  tooremove uma regra de ACL de rede com permitir regras para uma sub-rede remota, abra uma ISE do PowerShell do Azure. Copie e cole o script Olá abaixo, configurando o script de Olá com os seus próprios valores e, em seguida, execute o script de Olá.

1. Primeiro passo é o objeto de ACL de rede de Olá tooget para o ponto final de máquina virtual de Olá. Em seguida, removeremos a regra de ACL de Olá. Neste caso, estamos a removê-lo por ID de regra. Isto removerá o ID de regra de Olá 0 apenas do Olá ACL. Não remove objecto ACL de Olá do ponto final de máquina virtual de Olá.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. Em seguida, tem de aplicar Olá ACL de rede objeto toohello virtual ponto final da máquina e atualizar a máquina virtual de Olá.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Remover uma ACL de rede de um ponto final da máquina virtual
Em certos cenários, pode querer tooremove um objeto de ACL de rede a partir de um ponto final da máquina virtual. toodo que, abra uma ISE do PowerShell do Azure. Copie e cole o script Olá abaixo, configurando o script de Olá com os seus próprios valores e, em seguida, execute o script de Olá.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Passos seguintes
[O que é uma lista de controlo de acesso de rede (ACL)?](virtual-networks-acl.md)

