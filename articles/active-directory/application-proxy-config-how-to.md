---
title: "aaaHow tooconfigure uma aplicação de Proxy de aplicações | Microsoft Docs"
description: "Saiba como toocreate um configurar uma aplicação de Proxy de aplicações em alguns passos simples"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="4f2f4-103">Como tooconfigure uma aplicação de Proxy de aplicações</span><span class="sxs-lookup"><span data-stu-id="4f2f4-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="4f2f4-104">Este artigo ajudá-lo toounderstand como tooconfigure uma aplicação de Proxy de aplicações dentro do Azure AD tooexpose sua toohello de aplicações no local na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="4f2f4-105">Documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="4f2f4-105">Recommended documents</span></span> 

<span data-ttu-id="4f2f4-106">toolearn sobre configurações inicial Olá e criação de uma aplicação de Proxy de aplicações através do Portal de administração de Olá siga Olá [publicar aplicações através do Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="4f2f4-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="4f2f4-107">Para obter mais informações sobre como configurar conectores, consulte [ativar o Proxy da aplicação no portal do Azure de Olá](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="4f2f4-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="4f2f4-108">Para informações sobre como carregar certificados e a utilização de domínios personalizados, consulte [trabalhar com domínios personalizados no Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="4f2f4-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="4f2f4-109">Criar Olá/definição da aplicação Olá URLs</span><span class="sxs-lookup"><span data-stu-id="4f2f4-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="4f2f4-110">Se estiver a seguir os passos de Olá em Olá [publicar aplicações através do Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) tem e a documentação de obter um erro ao criar a aplicação Olá, consulte os detalhes do erro Olá para informações e sugestões sobre como aplicação de Olá toofix.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="4f2f4-111">A maioria das mensagens de erro incluem uma correção sugerida.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="4f2f4-112">erros comuns tooavoid, certifique-se:</span><span class="sxs-lookup"><span data-stu-id="4f2f4-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="4f2f4-113">É um administrador com permissão toocreate uma aplicação de Proxy de aplicações</span><span class="sxs-lookup"><span data-stu-id="4f2f4-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="4f2f4-114">URL interno Olá é exclusivo</span><span class="sxs-lookup"><span data-stu-id="4f2f4-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="4f2f4-115">URL externo Olá é exclusivo</span><span class="sxs-lookup"><span data-stu-id="4f2f4-115">hello external URL is unique</span></span>

-   <span data-ttu-id="4f2f4-116">Olá URLs início com http ou https e terminar com um "/"</span><span class="sxs-lookup"><span data-stu-id="4f2f4-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="4f2f4-117">URL de Olá deve ser um nome de domínio, não um endereço IP</span><span class="sxs-lookup"><span data-stu-id="4f2f4-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="4f2f4-118">mensagem de erro de saudação deve apresentar no canto superior direito Olá quando criar aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="4f2f4-119">Também pode selecionar Olá notificação ícone toosee Olá as mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Pedido de notificação](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="4f2f4-121">Configurar grupos de conectores/conector</span><span class="sxs-lookup"><span data-stu-id="4f2f4-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="4f2f4-122">Se estiver a ter dificuldade em configurar a sua aplicação devido a aviso sobre conectores Olá e grupos de conector, consulte as instruções sobre como ativar o Proxy da aplicação para obter detalhes sobre como conectores toodownload.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="4f2f4-123">Se pretender mais informações sobre conectores toolearn, veja Olá [documentação de conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="4f2f4-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="4f2f4-124">Se os conectores estão inativos, isto significa que estão serviço de Olá tooreach não é possível.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="4f2f4-125">Isto é, muitas vezes, porque todas as portas de Olá necessárias não estão abertas.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="4f2f4-126">toosee uma lista de portas necessárias, consulte a secção de pré-requisitos de Olá de Olá ativar a documentação do Proxy de aplicações.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="4f2f4-127">Carregar certificados para domínios personalizados</span><span class="sxs-lookup"><span data-stu-id="4f2f4-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="4f2f4-128">Domínios personalizados permitem-lhe domínio de Olá toospecify do seu URLs externos.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="4f2f4-129">domínios personalizados toouse, precisa de tooupload Olá certificado desse domínio.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="4f2f4-130">Para obter informações sobre como utilizar domínios e certificados personalizados, consulte [trabalhar com domínios personalizados no Proxy de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="4f2f4-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="4f2f4-131">Se tiver problemas com a carregar o certificado, procure mensagens de erro Olá no portal de Olá para obter informações adicionais sobre o problema de Olá com certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="4f2f4-132">Problemas de certificado comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="4f2f4-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="4f2f4-133">Certificado expirado</span><span class="sxs-lookup"><span data-stu-id="4f2f4-133">Expired certificate</span></span>

-   <span data-ttu-id="4f2f4-134">O certificado é autoassinado</span><span class="sxs-lookup"><span data-stu-id="4f2f4-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="4f2f4-135">Certificado não tem chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="4f2f4-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="4f2f4-136">apresentação de mensagem de erro de Olá no Olá canto superior direito, tente o certificado de Olá tooupload.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="4f2f4-137">Também pode selecionar Olá notificação ícone toosee Olá as mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="4f2f4-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Pedido de notificação](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="4f2f4-139">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4f2f4-139">Next steps</span></span>
[<span data-ttu-id="4f2f4-140">Publicar aplicações através do Proxy de aplicações do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f2f4-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
