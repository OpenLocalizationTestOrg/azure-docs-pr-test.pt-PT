---
title: "aaaSQL base de dados - otimização automática | Microsoft Docs"
description: Base de dados SQL analisa a consulta SQL e automaticaly feita toouser carga de trabalho.
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>Ajuste automático

Base de dados SQL do Azure é um serviço de dados completamente gerido que monitoriza consultas Olá que são executadas na base de dados de Olá e automaticamente podem melhorar o desempenho da carga de trabalho Olá. Base de dados SQL do Azure tem um mecanismo de intelligence incorporadas que pode otimizar e melhorar o desempenho das consultas através da adaptação dinamicamente a carga de trabalho de tooyour de base de dados de Olá automaticamente. A otimização automática na SQL Database do Azure pode ser uma das funcionalidades mais importantes de Olá que pode ativar no desempenho da base de dados do Azure SQL toooptimize das suas consultas.

Consulte este artigo para obter os passos Olá demasiado[ativar a otimização automática](sql-database-automatic-tuning-enable.md) utilizando Olá portal do Azure.

## <a name="why-automatic-tuning"></a>Por que razão a otimização automática?

Uma das tarefas principais de Olá na administração clássico da base de dados está a monitorizar carga de trabalho Olá, identificar SQL crítico consulta índices que devem ser adicionados tooimprove desempenho e raramente utilizado índices. Base de dados SQL do Azure fornece detalhadas aprofundadas índices e consultas de Olá terá toomonitor. No entanto, a monitorização contínua de bases de dados é uma tarefa difícil e entediante, especialmente se forem muitas. Gerir um grande número de bases de dados poderá ser toodo impossível eficientemente mesmo com todas as ferramentas disponíveis e relatórios que fornecem a SQL Database do Azure e o portal do Azure. Em vez de monitorização e otimizar a sua base de dados manualmente, poderá considerar delegar algumas das Olá monitorização e otimização ações tooAzure base de dados do SQL Server utilizando a funcionalidade de otimização automática. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Como funciona o trabalho de otimização automático?

Base de dados SQL do Azure tem um processo de análise e monitorização contínua de desempenho que constantemente aprende Olá características da sua carga de trabalho e identificar potenciais problemas e melhorias.

![Processo automático de otimização](./media/sql-database-automatic-tuning/tuning-process.png)

Ativa este processo SQL Database do Azure toodynamically adaptar tooyour carga de trabalho por localizar os índices e planos poderão melhorar o desempenho das cargas de trabalho e o que indexa afeta as cargas de trabalho. Com base nestes findings, a otimização automática aplica-se ações de otimização que melhoram o desempenho da sua carga de trabalho. Além disso, o SQL Database do Azure monitoriza continuamente o desempenho após qualquer alteração efetuada pelo tooensure otimização automática, que melhora o desempenho da sua carga de trabalho. Qualquer ação que não tenha a melhorar o desempenho é automaticamente revertida. O processo de verificação é uma funcionalidade chave que assegura que qualquer alteração efetuada pelo otimização automática não diminuir o desempenho de Olá da sua carga de trabalho.

Existem dois aspetos de otimização automáticos, que estão disponíveis no SQL Database do Azure:

 -  **A gestão automática de índices** que identifica os índices devem ser adicionados na base de dados e índices que devem ser removidos.
 -  **Correção automática plano** (disponível em breve, já disponível no SQL Server 2017) que identifica os planos problemáticos e correções SQL planear problemas de desempenho.

## <a name="automatic-index-management"></a>Gestão automática de índices

Na base de dados SQL do Azure, a gestão de índices é fácil porque a base de dados do Azure SQL aprende a carga de trabalho e garante que os dados sempre ideal estão indexados. Conceção do índice adequada é fundamental para otimizar o desempenho da sua carga de trabalho e a gestão automática de índices pode ajudar a otimizar os índices. A gestão automática de índices pode corrigir problemas de desempenho nas bases de dados incorretamente indexadas, ou manter e melhorar os índices no esquema de base de dados existente Olá. 

### <a name="why-do-you-need-index-management"></a>Por que motivo precisa de gestão de índice?

Os índices acelerar a algumas das suas consultas que leiam os dados das tabelas de Olá; No entanto, estas podem atrasar consultas Olá que atualizam dados. Terá de toocarefully analisar quando toocreate um índice e as colunas terá tooinclude no Olá índice. Não podem ser necessários alguns índices após algum tempo. Por conseguinte, terá de tooperiodically identificar e remover os índices de Olá não coloque qualquer benefícios. Se ignorar Olá índices não utilizados, o desempenho das consultas de Olá que atualizam dados deverá ser diminuído sem qualquer benefício em consultas de Olá que leu os dados. Os índices afetam também desempenho global do sistema de Olá porque atualizações adicionais exigem registo desnecessário.

Ao localizar o conjunto de ideal Olá dos índices melhorar o desempenho das consultas de Olá ler os dados das tabelas e que tenham um impacto mínimo sobre atualizações poderão exigir análise contínua e complexa.

Base de dados SQL do Azure utiliza intelligence incorporada e regras avançadas que analisar as suas consultas, identifique os índices que seriam ideais para cargas de trabalho atuais e índices de Olá podem ser removidos. Base de dados SQL do Azure garante que tem um conjunto mínimo necessário de índices otimizar as consultas de Olá que leu os dados, afetar Olá minimizado Olá outras consultas.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>Como tooidentify indexa toobe essa necessidade alterado na base de dados?

Base de dados SQL do Azure com o processo de gestão de índice mais fácil. Em vez do processo de Olá tedious de análise de carga de trabalho manual e monitorização do índice, SQL Database do Azure analisa a carga de trabalho, identifica as consultas de Olá que foi executadas mais rapidamente com um novo índice e identifica os índices utilizados ou duplicados. Encontrar mais informações sobre a identificação dos índices que devem ser alteradas em [encontrar recomendações do índice no portal do Azure](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Considerações sobre a gestão automática de índice

Se achar que regras incorporadas Olá melhorar o desempenho de Olá da base de dados, poderá permitem gerir automaticamente os índices de base de dados do SQL do Azure.

Ações necessárias toocreate índices necessários bases de dados do Azure SQL Server podem consumir recursos e temporariamente afetam o desempenho da carga de trabalho. impacto de Olá toominimize da criação do índice no desempenho da carga de trabalho, SQL Database do Azure localiza a janela de tempo adequados Olá em nenhuma operação de gestão do índice. Otimização de ação é adiada se precisar de base de dados de Olá recursos tooexecute a carga de trabalho e iniciada quando a base de dados de Olá tem espaço suficiente os recursos que podem ser utilizados para tarefas de manutenção de Olá. Uma funcionalidade importante na gestão automática de índices é uma verificação de ações de Olá. Quando a SQL Database do Azure cria ou ignora índice, um processo de monitorização analisa o desempenho da sua tooverify de carga de trabalho que a ação de Olá melhorada desempenho Olá. Se não coloque melhoria significativa – ação Olá imediatamente for revertida. Desta forma, SQL Database do Azure garante que ações automáticas não afetar negativamente o desempenho da sua carga de trabalho. Os índices criados pela otimização automática estão transparentes para a operação de manutenção de Olá no esquema subjacente Olá. Alterações do esquema, tais como remover ou mudar o nome de colunas não são bloqueadas por presença Olá índices criados automaticamente. Os índices são criados automaticamente pelo SQL Database do Azure são imediatamente removidos quando relacionadas com a tabela ou de colunas é ignorado.

## <a name="automatic-plan-choice-correction"></a>Correção de escolha do plano automática

Correção automática plano é uma nova funcionalidade otimização automática adicionada no SQL Server 2017 CTP2.0 que identifica os planos SQL que misbehave. Esta opção de otimização automática está disponível em breve na SQL Database do Azure. Encontrar mais informações em [otimização automática no SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Passos seguintes

- tooenable automática otimização na SQL Database do Azure e permitem automática totalmente a funcionalidade de otimização gerir a sua carga de trabalho, consulte [ativar a otimização automática](sql-database-automatic-tuning-enable.md).
- toouse manual de otimização, pode rever [otimização recomendações no portal do Azure](sql-database-advisor-portal.md) e aplicar manualmente Olá aqueles que melhoram o desempenho das consultas.
