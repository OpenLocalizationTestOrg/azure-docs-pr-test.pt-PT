---
title: "aaaUpload um certificado de API de gestão do Azure | Microsoft Docs"
description: "Saiba como tooupload athe API da gestão de certificados para Olá Portal clássico do Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="f9910-103">Carregar um certificado de gestão de API de gestão do Azure</span><span class="sxs-lookup"><span data-stu-id="f9910-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="f9910-104">Certificados de gestão permitem tooauthenticate com o modelo de implementação clássica Olá fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="f9910-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="f9910-105">Muitos programas e ferramentas (tais como o Visual Studio ou Olá SDK do Azure) utilizam estes configuração tooautomate de certificados e a implementação de vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9910-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="f9910-106">Tenha cuidado!</span><span class="sxs-lookup"><span data-stu-id="f9910-106">Be careful!</span></span> <span data-ttu-id="f9910-107">Estes tipos de certificados de permitir que qualquer pessoa que efetua a autenticação com os mesmos subscrição de Olá toomanage estão associados.</span><span class="sxs-lookup"><span data-stu-id="f9910-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="f9910-108">Se quiser obter mais informações sobre os certificados do Azure (incluindo a criar um certificado autoassinado), consulte o artigo [descrição geral de certificados para serviços de nuvem do Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="f9910-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="f9910-109">Também pode utilizar [do Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate-código de cliente para fins de automatização.</span><span class="sxs-lookup"><span data-stu-id="f9910-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="f9910-110">Carregar um certificado de gestão</span><span class="sxs-lookup"><span data-stu-id="f9910-110">Upload a management certificate</span></span>
<span data-ttu-id="f9910-111">Depois de ter um certificado de gestão criado, (ficheiro. cer com apenas Olá chave pública) pode carregá-lo no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="f9910-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="f9910-112">Quando estiver disponível no portal de Olá certificado de Olá, qualquer pessoa com um certificado correspondente (chave privada) pode ligar através de recursos de Olá de API de gestão e acesso Olá da Olá associado à subscrição.</span><span class="sxs-lookup"><span data-stu-id="f9910-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="f9910-113">Inicie sessão no toohello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9910-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="f9910-114">Clique em **mais serviços** na lista de serviço do Azure do Olá na parte inferior, em seguida, selecione **subscrições** no Olá _geral_ grupo de serviço.</span><span class="sxs-lookup"><span data-stu-id="f9910-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Menu de subscrição](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="f9910-116">Certifique-se tooselect Olá correta subscrição que pretende que o tooassociate com certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="f9910-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="f9910-117">Depois de selecionar a subscrição correta Olá, prima **certificados de gestão** no Olá _definições_ grupo.</span><span class="sxs-lookup"><span data-stu-id="f9910-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![Definições](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="f9910-119">Olá prima **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="f9910-119">Press hello **Upload** button.</span></span>

    ![Carregar a página de certificados](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="f9910-121">Preencha as informações de caixa de diálogo Olá e prima **carregar**.</span><span class="sxs-lookup"><span data-stu-id="f9910-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![Definições](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="f9910-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f9910-123">Next steps</span></span>
<span data-ttu-id="f9910-124">Agora que tem um certificado de gestão associado a uma subscrição, pode (após a instalação Olá correspondente ao certificado localmente) através de programação ligar toohello [REST API do modelo de implementação clássica](https://msdn.microsoft.com/library/azure/mt420159.aspx) e automatizar Olá vários recursos do Azure que também estão associados essa subscrição.</span><span class="sxs-lookup"><span data-stu-id="f9910-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
