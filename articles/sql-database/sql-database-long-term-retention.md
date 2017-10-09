---
title: "aaaStore SQL Database do Azure cópias de segurança para cópia de segurança too10 anos | Microsoft Docs"
description: "Saiba como o SQL Database do Azure suporta armazenar cópias de segurança para cópia de segurança too10 anos."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Armazenar a base de dados do Azure SQL cópias de segurança para cópia de segurança too10 anos
Muitas aplicações terem regulamentação, conformidade ou de outras empresas fins que necessitam que tooretain cópias de segurança de base de dados para além de Olá dias 7-35 fornecidos pelo SQL Database do Azure [cópias de segurança automáticas](sql-database-automated-backups.md). Ao utilizar a funcionalidade de cópia de segurança de retenção de longo prazo Olá, pode armazenar as cópias de segurança de base de dados do SQL Server num cofre dos serviços de recuperação do Azure para cópia de segurança too10 anos. Pode armazenar cópias de segurança too1, 000 bases de dados por cofre. Em seguida, pode selecionar qualquer cópia de segurança na Olá cofre toorestore-o como uma nova base de dados.

> [!IMPORTANT]
> Retenção de cópias de segurança de longa duração está atualmente em pré-visualização e está disponível no Olá seguintes regiões: Leste da Austrália, Sudeste da Austrália, sul do Brasil, EUA Central, Ásia Oriental, EUA leste, EUA Leste 2, Índia Central, Sul da Índia, leste do Japão, oeste do Japão, Norte Central dos EUA, Norte Europa, EUA Centro-Sul, Sudeste asiático, Europa Ocidental e EUA oeste.
>

> [!NOTE]
> Pode ativar a cópia de segurança too200 bases de dados por cofre durante um período de 24 horas. Recomendamos que utilize um cofre separado para cada servidor toominimize Olá impacto este limite. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>Como funciona a retenção de cópias de segurança de longa duração de base de dados SQL

Com retenção de cópias de segurança de longo prazo, pode associar um servidor de base de dados SQL com um cofre dos serviços de recuperação do Azure. 

* Tem de criar cofre Olá no Olá mesma subscrição do Azure que criar do SQL Server de Olá e no Olá mesmo grupo de recursos e a região geográfico. 
* Em seguida, configure uma política de retenção para uma base de dados. Olá política causas Olá semanal completa da base de dados cópias de segurança toobe copiado toohello Cofre de serviços de recuperação e retidos por período de retenção especificado Olá (cópia de segurança too10 anos). 
* Em seguida, pode restaurar a base de dados de Olá de qualquer um destas cópias de segurança tooa nova base de dados em qualquer servidor na subscrição Olá. Armazenamento do Azure cria uma cópia de cópias de segurança existentes e cópia de Olá não tem nenhum impacto no desempenho na base de dados existente Olá.

> [!TIP]
> Para um tooguide como, consulte [configurar e restauro a partir da retenção de cópias de segurança de longa duração de base de dados do Azure SQL](sql-database-long-term-backup-retention-configure.md).

## <a name="enable-long-term-backup-retention"></a>Ativar a retenção de cópias de segurança de longa duração

tooconfigure cópia de segurança retenção de longo prazo para uma base de dados:

1. Criar um cofre dos serviços de recuperação do Azure no Olá mesmo grupo de recurso, de subscrição e região que o servidor de base de dados do SQL Server. 
2. Registe o Cofre de toohello Olá servidor.
3. Crie uma política de proteção do Azure Recovery Services.
4. Aplica Olá proteção política toohello bases de dados que necessitam de retenção de cópias de segurança de longa duração.

tooconfigure, gerir e restaurar uma base de dados de retenção de cópias de segurança de longa duração das cópias de segurança automatizadas num cofre dos serviços de recuperação do Azure, efetue um dos seguintes Olá:

* Olá, utilizando o portal do Azure: clique em **retenção de cópias de segurança de longa duração**, selecione uma base de dados e, em seguida, clique em **configurar**. 

   ![Selecione uma base de dados para a retenção de cópias de segurança de longa duração](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* Através do PowerShell: Aceda demasiado[configurar e restauro a partir da retenção de cópias de segurança de longa duração de base de dados do Azure SQL](sql-database-long-term-backup-retention-configure.md).

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>Restaurar uma base de dados que é armazenado com funcionalidade de cópia de segurança de retenção de longo prazo Olá

toorecover de uma cópia de segurança de retenção de cópias de segurança longo prazo:

1. Cofre do Olá de lista onde está armazenada a cópia de segurança de Olá.
2. Lista Olá contentor servidor lógico tooyour mapeada.
3. Origem de dados de Olá de lista no Cofre de Olá que é mapeado tooyour base de dados.
4. Lista Olá pontos de recuperação que estão disponível toorestore.
5. Restaure a base de dados de Olá Olá recuperação ponto toohello do servidor de destino na sua subscrição.

tooconfigure, gerir e restaurar uma base de dados de retenção de cópias de segurança de longa duração das cópias de segurança automatizadas num cofre dos serviços de recuperação do Azure, efetue um dos seguintes Olá:

* Olá, utilizando o portal do Azure: aceda demasiado[gerir longo prazo retenção de cópias de segurança utilizando Olá portal do Azure](sql-database-long-term-backup-retention-configure.md). 

* Através do PowerShell: Aceda demasiado[gerir retenção de cópias de segurança de longo prazo com o PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="get-pricing-for-long-term-backup-retention"></a>Obter o preço da retenção de cópias de segurança de longa duração

Retenção de cópias de segurança de longa duração de uma base de dados do SQL Server é cobrada de acordo com toohello [serviços de cópia de segurança do Azure, taxas de preços](https://azure.microsoft.com/pricing/details/backup/).

Depois do servidor de base de dados do SQL Server Olá toohello registado cofre, são-lhe cobrados para armazenamento total Olá que é utilizado pelo Olá semanal cópias de segurança armazenadas no Cofre de Olá.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>Vista disponíveis cópias de segurança que são armazenadas na retenção de cópias de segurança de longa duração

tooconfigure, gerir e restaurar uma base de dados de retenção de cópias de segurança de longa duração das cópias de segurança automatizadas num cofre do Azure Recovery Services utilizando Olá portal do Azure, efetue um dos seguintes Olá:

* Olá, utilizando o portal do Azure: aceda demasiado[gerir longo prazo retenção de cópias de segurança utilizando Olá portal do Azure](sql-database-long-term-backup-retention-configure.md). 

* Através do PowerShell: Aceda demasiado[gerir retenção de cópias de segurança de longo prazo com o PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="disable-long-term-retention"></a>Desativar a retenção de longo prazo

serviço de recuperação Olá automaticamente processa limpeza Olá de cópias de segurança com base no Olá fornecido a política de retenção. 

toostop envio Olá cópias de segurança para um cofre de toohello de base de dados específica, remova a política de retenção de Olá para essa base de dados.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> as cópias de segurança de Olá que já estão num cofre Olá não são afetadas. Estes são eliminados automaticamente pelo serviço de recuperação Olá quando o respetivo período de retenção expira.

## <a name="long-term-backup-retention-faq"></a>Retenção de cópias de segurança de longa duração FAQ

**Posso manualmente a eliminar as cópias de segurança específicas no Cofre de Olá?**

Atualmente não. cofre Olá limpa automaticamente cópias de segurança quando o período de retenção de Olá expirou.

**Pode registar os meus toomore de cópias de segurança do servidor toostore que um cofre?**

Não, atualmente, pode armazenar um cofre de cópias de segurança tooonly cada vez.

**Posso ter um cofre e o servidor em diferentes subscrições?**

Não, atualmente Olá cofre e o servidor tem de constar Olá mesmo grupo de recursos e de subscrição.

**Pode utilizar um cofre que criar numa região diferente da região do meu servidor?**

Não, Olá cofre e o servidor tem de ser Olá mesma região toominimize copiar tempo e evitar custos de tráfego.

**Como muitas bases de dados pode armazenar um cofre?**

Atualmente, fornecemos suporte cópias de segurança too1, 000 bases de dados por cofre. 

**Quantos cofres pode criar por subscrição**

Pode criar cópias de segurança too25 cofres por subscrição.

**Como muitas bases de dados pode configurar por dia por Cofre?**

Pode configurar 200 bases de dados por dia por cofre.

**Retenção de cópias de segurança de longa duração funciona com conjuntos elásticos?**

Sim. Qualquer base de dados no agrupamento de Olá pode ser configurado com a política de retenção de Olá.

**Pode escolher em que é criada a cópia de segurança de Olá de tempo de Olá?**

Não, a base de dados SQL controla Olá agenda de cópia de segurança toominimize Olá impacto no desempenho nas suas bases de dados.

**Tenho a encriptação transparente de dados ativada para a minha base de dados. Posso utilizá-lo com o Cofre de Olá?** 

Sim, a encriptação transparente de dados é suportada. Pode restaurar a base de dados de Olá do Cofre de Olá, mesmo se a base de dados original Olá já não existe.

**O que acontece com as cópias de segurança de Olá no Cofre de Olá minha subscrição está suspensa?** 

Se a sua subscrição está suspensa, vamos manter bases de dados existente do Olá e cópias de segurança. Novas cópias de segurança não são copiados toohello cofre. Após reativar subscrição Olá, o serviço Olá retoma de cópias de segurança toohello Cofre de cópia. O Cofre torna-se operações de restauro toohello acessível através da utilização de cópias de segurança de Olá que foram copiadas existe antes de subscrição de Olá foi suspenso. 

**Posso obter acesso ficheiros de cópia de segurança de base de dados do toohello SQL para que posso pode transferir ou restaurá-las do SQL Server de toohello?**

Não, atualmente não.

**É possível toohave várias agendas (diariamente, semanalmente, mensalmente, anualmente) dentro de uma política de retenção do SQL Server.**

Não, vários agendamentos atualmente só estão disponíveis para cópias de segurança da máquina virtual.

**E se configuramos retenção de cópias de segurança de longa duração numa base de dados que é uma base de dados secundária georreplicação ativa?**

Uma vez que não fazer cópias de segurança em réplicas, atualmente não é efectuada nenhuma opção para a retenção de cópias de segurança de longa duração em bases de dados secundárias. No entanto, é importante para os utilizadores tooset segurança de retenção de cópias de segurança de longa duração numa base de dados secundária georreplicação ativa para estes motivos:
* Quando ocorre uma ativação pós-falha e a base de dados de Olá torna-se uma base de dados primária, iremos efetuar um completo cópia de segurança, que é carregado toovault.
* Não há nenhum extra de cliente de toohello custo para configurar a retenção de cópias de segurança de longa duração numa base de dados secundária.

## <a name="next-steps"></a>Passos seguintes
Porque as cópias de segurança da base de dados proteger os dados de danos acidentais ou eliminação, se estiver a uma parte essencial dos quaisquer continuidade do negócio e a estratégia de recuperação após desastre. toolearn sobre Olá outras soluções de continuidade do negócio da base de dados SQL, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md).
