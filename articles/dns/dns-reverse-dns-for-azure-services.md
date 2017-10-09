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
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="9bfd5-103">Configurar o DNS inversa para serviços alojados no Azure</span><span class="sxs-lookup"><span data-stu-id="9bfd5-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="9bfd5-104">Este artigo explica como tooconfigure inverso pesquisas de DNS para serviços alojados no Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="9bfd5-105">Os serviços no Azure utilizar endereços IP atribuído pelo Azure e pertencente à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="9bfd5-106">Estes registos DNS inversas (registos PTR) tem de ser criados no Olá correspondentes pertencentes à Microsoft zonas DNS inversas pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="9bfd5-107">Este artigo explica como toodo isto.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-107">This article explains how toodo this.</span></span>

<span data-ttu-id="9bfd5-108">Este cenário deve não ser confundido com capacidade de Olá demasiado[alojar Olá zonas DNS inversas pesquisa para os intervalos IP atribuídos no DNS do Azure](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="9bfd5-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="9bfd5-109">Neste caso, os intervalos de IP Olá representados por zona de pesquisa inversa de Olá devem ser atribuídos tooyour organização, normalmente pelo seu ISP.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="9bfd5-110">Antes de ler este artigo, deve estar familiarizado com esta [descrição geral do DNS inversa e de suporte no Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bfd5-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="9bfd5-111">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9bfd5-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="9bfd5-112">No modelo de implementação do Resource Manager Olá, recursos de computação (por exemplo, as máquinas virtuais, conjuntos de dimensionamento de máquina virtual ou clusters de Service Fabric) são expostos através de um recurso de PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="9bfd5-113">Pesquisas inversas de DNS estão configuradas ao utilizar a propriedade 'ReverseFqdn' Olá Olá PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="9bfd5-114">No modelo de implementação clássica Olá, recursos de computação são expostos utilizar serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="9bfd5-115">Pesquisas inversas de DNS estão configuradas ao utilizar a propriedade 'ReverseDnsFqdn' Olá Olá serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="9bfd5-116">DNS inversa não é atualmente suportado para Olá App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="9bfd5-117">Validação de registos DNS inversas</span><span class="sxs-lookup"><span data-stu-id="9bfd5-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="9bfd5-118">Uma linha de terceiros não deve ser capaz de toocreate inversas registos DNS para os seus domínios DNS de tooyour de mapeamento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="9bfd5-119">tooprevent, Azure só permite a criação de Olá de um registo DNS inverso em que o nome de domínio especificado no registo DNS inverso Olá é seja resolvido para Olá nome DNS ou endereço IP de um PublicIpAddress ou uma nuvem de serviço no Olá mesmo ou Olá igual à subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="9bfd5-120">Esta validação só é executada quando o registo DNS inverso Olá é definido ou modificado.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="9bfd5-121">Não é efetuada a validação de reativação periódica.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="9bfd5-122">Por exemplo: Suponhamos Olá PublicIpAddress recurso tem contosoapp1.northus.cloudapp.azure.com de nome DNS Olá e endereço IP 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="9bfd5-123">Olá ReverseFqdn para Olá que publicipaddress podem ser especificados como:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="9bfd5-124">nome DNS de Olá para Olá PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="9bfd5-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="9bfd5-125">Olá de nome DNS para um PublicIpAddress diferentes no Olá mesma subscrição, tais como contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="9bfd5-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="9bfd5-126">Um intuitivos nomes DNS, tais como app1.contoso.com, desde que este nome é *primeiro* configurado como um CNAME toocontosoapp1.northus.cloudapp.azure.com ou tooa PublicIpAddress diferentes no Olá mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="9bfd5-127">Um intuitivos nomes DNS, tais como app1.contoso.com, desde que este nome é *primeiro* configurado como um endereço IP de registo toohello A 23.96.52.53 ou endereço IP toohello um PublicIpAddress diferentes no Olá mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="9bfd5-128">Olá mesmas restrições aplicam-se tooreverse DNS para serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="9bfd5-129">Inversa de DNS para recursos PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9bfd5-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="9bfd5-130">Esta secção fornece instruções detalhadas sobre como tooconfigure inversa DNS para os recursos de PublicIpAddress no modelo de implementação do Resource Manager Olá, utilizando o Azure PowerShell, CLI do Azure 1.0 ou 2.0 de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="9bfd5-131">Configurar o DNS inversa PublicIpAddress recursos não é atualmente suportada através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="9bfd5-132">Azure atualmente suporta inversa DNS apenas para recursos IPv4 PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="9bfd5-133">Não é suportada para IPv6.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="9bfd5-134">Adicionar inversa de DNS de tooan existente PublicIpAddresses</span><span class="sxs-lookup"><span data-stu-id="9bfd5-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="9bfd5-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bfd5-135">PowerShell</span></span>

<span data-ttu-id="9bfd5-136">tooadd existente PublicIpAddress inversa tooan DNS:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="9bfd5-137">tooadd inverso tooan DNS existente PublicIpAddress que já não tem um nome DNS, também tem de especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="9bfd5-138">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9bfd5-138">Azure CLI 1.0</span></span>

<span data-ttu-id="9bfd5-139">tooadd existente PublicIpAddress inversa tooan DNS:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="9bfd5-140">tooadd inverso tooan DNS existente PublicIpAddress que já não tem um nome DNS, também tem de especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="9bfd5-141">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="9bfd5-141">Azure CLI 2.0</span></span>

<span data-ttu-id="9bfd5-142">tooadd existente PublicIpAddress inversa tooan DNS:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="9bfd5-143">tooadd inverso tooan DNS existente PublicIpAddress que já não tem um nome DNS, também tem de especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="9bfd5-144">Criar um endereço IP público com o DNS inversa</span><span class="sxs-lookup"><span data-stu-id="9bfd5-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="9bfd5-145">toocreate um PublicIpAddress novo com a propriedade Olá inversa DNS já especificado:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="9bfd5-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bfd5-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="9bfd5-147">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9bfd5-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="9bfd5-148">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="9bfd5-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="9bfd5-149">Vista DNS inverso para um PublicIpAddress existente</span><span class="sxs-lookup"><span data-stu-id="9bfd5-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="9bfd5-150">Olá tooview configurados valor para um PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="9bfd5-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bfd5-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="9bfd5-152">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9bfd5-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="9bfd5-153">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="9bfd5-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="9bfd5-154">Remover DNS inversa de endereços IP públicos existentes</span><span class="sxs-lookup"><span data-stu-id="9bfd5-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="9bfd5-155">tooremove uma propriedade DNS inversa de um PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="9bfd5-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bfd5-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="9bfd5-157">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9bfd5-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="9bfd5-158">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="9bfd5-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="9bfd5-159">Configurar inversa de DNS para serviços em nuvem</span><span class="sxs-lookup"><span data-stu-id="9bfd5-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="9bfd5-160">Esta secção fornece instruções detalhadas sobre como tooconfigure inversa DNS para serviços em nuvem no modelo de implementação clássica de Olá, com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="9bfd5-161">Configurar o inversa de DNS para serviços em nuvem não é suportada através do portal do Azure, Olá da CLI do Azure 1.0 ou 2.0 de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="9bfd5-162">Adicionar serviços de Cloud de tooexisting DNS inversa</span><span class="sxs-lookup"><span data-stu-id="9bfd5-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="9bfd5-163">tooadd um tooan de registo DNS inverso existente serviço em nuvem:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="9bfd5-164">Criar um serviço em nuvem com o DNS inversa</span><span class="sxs-lookup"><span data-stu-id="9bfd5-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="9bfd5-165">um novo serviço em nuvem com a propriedade Olá inversa DNS especificada já toocreate:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="9bfd5-166">Vista DNS inversa para serviços de Cloud existente</span><span class="sxs-lookup"><span data-stu-id="9bfd5-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="9bfd5-167">tooview Olá inversa DNS propriedade para um serviço em nuvem existente:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="9bfd5-168">Remover inversa de DNS dos serviços de nuvem existente</span><span class="sxs-lookup"><span data-stu-id="9bfd5-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="9bfd5-169">tooremove uma propriedade DNS inversa de um serviço em nuvem existente:</span><span class="sxs-lookup"><span data-stu-id="9bfd5-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="9bfd5-170">FAQ</span><span class="sxs-lookup"><span data-stu-id="9bfd5-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="9bfd5-171">Quanto inverter o custo de registos DNS?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="9bfd5-172">Se estiverem livres!</span><span class="sxs-lookup"><span data-stu-id="9bfd5-172">They're free!</span></span>  <span data-ttu-id="9bfd5-173">Não há sem custos adicionais para inversas de DNS de registos ou consultas.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="9bfd5-174">Será o meu resolve de registos DNS inversa de Olá internet?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="9bfd5-175">Sim.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-175">Yes.</span></span> <span data-ttu-id="9bfd5-176">Depois de definir a propriedade DNS inversa Olá para o serviço do Azure, Azure gere todas as delegações do Olá DNS e zonas DNS necessário resolve tooensure inverter o registo DNS para todos os utilizadores de Internet.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="9bfd5-177">Registos DNS inversas predefinida são criados para os meus serviços do Azure?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="9bfd5-178">Não.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-178">No.</span></span> <span data-ttu-id="9bfd5-179">Inversa de DNS é uma funcionalidade de recusa.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="9bfd5-180">Sem predefinição inversas de DNS de registos são criados se optar por não tooconfigure-los.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="9bfd5-181">O que é o formato de Olá para o nome de domínio completamente qualificado (FQDN) do Olá?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="9bfd5-182">Estão especificados na ordem de pesquisa direta e FQDNs tem de ser terminadas por um ponto (por exemplo, "app1.contoso.com.").</span><span class="sxs-lookup"><span data-stu-id="9bfd5-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="9bfd5-183">O que acontece se a verificação de validação de Olá para Olá inversa DNS posso especificadas falha?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="9bfd5-184">Onde hello inversa DNS validação verificação falha, falha Olá operação tooconfigure Olá inverso registo DNS.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="9bfd5-185">Corrija o valor DNS inversa Olá conforme necessário e repita.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="9bfd5-186">Pode configurar inversa de DNS para o App Service do Azure?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="9bfd5-187">Não.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-187">No.</span></span> <span data-ttu-id="9bfd5-188">DNS inversa não é suportada para Olá App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="9bfd5-189">Pode configurar vários registos DNS inversas para o meu serviço do Azure?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="9bfd5-190">Não.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-190">No.</span></span> <span data-ttu-id="9bfd5-191">Azure suporta um único registo DNS inverso para cada serviço de nuvem do Azure ou um PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="9bfd5-192">Pode configurar inversa de DNS para recursos de IPv6 PublicIpAddress?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="9bfd5-193">Não.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-193">No.</span></span> <span data-ttu-id="9bfd5-194">Azure atualmente suporta inversa DNS apenas para IPv4 PublicIpAddress recursos e serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="9bfd5-195">Pode enviar mensagens de correio eletrónico tooexternal domínios dos meus serviços de computação do Azure?</span><span class="sxs-lookup"><span data-stu-id="9bfd5-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="9bfd5-196">Não.</span><span class="sxs-lookup"><span data-stu-id="9bfd5-196">No.</span></span> [<span data-ttu-id="9bfd5-197">Serviços de computação do Azure não suportam domínios de tooexternal enviar mensagens de correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="9bfd5-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="9bfd5-198">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9bfd5-198">Next steps</span></span>

<span data-ttu-id="9bfd5-199">Para obter mais informações sobre inversa DNS, consulte [pesquisa inversa de DNS em Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="9bfd5-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="9bfd5-200">Saiba como demasiado[zona de pesquisa inversa de Olá de anfitrião para o intervalo de IP ISP atribuído no DNS do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="9bfd5-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

