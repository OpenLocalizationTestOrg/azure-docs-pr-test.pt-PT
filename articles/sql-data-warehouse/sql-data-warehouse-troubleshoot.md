---
title: aaaTroubleshooting Azure SQL Data Warehouse | Microsoft Docs
description: "Resolução de problemas do armazém de dados SQL do Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Resolução de problemas do armazém de dados SQL do Azure
Esta lista de tópico Olá algumas das perguntas de resolução de problemas mais comuns recebemos dos nossos clientes.

## <a name="connecting"></a>A ligação
| Problema | Resolução |
|:--- |:--- |
| Falha ao iniciar sessão para o utilizador 'Início de sessão do NT AUTHORITY\ANONYMOUS'. (Microsoft SQL Server, erro: 18456) |Este erro ocorre quando um utilizador do AAD tenta tooconnect toohello principal da base de dados, mas não tem um utilizador no mestre.  toocorrect este problema, especifique Olá desejar tempo de ligação de tooat tooconnect ou adicionar Olá utilizador toohello base de dados mestra do SQL Data Warehouse.  Consulte [descrição geral de segurança] [ Security overview] artigo para obter mais detalhes. |
| servidor de Olá principal "MyUserName" não é possível tooaccess Olá base de dados "master" no contexto de segurança atual Olá. Não é possível abrir a base de dados do utilizador predefinida. Falha ao iniciar sessão. Falha ao iniciar sessão para o utilizador 'MyUserName'. (Microsoft SQL Server, erro: 916) |Este erro ocorre quando um utilizador do AAD tenta tooconnect toohello principal da base de dados, mas não tem um utilizador no mestre.  toocorrect este problema, especifique Olá desejar tempo de ligação de tooat tooconnect ou adicionar Olá utilizador toohello base de dados mestra do SQL Data Warehouse.  Consulte [descrição geral de segurança] [ Security overview] artigo para obter mais detalhes. |
| Erro CTAIP |Este erro pode ocorrer quando tiver sido criado um início de sessão no Olá servidor mestre base de dados SQL, mas não se encontra na base de dados do SQL Data Warehouse Olá.  Se ocorrer este erro, observe Olá [descrição geral de segurança] [ Security overview] artigo.  Este artigo explica como toocreate criar um início de sessão e o utilizador no mestre e, em seguida, como toocreate um utilizador no Olá base de dados do armazém de dados do SQL Server. |
| Bloqueado pela Firewall |Bases de dados SQL do Azure estão protegidos pelo servidor e base de dados tooensure firewalls nível conhecido apenas endereços IP têm de base de dados do access tooa. firewalls Olá são seguras por predefinição, o que significa que, tem de ativar explicitamente e endereço IP ou intervalo de endereços antes de poder ligar.  tooconfigure a firewall para acesso, siga Olá passos [configurar o acesso ao servidor de firewall para o IP de cliente] [ Configure server firewall access for your client IP] no Olá [aprovisionamento instruções] [Provisioning instructions]. |
| Não é possível estabelecer ligação com a ferramenta ou controladores |O SQL Data Warehouse recomenda a utilização [SSMS][SSMS], [SSDT para Visual Studio][SSDT for Visual Studio], ou [sqlcmd] [ sqlcmd] tooquery os dados. Para obter mais detalhes sobre controladores e tooSQL ligação do armazém de dados, consulte [controladores para o Azure SQL Data Warehouse] [ Drivers for Azure SQL Data Warehouse] e [ligar tooAzure SQL Data Warehouse] [ Connect tooAzure SQL Data Warehouse] artigos. |

## <a name="tools"></a>Ferramentas
| Problema | Resolução |
|:--- |:--- |
| Explorador de objetos do Visual Studio está em falta utilizadores AAD |Este é um problema conhecido.  Como solução, ver os utilizadores Olá [sys.database_principals][sys.database_principals].  Consulte [tooAzure autenticação SQL Data Warehouse] [ Authentication tooAzure SQL Data Warehouse] toolearn mais sobre como utilizar o Azure Active Directory com o SQL Data Warehouse. |
|Manual de scripting, utilizando o Assistente de scripting Olá ou ligação através do SSMS estiver lentos, bloqueados ou produção erros| Certifique-se que os utilizadores foram criados na base de dados mestra Olá. Nas opções de scripts, certifique-se também que edição do motor de Olá está definida como "Microsoft Azure SQL Data Warehouse Edition" e tipo de motor é "Microsoft SQL Database do Azure".|

## <a name="performance"></a>Desempenho
| Problema | Resolução |
|:--- |:--- |
| Resolução de problemas de desempenho de consulta |Se estiver a tentar tootroubleshoot uma consulta específica, começar a utilizar [Learning como toomonitor as suas consultas][Learning how toomonitor your queries]. |
| Desempenho das consultas fraco e planos é frequentemente um resultado de estatísticas em falta |Olá causa mais comum fraco desempenho é a falta de estatísticas das tabelas.  Consulte [manter as estatísticas da tabela] [ Statistics] para obter detalhes sobre como toocreate estatísticas e porquê forem críticos tooyour desempenho. |
| Simultaneidade baixa / colocados em fila de consultas |Noções sobre [gestão da carga de trabalho] [ Workload management] é importante na ordem toounderstand como toobalance a atribuição de memória com a simultaneidade. |
| Como tooimplement melhores práticas |Olá melhor local toostart toolearn formas tooimprove desempenho das consultas é [melhores práticas do SQL Data Warehouse] [ SQL Data Warehouse best practices] artigo. |
| Como desempenho tooimprove com dimensionamento |Por vezes, o desempenho da tooimproving Olá solução é toosimply adicionar mais computação consultas tooyour energia [dimensionamento do SQL Data Warehouse][Scaling your SQL Data Warehouse]. |
| Desempenho das consultas fraco como resultado de qualidade de índice fraco |Consultas de algumas vezes podem slowdown porque [qualidade de índice columnstore fraco][Poor columnstore index quality].  Consulte este artigo para obter mais informações e como demasiado[reconstrução indexa qualidade de segmento de tooimprove][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Gestão do sistema
| Problema | Resolução |
|:--- |:--- |
| Tarifas de mensagens 40847: Não foi possível efetuar a operação de Olá porque o servidor iria exceder Olá permitido quota de unidade de transação de base de dados de 45000. |Reduza Olá [DWU] [ DWU] da base de dados de Olá que está a tentar toocreate ou [pedir um aumento de quota][request a quota increase]. |
| Investigar a utilização de espaço |Consulte [tabela tamanhos] [ Table sizes] toounderstand de utilização do espaço Olá do seu sistema. |
| Ajudar na gestão de tabelas |Consulte Olá [descrição geral da tabela] [ Overview] artigo para obter ajuda com a gerir as tabelas.  Este artigo também inclui ligações para tópicos mais detalhadas sobre como [tipos de dados de tabela][Data types], [distribuir uma tabela][Distribute], [Uma tabela de indexação][Index], [uma tabela de criação de partições][Partition], [manter as estatísticas da tabela] [ Statistics] e [tabelas temporárias][Temporary]. |
|Barra de progresso de encriptação (TDE) transparente de dados não está a atualizar em Olá Portal do Azure|Pode ver o estado Olá TDE através de [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>Polybase
| Problema | Resolução |
|:--- |:--- |
| Carga falha devido à grande linhas |Atualmente o suporte de linha grande não está disponível para o Polybase.  Isto significa que se a tabela contiver varchar (Max), nvarchar (Max) ou varbinary (Max), as tabelas externas não podem ser utilizado tooload os dados.  Cargas grandes linhas está atualmente só é suportada através do Azure Data Factory (com o BCP), do Azure Stream Analytics, SSIS, BCP ou Olá classe de .NET SQLBulkCopy. Suporte do PolyBase linhas grande será adicionado numa versão futura. |
| está a falhar carga BCP da tabela com o tipo de dados de máx. |Não há um problema conhecido que requer que varchar (Max), nvarchar (Max) ou varbinary (Max) ser colocados no fim de Olá da tabela de Olá em alguns cenários.  Tente mover o fim de toohello do máx. colunas da tabela de Olá. |

## <a name="differences-from-sql-database"></a>Diferenças a partir da base de dados SQL
| Problema | Resolução |
|:--- |:--- |
| Funcionalidades de base de dados SQL não suportadas |Consulte [tabela funcionalidades não suportadas][Unsupported table features]. |
| Tipos de dados de base de dados SQL não suportados |Consulte [não suportada de tipos de dados][Unsupported data types]. |
| ELIMINAR e limitações de ATUALIZAÇÃO |Consulte [soluções de ATUALIZAÇÃO][UPDATE workarounds], [eliminar soluções] [ DELETE workarounds] e [toowork CTAS utilizar à volta de ATUALIZAÇÃO não suportada e Sintaxe de eliminação][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| Instrução MERGE não é suportada |Consulte [soluções de intercalação][MERGE workarounds]. |
| Limitações do procedimento armazenado |Consulte [armazenados limitações do procedimento] [ Stored procedure limitations] toounderstand algumas das limitações de Olá de procedimentos armazenados. |
| UDFs não suportam instruções SELECT |Esta é uma limitação atual do nosso UDFs.  Consulte [CREATE FUNCTION] [ CREATE FUNCTION] para sintaxe Olá suportamos. |

## <a name="next-steps"></a>Passos seguintes
Se estiver foram toofind não é possível um problema de tooyour solução superior, estão aqui alguns outros recursos, pode tentar.

* [Blogues]
* [Pedidos de funcionalidades]
* [Vídeos]
* [Blogues da equipa CAT]
* [Criar pedido de suporte]
* [Fórum do MSDN]
* [Fórum do Stack Overflow]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Criar pedido de suporte]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Blogues]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogues da equipa CAT]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Pedidos de funcionalidades]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Fórum do MSDN]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Fórum do Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Vídeos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
