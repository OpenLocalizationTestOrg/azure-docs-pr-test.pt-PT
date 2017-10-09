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
# <a name="require-secure-transfer"></a>Requer transferência segura

opção de Olá "transferência segura necessária" melhora a segurança de Olá da sua conta de armazenamento ao permitir apenas pedidos toohello a conta de armazenamento de ligações seguras. Por exemplo, ao chamar REST APIs tooaccess a sua conta do storage, tem de ligar através de HTTPS. Todos os pedidos de HTTP a utilizar são rejeitados quando o "Seguro transferência necessária" está ativado.

Quando estiver a utilizar o serviço de ficheiros do Azure Olá, todas as ligações sem encriptação falha quando "Seguro transferência necessária" está ativada. Isto inclui cenários utilizando o SMB 2.1, SMB 3.0 sem encriptação e alguns tipos de Olá cliente Linux SMB. 

Por predefinição, a opção de Olá "transferência segura necessária" está desativada.

> [!NOTE]
> Porque o armazenamento do Azure não suporta HTTPS para nomes de domínio personalizado, esta opção não está aplicada ao utilizar um nome de domínio personalizado.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>Ativar "Transferência segura necessária" no Olá portal do Azure

Pode ativar Olá "transferência segura necessária" definição ambos quando criar uma conta do storage no Olá [portal do Azure](https://portal.azure.com)e para contas do storage existentes.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Exigir a transferência segura quando criar uma conta de armazenamento

1. Abra Olá **criar conta de armazenamento** painel no Olá portal do Azure.
1. Em **Secure transferência necessária**, selecione **ativado**.

  ![Captura de ecrã](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Exigir a transferência segura para uma conta de armazenamento existente

1. Selecione uma conta de armazenamento existente na Olá portal do Azure.
1. Selecione **configuração** em **definições** no painel de menu da conta de armazenamento de Olá.
1. Em **Secure transferência necessária**, selecione **ativado**.

  ![Captura de ecrã](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Ativar "Seguro transferência necessária" através de programação

nome da definição Olá é _supportsHttpsTrafficOnly_ nas propriedades da conta de armazenamento. Pode ativar "Transferência segura necessária" definição com a REST API, ferramentas ou bibliotecas:

* **REST API** (versão: 2016-12-01): [pacote da versão](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (versão: 4.1.0): [pacote da versão](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (versão: 2.0.11): [pacote da versão](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (versão: 1.1.0): [pacote da versão](https://www.npmjs.com/package/azure-arm-storage/)
* **.NET SDK** (versão: 6.3.0): [pacote da versão](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Python SDK** (versão: 1.1.0): [pacote da versão](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Ruby SDK** (versão: 0.11.0): [pacote da versão](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Ativar "Transferência segura necessária" definição com a REST API

toosimplify testar com a REST API, pode utilizar [ArmClient](https://github.com/projectkudu/ARMClient) toocall da linha de comandos.

 Pode utilizar abaixo definição Olá de toocheck de linha de comandos com Olá REST API:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

Em resposta Olá, pode encontrar _supportsHttpsTrafficOnly_ definição. Exemplo:

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

Pode utilizar abaixo definição Olá de tooenable de linha de comandos com Olá REST API:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Exemplo de Input:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Passos seguintes
Storage do Azure fornece um conjunto completo de capacidades de segurança, em conjunto, permitir que os programadores de aplicações seguras toobuild. Para obter mais detalhes, visite Olá [manual de segurança de armazenamento](storage-security-guide.md).
