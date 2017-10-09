---
title: "Memória aaaIn OLTP melhora o desempenho do SQL Server txn | Microsoft Docs"
description: "Adopt dentro da memória OLTP tooimprove transacional desempenho uma base de dados existente do SQL Server."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>Utilização de memória OLTP tooimprove o desempenho da aplicação na base de dados do SQL Server
[OLTP na memória](sql-database-in-memory.md) podem ser utilizados tooimprove Olá desempenho do processamento de transações, a ingestão de dados e cenários de dados transitório, [Premium](sql-database-service-tiers.md) bases de dados do Azure SQL sem aumentar Olá escalão de preço. 

> [!NOTE] 
> Saiba como [quórum duplica carga de trabalho de chave da base de dados ao reduzirem DTU por 70% com base de dados SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)


Siga estes passos tooadopt OLTP dentro da memória na base de dados existente.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Passo 1: Certifique-se de que está a utilizar uma base de dados Premium
OLTP dentro da memória só é suportado em bases de dados Premium. Dentro da memória é suportada se Olá devolveu o resultado é 1 (não 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* representa *Alpine processamento de transação*



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>Passo 2: Identificar objetos toomigrate tooIn memória OLTP
SSMS inclui um **descrição geral de análise do desempenho de transação** relatório que pode executar em relação a uma base de dados com uma carga de trabalho ativa. relatório de Olá identifica as tabelas e procedimentos armazenados que sejam candidatas para a migração tooIn memória OLTP.

No SSMS, relatório de Olá toogenerate:

* No Olá **Object Explorer**, clique com o botão direito do nó de base de dados.
* Clique em **relatórios** > **relatórios padrão** > **descrição geral de análise do desempenho de transação**.

Para obter mais informações, consulte [Determining se uma tabela ou armazenados procedimento deve ser convertidos serem OLTP de memória tooIn](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Passo 3: Criar uma base de dados de teste comparável
Suponhamos Olá relatório indica que a base de dados tem uma tabela que seria beneficiam de ser convertida tabela com otimização de memória de tooa. Recomendamos que teste primeiro indicação de Olá tooconfirm ao testar.

Precisa de uma cópia de teste da sua base de dados de produção. Olá base de dados de teste deve ser em Olá service mesmo nível de como a base de dados de produção.

tooease testar, otimizar a base de dados de teste da seguinte forma:

1. Liga a base de dados de teste de toohello, utilizando o SSMS.
2. tooavoid necessitar Olá opção WITH (SNAPSHOT) em consultas, defina a opção de base de dados de Olá conforme mostrado no Olá seguinte declaração de T-SQL:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Passo 4: Migrar tabelas
Tem de criar e preencher uma cópia com otimização de memória da tabela de Olá pretende tootest. Pode criá-la utilizando:

* Olá à mão Assistente de otimização de memória no SSMS.
* Manual de T-SQL.

#### <a name="memory-optimization-wizard-in-ssms"></a>Assistente de otimização de memória no SSMS
toouse esta opção de migração:

1. Ligar a base de dados de teste de toohello com o SSMS.
2. No Olá **Object Explorer**, faça duplo clique na tabela de Olá e, em seguida, clique em **Advisor de otimização de memória**.
   
   * Olá **tabela memória otimizador Advisor** é apresentado o assistente.
3. No Assistente de Olá, clique em **validação de migração** (ou Olá **seguinte** botão) toosee se a tabela de Olá tem quaisquer funcionalidades não suportadas que não são suportadas em tabelas com otimização de memória. Para obter mais informações, consulte:
   
   * Olá *lista de verificação de otimização de memória* no [Advisor de otimização de memória](http://msdn.microsoft.com/library/dn284308.aspx).
   * [As construções de Transact-SQL não suportadas pelo OLTP na memória](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Migrar tooIn memória OLTP](http://msdn.microsoft.com/library/dn247639.aspx).
4. Se a tabela de Olá não tem nenhum funcionalidades não suportadas, advisor de Olá pode executar esquema real Olá e migração de dados para si.

#### <a name="manual-t-sql"></a>Manual de T-SQL
toouse esta opção de migração:

1. Liga a base de dados de teste de tooyour utilizando o SSMS (ou um utilitário semelhante).
2. Obter o script T-SQL completado Olá para a tabela e seus índices.
   
   * No SSMS, clique no nó da tabela.
   * Clique em **Script tabela como** > **criar para** > **nova janela de consulta**.
3. Na janela de script de Olá, adicionar WITH (MEMORY_OPTIMIZED = ON) toohello instrução CREATE TABLE.
4. Se existir um índice em cluster, alterá-la tooNONCLUSTERED.
5. Mudar o nome da tabela existente Olá utilizando SP_RENAME.
6. Crie Olá nova com otimização de memória cópia da tabela de Olá executando o script de CREATE TABLE editado.
7. Copie a tabela de otimização de memória do Olá dados tooyour utilizando INSERT... SELECIONE * PARA:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Passo 5 (opcional): Migrar procedimentos armazenados
funcionalidade de memória de Olá também pode modificar um procedimento armazenado para um melhor desempenho.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Considerações de procedimentos armazenados compilados nativamente
Um procedimento armazenado compilado nativamente tem de ter Olá opções na sua cláusula T-SQL com os seguintes:

* NATIVE_COMPILATION
* SCHEMABINDING: tabelas significado Olá procedimento armazenado não podem ter as respetivas definições de coluna alteradas de qualquer forma que iria afetar o procedimento armazenado de Olá, a menos que largar o procedimento de Olá armazenado.

Um módulo nativo tem de utilizar uma grande [em blocos ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) para a gestão de transação. Não há nenhuma função para uma transação começar explícita ou para ROLLBACK TRANSACTION. Se o seu código detetar uma violação de uma regra de negócio, pode terminar o bloco atomic de Olá com um [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instrução.

### <a name="typical-create-procedure-for-natively-compiled"></a>CREATE PROCEDURE típico para compilados nativamente
Normalmente, Olá T-SQL toocreate um procedimento armazenado compilado nativamente é semelhante toohello modelo os seguintes:

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* Para Olá TRANSACTION_ISOLATION_LEVEL, o INSTANTÂNEO é procedimento de valor para Olá compilado nativamente armazenado mais comuns Olá. No entanto, um subconjunto de Olá outros valores também são suportados:
  
  * LEITURA REPETIDA
  * SERIALIZÁVEL
* Olá valor de idioma deve estar presente na vista de sys.languages Olá.

### <a name="how-toomigrate-a-stored-procedure"></a>Como toomigrate um procedimento armazenado
passos de migração de Olá são:

1. Obter Olá CREATE PROCEDURE script toohello regular interpretado procedimento armazenado.
2. O modelo anterior do cabeçalho toomatch Olá de regravação.
3. Ascertain se o procedimento armazenado de Olá código T-SQL utiliza quaisquer funcionalidades que não são suportadas para procedimentos armazenados compilados nativamente. Implementar soluções se necessário.
   
   * Para mais informações, consulte [problemas de migração para compilada nativamente procedimentos armazenados](http://msdn.microsoft.com/library/dn296678.aspx).
4. Mudar o nome de procedimento armazenado de antigo Olá utilizando SP_RENAME. Ou, basta REMOVÊ-la.
5. Execute o script Criar procedimento T-SQL editado.

## <a name="step-6-run-your-workload-in-test"></a>Passo 6: Executar a carga de trabalho no teste
Execute uma carga de trabalho na sua base de dados de teste que é semelhante toohello a carga de trabalho é executado na sua base de dados de produção. Isto deve revelar ganhos de desempenho de Olá alcançado através da utilização da funcionalidade de memória de Olá para tabelas e procedimentos armazenados.

Atributos principais da carga de trabalho Olá são:

* Número de ligações em simultâneo.
* Rácio de leitura/escrita.

tootailor e Olá executar a carga de trabalho de teste, considere a utilização da ferramenta de ostress.exe à mão de Olá, ilustrado na [aqui](sql-database-in-memory.md).

Latência de rede toominimize, execute o teste no Olá mesma região geográfica do Azure onde a base de dados de Olá existe.

## <a name="step-7-post-implementation-monitoring"></a>Passo 7: Monitorização de pós-implementação
Considere os efeitos de desempenho de Olá das suas implementações de dentro da memória na produção de monitorização:

* [Monitorizar o armazenamento em memória](sql-database-in-memory-oltp-monitoring.md).
* [Monitorizar a Base de Dados SQL do Azure com vistas de gestão dinâmica (Monitoring Azure SQL Database using dynamic management views)](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Ligações relacionadas
* [OLTP (otimização de memória) de memória](http://msdn.microsoft.com/library/dn133186.aspx)
* [TooNatively de introdução-compilado procedimentos armazenados](http://msdn.microsoft.com/library/dn133184.aspx)
* [Advisor de otimização de memória](http://msdn.microsoft.com/library/dn284308.aspx)

