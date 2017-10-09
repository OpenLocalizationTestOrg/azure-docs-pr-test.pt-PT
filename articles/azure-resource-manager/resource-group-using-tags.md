---
title: "aaaTag Azure recursos da organização lógica | Microsoft Docs"
description: "Mostra como tooapply etiquetas tooorganize Azure recursos para faturação e gestão."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="d91eb-103">Utilize etiquetas tooorganize os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d91eb-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="d91eb-104">Pode aplicar etiquetas tooresources apenas que suportam o Azure Resource Manager operations.</span><span class="sxs-lookup"><span data-stu-id="d91eb-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="d91eb-105">Se tiver criado uma máquina virtual, a rede virtual ou a conta de armazenamento através do modelo de implementação clássica Olá (tais como através de Olá portal clássico do Azure), não é possível aplicar um recurso de toothat etiquetas.</span><span class="sxs-lookup"><span data-stu-id="d91eb-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="d91eb-106">toosupport etiquetagem, volte a implementar estes recursos através do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d91eb-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="d91eb-107">Todos os outros recursos suportam a etiquetagem.</span><span class="sxs-lookup"><span data-stu-id="d91eb-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="d91eb-108">Políticas para a consistência da etiqueta</span><span class="sxs-lookup"><span data-stu-id="d91eb-108">Policies for tag consistency</span></span>

<span data-ttu-id="d91eb-109">Pode utilizar regras padrão do toocreate de políticas de recursos para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="d91eb-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="d91eb-110">Pode criar políticas que se certifique-se de recursos são etiquetados com os valores adequados Olá.</span><span class="sxs-lookup"><span data-stu-id="d91eb-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="d91eb-111">Para obter mais informações, consulte [aplicar políticas de recursos de etiquetas](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="d91eb-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="d91eb-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d91eb-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="d91eb-113">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d91eb-113">Azure CLI</span></span>

<span data-ttu-id="d91eb-114">Olá, toosee etiquetas existentes para um *grupo de recursos*, utilize:</span><span class="sxs-lookup"><span data-stu-id="d91eb-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="d91eb-115">Se o script devolve Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="d91eb-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="d91eb-116">Olá, toosee etiquetas existentes para um *recursos que tem um ID de recurso especificado*, utilize:</span><span class="sxs-lookup"><span data-stu-id="d91eb-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="d91eb-117">Ou, toosee Olá etiquetas existentes para um *recursos que tem um grupo de recurso, tipo e nome*, utilize:</span><span class="sxs-lookup"><span data-stu-id="d91eb-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="d91eb-118">utilizar grupos de recursos de tooget que tenham uma tag específica, `az group list`:</span><span class="sxs-lookup"><span data-stu-id="d91eb-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="d91eb-119">tooget todos os recursos de Olá que tenham uma etiqueta específica e o valor, utilize `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="d91eb-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="d91eb-120">Sempre que aplicar etiquetas tooa recursos ou um grupo de recursos, substituir etiquetas existente do Olá nesse recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d91eb-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="d91eb-121">Por conseguinte, tem de utilizar uma abordagem diferente com base se os recursos de Olá ou grupo de recursos tem etiquetas existentes.</span><span class="sxs-lookup"><span data-stu-id="d91eb-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="d91eb-122">tooadd etiquetas tooa *grupo de recursos sem etiquetas existentes*, utilize:</span><span class="sxs-lookup"><span data-stu-id="d91eb-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="d91eb-123">tooadd etiquetas tooa *recursos sem etiquetas existentes*, utilize:</span><span class="sxs-lookup"><span data-stu-id="d91eb-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="d91eb-124">tooadd etiquetas tooa recurso que já tem etiquetas, obter etiquetas existente Olá, reformatar esse valor e volte a aplicar etiquetas de Olá existentes e novas:</span><span class="sxs-lookup"><span data-stu-id="d91eb-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="d91eb-125">tooapply todas as etiquetas de um recurso do grupo tooits de recursos, e *mantém as etiquetas existentes nos recursos de Olá*, utilize Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="d91eb-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

<span data-ttu-id="d91eb-126">tooapply todas as etiquetas de um recurso do grupo tooits de recursos, e *etiquetas existentes nos recursos de manter*, utilize Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="d91eb-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a><span data-ttu-id="d91eb-127">Modelos</span><span class="sxs-lookup"><span data-stu-id="d91eb-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="d91eb-128">Portal</span><span class="sxs-lookup"><span data-stu-id="d91eb-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="d91eb-129">API REST</span><span class="sxs-lookup"><span data-stu-id="d91eb-129">REST API</span></span>
<span data-ttu-id="d91eb-130">Olá portal do Azure e o PowerShell utilizam Olá [API de REST do Resource Manager](https://docs.microsoft.com/rest/api/resources/) em segundo plano de Olá.</span><span class="sxs-lookup"><span data-stu-id="d91eb-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="d91eb-131">Se precisar de toointegrate etiquetagem para outro ambiente, pode obter etiquetas utilizando **obter** Olá recurso ID e a atualização Olá conjunto das etiquetas, utilizando um **PATCH** chamada.</span><span class="sxs-lookup"><span data-stu-id="d91eb-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="d91eb-132">As etiquetas e faturação</span><span class="sxs-lookup"><span data-stu-id="d91eb-132">Tags and billing</span></span>
<span data-ttu-id="d91eb-133">Pode utilizar etiquetas toogroup os dados de faturação.</span><span class="sxs-lookup"><span data-stu-id="d91eb-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="d91eb-134">Por exemplo, se estiver a executar várias VMs para diferentes organizações, utilize Olá etiquetas toogroup utilização pelo centro de custos.</span><span class="sxs-lookup"><span data-stu-id="d91eb-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="d91eb-135">Também pode utilizar os custos de toocategorize etiquetas ao ambiente de tempo de execução, como a utilização de faturação Olá para VMs em execução no ambiente de produção Olá.</span><span class="sxs-lookup"><span data-stu-id="d91eb-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="d91eb-136">Pode obter informações sobre etiquetas através de Olá [utilização de recursos do Azure e RateCard APIs](../billing/billing-usage-rate-card-overview.md) ou ficheiro de valores separados por vírgulas (CSV) de utilização de Olá.</span><span class="sxs-lookup"><span data-stu-id="d91eb-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="d91eb-137">Transferir o ficheiro de utilização de Olá de Olá [portal de contas do Azure](https://account.windowsazure.com/) ou [EA portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d91eb-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="d91eb-138">Para obter mais informações sobre as informações de toobilling acesso programático, consulte [obter informações acerca do consumo de recursos do Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d91eb-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="d91eb-139">Para operações de REST API, consulte [referência de API de REST de faturação do Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="d91eb-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="d91eb-140">Quando transferir a utilização de Olá CSV para serviços que suportam etiquetas com faturação, etiquetas Olá são apresentadas no Olá **etiquetas** coluna.</span><span class="sxs-lookup"><span data-stu-id="d91eb-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="d91eb-141">Para obter mais informações, consulte [compreender a fatura do Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="d91eb-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Consulte as etiquetas na faturação](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="d91eb-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d91eb-143">Next steps</span></span>
* <span data-ttu-id="d91eb-144">Pode aplicar restrições e convenções na sua subscrição através da utilização de políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d91eb-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="d91eb-145">Uma política que definir poderão exigir que todos os recursos têm um valor para uma tag específica.</span><span class="sxs-lookup"><span data-stu-id="d91eb-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="d91eb-146">Para obter mais informações, consulte [utilizar políticas toomanage recursos e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d91eb-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="d91eb-147">Para um toousing de introdução do Azure PowerShell quando estiver a implementar recursos, consulte o artigo [utilizar o Azure PowerShell com o Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d91eb-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="d91eb-148">Para um Olá toousing de introdução CLI do Azure quando estiver a implementar recursos, consulte o artigo [Using Olá CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d91eb-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="d91eb-149">Para uma introdução toousing Olá do portal, consulte [Using Olá toomanage portal do Azure, os recursos do Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d91eb-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="d91eb-150">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d91eb-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

