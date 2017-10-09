---
title: "Azure escalões de serviço e o desempenho de base de dados SQL | Microsoft Docs"
description: "Compare os escalões de serviço de base de dados SQL e níveis de desempenho das bases de dados e apresentar conjuntos elásticos SQL"
keywords: "opções da base de dados, desempenho da base de dados"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Que opções de desempenho estão disponíveis para uma base de dados do SQL do Azure

[Base de dados SQL do Azure](sql-database-technical-overview.md) oferece quatro camadas de serviços para ambos os único e [agrupados](sql-database-elastic-pool.md) bases de dados. Estes escalões de serviço são: **básico**, **padrão**, **Premium**, e **Premium RS**. Em cada camada de serviço são vários níveis de desempenho ([DTUs](sql-database-what-is-a-dtu.md)) e tamanhos de cargas de trabalho e dados diferentes no toohandle as opções de armazenamento. Níveis de desempenho superiores fornecem computação adicional e recursos de armazenamento foi concebido toodeliver débito de velocidades cada vez e a capacidade. Pode alterar camadas de serviços, níveis de desempenho e armazenamento dinamicamente sem períodos de indisponibilidade. 
- **Básico**, **padrão** e **Premium** escalões de serviço todos os têm um SLA de 99.99%, opções de continuidade do negócio flexíveis, funcionalidades de segurança e faturação por hora de disponibilidade. 
- Olá **Premium RS** camada fornece Olá mesmos níveis de desempenho hello escalão Premium com um SLA reduzido porque é executada com um número inferior de cópias redundantes que uma base de dados no Olá outros escalões de serviço. Por isso, no evento Olá de uma falha de serviço, poderá ser necessário toorecover a base de dados de uma cópia de segurança com segurança tooa desfasamento de 5 minutos.

> [!IMPORTANT]
> Uma base de dados SQL do Azure obtém um conjunto de recursos garantido e Olá esperados características de desempenho da base de dados não são afetadas por qualquer outra base de dados no Azure. 

## <a name="choosing-a-service-tier"></a>Escolher uma camada de serviços
Olá tabela seguinte fornece exemplos de camadas de Olá melhor adequados para cargas de trabalho de aplicação diferente.

| Camada de serviços | Cargas de trabalho de destino |
| :--- | --- |
| **Básica** | Mais adequada para uma base de dados pequena, suportando normalmente uma única operação ativa num determinado momento. Os exemplos incluem bases de dados utilizadas para desenvolvimento ou testes, ou aplicações de dimensionamento pequeno raramente utilizadas. |
| **Standard** |Olá toooption de ir para aplicações em nuvem com requisitos de desempenho de e/s toomedium baixa, suportando várias consultas em simultâneo. Os exemplos incluem aplicações de grupo de trabalho ou Web. |
| **Premium** | Concebido para elevado volume transacional com requisitos de desempenho E/S elevados, suporta muitos utilizadores em simultâneo. Os exemplos são bases de dados que suportam aplicações fundamentais. |
| **Premium RS** | Concebida para cargas de trabalho de e/s intensivas que não necessitem de garantias de disponibilidade mais elevadas Olá. Os exemplos incluem o teste de cargas de trabalho de elevado desempenho ou uma carga de trabalho analítica em que a base de dados de Olá não é sistema Olá de registo. |
|||

Pode criar bases de dados individuais com recursos dedicados dentro de uma camada de serviços em específico [nível de desempenho](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) ou também pode criar bases de dados dentro de um [agrupamento elástico de SQL](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). No agrupamento elástico de SQL Server, os recursos de computação e armazenamento Olá são partilhados entre várias bases de dados dentro de um único servidor lógico. 

Recursos disponíveis para bases de dados individuais são expressas em termos de unidades de transação de base de dados (DTUs) e recursos para um conjuntos elásticos do SQL Server são expressas em termos de unidades de transação de base de dados elásticas (eDTUs). Para mais informações sobre as DTUs e eDTUs, consulte [quais são as DTUs e eDTUs?](sql-database-what-is-a-dtu.md).

toodecide a camada de serviço, comece por determinar funcionalidades de base de dados mínimo Olá que precisa de:

| **Funcionalidades do escalão de serviço** | **Básica** | **Standard** | **Premium** | **Premium RS**|
| :-- | --: | --: | --: | --: |
| Tamanho máximo de bases de dados único | 2GB | 250 GB | 4 TB *  | 500 GB  |
| Tamanho máximo do conjunto elástico | 156 GB | 2,9 TB | 4 TB * | 750 GB |
| Tamanho máximo da base de dados num agrupamento elástico | 2GB | 250 GB | 500 GB | 500 GB |
| Número máximo de bases de dados por agrupamento | 500  | 500 | 100 | 100 |
| Máximo base de dados individual DTUs | 5 | 100 | 4000 | 1000 |
| Máximas DTUs por base de dados num agrupamento elástico | 5 | 3000 | 4000 | 1000 |
| Período de retenção de cópias de segurança de base de dados | 7 dias | 35 dias | 35 dias | 35 dias |
||||||

> [!IMPORTANT]
> Armazenamento de cópia de segurança too4 TB está atualmente disponível na Olá seguintes regiões: East2 nos, EUA oeste, Virginia us dos EUA, Europa Ocidental, Alemanha Central, Sul Oriental, leste do Japão, leste da Austrália, Canadá Central e Canadá Leste. Consulte [limitações atuais 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Depois de ter determinado a camada de serviço apropriado Olá, são nível de desempenho de Olá toodetermine pronto (Olá o número de DTUs) e a quantidade de armazenamento Olá da base de dados de Olá. 

- Olá S2 e S3 níveis de desempenho no Olá **padrão** camada são, muitas vezes, um ponto de partida. 
- Para bases de dados com requisitos de CPU ou e/s elevados, Olá níveis de desempenho no Olá **Premium** camada são o ponto de partida direita Olá. 
- Olá **Premium** camada oferece mais CPU e é iniciado em 10x mais e/s em comparação com toohello nível de desempenho mais elevado numa Olá **padrão** camada.
- Olá **PremiumRS** camada oferece um desempenho Olá de Olá **Premium** camada um custo mais baixo, mas com um SLA reduzido.

> [!IMPORTANT]
> Olá revisão [conjuntos elásticos SQL](sql-database-elastic-pool.md) tópico para Olá obter detalhes sobre o agrupamento de bases de dados em elástico SQL agrupamentos de recursos de computação e armazenamento tooshare. resto Olá este tópico centra-se nos escalões de serviço e níveis de desempenho das bases de dados.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Camadas de serviços de bases de dados individuais e níveis de desempenho
Para bases de dados individuais, existem vários níveis de desempenho e quantidades de armazenamento em cada camada de serviço. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Aumentar ou reduzir verticalmente uma base de dados individual

Após escolher inicialmente um escalão de serviço e nível de desempenho, pode aumentar ou reduzir verticalmente e de forma dinâmica uma base de dados individual com base na experiência real.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Alterar Olá camada e/ou de desempenho de nível de serviço de uma base de dados cria uma réplica da base de dados original Olá ao nível de desempenho novo Olá e, em seguida, passa ligações toohello réplica. Não se tenha perdido nenhum dado durante este processo, mas durante Olá breve neste momento quando iremos comutador através de réplica toohello, base de dados do ligações toohello estiverem desativados, pelo que alguns transações em trânsito poderão ser revertidas. período de Olá de tempo para mudar Olá varia, mas é, geralmente, é de 4 segundos menos de 30 segundos 99% de tempo de Olá. Se existirem grande número de transações em trânsito em ligações de momento Olá estão desativadas, hello período de tempo para mudar Olá pode ser maior.  

duração de Olá do processo de dimensionamento todo Olá depende de ambos os tamanho Olá e escalão de serviço da Olá da base de dados antes e depois de alterar Olá. Por exemplo, uma base de dados de 250 GB que está a alterar para, de, ou dentro de um escalão Standard, deverá ser concluída no prazo de seis horas. Para uma base de dados de Olá mesmo tamanho que a alteração níveis de desempenho na camada de serviço Olá Premium deve ser concluído dentro de 3 horas.

> [!TIP]
> toocheck Estado Olá uma base de dados do SQL Server em curso operação de dimensionamento, pode utilizar Olá seguinte consulta: ```select * from sys.dm_operation_status```.
>

* Se estiver a atualizar tooa superior camada ou desempenho de nível de serviço, o tamanho de base de dados máximo Olá não aumenta a menos que especifique explicitamente um maior tamanho máximo.
* toodowngrade uma base de dados, a base de dados de Olá tem de ser inferior a Olá tamanho máximo permitido de camada de serviço de destino Olá. 
* Ao atualizar a base de dados com [georreplicação](sql-database-geo-replication-portal.md) ativada, atualize o escalão de desempenho pretendidos de toohello de bases de dados secundária antes de atualizar a base de dados primária do Olá (orientações gerais). Quando atualizar tooa edição diferente ugrading Olá base de dados secundária primeiro é necessário. 
* Quando a desatualização de uma base de dados com [georreplicação](sql-database-geo-replication-portal.md) ativada, mudar a respetiva camada de desempenho pretendidos toohello bases de dados primária antes desatualização de base de dados secundária do Olá (orientações gerais). Quando desatualização tooa edição diferente desatualização Olá base de dados primária primeiro é necessário. 

* Olá restauro ofertas de serviço são diferentes para Olá vários escalões de serviço. Se estiver a desatualização toohello **básico** camada, terá de um período de retenção de cópias de segurança inferior - consulte [cópias de segurança do Azure SQL da base de dados](sql-database-automated-backups.md).
* Propriedades da nova base de dados de Olá Olá não são aplicadas até que as alterações de Olá estiverem concluídas.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>Limitações atuais das bases de dados P11 e P15 com maxsize de 4 TB

Um tamanho máximo de 4 TB para P11 e P15 base de dados é suportado em algumas regiões (conforme discutidos anteriormente). Olá seguintes considerações e limitações aplicam-se tooP11 e P15 bases de dados com maxsize de 4 TB:

- Se escolher a opção de maxsize de 4 TB Olá ao criar uma base de dados (utilizando um valor de 4096 GB ou de 4 TB), Olá criar comando falha com um erro se a base de dados de Olá é aprovisionado numa região não suportada.
- Para existentes P11 P15 bases de dados e localizados das regiões Olá suportada, pode aumentar Olá maxsize armazenamento too4 TB. Isto pode ser verificado ao utilizar Olá [SELECIONE DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) ou através da inspeção de tamanho de base de dados de Olá em Olá portal do Azure. Atualizar um P11 existente ou P15 base de dados só pode ser efetuada por um início de sessão principal ao nível do servidor ou por membros da função de base de dados do Olá dbmanager. 
- Se for executada uma operação de atualização numa configuração de Olá região suportada é atualizada imediatamente. base de dados de Olá permanece online durante o processo de atualização de Olá. No entanto, não é possível utilizar Olá completa 4 TB de armazenamento até que os ficheiros de base de dados real de Olá tem sido atualizado toohello maxsize de novo. Olá período de tempo necessária depende após tamanho Olá da base de dados de Olá a ser atualizado.  
- Quando criar ou atualizar uma base de dados P11 ou P15, apenas pode escolher entre 1 TB e 4 TB maxsize. Tamanhos de armazenamento intermédio não são atualmente suportados. Ao criar um P11/P15, é pré-seleccionado a opção de armazenamento Olá predefinida de 1 TB. Para bases de dados localizados dos regiões Olá suportada, pode aumentar Olá armazenamento too4TB máximo para uma base de dados nova ou existente. Para todas as outras regiões, o tamanho máximo não pode ser aumentado superiores a 1 TB. preços Olá não se altera quando seleciona 4 TB de armazenamento incluído.
- Olá maxsize de base de dados de 4 TB não pode ser alterada too1 TB mesmo armazenamento real Olá utilizado é inferior a 1 TB. Assim, não é possível mudar um tooa P11 - 4 TB/P15 - 4 TB P11 - 1 TB/P15 - 1 TB ou de uma camada de desempenho inferior por exemplo, tooP1-P6) até que estamos a proporcionar opções de armazenamento adicional para o resto Olá Olá escalões de desempenho. Esta restrição também se aplica toohello restauro e cenários de cópia, incluindo o ponto no tempo, georrestauro, longo-prazo-cópia de segurança-retenção e a cópia da base de dados. Depois de uma base de dados está configurado com a opção de 4 TB Olá, todas as operações de restauro desta base de dados devem ser executadas para um P11/P15 com 4 TB maxsize.
- Quando criar ou atualizar uma base de dados P11/P15 numa região não suportada, hello criar ou a operação de atualização falha com Olá seguir a mensagem de erro: **P11 e P15 base de dados com cópia de segurança too4TB de armazenamento estão disponíveis no East2 nos, EUA oeste, EUA us Virginia, Europa Ocidental, Central na Alemanha, Sudeste asiático, leste do Japão, leste da Austrália, Canadá Central e Canadá Leste.**
- Para cenários de replicação geográfica activa:
   - Configurar uma relação de replicação geográfica: se a base de dados primária Olá for P11 ou P15, Olá secondary(ies) também tem de ser P11 ou P15; os escalões de desempenho inferiores são rejeitados como bases de dados secundárias, uma vez que não são capazes de oferecer suporte 4 TB.
   - Atualizar Olá base de dados primária numa relação de replicação geográfica: alterar Olá maxsize too4 TB numa base de dados primária aciona Olá mesmo alterados na base de dados secundária Olá. Tem de ser efetuada com êxito para alteração Olá em efeito de tootake primário Olá ambas as atualizações. Limitações de região para a opção de 4TB Olá aplicam (consultar acima). Se Olá secundário está numa região que não suporta 4 TB, Olá principal não está atualizado.
- Não é suportada com o serviço de importação/exportação Olá para carregar as bases de dados P11 - 4TB/P15 - 4TB. Utilizar SqlPackage.exe demasiado[importar](sql-database-import.md) e [exportar](sql-database-export.md) dados.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>Gerir os escalões de serviço de base de dados individual e níveis de desempenho utilizando Olá portal do Azure

Olá, tooset ou altere a camada de serviço, nível de desempenho ou a quantidade de armazenamento para uma nova ou existente SQL database do Azure utilizando Olá portal do Azure, abra Olá **Configurar desempenho** janela para a base de dados clicando  **O escalão de preço (dimensionamento DTUs)** - conforme mostrado na seguinte captura de ecrã de Olá. 

- Definir ou alterar o escalão de serviço de Olá, selecionando a camada de serviços de Olá para a carga de trabalho. 
- Definir ou alterar o nível de desempenho de Olá (**DTUs**) dentro de uma camada de serviços utilizando Olá **DTU** controlo de deslize.
- Definir ou alterar a quantidade de armazenamento Olá por nível de desempenho de Olá utilizando Olá **armazenamento** controlo de deslize. 

  ![Configurar o nível de desempenho e o escalão de serviço](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Reveja [limitações atuais das bases de dados P11 e P15 com 4 TB maxsize](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize) ao selecionar uma camada de serviço P11 ou P15.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Gerir os escalões de serviço de base de dados individual e níveis de desempenho com o PowerShell

tooset ou alterar camadas de serviços de bases de dados SQL do Azure, níveis de desempenho e a quantidade de armazenamento com o PowerShell, utilizam Olá os seguintes cmdlets do PowerShell. Se precisar de tooinstall ou atualizar o PowerShell, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps). 

| Cmdlet | Descrição |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Cria uma base de dados |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtém um ou mais bases de dados|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Define as propriedades para uma base de dados ou move de uma base de dados existente para um conjunto elástico|


> [!TIP]
> Para um script de exemplo do PowerShell que monitoriza Olá desempenho das métricas da base de dados, dimensiona este nível de desempenho superior tooa e cria uma regra de alerta num Olá métricas de desempenho, consulte [monitorizar e dimensionar um único SQL da base de dados a utilizar PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>Gerir os escalões de serviço de base de dados individual e níveis de desempenho utilizando Olá CLI do Azure

tooset ou alterar camadas de serviços de bases de dados SQL do Azure, níveis de desempenho e a quantidade de armazenamento utilizando Olá CLI do Azure, utilizam o seguinte de Olá [SQL Database do Azure CLI](/cli/azure/sql/db) comandos. Olá utilize [nuvem Shell](/azure/cloud-shell/overview) toorun Olá CLI no seu browser, ou [instalar](/cli/azure/install-azure-cli) -lo no macOS, Linux ou do Windows. Para criar e gerir conjuntos elásticos SQL, consulte [conjuntos elásticos](sql-database-elastic-pool.md).

| Cmdlet | Descrição |
| --- | --- |
|[Criar BD do sql AZ](/cli/azure/sql/db#create) |Cria uma base de dados|
|[lista de BD do SQL Server AZ](/cli/azure/sql/db#list)|Apresenta uma lista de todas as bases de dados e os armazéns de dados num servidor, ou todas as bases de dados num agrupamento elástico|
|[base de dados de sql AZ lista-edições](/cli/azure/sql/db#list-editions)|Apresenta uma lista de serviços disponíveis objetivos e limites de armazenamento|
|[base de dados de sql AZ lista-utilizações](/cli/azure/sql/db#list-usages)|Devolve as utilizações de base de dados|
|[Mostrar de BD do SQL Server AZ](/cli/azure/sql/db#show)|Obtém um armazém de dados ou base de dados|
|[atualização de base de dados do sql AZ](/cli/azure/sql/db#update)|Atualizações de uma base de dados|

> [!TIP]
> Para um script de exemplo da CLI do Azure que dimensiona um nível de desempenho diferentes do tooa de base de dados SQL do Azure único depois de consultar as informações de tamanho da base de dados de Olá Olá, consulte [toomonitor CLI de utilização e o dimensionamento uma única base de dados do SQL Server](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Gerir os escalões de serviço de base de dados individual e níveis de desempenho com o Transact-SQL

tooset ou alterar camadas de serviços de bases de dados SQL do Azure, níveis de desempenho e a quantidade de armazenamento com o Transact-SQL, utilizam Olá os seguintes comandos T-SQL. Pode emitir estes comandos utilizando Olá portal do Azure, [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), ou qualquer outro programa que pode ligar o servidor de base de dados do Azure SQL tooan e passar o Transact-SQL comandos. 

| Comando | Descrição |
| --- | --- |
|[Criar base de dados (SQL Database do Azure)](/sql/t-sql/statements/create-database-azure-sql-database)|Cria uma nova base de dados. Tem de ser ligado toohello base de dados mestra toocreate uma nova base de dados.|
| [Falha de ALTER DATABASE (base de dados SQL do Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifica uma base de dados SQL do Azure. |
|[sys.database_service_objectives (SQL Database do Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Devolve Olá edition (camada de serviço), o objetivo de serviço (escalão de preço) e o nome do conjunto elástico, se existir, para uma base de dados SQL do Azure ou um Azure SQL Data Warehouse. Se tiver sessão iniciada no toohello base de dados mestra um servidor de base de dados do Azure SQL, devolve informações sobre todas as bases de dados. Para o Azure SQL Data Warehouse, tem de ser a base de dados mestra toohello ligado.|
|[sys.database_usage (SQL Database do Azure)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Apresenta o número de Olá, tipo e a duração das bases de dados num servidor SQL Database do Azure.|

Olá exemplo seguinte mostra Olá maxsize a ser alterada através do comando ALTER DATABASE Olá:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Gerir bases de dados individuais utilizando Olá REST API

tooset ou alterar camadas de serviços de bases de dados SQL do Azure, níveis de desempenho e a quantidade de armazenamento utilizando Olá REST API, consulte [API de REST de base de dados do Azure SQL](/rest/api/sql/).

## <a name="next-steps"></a>Passos seguintes

* Saiba mais sobre [DTUs](sql-database-what-is-a-dtu.md).
* toolearn sobre a monitorização de utilização, consulte [monitorização e a otimização de desempenho](sql-database-troubleshoot-performance.md).

