---
title: "Serviços de back-end aaaSecure utilizando a autenticação de certificado de cliente - API Management do Azure | Microsoft Docs"
description: "Saiba como serviços de back-end toosecure utilizando o cliente de certificado de autenticação na API Management do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="1f88c-103">Como serviços de back-end toosecure utilizando o cliente de certificado de autenticação na API Management do Azure</span><span class="sxs-lookup"><span data-stu-id="1f88c-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="1f88c-104">A API Management fornece Olá capacidade toosecure toohello back-end serviço de acesso de uma API utilizando certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="1f88c-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="1f88c-105">Este guia mostra como toomanage certificados no portal do publicador Olá API e como tooconfigure uma API toouse tooaccess um certificado respetivo serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="1f88c-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="1f88c-106">Para obter informações sobre como gerir certificados Olá API de REST de gestão de API a utilizar, consulte [entidade de certificado de API do REST de gestão do Azure API][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="1f88c-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="1f88c-107"><a name="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f88c-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="1f88c-108">Este guia mostra como tooconfigure as API Management service instância toouse cliente certificado autenticação tooaccess Olá serviço de back-end para uma API.</span><span class="sxs-lookup"><span data-stu-id="1f88c-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="1f88c-109">Antes de os passos seguinte Olá neste tópico, deve ter o seu serviço de back-end configurado para autenticação de certificados de cliente ([certificado tooconfigure autenticação em sites Web do Azure consulte o artigo toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), e ter acesso toohello certificado e Olá palavra-passe para o certificado de Olá para carregar no portal do publicador da API Management Olá.</span><span class="sxs-lookup"><span data-stu-id="1f88c-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="1f88c-110"><a name="step1"></a>Carregar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="1f88c-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="1f88c-111">tooget iniciado, clique em **portal do publicador** no Olá Portal do Azure para o seu serviço de API Management.</span><span class="sxs-lookup"><span data-stu-id="1f88c-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="1f88c-112">Isto leva-o portal do publicador da API Management toohello.</span><span class="sxs-lookup"><span data-stu-id="1f88c-112">This takes you toohello API Management publisher portal.</span></span>

![Portal do publicador da API][api-management-management-console]

> <span data-ttu-id="1f88c-114">Se ainda não criou uma instância de serviço de API Management, consulte [criar uma instância de serviço de API Management] [ Create an API Management service instance] no Olá [introdução à API Management do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="1f88c-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="1f88c-115">Clique em **segurança** de Olá **API Management** menu Olá esquerda e clique em **certificados de cliente**.</span><span class="sxs-lookup"><span data-stu-id="1f88c-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![Certificados de cliente][api-management-security-client-certificates]

<span data-ttu-id="1f88c-117">tooupload um novo certificado, clique em **carregar certificado**.</span><span class="sxs-lookup"><span data-stu-id="1f88c-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Carregar certificado][api-management-upload-certificate]

<span data-ttu-id="1f88c-119">Procurar tooyour certificado e, em seguida, introduza a palavra-passe de Olá certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="1f88c-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="1f88c-120">tem de estar no certificado Olá **. pfx** formato.</span><span class="sxs-lookup"><span data-stu-id="1f88c-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="1f88c-121">Certificados autoassinados são permitidos.</span><span class="sxs-lookup"><span data-stu-id="1f88c-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Carregar certificado][api-management-upload-certificate-form]

<span data-ttu-id="1f88c-123">Clique em **carregar** certificado de Olá tooupload.</span><span class="sxs-lookup"><span data-stu-id="1f88c-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="1f88c-124">palavra-passe do Olá certificado é validado neste momento.</span><span class="sxs-lookup"><span data-stu-id="1f88c-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="1f88c-125">Se estiver incorreto é apresentada uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="1f88c-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificado carregado][api-management-certificate-uploaded]

<span data-ttu-id="1f88c-127">Depois do certificado de Olá é carregado, é apresentado no Olá **certificados de cliente** separador. Se tiver vários certificados, tome nota do requerente Olá ou Olá últimos quatro carateres do thumbprint Olá, que são certificados de Olá tooselect utilizada quando configurar um toouse API certificados, conforme descritas na íntegra no seguinte Olá [configurar um API toouse um certificado de cliente para autenticação de gateway] [ Configure an API toouse a client certificate for gateway authentication] secção.</span><span class="sxs-lookup"><span data-stu-id="1f88c-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="1f88c-128">tooturn desativar validação da cadeia de certificados quando utilizar, por exemplo, um certificado autoassinado, siga os passos de Olá descritos neste FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="1f88c-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="1f88c-129"><a name="step1a"></a>Eliminar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="1f88c-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="1f88c-130">toodelete um certificado, clique em **eliminar** ao lado do certificado pretendido Olá.</span><span class="sxs-lookup"><span data-stu-id="1f88c-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Eliminar o certificado][api-management-certificate-delete]

<span data-ttu-id="1f88c-132">Clique em **Sim, elimine-o** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1f88c-132">Click **Yes, delete it** tooconfirm.</span></span>

![Confirmar eliminação][api-management-confirm-delete]

<span data-ttu-id="1f88c-134">Se o certificado de Olá está a ser utilizado por uma API, um ecrã de aviso é apresentado.</span><span class="sxs-lookup"><span data-stu-id="1f88c-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="1f88c-135">certificado de Olá toodelete tem de remover primeiro Olá de certificado a partir de qualquer APIs que estão configurado toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="1f88c-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![Confirmar eliminação][api-management-confirm-delete-policy]

## <span data-ttu-id="1f88c-137"><a name="step2"></a>Configurar toouse uma API um certificado de cliente para autenticação de gateway</span><span class="sxs-lookup"><span data-stu-id="1f88c-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="1f88c-138">Clique em **APIs** de Olá **API Management** Olá menu à esquerda, clique no nome de Olá da API de Olá pretendida e clique Olá **segurança** separador.</span><span class="sxs-lookup"><span data-stu-id="1f88c-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![Segurança de API][api-management-api-security]

<span data-ttu-id="1f88c-140">Selecione **certificados de cliente** de Olá **com credenciais** na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="1f88c-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![Certificados de cliente][api-management-mutual-certificates]

<span data-ttu-id="1f88c-142">Selecione Olá certificado pretendido Olá **certificado de cliente** na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="1f88c-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="1f88c-143">Se existirem vários certificados pode observar o requerente Olá ou Olá últimos quatro carateres do thumbprint Olá conforme indicado no Olá anterior secção toodetermine Olá certificado correto.</span><span class="sxs-lookup"><span data-stu-id="1f88c-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Selecione o certificado][api-management-select-certificate]

<span data-ttu-id="1f88c-145">Clique em **guardar** toohello de alteração de configuração do toosave Olá API.</span><span class="sxs-lookup"><span data-stu-id="1f88c-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="1f88c-146">Esta alteração tem efeita imediato e chamadas toooperations essa API utilizará Olá tooauthenticate de certificado no servidor de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="1f88c-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![Guardar as alterações de API][api-management-save-api]

> <span data-ttu-id="1f88c-148">Quando é especificado um certificado para autenticação de gateway para o serviço de back-end de Olá de uma API, este torna-se parte da política de Olá para essa API e pode ser visualizado no editor de políticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="1f88c-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Política de certificado][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="1f88c-150">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1f88c-150">Next steps</span></span>
<span data-ttu-id="1f88c-151">Para mais informações sobre outra formas toosecure o serviço de back-end, tal como HTTP autenticação básica ou partilhado secreta, consulte Olá seguir as vídeo.</span><span class="sxs-lookup"><span data-stu-id="1f88c-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



