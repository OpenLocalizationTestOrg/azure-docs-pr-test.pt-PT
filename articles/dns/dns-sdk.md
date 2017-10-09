---
title: "zonas DNS aaaCreate e conjuntos de registos no DNS do Azure utilizando Olá .NET SDK | Microsoft Docs"
description: "Como zonas DNS toocreate registos e conjuntos no DNS do Azure utilizando Olá .NET SDK."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="1c4c2-103">Criar zonas DNS e conjuntos de registos utilizando Olá .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1c4c2-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="1c4c2-104">Pode automatizar operações toocreate, delete ou update zonas DNS, os conjuntos de registos e registos utilizando o SDK de DNS com a biblioteca de gestão de DNS do .NET.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="1c4c2-105">Um projeto do Visual Studio completo está disponível [aqui.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="1c4c2-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="1c4c2-106">Criar uma conta do principal de serviço</span><span class="sxs-lookup"><span data-stu-id="1c4c2-106">Create a service principal account</span></span>

<span data-ttu-id="1c4c2-107">Normalmente, é concedido acesso programático a recursos de tooAzure através de uma conta dedicada em vez das suas próprias credenciais de utilizador.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="1c4c2-108">Estas contas dedicadas são denominadas contas 'principal de serviço'.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="1c4c2-109">projeto de exemplo de Olá toouse SDK de DNS do Azure, primeiro precisa toocreate uma conta do principal de serviço e atribua-lhe permissões corretas Olá.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="1c4c2-110">Siga [estas instruções](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate uma conta do principal de serviço (o projeto de exemplo do SDK de DNS do Azure Olá pressupõe autenticação baseada em palavra-passe).</span><span class="sxs-lookup"><span data-stu-id="1c4c2-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="1c4c2-111">Criar um grupo de recursos ([Eis como](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="1c4c2-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="1c4c2-112">Utilização do Azure RBAC toogrant Olá serviço conta do principal 'Contribuinte da zona de DNS' permissões toohello grupo de recursos ([Eis como](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="1c4c2-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="1c4c2-113">Se utilizar o projeto de exemplo Olá SDK de DNS do Azure, edite ficheiro de 'program.cs' Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="1c4c2-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="1c4c2-114">Inserir valores corretos a Olá para tenantId Olá, clientId (também conhecido como ID de conta), o segredo (service principal conta palavra-passe) e subscriptionId como utilizada no passo 1.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="1c4c2-115">Introduza o nome de grupo de recursos de Olá escolhido no passo 2.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="1c4c2-116">Introduza um nome de zona DNS da sua preferência.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="1c4c2-117">Pacotes de NuGet e declarações de espaço de nomes</span><span class="sxs-lookup"><span data-stu-id="1c4c2-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="1c4c2-118">toouse Olá DNS do Azure .NET SDK, precisa de tooinstall Olá **biblioteca de gestão do DNS do Azure** pacote NuGet e outros necessitem pacotes do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="1c4c2-119">No **Visual Studio**, abra um projeto ou um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="1c4c2-120">Aceda demasiado**ferramentas**  **>**  **Gestor de pacotes NuGet**  **>**  **gerir pacotes NuGet para Solução...** .</span><span class="sxs-lookup"><span data-stu-id="1c4c2-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="1c4c2-121">Clique em **procurar**, ativar Olá **incluir pré-lançamento** caixa de verificação e escreva **Microsoft.Azure.Management.Dns** na caixa de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="1c4c2-122">Selecione o pacote de Olá e clique em **instalar** tooadd-tooyour projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="1c4c2-123">Repita o processo Olá acima tooalso Olá de instalar os seguintes pacotes: **Microsoft.Rest.ClientRuntime.Azure.Authentication** e **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="1c4c2-124">Adicionar declarações de espaço de nomes</span><span class="sxs-lookup"><span data-stu-id="1c4c2-124">Add namespace declarations</span></span>

<span data-ttu-id="1c4c2-125">Adicione as seguintes declarações de espaço de nomes de Olá</span><span class="sxs-lookup"><span data-stu-id="1c4c2-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="1c4c2-126">Inicializar o cliente de gestão do DNS Olá</span><span class="sxs-lookup"><span data-stu-id="1c4c2-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="1c4c2-127">Olá *DnsManagementClient* contém métodos Olá e as propriedades necessárias para gerir zonas DNS e recordsets.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="1c4c2-128">Olá seguinte código regista na conta do principal de serviço toohello e cria um objeto de DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="1c4c2-129">Criar ou atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="1c4c2-129">Create or update a DNS zone</span></span>

<span data-ttu-id="1c4c2-130">toocreate uma zona DNS, primeiro "Zona" é criado um objeto parâmetros de zona DNS de Olá toocontain.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="1c4c2-131">Como zonas DNS não são região específica tooa ligado, a localização Olá está definida too'global'.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="1c4c2-132">Neste exemplo, um [do Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) também é adicionada toohello zona.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="1c4c2-133">Criar tooactually ou atualização Olá zona no DNS do Azure, o objeto de zona Olá que contém os parâmetros de zona Olá é transmitida toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* método.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="1c4c2-134">DnsManagementClient suporta três modos de funcionamento: síncrona ('CreateOrUpdate'), assíncrona ('CreateOrUpdateAsync'), ou assíncrona com a resposta HTTP de toohello de acesso ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="1c4c2-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="1c4c2-135">Pode escolher qualquer um dos modos destas, dependendo das necessidades da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="1c4c2-136">O DNS do Azure suporta simultaneidade otimista, denominada [Etags](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="1c4c2-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="1c4c2-137">Neste exemplo, especificar "*" para o cabeçalho de Olá 'If-None-Match' diz ao DNS do Azure toocreate uma zona DNS se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="1c4c2-138">Falha na chamada de Olá se já existir uma zona com o nome fornecido Olá na Olá dado o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="1c4c2-139">Criar conjuntos de registos de DNS e registos</span><span class="sxs-lookup"><span data-stu-id="1c4c2-139">Create DNS record sets and records</span></span>

<span data-ttu-id="1c4c2-140">Registos DNS são geridos como um conjunto de registos.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="1c4c2-141">Um conjunto de registos é um conjunto de registos com Olá mesmo nome e registe tipo dentro de uma zona.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="1c4c2-142">nome do conjunto de registos de Olá é o nome da zona toohello relativo, não Olá nome DNS completamente qualificado.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="1c4c2-143">toocreate ou atualização de um conjunto de registos, um objeto de parâmetros de "RecordSet" é criado e passou demasiado*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="1c4c2-144">Como com zonas DNS, existem três modos de funcionamento: síncrona ('CreateOrUpdate'), assíncrona ('CreateOrUpdateAsync'), ou assíncrona com a resposta HTTP de toohello de acesso ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="1c4c2-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="1c4c2-145">Tal como acontece com zonas DNS, operações em conjuntos de registos incluem suporte para simultaneidade otimista.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="1c4c2-146">Neste exemplo, uma vez que não 'If-Match' nem 'If-None-Match' é especificados, conjunto de registos de Olá é sempre criado.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="1c4c2-147">Esta chamada substitui quaisquer existente conjunto de registos com Olá mesmo nome e registe tipo nesta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="1c4c2-148">Obter conjuntos de registos e zonas</span><span class="sxs-lookup"><span data-stu-id="1c4c2-148">Get zones and record sets</span></span>

<span data-ttu-id="1c4c2-149">Olá *DnsManagementClient.Zones.Get* e *DnsManagementClient.RecordSets.Get* métodos obter zonas individuais e conjuntos de registos, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="1c4c2-150">RecordSets são identificados pelo respetivo tipo, o nome e o grupo de recursos e horário de Olá existam na.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="1c4c2-151">Zonas são identificadas pelo respetivo grupo de recursos de nome e Olá existam na.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="1c4c2-152">Atualize um conjunto de registos existente</span><span class="sxs-lookup"><span data-stu-id="1c4c2-152">Update an existing record set</span></span>

<span data-ttu-id="1c4c2-153">tooupdate um registo DNS existente definido, obtenha primeiro o conjunto de registos de Olá, em seguida, atualização Olá registo defina conteúdo, em seguida, submeter alteração Olá.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="1c4c2-154">Neste exemplo, especificamos Olá 'Etag' a partir de Olá obter conjunto de registos no parâmetro de 'If-Match' Olá.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="1c4c2-155">chamada de Olá falha se uma operação simultânea alterou Olá conjunto de registos no Olá entretanto.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="1c4c2-156">Os conjuntos de registos e zonas de lista</span><span class="sxs-lookup"><span data-stu-id="1c4c2-156">List zones and record sets</span></span>

<span data-ttu-id="1c4c2-157">zonas toolist, utilize Olá *DnsManagementClient.Zones.List...*  métodos, que suportam a listar o todas as zonas de um grupo de recursos específico ou todas as zonas de uma determinada subscrição do Azure (em ficheiros de recursos grupos.) toolist os conjuntos de registos, utilizam *DnsManagementClient.RecordSets.List...*  métodos, que suportam a listagem de todos os conjuntos de registos numa determinada zona ou apenas os conjuntos de registos de um tipo específico.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="1c4c2-158">Tenha em atenção quando listar zonas e poderão ser paginated conjuntos de registos resultante.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="1c4c2-159">Olá seguinte exemplo mostra como tooiterate através de Olá nas páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="1c4c2-160">(Um tamanho de página artificialmente pequeno de '2' utilizado tooforce paginação; na prática, este parâmetro deve ser omitido e Olá tamanho da página predefinido utilizado.)</span><span class="sxs-lookup"><span data-stu-id="1c4c2-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="1c4c2-161">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1c4c2-161">Next steps</span></span>

<span data-ttu-id="1c4c2-162">Transferir Olá [projeto de exemplo do SDK .NET da Azure DNS](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), que inclui mais exemplos de como toouse Olá SDK .NET de DNS do Azure, incluindo exemplos para outros tipos de registos de DNS.</span><span class="sxs-lookup"><span data-stu-id="1c4c2-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
