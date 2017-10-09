---
title: administradores de servidor aaaManage no Azure Analysis Services | Microsoft Docs
description: Saiba como toomanage administradores de servidor para um servidor de Analysis Services no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="73076-103">Gerir administradores de servidor</span><span class="sxs-lookup"><span data-stu-id="73076-103">Manage server administrators</span></span>
<span data-ttu-id="73076-104">Os administradores de servidores tem de ser um utilizador ou grupo válido no Olá Azure Active Directory (Azure AD) para o inquilino Olá no qual Olá reside o servidor.</span><span class="sxs-lookup"><span data-stu-id="73076-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="73076-105">Pode utilizar **administradores de serviços de análise** no painel de controlo de Olá para o servidor no portal do Azure ou propriedades do servidor em que os administradores de servidores do SSMS toomanage.</span><span class="sxs-lookup"><span data-stu-id="73076-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="73076-106">administradores de servidores de tooadd utilizando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="73076-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="73076-107">No painel de controlo de hello do servidor, clique em **administradores de serviços de análise**.</span><span class="sxs-lookup"><span data-stu-id="73076-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="73076-108">No Olá  **\<servername >-administradores de serviços de análise** painel, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="73076-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="73076-109">No Olá **adicionar administradores de servidor** painel, selecione as contas de utilizador do seu Azure AD ou convidar utilizadores externos ao endereço de correio eletrónico.</span><span class="sxs-lookup"><span data-stu-id="73076-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administradores de servidor no portal do Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="73076-111">administradores de servidores de tooadd utilizando SSMS</span><span class="sxs-lookup"><span data-stu-id="73076-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="73076-112">Servidor do contexto Olá > **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="73076-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="73076-113">No **propriedades do Analysis Server**, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="73076-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="73076-114">Clique em **adicionar**e, em seguida, introduza o endereço de correio eletrónico Olá para um utilizador ou grupo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73076-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Adicionar administradores de servidor no SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="73076-116">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="73076-116">Next steps</span></span> 
[<span data-ttu-id="73076-117">Autenticação e permissões de utilizador</span><span class="sxs-lookup"><span data-stu-id="73076-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="73076-118">Gerir utilizadores e funções de base de dados</span><span class="sxs-lookup"><span data-stu-id="73076-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="73076-119">Controlo de Acesso Baseado em Funções</span><span class="sxs-lookup"><span data-stu-id="73076-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

