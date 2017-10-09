---
title: "transferência segura de aaaRequire no armazenamento do Azure | Microsoft Docs"
description: "Saiba mais sobre a funcionalidade de \"Exigir a transferência segura\" Olá do Storage do Azure e como tooenable-lo."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="3d7c2-103">Requer transferência segura</span><span class="sxs-lookup"><span data-stu-id="3d7c2-103">Require secure transfer</span></span>

<span data-ttu-id="3d7c2-104">opção de Olá "transferência segura necessária" melhora a segurança de Olá da sua conta de armazenamento ao permitir apenas pedidos toohello a conta de armazenamento de ligações seguras.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="3d7c2-105">Por exemplo, ao chamar REST APIs tooaccess a sua conta do storage, tem de ligar através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="3d7c2-106">Todos os pedidos de HTTP a utilizar são rejeitados quando o "Seguro transferência necessária" está ativado.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="3d7c2-107">Quando estiver a utilizar o serviço de ficheiros do Azure Olá, todas as ligações sem encriptação falha quando "Seguro transferência necessária" está ativada.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="3d7c2-108">Isto inclui cenários utilizando o SMB 2.1, SMB 3.0 sem encriptação e alguns tipos de Olá cliente Linux SMB.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="3d7c2-109">Por predefinição, a opção de Olá "transferência segura necessária" está desativada.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="3d7c2-110">Porque o armazenamento do Azure não suporta HTTPS para nomes de domínio personalizado, esta opção não está aplicada ao utilizar um nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="3d7c2-111">Ativar "Transferência segura necessária" no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3d7c2-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="3d7c2-112">Pode ativar Olá "transferência segura necessária" definição ambos quando criar uma conta do storage no Olá [portal do Azure](https://portal.azure.com)e para contas do storage existentes.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="3d7c2-113">Exigir a transferência segura quando criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3d7c2-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="3d7c2-114">Abra Olá **criar conta de armazenamento** painel no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="3d7c2-115">Em **Secure transferência necessária**, selecione **ativado**.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Captura de ecrã](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="3d7c2-117">Exigir a transferência segura para uma conta de armazenamento existente</span><span class="sxs-lookup"><span data-stu-id="3d7c2-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="3d7c2-118">Selecione uma conta de armazenamento existente na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="3d7c2-119">Selecione **configuração** em **definições** no painel de menu da conta de armazenamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="3d7c2-120">Em **Secure transferência necessária**, selecione **ativado**.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![Captura de ecrã](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="3d7c2-122">Ativar "Seguro transferência necessária" através de programação</span><span class="sxs-lookup"><span data-stu-id="3d7c2-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="3d7c2-123">nome da definição Olá é _supportsHttpsTrafficOnly_ nas propriedades da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="3d7c2-124">Pode ativar "Transferência segura necessária" definição com a REST API, ferramentas ou bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="3d7c2-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="3d7c2-125">**REST API** (versão: 2016-12-01): [pacote da versão](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="3d7c2-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="3d7c2-126">**PowerShell** (versão: 4.1.0): [pacote da versão](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="3d7c2-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="3d7c2-127">**CLI** (versão: 2.0.11): [pacote da versão](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="3d7c2-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="3d7c2-128">**NodeJS** (versão: 1.1.0): [pacote da versão](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="3d7c2-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="3d7c2-129">**.NET SDK** (versão: 6.3.0): [pacote da versão](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="3d7c2-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="3d7c2-130">**Python SDK** (versão: 1.1.0): [pacote da versão](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="3d7c2-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="3d7c2-131">**Ruby SDK** (versão: 0.11.0): [pacote da versão](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="3d7c2-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="3d7c2-132">Ativar "Transferência segura necessária" definição com a REST API</span><span class="sxs-lookup"><span data-stu-id="3d7c2-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="3d7c2-133">toosimplify testar com a REST API, pode utilizar [ArmClient](https://github.com/projectkudu/ARMClient) toocall da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="3d7c2-134">Pode utilizar abaixo definição Olá de toocheck de linha de comandos com Olá REST API:</span><span class="sxs-lookup"><span data-stu-id="3d7c2-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="3d7c2-135">Em resposta Olá, pode encontrar _supportsHttpsTrafficOnly_ definição.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="3d7c2-136">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3d7c2-136">Sample:</span></span>

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

<span data-ttu-id="3d7c2-137">Pode utilizar abaixo definição Olá de tooenable de linha de comandos com Olá REST API:</span><span class="sxs-lookup"><span data-stu-id="3d7c2-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="3d7c2-138">Exemplo de Input:</span><span class="sxs-lookup"><span data-stu-id="3d7c2-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="3d7c2-139">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3d7c2-139">Next steps</span></span>
<span data-ttu-id="3d7c2-140">Storage do Azure fornece um conjunto completo de capacidades de segurança, em conjunto, permitir que os programadores de aplicações seguras toobuild.</span><span class="sxs-lookup"><span data-stu-id="3d7c2-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="3d7c2-141">Para obter mais detalhes, visite Olá [manual de segurança de armazenamento](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="3d7c2-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
