---
title: "Do Azure AD Connect: Instâncias do serviço de sincronização | Microsoft Docs"
description: "Esta página documentos considerações especiais para instâncias do Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="6cea2-103">O Azure AD Connect: Considerações especiais para instâncias</span><span class="sxs-lookup"><span data-stu-id="6cea2-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="6cea2-104">O Azure AD Connect é utilizado frequentemente com a instância de todo o mundo Olá do Azure AD e o Office 365.</span><span class="sxs-lookup"><span data-stu-id="6cea2-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="6cea2-105">Mas também existem outras instâncias e estes têm diferentes requisitos para os URLs e outras considerações especiais.</span><span class="sxs-lookup"><span data-stu-id="6cea2-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="6cea2-106">Microsoft Cloud Alemanha</span><span class="sxs-lookup"><span data-stu-id="6cea2-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="6cea2-107">Olá [Datacenters da Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) é uma nuvem sovereign operada por uma trustee de dados em alemão.</span><span class="sxs-lookup"><span data-stu-id="6cea2-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="6cea2-108">URLs tooopen no servidor de proxy</span><span class="sxs-lookup"><span data-stu-id="6cea2-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="6cea2-109">\*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="6cea2-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="6cea2-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="6cea2-110">\*.windows.net</span></span> |
| <span data-ttu-id="6cea2-111">+ Listas de revogação de certificados</span><span class="sxs-lookup"><span data-stu-id="6cea2-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="6cea2-112">Quando inicia sessão no inquilino do Azure AD tooyour, tem de utilizar uma conta no domínio de onmicrosoft.de Olá.</span><span class="sxs-lookup"><span data-stu-id="6cea2-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="6cea2-113">Funcionalidades atualmente não estão presentes na Olá Microsoft Cloud Datacenters:</span><span class="sxs-lookup"><span data-stu-id="6cea2-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="6cea2-114">**O Azure AD Connect Health** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="6cea2-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="6cea2-115">**As atualizações automáticas** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="6cea2-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="6cea2-116">**Repetição de escrita de palavras-passe** está disponível para pré-visualização com a versão do Azure AD Connect 1.1.570.0 e depois.</span><span class="sxs-lookup"><span data-stu-id="6cea2-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="6cea2-117">Não estão disponíveis outros serviços do Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="6cea2-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="6cea2-118">Nuvem do Microsoft Azure Government</span><span class="sxs-lookup"><span data-stu-id="6cea2-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="6cea2-119">Olá [cloud do Microsoft Azure Government](https://azure.microsoft.com/features/gov/) é uma nuvem para dos EUA.</span><span class="sxs-lookup"><span data-stu-id="6cea2-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="6cea2-120">Esta nuvem é suportada por versões anteriores do DirSync.</span><span class="sxs-lookup"><span data-stu-id="6cea2-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="6cea2-121">De compilação 1.1.180 do Azure AD Connect, Olá próxima geração da nuvem hello é suportado.</span><span class="sxs-lookup"><span data-stu-id="6cea2-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="6cea2-122">Esta geração está a utilizar apenas de E.U.A. baseada em pontos finais e ter uma lista de URLs tooopen diferente no seu servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="6cea2-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="6cea2-123">URLs tooopen no servidor de proxy</span><span class="sxs-lookup"><span data-stu-id="6cea2-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="6cea2-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6cea2-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="6cea2-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="6cea2-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="6cea2-126">\*. gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6cea2-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="6cea2-127">+ Listas de revogação de certificados</span><span class="sxs-lookup"><span data-stu-id="6cea2-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="6cea2-128">O Azure AD Connect não é capaz de tooautomatically detetar que o inquilino do Azure AD está localizado na nuvem de Government Olá.</span><span class="sxs-lookup"><span data-stu-id="6cea2-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="6cea2-129">Em vez disso, terá de Olá tootake seguintes ações quando instalar o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6cea2-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="6cea2-130">Inicie a instalação do Olá do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6cea2-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="6cea2-131">Quando for apresentada a página primeiro olá onde é suposto tooaccept Olá EULA, não continuar, mas deixe o Assistente de instalação de Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="6cea2-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="6cea2-132">Inicie o regedit e alterar a chave de registo Olá `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valor `2`.</span><span class="sxs-lookup"><span data-stu-id="6cea2-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="6cea2-133">Voltar atrás Assistente de instalação do toohello do Azure AD Connect, aceite o EULA de Olá e continuar.</span><span class="sxs-lookup"><span data-stu-id="6cea2-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="6cea2-134">Durante a instalação, certifique-se de que toouse Olá **configuração personalizada** caminho de instalação (e não a instalação Express).</span><span class="sxs-lookup"><span data-stu-id="6cea2-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="6cea2-135">Em seguida, continue a instalação de Olá como habitualmente.</span><span class="sxs-lookup"><span data-stu-id="6cea2-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="6cea2-136">Funcionalidades atualmente não estão presentes na nuvem do Microsoft Azure Government de Olá:</span><span class="sxs-lookup"><span data-stu-id="6cea2-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="6cea2-137">**O Azure AD Connect Health** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="6cea2-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="6cea2-138">**As atualizações automáticas** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="6cea2-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="6cea2-139">**Repetição de escrita de palavras-passe** está disponível para pré-visualização com a versão do Azure AD Connect 1.1.570.0 e depois.</span><span class="sxs-lookup"><span data-stu-id="6cea2-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="6cea2-140">Não estão disponíveis outros serviços do Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="6cea2-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cea2-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6cea2-141">Next steps</span></span>
<span data-ttu-id="6cea2-142">Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="6cea2-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
