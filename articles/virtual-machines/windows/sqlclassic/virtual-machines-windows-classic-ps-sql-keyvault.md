---
title: "aaaIntegrate Cofre de chaves com o SQL Server em VMs do Windows no Azure (clássica) | Microsoft Docs"
description: "Saiba como tooautomate Olá configuração de encriptação do SQL Server para utilização com o Cofre de chaves do Azure. Este tópico explica como toouse integração do Cofre de chaves do Azure com as máquinas virtuais do SQL Server criar no modelo de implementação clássica Olá."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Configurar a integração do Cofre de chaves do Azure para o SQL Server em Virtual Machines do Azure (clássica)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Clássico](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Descrição geral
Existem várias funcionalidades de encriptação do SQL Server, tais como [encriptação de dados transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [encriptação de nível de coluna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), e [encriptação de cópias de segurança](https://msdn.microsoft.com/library/dn449489.aspx). Estes formulários de encriptação requerem toomanage e armazenam as chaves criptográficas Olá que utilizar para a encriptação. Olá serviço Cofre de chaves do Azure (AKV) é concebida tooimprove Olá segurança e a gestão destas chaves numa localização segura e altamente disponível. Olá [conector do SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permite que o SQL Server toouse estas chaves a partir do Cofre de chaves do Azure.

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

Se estiver a executar o SQL Server com máquinas no local, existem [passos que pode seguir tooaccess Cofre de chaves do Azure a partir do seu computador do SQL Server no local](https://msdn.microsoft.com/library/dn198405.aspx). Mas para o SQL Server em VMs do Azure, pode poupar tempo ao utilizar Olá *integração do Cofre de chaves do Azure* funcionalidade. Com alguns tooenable de cmdlets do Azure PowerShell esta funcionalidade, pode automatizar Olá configuração necessária para uma VM do SQL Server tooaccess seu Cofre de chaves.

Quando esta funcionalidade está ativada, é automaticamente instalada Olá conector do SQL Server, configura tooaccess de fornecedor EKM Olá Cofre de chaves do Azure e cria Olá credencial tooallow que tooaccess o cofre. Se de que consultou passos Olá Olá mencionado anteriormente documentação no local, pode ver que esta funcionalidade automatiza os passos 2 e 3. Olá única coisa que ainda terá toodo manualmente é o Cofre de chaves do toocreate Olá e as chaves. A partir daí, a configuração completa Olá da sua VM do SQL Server é um processo automatizada. Depois desta funcionalidade concluída esta configuração, pode executar T-SQL instruções toobegin encriptar as cópias de segurança ou bases de dados, como faria normalmente.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Configurar a integração AKV
Utilize o PowerShell tooconfigure integração do Cofre de chaves do Azure. Olá secções a seguir fornece uma descrição geral dos parâmetros de Olá necessário e, em seguida, um script do PowerShell de exemplo.

### <a name="install-hello-sql-server-iaas-extension"></a>Instalar Olá extensão de IaaS do SQL Server
Primeiro, [instalar Olá extensão do SQL Server IaaS](../classic/sql-server-agent-extension.md).

### <a name="understand-hello-input-parameters"></a>Compreender os parâmetros de entrada Olá
Olá seguinte tabela apresenta uma lista de Olá os parâmetros necessários script do PowerShell Olá toorun na secção seguinte, Olá.

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| **$akvURL** |**URL do Cofre de chaves de Olá** |"https://contosokeyvault.vault.azure.net/" |
| **$spName** |**Nome Principal de serviço** |"fde2b411 - 33d 5-4e11-af04eb07b669ccf2" |
| **$spSecret** |**Segredo Principal de serviço** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM =" |
| **$credName** |**Nome da credencial**: a integração AKV cria uma credencial dentro do SQL Server, permitindo Olá VM toohave acesso toohello Cofre de chaves. Escolha um nome para esta credencial. |"mycred1" |
| **$vmName** |**Nome da máquina virtual**: nome de Olá de uma VM do SQL Server criado anteriormente. |"myvmname" |
| **$serviceName** |**Nome do serviço**: nome do serviço em nuvem Olá que estão associado com Olá VM do SQL Server. |"mycloudservicename" |

### <a name="enable-akv-integration-with-powershell"></a>Ativar a integração AKV com o PowerShell
Olá **New-AzureVMSqlServerKeyVaultCredentialConfig** cmdlet cria um objeto de configuração para a funcionalidade de integração do Cofre de chaves do Azure Olá. Olá **conjunto AzureVMSqlServerExtension** configura esta integração com Olá **KeyVaultCredentialSettings** parâmetro. Olá, como os seguintes passos Mostrar toouse estes comandos.

1. No Azure PowerShell, primeiro de configurar os parâmetros de entrada Olá com os seus valores específicos conforme descrito nas secções anteriores do Olá deste tópico. Olá script a seguir-se um exemplo.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. Em seguida, utilize Olá apresentado a seguir script tooconfigure e ativar a integração AKV.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Olá extensão de agente do SQL Server IaaS será atualizado Olá VM do SQL Server com esta nova configuração.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

