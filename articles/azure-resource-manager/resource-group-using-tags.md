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
# <a name="use-tags-tooorganize-your-azure-resources"></a>Utilize etiquetas tooorganize os recursos do Azure
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> Pode aplicar etiquetas tooresources apenas que suportam o Azure Resource Manager operations. Se tiver criado uma máquina virtual, a rede virtual ou a conta de armazenamento através do modelo de implementação clássica Olá (tais como através de Olá portal clássico do Azure), não é possível aplicar um recurso de toothat etiquetas. toosupport etiquetagem, volte a implementar estes recursos através do Resource Manager. Todos os outros recursos suportam a etiquetagem.
> 
> 

## <a name="policies-for-tag-consistency"></a>Políticas para a consistência da etiqueta

Pode utilizar regras padrão do toocreate de políticas de recursos para a sua organização. Pode criar políticas que se certifique-se de recursos são etiquetados com os valores adequados Olá. Para obter mais informações, consulte [aplicar políticas de recursos de etiquetas](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>CLI do Azure

Olá, toosee etiquetas existentes para um *grupo de recursos*, utilize:

```azurecli
az group show -n examplegroup --query tags
```

Se o script devolve Olá seguinte formato:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

Olá, toosee etiquetas existentes para um *recursos que tem um ID de recurso especificado*, utilize:

```azurecli
az resource show --id {resource-id} --query tags
```

Ou, toosee Olá etiquetas existentes para um *recursos que tem um grupo de recurso, tipo e nome*, utilize:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

utilizar grupos de recursos de tooget que tenham uma tag específica, `az group list`:

```azurecli
az group list --tag Dept=IT
```

tooget todos os recursos de Olá que tenham uma etiqueta específica e o valor, utilize `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Sempre que aplicar etiquetas tooa recursos ou um grupo de recursos, substituir etiquetas existente do Olá nesse recurso ou grupo de recursos. Por conseguinte, tem de utilizar uma abordagem diferente com base se os recursos de Olá ou grupo de recursos tem etiquetas existentes. 

tooadd etiquetas tooa *grupo de recursos sem etiquetas existentes*, utilize:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd etiquetas tooa *recursos sem etiquetas existentes*, utilize:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

tooadd etiquetas tooa recurso que já tem etiquetas, obter etiquetas existente Olá, reformatar esse valor e volte a aplicar etiquetas de Olá existentes e novas: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply todas as etiquetas de um recurso do grupo tooits de recursos, e *mantém as etiquetas existentes nos recursos de Olá*, utilize Olá seguintes script:

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

tooapply todas as etiquetas de um recurso do grupo tooits de recursos, e *etiquetas existentes nos recursos de manter*, utilize Olá seguintes script:

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


## <a name="templates"></a>Modelos

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>API REST
Olá portal do Azure e o PowerShell utilizam Olá [API de REST do Resource Manager](https://docs.microsoft.com/rest/api/resources/) em segundo plano de Olá. Se precisar de toointegrate etiquetagem para outro ambiente, pode obter etiquetas utilizando **obter** Olá recurso ID e a atualização Olá conjunto das etiquetas, utilizando um **PATCH** chamada.

## <a name="tags-and-billing"></a>As etiquetas e faturação
Pode utilizar etiquetas toogroup os dados de faturação. Por exemplo, se estiver a executar várias VMs para diferentes organizações, utilize Olá etiquetas toogroup utilização pelo centro de custos. Também pode utilizar os custos de toocategorize etiquetas ao ambiente de tempo de execução, como a utilização de faturação Olá para VMs em execução no ambiente de produção Olá.


Pode obter informações sobre etiquetas através de Olá [utilização de recursos do Azure e RateCard APIs](../billing/billing-usage-rate-card-overview.md) ou ficheiro de valores separados por vírgulas (CSV) de utilização de Olá. Transferir o ficheiro de utilização de Olá de Olá [portal de contas do Azure](https://account.windowsazure.com/) ou [EA portal](https://ea.azure.com). Para obter mais informações sobre as informações de toobilling acesso programático, consulte [obter informações acerca do consumo de recursos do Microsoft Azure](../billing/billing-usage-rate-card-overview.md). Para operações de REST API, consulte [referência de API de REST de faturação do Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Quando transferir a utilização de Olá CSV para serviços que suportam etiquetas com faturação, etiquetas Olá são apresentadas no Olá **etiquetas** coluna. Para obter mais informações, consulte [compreender a fatura do Microsoft Azure](../billing/billing-understand-your-bill.md).

![Consulte as etiquetas na faturação](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Passos seguintes
* Pode aplicar restrições e convenções na sua subscrição através da utilização de políticas personalizadas. Uma política que definir poderão exigir que todos os recursos têm um valor para uma tag específica. Para obter mais informações, consulte [utilizar políticas toomanage recursos e controlar o acesso](resource-manager-policy.md).
* Para um toousing de introdução do Azure PowerShell quando estiver a implementar recursos, consulte o artigo [utilizar o Azure PowerShell com o Azure Resource Manager](powershell-azure-resource-manager.md).
* Para um Olá toousing de introdução CLI do Azure quando estiver a implementar recursos, consulte o artigo [Using Olá CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).
* Para uma introdução toousing Olá do portal, consulte [Using Olá toomanage portal do Azure, os recursos do Azure](resource-group-portal.md).  
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

