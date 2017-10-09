---
title: aaaManage bases de dados no Azure SQL Data Warehouse | Microsoft Docs
description: "Descrição geral da gestão de bases de dados do armazém de dados do SQL Server. Inclui ferramentas de gestão, as DWUs e o desempenho de escalamento horizontal, resolução de problemas de desempenho das consultas, estabelecer políticas boa segurança e restaurar uma base de dados de Corrupção de dados ou a partir de uma falha regional."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>Gerir bases de dados no Azure SQL Data Warehouse
O SQL Data Warehouse automatiza vários aspetos da gestão de bases de dados. Por exemplo, desempenho tooscale basta tooadjust e paga Olá neste nível de recursos de computação e, em seguida, permitir que o SQL Data Warehouse fazê-lo a todos os Olá trabalho de ampliar e dimensionamento back.

Undoubtedly convém toomonitor sua tooidentify de carga de trabalho, o desempenho tem de, bem como resolver problemas relacionados com consultas de execução longa. Também terá de tooperform algumas tarefas toomanage as permissões de segurança para utilizadores e os inícios de sessão.

Esta descrição geral inclui estes aspetos da gestão do armazém de dados do SQL Server.

* Ferramentas de gestão
* Dimensionar a computação
* Colocar em pausa e retomar
* Melhores práticas do desempenho
* Monitorização de consulta
* Segurança
* Cópia de segurança e restauro

## <a name="management-tools"></a>Ferramentas de gestão
Pode utilizar uma variedade de bases de dados de toomanage de ferramentas no SQL Data Warehouse. Como gerir bases de dados, irá desenvolver as preferências de ferramenta para cada tipo de tarefa terá tooperform.

### <a name="azure-portal"></a>Portal do Azure
Olá [portal do Azure] [ Azure portal] é um portal baseado na web, onde pode criar, atualizar e eliminar as bases de dados-las e monitorizar os recursos de base de dados. Esta ferramenta é uma grande é se que está a começar com o Azure, gerir um pequeno número de bases de dados, ou precisar de tooquickly fazer algo.

tooget começar Olá portal do Azure, consulte [criar um SQL Data Warehouse (portal do Azure)][Create a SQL Data Warehouse (Azure portal)].

### <a name="sql-server-data-tools-in-visual-studio"></a>Ferramentas de dados do SQL Server no Visual Studio
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) no Visual Studio permite-lhe tooconnect gerir e desenvolver as bases de dados. Se tiver um programador de aplicações familiarizado com o Visual Studio ou outros ambientes de desenvolvimento integrado (IDEs), experimente utilizar SSDT no Visual Studio.

SSDT inclui Olá SQL Server Object Explorer que lhe permite toovisualize, ligar e executar scripts em bases de dados do armazém de dados do SQL Server. tooquickly ligar tooSQL do armazém de dados, basta clicar em Olá **abrir no Visual Studio** botão na barra de comando Olá quando visualiza detalhes de base de dados de Olá em Olá Portal clássico do Azure.  

tooget iniciado com SSDT no Visual Studio, consulte [consultar o Azure SQL Data Warehouse com o Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].

### <a name="command-line-tools"></a>Ferramentas de linha de comandos
Ferramentas de linha de comandos são ideais para automatizar as cargas de trabalho.  PowerShell sqlcmd, sendo duas formas excelente tooautomate os processos.  Recomendamos que estas ferramentas para gerir um grande número de servidores de lógicas e implementar as alterações de recursos num ambiente de produção como tarefas de Olá necessárias podem ser convertidos em script e, em seguida, automatizadas.

### <a name="dynamic-management-views"></a>Vistas de gestão dinâmica
DMVs são Olá bread e butter da gestão do armazém de dados do SQL Server. Quase todas as informações que analisa no portal de Olá depende DMVs. toosee uma lista de DMVs de armazém de dados do SQL Server, consulte [vistas de sistema do SQL Data Warehouse][SQL Data Warehouse system views].

tooget iniciado, consulte [ligar e consultar com sqlcmd][Connect and query with sqlcmd], e [criar uma base de dados (PowerShell)][Create a database (PowerShell)].

## <a name="scale-compute"></a>Dimensionar a computação
No SQL Data Warehouse, pode dimensionar rapidamente o desempenho out ou retroceder por aumente ou diminua a recursos de computação de CPU, memória e largura de banda de e/s. desempenho de tooscale, tudo o que precisa toodo é ajuste Olá número de unidades do data warehouse (DWUs) que o SQL Data Warehouse aloca tooyour base de dados. O SQL Data Warehouse rapidamente torna Olá alterar e processa todos os Olá subjacente alterações toohardware ou software.

toolearn mais informações sobre dimensionamento DWUs, consulte [Dimensionar desempenho].

## <a name="pause-and-resume"></a>Colocar em pausa e retomar
custos de toosave, pode colocar em pausa e retomar computação recursos a pedido. Por exemplo, se não utilizar a base de dados de Olá durante a noite Olá e no fim de semana, pode colocar em pausa-lo durante essas horas e retomá-lo durante o dia de Olá. Não lhe será cobrado dwus enquanto a base de dados de Olá está em pausa.

Para obter mais informações, consulte [colocar em pausa computação][Pause compute], e [retomar a computação][Resume compute].

## <a name="performance-best-practices"></a>Melhores práticas do desempenho
Quando a introdução com uma nova tecnologia, detetar truques que funcionam melhor direito de início de Olá e sugestões de Olá pode poupar muitos de tempo.  Encontrará as melhores práticas ao longo de muitos dos nossos tópicos.

toosee muitos um resumo das considerações mais importantes de Olá quando desenvolver a sua carga de trabalho, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].

## <a name="query-monitoring"></a>Monitorização de consulta
Por vezes, uma consulta está a ser executado demasiado tempo, mas não é Certifique-se de que é culprit Olá. O SQL Data Warehouse tem vistas de gestão dinâmica (DMVs) que pode utilizar toofigure saída que consulta está a demorar demasiado tempo.

consultas de execução longa toofind, consulte [monitorizar a carga de trabalho com DMVs][Monitor your workload using DMVs].

## <a name="security"></a>Segurança
toomaintain um sistema seguro, tem de estar num alerta Olá e proteger contra qualquer tipo de acesso não autorizado. Um sistema de segurança tem toomake se as regras de firewall estão em vigor autorizado para apenas endereços IP podem ligar. Necessita de uma autenticação adequada das credenciais do utilizador. Depois de um utilizador tenha ligado toohello base de dados, Olá utilizador deve apenas tem permissões tooperform um número mínimo de ações. toosecure dados, pode utilizar a encriptação. Também é importante toohave auditoria e controlo para pode retrace eventos se não houver qualquer atividade suspeita.

toolearn sobre a gestão de segurança, head através de toohello [descrição geral de segurança][Security overview].

## <a name="backup-and-restore"></a>Cópia de segurança e restauro
Ter backps fiável dos seus dados é uma parte essencial dos qualquer base de dados de produção. Armazém de dados do SQL Server mantém os seus dados seguros por automaticamente fazer cópias de segurança das bases de dados do Active Directory em intervalos regulares. Estas cópias de segurança permitem-lhe toorecover de cenários em que tiver danificado os dados ou acidentalmente ignorados os dados ou a base de dados.  Para a agenda de cópia de segurança de dados Olá, política de retenção e como toorestore uma base de dados, consulte [restaurar a partir do instantâneo][Restore from snapshot].

## <a name="next-steps"></a>Passos seguintes
A utilização de princípios de design da base de dados boa tornarão mais fácil toomanage as bases de dados no armazém de dados do SQL Server. toolearn mais, head através de toohello [descrição geral do desenvolvimento][Development overview].

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Dimensionar desempenho]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
