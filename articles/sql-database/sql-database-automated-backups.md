---
title: "aaaAzure base de dados SQL automáticas georredundante cópias de segurança | Microsoft Docs"
description: "Base de dados SQL cria uma cópia de segurança da base de dados local cada alguns minutos e utiliza o Azure armazenamento georredundante com acesso de leitura para a redundância geográfica automaticamente."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>Saiba mais sobre cópias de segurança de base de dados SQL automáticas

Base de dados SQL cria cópias de segurança da base de dados e utiliza o armazenamento com redundância geográfica do Azure acesso de leitura (RA-GRS) georredundância tooprovide automaticamente. Estas cópias de segurança são criadas automaticamente e, sem encargos adicionais. Não precisa de toodo qualquer caráter toomake que acontecê-los. Cópias de segurança da base de dados são uma parte essencial de qualquer estratégia de recuperação de continuidade e desastre negócio porque protegem os dados de danos acidentais ou eliminação. Se quiser tookeep cópias de segurança no seu próprio contentor de armazenamento pode configurar uma política de retenção de cópias de segurança de longa duração. Para obter mais informações, veja [Retenção de longa duração](sql-database-long-term-retention.md).

## <a name="what-is-a-sql-database-backup"></a>O que é uma cópia de segurança da base de dados SQL?

Base de dados do SQL Server utiliza o SQL Server tecnologia toocreate [completa](https://msdn.microsoft.com/library/ms186289.aspx), [diferencial](https://msdn.microsoft.com/library/ms175526.aspx), e [registo de transações](https://msdn.microsoft.com/library/ms191429.aspx) cópias de segurança. cópias de segurança de registos de transação de Olá acontecem, geralmente, a cada 5-10 minutos, com frequência Olá com base no nível de desempenho de Olá e a quantidade de atividade de base de dados. Transação registo as cópias de segurança, com as cópias de segurança completas e diferenciais, permitem-lhe toorestore uma base de dados tooa específico ponto no tempo toohello mesmo servidor que aloja a base de dados de Olá. Ao restaurar uma base de dados, Olá figuras de serviço que completo, o valor diferencial e a transação cópias de segurança do registo necessário toobe restaurada.


Pode utilizar estas cópias de segurança para:

* Restaure uma base de dados tooa no momento dentro do período de retenção de Olá. Esta operação irá criar uma nova base de dados no Olá mesmo servidor que a base de dados original Olá.
* Restaure um período de toohello de base de dados eliminada que tiver sido eliminado ou a qualquer altura dentro do período de retenção de Olá. base de dados de Olá eliminado só pode ser restaurado em Olá mesmo servidor onde a base de dados original Olá foi criado.
* Restaure uma região geográfica do tooanother de base de dados. Isto permite-lhe toorecover de desastres geográfica quando não é possível aceder ao servidor e base de dados. Cria uma nova base de dados em qualquer servidor existente em qualquer lugar na Olá mundo. 
* Restaure uma base de dados a partir de uma cópia de segurança específica armazenada no seu Cofre de serviços de recuperação do Azure. Isto permite-lhe toorestore uma versão antiga da base de dados de Olá toosatisfy um pedido de conformidade ou toorun uma versão antiga da aplicação Olá. Consulte [retenção de longo prazo](sql-database-long-term-retention.md).
* tooperform um restauro, consulte [restaurar base de dados de cópias de segurança](sql-database-recovery-using-backups.md).

> [!NOTE]
> No armazenamento do Azure, o termo de Olá *replicação* refere-se toocopying ficheiros a partir de uma localização tooanother. Do SQL Server *replicação de base de dados* refere-se tookeeping toomultiple secundário bases de dados sincronizadas com a base de dados primária. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>Quantidade de armazenamento cópia de segurança está incluído sem qualquer custo?
Base de dados do SQL Server fornece cópias de segurança too200% do seu armazenamento de base de dados aprovisionado máximo como armazenamento de cópia de segurança sem custos adicionais. Por exemplo, se tiver uma instância de base de dados Standard com um tamanho de base de dados de aprovisionamento de 250 GB, ter 500 GB de armazenamento de cópia de segurança, sem encargos adicionais. Se a base de dados exceder Olá fornecido o armazenamento de cópia de segurança, pode escolher o período de retenção de Olá tooreduce contactando o suporte do Azure. Outra opção é toopay para armazenamento de cópia de segurança extra que é faturado a taxa de acesso de leitura geograficamente armazenamento redundantes (RA-GRS) padrão Olá. 

## <a name="how-often-do-backups-happen"></a>Frequência cópias de segurança acontecem?
Cópias de segurança da base de dados completa semanal, acontecem cópias de segurança da base de dados diferencial acontecem, geralmente, cada algumas horas e registo de transações cópias de segurança acontecem, geralmente, a cada 5-10 minutos. Olá primeira cópia de segurança completa é agendada imediatamente depois de uma base de dados. Normalmente, terminar dentro de 30 minutos, mas poderá demorar mais quando a base de dados de Olá tenha um tamanho significativo. Por exemplo, a cópia de segurança inicial Olá poderá demorar mais de uma base de dados restaurada ou uma cópia da base de dados. Depois de Olá primeira cópia de segurança completa, todas as cópias de segurança adicionais são agendadas automaticamente e geridas automaticamente em segundo plano de Olá. Temporização exato de Olá de todas as cópias de segurança da base de dados é determinada pelo Olá serviço base de dados do SQL Server como equilibra a Olá geral carga de trabalho do sistema. 

ocorre com base numa agenda de replicação de armazenamento do Azure Olá georreplicação Olá armazenamento de cópia de segurança.

## <a name="how-long-do-you-keep-my-backups"></a>O período de tempo, manter a minha cópias de segurança?
Cada cópia de segurança da base de dados do SQL Server tem um período de retenção baseia Olá [camada de serviço](sql-database-service-tiers.md) da base de dados de Olá. período de retenção de Olá para uma base de dados no:


* Camada de serviço básico é de 7 dias.
* Camada de serviço Standard é 35 dias.
* Camada de serviço Premium é 35 dias.

Se mudar a base de dados de Olá Standard ou Premium serviço camadas tooBasic, cópias de segurança de Olá são guardadas para sete dias. Todas as cópias de segurança existentes com mais de sete dias já não estão disponíveis. 

Se atualizar a base de dados do tooStandard de camada de serviço básico Olá ou Premium, base de dados SQL mantém cópias de segurança existentes antes de serem 35 dias. Mantém cópias de segurança novas à medida que ocorrem 35 dias.

Se eliminar uma base de dados, base de dados SQL mantém cópias de segurança de Olá na Olá mesma forma que faria para uma base de dados online. Por exemplo, suponha que elimine uma base de dados básica que tem um período de retenção de sete dias. É guardada uma cópia de segurança que é de quatro dias de antiguidade para três dias mais.

> [!IMPORTANT]
> Se eliminar o servidor de SQL do Azure Olá que aloja as bases de dados do SQL Server, todas as bases de dados que pertencem toohello servidor também são eliminados e não podem ser recuperados. Não é possível restaurar um servidor eliminado.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>Como tooextend Olá de cópia de segurança período de retenção?
Se a sua aplicação requer que as cópias de segurança Olá estão disponíveis para o período de tempo pode expandir o período de retenção incorporada Olá configurando Olá política de retenção de cópias de segurança longo prazo para bases de dados individuais (política imediatamente disponíveis). Isto permite-lhe período de retenção de incorporada-it de Olá de tooextend de anos de too10 tooup de 35 dias. Para obter mais informações, veja [Retenção de longa duração](sql-database-long-term-retention.md).

Depois de adicionar Olá imediatamente disponíveis política tooa da base de dados utilizando o portal do Azure ou a API, cópias de segurança Olá semanais completa da base de dados serão copiado automaticamente tooyour seu Cofre de serviço de cópia de segurança do Azure. Se a base de dados é encriptado com TDE Olá as cópias de segurança são encriptadas automaticamente inativos.  Olá cofre dos serviços será automaticamente eliminar as cópias de segurança expiradas com base nas respetivas timestamp e Olá política imediatamente disponíveis.  Para que não precisa de agenda de cópia de segurança de Olá toomanage ou preocupe sobre a limpeza de Olá de Olá ficheiros antigos. Olá, suporta a API Olá restauro Cofre de cópias de segurança armazenadas no Olá, desde que o Cofre Olá está na mesma subscrição que a base de dados do SQL Server. Pode utilizar o portal do Azure de Olá ou PowerShell tooaccess estas cópias de segurança.

> [!TIP]
> Para um tooguide como, consulte [configurar e restauro a partir da retenção de cópias de segurança de longa duração de SQL Database do Azure](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>As cópias de segurança são encriptadas?

Quando TDE está ativada para uma base de dados SQL do Azure, cópias de segurança também são encriptadas. Todas as novas bases de dados do SQL do Azure estão configurados com TDE ativada por predefinição. Para obter mais informações sobre TDE, consulte [encriptação transparente de dados com a SQL Database do Azure](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).

## <a name="next-steps"></a>Passos seguintes

- Cópias de segurança da base de dados são uma parte essencial de qualquer estratégia de recuperação de continuidade e desastre negócio porque protegem os dados de danos acidentais ou eliminação. toolearn sobre Olá outras soluções de continuidade do negócio SQL Database do Azure, consulte [descrição geral da continuidade do negócio](sql-database-business-continuity.md).
- toorestore tooa ponto no tempo utilizando Olá portal do Azure, consulte [restaurar base de dados tooa ponto no tempo utilizando o portal do Azure de Olá](sql-database-recovery-using-backups.md).
- toorestore tooa ponto no tempo com o PowerShell, consulte [restaurar base de dados tooa ponto no tempo com o PowerShell](scripts/sql-database-restore-database-powershell.md).
- tooconfigure, gerir e restaurar a partir de retenção de longa duração das cópias de segurança automatizadas num cofre do Azure Recovery Services utilizando Olá Consulte portal, do Azure [gerir longo prazo retenção de cópias de segurança utilizando Olá portal do Azure](sql-database-long-term-backup-retention-configure.md).
- tooconfigure, gerir e restaurar a partir de retenção de longa duração das cópias de segurança automatizadas num cofre do Azure Recovery Services com o PowerShell, consulte [gerir retenção de cópias de segurança de longo prazo com o PowerShell](sql-database-long-term-backup-retention-configure.md).
