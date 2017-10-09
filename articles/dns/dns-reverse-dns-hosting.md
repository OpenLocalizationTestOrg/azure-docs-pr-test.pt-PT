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
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="935fd-103">Aloja zonas de pesquisa inversas DNS no DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="935fd-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="935fd-104">Este artigo explica como toohost Olá inverso zonas de pesquisa DNS para os intervalos IP atribuídos no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="935fd-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="935fd-105">intervalos IP Olá representados por zona de pesquisa inversa de Olá devem ser atribuídos tooyour organização, normalmente pelo seu ISP.</span><span class="sxs-lookup"><span data-stu-id="935fd-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="935fd-106">tooconfigure inversa de DNS para o IP pertencente ao Azure endereço atribuído tooyour serviço do Azure, consulte [Configurar pesquisa inversa Olá para endereços IP Olá alocado tooyour serviço do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="935fd-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="935fd-107">Antes de ler este artigo, deve estar familiarizado com esta [descrição geral do DNS inversa e de suporte no Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="935fd-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="935fd-108">Este artigo explica Olá passos toocreate a primeira zona DNS de pesquisa inversa e registo utilizando Olá portal do Azure, Azure PowerShell, a CLI do Azure 1.0 ou 2.0 de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="935fd-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="935fd-109">Criar uma zona de pesquisa inversa de DNS</span><span class="sxs-lookup"><span data-stu-id="935fd-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="935fd-110">Inicie sessão no toohello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="935fd-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="935fd-111">No menu do Hub de Olá, clique em e clique em **novo** > **redes** > e, em seguida, clique em **zona DNS** tooopen Olá **zona de DNS criar**painel.</span><span class="sxs-lookup"><span data-stu-id="935fd-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="935fd-113">No Olá **zona DNS criar** painel, nome da sua zona DNS.</span><span class="sxs-lookup"><span data-stu-id="935fd-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="935fd-114">nome de Olá da zona de Olá é crafted de forma diferente para os prefixos de IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="935fd-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="935fd-115">Utilizar qualquer uma das instruções Olá para [IPV4](#ipv4) ou [IPv6](#ipv6) tooname sua zona.</span><span class="sxs-lookup"><span data-stu-id="935fd-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="935fd-116">Quando concluir clique **criar** zona de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="935fd-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="935fd-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="935fd-117">IPv4</span></span>

<span data-ttu-id="935fd-118">nome de Olá de uma zona de pesquisa inversa IPv4 é baseado no intervalo IP Olá representa.</span><span class="sxs-lookup"><span data-stu-id="935fd-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="935fd-119">Deve ser Olá seguinte formato: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="935fd-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="935fd-120">Para obter exemplos, consulte [descrição geral do DNS inversa e de suporte no Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="935fd-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="935fd-121">Quando criar classless zonas de pesquisa inversas de DNS no DNS do Azure, tem de utilizar um hífen (`-`) em vez de uma barra ('/ ') no nome da zona Olá.</span><span class="sxs-lookup"><span data-stu-id="935fd-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="935fd-122">Por exemplo, para Olá IP intervalo 192.0.2.128/26, tem de utilizar `128-26.2.0.192.in-addr.arpa` como nome da zona Olá em vez de `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="935fd-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="935fd-123">Isto acontece porque, embora ambos são suportadas pelo normas DNS Olá, de zona DNS nomes que contêm barra Olá (`/`) carateres não são suportadas no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="935fd-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="935fd-124">Olá exemplo seguinte mostra como toocreate 'Classe C' Inverter zona DNS com o nome `2.0.192.in-addr.arpa` no DNS do Azure através de Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="935fd-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![criar a zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="935fd-126">Olá 'Localização do grupo de recursos' define a localização de Olá Olá grupo de recursos e não tem impacto na zona DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="935fd-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="935fd-127">localização de zona DNS Olá é sempre 'global' e não é apresentada.</span><span class="sxs-lookup"><span data-stu-id="935fd-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="935fd-128">Olá exemplos seguintes mostram como toocomplete esta tarefa com o Azure PowerShell e Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="935fd-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="935fd-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="935fd-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="935fd-130">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="935fd-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="935fd-131">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="935fd-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="935fd-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="935fd-132">IPv6</span></span>

<span data-ttu-id="935fd-133">Olá nome de uma zona de pesquisa inversa IPv6 devem ter Olá seguinte formato: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="935fd-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="935fd-134">Para obter exemplos, consulte [descrição geral do DNS inversa e de suporte no Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="935fd-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="935fd-135">Olá exemplo seguinte mostra como toocreate uma zona de pesquisa DNS inversa IPv6 com o nome `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` no DNS do Azure através de Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="935fd-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![criar a zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="935fd-137">Olá 'Localização do grupo de recursos' define a localização de Olá Olá grupo de recursos e não tem impacto na zona DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="935fd-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="935fd-138">localização de zona DNS Olá é sempre 'global' e não é apresentada.</span><span class="sxs-lookup"><span data-stu-id="935fd-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="935fd-139">Olá exemplos seguintes mostram como toocomplete esta tarefa com o Azure PowerShell e Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="935fd-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="935fd-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="935fd-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="935fd-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="935fd-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="935fd-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="935fd-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="935fd-143">Delegar a uma zona de pesquisa inversa DNS</span><span class="sxs-lookup"><span data-stu-id="935fd-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="935fd-144">Ter criado a sua zona de pesquisa inversa DNS, tem de garantir que zona Olá é delegada da zona de principal de Olá.</span><span class="sxs-lookup"><span data-stu-id="935fd-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="935fd-145">Delegação de DNS permite Olá nome resolução processo toofind Olá servidores de nomes DNS que aloja a zona de pesquisa inversa DNS.</span><span class="sxs-lookup"><span data-stu-id="935fd-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="935fd-146">Isto permite que esses servidores tooanswer DNS inversas consultas de nome para endereços IP Olá no seu intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="935fd-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="935fd-147">Para zonas de pesquisa direta, o processo de Olá de delegação de uma zona DNS é descrito em [delegar a tooAzure de domínio DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="935fd-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="935fd-148">Funciona a delegação de zonas de pesquisa inversa Olá mesma forma.</span><span class="sxs-lookup"><span data-stu-id="935fd-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="935fd-149">Step-by-Olá única diferença é que tem de servidores de nomes de Olá tooconfigure com Olá ISP que forneceu o intervalo de IP, em vez da sua entidade de registo de nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="935fd-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="935fd-150">Criar um registo DNS PTR</span><span class="sxs-lookup"><span data-stu-id="935fd-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="935fd-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="935fd-151">IPv4</span></span>

<span data-ttu-id="935fd-152">Olá seguinte exemplo explica Olá processo de criação de um registo PTR numa zona DNS inversa no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="935fd-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="935fd-153">Para outros tipos de registos e registos existentes toomodify, consulte [registos DNS de gerir e conjuntos de registos utilizando o portal do Azure de Olá](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="935fd-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="935fd-154">Na parte superior de Olá de Olá **zona DNS** painel, selecione **+ conjunto de registos** tooopen Olá **adicionar conjunto de registos** painel.</span><span class="sxs-lookup"><span data-stu-id="935fd-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="935fd-156">No Olá **adicionar conjunto de registos** painel.</span><span class="sxs-lookup"><span data-stu-id="935fd-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="935fd-157">Selecione **PTR** do registo de Olá "**tipo**" menu.</span><span class="sxs-lookup"><span data-stu-id="935fd-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="935fd-158">Olá nome do conjunto de registos de Olá para um registo PTR tem toobe restante Olá Olá endereço IPv4 na ordem inversa.</span><span class="sxs-lookup"><span data-stu-id="935fd-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="935fd-159">Neste exemplo, hello três primeiros octetos já estão povoados como parte do nome da zona Olá (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="935fd-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="935fd-160">Por conseguinte, apenas Olá último octeto é fornecido no campo de nome de Olá.</span><span class="sxs-lookup"><span data-stu-id="935fd-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="935fd-161">Por exemplo, pode dar nome do conjunto de registos "**15**" para um recurso cujo endereço IP é 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="935fd-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="935fd-162">No Olá "**nome de domínio**" campo, introduza o nome de domínio completamente qualificado (FQDN) Olá do recurso de Olá Olá IP a utilizar.</span><span class="sxs-lookup"><span data-stu-id="935fd-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="935fd-163">Selecione **OK** em Olá parte inferior da registo DNS do Olá painel toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="935fd-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![adicionar o conjunto de registos](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="935fd-165">Olá seguem-se exemplos sobre como toocomplete esta tarefa com o PowerShell e Olá AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="935fd-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="935fd-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="935fd-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="935fd-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="935fd-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="935fd-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="935fd-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="935fd-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="935fd-169">IPv6</span></span>

<span data-ttu-id="935fd-170">Olá seguinte exemplo explica Olá processo de criação de novo registo de "PTR".</span><span class="sxs-lookup"><span data-stu-id="935fd-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="935fd-171">Para outros tipos de registos e registos existentes toomodify, consulte [registos DNS de gerir e conjuntos de registos utilizando o portal do Azure de Olá](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="935fd-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="935fd-172">Na parte superior de Olá de Olá **painel de zona DNS**, selecione **+ conjunto de registos** tooopen Olá **adicionar conjunto de registos** painel.</span><span class="sxs-lookup"><span data-stu-id="935fd-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![Painel de zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="935fd-174">No Olá **adicionar conjunto de registos** painel.</span><span class="sxs-lookup"><span data-stu-id="935fd-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="935fd-175">Selecione **PTR** do registo de Olá "**tipo**" menu.</span><span class="sxs-lookup"><span data-stu-id="935fd-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="935fd-176">Olá nome do conjunto de registos de Olá para um registo PTR tem toobe restante Olá Olá endereço IPv6 na ordem inversa.</span><span class="sxs-lookup"><span data-stu-id="935fd-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="935fd-177">Não tem de incluir quaisquer zero compressão.</span><span class="sxs-lookup"><span data-stu-id="935fd-177">It must not include any zero compression.</span></span> <span data-ttu-id="935fd-178">Neste exemplo, Olá primeiro 64 bits de Olá IPv6 já estão povoados como parte do nome da zona Olá (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="935fd-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="935fd-179">Por conseguinte, são fornecidos apenas Olá últimos 64 bits no campo de nome de Olá.</span><span class="sxs-lookup"><span data-stu-id="935fd-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="935fd-180">Olá últimos 64 bits do endereço IP Olá são introduzidos na ordem inversa, utilizando um período como delimitador Olá entre cada número hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="935fd-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="935fd-181">Por exemplo, pode dar nome do conjunto de registos "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" para um recurso cujo endereço IP é 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="935fd-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="935fd-182">No Olá "**nome de domínio**" campo, introduza o nome de domínio completamente qualificado (FQDN) Olá do recurso de Olá Olá IP a utilizar.</span><span class="sxs-lookup"><span data-stu-id="935fd-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="935fd-183">Selecione **OK** em Olá parte inferior da registo DNS do Olá painel toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="935fd-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![adicionar o painel do conjunto de registos](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="935fd-185">Olá seguem-se exemplos sobre como toocomplete esta tarefa com o PowerShell e Olá AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="935fd-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="935fd-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="935fd-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="935fd-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="935fd-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="935fd-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="935fd-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="935fd-189">Ver registos</span><span class="sxs-lookup"><span data-stu-id="935fd-189">View Records</span></span>

<span data-ttu-id="935fd-190">registos de Olá tooview que criou, navegue tooyour zona DNS no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="935fd-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="935fd-191">No Olá reduzir parte Olá **zona DNS** painel, pode ver os registos de Olá para Olá DNS zona.</span><span class="sxs-lookup"><span data-stu-id="935fd-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="935fd-192">Deverá ver Olá predefinido NS e SOA registos, que são criados em cada zona, além de quaisquer novos registos que criou.</span><span class="sxs-lookup"><span data-stu-id="935fd-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="935fd-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="935fd-193">IPv4</span></span>

<span data-ttu-id="935fd-194">No painel de zona DNS, que mostra os registos IPv4 PTR:</span><span class="sxs-lookup"><span data-stu-id="935fd-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Painel de zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="935fd-196">Olá exemplos seguintes mostram como tooview Olá PTR regista com o PowerShell ou Olá CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="935fd-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="935fd-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="935fd-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="935fd-198">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="935fd-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="935fd-199">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="935fd-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="935fd-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="935fd-200">IPv6</span></span>

<span data-ttu-id="935fd-201">No painel de zona DNS, que mostra os registos IPv6 PTR:</span><span class="sxs-lookup"><span data-stu-id="935fd-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Painel de zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="935fd-203">Olá, são exemplos sobre como tooview Olá regista com o PowerShell e Olá AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="935fd-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="935fd-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="935fd-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="935fd-205">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="935fd-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="935fd-206">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="935fd-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="935fd-207">FAQ</span><span class="sxs-lookup"><span data-stu-id="935fd-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="935fd-208">Pode alojar zonas de pesquisa inversas DNS para os meus blocos IP ISP atribuído no DNS do Azure?</span><span class="sxs-lookup"><span data-stu-id="935fd-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="935fd-209">Sim.</span><span class="sxs-lookup"><span data-stu-id="935fd-209">Yes.</span></span> <span data-ttu-id="935fd-210">Aloja zonas de pesquisa inversa (ARPA) Olá para os seus próprios intervalos IP no DNS do Azure é totalmente suportada.</span><span class="sxs-lookup"><span data-stu-id="935fd-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="935fd-211">Crie a zona de pesquisa inversa de Olá no DNS do Azure como explicado neste artigo, em seguida, trabalhar com o seu ISP demasiado[delegado Olá zona](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="935fd-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="935fd-212">Em seguida, pode gerir os registos PTR Olá para cada pesquisa inversa no Olá mesma forma que outras tipos de registo.</span><span class="sxs-lookup"><span data-stu-id="935fd-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="935fd-213">É quanto o meu custo de zona de pesquisa DNS inverso de alojamento?</span><span class="sxs-lookup"><span data-stu-id="935fd-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="935fd-214">Zona de pesquisa DNS inversa Olá de alojamento para o bloco IP ISP atribuído no DNS do Azure é cobrado [a taxas padrão do DNS do Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="935fd-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="935fd-215">Pode alojar zonas de pesquisa DNS inversas para endereços IPv4 e IPv6 no DNS do Azure?</span><span class="sxs-lookup"><span data-stu-id="935fd-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="935fd-216">Sim.</span><span class="sxs-lookup"><span data-stu-id="935fd-216">Yes.</span></span> <span data-ttu-id="935fd-217">Este artigo explica como toocreate IPv4 e IPv6 inverso zonas de pesquisa DNS no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="935fd-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="935fd-218">Pode importar uma zona de pesquisa DNS inversa existente?</span><span class="sxs-lookup"><span data-stu-id="935fd-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="935fd-219">Sim.</span><span class="sxs-lookup"><span data-stu-id="935fd-219">Yes.</span></span> <span data-ttu-id="935fd-220">Pode utilizar o zonas DNS Olá CLI do Azure tooimport existentes no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="935fd-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="935fd-221">Isto funciona para as zonas de pesquisa direta e zonas de pesquisa inversa.</span><span class="sxs-lookup"><span data-stu-id="935fd-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="935fd-222">Para obter mais informações, consulte [importação e exportação de uma zona DNS ficheiros com Olá CLI do Azure](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="935fd-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="935fd-223">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="935fd-223">Next steps</span></span>

<span data-ttu-id="935fd-224">Para obter mais informações sobre inversa DNS, consulte [pesquisa inversa de DNS em Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="935fd-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="935fd-225">Saiba como demasiado[gerir registos inversas de DNS para os serviços do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="935fd-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
