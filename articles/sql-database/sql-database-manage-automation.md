---
title: "aaaManage bases de dados do SQL do Azure através da automatização do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automatização do Azure pode ser utilizados toomanage bases de dados de SQL do Azure à escala."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Gerir bases de dados do SQL do Azure através da automatização do Azure
Este guia irá apresentar toohello serviço de automatização do Azure e como pode ser utilizado toosimplify gestão das bases de dados SQL do Azure.

## <a name="what-is-azure-automation"></a>O que é a Automatização do Azure?
[A automatização do Azure](https://azure.microsoft.com/services/automation/) é um serviço do Azure para simplificar a gestão de nuvem através de automatização de processos. Tarefas de longa execução, manuais, propensas ao erro e frequentemente repetidas através da automatização do Azure, podem ser automatizada tooincrease fiabilidade, eficiência e toovalue de tempo para a sua organização.

A automatização do Azure fornece um motor de execução do fluxo de trabalho altamente fiáveis e elevada disponibilidade que ajusta às suas necessidades de toomeet à medida que aumenta a sua organização. Na automatização do Azure, os processos podem ser arrancou manualmente, por sistemas de terceiros 3rd ou em intervalos agendados para que as tarefas acontecer exatamente quando necessário.

Reduzir a sobrecarga operacional e libertar IT / toofocus de pessoal de DevOps no trabalho que adiciona o valor de negócio, movendo a sua toobe de tarefas de gestão de nuvem são executadas automaticamente pela automatização do Azure.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Como pode que o automatização do Azure ajuda a gerir bases de dados SQL do Azure?
Base de dados SQL do Azure podem ser gerido na automatização do Azure utilizando Olá [cmdlets do PowerShell de base de dados do SQL Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) que estão disponíveis no Olá [ferramentas do Azure PowerShell](/powershell/azure/overview). A automatização do Azure tem estes cmdlets PowerShell de base de dados SQL do Azure disponíveis Box Olá, para que possam executar todas as tarefas de gestão de BD do SQL no âmbito do serviço de Olá. Também pode ser emparelhado estes cmdlets na automatização do Azure com cmdlets de Olá para outros serviços do Azure, as tarefas complexas tooautomate através de serviços do Azure e 3rd sistemas de terceiros.

A automatização do Azure também tem Olá capacidade toocommunicate com servidores SQL diretamente, ao emitir comandos SQL com o PowerShell.

Olá [Galeria de runbooks de automatização do Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contém uma variedade de produto equipa e da Comunidade runbooks tooget iniciado a automatizar a gestão de bases de dados do Azure SQL, outros serviços do Azure e 3rd sistemas de terceiros. Galeria runbooks incluem:

* [Executar consultas do SQL Server em relação a uma base de dados do SQL Server](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [Aumentar verticalmente (ou reduzir verticalmente) uma base de dados do SQL do Azure com base numa agenda](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Truncar uma tabela SQL, se a sua base de dados se aproxima o tamanho máximo](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Índice de tabelas numa base de dados SQL do Azure se estes são muito fragmentados](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá da automatização do Azure e como pode ser utilizado toomanage bases de dados de SQL do Azure, siga estas toolearn ligações mais sobre a automatização do Azure.

* [Descrição geral da automatização do Azure](../automation/automation-intro.md)
* [O meu primeiro runbook](../automation/automation-first-runbook-graphical.md)
* [Mapa de aprendizagem de automatização do Azure](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Automatização do Azure: O SQL Server Agent no Olá na nuvem](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

