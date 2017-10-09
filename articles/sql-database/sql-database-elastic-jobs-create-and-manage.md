---
title: grupos de aaaManage das bases de dados SQL do Azure | Microsoft Docs
description: "Percorrer a criação e gestão de uma tarefa elástica."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>Criar e gerir expandido terminar as bases de dados de SQL do Azure utilizando as tarefas elásticas (pré-visualização)


**As tarefas de base de dados elásticas** simplificar a gestão de grupos de bases de dados ao executar operações administrativas como alterações de esquema, gestão de credenciais, as atualizações de dados de referência, recolha de dados de desempenho ou telemetria de inquilino (cliente) coleção. As tarefas de base de dados elásticas está atualmente disponível através de Olá portal do Azure e os cmdlets do PowerShell. No entanto, Olá funcionalidade reduzida do Azure analisa portal limitada tooexecution em todas as bases de dados num [conjunto elástico (pré-visualização)](sql-database-elastic-pool.md). conjunto de funcionalidades adicionais tooaccess e a execução de scripts entre um grupo de bases de dados, incluindo uma coleção personalizado ou um ID de partição horizontal (criado utilizando [biblioteca de clientes de base de dados elástica](sql-database-elastic-scale-introduction.md)), consulte [criar e gerir as tarefas através do PowerShell](sql-database-elastic-jobs-powershell.md). Para obter mais informações sobre tarefas, consulte [descrição geral de tarefas de bases de dados elásticas](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Pré-requisitos
* Uma subscrição do Azure. Para uma versão de avaliação gratuita, consulte [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Um conjunto elástico. Consulte [sobre conjuntos elásticos](sql-database-elastic-pool.md).
* Instalação de componentes do serviço de tarefa de bases de dados elásticas. Consulte [instalar o serviço de tarefas de bases de dados elásticas Olá](sql-database-elastic-jobs-service-installation.md).

## <a name="creating-jobs"></a>Criar tarefas
1. Utilizar Olá [portal do Azure](https://portal.azure.com), de um conjunto de trabalho de bases de dados elásticas existente, clique em **criar tarefa**.
2. Escreva Olá nome de utilizador e palavra-passe de administrador de bases de dados de Olá (criado durante a instalação de tarefas) para a base de dados de controlo de tarefas Olá (armazenamento de metadados para as tarefas).
   
    ![Tarefa de Olá nome, escreva ou cole no código e clique em executar][1]
3. No Olá **criar tarefa** painel, escreva um nome para a tarefa de Olá.
4. Escreva Olá nome e palavra-passe tooconnect toohello destino bases de dados com permissões suficientes para toosucceed de execução do script.
5. Cole ou escreva no script de Olá T-SQL.
6. Clique em **guardar** e, em seguida, clique em **executar**.
   
    ![Criar tarefas e executar][5]

## <a name="run-idempotent-jobs"></a>Executar tarefas de idempotent
Quando executar um script face a um conjunto de bases de dados, tem de ser se de que o script de Olá idempotent. Ou seja, Olá script deve ser capaz de toorun várias vezes, mesmo que não conseguiu antes de um estado incompleto. Por exemplo, um script falha, a tarefa de Olá será automaticamente repetida até ter êxito (dentro dos limites como tentativas de Olá lógica irá eventualmente cessar Olá repetir). Olá forma toodo isto toouse Olá uma cláusula "Se existe" e eliminar qualquer instância encontrada antes de criar um novo objeto. Um exemplo é mostrado aqui:

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

Em alternativa, utilize uma cláusula "Se não existe" antes de criar uma nova instância:

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

Este script, em seguida, atualiza tabela Olá criada anteriormente.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>A verificar o estado da tarefa
Depois de uma tarefa foi iniciada, poder verificar o progresso da mesma.

1. Na página do conjunto elástico Olá, clique em **gerir tarefas**.
   
    ![Clique em "Gerir tarefas"][2]
2. Clique em Olá nome (a) de uma tarefa. Olá **estado** pode ser "Concluída" ou "Falha". Detalhes da tarefa de Olá aparecem (b) com a data e hora de criação e em execução. lista de Olá (c) abaixo Olá que mostra o progresso de Olá de script de Olá em relação a cada base de dados no agrupamento de Olá, fornecer os detalhes de data e hora.
   
    ![A verificação de uma tarefa concluída][3]

## <a name="checking-failed-jobs"></a>A verificação de tarefas com falha
Se uma tarefa falhar, pode encontrar um registo sua execução. Clique no nome de Olá de Olá falha na tarefa toosee os respetivos detalhes.

![Uma tarefa de verificação][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


