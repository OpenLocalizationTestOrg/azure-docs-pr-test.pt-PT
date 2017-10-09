---
title: "aaaCreate e publicar uma aplicação gerida do catálogo de serviço do Azure | Microsoft Docs"
description: "Mostra como toocreate do Azure gerida a aplicação que foi concebida para os membros da sua organização."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="a7331-103">Publicar uma aplicação gerida para consumo interno</span><span class="sxs-lookup"><span data-stu-id="a7331-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="a7331-104">Pode criar e publicar Azure [geridos aplicações](managed-application-overview.md) que se destinam a ser membros da sua organização.</span><span class="sxs-lookup"><span data-stu-id="a7331-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="a7331-105">Por exemplo, um departamento de TI pode publicar aplicações geridas que garantir a conformidade com as normas organizacionais.</span><span class="sxs-lookup"><span data-stu-id="a7331-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="a7331-106">Estas aplicações geridas estão disponíveis através do catálogo de serviços de Olá, Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a7331-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="a7331-107">uma aplicação gerida para o catálogo de serviço Olá toopublish, tem de:</span><span class="sxs-lookup"><span data-stu-id="a7331-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="a7331-108">Crie um pacote. zip que contém ficheiros de modelo necessários três Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="a7331-109">Decida que utilizador, grupo ou aplicação precisa de aceder toohello o grupo de recursos na subscrição do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="a7331-110">Crie a definição da aplicação Olá gerido que pontos toohello. zip pacote e pedidos de acesso para a identidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="a7331-111">Criar um pacote de aplicações geridas</span><span class="sxs-lookup"><span data-stu-id="a7331-111">Create a managed application package</span></span>

<span data-ttu-id="a7331-112">Step-by-Olá primeiro passo é toocreate Olá três modelo necessários ficheiros.</span><span class="sxs-lookup"><span data-stu-id="a7331-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="a7331-113">Todos os três ficheiros de pacote para um ficheiro. zip e carregue a mesma localização acessível tooan, por exemplo, uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a7331-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="a7331-114">Passar o ficheiro. zip toothis ligação quando criar Olá gerido definição da aplicação.</span><span class="sxs-lookup"><span data-stu-id="a7331-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="a7331-115">**applianceMainTemplate.json**: este ficheiro define Olá Azure recursos aprovisionados como parte da Olá aplicações geridas.</span><span class="sxs-lookup"><span data-stu-id="a7331-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="a7331-116">modelo de Olá é não diferente de um modelo do Resource Manager regular.</span><span class="sxs-lookup"><span data-stu-id="a7331-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="a7331-117">Por exemplo, toocreate uma conta de armazenamento através de uma aplicação gerida, applianceMainTemplate.json contém:</span><span class="sxs-lookup"><span data-stu-id="a7331-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* <span data-ttu-id="a7331-118">**mainTemplate.json**: os utilizadores implementar este modelo quando criar Olá aplicações geridas.</span><span class="sxs-lookup"><span data-stu-id="a7331-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="a7331-119">Define recursos de aplicação Olá gerido, que é um tipo de recurso Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="a7331-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="a7331-120">Este ficheiro contém todos os parâmetros de Olá que precisa para recursos Olá applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a7331-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="a7331-121">Definir duas propriedades importantes neste modelo.</span><span class="sxs-lookup"><span data-stu-id="a7331-121">You set two important properties in this template.</span></span> <span data-ttu-id="a7331-122">Em primeiro lugar, Olá **applianceDefinitionId** propriedade é Olá ID de definição da aplicação Olá gerido.</span><span class="sxs-lookup"><span data-stu-id="a7331-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="a7331-123">Criar definição Olá posterior deste tópico.</span><span class="sxs-lookup"><span data-stu-id="a7331-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="a7331-124">Quando a definição deste valor, tem de decidir quais subscrição e toouse do grupo de recursos para armazenar Olá definições de aplicações geridas.</span><span class="sxs-lookup"><span data-stu-id="a7331-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="a7331-125">Além disso, tem de decidir um nome para a definição de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="a7331-126">ID de Olá está num formato de Olá:</span><span class="sxs-lookup"><span data-stu-id="a7331-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="a7331-127">Segundo, Olá **managedResourceGroupId** propriedade é o ID de Olá Olá do grupo de recursos onde hello recursos do Azure são criados.</span><span class="sxs-lookup"><span data-stu-id="a7331-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="a7331-128">Pode atribuir um valor para este nome de grupo de recursos ou permitir que o utilizador Olá, forneça um nome.</span><span class="sxs-lookup"><span data-stu-id="a7331-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="a7331-129">formato de Olá do ID de Olá é:</span><span class="sxs-lookup"><span data-stu-id="a7331-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="a7331-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="a7331-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="a7331-131">Olá seguinte exemplo mostra um ficheiro de mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a7331-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="a7331-132">Especifica um grupo de recursos para recursos de Olá implementado.</span><span class="sxs-lookup"><span data-stu-id="a7331-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="a7331-133">Olá ID da definição é toouse conjunto com o nome de uma definição **storageApp** num grupo de recursos denominado **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="a7331-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="a7331-134">Pode alterar estes valores toouse diferentes nomes.</span><span class="sxs-lookup"><span data-stu-id="a7331-134">You can change these values toouse different names.</span></span> <span data-ttu-id="a7331-135">Forneça a suas próprias ID de subscrição no ID de definição de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-135">Provide your own subscription ID in hello definition ID.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* <span data-ttu-id="a7331-136">**applianceCreateUiDefinition.json**: Olá portal do Azure utiliza este ficheiro toogenerate Olá interface de utilizador para os utilizadores que criam Olá aplicações geridas.</span><span class="sxs-lookup"><span data-stu-id="a7331-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="a7331-137">Definir a forma como os utilizadores forneçam entrada para cada parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a7331-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="a7331-138">Pode utilizar as opções, como uma lista pendente, caixa de texto, a caixa de palavra-passe e outras ferramentas de entrada.</span><span class="sxs-lookup"><span data-stu-id="a7331-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="a7331-139">toolearn como toocreate um ficheiro de definição de IU para uma aplicação gerida, consulte [começar com CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7331-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="a7331-140">Olá exemplo seguinte mostra um ficheiro de applianceCreateUiDefinition.json que permite que os utilizadores toospecify Olá armazenamento conta prefixo do nome através de uma caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a7331-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

<span data-ttu-id="a7331-141">Depois de todos os ficheiros de Olá necessário estiverem prontos, empacotá-las como um ficheiro. zip.</span><span class="sxs-lookup"><span data-stu-id="a7331-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="a7331-142">Step-by-Olá três ficheiros deverão estar no nível de raiz de Olá de ficheiro. zip de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="a7331-143">Se o put-los numa pasta, receberá um erro quando criar Olá gerido a definição da aplicação que indica a Olá necessários ficheiros não estão presentes.</span><span class="sxs-lookup"><span data-stu-id="a7331-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="a7331-144">Carregar localização acessível do Olá pacote tooan onde podem ser consumidos.</span><span class="sxs-lookup"><span data-stu-id="a7331-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="a7331-145">resto Olá deste artigo assume que o ficheiro. zip de Olá existe no contentor do blob storage acessível publicamente.</span><span class="sxs-lookup"><span data-stu-id="a7331-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="a7331-146">Criar um grupo de utilizadores do Azure Active Directory ou a aplicação</span><span class="sxs-lookup"><span data-stu-id="a7331-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="a7331-147">segundo passo de Olá é tooselect um grupo de utilizadores ou aplicações para gerir recursos de Olá em nome do cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="a7331-148">Este grupo de utilizadores ou a aplicação não tem permissões no Olá gerido grupo de acordo com toohello função de recursos que está atribuída.</span><span class="sxs-lookup"><span data-stu-id="a7331-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="a7331-149">função de Olá pode ser qualquer função de controlo de acesso baseado em funções (RBAC) incorporada, como o proprietário ou contribuinte.</span><span class="sxs-lookup"><span data-stu-id="a7331-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="a7331-150">Também pode dar um utilizador individual recursos de Olá toomanage de permissão, mas normalmente atribuir o grupo de utilizadores de tooa esta permissão.</span><span class="sxs-lookup"><span data-stu-id="a7331-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="a7331-151">toocreate um novo grupo de utilizadores do Active Directory, consulte [criar um grupo e adicionar membros no Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a7331-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="a7331-152">Terá de ID de objeto Olá de Olá utilizador grupo toouse para gerir recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="a7331-153">Olá seguinte exemplo mostra como tooget Olá ID de objeto de nome a apresentar do grupo de Olá:</span><span class="sxs-lookup"><span data-stu-id="a7331-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="a7331-154">comando de exemplo de Olá devolve Olá seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="a7331-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="a7331-155">ID de objeto de Olá apenas tooretrieve, utilize:</span><span class="sxs-lookup"><span data-stu-id="a7331-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="a7331-156">Obter ID de definição de função Olá</span><span class="sxs-lookup"><span data-stu-id="a7331-156">Get hello role definition ID</span></span>

<span data-ttu-id="a7331-157">Em seguida, terá de ID de definição de função Olá de Olá função incorporada RBAC pretende que o utilizador de toohello toogrant acesso, grupo de utilizadores ou aplicações.</span><span class="sxs-lookup"><span data-stu-id="a7331-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="a7331-158">Normalmente, utiliza Olá proprietário ou função de contribuinte ou leitor.</span><span class="sxs-lookup"><span data-stu-id="a7331-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="a7331-159">Olá comando a seguir mostra como tooget Olá ID de definição de função para a função de proprietário Olá:</span><span class="sxs-lookup"><span data-stu-id="a7331-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="a7331-160">Se o comando devolve Olá seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="a7331-160">That command returns hello following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

<span data-ttu-id="a7331-161">É necessário o valor de Olá da propriedade de "name" Olá de Olá anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="a7331-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="a7331-162">Pode obter apenas essa propriedade com:</span><span class="sxs-lookup"><span data-stu-id="a7331-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="a7331-163">Criar a definição da aplicação Olá gerido</span><span class="sxs-lookup"><span data-stu-id="a7331-163">Create hello managed application definition</span></span>

<span data-ttu-id="a7331-164">Se ainda não tiver um grupo de recursos para armazenar a definição da aplicação gerida, crie uma agora:</span><span class="sxs-lookup"><span data-stu-id="a7331-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="a7331-165">Agora, crie o recurso de definição de aplicação Olá gerido.</span><span class="sxs-lookup"><span data-stu-id="a7331-165">Now, create hello managed application definition resource.</span></span>

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

<span data-ttu-id="a7331-166">os parâmetros de Olá utilizados Olá anterior exemplo são:</span><span class="sxs-lookup"><span data-stu-id="a7331-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="a7331-167">**grupo de recursos**: nome de Olá Olá do grupo de recursos onde Olá geridos a definição da aplicação é criado.</span><span class="sxs-lookup"><span data-stu-id="a7331-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="a7331-168">**nível de bloqueio**: tipo de Olá de bloqueio colocadas num grupo de recursos geridos de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="a7331-169">Impede que o cliente de Olá efetuar operações indesejáveis neste grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a7331-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="a7331-170">Atualmente, só de leitura é Olá suportado apenas o nível de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="a7331-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="a7331-171">Quando é especificado só de leitura, o cliente Olá pode apenas ler recursos de Olá presentes no grupo de recursos geridos de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7331-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="a7331-172">**autorizações**: descreve Olá ID de principal e o ID de definição de função Olá são o grupo de recursos geridos de toohello de permissão de toogrant utilizados.</span><span class="sxs-lookup"><span data-stu-id="a7331-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="a7331-173">Foi especificado no formato de Olá de `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="a7331-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="a7331-174">Vários valores também podem ser especificados para esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="a7331-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="a7331-175">Se forem necessárias vários valores, deve ser especificados no formato de Olá `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="a7331-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="a7331-176">Vários valores separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="a7331-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="a7331-177">**uri de ficheiro de pacote**: Olá localização Olá gerido do pacote de aplicação que contém ficheiros de modelo de Olá, que podem ser um blob de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7331-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7331-178">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a7331-178">Next steps</span></span>

* <span data-ttu-id="a7331-179">Para aplicações de toomanaged uma introdução, consulte [descrição geral de aplicações gerido](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7331-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a7331-180">Para obter exemplos de ficheiros de Olá, consulte [geridos amostras de aplicação](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="a7331-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="a7331-181">Para obter informações sobre a consumir uma aplicação do catálogo de serviço geridas, consulte [consumir uma aplicação do catálogo de serviço geridas](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="a7331-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="a7331-182">Para obter informações sobre a publicação de aplicações geridas de toohello Azure Marketplace, consulte [Azure geridos aplicações no mercado de Olá](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="a7331-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="a7331-183">Para obter informações sobre a consumir uma aplicação gerida Olá Marketplace, consulte [consuma Azure gerida aplicações no mercado de Olá](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="a7331-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="a7331-184">toolearn como toocreate um ficheiro de definição de IU para uma aplicação gerida, consulte [começar com CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7331-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
