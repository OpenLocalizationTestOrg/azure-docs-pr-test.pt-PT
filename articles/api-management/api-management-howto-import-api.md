---
title: aaaImport uma API na API Management do Azure | Microsoft Docs
description: "Saiba como tooimport uma API e as suas operações na API Management do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>Como tooimport Olá a definição de uma API com operações em API Management do Azure
Na API Management, podem ser criadas novas APIs e operações de Olá adicionadas manualmente ou Olá API pode ser importados juntamente com operações de Olá num único passo.

APIs e as respetivas operações podem ser importadas utilizando Olá seguintes formatos.

* WADL
* Swagger

Este guia mostra como criar uma nova API e importar as respetivas operações num único passo. Para informações sobre como criar manualmente uma API e adicionar operações, consulte [como toocreate APIs] [ How toocreate APIs] e [como tooadd operações tooan API] [ How tooadd operations tooan API].

## <a name="import-api"> </a>Importar uma API
As APIs são criadas e configuradas no portal do publicador Olá. tooaccess Olá clique portal, publicador **portal do publicador** no Olá Portal do Azure para o seu serviço de API Management. Se ainda não criou uma instância de serviço de API Management, consulte [criar uma instância de serviço de API Management] [ Create an API Management service instance] no Olá [introdução à API Management do Azure] [ Get started with Azure API Management] tutorial.

![Portal do publicador][api-management-management-console]

Clique em **APIs** de Olá **API Management** menu Olá à esquerda e, em seguida, clique em **importar API**.

![API de importação][api-management-import-apis]

Olá **API de importação** janela tem três separadores que correspondem a especificação do toohello três formas tooprovide Olá API.

* **Na área de transferência** permite a especificação de Olá API toopaste na caixa de texto designado de Olá.
* **Ficheiro** permite-lhe toobrowse tooand Olá selecione ficheiro que contém a especificação de Olá API.
* **Partir do URL** permite-lhe toosupply Olá URL toohello a especificação de Olá API.

![Formato de importar API][api-management-import-api-clipboard]

Depois de fornecer a especificação de Olá API, utilize os botões de opção de Olá no formato de especificação do Olá tooindicate direita Olá. Olá seguintes formatos é suportada.

* WADL
* Swagger

Em seguida, introduza um **sufixo do URL da API Web**. Este é o URL de base de toohello anexado, para o seu serviço de gestão de API. URL de base de Olá é comum para todos os APIs alojadas em cada instância de um serviço de API Management. Gestão de API distingue APIs pelo respetivo sufixo e, por conseguinte, o sufixo de Olá tem de ser exclusivo para cada API numa instância de serviço de gestão de API específica.

Depois de todos os valores são introduzidos, clique em **guardar** toocreate Olá API e Olá associados operações. 

> [!NOTE]
> Para obter um tutorial importar uma API de calculadora básica no formato Swagger, consulte [gerir a sua primeira API na API Management do Azure](api-management-get-started.md).
> 
> 

## <a name="export-api"></a> Exportar uma API
Na adição tooimporting novas APIs, pode exportar definições de Olá das suas APIs do portal do publicador Olá. toodo por isso, clique em **exportar API** de Olá **separador Resumo** do seu **API**.

![Exportação de API][api-management-export-api]

APIs podem ser exportadas utilizando WADL ou Swagger. Selecione formato pretendido Olá, clique em **guardar**e escolha a localização de Olá no qual o ficheiro Olá toosave.

![Formato de API de exportação][api-management-export-api-format]

## <a name="next-steps"> </a>Passos seguintes
Depois de uma API é criada e operações de Olá importadas, pode rever e configurar as definições adicionais, adicione Olá API tooa produto e publicá-lo para que fique disponível para programadores. Para obter mais informações, consulte Olá seguintes guias.

* [Como as definições de tooconfigure API][How tooconfigure API settings]
* [Como toocreate e publicar um produto][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
