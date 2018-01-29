---
title: "Acesso condicional - base de dados SQL do Azure e do armazém de dados | Documentação da Microsoft"
description: "Saiba como configurar o acesso condicional para o SQL Database do Azure e do armazém de dados."
services: sql-database
author: GithubMirek
manager: johammer
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: mireks
ms.workload: Inactive
ms.openlocfilehash: b1c569e414de292b59e0915483d45bf011edb1a6
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/11/2018
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Acesso condicional (MFA) com base de dados SQL do Azure e do armazém de dados  

Base de dados SQL e do armazém de dados do SQL Server suportam o acesso condicional do Microsoft. Os passos seguintes mostram como configurar a base de dados SQL para impor uma política de acesso condicional.  

## <a name="prerequisites"></a>Pré-requisitos  
- Tem de configurar a base de dados do SQL Server ou do armazém de dados do SQL Server para suportar a autenticação do Azure Active Directory. Para obter passos específicos, consulte [configurar e gerir a autenticação do Azure Active Directory com a base de dados SQL ou SQL Data Warehouse](sql-database-aad-authentication-configure.md).  
- Quando a autenticação multifator estiver ativada, tem de ligar com a ferramenta suportada, por exemplo, o SSMS mais recente. Para obter mais informações, consulte [configurar a base de dados de SQL do Azure multi-factor authentication para SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Configurar a AC para a base de dados/armazém de dados do SQL do Azure  
1.  Inicie sessão no Portal, selecione **do Azure Active Directory**e, em seguida, selecione **acesso condicional**. Para obter mais informações, consulte [referência técnica do Azure Active Directory condicional acesso](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![Painel de acesso condicional](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  No **políticas de acesso condicional** painel, clique em **nova política**, forneça um nome e, em seguida, clique em **configurar regras**.  
3.  Em **atribuições**, selecione **utilizadores e grupos**, verifique **selecionar utilizadores e grupos**e, em seguida, selecione o utilizador ou grupo de acesso condicional. Clique em **selecione**e, em seguida, clique em **feito** para aceitar a sua seleção.  
  ![Selecionar utilizadores e grupos](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Selecione **aplicações em nuvem**, clique em **selecionar aplicações**. Pode ver todas as aplicações disponíveis para o acesso condicional. Selecione **SQL Database do Azure**, na parte inferior, clique em **selecione**e, em seguida, clique em **feito**.  
  ![Selecione a base de dados SQL](./media/sql-database-conditional-access/select-sql-database.png)  
  Se não encontrar **SQL Database do Azure** listados na captura de ecrã de terceiro seguinte, conclua os seguintes passos:   
  - Inicie sessão sua instância do Azure SQL DB/armazém de dados com o SSMS com uma conta de administrador do AAD.  
  - Executar `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Inicie sessão no AAD e certifique-se de que o SQL Database do Azure e do armazém de dados estão listados nas aplicações no seu AAD.  

5.  Selecione **controlos de acesso**, selecione **conceder**e, em seguida, verifique a política que pretende aplicar. Neste exemplo, selecione **requer autenticação multifator**.  
  ![Selecione a conceder acesso](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Resumo  
A aplicação selecionada (SQL Database do Azure), permitindo ligar ao Azure SQL DB/armazém de dados utilizando o Azure AD Premium, agora impõe a política de acesso condicional selecionada, **necessária autenticação multifator.**  
Para perguntas sobre a SQL Database do Azure e do armazém de dados sobre a autenticação multifator, contacte MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Passos Seguintes  

Para um tutorial, consulte [proteger a base de dados do SQL do Azure](sql-database-security-tutorial.md).
