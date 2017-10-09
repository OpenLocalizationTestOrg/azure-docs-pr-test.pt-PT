## <a name="repeatability-during-copy"></a>Repetibilidade durante a cópia
Quando copiar tooAzure de dados do SQL Server/SQL Server a partir de outros dados armazena um repetibilidade de tookeep necessidades em mente tooavoid resultados inesperados. 

Quando copiar dados tooAzure base de dados do SQL Server/SQL Server, atividade de cópia irá pela tabela de receptores de toohello Olá conjunto de dados predefinido ACRESCENTAR por predefinição. Por exemplo, quando copiar dados a partir de uma origem de ficheiro CSV (dados de valores separados por vírgulas) que contém dois regista tooAzure base de dados do SQL Server/SQL Server, isto é que tabela Olá parece ser:

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Suponha que encontrou erros no ficheiro de origem e a quantidade de Olá atualizada de baixo Tube de 2 too4 no ficheiro de origem Olá. Se executar novamente o setor de dados de Olá durante esse período, encontrará dois novos registos anexado tooAzure base de dados do SQL Server/SQL Server. Olá abaixo parte do princípio de que nenhuma das colunas de Olá na tabela de Olá tem restrição de chave primária Olá.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid isto, terá de semântica UPSERT toospecify tirando partido de uma das Olá abaixo 2 mecanismos indicado abaixo.

> [!NOTE]
> Um setor pode ser novamente executado automaticamente no Azure Data Factory de acordo com a política de repetição de Olá especificada.
> 
> 

### <a name="mechanism-1"></a>Mecanismo de 1
Pode tirar partido **sqlWriterCleanupScript** propriedade toofirst efetuar a ação de limpeza quando um setor é executado. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Olá script de limpeza iria ser executado primeiro durante a cópia de um setor dado que iria a eliminar dados de Olá do setor de toothat correspondente do Olá tabela SQL. atividade de Olá subsequentemente irá inserir dados Olá na Olá tabela SQL. 

Se o setor de Olá está agora volte a executar, em seguida, pode encontrar a quantidade de Olá é atualizada como pretendido.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Suponha que Olá registo Washer simples é removido do csv original Olá. Em seguida, volte em execução setor de Olá produziria Olá seguinte resultado: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
Nada de novo tinha toobe concluído. atividade de cópia de Olá ficou Olá limpeza toodelete Olá correspondente dados de script para esse setor. Em seguida, lê-lo entrada Olá do ficheiro csv de Olá (que, em seguida, contidos apenas 1 registo) e inseridas-Olá tabela. 

### <a name="mechanism-2"></a>Mecanismo de 2
> [!IMPORTANT]
> sliceIdentifierColumnName não é suportada para o Azure SQL Data Warehouse neste momento. 

Repetibilidade de tooachieve outro mecanismo é ter uma coluna dedicada (**sliceIdentifierColumnName**) no Olá tabela de destino. Esta coluna seria utilizada pelo Azure Data Factory tooensure Olá origem e destino mantenha-se sincronizados. Esta abordagem funciona quando existe flexibilidade na alterar ou a definição de esquema de tabela de SQL de destino Olá. 

Esta coluna seria utilizada pelo Azure Data Factory para fins de repetibilidade e no processo de Olá do Azure Data Factory não efetuará quaisquer esquema toohello tabela é alterado. Forma toouse esta abordagem:

1. Defina uma coluna do tipo binário (32) no destino Olá tabela SQL. Não deverá haver nenhum restrições nesta coluna. Vamos nome desta coluna como 'ColumnForADFuseOnly' para este exemplo.
2. Utilizá-lo na atividade de cópia de Olá da seguinte forma:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

O Azure Data Factory preencherá esta coluna de acordo com a respetiva necessidade tooensure Olá origem e de destino permanecem sincronizadas. valores Olá esta coluna não devem ser utilizados fora neste contexto por utilizador Olá. 

Semelhante toomechanism 1, será de atividade de cópia automaticamente primeiro limpar dados de Olá para Olá dado o setor do destino de Olá tabela SQL e, em seguida, executar a atividade de cópia de Olá normalmente tooinsert dados Olá toodestination de origem para essa setor. 

