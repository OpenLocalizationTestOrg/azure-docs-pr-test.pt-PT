---
title: "instalar aaaProblem Olá conector do agente de Proxy de aplicações | Microsoft Docs"
description: "Como tootroubleshoot problemas que poderá Olá, enfrentam ao instalar o conector do agente de Proxy de aplicações"
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
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="34508-103">Problema Olá conector do agente de Proxy de aplicações a instalar</span><span class="sxs-lookup"><span data-stu-id="34508-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="34508-104">Conector do Proxy de aplicações do Microsoft AAD é um componente de domínio interno que utiliza a conectividade de Olá tooestablish de ligações de saída do domínio interno do Olá nuvem ponto final disponível toohello.</span><span class="sxs-lookup"><span data-stu-id="34508-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="34508-105">Áreas de problema geral com a instalação do conector</span><span class="sxs-lookup"><span data-stu-id="34508-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="34508-106">Quando a instalação de Olá de um conector falha, causa de raiz de Olá é normalmente uma das Olá seguintes áreas:</span><span class="sxs-lookup"><span data-stu-id="34508-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="34508-107">**Conectividade** – toocomplete uma instalação com êxito, Olá tooregister de necessidades do novo conector e estabelecer propriedades de fidedignidade futuras.</span><span class="sxs-lookup"><span data-stu-id="34508-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="34508-108">Isto é feito através da ligação toohello serviço de nuvem do Proxy de aplicações do AAD.</span><span class="sxs-lookup"><span data-stu-id="34508-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="34508-109">**Estabelecimento de confiança** – novo conector de Olá cria um certificado autoassinado e regista toohello o serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="34508-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="34508-110">**Autenticação de Olá, admin** – durante a instalação, Olá utilizador tem de fornecer credenciais de administrador de instalação de conectores toocomplete Olá.</span><span class="sxs-lookup"><span data-stu-id="34508-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="34508-111">Certifique-se de que serviço de Proxy de aplicações de nuvem de toohello de conectividade e página Microsoft Login</span><span class="sxs-lookup"><span data-stu-id="34508-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="34508-112">**Objetivo:** Certifique-se de que a máquina conector Olá pode ligar-se de ponto final do registo de Proxy de aplicações do AAD toohello, bem como a página de início de sessão da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="34508-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="34508-113">Abra um toohello browser e aceda a seguinte página web: <https://aadap-portcheck.connectorporttest.msappproxy.net> e certifique-se de que tooCentral de conectividade Olá E.U.A. e centros de dados de EUA Leste com as portas 9090 e 9091 está a funcionar.</span><span class="sxs-lookup"><span data-stu-id="34508-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="34508-114">Se qualquer um dessas portas não for bem sucedida (não tem uma marca de verificação verde), certifique-se de que Olá Firewall ou tem o proxy de back-end \*. msappproxy.net com portas 9090 e 9091 definido corretamente.</span><span class="sxs-lookup"><span data-stu-id="34508-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="34508-115">Abra um browser (separador separado) e aceda toohello seguir página web: <https://login.microsoftonline.com>, certifique-se de que pode iniciar sessão toothat página.</span><span class="sxs-lookup"><span data-stu-id="34508-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="34508-116">Certifique-se de que os componentes de máquina e back-end suportem para o certificado de confiança do Proxy de aplicações</span><span class="sxs-lookup"><span data-stu-id="34508-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="34508-117">**Objetivo:** Certifique-se de que a máquina de conector Olá, back-end proxy e firewall do podem suportar certificado Olá criado pelo conector Olá confiança futuras.</span><span class="sxs-lookup"><span data-stu-id="34508-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="34508-118">conector Olá tenta toocreate um certificado de SHA512 que é suportado pelo TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="34508-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="34508-119">Se a máquina Olá ou firewall back-end de Olá e proxy não suportar TLS1.2, instalação de Olá falhar.</span><span class="sxs-lookup"><span data-stu-id="34508-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="34508-120">**problema de Olá tooresolve:**</span><span class="sxs-lookup"><span data-stu-id="34508-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="34508-121">Certifique-se a máquina de Olá suporta TLS1.2 – versões de todas as janelas após 2012 R2 devem suportar TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="34508-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="34508-122">Se a máquina de conector está a partir de uma versão do 2012 R2 ou versões anteriores, certifique-se de que Olá KBs seguintes estão instalados na máquina de Olá: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="34508-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="34508-123">Contacte o administrador de rede e peça tooverify que Olá back-end proxy e de firewall não bloqueia SHA512 para tráfego de saída.</span><span class="sxs-lookup"><span data-stu-id="34508-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="34508-124">Certifique-se de administração utilizados tooinstall Olá conector</span><span class="sxs-lookup"><span data-stu-id="34508-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="34508-125">**Objetivo:** Certifique-se de que o utilizador Olá que tenta conector de Olá tooinstall é um administrador com as credenciais corretas.</span><span class="sxs-lookup"><span data-stu-id="34508-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="34508-126">Atualmente, Olá utilizador tem de ser um administrador global para Olá toosucceed de instalação.</span><span class="sxs-lookup"><span data-stu-id="34508-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="34508-127">**as credenciais de Olá tooverify estão corretas:**</span><span class="sxs-lookup"><span data-stu-id="34508-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="34508-128">Ligar demasiado<https://login.microsoftonline.com> e utilize Olá as mesmas credenciais.</span><span class="sxs-lookup"><span data-stu-id="34508-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="34508-129">Certifique-se de que o início de sessão Olá é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="34508-129">Make sure hello login is successful.</span></span> <span data-ttu-id="34508-130">Pode verificar a função de utilizador Olá acedendo demasiado**do Azure Active Directory**  - &gt; **utilizadores e grupos**  - &gt; **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="34508-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="34508-131">Selecione a sua conta de utilizador, em seguida, "função de diretório" no menu resultante Olá.</span><span class="sxs-lookup"><span data-stu-id="34508-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="34508-132">Certifique-se de que essa função selecionada Olá é "Administrador Global".</span><span class="sxs-lookup"><span data-stu-id="34508-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="34508-133">Se não é possível tooaccess qualquer um dos Olá páginas ao longo estes passos, não é um administrador global.</span><span class="sxs-lookup"><span data-stu-id="34508-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34508-134">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="34508-134">Next steps</span></span>
[<span data-ttu-id="34508-135">Compreender os conectores de Proxy de aplicações do Azure AD</span><span class="sxs-lookup"><span data-stu-id="34508-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
