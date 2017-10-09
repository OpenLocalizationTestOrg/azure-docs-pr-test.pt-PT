---
title: aaaPublish-WebApplicationWebSite (script do Windows PowerShell) | Microsoft Docs
description: "Saiba como toopublish uma web projeto tooan Web site Azure. Este script cria recursos Olá necessária na sua subscrição do Azure, caso não existam."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publicar-WebApplicationWebSite (script do Windows PowerShell)
## <a name="syntax"></a>Sintaxe
Publica um tooan de projeto do web site do Azure. o script de Olá cria recursos Olá necessária na sua subscrição do Azure, caso não existam.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Configuração
Olá caminho toohello ficheiro de configuração JSON que descreve os detalhes de Olá da implementação de Olá.

| Parâmetro | Valor predefinido |
| --- | --- |
| Aliases |Nenhum |
| Necessário? |VERDADEIRO |
| Posição |com o nome |
| Valor predefinido |Nenhum |
| Aceitar entrada de pipeline? |FALSO |
| Aceitar carateres universais? |FALSO |

## <a name="subscriptionname"></a>SubscriptionName
nome de Olá do Olá subscrição do Azure que pretende o Web site de Olá toocreate no.

| Parâmetro | Valor predefinido |
| --- | --- |
| Aliases |Nenhum |
| Necessário? |FALSO |
| Posição |com o nome |
| Valor predefinido |Nenhum |
| Aceitar entrada de pipeline? |FALSO |
| Aceitar carateres universais? |FALSO |

## <a name="webdeploypackage"></a>WebDeployPackage
Olá caminho toohello implementação pacote toopublish toohello site web. Pode criar este pacote utilizando o Assistente de publicar Web Olá no Visual Studio. Para obter mais informações, consulte [introdução ao Cloud Services do Azure e ao ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parâmetro | Valor predefinido |
| --- | --- |
| Aliases |Nenhum |
| Necessário? |FALSO |
| Posição |com o nome |
| Valor predefinido |Nenhum |
| Aceitar entrada de pipeline? |FALSO |
| Aceitar carateres universais? |FALSO |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
Olá nome de utilizador e palavra-passe para Olá SQL da base de dados no Azure.

| Parâmetro | Valor predefinido |
| --- | --- |
| Aliases |Nenhum |
| Necessário? |FALSO |
| Posição |com o nome |
| Valor predefinido |Nenhum |
| Aceitar entrada de pipeline? |FALSO |
| Aceitar carateres universais? |FALSO |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Se for VERDADEIRO, mensagens de impressão de Olá script toohello fluxo de saída.

| Parâmetro | Valor predefinido |
| --- | --- |
| Aliases |Nenhum |
| Necessário? |FALSO |
| Posição |com o nome |
| Valor predefinido |FALSO |
| Aceitar entrada de pipeline? |FALSO |
| Aceitar carateres universais? |FALSO |

## <a name="remarks"></a>Observações
Para obter uma explicação completa do como toouse Olá script toocreate Dev e ambientes de teste, consulte [utilizando Scripts do Windows PowerShell tooPublish tooDev e ambientes de teste](vs-azure-tools-publishing-using-powershell-scripts.md).

ficheiro de configuração JSON Olá Especifica os detalhes de Olá que é toobe implementado. Inclui informações de Olá que especificou quando criou o projeto de Olá, como o nome de Olá e nome de utilizador para o Web site Olá. Também inclui Olá tooprovision de base de dados, se aplicável. Olá código a seguir mostra um ficheiro de configuração do JSON de exemplo:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Pode editar Olá JSON configuração ficheiro toochange o que é implementado. Não é necessária uma secção de Web site, mas a secção de base de dados de Olá é opcional.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte [publicar-WebApplicationVM (script do Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)

