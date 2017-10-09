---
title: "configuração federada-início de sessão único para uma aplicação não Galeria de aaaProblem | Microsoft Docs"
description: "Resolver alguns dos problemas comuns de Olá que poderão surgir quando configurar aplicação SAML personalizada federado único início de sessão tooyour que não está listada no Olá Galeria de aplicações do Azure AD"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="de80c-103">Configuração federada-início de sessão único para uma aplicação não galeria do problema</span><span class="sxs-lookup"><span data-stu-id="de80c-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="de80c-104">Se ocorrer um problema ao configurar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="de80c-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="de80c-105">Certifique-se de que seguiu todos os passos de Olá artigo Olá [configurar único início de sessão tooapplications que não estejam na Galeria de aplicações do Azure Active Directory Olá.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="de80c-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="de80c-106">Não é possível adicionar outra instância da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="de80c-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="de80c-107">tooadd uma segunda instância de uma aplicação, terá de toobe capaz de:</span><span class="sxs-lookup"><span data-stu-id="de80c-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="de80c-108">Configure um identificador exclusivo para a segunda instância de Olá.</span><span class="sxs-lookup"><span data-stu-id="de80c-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="de80c-109">Não será Olá tooconfigure capaz de identificador do mesmo utilizado para a primeira instância de Olá.</span><span class="sxs-lookup"><span data-stu-id="de80c-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="de80c-110">Configure um certificado diferente que Olá utilizada para Olá primeira instância.</span><span class="sxs-lookup"><span data-stu-id="de80c-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="de80c-111">Se hello aplicação não suporta qualquer um dos Olá acima.</span><span class="sxs-lookup"><span data-stu-id="de80c-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="de80c-112">Em seguida, não será capaz de tooconfigure uma segunda instância.</span><span class="sxs-lookup"><span data-stu-id="de80c-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="de80c-113">Onde definir o formato do Olá EntityID (identificador de utilizador)</span><span class="sxs-lookup"><span data-stu-id="de80c-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="de80c-114">Não ter o formato de EntityID (utilizador Identifier) de Olá de tooselect consegue que do Azure AD envia toohello aplicação resposta Olá após a autenticação de utilizador.</span><span class="sxs-lookup"><span data-stu-id="de80c-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="de80c-115">Formato de Olá selecione AD do Azure para o atributo de NameID Olá (identificador de utilizador) com base no valor de Olá selecionado ou Olá formato pedido por aplicação Olá Olá SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="de80c-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="de80c-116">Para obter mais informações, visite artigo Olá [protocolo SAML de início de sessão único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na secção de Olá NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="de80c-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="de80c-117">Onde posso obter metadados da aplicação Olá ou o certificado do Azure AD</span><span class="sxs-lookup"><span data-stu-id="de80c-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="de80c-118">metadados da aplicação Olá toodownload ou o certificado do Azure AD, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="de80c-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="de80c-119">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="de80c-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="de80c-120">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="de80c-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="de80c-121">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="de80c-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="de80c-122">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de80c-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="de80c-123">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="de80c-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="de80c-124">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="de80c-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="de80c-125">Selecione aplicação Olá tiver configurado o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="de80c-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="de80c-126">Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="de80c-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="de80c-127">Aceda demasiado**certificado de assinatura de SAML** secção, em seguida, clique em **transferir** valor da coluna.</span><span class="sxs-lookup"><span data-stu-id="de80c-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="de80c-128">Dependendo do que aplicação Olá necessita de configurar o início de sessão único, consulte o toodownload de opção Olá Olá XML de metadados ou Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="de80c-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="de80c-129">Azure AD não fornece uma metadados de Olá tooget URL.</span><span class="sxs-lookup"><span data-stu-id="de80c-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="de80c-130">Olá metadados só podem ser obtidos como um ficheiro XML.</span><span class="sxs-lookup"><span data-stu-id="de80c-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="de80c-131">Não sabe como toocustomize SAML afirmações enviadas tooan aplicação</span><span class="sxs-lookup"><span data-stu-id="de80c-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="de80c-132">toolearn como afirmações de atributo do toocustomize Olá SAML enviada tooyour aplicação, consulte [afirmações mapeamento no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="de80c-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de80c-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="de80c-133">Next steps</span></span>
[<span data-ttu-id="de80c-134">Gestão de aplicações com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de80c-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
