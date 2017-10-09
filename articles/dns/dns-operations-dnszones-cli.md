---
title: aaaManage DNS zonas no DNS do Azure - Azure CLI 2.0 | Microsoft Docs
description: Pode gerir zonas DNS a utilizar o Azure CLI 2.0. Este artigo mostra como tooupdate, eliminar e criar zonas DNS no DNS do Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="18846-104">Como toomanage zonas de DNS no DNS do Azure utilizando Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="18846-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="18846-105">Portal</span><span class="sxs-lookup"><span data-stu-id="18846-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="18846-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18846-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="18846-107">CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="18846-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="18846-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="18846-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="18846-109">Este guia mostra como toomanage seu DNS zonas utilizando Olá entre plataformas CLI do Azure, que está disponível para o Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="18846-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="18846-110">Também pode gerir as zonas DNS utilizando [Azure PowerShell](dns-operations-dnszones.md) ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="18846-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="18846-111">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="18846-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="18846-112">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="18846-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="18846-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -nosso CLI para Olá clássica e resource Gestão modelos de implementação.</span><span class="sxs-lookup"><span data-stu-id="18846-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="18846-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="18846-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="18846-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="18846-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="18846-116">Configurar a CLI 2.0 do Azure para o Azure DNS</span><span class="sxs-lookup"><span data-stu-id="18846-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="18846-117">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="18846-117">Before you begin</span></span>

<span data-ttu-id="18846-118">Certifique-se de que tem Olá seguintes itens antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="18846-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="18846-119">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="18846-119">An Azure subscription.</span></span> <span data-ttu-id="18846-120">Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18846-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="18846-121">Instale a versão mais recente do Olá do Olá 2.0 CLI do Azure, disponível para Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="18846-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="18846-122">Estão disponíveis mais informações no [Olá de instalação do Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="18846-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="18846-123">Inicie sessão no tooyour a conta do Azure</span><span class="sxs-lookup"><span data-stu-id="18846-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="18846-124">Abra uma janela de consola e autentique com as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="18846-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="18846-125">Para obter mais informações, consulte o registo no tooAzure de Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="18846-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="18846-126">Selecione a subscrição de Olá</span><span class="sxs-lookup"><span data-stu-id="18846-126">Select hello subscription</span></span>

<span data-ttu-id="18846-127">Verifique Olá subscrições para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="18846-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="18846-128">Escolha qual das suas toouse de subscrições do Azure.</span><span class="sxs-lookup"><span data-stu-id="18846-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="18846-129">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="18846-129">Create a resource group</span></span>

<span data-ttu-id="18846-130">O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização,</span><span class="sxs-lookup"><span data-stu-id="18846-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="18846-131">Isto é utilizado como localização predefinida de Olá para recursos nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="18846-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="18846-132">No entanto, uma vez que todos os recursos DNS são globais, não regionais, escolha de Olá de localização do grupo de recursos não tem impacto no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="18846-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="18846-133">Pode ignorar este passo se estiver a utilizar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="18846-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="18846-134">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="18846-134">Getting help</span></span>

<span data-ttu-id="18846-135">Todos os comandos de CLI 2.0 referentes tooAzure DNS começar a utilizar `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="18846-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="18846-136">Ajuda está disponível para cada comando utilizando Olá `--help` opção (formato curto `-h`).</span><span class="sxs-lookup"><span data-stu-id="18846-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="18846-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="18846-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="18846-138">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="18846-138">Create a DNS zone</span></span>

<span data-ttu-id="18846-139">Uma zona DNS é criada utilizando Olá `az network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="18846-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="18846-140">Para obter ajuda, consulte `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="18846-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="18846-141">Olá exemplo seguinte cria uma zona DNS denominada *contoso.com* no grupo de recursos de Olá denominado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="18846-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="18846-142">toocreate uma zona DNS com etiquetas</span><span class="sxs-lookup"><span data-stu-id="18846-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="18846-143">Olá exemplo seguinte mostra como toocreate um DNS zona com dois [etiquetas do Azure Resource Manager](dns-zones-records.md#tags), *projeto = demonstração* e *env = test*, utilizando Olá `--tags` parâmetro (formato curto `-t`):</span><span class="sxs-lookup"><span data-stu-id="18846-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="18846-144">Obter uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="18846-144">Get a DNS zone</span></span>

<span data-ttu-id="18846-145">tooretrieve uma zona DNS, utilize `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="18846-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="18846-146">Para obter ajuda, consulte `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="18846-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="18846-147">Olá exemplo seguinte devolve zona DNS Olá *contoso.com* e os respetivos dados associados do grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="18846-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="18846-148">Olá seguinte o exemplo é resposta Olá.</span><span class="sxs-lookup"><span data-stu-id="18846-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="18846-149">Tenha em atenção que os registos DNS não são devolvidos pelo `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="18846-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="18846-150">Utilize registos DNS toolist, `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="18846-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="18846-151">Zonas DNS de lista</span><span class="sxs-lookup"><span data-stu-id="18846-151">List DNS zones</span></span>

<span data-ttu-id="18846-152">tooenumerate zonas DNS, utilize `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="18846-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="18846-153">Para obter ajuda, consulte `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="18846-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="18846-154">Grupo de recursos de Olá especificação lista apenas dessas zonas dentro do grupo de recursos de Olá:</span><span class="sxs-lookup"><span data-stu-id="18846-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="18846-155">Grupo de recursos de Olá omitindo apresenta uma lista de todas as zonas na subscrição Olá:</span><span class="sxs-lookup"><span data-stu-id="18846-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="18846-156">Atualize uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="18846-156">Update a DNS zone</span></span>

<span data-ttu-id="18846-157">Tooa alterações recursos de zona DNS podem ser efetuados utilizando `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="18846-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="18846-158">Para obter ajuda, consulte `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="18846-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="18846-159">Este comando não atualizar qualquer um dos conjuntos de registos DNS Olá dentro da zona de Olá (consulte [como registos DNS tooManage](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="18846-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="18846-160">É tooupdate utilizados apenas propriedades de recurso de zona de Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="18846-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="18846-161">Estas propriedades são actualmente limitada toohello [do Azure Resource Manager 'etiquetas'](dns-zones-records.md#tags) para o recurso de zona Olá.</span><span class="sxs-lookup"><span data-stu-id="18846-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="18846-162">Olá exemplo seguinte mostra como Olá tooupdate etiquetas numa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="18846-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="18846-163">etiquetas existente Olá são substituídas pelos Olá valor especificado.</span><span class="sxs-lookup"><span data-stu-id="18846-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="18846-164">Eliminar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="18846-164">Delete a DNS zone</span></span>

<span data-ttu-id="18846-165">Zonas DNS podem ser eliminadas utilizando `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="18846-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="18846-166">Para obter ajuda, consulte `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="18846-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="18846-167">Também eliminar uma zona DNS elimina todos os registos DNS na zona de Olá.</span><span class="sxs-lookup"><span data-stu-id="18846-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="18846-168">Esta operação não pode ser anulada.</span><span class="sxs-lookup"><span data-stu-id="18846-168">This operation cannot be undone.</span></span> <span data-ttu-id="18846-169">Se a zona DNS Olá está a ser utilizado, serviços, utilizando a zona de Olá irão falhar quando zona Olá é eliminada.</span><span class="sxs-lookup"><span data-stu-id="18846-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="18846-170">tooprotect contra eliminação acidental de zona, consulte [como tooprotect DNS zonas e regista](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="18846-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="18846-171">Este comando solicita a confirmação.</span><span class="sxs-lookup"><span data-stu-id="18846-171">This command prompts for confirmation.</span></span> <span data-ttu-id="18846-172">Olá opcional `--yes` comutador suprime esta linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="18846-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="18846-173">Olá exemplo seguinte mostra como toodelete Olá zona *contoso.com* do grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="18846-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="18846-174">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="18846-174">Next steps</span></span>

<span data-ttu-id="18846-175">Saiba como demasiado[gerir conjuntos de registos e registos](dns-getstarted-create-recordset-cli.md) na sua zona DNS.</span><span class="sxs-lookup"><span data-stu-id="18846-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="18846-176">Saiba como demasiado[delegar a tooAzure de domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="18846-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

