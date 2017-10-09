---
title: "aaaConditional acesso - SQL Database do Azure e do armazém de dados | Documentação da Microsoft"
description: "Saiba como tooconfigure de acesso condicional para o SQL Database do Azure e do armazém de dados."
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Acesso condicional (MFA) com base de dados SQL do Azure e do armazém de dados  

Base de dados SQL e do armazém de dados do SQL Server suportam o acesso condicional do Microsoft. Olá, como os seguintes passos Mostrar tooenforce de base de dados SQL tooconfigure uma política de acesso condicional.  

## <a name="prerequisites"></a>Pré-requisitos  
- Tem de configurar a autenticação do Azure Active Directory de toosupport base de dados SQL ou SQL Data Warehouse. Para obter passos específicos, consulte [configurar e gerir a autenticação do Azure Active Directory com a base de dados SQL ou SQL Data Warehouse](sql-database-aad-authentication-configure.md).  
- Quando a autenticação multifator estiver ativada, tem de ligar com a ferramenta suportada, tais como Olá SSMS mais recente. Para obter mais informações, consulte [configurar a base de dados de SQL do Azure multi-factor authentication para SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Configurar a AC para a base de dados/armazém de dados do SQL do Azure  
1.  Início de sessão toohello Portal, selecione **do Azure Active Directory**e, em seguida, selecione **acesso condicional**. Para obter mais informações, consulte [referência técnica do Azure Active Directory condicional acesso](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![Painel de acesso condicional](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  No Olá **políticas de acesso condicional** painel, clique em **nova política**, forneça um nome e, em seguida, clique em **configurar regras**.  
3.  Em **atribuições**, selecione **utilizadores e grupos**, verifique **selecionar utilizadores e grupos**e, em seguida, selecione o utilizador Olá ou o grupo de acesso condicional. Clique em **selecione**e, em seguida, clique em **feito** tooaccept a seleção.  
  ![Selecionar utilizadores e grupos](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Selecione **aplicações em nuvem**, clique em **selecionar aplicações**. Pode ver todas as aplicações disponíveis para o acesso condicional. Selecione **SQL Database do Azure**, na parte inferior de Olá clique **selecione**e, em seguida, clique em **feito**.  
  ![Selecione a base de dados SQL](./media/sql-database-conditional-access/select-sql-database.png)  
  Se não encontrar **SQL Database do Azure** listado no Olá terceira captura de ecrã a seguir, conclua Olá os seguintes passos:   
  - Inicie sessão na instância do Azure SQL DB/armazém de dados tooyour com o SSMS com uma conta de administrador do AAD.  
  - Executar `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Inicie sessão tooAAD e certifique-se de que o SQL Database do Azure e do armazém de dados estão listados em aplicações de Olá no seu AAD.  

5.  Selecione **controlos de acesso**, selecione **conceder**e, em seguida, verifique Olá política, tooapply. Neste exemplo, selecione **requer autenticação multifator**.  
  ![Selecione a conceder acesso](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Resumo  
aplicação de Olá selecionado (SQL Database do Azure), permitindo tooconnect tooAzure SQL DB/armazém de dados utilizando o Azure AD Premium, agora impõe a política de acesso condicional Olá selecionado, **necessária autenticação multifator.**  
Para perguntas sobre a SQL Database do Azure e do armazém de dados sobre a autenticação multifator, contacte MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Passos seguintes  

Para um tutorial, consulte [proteger a base de dados do SQL do Azure](sql-database-security-tutorial.md).
