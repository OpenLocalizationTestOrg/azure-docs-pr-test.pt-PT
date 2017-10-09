---
title: "verificação de aaaTwo passo e o AD FS - MFA do Azure | Microsoft Docs"
description: "Esta é a página de autenticação do Olá multi-factor do Azure que descreve como tooget utilizar a MFA do Azure e o AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="0ff2e-103">Introdução ao Multi-Factor Authentication do Azure e aos Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ff2e-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="0ff2e-104"><center>![Nuvem](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="0ff2e-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="0ff2e-105">Se a sua organização tiver federado o seu Active Directory no local com o Azure Active Directory através do AD FS, existem duas opções para utilizar o Multi-Factor Authentication do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="0ff2e-106">Proteger recursos da nuvem com o Multi-Factor Authentication do Azure ou os Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ff2e-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="0ff2e-107">Proteger recursos na nuvem e no local com o Servidor Multi-Factor Authentication do Azure</span><span class="sxs-lookup"><span data-stu-id="0ff2e-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="0ff2e-108">Olá, a tabela seguinte resume a experiência de verificação de Olá entre proteger recursos com o Azure multi-factor Authentication e o AD FS</span><span class="sxs-lookup"><span data-stu-id="0ff2e-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="0ff2e-109">Experiência de Verificação - Aplicações baseadas no browser</span><span class="sxs-lookup"><span data-stu-id="0ff2e-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="0ff2e-110">Experiência de Verificação - Aplicações não baseadas no browser</span><span class="sxs-lookup"><span data-stu-id="0ff2e-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ff2e-111">Proteger recursos do Azure AD com o Multi-Factor Authentication do Azure</span><span class="sxs-lookup"><span data-stu-id="0ff2e-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="0ff2e-112">primeiro passo de verificação Olá é efetuado no local utilizando o AD FS.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="0ff2e-113">Step-by-Olá segundo passo é um método baseado em telefone efetuado através da autenticação em nuvem.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="0ff2e-114">Proteger recursos do Azure AD com os Serviços de Federação do Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ff2e-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="0ff2e-115">primeiro passo de verificação Olá é efetuado no local utilizando o AD FS.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="0ff2e-116">Step-by-Olá segundo passo é executado no local honrando a afirmação Olá.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="0ff2e-117">Advertências com palavras-passe de aplicação para utilizadores federados:</span><span class="sxs-lookup"><span data-stu-id="0ff2e-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="0ff2e-118">As palavras-passe da aplicação são verificadas com a autenticação na nuvem, para que possam ignorar a federação.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="0ff2e-119">A federação apenas é utilizada ativamente ao definir uma palavra-passe de aplicação.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="0ff2e-120">As definições de Controlo de Acesso de Cliente no local não são honradas pelas palavras-passe de aplicações.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="0ff2e-121">Perde a capacidade de registos de autenticação no local para as palavras-passe de aplicações.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="0ff2e-122">A desativação/eliminação da conta pode demorar horas toothree para sincronização de diretórios, atrasando a desativação/eliminação de palavras-passe de aplicação na identidade de nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="0ff2e-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ff2e-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0ff2e-123">Next steps</span></span>
<span data-ttu-id="0ff2e-124">Para informações sobre como configurar o Azure multi-factor Authentication ou Olá Azure multi-factor Authentication Server com o AD FS, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="0ff2e-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="0ff2e-125">Proteger recursos da nuvem com o Multi-Factor Authentication do Azure e o AD FS</span><span class="sxs-lookup"><span data-stu-id="0ff2e-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="0ff2e-126">Proteger recursos na nuvem e no local utilizando o Servidor Multi-Factor Authentication do Azure com o Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="0ff2e-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="0ff2e-127">Proteger recursos na nuvem e no local utilizando o Servidor Multi-Factor Authentication do Azure com o AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="0ff2e-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
