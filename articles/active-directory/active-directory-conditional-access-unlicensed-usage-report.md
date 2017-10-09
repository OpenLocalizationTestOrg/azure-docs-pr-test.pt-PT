---
title: "aaaUnlicensed relatório de utilização | Microsoft Docs"
description: "Olá, relatório de utilização não autorizada paga de ajuda a que identificar os utilizadores sem licença que estão a utilizar funcionalidades do Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="3589e-103">Relatório de utilização não autorizada</span><span class="sxs-lookup"><span data-stu-id="3589e-103">Unlicensed usage report</span></span>
<span data-ttu-id="3589e-104">Olá, relatório de utilização não autorizada paga de ajuda a que identificar os utilizadores sem licença que estão a utilizar funcionalidades do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3589e-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="3589e-105">Isto permite-lhe toomake utilize melhor de licenças que adquiriu e tooidentify sabe quando poderá ter licenças adicionais.</span><span class="sxs-lookup"><span data-stu-id="3589e-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="3589e-106">relatório de Olá mostra a utilização de Active Directory de Olá paga funcionalidades no Olá últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="3589e-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="3589e-107">Estrutura de relatório</span><span class="sxs-lookup"><span data-stu-id="3589e-107">Report structure</span></span>
| <span data-ttu-id="3589e-108">Nome da coluna</span><span class="sxs-lookup"><span data-stu-id="3589e-108">Column name</span></span> | <span data-ttu-id="3589e-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="3589e-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3589e-110">Sem licença de utilizador</span><span class="sxs-lookup"><span data-stu-id="3589e-110">Unlicensed User</span></span> |<span data-ttu-id="3589e-111">Nome de utilizador de Olá</span><span class="sxs-lookup"><span data-stu-id="3589e-111">Name of hello user</span></span> |
| <span data-ttu-id="3589e-112">Funcionalidade</span><span class="sxs-lookup"><span data-stu-id="3589e-112">Feature</span></span> |<span data-ttu-id="3589e-113">nome da funcionalidade Olá.</span><span class="sxs-lookup"><span data-stu-id="3589e-113">hello feature name.</span></span> <span data-ttu-id="3589e-114">Por exemplo: acesso condicional</span><span class="sxs-lookup"><span data-stu-id="3589e-114">For example: conditional access</span></span> |
| <span data-ttu-id="3589e-115">Aplicação acedida</span><span class="sxs-lookup"><span data-stu-id="3589e-115">Application Accessed</span></span> |<span data-ttu-id="3589e-116">nome da aplicação Olá que estiver a ser acedido com funcionalidade Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="3589e-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="3589e-117">Por exemplo: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="3589e-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="3589e-118">Se uma conta de utilizador foi eliminada Olá 'Sem licença User' coluna será preenchida com o ID, como 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="3589e-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="3589e-119">Funcionalidade de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="3589e-119">Conditional access feature</span></span>
<span data-ttu-id="3589e-120">Utilizadores sem licença vai ser sinalizados quando acedem a um serviço com a política de acesso condicional aplicada se não tiver uma licença do Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="3589e-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="3589e-121">Isto aplica-se tooMFA / políticas de localização, bem como dispositivos políticas que utilizar o Intune.</span><span class="sxs-lookup"><span data-stu-id="3589e-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="3589e-122">Consultar também</span><span class="sxs-lookup"><span data-stu-id="3589e-122">See also</span></span>
* [<span data-ttu-id="3589e-123">Utilizar o acesso condicional com o Office 365 e outros Azure Active Directory ligado aplicações</span><span class="sxs-lookup"><span data-stu-id="3589e-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="3589e-124">Introdução ao acesso condicional tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="3589e-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

