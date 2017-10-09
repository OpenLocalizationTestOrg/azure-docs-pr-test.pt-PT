---
title: "aaaMigrate armazenamento toopremium do armazém de dados existentes do Azure | Microsoft Docs"
description: "Instruções para migrar um armazenamento toopremium do armazém de dados existente"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Migrar o armazenamento de toopremium do armazém de dados
O Azure SQL Data Warehouse recentemente adicionadas [armazenamento premium para previsão de desempenho superior][premium storage for greater performance predictability]. Os dados existentes armazéns atualmente no armazenamento standard podem agora ser migradas toopremium armazenamento. Pode tirar partido da migração automática, ou se preferir toocontrol quando toomigrate (que envolvem algum período de indisponibilidade), pode fazê-lo Olá migração por si.

Se tiver mais do que um armazém de dados, utilize Olá [agenda migração automática] [ automatic migration schedule] toodetermine quando também será migrada.

## <a name="determine-storage-type"></a>Determinar o tipo de armazenamento
Se tiver criado um armazém de dados antes de Olá seguir datas, está atualmente a utilizar armazenamento standard.

| **Região** | **Armazém de dados criado antes desta data** |
|:--- |:--- |
| Leste da Austrália |Armazenamento Premium ainda não está disponível |
| Leste da China |1 de Novembro de 2016 |
| China Norte |1 de Novembro de 2016 |
| Alemanha Central |1 de Novembro de 2016 |
| Alemanha Nordeste |1 de Novembro de 2016 |
| Índia Ocidental |Armazenamento Premium ainda não está disponível |
| Oeste do Japão |Armazenamento Premium ainda não está disponível |
| EUA Centro-Norte |10 de Novembro de 2016 |

## <a name="automatic-migration-details"></a>Detalhes de migração automática
Por predefinição, iremos migrar a base de dados para si entre as 18:00:00 e 6:00:00 na sua região local durante Olá [agenda migração automática][automatic migration schedule]. O armazém de dados existente ficará inutilizável durante a migração de Olá. migração de Olá irá demorar, aproximadamente, uma hora por com vários terabytes de armazenamento do armazém de dados. Não será cobrada durante qualquer parte da migração automática Olá.

> [!NOTE]
> Quando Olá migração estiver concluída, o armazém de dados será novamente online e utilizável.
>
>

Microsoft está a demorar Olá os seguintes passos toocomplete Olá, a migração (estes não requerem qualquer envolvimento da sua parte). Neste exemplo, imagine que o armazém de dados existente no armazenamento standard atualmente com o nome "MyDW."

1. Microsoft muda o nome "MyDW" demasiado "MyDW_DO_NOT_USE_ [Timestamp]".
2. Microsoft interrompe "MyDW_DO_NOT_USE_ [Timestamp]". Durante este período, foi efetuada uma cópia de segurança. Poderá ver várias coloca em pausa e retoma se podemos encontre quaisquer problemas durante este processo.
3. Microsoft cria um novo armazém de dados com o nome "MyDW" no armazenamento premium da cópia de segurança de Olá executada no passo 2. "MyDW" não será apresentado até após a conclusão do restauro Olá.
4. Após a conclusão do restauro Olá, "MyDW" devolve toohello mesmos dados do armazém de unidades e de estado (em pausa ou Active Directory) que se encontravam antes da migração de Olá.
5. Depois de concluída a migração de Olá, a Microsoft elimina "MyDW_DO_NOT_USE_ [Timestamp]".

> [!NOTE]
> Olá seguintes definições não passa como parte da migração de Olá:
>
> * Auditoria ao nível da base de dados de Olá tem toobe reativada.
> * Regras de firewall ao nível da base de dados de Olá necessário toobe adicionado novamente. Regras de firewall ao nível do servidor de Olá não são afetadas.
>
>

### <a name="automatic-migration-schedule"></a>Agenda de migração automática
Migrações automáticas ocorrerem entre as 18:00:00 e 6:00:00 (hora local por região) durante Olá seguinte agenda de indisponibilidade.

| **Região** | **Data de início estimado** | **Data de fim estimado** |
|:--- |:--- |:--- |
| Leste da Austrália |Não determinar ainda |Não determinar ainda |
| Leste da China |9 de Janeiro de 2017 |13 de Janeiro de 2017 |
| China Norte |9 de Janeiro de 2017 |13 de Janeiro de 2017 |
| Alemanha Central |9 de Janeiro de 2017 |13 de Janeiro de 2017 |
| Alemanha Nordeste |9 de Janeiro de 2017 |13 de Janeiro de 2017 |
| Índia Ocidental |Não determinar ainda |Não determinar ainda |
| Oeste do Japão |Não determinar ainda |Não determinar ainda |
| EUA Centro-Norte |9 de Janeiro de 2017 |13 de Janeiro de 2017 |

## <a name="self-migration-toopremium-storage"></a>Armazenamento de toopremium migração automática
Se pretender toocontrol quando o período de indisponibilidade irá ocorrer, pode utilizar Olá seguindo os passos toomigrate um armazém de dados existente do armazenamento de toopremium de armazenamento standard. Se escolher esta opção, tem de Concluir migração automática Olá antes do início da migração automática Olá nessa região. Isto garante que evitar quaisquer risco da migração automática Olá provocando um conflito (consulte toohello [agenda migração automática][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Instruções de migração automática
toomigrate os dados do armazém de si próprio, utilizam Olá cópia de segurança e restaurar as funcionalidades. Olá restauro parte migração Olá é esperado tootake aproximadamente uma hora por com vários terabytes de armazenamento do armazém de dados. Se quiser Olá tookeep mesmo nome após a conclusão da migração, siga Olá [toorename passos durante a migração][steps toorename during migration].

1. [Colocar em pausa] [ Pause] o armazém de dados. Isto leva uma cópia de segurança automática.
2. [Restaurar] [ Restore] do seu instantâneo mais recente.
3. Elimine o armazém de dados existente no armazenamento standard. **Se falharem toodo neste passo, será cobrada para ambos os armazéns de dados.**

> [!NOTE]
> Olá seguintes definições não passa como parte da migração de Olá:
>
> * Auditoria ao nível da base de dados de Olá tem toobe reativada.
> * Regras de firewall ao nível da base de dados de Olá necessário toobe adicionado novamente. Regras de firewall ao nível do servidor de Olá não são afetadas.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Mudar o nome do armazém de dados durante a migração (opcional)
Duas bases de dados no mesmo servidor lógico não pode ter de Olá Olá o mesmo nome. Armazém de dados do SQL Server suporta agora Olá capacidade toorename um armazém de dados.

Neste exemplo, imagine que o armazém de dados existente no armazenamento standard atualmente com o nome "MyDW."

1. Mudar o nome "MyDW" utilizando Olá seguir o comando ALTER DATABASE. (Neste exemplo, iremos irá mude o nome "MyDW_BeforeMigration.")  Este comando para todas as transações existentes e tem de ser efetuado no Olá toosucceed de base de dados mestra.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Colocar em pausa] [ Pause] "MyDW_BeforeMigration." Isto leva uma cópia de segurança automática.
3. [Restaurar] [ Restore] do seu instantâneo mais recente uma nova base de dados com o nome de Olá que utilizado toobe (por exemplo, "MyDW").
4. Eliminar "MyDW_BeforeMigration." **Se falharem toodo neste passo, será cobrada para ambos os armazéns de dados.**


## <a name="next-steps"></a>Passos seguintes
Com Olá alterar toopremium armazenamento, tem também um aumento do número de ficheiros de blob de base de dados na arquitetura subjacente do Olá do seu armazém de dados. benefícios de desempenho de Olá toomaximize desta alteração, reconstruir os índices columnstore em cluster utilizando Olá script a seguir. script de Olá funciona forçando alguns dos seus existente blobs adicionais de toohello de dados. Se não efetuar qualquer ação, dados de Olá naturalmente redistribuir ao longo do tempo como carregados mais dados para as tabelas.

**Pré-requisitos:**

- Hello do armazém de dados deve ser executada com unidades de armazém de 1000 dados ou superior (consulte [poder de computação de escala][scale compute power]).
- Olá utilizador a executar o script de Olá deve estar no Olá [mediumrc função] [ mediumrc role] ou superior. tooadd uma função de utilizador de toothis, execute o seguinte Olá:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Se tiver quaisquer problemas com o armazém de dados, [criar um pedido de suporte] [ create a support ticket] e de referência "armazenamento de toopremium de migração" como uma causa possível Olá.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
