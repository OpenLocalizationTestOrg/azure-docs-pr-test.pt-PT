---
title: "aaaConsume aplicação gerida do Azure no marketplace | Microsoft Docs"
description: "Describeshow toocreate uma aplicação de gerida do Azure que está disponível através do Olá Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a>Consumir Azure geridos aplicações no Olá Marketplace

Tal como explicado Olá [descrição geral de aplicações geridas](managed-application-overview.md) artigo, existem dois cenários Olá final tooend experiência. Um é publicador Olá ou o fornecedor que pretende toocreate uma aplicação gerida para utilização pelos clientes. Olá segundo é consumidor Olá da aplicação Olá gerido ou o cliente do fim de Olá. Este artigo abrange o segundo cenário de Olá. Descreve como pode implementar uma aplicação gerida Olá Microsoft Azure Marketplace.

## <a name="create-from-hello-marketplace"></a>Criar a partir de Olá Marketplace

Implementar uma aplicação gerida Olá Marketplace é semelhante toodeploying qualquer tipo de recursos a partir de Olá Marketplace. 

No portal de Olá, selecione **+ novo** e procure o tipo de Olá de toodeploy de solução. Nas opções disponíveis Olá, selecione Olá um que precisa.

![soluções de pesquisa](./media/managed-application-consume-marketplace/search-apps.png)

Reveja o resumo de Olá da aplicação Olá e selecione **criar**.

![criar aplicações geridas](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

Como qualquer outra solução, é apresentada com os valores de tooprovide de campos para. Estes campos variam consoante o tipo de Olá da aplicação gerida que cria. 

## <a name="view-support-information"></a>Ver informações de suporte

Após ter implementado a sua aplicação gerida, ver as informações de suporte de Olá para aplicação Olá. No painel de aplicações geridas Olá, as informações de suporte de Olá estão listadas.

![Suporte](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a>Permissões do publicador de vista

fornecedor de Olá que gere a sua aplicação é concedido acesso tooyour recursos. toosee essas permissões, selecione **autorizações**.

![autorizações](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a>Passos seguintes

* Para obter informações sobre a publicação de uma aplicação gerida Olá Marketplace, consulte [aplicações geridas do Azure no Marketplace](managed-application-author-marketplace.md).
* toopublish geridos aplicações que estão apenas disponíveis toousers na sua organização, consulte [criar e publicar a aplicação gerida do serviço catálogo](managed-application-publishing.md).
* tooconsume geridos aplicações que estão apenas disponíveis toousers na sua organização, consulte [consumir uma aplicação gerida do serviço catálogo](managed-application-consumption.md).
