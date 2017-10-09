---
title: "aplicações geridas do aaaConsume do Azure | Microsoft Docs"
description: "Descreve como um cliente cria um Azure aplicações geridas do ficheiros publicados."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Consumir uma aplicação gerida interna

Pode consumir Azure [geridos aplicações](managed-application-overview.md) que se destinam a ser membros da sua organização. Por exemplo, pode selecionar aplicações geridas do departamento de TI garantir a conformidade com as normas organizacionais. Estas aplicações geridas estão disponíveis através de Olá catálogo de serviços, Olá Azure Marketplace.

Antes de continuar com este artigo, tem de ter uma aplicação gerida disponível no catálogo de serviços de Olá para a sua subscrição. Se alguém na sua organização não já tiver criado uma aplicação gerida, consulte [publicar uma aplicação gerida para consumo interno](managed-application-publishing.md).

Atualmente, pode utilizar a CLI do Azure ou Olá tooconsume do portal do Azure, uma aplicação gerida.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Criar aplicação Olá gerido utilizando o portal de Olá

toodeploy uma aplicação gerida através do portal Olá, siga estes passos:

1. Aceda toohello portal do Azure. Procurar **aplicações geridas do catálogo de serviço**.

   ![Aplicações geridas do catálogo de serviço](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Selecione Olá geridos aplicação que pretende toocreate da lista de Olá das soluções disponíveis. Selecione **Criar**.

   ![Seleção de aplicações geridas](./media/managed-application-consumption/select-offer.png)

1. Fornece valores para parâmetros de Olá que são necessárias tooprovision Olá recursos. Selecione **Central EUA oeste** para a localização. Selecione **OK**.

   ![Parâmetros de aplicações geridas](./media/managed-application-consumption/input-parameters.png)

1. modelo de Olá valida os valores de Olá fornecida. Se a validação for bem sucedida, selecione **OK** implementação de Olá toostart.

   ![Validação de aplicações geridas](./media/managed-application-consumption/validation.png)

Após a conclusão da implementação de Olá, recursos adequados Olá definidos no modelo de Olá aprovisionados no grupo de recursos geridos de Olá fornecida.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Criar aplicação Olá gerido utilizando a CLI do Azure

Existem duas formas toocreate uma aplicação gerida utilizando a CLI do Azure:

* Utilize o comando de Olá para a criação de aplicações geridas.
* Utilize o comando de implementação de modelo normal de Olá.

### <a name="use-hello-template-deployment-command"></a>Utilize o comando de implementação do modelo de Olá

Implemente ficheiro applianceMainTemplate.json Olá Olá fornecedor criado.

Em seguida, crie dois grupos de recursos. Olá primeiro grupo de recursos é onde hello aplicações geridas recurso é criado: Microsoft.Solutions/appliances. grupo de recursos segundo Olá contém todos os recursos de Olá definidos no mainTemplate.json. Este grupo de recursos é gerido pelo Olá ISV.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Utilize `westcentralus` como localização de Olá Olá do grupo de recursos.
>

toodeploy applianceMainTemplate.json no mainResourceGroup, Olá utilize os seguintes comandos:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Depois de Olá precedente execuções de modelo, este pede-lhe para os valores dos parâmetros de Olá que são definidos no modelo de Olá Olá. Além disso toohello parâmetros que são necessárias tooprovision recursos num modelo, precisa de dois valores de parâmetro de chave:

- **managedResourceGroupId**: Olá ID Olá recursos grupo contentor Olá recursos definido no applianceMainTemplate.json. ID de Olá tem o formato de Olá `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. No Olá anterior exemplo,-do ID Olá `managedResourceGroup`.
- **applianceDefinitionId**: Olá ID Olá geridos recurso de definição de aplicação. Este valor é fornecido por Olá ISV.

> [!NOTE]
> publicador de Olá tem de conceder acesso toohello recursos grupo que contém a definição da aplicação Olá gerido. recurso de definição de Olá é criado na subscrição do publicador de Olá. Por conseguinte, um utilizador, grupo de utilizadores ou aplicações no inquilino do cliente Olá tem acesso de leitura toothis recursos.

Após a conclusão com êxito da implementação de Olá, consulte Olá gerido aplicação é criada no mainResourceGroup. recurso de storageAccount Olá é criado na managedResourceGroup.

### <a name="use-hello-create-command"></a>Olá utilize criar comando

Pode utilizar Olá `az managedapp create` comando toocreate uma aplicação gerida Olá geridos definição da aplicação.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **Id de definição de aplicação**: ID de recurso Olá de Olá gerido criada no Olá precedente passo de definição de aplicação. tooobtain este ID, execute Olá os seguintes comandos:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  Este comando devolve a definição da aplicação Olá gerido. É necessário o valor de Olá da propriedade de ID de Olá.

* **gerido-rg-id**: nome de Olá Olá recursos grupo contentor Olá recursos definido no applianceMainTemplate.json. Este grupo de recursos é o grupo de recursos geridos de Olá. É gerida pelo publicador de Olá. Se não existir, é criado para si.
* **grupo de recursos**: grupo de recursos de olá onde Olá geridos recurso de aplicação é criado. Olá Microsoft.Solutions/appliance recurso se encontra neste grupo de recursos.
* **os parâmetros**: Olá parâmetros que são necessários para os recursos de Olá definidos no applianceMainTemplate.json.

## <a name="known-issues"></a>Problemas conhecidos

Esta versão de pré-visualização inclui Olá os seguintes problemas:

* É apresentado um erro de servidor interno 500 durante a criação de Olá da aplicação Olá gerido. Caso se depare com este problema, é provável que toobe intermitente. Repita a operação de Olá.
* É necessário um novo grupo de recursos para o grupo de recursos geridos de Olá. Se utilizar um grupo de recursos existente, a implementação de Olá falhar.
* Olá grupo de recursos contém recursos de Microsoft.Solutions/appliances Olá tem de ser criado no Olá **westcentralus** localização.

## <a name="next-steps"></a>Passos seguintes

* Para aplicações de toomanaged uma introdução, consulte [descrição geral de aplicações gerido](managed-application-overview.md).
* Para obter informações sobre como publicar uma aplicação do catálogo de serviço geridas, consulte [criar e publicar uma aplicação do catálogo de serviço geridas](managed-application-publishing.md).
* Para obter informações sobre a publicação de aplicações geridas de toohello Azure Marketplace, consulte [Azure geridos aplicações no mercado de Olá](managed-application-author-marketplace.md).
* Para obter informações sobre a consumir uma aplicação gerida Olá Marketplace, consulte [consuma Azure gerida aplicações no mercado de Olá](managed-application-consume-marketplace.md).
