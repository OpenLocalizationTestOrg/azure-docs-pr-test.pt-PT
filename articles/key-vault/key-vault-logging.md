---
title: Registo do Cofre de chave de aaaAzure | Microsoft Docs
description: "Utilize este tutorial toohelp começar com o Cofre de chaves do Azure registo."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Registo do Cofre de Chaves do Azure
O Cofre de Chaves do Azure chave está disponível na maior parte das regiões. Para obter mais informações, consulte Olá [Cofre de chaves página de preços](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introdução
Depois de criar um ou mais cofres de chaves, irá provavelmente pretender toomonitor como e quando a sua chave de cofres dos são acedidos e por quem. Esta ação é possível ao ativar o registo do Cofre de Chaves, que guarda as informações numa conta de armazenamento do Azure que indicar. É automaticamente criado um novo contentor designado **insights-logs-auditevent** na sua conta de armazenamento especificada, sendo que também pode utilizar essa mesma conta de armazenamento para recolher registos para vários cofres de chaves.

Pode aceder às suas informações de registo no máximo, 10 minutos após a chave de Olá operação do cofre. Na maioria dos casos, o processo será ainda mais rápido.  Está a funcionar tooyou toomanage os seus registos na sua conta de armazenamento:

* Utilize toosecure de métodos de controlo de acesso do Azure standard os seus registos, restringindo quem pode aceder a eles.
* Elimine registos que já não pretende que tookeep na sua conta de armazenamento.

Utilize este tutorial toohelp começar com o cofre do Azure chave de registo, toocreate a conta de armazenamento, ativar o registo e interpretar as informações de registo de Olá recolhidas.  

> [!NOTE]
> Este tutorial não inclui instruções sobre como toocreate chave cofres, chaves ou segredos. Para obter estas informações, consulte o artigo [Introdução ao Cofre de Chaves do Azure](key-vault-get-started.md). Ou, para obter instruções sobre a Interface de Linha de Comandos de várias plataformas, veja o [tutorial equivalente](key-vault-manage-with-cli2.md).
>
> Atualmente, não é possível configurar o Cofre de chaves do Azure no Olá portal do Azure. Em alternativa, utilize estas instruções do Azure PowerShell.
>
>

Para obter informações gerais sobre o Cofre de Chaves do Azure, consulte o artigo [O que é o Cofre de Chaves do Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, tem de ter Olá seguintes:

* Um cofre de chaves que tiver utilizado.  
* Azure PowerShell, **versão mínima 1.0.1**. tooinstall Azure PowerShell e associá-lo à sua subscrição do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Se já tiver instalado o Azure PowerShell e não souber a versão de Olá, a partir da consola do Azure PowerShell Olá, escreva `(Get-Module azure -ListAvailable).Version`.  
* Armazenamento suficiente no Azure para os seus registos do Cofre de Chaves.

## <a id="connect"></a>Ligar a subscrições tooyour
Iniciar uma sessão do Azure PowerShell e inicie sessão tooyour conta do Azure com Olá os seguintes comandos:  

    Login-AzureRmAccount

Na janela de pop-up do browser de Olá, introduza o nome de utilizador da conta do Azure e a palavra-passe. Azure PowerShell irá obter todas as subscrições de Olá que estão associadas esta conta e, por predefinição, utiliza Olá primeiro.

Se tiver várias subscrições, poderá ter toospecify uma definição específica que foi utilizado toocreate seu Cofre de chaves do Azure. Escreva Olá subscrições de Olá toosee da sua conta os seguintes:

    Get-AzureRmSubscription

Em seguida, toospecify Olá subscrição associado ao seu Cofre de chaves que irá registar, tipo:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> Isto é um passo importante e especialmente útil se tiver várias subscrições associadas à sua conta. Poderá receber um erro tooregister insights se este passo é ignorado.
>   
>

Para obter mais informações sobre como configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a id="storage"></a>Criar uma nova conta de armazenamento para os seus registos
Apesar de poder utilizar uma conta de armazenamento existente para os seus registos, vamos criar uma nova conta de armazenamento que serão os registos do cofre tooKey dedicado. Para sua comodidade que poderemos ter toospecify isto mais tarde, iremos guardar Olá detalhes numa variável designada **sa**.

Para facilitar ainda mais a gestão, também iremos utilizar Olá mesmo grupo de recursos como Olá que contém o nosso Cofre de chaves. De Olá [tutorial de introdução](key-vault-get-started.md), este grupo de recursos será designado **ContosoResourceGroup** e continuaremos toouse Olá Oriental como localização. Substitua estes valores pelos seus próprios valores, conforme aplicável:

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Se decidir toouse uma conta de armazenamento existente, tem de utilizar Olá mesma subscrição, como o seu Cofre de chaves e devem utilizar o modelo de implementação do Resource Manager Olá, em vez de modelo de implementação clássica Olá.
>
>

## <a id="identify"></a>Identificar o Cofre de chaves Olá para os seus registos
No nosso tutorial de introdução, o nome do nosso Cofre de chaves era **ContosoKeyVault**, por isso, continuaremos toouse que atribua um nome e armazenar os detalhes de Olá numa variável designada **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Ativar registo
tooenable registo para o Cofre de chaves, iremos utilizar o cmdlet Olá Set-AzureRmDiagnosticSetting, juntamente com variáveis de Olá criadas para a nossa nova conta de armazenamento e o nosso Cofre de chaves. Também iremos definir Olá **-ativado** sinalizador demasiado**$true** e defina Olá categoria tooAuditEvent (Olá única categoria para o registo do Cofre de chaves):

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

Olá resultado inclui:

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Isto confirma que o registo está agora ativado para o seu Cofre de chaves, guardar a conta de armazenamento de tooyour de informações.

Opcionalmente, pode também definir a política de retenção dos seus registos de forma a que os registos mais antigos sejam eliminados automaticamente. Por exemplo, definir a política de retenção utilizar **- RetentionEnabled** sinalizador demasiado**$true** e defina **- RetentionInDays** parâmetro demasiado**90** para Se os registos com mais de 90 dias serão automaticamente eliminados.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

O que é registado:

* Todos os pedidos de REST API autenticados são registados, o que inclui os pedidos falhados resultantes de erros de permissões de acesso, erros do sistema ou pedidos incorretos.
* Operações na chave de Olá próprio, o que inclui a criação, eliminação, políticas de acesso do Cofre de chaves de definição, cofre e atualizar os atributos do Cofre de chaves, tais como etiquetas.
* Operações sobre chaves e segredos no Olá Cofre de chaves, que inclui a criação, modificação ou eliminação dessas chaves ou segredos; operações como assinar, verificar, encriptar, desencriptar, moldar e desenrolar chaves, obter segredos, listar e segredos e as respetivas versões.
* Pedidos não autenticados que resultam numa resposta 401. Por exemplo, pedidos que não têm um token de portador ou pedidos incorretamente formulados ou expirados ou com um token inválido.  

## <a id="access"></a>Aceder aos seus registos
Os registos do Cofre de chaves são armazenados na Olá **insights-logs-auditevent** contentor na conta de armazenamento de Olá que indicou. toolist todos os blobs Olá neste contentor, escreva:

Em primeiro lugar, crie uma variável de nome do contentor Olá. Este será utilizado ao longo do resto Olá Olá percurso através de.

    $container = 'insights-logs-auditevent'

toolist todos os blobs Olá neste contentor, escreva:

    Get-AzureStorageBlob -Container $container -Context $sa.Context
saída de Olá procurará toothis algo semelhante:

**Uri do contentor: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Nome**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Como pode neste resultado, os blobs de Olá seguem uma convenção de nomenclatura: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**

valores de data e hora Olá utilizam o UTC.

Como hello mesma conta de armazenamento pode ser utilizados toocollect registos para vários recursos, hello ID de recurso completo no nome do blob Olá é tooaccess muito útil ou blobs de Olá apenas de transferência que precisa. Mas antes de podermos fazer isso, teremos primeiro de saber como toodownload Olá todos os blobs.

Em primeiro lugar, crie um Olá de toodownload pasta blobs. Por exemplo:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

Em seguida, obtenha uma lista de todos os blobs:  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Encaminhe esta lista através de blobs de Olá toodownload de 'Get-AzureStorageBlobContent' para a nossa pasta de destino:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

Quando executar este segundo comando, Olá  **/**  delimitador dos nomes de blob Olá criar uma estrutura de pasta completa sob a pasta de destino Olá, e esta estrutura serão utilizados toodownload e arquivo Olá os blobs como ficheiros.

tooselectively transferir blobs, utilize carateres universais. Por exemplo:

* Se tiver vários cofres de chaves e pretender obter registos toodownload de apenas um cofre de chaves, designado CONTOSOKEYVAULT3:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Se tiver vários grupos de recursos e pretende registos toodownload para apenas um grupo de recursos, utilize `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Se quiser toodownload todos os registos de Olá mês Olá de Janeiro de 2016, utilize `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Está agora pronto toostart observar o que está a ser Olá registos. Mas antes dessa, dois parâmetros adicionais para que poderá ter tooknow Get-AzureRmDiagnosticSetting:

* Estado de Olá tooquery das definições de diagnóstico para o seu recurso do Cofre de chaves:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* registo de toodisable para o recurso do Cofre de chaves:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Interpretar os registos do seu Cofre de Chaves
Os blobs individuais são armazenadas como texto, formatados como um blob JSON. Esta é uma entrada de registo de exemplo em execução `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Olá tabela seguinte lista os nomes de campo Olá e descrições.

| Nome do campo | Descrição |
| --- | --- |
| hora |Data e hora (UTC). |
| resourceId |ID do Recurso do Azure Resource Manager Para os registos do Cofre de chaves, o que é sempre ID de recurso do Olá Cofre de chaves. |
| operationName |Nome da operação de Olá, conforme documentada na tabela seguinte Olá. |
| operationVersion |Esta é a versão de REST API de Olá solicitada pelo cliente de Olá. |
| categoria |Para os registos do Cofre de chaves, AuditEvent é Olá único valor disponível. |
| resultType |Resultado do pedido de API REST. |
| resultSignature |Estado de HTTP. |
| resultDescription |Descrição adicional sobre o resultado de Olá, quando disponível. |
| durationMs |Tempo que demorou pedido de REST API do tooservice Olá, em milissegundos. Não inclui latência de rede Olá, pelo que o tempo de Olá que medir do lado do cliente de Olá poderá não corresponder a este período de tempo. |
| callerIpAddress |Endereço IP do cliente de Olá que efetuou o pedido de Olá. |
| correlationId |Um GUID opcional que hello do cliente pode passar toocorrelate registos do lado do cliente com os registos do lado do serviço (Cofre de chaves). |
| identidade |Identidade do token de Olá apresentado aquando do pedido de API de REST Olá. Trata-se geralmente de um "utilizador", um "principal de serviço" ou uma combinação "utilizador + appId", como no caso de um pedido resultante de um cmdlet do Azure PowerShell. |
| propriedades |Este campo irá conter diversas informações com base na operação de Olá (Oeprationname). Na maioria dos casos, contém informações de cliente (Olá cadeia useragent transmitida pelo cliente de Olá), Olá URI exato de pedido de REST API e código de estado HTTP. Além disso, quando um objeto é devolvido como resultado de um pedido (por exemplo, KeyCreate ou VaultGet), também irá conter Olá URI de chave (como "id"), o cofre do URI ou o segredo do URI. |

Olá **operationName** valores dos campos estão no formato ObjectVerb. Por exemplo:

* Todas as operações do Cofre de chaves têm Olá ' cofre`<action>`' Formatar, tais como `VaultGet` e `VaultCreate`.
* Todas as operações de chaves têm Olá ' chave`<action>`' Formatar, tais como `KeySign` e `KeyList`.
* Todas as operações de segredo têm Olá ' segredo`<action>`' Formatar, tais como `SecretGet` e `SecretListVersions`.

Olá, a tabela seguinte lista o operationName Olá e comando REST API correspondente.

| operationName | Comando API REST |
| --- | --- |
| Autenticação |Através do ponto final do Azure Active Directory |
| VaultGet |[Obter informações sobre um cofre de chaves](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Criar ou atualizar um cofre de chaves](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Eliminar um cofre de chaves](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Atualizar um cofre de chaves](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Lista todos os cofres de chaves num grupo de recursos](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Criar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Obter informações sobre uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Importar uma chave para um cofre](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Fazer uma cópia de segurança de uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx). |
| KeyDelete |[Eliminar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Restaurar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Assinar com uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Verificar com uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Moldar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Desenrolar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Encriptar com uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Desencriptar com uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Atualizar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Lista Olá chaves num cofre](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Lista as versões de Olá de uma chave](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Criar um segredo](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Obter um segredo](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Atualizar um segredo](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Eliminar um segredo](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Lista os segredos num cofre](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Lista as versões de um segredo](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Utilizar o Log Analytics

Pode utilizar solução Cofre de chaves do Azure de Olá tooreview de análise de registos do Azure chave de cofre AuditEvent registos. Para obter mais informações, incluindo como tooset esta cópia de segurança, consulte [solução Cofre de chaves do Azure na análise de registos](../log-analytics/log-analytics-azure-key-vault.md). Este artigo também contém instruções se precisar de toomigrate da solução Cofre de chaves antiga Olá que foi fornecida durante a pré-visualização de análise de registos de Olá, onde primeiro encaminhados sua tooan registos de conta de armazenamento do Azure e configurado tooread de análise de registos a partir daí.

## <a id="next"></a>Passos seguintes
Para um tutorial que utiliza o Cofre de Chaves do Azure numa aplicação Web, consulte o artigo [Utilizar o Cofre de Chaves do Azure a partir de uma Aplicação Web](key-vault-use-from-web-application.md).

Para as referências de programação, consulte [Olá guia para programadores do Cofre de chaves do Azure](key-vault-developers-guide.md).

Para obter uma lista dos cmdlets do Azure PowerShell 1.0 para o Cofre de Chaves do Azure, consulte o artigo [Cmdlets do Cofre de Chaves do Azure](/powershell/module/azurerm.keyvault/#key_vault).

Para um tutorial de rotação da chave e auditoria do registo com o Cofre de chaves do Azure, consulte [como toosetup Cofre de chaves com final tooend chave auditoria e rotação](key-vault-key-rotation-log-monitoring.md).
