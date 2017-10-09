---
title: "Exemplos de armazenamento aaaAzure através do .NET | Microsoft Docs"
description: "Ver, transferir e executar o código de exemplo e aplicações para o Storage do Azure. Introdução aos exemplos de ficheiros, tabelas, filas e blobs utilizando bibliotecas de cliente de armazenamento de .NET Olá de deteção."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 9a7055645b0f0658b850f024b8b19ab19840330e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a>Exemplos de armazenamento do Azure através do .NET

## <a name="net-sample-index"></a>Índice de exemplo do .NET

Olá tabela seguinte fornece uma descrição geral dos nossos exemplos de cenários de repositório e Olá abrangidas cada amostra. Clique em Olá ligações tooview Olá correspondente código de exemplo no GitHub.

<table style="font-size:90%"><thead><tr><th style="font-size:110%">Ponto Final</th><th style="font-size:110%">Cenário</th><th style="font-size:110%">Código de exemplo</th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><b>Blob</b></td>
<td>Blob de acréscimo</td> 
<td><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Exemplo de método CloudBlobContainer.GetAppendBlobReference</a></td> 
</tr> 
<tr> 
<td>Blob de bloco</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicação Web de Galeria de fotografias de armazenamento de Blobs do Azure</a></td>
</tr> 
<tr> 
<td>Encriptação do Lado do Cliente</td>
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Exemplos de encriptação de blob</a></td>
</tr> 
<tr> 
<td>Copiar Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></td>
</tr> 
<tr> 
<td>Criar contentor</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicação Web de Galeria de fotografias de armazenamento de Blobs do Azure</a></td>
</tr> 
<tr> 
<td>Eliminar o Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicação Web de Galeria de fotografias de armazenamento de Blobs do Azure</a></td>
</tr> 
<tr> 
<td>Eliminar o contentor</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></td>
</tr> 
<tr> 
<td>Blob metadados/propriedades/estatísticas</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></td>
</tr> 
<tr> 
<td>ACL/metadados/as propriedades do contentor</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicação Web de Galeria de fotografias de armazenamento de Blobs do Azure</a></td>
</tr> 
<tr> 
<td>Obter intervalos de página</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></td>
</tr> 
<tr> 
<td>Concessão de contentor do Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></td>
</tr> 
<tr> 
<td>Lista/contentor do Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos Blobs</a></td>
</tr> 
<tr> 
<td>Blob de página</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos Blobs</a></td>
</tr>
<tr> 
<td>SAS</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></td>
</tr>   
<tr> 
<td>Propriedades do Serviço</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></td>
</tr>           
<tr> 
<td>Blob de instantâneo</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Discos de cópia de segurança Máquina Virtual do Azure com instantâneos Incremental</a></td>
</tr> 
<tr> 
<td rowspan="9"><b>Ficheiro</b></td>
<td>Criar partilhas/diretórios/ficheiros</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></td> 
</tr>
<tr> 
<td>Eliminar diretórios/partilhas/ficheiros</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Introdução ao serviço de ficheiros do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Propriedades/metadados do diretório</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Transferir ficheiros</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Ficheiro de metadados/propriedades/métricas</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Propriedades do serviço de ficheiro</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Lista de diretórios e ficheiros</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></td> 
</tr>
<tr> 
<td>Listar partilhas</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></td> 
</tr>
<tr> 
<td>Partilhar metadados/propriedades/estatísticas</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></td> 
</tr>
<tr> 
<td rowspan="8"><b>Fila</b></td>
<td>Adicionar mensagem</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Encriptação do Lado do Cliente</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Encriptação do lado do cliente de fila de .NET de armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Criar filas</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Eliminar a fila de mensagens /</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Observar mensagem</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Fila ACL/metadados/estatísticas</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao serviço de fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Propriedades do serviço fila</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao serviço de fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Mensagem de actualização</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td rowspan="7"><b>Tabela</b></td>
<td>Criar tabela</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestão de concorrência com o Storage do Azure - exemplo de aplicação</a></td> 
</tr> 
<tr> 
<td>Eliminar uma entidade/tabela</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabelas do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Entidade de intercalação/INSERT/substituir</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestão de concorrência com o Storage do Azure - exemplo de aplicação</a></td> 
</tr> 
<tr> 
<td>Entidades de consulta</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabelas do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Tabelas de consulta</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabelas do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Tabela ACL/propriedades</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introdução ao Armazenamento de Tabelas do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Entidade de atualização</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestão de concorrência com o Storage do Azure - exemplo de aplicação</a></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a>Biblioteca de exemplos de código do Azure

biblioteca de exemplo completo de Olá tooview, aceda toohello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteca, o que inclui exemplos de armazenamento do Azure que pode transferir e executar localmente. Biblioteca do código de exemplo de Olá fornece código de exemplo no formato. zip. Em alternativa, pode procurar e clonar o repositório do GitHub Olá para cada amostra.

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a>Obter guias de introdução

Veja Olá seguintes guias se pretender para instruções sobre como tooinstall e começar a utilizar com Olá bibliotecas de cliente de armazenamento do Azure.

* [Introdução ao serviço Blob do Azure no .NET](storage-dotnet-how-to-use-blobs.md)
* [Introdução ao serviço de fila do Azure no .NET](storage-dotnet-how-to-use-queues.md)
* [Introdução ao serviço de tabela do Azure no .NET](storage-dotnet-how-to-use-tables.md)
* [Introdução ao serviço de ficheiros do Azure no .NET](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a>Passos seguintes

Para informações sobre amostras para outros idiomas:

* Java: [exemplos de armazenamento do Azure utilizando Java](storage-samples-java.md)
* Todos os outros idiomas: [exemplos de armazenamento do Azure](storage-samples.md)
