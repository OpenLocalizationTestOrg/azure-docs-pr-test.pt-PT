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
# <a name="manage-server-administrators"></a>Gerir administradores de servidor
Os administradores de servidores tem de ser um utilizador ou grupo válido no Olá Azure Active Directory (Azure AD) para o inquilino Olá no qual Olá reside o servidor. Pode utilizar **administradores de serviços de análise** no painel de controlo de Olá para o servidor no portal do Azure ou propriedades do servidor em que os administradores de servidores do SSMS toomanage. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>administradores de servidores de tooadd utilizando o portal do Azure
1. No painel de controlo de hello do servidor, clique em **administradores de serviços de análise**.
2. No Olá  **\<servername >-administradores de serviços de análise** painel, clique em **adicionar**.
3. No Olá **adicionar administradores de servidor** painel, selecione as contas de utilizador do seu Azure AD ou convidar utilizadores externos ao endereço de correio eletrónico.

    ![Administradores de servidor no portal do Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>administradores de servidores de tooadd utilizando SSMS
1. Servidor do contexto Olá > **propriedades**.
2. No **propriedades do Analysis Server**, clique em **segurança**.
3. Clique em **adicionar**e, em seguida, introduza o endereço de correio eletrónico Olá para um utilizador ou grupo no Azure AD.
   
    ![Adicionar administradores de servidor no SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Passos seguintes 
[Autenticação e permissões de utilizador](analysis-services-manage-users.md)  
[Gerir utilizadores e funções de base de dados](analysis-services-database-users.md)  
[Controlo de Acesso Baseado em Funções](../active-directory/role-based-access-control-what-is.md)  

