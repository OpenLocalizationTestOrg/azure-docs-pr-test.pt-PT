---
title: aaaCopy uma base de dados SQL do Azure | Microsoft Docs
description: "Criar uma cópia de uma base de dados SQL do Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Copiar uma base de dados SQL do Azure

Base de dados SQL do Azure fornece vários métodos para criar uma cópia de uma forma consistente de um SQL do Azure existente da base de dados em qualquer um dos Olá mesmo servidor ou um servidor diferente. Pode copiar uma base de dados do SQL Server utilizando Olá portal do Azure, o PowerShell ou o T-SQL. 

## <a name="overview"></a>Descrição geral

Uma cópia da base de dados é um instantâneo da base de dados a partir da hora de Olá do pedido de cópia de Olá Olá origem. Pode selecionar Olá mesmo servidor ou um servidor diferente, o nível de desempenho e o escalão de serviço ou um nível de desempenho diferente dentro Olá mesma camada de serviço (edição). Depois de concluída a cópia de Olá, torna-se uma base de dados totalmente funcional, independente. Neste momento, pode atualizar ou mudar-tooany edição. inícios de sessão Olá, os utilizadores e permissões podem ser geridas de forma independente.  

## <a name="logins-in-hello-database-copy"></a>Inícios de sessão na cópia da base de dados de Olá

Quando copiar uma base de dados toohello mesmo servidor lógico, Olá inícios de sessão mesmos podem ser utilizados em ambas as bases de dados. utilizar base de dados do toocopy Olá principal de segurança Olá torna-se proprietário da base de dados de Olá na base de dados nova Olá. Todos os utilizadores de base de dados, as suas permissões e a segurança dos mesmos identificadores (SIDs) são copiados toohello cópia de base de dados.  

Quando copia a base de dados tooa lógica servidor diferente, segurança Olá principal num servidor novo Olá fica proprietário da base de dados de Olá na base de dados nova Olá. Se utilizar [continha os utilizadores de base de dados](sql-database-manage-logins.md) para acesso a dados, certifique-se de que ambos Olá primário e de bases de dados secundárias tem sempre Olá mesmas credenciais de utilizador, pelo que concluir após a conclusão da cópia de Olá imediatamente podem aceder com Olá mesmo credenciais. 

Se utilizar [do Azure Active Directory](../active-directory/active-directory-whatis.md), pode eliminar completamente Olá necessário para a gestão de credenciais na cópia de Olá. No entanto, quando copiar o novo servidor tooa da base de dados de Olá, acesso baseado no início de sessão de Olá poderá não funcionar, porque não existem inícios de sessão Olá no novo servidor de Olá. toolearn sobre a gestão de inícios de sessão quando copiar um base de dados tooa outro servidor lógico, consulte [como toomanage SQL do Azure da base de dados segurança após a recuperação de desastre](sql-database-geo-replication-security-config.md). 

Depois de copiar Olá for bem sucedida e antes de outros utilizadores são novamente mapeados, apenas hello início de sessão que iniciadas Olá copiar, proprietário da base de dados de Olá, pode iniciar sessão toohello nova base de dados. Consulte tooresolve inícios de sessão após a conclusão, Olá copiar operação [resolver inícios de sessão](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Copiar uma base de dados utilizando Olá portal do Azure

toocopy uma base de dados utilizando Olá portal do Azure, a página Olá aberto para a base de dados e, em seguida, clique em **cópia**. 

   ![Cópia de base de dados](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Copiar uma base de dados utilizando o PowerShell

toocopy uma base de dados utilizando o PowerShell, utilize Olá [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Para um script de exemplo completa, consulte [copiar um base de dados tooa novo servidor](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Copiar uma base de dados, utilizando Transact-SQL

Inicie sessão no toohello mestra da base de dados com o início de sessão principal Olá ao nível do servidor ou o início de sessão de Olá criado Olá base de dados toocopy. Para a base de dados está a copiar toosucceed, inícios de sessão que não são principal ao nível do servidor de Olá tem de ser membros da função de dbmanager Olá. Para mais informações sobre os inícios de sessão e ligação toohello server, consulte [gerir inícios de sessão](sql-database-manage-logins.md).

Começar a copiar a base de dados de origem de Olá com Olá [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) instrução. Executar esta instrução inicia a base de dados de Olá copiar processo. Como copiar uma base de dados é um processo assíncrono, Olá instrução CREATE DATABASE devolve antes da cópia da base de dados de Olá está concluída.

### <a name="copy-a-sql-database-toohello-same-server"></a>Copiar uma toohello de base de dados do SQL server do mesmo
Inicie sessão no toohello mestra da base de dados com o início de sessão principal Olá ao nível do servidor ou o início de sessão de Olá criado Olá base de dados toocopy. Para a base de dados está a copiar toosucceed, inícios de sessão que não são principal ao nível do servidor de Olá tem de ser membros da função de dbmanager Olá.

Este comando copia Database1 tooa nova base de dados com o nome Database2 Olá mesmo servidor. Consoante o tamanho da base de dados Olá, Olá copiar operação poderá demorar toocomplete algum tempo.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Copie um servidor diferente do SQL Server da base de dados tooa

Inicie sessão no toohello mestra da base de dados hello do servidor de destino, servidor de base de dados do SQL Server do olá onde a nova base de dados Olá é toobe criado. Utilize um início de sessão tem Olá o mesmo nome e palavra-passe como proprietário da base de dados de Olá da base de dados de origem de Olá no servidor de base de dados SQL do Olá origem. início de sessão Olá no servidor de destino Olá têm também de ser um membro da função de dbmanager Olá ou início de sessão principal Olá ao nível do servidor.

Este comando copia Database1 no servidor1 tooa nova base de dados com o nome Database2 no Servidor2. Consoante o tamanho da base de dados Olá, Olá copiar operação poderá demorar toocomplete algum tempo.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Monitorizar o progresso de Olá de Olá copiar operação

Monitorizar o processo de cópia de Olá consultando vistas de Databases e sys.dm_database_copies Olá. Enquanto Olá copiar está em curso, Olá **state_desc** coluna da vista de Databases Olá para a nova base de dados Olá estiver definida demasiado**copiar**.

* Se copiar Olá falhar, Olá **state_desc** coluna da vista de Databases Olá para a nova base de dados Olá estiver definida demasiado**SUSPEITAR**. Executar Olá instrução DROP na base de dados nova Olá e tente novamente mais tarde.
* Se copiar Olá for bem sucedida, hello **state_desc** coluna da vista de Databases Olá para a nova base de dados Olá estiver definida demasiado**ONLINE**. Copiar Olá estiver concluída, não sendo nova base de dados Olá uma base de dados normal que pode ser alterado independente da base de dados de origem de Olá.

> [!NOTE]
> Se decidir toocancel Olá copiar enquanto esta se encontra em curso, executar Olá [remover a base de dados](https://msdn.microsoft.com/library/ms178613.aspx) instrução na base de dados nova Olá. Em alternativa, ao executar a instrução de remover a base de dados de Olá na base de dados de origem de Olá também cancela Olá copiar processo.
> 

## <a name="resolve-logins"></a>Resolver inícios de sessão

Após a conclusão da nova base de dados Olá online no servidor de destino Olá, utilize Olá [ALTER utilizador](https://msdn.microsoft.com/library/ms176060.aspx) instrução tooremap Olá utilizadores Olá novos da base de dados toologins no servidor de destino Olá. utilizadores de tooresolve órfão, consulte [resolver utilizadores órfãos](https://msdn.microsoft.com/library/ms175475.aspx). Consulte também [como toomanage SQL do Azure da base de dados segurança após a recuperação de desastre](sql-database-geo-replication-security-config.md).

Todos os utilizadores na base de dados nova Olá mantém as permissões de Olá que tinham na base de dados de origem de Olá. utilizador de Olá que iniciou a cópia da base de dados de Olá torna-se Olá proprietário de base de dados da base de dados nova Olá e é atribuído um novo identificador de segurança (SID). Depois de copiar Olá for bem sucedida e antes de outros utilizadores são novamente mapeados, apenas hello início de sessão que iniciadas Olá copiar, proprietário da base de dados de Olá, pode iniciar sessão toohello nova base de dados.

toolearn sobre a gestão de utilizadores e os inícios de sessão quando copiar um base de dados tooa outro servidor lógico, consulte [como toomanage SQL do Azure da base de dados segurança após a recuperação de desastre](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Passos seguintes

* Para obter informações sobre os inícios de sessão, consulte [gerir inícios de sessão](sql-database-manage-logins.md) e [como toomanage SQL do Azure da base de dados segurança após a recuperação de desastre](sql-database-geo-replication-security-config.md).
* tooexport uma base de dados, consulte [exportar a base de dados de Olá tooa BACPAC](sql-database-export.md).
