---
title: aaaHosting inverso zonas de pesquisa DNS no DNS do Azure | Microsoft Docs
description: "Saiba como Olá de toohost de DNS do Azure toouse inverso zonas de pesquisa DNS para os intervalos de IP"
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>Aloja zonas de pesquisa inversas DNS no DNS do Azure

Este artigo explica como toohost Olá inverso zonas de pesquisa DNS para os intervalos IP atribuídos no DNS do Azure. intervalos IP Olá representados por zona de pesquisa inversa de Olá devem ser atribuídos tooyour organização, normalmente pelo seu ISP.

tooconfigure inversa de DNS para o IP pertencente ao Azure endereço atribuído tooyour serviço do Azure, consulte [Configurar pesquisa inversa Olá para endereços IP Olá alocado tooyour serviço do Azure](dns-reverse-dns-for-azure-services.md).

Antes de ler este artigo, deve estar familiarizado com esta [descrição geral do DNS inversa e de suporte no Azure](dns-reverse-dns-overview.md).

Este artigo explica Olá passos toocreate a primeira zona DNS de pesquisa inversa e registo utilizando Olá portal do Azure, Azure PowerShell, a CLI do Azure 1.0 ou 2.0 de CLI do Azure.

## <a name="create-a-reverse-lookup-dns-zone"></a>Criar uma zona de pesquisa inversa de DNS

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com)
1. No menu do Hub de Olá, clique em e clique em **novo** > **redes** > e, em seguida, clique em **zona DNS** tooopen Olá **zona de DNS criar**painel.

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. No Olá **zona DNS criar** painel, nome da sua zona DNS. nome de Olá da zona de Olá é crafted de forma diferente para os prefixos de IPv4 e IPv6. Utilizar qualquer uma das instruções Olá para [IPV4](#ipv4) ou [IPv6](#ipv6) tooname sua zona. Quando concluir clique **criar** zona de Olá toocreate.

### <a name="ipv4"></a>IPv4

nome de Olá de uma zona de pesquisa inversa IPv4 é baseado no intervalo IP Olá representa. Deve ser Olá seguinte formato: `<IPv4 network prefix in reverse order>.in-addr.arpa`. Para obter exemplos, consulte [descrição geral do DNS inversa e de suporte no Azure](dns-reverse-dns-overview.md#ipv4).

> [!NOTE]
> Quando criar classless zonas de pesquisa inversas de DNS no DNS do Azure, tem de utilizar um hífen (`-`) em vez de uma barra ('/ ') no nome da zona Olá.
>
> Por exemplo, para Olá IP intervalo 192.0.2.128/26, tem de utilizar `128-26.2.0.192.in-addr.arpa` como nome da zona Olá em vez de `128/26.2.0.192.in-addr.arpa`.
>
> Isto acontece porque, embora ambos são suportadas pelo normas DNS Olá, de zona DNS nomes que contêm barra Olá (`/`) carateres não são suportadas no DNS do Azure.

Olá exemplo seguinte mostra como toocreate 'Classe C' Inverter zona DNS com o nome `2.0.192.in-addr.arpa` no DNS do Azure através de Olá portal do Azure:

 ![criar a zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

Olá 'Localização do grupo de recursos' define a localização de Olá Olá grupo de recursos e não tem impacto na zona DNS Olá. localização de zona DNS Olá é sempre 'global' e não é apresentada.

Olá exemplos seguintes mostram como toocomplete esta tarefa com o Azure PowerShell e Olá CLI do Azure:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI do Azure 1.0

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

Olá nome de uma zona de pesquisa inversa IPv6 devem ter Olá seguinte formato: `<IPv6 network prefix in reverse order>.ip6.arpa`.  Para obter exemplos, consulte [descrição geral do DNS inversa e de suporte no Azure](dns-reverse-dns-overview.md#ipv6).


Olá exemplo seguinte mostra como toocreate uma zona de pesquisa DNS inversa IPv6 com o nome `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` no DNS do Azure através de Olá portal do Azure:

 ![criar a zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

Olá 'Localização do grupo de recursos' define a localização de Olá Olá grupo de recursos e não tem impacto na zona DNS Olá. localização de zona DNS Olá é sempre 'global' e não é apresentada.

Olá exemplos seguintes mostram como toocomplete esta tarefa com o Azure PowerShell e Olá CLI do Azure:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>Delegar a uma zona de pesquisa inversa DNS

Ter criado a sua zona de pesquisa inversa DNS, tem de garantir que zona Olá é delegada da zona de principal de Olá. Delegação de DNS permite Olá nome resolução processo toofind Olá servidores de nomes DNS que aloja a zona de pesquisa inversa DNS. Isto permite que esses servidores tooanswer DNS inversas consultas de nome para endereços IP Olá no seu intervalo de endereços.

Para zonas de pesquisa direta, o processo de Olá de delegação de uma zona DNS é descrito em [delegar a tooAzure de domínio DNS](dns-delegate-domain-azure-dns.md). Funciona a delegação de zonas de pesquisa inversa Olá mesma forma. Step-by-Olá única diferença é que tem de servidores de nomes de Olá tooconfigure com Olá ISP que forneceu o intervalo de IP, em vez da sua entidade de registo de nome de domínio.

## <a name="create-a-dns-ptr-record"></a>Criar um registo DNS PTR

### <a name="ipv4"></a>IPv4

Olá seguinte exemplo explica Olá processo de criação de um registo PTR numa zona DNS inversa no DNS do Azure. Para outros tipos de registos e registos existentes toomodify, consulte [registos DNS de gerir e conjuntos de registos utilizando o portal do Azure de Olá](dns-operations-recordsets-portal.md).

1.  Na parte superior de Olá de Olá **zona DNS** painel, selecione **+ conjunto de registos** tooopen Olá **adicionar conjunto de registos** painel.

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. No Olá **adicionar conjunto de registos** painel. 
1. Selecione **PTR** do registo de Olá "**tipo**" menu.  
1. Olá nome do conjunto de registos de Olá para um registo PTR tem toobe restante Olá Olá endereço IPv4 na ordem inversa. Neste exemplo, hello três primeiros octetos já estão povoados como parte do nome da zona Olá (.2.0.192). Por conseguinte, apenas Olá último octeto é fornecido no campo de nome de Olá. Por exemplo, pode dar nome do conjunto de registos "**15**" para um recurso cujo endereço IP é 192.0.2.15.  
1. No Olá "**nome de domínio**" campo, introduza o nome de domínio completamente qualificado (FQDN) Olá do recurso de Olá Olá IP a utilizar.
1. Selecione **OK** em Olá parte inferior da registo DNS do Olá painel toocreate Olá.

 ![adicionar o conjunto de registos](./media/dns-reverse-dns-hosting/figure5.png)

Olá seguem-se exemplos sobre como toocomplete esta tarefa com o PowerShell e Olá AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>IPv6

Olá seguinte exemplo explica Olá processo de criação de novo registo de "PTR". Para outros tipos de registos e registos existentes toomodify, consulte [registos DNS de gerir e conjuntos de registos utilizando o portal do Azure de Olá](dns-operations-recordsets-portal.md).

1. Na parte superior de Olá de Olá **painel de zona DNS**, selecione **+ conjunto de registos** tooopen Olá **adicionar conjunto de registos** painel.

  ![Painel de zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. No Olá **adicionar conjunto de registos** painel. 
3. Selecione **PTR** do registo de Olá "**tipo**" menu.  
4. Olá nome do conjunto de registos de Olá para um registo PTR tem toobe restante Olá Olá endereço IPv6 na ordem inversa. Não tem de incluir quaisquer zero compressão. Neste exemplo, Olá primeiro 64 bits de Olá IPv6 já estão povoados como parte do nome da zona Olá (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa). Por conseguinte, são fornecidos apenas Olá últimos 64 bits no campo de nome de Olá. Olá últimos 64 bits do endereço IP Olá são introduzidos na ordem inversa, utilizando um período como delimitador Olá entre cada número hexadecimal. Por exemplo, pode dar nome do conjunto de registos "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" para um recurso cujo endereço IP é 2001:0db8:abdc:0000:f524:10bc:1af9:405e.  
5. No Olá "**nome de domínio**" campo, introduza o nome de domínio completamente qualificado (FQDN) Olá do recurso de Olá Olá IP a utilizar.
6. Selecione **OK** em Olá parte inferior da registo DNS do Olá painel toocreate Olá.

![adicionar o painel do conjunto de registos](./media/dns-reverse-dns-hosting/figure7.png)

Olá seguem-se exemplos sobre como toocomplete esta tarefa com o PowerShell e Olá AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>Ver registos

registos de Olá tooview que criou, navegue tooyour zona DNS no Olá portal do Azure. No Olá reduzir parte Olá **zona DNS** painel, pode ver os registos de Olá para Olá DNS zona. Deverá ver Olá predefinido NS e SOA registos, que são criados em cada zona, além de quaisquer novos registos que criou.

### <a name="ipv4"></a>IPv4

No painel de zona DNS, que mostra os registos IPv4 PTR:

![Painel de zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

Olá exemplos seguintes mostram como tooview Olá PTR regista com o PowerShell ou Olá CLI do Azure:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI do Azure 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

No painel de zona DNS, que mostra os registos IPv6 PTR:

![Painel de zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

Olá, são exemplos sobre como tooview Olá regista com o PowerShell e Olá AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI do Azure 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>FAQ

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>Pode alojar zonas de pesquisa inversas DNS para os meus blocos IP ISP atribuído no DNS do Azure?

Sim. Aloja zonas de pesquisa inversa (ARPA) Olá para os seus próprios intervalos IP no DNS do Azure é totalmente suportada.

Crie a zona de pesquisa inversa de Olá no DNS do Azure como explicado neste artigo, em seguida, trabalhar com o seu ISP demasiado[delegado Olá zona](dns-domain-delegation.md).  Em seguida, pode gerir os registos PTR Olá para cada pesquisa inversa no Olá mesma forma que outras tipos de registo.

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>É quanto o meu custo de zona de pesquisa DNS inverso de alojamento?

Zona de pesquisa DNS inversa Olá de alojamento para o bloco IP ISP atribuído no DNS do Azure é cobrado [a taxas padrão do DNS do Azure](https://azure.microsoft.com/pricing/details/dns/).

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>Pode alojar zonas de pesquisa DNS inversas para endereços IPv4 e IPv6 no DNS do Azure?

Sim. Este artigo explica como toocreate IPv4 e IPv6 inverso zonas de pesquisa DNS no DNS do Azure.

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>Pode importar uma zona de pesquisa DNS inversa existente?

Sim. Pode utilizar o zonas DNS Olá CLI do Azure tooimport existentes no DNS do Azure. Isto funciona para as zonas de pesquisa direta e zonas de pesquisa inversa.

Para obter mais informações, consulte [importação e exportação de uma zona DNS ficheiros com Olá CLI do Azure](dns-import-export.md).

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre inversa DNS, consulte [pesquisa inversa de DNS em Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Saiba como demasiado[gerir registos inversas de DNS para os serviços do Azure](dns-reverse-dns-for-azure-services.md).
