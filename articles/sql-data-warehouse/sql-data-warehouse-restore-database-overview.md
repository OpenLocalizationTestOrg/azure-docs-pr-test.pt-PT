---
title: "aaaRestore um armazém de dados do Azure - local e georredundante | Microsoft Docs"
description: "Descrição geral das opções de restauro de base de dados de Olá para recuperar uma base de dados no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>Restauro do SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Descrição geral][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

SQL Data Warehouse oferece restauros geográficas tanto locais como parte do respetivo após desastre do armazém de dados capacidades de recuperação. Utilize toorestore de cópias de segurança para do armazém de dados o restauro de tooa do armazém de dados do ponto na região primária Olá ou utilize cópias de segurança georredundante toorestore tooa diferentes região geográfica. Este artigo explica especificações Olá restaurar um armazém de dados.

## <a name="what-is-a-data-warehouse-restore"></a>O que é um restauro do armazém de dados?
Um restauro do armazém de dados é um novo armazém de dados que é criado a partir de uma cópia de segurança existente ou do armazém de dados eliminada. armazém de dados restaurada do Olá recria o armazém de dados de cópia de segurança de Olá num momento específico. Uma vez que o SQL Data Warehouse é um sistema distribuído, um restauro do armazém de dados é criado a partir de muitos ficheiros de cópia de segurança que são armazenados em blobs do Azure. 

Restauro da base de dados é uma parte essencial de qualquer estratégia de recuperação de continuidade e desastre negócio porque cria novamente os dados depois de danos acidentais ou eliminação.

Para obter mais informações, consulte:

* [Cópias de segurança do SQL Data Warehouse](sql-data-warehouse-backups.md)
* [Descrição geral da continuidade de negócio](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Pontos de restauro do armazém de dados
Como uma vantagem de utilizar o Premium Storage do Azure, o SQL Data Warehouse utiliza o Blob de armazenamento do Azure instantâneos toobackup Olá principal do armazém de dados. Cada instantâneo tiver um ponto de restauro que representa o tempo de Olá instantâneo Olá foi iniciado. toorestore um armazém de dados, escolha um ponto de restauro e emitir um comando de restauro.  

O SQL Data Warehouse sempre restaura Olá tooa cópia de segurança novo armazém de dados. Pode manter o armazém de dados restaurada do Olá e Olá atual ou elimine um deles. Se quiser tooreplace Olá atual do armazém de dados com Olá restaurada do armazém de dados, pode alterá-lo.

Se precisar de toorestore um armazém de dados eliminada ou em pausa, pode [criar um pedido de suporte](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Georredundante restauro
Pode restaurar a sua região tooany do armazém de dados que suportam o Azure SQL Data Warehouse ao seu nível de desempenho que escolheu. Tenha em atenção que DWU 9000 e 18000 não são suportados em todas as regiões durante a pré-visualização de Olá.

> [!NOTE]
> restauro de um georredundante tooperform que tem não optou por fora esta funcionalidade.
> 
> 

## <a name="restore-timeline"></a>Restaurar a linha cronológica
Pode restaurar um ponto de restauro disponíveis de tooany de base de dados dentro de Olá últimos sete dias. Instantâneos de iniciar a cada quatro horas tooeight e estão disponíveis para sete dias. Quando um instantâneo com mais de sete dias, expirar e o respetivo ponto de restauro já não está disponível.

## <a name="restore-costs"></a>Restaurar os custos
encargos de armazenamento Olá Olá restaurada do armazém de dados é faturado a taxa de Premium Storage do Azure Olá. 

Se colocar em pausa de um armazém de dados restaurada, são-lhe cobrados para armazenamento a taxa de Premium Storage do Azure Olá. Olá vantagem colocar em pausa não é que lhe serem cobrados para recursos de informática Olá DWU.

Para obter mais informações sobre preços do SQL Data Warehouse, consulte [preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Utilizações de restauro
a utilização de primário Olá do restauro do armazém de dados está toorecover dados após a perda acidental de dados ou danos.

Também pode utilizar tooretain de restauro do armazém de dados uma cópia de segurança para mais de sete dias. Depois de o restauro da cópia de segurança de Olá, que tem o armazém de dados de Olá online e pode colocar em pausa-indefinidamente toosave custos de computação. base de dados em pausa Olá implica a taxa de Premium Storage do Azure Olá, os encargos de armazenamento. 

## <a name="related-topics"></a>Tópicos relacionados
### <a name="scenarios"></a>Cenários
* Para obter uma descrição de continuidade do negócio, consulte [descrição geral da continuidade de negócio](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

tooperform um armazém de dados restaurar, o restauro utilizando:

* Consulte portal, do Azure [restaurar um armazém de dados utilizando Olá portal do Azure](sql-data-warehouse-restore-database-portal.md)
* Cmdlets do PowerShell, consulte [restaurar um armazém de dados utilizando cmdlets do PowerShell](sql-data-warehouse-restore-database-powershell.md)
* APIs de REST, consulte [restaurar um armazém de dados utilizando Olá REST APIs](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
