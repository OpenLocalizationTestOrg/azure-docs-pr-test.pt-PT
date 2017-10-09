---
title: "aaaRestore uma única tabela de cópia de segurança de SQL Database do Azure | Microsoft Docs"
description: "Saiba como toorestore uma única tabela de cópia de segurança de SQL Database do Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Como toorestore uma única tabela de uma cópia de segurança de SQL Database do Azure
Poderá encontrar uma situação em que modificou acidentalmente alguns dados na base de dados SQL e agora pretende toorecover Olá única afetados tabela. Este artigo descreve como toorestore uma única tabela numa base de dados a partir de um Olá base de dados SQL [cópias de segurança automáticas](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Passos de preparação: mudar o nome da tabela de Olá e restaurar uma cópia da base de dados de Olá
1. Identifica a tabela de Olá na base de dados SQL do Azure que pretende que o tooreplace com cópia Olá restaurada. Utilize a tabela do Microsoft SQL Server Management Studio toorename Olá. Por exemplo, mudar o nome da tabela de Olá como &lt;nome da tabela&gt;_old.
   
   > [!NOTE]
   > tooavoid a ser bloqueado, certifique-se de que não há nenhuma atividade em execução na tabela de Olá que são mudar o nome. Se ocorrerem problemas, certifique-se de que efetuar este procedimento durante uma janela de manutenção.
   >

2. Restaurar uma cópia de segurança da sua base de dados tooa ponto no tempo que pretende que o toorecover toousing Olá [ponto-In_Time restaurar](sql-database-recovery-using-backups.md#point-in-time-restore) passos.
   
   > [!NOTE]
   > nome de Olá da base de dados de Olá restaurada vai estar no formato de DBName + TimeStamp de Olá; Por exemplo, **Adventureworks2012_2016-01-01T22-12Z**. Este passo não substituir o nome da base de dados existente Olá no servidor de Olá. Esta é uma medida de segurança e destina-se tooallow Olá tooverify restaurar base de dados antes de serem remover respetiva base de dados atual e mudar o nome da base de dados de Olá restaurado para utilização em produção.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Copiar Olá tabela da Olá restaurar base de dados utilizando a ferramenta de migração de base de dados do SQL Server Olá

1. Transfira e instale Olá [Assistente de migração de base de dados do SQL Server](https://sqlazuremw.codeplex.com).
2. Abra Olá Assistente de migração da base de dados SQL no Olá **selecione processo** página, selecione **base de dados em analisar/migrar**e, em seguida, clique em **seguinte**.

   ![Assistente de migração de base de dados do SQL Server - selecione processo](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. No Olá **ligar tooServer** diálogo caixa, aplicar Olá seguintes definições:

   * Nome do servidor: **do seu SQL Server**
   * Autenticação: **autenticação do SQL Server**
   * Início de sessão: **o início de sessão**
   * Palavra-passe: **a palavra-passe**
   * Base de dados: **Master DB (lista de todas as bases de dados)**
   
   > [!NOTE]
   > Por predefinição, o Assistente de Olá guarda as informações de início de sessão. Se não pretender que ele, selecione **se esqueça de informações de início de sessão**.
   >
   
     ![Passo de migração de base de dados SQL do assistente - selecionar origem de - 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. No Olá **selecionar origem** caixa de diálogo, nome de base de dados de Olá selecione restaurada de Olá **passos de preparação** secção como a origem e, em seguida, clique em **seguinte**.
   
    ![Passo de migração de base de dados SQL do assistente - selecionar origem - 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. No Olá **escolha objetos** caixa de diálogo, selecione de Olá **selecionar objetos de base de dados específica** opção e, em seguida, selecione table(or tables) Olá que pretende que o servidor de destino toomigrate toohello.
   ![Assistente de migração de base de dados do SQL Server - escolha objetos](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. No Olá **resumo do Assistente de Script** página, clique em **Sim** quando lhe for pedida sobre se estiver pronto toogenerate um script do SQL Server. Também tem Olá opção toosave Olá TSQL Script para utilização posterior.
   ![Assistente de migração de base de dados do SQL Server - resumo do Assistente de Script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. No Olá **resumo de resultados** página, clique em **seguinte**.
   ![Assistente de migração de base de dados do SQL Server - resumo de resultados](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. No Olá **configurar a ligação ao servidor de destino** página, clique em **ligar tooServer**e, em seguida, introduza os detalhes de Olá da seguinte forma:
   
   * **Nome do servidor**: instância de servidor de destino
   * **Autenticação**: **autenticação do SQL Server**. Introduza as credenciais de início de sessão.
   * **Base de dados**: **Master DB (lista de todas as bases de dados)**. Esta opção apresenta uma lista de todas as bases de dados de Olá no servidor de destino Olá.
     
     ![Assistente de migração de base de dados do SQL Server - configurar a ligação ao servidor de destino](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Clique em **Connect**, selecione base de dados do destino Olá que pretende tabela de Olá toomove para e, em seguida, clique em **seguinte**. Isto deve ser concluída a executar o script Olá gerado anteriormente e deverá ver Olá movido recentemente a base de dados de destino de toohello copiados de tabela.

## <a name="verification-step"></a>Passo de verificação

- Consulta e teste Olá recentemente copiados toomake tabela se de que os dados de Olá estão intactos. Após a confirmação, pode remover o formulário de tabela Olá mudado **passos de preparação** secção. (por exemplo, &lt;nome da tabela&gt;_old).

## <a name="next-steps"></a>Passos seguintes
[Cópias de segurança automáticas de base de dados SQL](sql-database-automated-backups.md)

