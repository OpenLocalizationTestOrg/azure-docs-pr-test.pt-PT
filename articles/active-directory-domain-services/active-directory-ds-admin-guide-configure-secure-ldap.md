---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do Azure AD | Microsoft Docs"
description: "Configurar o LDAP seguro (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="3a9d7-103">Configurar segura LDAP (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a9d7-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="3a9d7-104">Este artigo mostra como pode permitir proteger Lightweight Directory acesso protocolo (LDAPS) para o seu domínio gerido dos serviços de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="3a9d7-105">LDAP seguro também é conhecido como "acesso protocolo LDAP (Lightweight Directory) através de Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3a9d7-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3a9d7-106">Before you begin</span></span>
<span data-ttu-id="3a9d7-107">tarefas de Olá tooperform apresentadas neste artigo, tem de:</span><span class="sxs-lookup"><span data-stu-id="3a9d7-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="3a9d7-108">Um **subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="3a9d7-109">Um **diretório do Azure AD** -está sincronizada com um diretório no local ou um diretório apenas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="3a9d7-110">**Serviços de domínio do Azure AD** tem de estar ativada para o diretório de Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="3a9d7-111">Se ainda não o feito, siga todas as tarefas de Olá descritas em Olá [guia de introdução](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3a9d7-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="3a9d7-112">A **certificado toobe utilizado tooenable LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="3a9d7-113">**Recomendado** -obter um certificado de uma autoridade de certificação pública fidedigna.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="3a9d7-114">Esta opção de configuração é mais segura.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="3a9d7-115">Em alternativa, pode também optar por demasiado[criar um certificado autoassinado](#task-1---obtain-a-certificate-for-secure-ldap) conforme mostrado posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="3a9d7-116">Requisitos do certificado LDAP seguro Olá</span><span class="sxs-lookup"><span data-stu-id="3a9d7-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="3a9d7-117">Adquirir um certificado válido por Olá seguir diretrizes, antes de ativar LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="3a9d7-118">Ocorrerem falhas, se tentar tooenable LDAP seguro para o seu domínio gerido com um certificado inválido incorreto.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="3a9d7-119">**Emissor fidedigno** -Olá certificado tem de ser emitido por uma autoridade fidedigna pelos computadores que ligam toohello domínio gerido utilizando LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="3a9d7-120">Esta autoridade pode ser uma autoridade de certificação pública fidedigna por estes computadores.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="3a9d7-121">**Duração** -Olá certificado tem de ser válido para, pelo menos, Olá próximos 3 a 6 meses.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="3a9d7-122">LDAP acesso tooyour gerido domínio seguro é interrompido quando Olá certificado expirar.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="3a9d7-123">**Nome do requerente** -nome de requerente Olá no certificado Olá tem de ser um caráter universal para o seu domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="3a9d7-124">Por exemplo, se o seu domínio com o nome 'contoso100.com', nome do requerente do certificado Olá tem de ser ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="3a9d7-125">Definir Olá DNS (nome alternativo do requerente) toothis universal nome.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="3a9d7-126">**Utilização da chave** - certificado Olá tem de ser configurado para Olá seguinte utiliza - as assinaturas Digital e cifragem de chaves.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="3a9d7-127">**Objetivo do certificado** -Olá certificado tem de ser válido para autenticação de servidor SSL.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="3a9d7-128">**Autoridades de certificação empresarial:** dos serviços de domínio do Azure AD não suporta a utilização segurados LDAP certificados emitidos pela autoridade de certificação empresarial da sua organização.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="3a9d7-129">Esta restrição é porque o serviço de Olá não fidedigna a AC como uma autoridade de certificação de raiz empresarial.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="3a9d7-130">Tarefa 1 - obter um certificado para o LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="3a9d7-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="3a9d7-131">tarefa primeiro Olá envolve a obtenção de um certificado utilizado para proteger LDAP acesso toohello domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="3a9d7-132">Tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="3a9d7-132">You have two options:</span></span>

* <span data-ttu-id="3a9d7-133">Obtenha um certificado de uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="3a9d7-134">autoridade de Olá pode ser uma autoridade de certificação pública.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="3a9d7-135">Crie um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="3a9d7-136">Opção (recomendado) - obter um certificado LDAP seguro de uma autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="3a9d7-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="3a9d7-137">Se a sua organização obtém os certificados de autoridades de certificação pública, terá de tooobtain Olá seguro LDAP certificado nessa autoridade de certificação pública.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="3a9d7-138">Quando solicitar um certificado, certifique-se de que satisfaçam todos os requisitos de Olá descritos na [requisitos para o certificado LDAP seguro Olá](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="3a9d7-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="3a9d7-139">Computadores cliente que necessitam de tooconnect toohello domínio gerido utilizando LDAP seguro têm de confiar emissor Olá do certificado LDAP seguro Olá.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="3a9d7-140">Opção B - criar um certificado autoassinado para o LDAP seguro</span><span class="sxs-lookup"><span data-stu-id="3a9d7-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="3a9d7-141">Se não conta toouse um certificado de uma autoridade de certificação pública, pode escolher um certificado autoassinado para o LDAP seguro para toocreate.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="3a9d7-142">**Criar um certificado autoassinado com o PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3a9d7-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="3a9d7-143">No seu computador Windows, abra uma nova janela do PowerShell como **administrador** e Olá tipo os seguintes comandos, toocreate um novo certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="3a9d7-144">No Olá anterior exemplo, substitua '*. contoso100.com' com o nome de domínio DNS Olá do seu domínio gerido. Por exemplo, se tiver criado um domínio gerido chamado 'contoso100.onmicrosoft.com', substitua '*. contoso100.com' no Olá acima script com ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="3a9d7-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Selecionar o Azure AD Directory](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="3a9d7-146">certificado autoassinado Olá recém-criado é colocado no arquivo de certificados de Olá local da máquina.</span><span class="sxs-lookup"><span data-stu-id="3a9d7-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="3a9d7-147">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="3a9d7-147">Next step</span></span>
[<span data-ttu-id="3a9d7-148">Tarefa 2 - exportar Olá segura LDAP certificado tooa. Ficheiro PFX</span><span class="sxs-lookup"><span data-stu-id="3a9d7-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
