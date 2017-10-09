---
title: aaaUsing PowerShell toomanage Traffic Manager no Azure | Microsoft Docs
description: "Com o PowerShell para o Gestor de tráfego com o Azure Resource Manager"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>Utilizar o PowerShell toomanage Gestor de tráfego

O Azure Resource Manager é Olá a interface de gestão preferenciais para serviços no Azure. Perfis do Traffic Manager do Azure podem ser geridos através de APIs do Azure Resource Manager e as ferramentas.

## <a name="resource-model"></a>Modelo de recursos

Traffic Manager do Azure está configurado com uma coleção de definições denominado um perfil do Traffic Manager. Este perfil contém as definições de DNS, as definições de encaminhamento de tráfego, ponto final de definições de monitorização e uma lista de tráfego de toowhich pontos finais do serviço é encaminhada.

Cada perfil de Gestor de tráfego é representada por um recurso do tipo 'TrafficManagerProfiles'. Ao nível da API de REST Olá, Olá URI para cada perfil é:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Configurar o Azure PowerShell

Estas instruções utilizam o Microsoft Azure PowerShell. Olá seguinte artigo explica como tooinstall e configurar o Azure PowerShell.

* [Como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview)

Exemplos de Olá deste artigo partem do princípio de que tem um grupo de recursos existente. Pode criar um grupo de recursos com Olá os seguintes comandos:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> O Azure Resource Manager requer que todos os grupos de recursos tem uma localização. Esta localização é utilizada como predefinição de Olá de recursos criados nesse grupo de recursos. No entanto, uma vez que os recursos de perfil do Gestor de tráfego são globais, não regionais, escolha de Olá de localização do grupo de recursos não tem impacto no Gestor de tráfego do Azure.

## <a name="create-a-traffic-manager-profile"></a>Criar um perfil de Gestor de tráfego

toocreate um perfil do Traffic Manager, utilize Olá `New-AzureRmTrafficManagerProfile` cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Olá, a tabela seguinte descreve os parâmetros de Olá:

| Parâmetro | Descrição |
| --- | --- |
| Nome |nome do recurso de Olá para Olá recursos de perfil do Gestor de tráfego. Os perfis do Olá mesmo grupo de recursos tem de ter nomes exclusivos. Este nome está separado do nome DNS Olá utilizada para consultas DNS. |
| resourceGroupName |nome de Olá do Olá recursos que contém Olá perfil recurso do grupo. |
| TrafficRoutingMethod |Especifica Olá encaminhamento de tráfego método utilizado toodetermine o ponto final é devolvido em resposta uma consulta DNS. Os valores possíveis são 'Desempenho', 'Weighted' ou 'Priority'. |
| RelativeDnsName |Especifica a parte do nome de anfitrião Olá Olá DNS do nome de fornecido por este perfil do Traffic Manager. Este valor é combinado com o nome de domínio DNS de Olá utilizada pelo Gestor de tráfego do Azure tooform Olá nome domínio completamente qualificado (FQDN) do perfil de Olá. Por exemplo, definir o valor de Olá da "contoso" fica 'contoso.trafficmanager.net'. |
| VALOR DE TTL |Especifica Olá DNS Time-to-Live (TTL), em segundos. Este valor de TTL informa as resoluções Local DNS Olá e clientes DNS quanto toocache, as respostas DNS, para este perfil do Traffic Manager. |
| MonitorProtocol |Especifica o estado de funcionamento do Olá protocolo toouse toomonitor ponto final. Os valores possíveis são 'HTTP' e 'HTTPS'. |
| MonitorPort |Especifica Olá a porta TCP utilizada toomonitor estado de funcionamento do ponto final. |
| MonitorPath |Especifica o nome de domínio de ponto final do Olá caminho relativo toohello utilizado tooprobe para Estado de funcionamento do ponto final. |

Olá cmdlet cria um perfil do Traffic Manager no Azure e devolve um objeto tooPowerShell correspondente do perfil. Neste momento, o perfil de Olá não contém quaisquer pontos finais. Para obter mais informações sobre como adicionar o perfil do Gestor de tráfego de tooa de pontos finais, consulte [adicionar pontos finais de Gestor de tráfego](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Obter um perfil do Traffic Manager

tooretrieve um objeto de perfil do Traffic Manager existente, utilize Olá `Get-AzureRmTrafficManagerProfle` cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Este cmdlet devolve um objeto de perfil do Traffic Manager.

## <a name="update-a-traffic-manager-profile"></a>Atualizar um perfil do Traffic Manager

Modificar perfis do Traffic Manager segue um processo do passo 3:

1. Obter Olá perfil utilizar `Get-AzureRmTrafficManagerProfile` ou utilizar o perfil de Olá devolvido pelo `New-AzureRmTrafficManagerProfile`.
2. Modificar o perfil de Olá. Pode adicionar e remover pontos finais ou altere os parâmetros do ponto final ou o perfil. Estas alterações são operações offline. Só está a alterar o objeto local do Olá na memória que representa o perfil de Olá.
3. Consolidar as alterações utilizando Olá `Set-AzureRmTrafficManagerProfile` cmdlet.

Todas as propriedades de perfil podem ser alteradas, exceto RelativeDnsName do perfil de Olá. toochange Olá RelativeDnsName, tem de eliminar o perfil e um novo perfil com um novo nome.

Olá seguinte o exemplo demonstra como toochange Olá TTL do perfil:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Existem três tipos de pontos finais do Gestor de tráfego:

1. **Pontos finais Azure** são serviços alojados no Azure
2. **Pontos finais externos** são serviços alojados fora do Azure
3. **Pontos finais de aninhada** são utilizados tooconstruct aninhada hierarquias de perfis do Traffic Manager. Pontos finais aninhados ativar o encaminhamento de tráfego configurações avançadas para aplicações complexas.

Em três casos, é possível adicionar pontos finais de duas formas:

1. Através de um processo de passo 3 descrito anteriormente. Olá vantagem este método é que várias alterações de ponto final podem ser efetuadas numa única atualização.
2. Utilizando o cmdlet New-AzureRmTrafficManagerEndpoint de Olá. Este cmdlet adiciona um perfil de Gestor de tráfego existente do ponto final tooan numa única operação.

## <a name="adding-azure-endpoints"></a>Adicionar pontos finais Azure

Pontos finais Azure referenciam serviços alojados no Azure. São suportados dois tipos de pontos finais do Azure:

1. Aplicações Web do Azure
2. Recursos PublicIpAddress do Azure (o que podem ser anexado tooa-Balanceador de carga ou uma máquina virtual NIC). Olá PublicIpAddress tem de ter um nome DNS atribuído toobe utilizado no Traffic Manager.

Em cada caso:

* o serviço de Olá é especificado utilizando o parâmetro de 'targetResourceId' Olá de `Add-AzureRmTrafficManagerEndpointConfig` ou `New-AzureRmTrafficManagerEndpoint`.
* Olá 'Target' e 'EndpointLocation' são implícito por Olá TargetResourceId.
* A especificação de Olá 'Peso' é opcional. Ponderações só são utilizadas se o perfil de Olá é o método de encaminhamento de tráfego do toouse configurado Olá 'Weighted'. Caso contrário, são ignorados. Se for especificado, o valor de Olá tem de ser um número entre 1 e 1000. valor predefinido de Olá é '1'.
* Olá especificando 'Priority' é opcional. Prioridades só são utilizadas se o perfil de Olá é o método de encaminhamento de tráfego do toouse configurado Olá 'Priority'. Caso contrário, são ignorados. Os valores válidos são de 1 too1000 com valores mais baixos que indica uma prioridade mais alta. Se for especificado para um ponto final, tem de ser especificados para todos os pontos finais. Se for omitido, os valores predefinidos a partir de '1' são aplicados por ordem de Olá que estão listados pontos finais de Olá.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Exemplo 1: Adicionar pontos finais de aplicação Web utilizando`Add-AzureRmTrafficManagerEndpointConfig`

Neste exemplo, vamos criar um perfil de Gestor de tráfego e adicionar dois pontos finais de aplicação Web utilizando Olá `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: Adicionar um publicIpAddress utilizando o ponto final`New-AzureRmTrafficManagerEndpoint`

Neste exemplo, um recurso de endereço IP público é adicionado o perfil do Traffic Manager toohello. endereço IP público Olá tem de ter um nome DNS configurado e pode ser vinculado a qualquer um dos toohello NIC um VM ou tooa de Balanceador de carga.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Adicionar pontos finais externos

O tráfego Manager utiliza pontos finais externos toodirect tráfego tooservices alojados fora do Azure. Como com pontos finais do Azure, pontos finais externos podem ser adicionados a utilizar `Add-AzureRmTrafficManagerEndpointConfig` seguido `Set-AzureRmTrafficManagerProfile`, ou `New-AzureRMTrafficManagerEndpoint`.

Quando especificar pontos finais externos:

* nome de domínio de ponto final de Olá tem de ser especificado utilizando o parâmetro de 'Target' Olá
* Se for utilizado Olá método de encaminhamento de tráfego 'Desempenho', é necessário o Olá 'EndpointLocation'. Caso contrário, é opcional. valor de Olá tem de ser um [nome da região do Azure válido](https://azure.microsoft.com/regions/).
* Olá 'Importância' e 'Priority' é opcional.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: Adicionar pontos finais externos utilizando `Add-AzureRmTrafficManagerEndpointConfig` e`Set-AzureRmTrafficManagerProfile`

Neste exemplo, vamos criar um perfil de Gestor de tráfego, adicionar dois pontos finais externos e consolidar as alterações de Olá.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: Adicionar pontos finais externos utilizando`New-AzureRmTrafficManagerEndpoint`

Neste exemplo, vamos adicionar um perfil existente de tooan de ponto final externo. perfil de Olá for especificado utilizando nomes de grupos de recursos e perfil Olá.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>Adicionar pontos finais de 'Nested'

Cada perfil do Traffic Manager Especifica um único método de encaminhamento de tráfego. No entanto, existem cenários que necessitam de mais sofisticadas encaminhamento do tráfego de encaminhamento de Olá fornecido por um único perfil do Gestor de tráfego. Podem aninhar vantagens Olá de toocombine de perfis do Gestor de tráfego de mais do que um método de encaminhamento de tráfego. Perfis aninhados permitem-lhe toooverride Olá predefinido do Traffic Manager comportamento toosupport maior e mais complexas implementações de aplicações. Para obter mais exemplos, consulte [perfis do Gestor de tráfego aninhada](traffic-manager-nested-profiles.md).

Pontos finais aninhados estão configurados no perfil de principal de Olá, com um tipo de ponto final específico, 'NestedEndpoints'. Quando especificar pontos finais aninhados:

* ponto final de Olá tem de ser especificado utilizando o parâmetro de 'targetResourceId' Olá
* Se for utilizado Olá método de encaminhamento de tráfego 'Desempenho', é necessário o Olá 'EndpointLocation'. Caso contrário, é opcional. valor de Olá tem de ser um [nome da região do Azure válido](http://azure.microsoft.com/regions/).
* Olá 'Importância' e 'Priority' é opcional, como pontos finais do Azure.
* parâmetro de 'MinChildEndpoints' Olá é opcional. valor predefinido de Olá é '1'. Se o número de Olá de pontos finais disponíveis está abaixo deste limiar, o perfil de principal de Olá considera perfil subordinado de Olá 'degradado' e diverts tráfego toohello outros pontos finais no perfil do Olá principal.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: Adicionar pontos finais aninhados utilizando `Add-AzureRmTrafficManagerEndpointConfig` e`Set-AzureRmTrafficManagerProfile`

Neste exemplo, vamos perfis principais e subordinados do novo Gestor de tráfego, adicionar subordinado Olá como um principal de toohello aninhada endpoint e consolidar alterações de Olá.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

De uma forma abreviada neste exemplo, não foi possível adicionar não quaisquer outros pontos finais toohello subordinado ou principal perfis.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: Adicionar pontos finais aninhados utilizando`New-AzureRmTrafficManagerEndpoint`

Neste exemplo, vamos adicionar um perfil subordinado existente como um perfil existente de principal do ponto final aninhada tooan. perfil de Olá for especificado utilizando nomes de grupos de recursos e perfil Olá.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Atualizar um ponto final do Gestor de tráfego

Existem duas formas tooupdate um ponto final do Traffic Manager existente:

1. Obter a utilização de perfil de Gestor de tráfego de Olá `Get-AzureRmTrafficManagerProfile`, atualizar as propriedades do ponto final de Olá no perfil de Olá e confirmar as alterações de Olá utilizando `Set-AzureRmTrafficManagerProfile`. Este método tem a vantagem de Olá de que está a ser capaz de tooupdate mais do que um ponto final numa única operação.
2. Obter através de ponto final de Gestor de tráfego de Olá `Get-AzureRmTrafficManagerEndpoint`, atualizar propriedades do ponto final de Olá e confirmar as alterações de Olá utilizando `Set-AzureRmTrafficManagerEndpoint`. Este método é mais simples, uma vez que não requer a indexação numa matriz de pontos finais de Olá no perfil de Olá.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: Atualizar pontos finais utilizando `Get-AzureRmTrafficManagerProfile` e`Set-AzureRmTrafficManagerProfile`

Neste exemplo, vamos modificar prioridade Olá em dois pontos finais dentro de um perfil existente.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Exemplo 2: Atualizar um ponto final utilizando `Get-AzureRmTrafficManagerEndpoint` e`Set-AzureRmTrafficManagerEndpoint`

Neste exemplo, vamos modificar ponderação Olá de um único ponto final num perfil existente.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Ativar e desativar pontos finais e perfis

Gestor de tráfego permite que os pontos finais individuais toobe ativados e desativados, bem como permitir que a ativação e a desativação dos perfis de todos.
Estas alterações podem ser efetuadas pelos recursos de ponto final ou o perfil de Olá obter/atualizar/definição. toostreamline estas operações comuns, são também suportadas através de cmdlets dedicados.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Exemplo 1: Ativar e desativar um perfil do Traffic Manager

tooenable um perfil do Traffic Manager, utilize `Enable-AzureRmTrafficManagerProfile`. perfil de Olá pode ser especificada utilizando um objeto de perfil. Olá perfil pode ser transmitido um objeto através do pipeline de Olá ou utilizando Olá '-TrafficManagerProfile' parâmetro. Neste exemplo, especificamos perfil Olá pelo nome do grupo de recursos e perfil Olá.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable um perfil de Gestor de tráfego:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

Olá desativar AzureRmTrafficManagerProfile cmdlet solicita a confirmação. Esta linha de comandos pode ser suprimida utilizando Olá '-Force' parâmetro.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Exemplo 2: Ativar e desativar um ponto final do Gestor de tráfego

utilizar um ponto final do Gestor de tráfego, de tooenable `Enable-AzureRmTrafficManagerEndpoint`. Existem dois ponto final do Olá de toospecify formas

1. Utilizando um objeto de TrafficManagerEndpoint transmitido através do pipeline de Olá ou Olá '-TrafficManagerEndpoint' parâmetro
2. Utilizar o nome do ponto final Olá, tipo de ponto final, o nome de perfil e nome do grupo de recursos:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Da mesma forma, toodisable um ponto final do Gestor de tráfego:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Tal como com `Disable-AzureRmTrafficManagerProfile`, Olá `Disable-AzureRmTrafficManagerEndpoint` cmdlet solicita a confirmação. Esta linha de comandos pode ser suprimida utilizando Olá '-Force' parâmetro.

## <a name="delete-a-traffic-manager-endpoint"></a>Eliminar um ponto final do Gestor de tráfego

pontos finais individuais tooremove, utilize Olá `Remove-AzureRmTrafficManagerEndpoint` cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Este cmdlet solicita a confirmação. Esta linha de comandos pode ser suprimida utilizando Olá '-Force' parâmetro.

## <a name="delete-a-traffic-manager-profile"></a>Eliminar um perfil do Gestor de tráfego

toodelete um perfil do Traffic Manager, utilize Olá `Remove-AzureRmTrafficManagerProfile` cmdlet, especificando os nomes de grupos de recursos e perfil Olá:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Este cmdlet solicita a confirmação. Esta linha de comandos pode ser suprimida utilizando Olá '-Force' parâmetro.

Olá perfil toobe eliminado também pode ser especificada utilizando um objeto de perfil:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Também pode ser ligada esta sequência:

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Passos seguintes

[Gestor de tráfego de monitorização](traffic-manager-monitoring.md)

[Considerações de desempenho para o Gestor de Tráfego](traffic-manager-performance-considerations.md)
