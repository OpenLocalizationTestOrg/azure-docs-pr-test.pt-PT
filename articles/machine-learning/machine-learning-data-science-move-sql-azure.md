---
title: aaaMove tooan de dados Azure SQL Database do Azure Machine Learning | Microsoft Docs
description: Criar tabela SQL e carregar dados tooSQL tabela
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Mover dados tooan SQL Database do Azure para o Azure Machine Learning
Este tópico descreve as opções de Olá para mover dados de ficheiros simples (formatos de CSV ou TSV) ou a partir dos dados armazenados numa no local do SQL Server tooan SQL database do Azure. Estas tarefas para mover dados na nuvem de toohello fazem parte do Olá o processo de ciência de dados de equipa.

Para um tópico que descreve as opções de Olá para mover dados tooan no local do SQL Server para o Machine Learning, consulte [mover dados tooSQL Server numa máquina virtual do Azure](machine-learning-data-science-move-sql-server-virtual-machine.md).

seguinte Olá **menu** liga tootopics que descrevem como dados tooingest em ambientes de destino onde os dados de Olá podem ser armazenados e processados durante Olá o processo de ciência de dados de equipa (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Olá tabela seguinte resume Olá as opções para mover dados tooan SQL Database do Azure.

| <b>ORIGEM</b> | <b>DESTINO: Base de dados SQL do Azure</b> |
| --- | --- |
| <b>Ficheiro simples (TSV formatado ou CSV)</b> |<a href="#bulk-insert-sql-query">Consulta SQL de inserção em massa |
| <b>SQL Server no local</b> |1. <a href="#export-flat-file">Exportar tooFlat ficheiro<br> 2. <a href="#insert-tables-bcp">Assistente de migração de base de dados do SQL Server<br> 3. <a href="#db-migration">Base de dados back cópias de segurança e restauro<br> 4. <a href="#adf">Fábrica de dados do Azure |

## <a name="prereqs"></a>Pré-requisitos
procedimentos de Olá aqui descritos requerem que tenha:

* Um **subscrição do Azure**. Se não tiver uma subscrição, pode inscrever-se numa [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Um **conta do storage do Azure**. Utilize uma conta de armazenamento do Azure para armazenar dados de Olá neste tutorial. Se não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo. Depois de ter criado a conta de armazenamento Olá, precisa de conta de Olá tooobtain chave utilizado armazenamento de Olá tooaccess. Consulte [gerir as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Acesso tooan **SQL Database do Azure**. Se tem de configurar uma base de dados de SQL do Azure, [introdução à base de dados do Microsoft Azure SQL](../sql-database/sql-database-get-started.md) fornece informações sobre como tooprovision uma nova instância de uma base de dados do SQL do Azure.
* Instalado e configurado **Azure PowerShell** localmente. Para obter instruções, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

**Dados**: processos de migração de Olá são demonstrados utilizando Olá [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/). Olá NYC Taxi conjunto de dados contém informações sobre dados de viagem e fairs e está disponível no armazenamento de Blobs do Azure: [NYC Taxi dados](http://www.andresmh.com/nyctaxitrips/). Um exemplo e uma descrição destes ficheiros são fornecidos na [NYC Taxi viagens Dataset Descrição](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Pode adaptar Olá procedimentos tooa aqui descrito conjunto de dados da sua própria ou siga os passos de Olá, conforme descrito utilizando Olá NYC Taxi conjunto de dados. Olá tooupload NYC Taxi conjunto de dados na base de dados do SQL Server no local, siga o procedimento de Olá descrito em [em massa importar dados na base de dados do SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Estas instruções se destinam a um SQL Server uma Máquina Virtual no Azure, mas o procedimento de Olá para carregar toohello SQL Server no local é Olá mesmo.

## <a name="file-to-azure-sql-database"></a>Mover dados de uma ficheiro simples origem tooan SQL database do Azure
Dados em ficheiros simples (formato CSV ou TSV) podem ser movidas tooan SQL database do Azure utilizando uma consulta de SQL de inserção em massa.

### <a name="bulk-insert-sql-query"></a>Consulta SQL de inserção em massa
passos de Olá para o procedimento de Olá utilizando Olá consulta de SQL de inserção em massa são semelhante toothose abordada nas secções Olá para mover dados de um tooSQL de origem do ficheiro simples Server numa VM do Azure. Para obter mais informações, consulte [consulta de SQL de inserção em massa](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Mover dados do local do SQL Server tooan SQL database do Azure
Se os dados de origem de Olá estiver armazenados num SQL Server no local, existem vários possibilidades para mover Olá dados tooan SQL database do Azure:

1. [Exportar tooFlat ficheiro](#export-flat-file)
2. [Assistente de migração de base de dados do SQL Server](#insert-tables-bcp)
3. [Base de dados back cópias de segurança e restauro](#db-migration)
4. [Azure Data Factory](#adf)

Olá passos para Olá três primeiros são muito semelhantes secções toothose [mover dados tooSQL Server numa máquina virtual do Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) que abrangem estes procedimentos mesmos. Ligações toohello adequadas secções dessa tópico são fornecidas na Olá seguir instruções.

### <a name="export-flat-file"></a>Exportar tooFlat ficheiro
passos de Olá para este ficheiro simples de tooa exportar são semelhante toothose abrangida [exportar tooFlat ficheiro](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Assistente de migração de base de dados do SQL Server
Olá passos para utilizar Olá Assistente de migração de base de dados do SQL Server são semelhante toothose abrangida [Assistente de migração de base de dados do SQL Server](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Base de dados back cópias de segurança e restauro
Olá os passos para utilizar a base de dados de cópia de segurança e restauro são semelhante toothose abrangida [da base de dados back cópias de segurança e restaurar](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Fábrica de dados do Azure
procedimento Olá para mover dados tooan SQL database do Azure com o Azure Data Factory (ADF) é fornecido no tópico Olá [mover dados de um tooSQL de servidor do SQL Server no local do Azure com o Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md). Este tópico mostra como toomove dados a partir de um tooan de base de dados do SQL Server no local do Azure SQL da base de dados através do Blob Storage do Azure com ADF.

Considere a utilização de ADF quando dados necessidades toobe continuamente migrado num cenário híbrido que acede no local e aos recursos na nuvem e quando os dados de Olá são transacionados ou tem toobe modificado ou lógica de negócio adicionou tooit quando a ser migrado. ADF permite Olá agendamento e a monitorização de tarefas utilizando scripts simples do JSON que gerem o movimento de Olá dos dados numa base periódica. ADF também tem outras funcionalidades, tais como o suporte para operações complexas.
