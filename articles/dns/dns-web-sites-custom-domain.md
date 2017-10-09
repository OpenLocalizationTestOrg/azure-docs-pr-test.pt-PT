---
title: "registos DNS personalizados aaaCreate para uma aplicação web | Microsoft Docs"
description: "Como o DNS de domínio personalizado de toocreate regista da aplicação web utilizando o DNS do Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="ed8bc-103">Criar registos DNS para uma aplicação web num domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ed8bc-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="ed8bc-104">Pode utilizar o DNS do Azure toohost um domínio personalizado para as suas aplicações web.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="ed8bc-105">Por exemplo, estiver a criar uma aplicação web do Azure e pretender que o seu tooaccess utilizadores-lo ao utilizar contoso.com ou www.contoso.com como um FQDN.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="ed8bc-106">toodo, tiver dois registos toocreate:</span><span class="sxs-lookup"><span data-stu-id="ed8bc-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="ed8bc-107">Um toocontoso.com de apontador de registo raiz "A"</span><span class="sxs-lookup"><span data-stu-id="ed8bc-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="ed8bc-108">Um "CNAME" de registo para o nome de www Olá que aponta toohello um registo</span><span class="sxs-lookup"><span data-stu-id="ed8bc-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="ed8bc-109">Tenha em atenção que, se criar um registo a para uma aplicação web no Azure, Olá que um registo tem de ser atualizado manualmente se Olá subjacente endereço IP para alterações de aplicações web Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ed8bc-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ed8bc-110">Before you begin</span></span>

<span data-ttu-id="ed8bc-111">Antes de começar, tem primeiro de criar uma zona DNS no DNS do Azure e delegar a zona de Olá no seu tooAzure de entidade de registo DNS.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="ed8bc-112">toocreate uma zona DNS, siga os passos Olá [criar uma zona DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="ed8bc-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="ed8bc-113">toodelegate tooAzure seu DNS DNS, siga Olá passos [delegação de domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ed8bc-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="ed8bc-114">Depois de criar uma zona e delegar-tooAzure DNS, em seguida, pode criar registos para o seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="ed8bc-115">1. Criar um registo a para o domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ed8bc-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="ed8bc-116">Um registo é toomap utilizado um endereço IP do nome tooits.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="ed8bc-117">No seguinte exemplo de Olá iremos atribuirá como um tooan de registo de um endereço IPv4:</span><span class="sxs-lookup"><span data-stu-id="ed8bc-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="ed8bc-118">Passo 1</span><span class="sxs-lookup"><span data-stu-id="ed8bc-118">Step 1</span></span>

<span data-ttu-id="ed8bc-119">Criar um registo a e atribuir tooa $rs variável</span><span class="sxs-lookup"><span data-stu-id="ed8bc-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="ed8bc-120">Passo 2</span><span class="sxs-lookup"><span data-stu-id="ed8bc-120">Step 2</span></span>

<span data-ttu-id="ed8bc-121">Adicionar o conjunto de registos Olá IPv4 valor toohello criado anteriormente "@" utilizando a variável de Olá $rs atribuído.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="ed8bc-122">Olá IPv4 valor atribuído será o endereço IP Olá para a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="ed8bc-123">endereço IP Olá toofind para uma aplicação web, siga os passos Olá [configurar um nome de domínio personalizado no App Service do Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ed8bc-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="ed8bc-124">Passo 3</span><span class="sxs-lookup"><span data-stu-id="ed8bc-124">Step 3</span></span>

<span data-ttu-id="ed8bc-125">Consolide o conjunto de registos do toohello Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="ed8bc-126">Utilize `Set-AzureRMDnsRecordSet` Olá tooupload alterações toohello tooAzure de conjunto de registos DNS:</span><span class="sxs-lookup"><span data-stu-id="ed8bc-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="ed8bc-127">2. Criar um registo CNAME para o domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ed8bc-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="ed8bc-128">Se o seu domínio já está a ser gerido pelo DNS do Azure (consulte [delegação de domínio DNS](dns-domain-delegation.md), pode utilizar Olá toocreate de exemplo de Olá um registo CNAME para contoso.azurewebsites.net a seguir.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="ed8bc-129">Passo 1</span><span class="sxs-lookup"><span data-stu-id="ed8bc-129">Step 1</span></span>

<span data-ttu-id="ed8bc-130">Abra o PowerShell e crie um novo conjunto de registos CNAME e atribua tooa $rs variável.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="ed8bc-131">Neste exemplo, irá criar um tipo de conjunto de registos CNAME com uma "Hora toolive" de 600 segundos na zona DNS com o nome "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="ed8bc-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="ed8bc-132">Olá seguinte o exemplo é resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-132">hello following example is hello response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="ed8bc-133">Passo 2</span><span class="sxs-lookup"><span data-stu-id="ed8bc-133">Step 2</span></span>

<span data-ttu-id="ed8bc-134">Assim que for criado Olá conjunto de registos CNAME, terá de toocreate um valor de alias que irá apontar toohello web app.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="ed8bc-135">Pode utilizar Olá atribuídos anteriormente a variável "$rs" para utilizar o comando do PowerShell Olá abaixo alias de Olá toocreate para contoso.azurewebsites.net de aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="ed8bc-136">Olá seguinte o exemplo é resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-136">hello following example is hello response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="ed8bc-137">Passo 3</span><span class="sxs-lookup"><span data-stu-id="ed8bc-137">Step 3</span></span>

<span data-ttu-id="ed8bc-138">Confirmar alterações Olá utilizando Olá `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ed8bc-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="ed8bc-139">Pode validar o registo de Olá foi criado corretamente consultando Olá "www.contoso.com" com nslookup, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="ed8bc-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="ed8bc-140">Crie um registo de "awverify" para as aplicações web</span><span class="sxs-lookup"><span data-stu-id="ed8bc-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="ed8bc-141">Se decidir toouse um registo para a sua aplicação web, tem de ir através de um tooensure do processo de verificação, domínio personalizado Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="ed8bc-142">Este passo de verificação é feito através da criação de um registo CNAME especial com o nome "awverify".</span><span class="sxs-lookup"><span data-stu-id="ed8bc-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="ed8bc-143">Esta secção aplica-se apenas a registos tooA.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="ed8bc-144">Passo 1</span><span class="sxs-lookup"><span data-stu-id="ed8bc-144">Step 1</span></span>

<span data-ttu-id="ed8bc-145">Crie Olá "awverify" registo.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-145">Create hello "awverify" record.</span></span> <span data-ttu-id="ed8bc-146">Exemplo de Olá abaixo, iremos criar registo de "aweverify" Olá contoso.com tooverify propriedade para o domínio personalizado Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="ed8bc-147">Olá seguinte o exemplo é resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-147">hello following example is hello response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="ed8bc-148">Passo 2</span><span class="sxs-lookup"><span data-stu-id="ed8bc-148">Step 2</span></span>

<span data-ttu-id="ed8bc-149">Após criar o conjunto de registos de Olá "awverify", atribua Olá Registro CNAME definir alias.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="ed8bc-150">Exemplo de Olá abaixo, iremos atribuirá Olá CNAMe conjunto de registos alias tooawverify.contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="ed8bc-151">Olá seguinte o exemplo é resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-151">hello following example is hello response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="ed8bc-152">Passo 3</span><span class="sxs-lookup"><span data-stu-id="ed8bc-152">Step 3</span></span>

<span data-ttu-id="ed8bc-153">Confirmar alterações Olá utilizando Olá `Set-AzureRMDnsRecordSet cmdlet`, conforme mostrado no comando Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="ed8bc-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ed8bc-154">Next steps</span></span>

<span data-ttu-id="ed8bc-155">Siga os passos Olá [configurar um nome de domínio personalizado para o App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure sua toouse de aplicação web um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ed8bc-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
