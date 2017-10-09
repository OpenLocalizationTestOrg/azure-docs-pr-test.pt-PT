---
title: aaaAzure arquitetura de conectividade da base de dados SQL | Microsoft Docs
description: "Este documento explica Olá Azure SQLDB conectividade arquitetura no Azure ou a partir de fora do Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Arquitetura de conectividade de base de dados SQL do Azure 

Este artigo explica a arquitetura de conectividade de base de dados do Azure SQL Olá e explica a forma como os diferentes componentes Olá funcionarem toodirect tráfego tooyour instância SQL Database do Azure. Estes componentes de conectividade da SQL Database do Azure funcionarem toohello de tráfego de rede toodirect da base de dados do Azure com os clientes ligar a partir de dentro do Azure e com os clientes ligar a partir de fora do Azure. Este artigo fornece também toochange de amostras de script como ocorre a conectividade e considerações de Olá relacionadas com definições de conetividade do toochanging Olá predefinido. Se existirem quaisquer perguntas depois de ler este artigo, entre em contacto com Dhruv em dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Arquitetura de conectividade

Olá diagrama a seguir fornece uma descrição geral de alto nível de Olá arquitetura de conectividade da SQL Database do Azure. 

![Descrição geral da arquitetura](./media/sql-database-connectivity-architecture/architecture-overview.png)


Olá passos seguintes descrevem como uma ligação é estabelecida tooan SQL database do Azure através de Olá SQL Database do Azure software Balanceador de carga (SLB) e o gateway do Olá SQL Database do Azure.

- Os clientes no Azure ou fora do Azure ligam toohello SLB, que tem um endereço IP público e escuta na porta 1433.
- Olá SLB direciona o gateway do tráfego toohello SQL Database do Azure.
- gateway de Olá redireciona o tráfego de Olá toohello middleware de proxy correta.
- Olá proxy middleware redireciona Olá tráfego toohello adequado SQL database do Azure.

> [!IMPORTANT]
> Cada um destes componentes tem ataques denial of protection service (DDoS distribuídos) incorporada na rede de Olá e a camada de aplicação de Olá.
>

## <a name="connectivity-from-within-azure"></a>Conectividade no Azure

Se estiver a ligar no Azure, as suas ligações tem uma política de ligação do **redirecionar** por predefinição. Uma política do **redirecionar** significa que as ligações após a conclusão da sessão TCP Olá toohello estabelecida SQL database do Azure, sessão de cliente Olá, em seguida, redirecionado toohello proxy middleware com um alteração toohello destino IP virtual do que um Olá SQL Database do Azure gateway toothat de Olá middleware de proxy. Depois disso, todos os pacotes subsequentes fluir diretamente através do middleware de proxy Olá, ignorando o gateway do Olá SQL Database do Azure. Olá seguinte diagrama ilustra o fluxo de tráfego.

![Descrição geral da arquitetura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Conectividade de fora do Azure

Se estiver a ligar a partir de fora do Azure, as suas ligações tem uma política de ligação do **Proxy** por predefinição. Uma política do **Proxy** Olá, significa que sessão TCP Olá é estabelecida através do gateway da SQL Database do Azure de Olá e todos os pacotes subsequentes fluxo através do gateway. Olá seguinte diagrama ilustra o fluxo de tráfego.

![Descrição geral da arquitetura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Endereços de IP do gateway de base de dados SQL do Azure

tooconnect tooan SQL database do Azure a partir dos recursos no local, terá de gateway de SQL Database do Azure de toohello de tráfego de rede de saída de tooallow para sua região do Azure. As suas ligações aceda apenas através do gateway de Olá ao ligar-se no modo de Proxy, que é a predefinição de Olá quando ligar a partir de recursos no local.

Olá listas de tabela a seguir Olá IPs primária e secundária do gateway de base de dados do Azure SQL Olá para todas as regiões de dados. Para algumas regiões, existem dois endereços IP. Estas regiões, endereço IP primário Olá é o endereço IP atual Olá do gateway de Olá e segundo endereço IP Olá é um endereço IP de ativação pós-falha. o endereço de ativação pós-falha de Olá é Olá endereço toowhich pode mover a servidor tookeep Olá serviço disponibilidade elevada. Para estas regiões, recomendamos que permitem a saída tooboth endereços IP Olá. endereço IP segundo Olá pertencente à Microsoft e não escutar todos os serviços até ser ativado através de ligações de tooaccept da SQL Database do Azure.

| Nome da Região | Endereço IP primário | Endereço IP secundário |
| --- | --- |--- |
| Leste da Austrália | 191.238.66.109 | 13.75.149.87 |
| Sudeste da Austrália | 191.239.192.109 | 13.73.109.251 |
| Sul do Brasil | 104.41.11.5 | |    
| Canadá Central | 40.85.224.249 | |    
| Leste do Canadá | 40.86.226.166 | |
| EUA Central | 23.99.160.139 | 13.67.215.62 |
| Ásia Oriental | 191.234.2.139 | 52.175.33.150 |
| EUA Leste 1 | 191.238.6.43 | 40.121.158.30 |
| EUA Leste 2 | 191.239.224.107 | 40.79.84.180 |
| Índia Central | 104.211.96.159  | |   
| Índia do Sul | 104.211.224.146  | |
| Índia Ocidental | 104.211.160.80 | |
| Leste do Japão | 191.237.240.43 | 13.78.61.196 |
| Oeste do Japão | 191.238.68.11 | 104.214.148.156 |
| Coreia Central | 52.231.32.42 | |
| Coreia do Sul | 52.231.200.86 |  |
| EUA Centro-Norte | 23.98.55.75 | 23.96.178.199 |
| Europa do Norte | 191.235.193.75 | 40.113.93.91 |
| EUA Centro-Sul | 23.98.162.75 | 13.66.62.124 |
| Sudeste Asiático | 23.100.117.95 | 104.43.15.0 |
| Norte do Reino Unido | 13.87.97.210 | |
| Sul do RU 1 | 51.140.184.11 | |    
| Sul do Reino Unido 2 | 13.87.34.7 | |
| Reino Unido Oeste | 51.141.8.11  | |
| EUA Centro-Oeste | 13.78.145.25 | |
| Europa Ocidental | 191.237.232.75 | 40.68.37.158 |
| EUA oeste 1 | 23.99.34.75 | 104.42.238.205 |
| EUA Oeste 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Alterar a política de ligação de SQL Database do Azure

Olá toochange política de ligação de SQL Database do Azure para um servidor de base de dados do Azure SQL, utilize Olá [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Se a política de ligação for definida demasiado**Proxy**, todos os pacotes de fluxo através do gateway da SQL Database do Azure de Olá de rede. Para esta definição, terá de IP do gateway tooallow tooonly saída Olá SQL Database do Azure. Utilizar uma definição de **Proxy** tem a latência mais que uma definição de **redirecionar**. 
- Se a política de ligação é **redirecionar**, todos os pacotes de rede diretamente fluxo toohello middleware proxy. Para esta definição, terá de tooallow saída toomultiple IPs. 

## <a name="script-toochange-connection-settings"></a>Definições de ligação do script toochange

> [!IMPORTANT]
> Este script requer Olá [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).
>

Olá script do PowerShell a seguir mostra como toochange Olá política de ligação.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Passos seguintes

- Para obter informações sobre como toochange Olá política de ligação de SQL Database do Azure para um servidor de base de dados do Azure SQL, consulte [Create ou política de ligação do servidor de atualização utilizando Olá REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- Para informações sobre o comportamento de ligação de SQL Database do Azure para clientes que utilizam ADO.NET 4.5 ou uma versão posterior, consulte [portas para além de 1433 para ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
- Para informações de descrição geral do desenvolvimento de aplicações gerais, consulte [descrição geral do desenvolvimento de aplicações de base de dados do SQL Server](sql-database-develop-overview.md).
