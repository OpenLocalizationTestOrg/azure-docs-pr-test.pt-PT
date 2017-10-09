---
title: "aaaRepeatable cópia no Azure Data Factory | Microsoft Docs"
description: "Saiba como tooavoid duplicados, apesar de um setor que copia dados é executado mais do que uma vez."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Repetíveis cópia no Azure Data Factory

## <a name="repeatable-read-from-relational-sources"></a>Repetíveis leitura a partir de origens relacionais
Quando copiar dados de arquivos de dados relacional, manter a repetibilidade em mente tooavoid resultados inesperados. No Azure Data Factory, pode voltar a executar um setor manualmente. Também pode configurar a política de repetição para um conjunto de dados para que um setor será novamente executado quando ocorre uma falha. Quando um setor é voltar a executar qualquer forma, terá de toomake certificar-se de que Olá mesmos dados é de leitura como não independentemente do número de vezes que um setor é executado.  
 
> [!NOTE]
> Olá exemplos seguintes são para o Azure SQL, mas são aplicáveis tooany arquivo de dados que suporta conjuntos de dados retangular. Poderá ter tooadjust Olá **tipo** de origem e Olá **consulta** propriedade (por exemplo: consulta em vez de sqlReaderQuery) para dados de Olá armazenar.   

Normalmente, ao ler do relacionais arquivos, quer tooread únicos Olá dados correspondente toothat setor. Uma forma toodo, por isso, seria utilizando Olá WindowStart e WindowEnd sistema variáveis disponíveis no Azure Data Factory. Leia sobre as variáveis de Olá e funções no Azure Data Factory aqui no Olá [do Azure Data Factory - as funções e variáveis do sistema](data-factory-functions-variables.md) artigo. Exemplo: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
Esta consulta lê os dados que se situe no intervalo de duração de setor de Olá (WindowStart -> WindowEnd) da tabela de Olá MyTable. Volte a executar este setor seria também Certifique-se sempre que Olá mesmos dados é de leitura. 

Noutros casos, poderá desejar tabela inteira de Olá tooread e podem definir Olá sqlReaderQuery da seguinte forma:

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>Escrita repetíveis tooSqlSink
Quando copiar dados demasiado**Azure SQL/SQL Server** de outros arquivos de dados, terá de tookeep repetibilidade em mente tooavoid resultados inesperados. 

Quando copiar dados tooAzure base de dados do SQL Server/SQL Server, a atividade de cópia de Olá acrescenta tabela do sink de toohello de dados por predefinição. Diga, está a copiar dados de um CSV (valores separados por vírgulas) ficheiros que contêm dois registos toohello uma base de dados do servidor SQL/SQL do Azure a tabela seguinte. Quando um setor é executado, os registos de duas de Olá são copiados toohello tabela SQL. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Suponha que encontrou erros no ficheiro de origem e atualizar a quantidade de Olá de baixo Tube de 2 too4. Se voltar a executar o setor de dados de Olá durante esse período manualmente, encontrará dois novos registos anexado tooAzure base de dados do SQL Server/SQL Server. Este exemplo parte do princípio de que nenhuma das colunas de Olá na tabela de Olá tem restrição de chave primária Olá.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid este comportamento, terá de semântica UPSERT toospecify utilizando um dos seguintes dois mecanismos de Olá:

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Mecanismo de 1: sqlWriterCleanupScript utilizando o
Pode utilizar Olá **sqlWriterCleanupScript** tooclean de propriedade dos dados da tabela do sink Olá antes de inserir dados Olá quando um setor é executado. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Quando um setor é executado, o script de limpeza Olá é executado primeiro dados toodelete que corresponde ao toohello setor da tabela SQL Olá. atividade de cópia de Olá, em seguida, insere dados no Olá tabela SQL. Se o setor de Olá será novamente executada, a quantidade de Olá é atualizada conforme pretendido.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Suponha que Olá registo Washer simples é removido do csv original Olá. Em seguida, volte a executar o setor de Olá produziria Olá seguinte resultado: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

atividade de cópia de Olá ficou Olá limpeza toodelete Olá correspondente dados de script para esse setor. Em seguida, lê-lo entrada Olá do ficheiro csv de Olá (que contidas, em seguida, apenas um registo) e inseridas-Olá tabela. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Mecanismo de 2: sliceIdentifierColumnName utilizando o
> [!IMPORTANT]
> Atualmente, sliceIdentifierColumnName não é suportada para o Azure SQL Data Warehouse. 

repetibilidade do Olá segundo mecanismo tooachieve é ter uma coluna dedicada (sliceIdentifierColumnName) na tabela de destino de Olá. Esta coluna seria utilizada pelo Azure Data Factory tooensure Olá origem e destino mantenha-se sincronizados. Esta abordagem funciona quando existe flexibilidade na alterar ou a definição de esquema de tabela de SQL de destino Olá. 

Esta coluna é utilizada pelo Azure Data Factory para fins de repetibilidade e processo de Olá do Azure Data Factory não fazer qualquer esquema toohello tabela é alterado. Forma toouse esta abordagem:

1. Definir uma coluna do tipo **binário (32)** no destino Olá tabela SQL. Não deverá haver nenhum restrições nesta coluna. Vamos nome desta coluna como AdfSliceIdentifier para este exemplo.


    Tabela de origem:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Tabela de destino: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Utilizá-lo na atividade de cópia de Olá da seguinte forma:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

O Azure Data Factory preenche esta coluna de acordo com a respetiva necessidade tooensure Olá origem e de destino permanecem sincronizadas. valores Olá esta coluna não devem ser utilizados fora neste contexto. 

Semelhante toomechanism 1, a atividade de cópia limpa automaticamente dados de Olá para Olá fornecido setor do destino de Olá tabela SQL. Em seguida, inserem dados de origem na tabela de destino toohello. 

## <a name="next-steps"></a>Passos seguintes
Reveja Olá seguintes artigos do conector que, para concluir os exemplos JSON: 

- [Base de Dados SQL do Azure](data-factory-azure-sql-connector.md)
- [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)