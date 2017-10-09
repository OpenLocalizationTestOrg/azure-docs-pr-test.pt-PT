---
title: "tolerância a falhas aaaAdd na atividade de cópia de fábrica de dados do Azure por ignorar linhas incompatíveis | Microsoft Docs"
description: "Saiba como tooadd tolerância a falhas na atividade de cópia de fábrica de dados do Azure por ignorar linhas incompatíveis durante a cópia"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Adicione tolerância a falhas na atividade de cópia ao ignorar linhas incompatíveis

O Azure Data Factory [atividade de cópia](data-factory-data-movement-activities.md) oferece linhas incompatível do duas formas toohandle ao copiar dados entre os arquivos de dados de origem e dependente:

- Pode abortar e efetuar a cópia de Olá atividade quando os dados incompatíveis encontrado (comportamento predefinido).
- Pode continuar toocopy todos os dados de Olá adicionando tolerância a falhas e a ignorar as linhas de dados incompatíveis. Além disso, pode iniciar sessão linhas incompatível Olá no Blob storage do Azure. Em seguida, que pode examinar Olá registo toolearn Olá causa da falha de Olá, corrigir dados Olá na origem de dados de Olá e repita a atividade de cópia de Olá.

## <a name="supported-scenarios"></a>Cenários suportados
Atividade de cópia suporta três cenários para detetar, ignorar, dados e registo incompatíveis:

- **Incompatibilidade entre Olá tipo de dados de origem e o tipo nativo de Olá sink**

    Por exemplo: copiar dados de um ficheiro CSV no Blob storage tooa SQL da base de dados com uma definição de esquema que contém três **INT** colunas de tipo. Olá linhas do ficheiro CSV que contêm dados numéricos, tais como `123,456,789` são copiados com êxito toohello arquivo de sink. No entanto, Olá linhas que contêm valores não numéricos, tais como `123,456,abc` são detetados como incompatíveis e são ignorados.

- **Erro de correspondência no número de Olá de colunas entre a origem de Olá e o sink de Olá**

    Por exemplo: copiar dados de um ficheiro CSV no Blob storage tooa SQL da base de dados com uma definição de esquema que contenha seis colunas. Olá linhas que contêm seis colunas são um ficheiro CSV foi copiado com êxito toohello arquivo de sink. Olá CSV ficheiro linhas que contêm mais ou menos de seis colunas são detetadas como incompatíveis e são ignoradas.

- **Violação da chave primária ao escrever a base de dados relacional tooa**

    Por exemplo: copiar dados de uma base de dados SQL de tooa de servidor do SQL Server. Uma chave primária está definida na base de dados SQL de receptores de Olá, mas essa nenhuma chave primária está definida no SQL server origem Olá. linhas de Olá duplicada que existam na origem de Olá não podem ser copiado toohello sink. Atividade de cópia copia apenas Olá primeira linha dos dados de origem Olá no sink Olá. Olá origem subsequentes linhas que contêm o valor de chave primária Olá duplicado são detetadas como incompatíveis e são ignoradas.

## <a name="configuration"></a>Configuração
Olá exemplo seguinte fornece um tooconfigure de definição JSON a ignorar as linhas de incompatível Olá na atividade de cópia:

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Ative a ignorar incompatíveis linhas durante a cópia ou não. | Verdadeiro<br/>FALSE (predefinição) | Não |
| **redirectIncompatibleRowSettings** | Um grupo de propriedades que podem ser especificados quando quiser linhas incompatível do toolog Olá. | &nbsp; | Não |
| **linkedServiceName** | serviço de Olá ligado do Storage do Azure toostore Olá registo que contém as linhas de Olá foi ignorada. | nome de Olá de um [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) serviço, que se refere-se a instância de armazenamento toohello que pretende que o ficheiro de registo do toouse toostore Olá ligado. | Não |
| **caminho** | caminho de Olá Olá do ficheiro de registo que contém Olá ignorada linhas. | Especifique o caminho de armazenamento de BLOBs de Olá que pretende que os dados do toouse toolog Olá incompatível. Se não fornecer um caminho, o serviço de Olá cria um contentor para si. | Não |

## <a name="monitoring"></a>Monitorização
Após a conclusão da atividade de cópia de Olá executar, pode ver o número de Olá de linhas ignorados na secção monitorização de Olá:

![Monitor ignorada linhas incompatíveis](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Se configurar linhas incompatível do toolog Olá, pode encontrar o ficheiro de registo de Olá neste caminho: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` no ficheiro de registo de Olá, pode ver as linhas de Olá que foram ignoradas e Olá causa de raiz de incompatibilidade Olá.

Dados originais Olá e erro correspondente Olá são registadas no ficheiro de Olá. Um exemplo de conteúdo do ficheiro de registo de Olá é o seguinte:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a atividade de cópia de fábrica de dados do Azure, consulte [mover dados utilizando a atividade de cópia](data-factory-data-movement-activities.md).
