---
title: aaaOperating arquivo de consultas na SQL Database do Azure
description: "Saiba como toooperate Olá arquivo de consultas na SQL Database do Azure"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>Sistema operativo Olá arquivo de consultas na SQL Database do Azure
O arquivo de consultas no Azure é uma funcionalidade de base de dados completamente gerido que continuamente recolhe e apresenta informações detalhadas de históricos sobre todas as consultas. Pode pensar sobre o arquivo de consultas como dados gravador semelhante avião de tooan que significativamente simplifica o desempenho das consultas de resolução de problemas para a nuvem e os clientes no local. Este artigo explica os aspetos específicos de operativo arquivo de consultas no Azure. Com esta consulta previamente recolhidos dados, pode rapidamente diagnosticar e resolver problemas de desempenho e, por conseguinte, demora mais tempo a concentrar-se na sua empresa. 

O arquivo de consultas foi [globalmente disponível](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) na base de dados do Azure SQL desde Novembro de 2015. Arquivo de consultas está foundation Olá para análise de desempenho e a otimização de funcionalidades, tais como [Advisor de base de dados do SQL Server e o Dashboard de desempenho](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). Momento Olá de publicação deste artigo, o arquivo de consultas está em execução em mais de 200 000 bases de dados do utilizador no Azure, recolha informações relacionadas com a consulta para vários meses, sem interrupção.

> [!IMPORTANT]
> A Microsoft está no processo de Olá de ativar o arquivo de consultas para todas as bases de dados do SQL do Azure (existentes e novos). 
> 
> 

## <a name="optimal-query-store-configuration"></a>Configuração do arquivo de consultas ideal
Esta secção descreve as predefinições de configuração ideal que são tooensure concebida operação fiável de arquivo de consultas Olá e funcionalidades dependentes, tais como [Advisor de base de dados do SQL Server e o Dashboard de desempenho](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). Configuração predefinida está otimizada para recolha de dados contínua, que é o mínimo tempo despendido no OFF/READ_ONLY Estados.

| Configuração | Descrição | Predefinição | Comentário |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Especifica o limite de Olá de espaço de dados de Olá que pode efetuar o arquivo de consultas no interior da base de dados de cliente de z |100 |Imposto para novas bases de dados |
| INTERVAL_LENGTH_MINUTES |Define o tamanho de janela de tempo durante os quais as estatísticas de tempo de execução recolhidos para planos de consulta são agregadas e persistente. Cada plano de consulta ativa tem no máximo uma linha para um período de tempo definido com esta configuração |60 |Imposto para novas bases de dados |
| STALE_QUERY_THRESHOLD_DAYS |Política de limpeza baseados no tempo que controla o período de retenção de Olá de estatísticas de tempo de execução persistente e consultas Inativas |30 |Imposto para novas bases de dados e bases de dados com predefinido anterior (367) |
| SIZE_BASED_CLEANUP_MODE |Especifica se a limpeza de dados automática ocorre quando o limite de Olá se aproxima de tamanho de dados de arquivo de consultas |AUTOMÁTICA |Imposto para todas as bases de dados |
| QUERY_CAPTURE_MODE |Especifica se são controlados todas as consultas ou apenas um subconjunto de consultas |AUTOMÁTICA |Imposto para todas as bases de dados |
| FLUSH_INTERVAL_SECONDS |Especifica o período máximo durante o qual as estatísticas de tempo de execução capturada são mantidas na memória, antes de libertar toodisk |900 |Imposto para novas bases de dados |
|  | | | |

> [!IMPORTANT]
> Estas predefinições são automaticamente aplicadas na fase final de Olá de ativação de arquivo de consultas em todas as bases de dados SQL do Azure (ver nota importante anterior). Após este leve cópias de segurança, SQL Database do Azure não estar a alterar os valores de configuração definidos pelos clientes, a menos que possam afetam negativamente carga de trabalho primária ou operações fiáveis de Olá arquivo de consultas.
> 
> 

Se pretender toostay com as definições personalizadas, utilize [ALTER DATABASE com opções de arquivo de consultas](https://msdn.microsoft.com/library/bb522682.aspx) estado anterior do toorevert configuração toohello. Veja [melhores práticas com Olá arquivo de consultas](https://msdn.microsoft.com/library/mt604821.aspx) ordem toolearn como superior escolheu parâmetros de configuração ideal.

## <a name="next-steps"></a>Passos seguintes
[Informações de desempenho de base de dados do SQL Server](sql-database-performance.md)

## <a name="additional-resources"></a>Recursos adicionais
Para obter mais informações modificações Olá seguintes artigos:

* [Um gravador de dados para a base de dados](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Monitorização de desempenho ao utilizar o arquivo de consultas Olá](https://msdn.microsoft.com/library/dn817826.aspx)
* [Cenários de utilização do arquivo de consultas](https://msdn.microsoft.com/library/mt614796.aspx)
* [Monitorização de desempenho ao utilizar o arquivo de consultas Olá](https://msdn.microsoft.com/library/dn817826.aspx) 

