---
title: aaaCreate um servidor de Analysis Services no Azure | Microsoft Docs
description: "Saiba como toocreate um servidor de Analysis Services instância no Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Criar um servidor de Analysis Services do Azure no portal do Azure
Este artigo explica como criar um recurso de servidor do Analysis Services na sua subscrição do Azure.

## <a name="before-you-begin"></a>Antes de começar
toocomplete este guia de introdução, precisa de:

* **Subscrição do Azure**: visite [avaliação gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate uma conta.
* **Azure Active Directory**: sua subscrição tem de ser associada a um inquilino do Azure Active Directory. E, terá de toobe com sessão iniciada tooAzure com uma conta no diretório do Azure Active Directory. Não são suportadas contas Microsoft. toolearn mais, consulte [permissões de autenticação e utilizador](analysis-services-manage-users.md).
* **Grupo de recursos**: Utilize um grupo de recursos já tiver ou [criar um novo](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> A criação de um servidor poderá resultar num novo serviço sujeito a faturação. toolearn mais, consulte [preços do Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate um servidor no portal do Azure
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).  
2. Clique em **+ novo** > **dados + análise** > **Analysis Services**.
3. No Olá **Analysis Services** painel, preencha os campos de Olá necessário e, em seguida, prima **criar**.
   
    ![Criar servidor do](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Nome do servidor**: escreva um servidor de Olá tooreference exclusivo utilizado.
   * **Subscrição**: selecione a subscrição de Olá faturas este servidor a.
   * **Grupo de recursos**: Estes contentores são toohelp concebida gerir uma coleção de recursos do Azure. toolearn mais, consulte [grupos de recursos](../azure-resource-manager/resource-group-overview.md).
   * **Localização**: Olá, anfitriões de localização de centro de dados do Azure este servidor. Escolha uma localização mais próximo da sua base de utilizadores maior.
   * **Escalão de preço**: selecione um escalão de preço. São suportados modelos em tabela segurança too400 GB. toolearn mais, consulte [preços do Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
4. Clique em **Criar**.

Criar normalmente tem num minuto; muitas vezes, apenas alguns segundos. Se tiver selecionado **adicionar tooPortal**, navegue tooyour portal toosee o novo servidor. Ou, navegue até demasiado**mais serviços** > **Analysis Services** toosee se o servidor está preparado.

 ![Dashboard](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Passos seguintes
Assim que tiver criado o seu servidor, pode [implementar um modelo](analysis-services-deploy.md) tooit utilizando SSDT ou com o SSMS.

Se um modelo de implementar o servidor de tooyour liga origens de dados de tooon local, terá de tooinstall um [gateway de dados no local](analysis-services-gateway.md) num computador na sua rede.

