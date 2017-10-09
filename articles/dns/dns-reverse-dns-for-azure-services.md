---
title: "aaaReverse DNS para serviços do Azure | Microsoft Docs"
description: "Saiba como tooconfigure inverso pesquisas de DNS para serviços alojados no Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Configurar o DNS inversa para serviços alojados no Azure

Este artigo explica como tooconfigure inverso pesquisas de DNS para serviços alojados no Azure.

Os serviços no Azure utilizar endereços IP atribuído pelo Azure e pertencente à Microsoft. Estes registos DNS inversas (registos PTR) tem de ser criados no Olá correspondentes pertencentes à Microsoft zonas DNS inversas pesquisa. Este artigo explica como toodo isto.

Este cenário deve não ser confundido com capacidade de Olá demasiado[alojar Olá zonas DNS inversas pesquisa para os intervalos IP atribuídos no DNS do Azure](dns-reverse-dns-hosting.md). Neste caso, os intervalos de IP Olá representados por zona de pesquisa inversa de Olá devem ser atribuídos tooyour organização, normalmente pelo seu ISP.

Antes de ler este artigo, deve estar familiarizado com esta [descrição geral do DNS inversa e de suporte no Azure](dns-reverse-dns-overview.md).

O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).
* No modelo de implementação do Resource Manager Olá, recursos de computação (por exemplo, as máquinas virtuais, conjuntos de dimensionamento de máquina virtual ou clusters de Service Fabric) são expostos através de um recurso de PublicIpAddress. Pesquisas inversas de DNS estão configuradas ao utilizar a propriedade 'ReverseFqdn' Olá Olá PublicIpAddress.
* No modelo de implementação clássica Olá, recursos de computação são expostos utilizar serviços em nuvem. Pesquisas inversas de DNS estão configuradas ao utilizar a propriedade 'ReverseDnsFqdn' Olá Olá serviço em nuvem.

DNS inversa não é atualmente suportado para Olá App Service do Azure.

## <a name="validation-of-reverse-dns-records"></a>Validação de registos DNS inversas

Uma linha de terceiros não deve ser capaz de toocreate inversas registos DNS para os seus domínios DNS de tooyour de mapeamento de serviço do Azure. tooprevent, Azure só permite a criação de Olá de um registo DNS inverso em que o nome de domínio especificado no registo DNS inverso Olá é seja resolvido para Olá nome DNS ou endereço IP de um PublicIpAddress ou uma nuvem de serviço no Olá mesmo ou Olá igual à subscrição do Azure.

Esta validação só é executada quando o registo DNS inverso Olá é definido ou modificado. Não é efetuada a validação de reativação periódica.

Por exemplo: Suponhamos Olá PublicIpAddress recurso tem contosoapp1.northus.cloudapp.azure.com de nome DNS Olá e endereço IP 23.96.52.53. Olá ReverseFqdn para Olá que publicipaddress podem ser especificados como:
* nome DNS de Olá para Olá PublicIpAddress, contosoapp1.northus.cloudapp.azure.com
* Olá de nome DNS para um PublicIpAddress diferentes no Olá mesma subscrição, tais como contosoapp2.westus.cloudapp.azure.com
* Um intuitivos nomes DNS, tais como app1.contoso.com, desde que este nome é *primeiro* configurado como um CNAME toocontosoapp1.northus.cloudapp.azure.com ou tooa PublicIpAddress diferentes no Olá mesma subscrição.
* Um intuitivos nomes DNS, tais como app1.contoso.com, desde que este nome é *primeiro* configurado como um endereço IP de registo toohello A 23.96.52.53 ou endereço IP toohello um PublicIpAddress diferentes no Olá mesma subscrição.

Olá mesmas restrições aplicam-se tooreverse DNS para serviços em nuvem.


## <a name="reverse-dns-for-publicipaddress-resources"></a>Inversa de DNS para recursos PublicIpAddress

Esta secção fornece instruções detalhadas sobre como tooconfigure inversa DNS para os recursos de PublicIpAddress no modelo de implementação do Resource Manager Olá, utilizando o Azure PowerShell, CLI do Azure 1.0 ou 2.0 de CLI do Azure. Configurar o DNS inversa PublicIpAddress recursos não é atualmente suportada através de Olá portal do Azure.

Azure atualmente suporta inversa DNS apenas para recursos IPv4 PublicIpAddress. Não é suportada para IPv6.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Adicionar inversa de DNS de tooan existente PublicIpAddresses

#### <a name="powershell"></a>PowerShell

tooadd existente PublicIpAddress inversa tooan DNS:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd inverso tooan DNS existente PublicIpAddress que já não tem um nome DNS, também tem de especificar um nome DNS:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>CLI do Azure 1.0

tooadd existente PublicIpAddress inversa tooan DNS:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd inverso tooan DNS existente PublicIpAddress que já não tem um nome DNS, também tem de especificar um nome DNS:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

tooadd existente PublicIpAddress inversa tooan DNS:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd inverso tooan DNS existente PublicIpAddress que já não tem um nome DNS, também tem de especificar um nome DNS:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Criar um endereço IP público com o DNS inversa

toocreate um PublicIpAddress novo com a propriedade Olá inversa DNS já especificado:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>CLI do Azure 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Vista DNS inverso para um PublicIpAddress existente

Olá tooview configurados valor para um PublicIpAddress existente:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>CLI do Azure 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Remover DNS inversa de endereços IP públicos existentes

tooremove uma propriedade DNS inversa de um PublicIpAddress existente:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>CLI do Azure 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Configurar inversa de DNS para serviços em nuvem

Esta secção fornece instruções detalhadas sobre como tooconfigure inversa DNS para serviços em nuvem no modelo de implementação clássica de Olá, com o Azure PowerShell. Configurar o inversa de DNS para serviços em nuvem não é suportada através do portal do Azure, Olá da CLI do Azure 1.0 ou 2.0 de CLI do Azure.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Adicionar serviços de Cloud de tooexisting DNS inversa

tooadd um tooan de registo DNS inverso existente serviço em nuvem:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Criar um serviço em nuvem com o DNS inversa

um novo serviço em nuvem com a propriedade Olá inversa DNS especificada já toocreate:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Vista DNS inversa para serviços de Cloud existente

tooview Olá inversa DNS propriedade para um serviço em nuvem existente:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Remover inversa de DNS dos serviços de nuvem existente

tooremove uma propriedade DNS inversa de um serviço em nuvem existente:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>FAQ

### <a name="how-much-do-reverse-dns-records-cost"></a>Quanto inverter o custo de registos DNS?

Se estiverem livres!  Não há sem custos adicionais para inversas de DNS de registos ou consultas.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>Será o meu resolve de registos DNS inversa de Olá internet?

Sim. Depois de definir a propriedade DNS inversa Olá para o serviço do Azure, Azure gere todas as delegações do Olá DNS e zonas DNS necessário resolve tooensure inverter o registo DNS para todos os utilizadores de Internet.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>Registos DNS inversas predefinida são criados para os meus serviços do Azure?

Não. Inversa de DNS é uma funcionalidade de recusa. Sem predefinição inversas de DNS de registos são criados se optar por não tooconfigure-los.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>O que é o formato de Olá para o nome de domínio completamente qualificado (FQDN) do Olá?

Estão especificados na ordem de pesquisa direta e FQDNs tem de ser terminadas por um ponto (por exemplo, "app1.contoso.com.").

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>O que acontece se a verificação de validação de Olá para Olá inversa DNS posso especificadas falha?

Onde hello inversa DNS validação verificação falha, falha Olá operação tooconfigure Olá inverso registo DNS. Corrija o valor DNS inversa Olá conforme necessário e repita.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Pode configurar inversa de DNS para o App Service do Azure?

Não. DNS inversa não é suportada para Olá App Service do Azure.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>Pode configurar vários registos DNS inversas para o meu serviço do Azure?

Não. Azure suporta um único registo DNS inverso para cada serviço de nuvem do Azure ou um PublicIpAddress.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>Pode configurar inversa de DNS para recursos de IPv6 PublicIpAddress?

Não. Azure atualmente suporta inversa DNS apenas para IPv4 PublicIpAddress recursos e serviços em nuvem.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>Pode enviar mensagens de correio eletrónico tooexternal domínios dos meus serviços de computação do Azure?

Não. [Serviços de computação do Azure não suportam domínios de tooexternal enviar mensagens de correio eletrónico](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre inversa DNS, consulte [pesquisa inversa de DNS em Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Saiba como demasiado[zona de pesquisa inversa de Olá de anfitrião para o intervalo de IP ISP atribuído no DNS do Azure](dns-reverse-dns-for-azure-services.md).

