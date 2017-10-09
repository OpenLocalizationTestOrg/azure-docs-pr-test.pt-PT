---
title: "Pré-requisitos de aaaNon técnica para criar uma oferta para Olá Azure Marketplace | Microsoft Docs"
description: "Compreender os requisitos de Olá para criar e implementar uma toohello oferta Azure Marketplace para outros toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3dae463b-8f48-4f52-8fa8-4e3975f09f43
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/18/2016
ms.author: hascipio
ms.openlocfilehash: 472096863084cc58dc921313419ab60b1a08a3bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="general-prerequisites-for-creating-an-offer-for-hello-azure-marketplace"></a>Pré-requisitos gerais para criar uma oferta para Olá Azure Marketplace
Compreenda o processo de criação de oferecer Olá geral, negócio processo-centrado em pré-requisitos que são toomove necessário com Olá.

## <a name="ensure-that-you-are-registered-as-a-seller-with-microsoft"></a>Certifique-se de que estão registados como um vendedor com a Microsoft
Para instruções detalhadas sobre como registar uma conta de vendedor com a Microsoft, visite demasiado[conta criação e registo](marketplace-publishing-accounts-creation-registration.md).

* **Se a sua empresa já está registada como um vendedor no Olá Dev Center e quiser toocreate uma nova oferta,** , em seguida, o início de sessão toohello publicação portal com Olá mesmo id com a qual Dev Center é efetuado o registo de e-mail. Este passo é necessário para que hello portal Dev Center e publicação estão ligados entre si.
* **Se a sua empresa já está registada como um vendedor no Olá Dev Center e quiser tooedit uma oferta existente,** , em seguida, o início de sessão toohello publicação portal de conta de administrador Olá ou com uma conta que é adicionada como coadministrador na Olá portal de publicação . Passos tooadd uma conta de coadministrador é indicado abaixo.

## <a name="steps-tooadd-a-co-admin-in-hello-publishing-portal"></a>Passos tooadd um coadministrador na Olá Portal de publicação
Administradores de Olá publicação portal pode adicionar Olá outros membros da empresa Olá, que estão a trabalhar na aplicação Olá, como um coadministrador na Olá portal de publicação. **Partindo do princípio que são Olá, admin,** indicados abaixo é Olá passos tooadd co-administrador.

> [!NOTE]
> Para os novos utilizadores, antes adiciona um coadministrador na Olá publicação portal, certifique-se de que criou, pelo menos, uma aplicação Olá portal de publicação. Isto é necessário como Olá **PUBLICADORES** separador são apresentados apenas depois de criar pelo menos uma aplicação no Olá portal de publicação.
> 
> 

1. Certifique-se esse id de correio eletrónico de coadministrador Olá um account(MSA) da Microsoft. Se não estiver, registe-o como uma MSA com este [ligação](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1).
2. Certifique-se de que existe pelo menos uma aplicação na conta de administrador Olá antes de tentar tooadd co-administrador.
3. Depois de Olá os passos acima terminar, toohello de início de sessão portal com o id de correio eletrónico de coadministrador Olá de publicação e, em seguida, terminar sessão.
4. Agora o início de sessão toohello portal com o id de correio eletrónico de admin Olá de publicação.
5. Navegue tooPublishers -> selecione a sua conta -> administradores -> Adicionar Olá coadministrador (captura de ecrã indicada abaixo)
   
    ![desenho](media/marketplace-publishing-pre-requisites/imgAddAdmin_05.png)
6. Certifique-se de que os ids de e-mail fornecido no Olá várias fases do processo (por exemplo, Dev Center, publicação portal) de publicação de Olá são monitorizados para qualquer comunicação da Microsoft.
7. Para o registo de Dev Center Evite utilizar uma conta associada a uma única pessoa. Isto é sugerido para remover a dependência de um indivíduo.
8. Se enfrentam quaisquer problemas com o registo de Dev Center, em seguida, volte emitir um pedido de utilizar esta [ligação](https://developer.microsoft.com/en-us/windows/support).

## <a name="steps-toodelete-a-co-admin-in-hello-publishing-portal"></a>Passos toodelete um coadministrador na Olá portal de publicação
**Partindo do princípio que são Olá, admin,** indicados abaixo é Olá passos toodelete co-administrador.

1. Início de sessão toohello portal com o id de correio eletrónico de admin Olá de publicação.
2. Navegue demasiado**publicadores** -> selecione a sua conta -> **administradores** -> **Coadministradores**.
3. Clique em Olá **X** no botão seguinte toohello coadministrador que pretende eliminar tot (captura de ecrã indicada abaixo).
   
    ![desenho](media/marketplace-publishing-pre-requisites/imgDeleteAdmin_03.png)

> [!IMPORTANT]
> Não dispõe de toocomplete dedução dos impostos e banco as informações da empresa se estiver a planear ofertas apenas livre toopublish (ou utilizar a sua própria licença).
> 
> registo de empresa Olá tem de ser concluída tooget foi iniciado. No entanto, enquanto a sua empresa funciona nas informações de dedução dos impostos e banco Olá na conta do Microsoft Developer Olá, os programadores de Olá podem começar a trabalhar na criação de imagem de máquina virtual de Olá no Olá [Portal publicação](https://publish.windowsazure.com), recuperá-la certificadas, e testá-lo no Olá ambiente de teste do Azure. Precisa de aprovação de conta do vendedor concluída Olá apenas para o passo final Olá publicação toohello sua oferta Azure Marketplace.
> 
> 

## <a name="acquire-an-azure-pay-as-you-go-subscription"></a>Adquirir uma subscrição do Azure "pay as you go"
Esta é a subscrição de Olá que irá utilizar toocreate as imagens VM e entregar através de Olá imagens toohello [Azure Marketplace](https://azure.microsoft.com/marketplace/). Se não tiver uma subscrição existente, em seguida, inscrever-se no https://account.windowsazure.com/signup?offer=ms-azr-0003p.

## <a name="sell-from-countries"></a>"Vende de" países
> [!WARNING]
> Na ordem toosell os serviços no Olá Azure Marketplace, tem de se certificar que a entidade registada é de um dos países/regiões Olá aprovado "vende-de". Esta restrição é por razões de dividendos e taxation. Iremos ativamente procura tooexpand esta lista de países em Olá perto de futuro, por isso, esteja atento e não. Para lista completa de Olá, consulte a secção 1b de Olá [políticas de participação do Azure Marketplace](http://go.microsoft.com/fwlink/?LinkID=526833).
> 
> 

## <a name="next-steps"></a>Passos seguintes
Depois de pré-requisitos não técnico Olá estiverem concluídos, em seguida é oferta Olá pré-requisitos técnicos específicos. Clique em artigo toohello de ligação de Olá para o tipo de oferta respetivos Olá que gostaria de toocreate para Olá Azure Marketplace.

* [VM técnicas pré-requisitos](marketplace-publishing-vm-image-creation-prerequisites.md)
* [Solução modelo técnicas pré-requisitos](marketplace-publishing-solution-template-creation-prerequisites.md)

## <a name="see-also"></a>Consultar também
* [Introdução: como toopublish toohello uma oferta Azure Marketplace](marketplace-publishing-getting-started.md)

