---
title: aaaRestore Azure SQL Data Warehouse (portal do Azure) | Microsoft Docs
description: Tarefas do portais do Azure para restaurar o Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Restaurar o Azure SQL Data Warehouse (portal)
> [!div class="op_single_selector"]
> * [Descrição geral][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
Neste artigo, ficará a saber como toorestore Azure SQL Data Warehouse, utilizando Olá portal do Azure.

## <a name="before-you-begin"></a>Antes de começar
**Certifique-se a capacidade DTU.** Cada instância do SQL Data Warehouse está hospedada num servidor de SQL Server (por exemplo, myserver.database.windows.net) que tem uma quota de (DTU) de unidade de débito de dados predefinida. Antes, pode restaurar o SQL Data Warehouse, certifique-se de que o servidor SQL tem suficiente restante quota de DTU de base de dados Olá que está a restaurar. toolearn como quota de DTU toocalculate ou toorequest mais DTUs, consulte [pedir uma alteração de quota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restaurar uma base de dados do Active Directory ou em pausa
toorestore uma base de dados:

1. Inicie sessão no toohello [portal do Azure][Azure portal].
2. No painel esquerdo Olá, selecione **procurar**e, em seguida, selecione **servidores SQL**.

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Localizar o servidor e, em seguida, selecioná-lo.

    ![Selecione o seu servidor](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Localize a instância de Olá do armazém de dados do SQL Server que pretende toorestore do e, em seguida, selecioná-lo.

    ![Selecione Olá instância do SQL Data Warehouse toorestore](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. Olá parte superior do painel de armazém de dados de Olá, selecione **restaurar**.

    ![Selecione o restauro](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Especifique um novo **nome de base de dados**.
7. Selecione Olá mais recente **ponto de restauro**.

   Certifique-se de que escolhe o último ponto de restauro Olá. Porque os pontos de restauro são apresentados na hora Universal Coordenada (UTC), opção predefinida de Olá poderá não ser o ponto de restauro mais recente Olá.

      ![Selecione um ponto de restauro](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Selecione **OK**.
9. processo de restauro de base de dados de Olá começará e pode utilizar **notificações** processo de Olá toomonitor.

> [!NOTE]
> Depois de terminar o restauro de Olá, pode configurar a base de dados recuperada, seguindo [configurar a base de dados após a recuperação][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Restaurar uma base de dados eliminada
toorestore uma base de dados eliminada:

1. Inicie sessão no toohello [portal do Azure][Azure portal].
2. No painel esquerdo Olá, selecione **procurar**e, em seguida, selecione **servidores SQL**.

    ![Selecione Procurar > servidores SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Localizar o servidor e, em seguida, selecioná-lo.

    ![Selecione o seu servidor](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Desloque para baixo toohello **operações** secção no painel do seu servidor.
5. Selecione Olá **eliminou bases de dados** mosaico.

    ![Selecione o mosaico de bases de dados do Olá eliminado](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Selecione Olá eliminado da base de dados que pretende que o toorestore.

    ![Selecione um toorestore de base de dados](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Especifique um novo **nome de base de dados**.

    ![Adicionar um nome de base de dados de Olá](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Selecione **OK**.
9. processo de restauro de base de dados de Olá começará e pode utilizar **notificações** processo de Olá toomonitor.

> [!NOTE]
> tooconfigure a base de dados depois de terminar o restauro de Olá, consulte [configurar a base de dados após a recuperação][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Passos seguintes
toolearn sobre as funcionalidades de continuidade de negócio Olá das edições do SQL Database do Azure, leia Olá [descrição geral da continuidade de negócio da linha de base de dados do Azure SQL][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
