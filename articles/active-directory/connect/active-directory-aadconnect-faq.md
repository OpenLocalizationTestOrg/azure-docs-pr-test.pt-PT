---
title: "Do Azure Active Directory Connect: FAQ – | Microsoft Docs"
description: "Esta página tem perguntas mais frequentes sobre o Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="2fb1a-103">Perguntas mais frequentes sobre Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="2fb1a-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="2fb1a-104">Instalação geral</span><span class="sxs-lookup"><span data-stu-id="2fb1a-104">General installation</span></span>
<span data-ttu-id="2fb1a-105">**P: instalação funcionará se Olá Administrador Global do AD do Azure tiver 2FA ativado?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="2fb1a-106">Com Olá compilações de Fevereiro de 2016, isto é suportado.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="2fb1a-107">**P: existe uma forma tooinstall do Azure AD Connect automático?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="2fb1a-108">É apenas suportado tooinstall do Azure AD Connect utilizando o Assistente de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="2fb1a-109">Não é suportada uma instalação automática e silenciosa.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="2fb1a-110">**P: Tenho uma floresta em que um domínio não pode ser contactado. Como instalar o Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="2fb1a-111">Com Olá compilações de Fevereiro de 2016, isto é suportado.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="2fb1a-112">**P: Olá o trabalho de agente de estado de funcionamento de AD DS no server core?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="2fb1a-113">Sim.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-113">Yes.</span></span> <span data-ttu-id="2fb1a-114">Depois de instalar o agente de Olá, pode concluir o processo de registo de Olá utilizando Olá seguinte cmdlet do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2fb1a-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="2fb1a-115">Rede</span><span class="sxs-lookup"><span data-stu-id="2fb1a-115">Network</span></span>
<span data-ttu-id="2fb1a-116">**P: Posso tem uma firewall, o dispositivo de rede ou outra coisa que limita a ligações de tempo máximo de Olá pode permanecer aberta na minha rede. Quanto tempo os meus limiar de tempo limite de lado do cliente estará ao utilizar o Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="2fb1a-117">Todo o software de rede, dispositivos físicos ou há mais alguma coisa que os limites de tempo máximo de Olá ligações podem permanecer abertas deve utilizar um limiar de, pelo menos, 5 minutos (300 segundos) para conetividade entre Olá servidor onde hello do Azure AD Connect cliente está instalado e o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="2fb1a-118">Isto também se aplica as ferramentas de sincronização do Microsoft Identity tooall anteriormente lançada.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="2fb1a-119">**P: são SLDs (domínios de etiqueta única) suportada?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="2fb1a-120">Não, do Azure AD Connect não suporta local florestas/domínios SLDs a utilizar.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="2fb1a-121">**P: são "separada por pontos" com o nome de NetBios suportado?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="2fb1a-122">Não, do Azure AD Connect não suporta florestas/domínios de no local onde o nome de NetBios Olá contenha um ponto final "." no nome de Olá.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="2fb1a-123">Federação</span><span class="sxs-lookup"><span data-stu-id="2fb1a-123">Federation</span></span>
<span data-ttu-id="2fb1a-124">**P: o que devo fazer se receber uma mensagem de e-mail que perguntar-me toorenew meu certificado do Office 365**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="2fb1a-125">Utilize as orientações de Olá que está destacada em Olá [renovar certificados](active-directory-aadconnect-o365-certs.md) tópico sobre como toorenew Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="2fb1a-126">**P: Posso ter "Atualizar automaticamente da entidade confiadora" definido para da entidade confiadora do Office 365. É necessário tootake qualquer ação quando faz o meu automaticamente o certificado de assinatura de token através de?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="2fb1a-127">Utilize as orientações de Olá que é descrita no artigo Olá [renovar certificados](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="2fb1a-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="2fb1a-128">Ambiente</span><span class="sxs-lookup"><span data-stu-id="2fb1a-128">Environment</span></span>
<span data-ttu-id="2fb1a-129">**P: é it suportado toorename Olá servidor após a instalação do Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="2fb1a-130">Não.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-130">No.</span></span> <span data-ttu-id="2fb1a-131">Alterar o nome do servidor Olá toonot de motor de sincronização de Olá causa será tooconnect capaz de base de dados SQL de toohello e serviço Olá não será capaz de toostart.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="2fb1a-132">Dados de identidade</span><span class="sxs-lookup"><span data-stu-id="2fb1a-132">Identity data</span></span>
<span data-ttu-id="2fb1a-133">**P: Olá UPN (userPrincipalName) atributo no Azure AD não corresponde ao hello UPN no local - por que motivo?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="2fb1a-134">Consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="2fb1a-134">See these articles:</span></span>

* [<span data-ttu-id="2fb1a-135">Olá, os nomes de utilizador no Office 365, Azure ou Intune não correspondem ao UPN no local ou o ID de início de sessão alternativo</span><span class="sxs-lookup"><span data-stu-id="2fb1a-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="2fb1a-136">As alterações não são sincronizadas pela ferramenta de sincronização de diretórios do Azure Active Directory Olá depois de alterar Olá UPN de um toouse de conta de utilizador outro domínio federado</span><span class="sxs-lookup"><span data-stu-id="2fb1a-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="2fb1a-137">Também pode configurar userPrincipalName de Olá ao tooupdate do motor de sincronização do Azure AD tooallow Olá conforme descrito em [funcionalidades do serviço de sincronização do Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="2fb1a-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="2fb1a-138">**P: for it suportado toosoft correspondência no local objetos de AD grupo/contacte com o objetos existentes do grupo/contacte do Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="2fb1a-139">Não, isto não é atualmente suportado.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-139">No, this is currently not supported.</span></span>

<span data-ttu-id="2fb1a-140">**P: é it suportado toomanually definir o atributo de ImmutableId no existente do Azure AD grupo/contacte objetos toohard correspondência tooon local objetos de AD grupo/contacto?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="2fb1a-141">Não, isto não é atualmente suportado.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="2fb1a-142">Configuração personalizada</span><span class="sxs-lookup"><span data-stu-id="2fb1a-142">Custom configuration</span></span>
<span data-ttu-id="2fb1a-143">**P: onde estão Olá cmdlets do PowerShell do Azure AD Connect documentado?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="2fb1a-144">Com exceção de Olá dos cmdlets de Olá documentados neste site, os outros cmdlets do PowerShell encontrados no Azure AD Connect não são suportados para utilização do cliente.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="2fb1a-145">**P: Posso utilizar "Servidor de exportação/importação do servidor" encontrada no *Synchronization Service Manager* toomove configuração entre servidores?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="2fb1a-146">Não.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-146">No.</span></span> <span data-ttu-id="2fb1a-147">Esta opção não irá obter todas as definições de configuração e não deve ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="2fb1a-148">Em vez disso, deve utilizar configuração base do Olá assistente toocreate Olá no segundo servidor de Olá e utilizar Olá sincronização regra editor toogenerate PowerShell scripts toomove qualquer regra personalizada entre servidores.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="2fb1a-149">Consulte [Swing migração](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="2fb1a-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="2fb1a-150">**P: as palavras-passe ser colocadas em cache para a página Olá o início de sessão do Azure e pode isto impedida porque contém um elemento de entrada de palavra-passe com Olá autocomplete = "false" atributo?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="2fb1a-151">Atualmente não suportamos modificação Olá HTML atributos Olá campo palavra-passe entrado, incluindo a tag de conclusão automática de Olá.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="2fb1a-152">Estamos atualmente uma funcionalidade que vai permitir Javascript personalizada que lhe permitirá tooadd qualquer campo de palavra-passe de toohello de atributo.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="2fb1a-153">Deve ser posterior disponível parte de 2017.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="2fb1a-154">**P: na página de início de sessão do Azure Olá, são apresentados os nomes de utilizador para os utilizadores que tenham anteriormente sessão iniciada com êxito.  Este comportamento pode ser ativado?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="2fb1a-155">Atualmente não suportamos atributos HTML Olá modificação da página de início de sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="2fb1a-156">Estamos atualmente uma funcionalidade que vai permitir Javascript personalizada que lhe permitirá tooadd qualquer campo de palavra-passe de toohello de atributo.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="2fb1a-157">Deve ser posterior disponível parte de 2017.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="2fb1a-158">**P: existe uma forma tooprevent sessões simultâneas?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="2fb1a-159">Não.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="2fb1a-160">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="2fb1a-160">Troubleshooting</span></span>
<span data-ttu-id="2fb1a-161">**P: como posso obter ajuda com o Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="2fb1a-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="2fb1a-162">Procurar Olá Base de dados de Conhecimento Microsoft (KB)</span><span class="sxs-lookup"><span data-stu-id="2fb1a-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="2fb1a-163">Procure Olá Base de dados de Conhecimento Microsoft (KB) para problemas de break-fix toocommon soluções técnicas sobre o suporte do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="2fb1a-164">Fóruns do Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2fb1a-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="2fb1a-165">Pode pesquisar e navegue para a technical questões e respostas da Comunidade Olá ou peça ao seu próprio pergunta clicando [aqui](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="2fb1a-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="2fb1a-166">Suporte ao cliente do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2fb1a-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="2fb1a-167">Utilize este suporte de tooget ligação através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb1a-167">Use this link tooget support through hello Azure portal.</span></span>

