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
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="8820a-104">Exemplos de armazenamento do Azure através do .NET</span><span class="sxs-lookup"><span data-stu-id="8820a-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="8820a-105">Índice de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="8820a-105">.NET sample index</span></span>

<span data-ttu-id="8820a-106">Olá tabela seguinte fornece uma descrição geral dos nossos exemplos de cenários de repositório e Olá abrangidas cada amostra.</span><span class="sxs-lookup"><span data-stu-id="8820a-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="8820a-107">Clique em Olá ligações tooview Olá correspondente código de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="8820a-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="8820a-108">Ponto Final</span><span class="sxs-lookup"><span data-stu-id="8820a-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="8820a-109">Cenário</span><span class="sxs-lookup"><span data-stu-id="8820a-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="8820a-110">Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="8820a-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="8820a-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="8820a-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="8820a-112">Blob de acréscimo</span><span class="sxs-lookup"><span data-stu-id="8820a-112">Append Blob</span></span></td> 
<td><span data-ttu-id="8820a-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Exemplo de método CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="8820a-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-114">Blob de bloco</span><span class="sxs-lookup"><span data-stu-id="8820a-114">Block Blob</span></span></td>
<td><span data-ttu-id="8820a-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicação Web de Galeria de fotografias de armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-116">Encriptação do Lado do Cliente</span><span class="sxs-lookup"><span data-stu-id="8820a-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="8820a-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Exemplos de encriptação de blob</a></span><span class="sxs-lookup"><span data-stu-id="8820a-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-118">Copiar Blob</span><span class="sxs-lookup"><span data-stu-id="8820a-118">Copy Blob</span></span></td>
<td><span data-ttu-id="8820a-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-120">Criar contentor</span><span class="sxs-lookup"><span data-stu-id="8820a-120">Create Container</span></span></td>
<td><span data-ttu-id="8820a-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicação Web de Galeria de fotografias de armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-122">Eliminar o Blob</span><span class="sxs-lookup"><span data-stu-id="8820a-122">Delete Blob</span></span></td>
<td><span data-ttu-id="8820a-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicação Web de Galeria de fotografias de armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-124">Eliminar o contentor</span><span class="sxs-lookup"><span data-stu-id="8820a-124">Delete Container</span></span></td>
<td><span data-ttu-id="8820a-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-126">Blob metadados/propriedades/estatísticas</span><span class="sxs-lookup"><span data-stu-id="8820a-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="8820a-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-128">ACL/metadados/as propriedades do contentor</span><span class="sxs-lookup"><span data-stu-id="8820a-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="8820a-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicação Web de Galeria de fotografias de armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-130">Obter intervalos de página</span><span class="sxs-lookup"><span data-stu-id="8820a-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="8820a-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-132">Concessão de contentor do Blob</span><span class="sxs-lookup"><span data-stu-id="8820a-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="8820a-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-134">Lista/contentor do Blob</span><span class="sxs-lookup"><span data-stu-id="8820a-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="8820a-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="8820a-136">Blob de página</span><span class="sxs-lookup"><span data-stu-id="8820a-136">Page Blob</span></span></td>
<td><span data-ttu-id="8820a-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="8820a-138">SAS</span><span class="sxs-lookup"><span data-stu-id="8820a-138">SAS</span></span></td>
<td><span data-ttu-id="8820a-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="8820a-140">Propriedades do Serviço</span><span class="sxs-lookup"><span data-stu-id="8820a-140">Service Properties</span></span></td>
<td><span data-ttu-id="8820a-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos Blobs</a></span><span class="sxs-lookup"><span data-stu-id="8820a-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="8820a-142">Blob de instantâneo</span><span class="sxs-lookup"><span data-stu-id="8820a-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="8820a-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Discos de cópia de segurança Máquina Virtual do Azure com instantâneos Incremental</a></span><span class="sxs-lookup"><span data-stu-id="8820a-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="8820a-144"><b>Ficheiro</b></span><span class="sxs-lookup"><span data-stu-id="8820a-144"><b>File</b></span></span></td>
<td><span data-ttu-id="8820a-145">Criar partilhas/diretórios/ficheiros</span><span class="sxs-lookup"><span data-stu-id="8820a-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="8820a-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="8820a-147">Eliminar diretórios/partilhas/ficheiros</span><span class="sxs-lookup"><span data-stu-id="8820a-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="8820a-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Introdução ao serviço de ficheiros do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-149">Propriedades/metadados do diretório</span><span class="sxs-lookup"><span data-stu-id="8820a-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="8820a-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-151">Transferir ficheiros</span><span class="sxs-lookup"><span data-stu-id="8820a-151">Download Files</span></span></td> 
<td><span data-ttu-id="8820a-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-153">Ficheiro de metadados/propriedades/métricas</span><span class="sxs-lookup"><span data-stu-id="8820a-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="8820a-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-155">Propriedades do serviço de ficheiro</span><span class="sxs-lookup"><span data-stu-id="8820a-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="8820a-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-157">Lista de diretórios e ficheiros</span><span class="sxs-lookup"><span data-stu-id="8820a-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="8820a-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="8820a-159">Listar partilhas</span><span class="sxs-lookup"><span data-stu-id="8820a-159">List Shares</span></span></td> 
<td><span data-ttu-id="8820a-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="8820a-161">Partilhar metadados/propriedades/estatísticas</span><span class="sxs-lookup"><span data-stu-id="8820a-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="8820a-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de armazenamento de ficheiros de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="8820a-163"><b>Fila</b></span><span class="sxs-lookup"><span data-stu-id="8820a-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="8820a-164">Adicionar mensagem</span><span class="sxs-lookup"><span data-stu-id="8820a-164">Add Message</span></span></td> 
<td><span data-ttu-id="8820a-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-166">Encriptação do Lado do Cliente</span><span class="sxs-lookup"><span data-stu-id="8820a-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="8820a-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Encriptação do lado do cliente de fila de .NET de armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8820a-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-168">Criar filas</span><span class="sxs-lookup"><span data-stu-id="8820a-168">Create Queues</span></span></td> 
<td><span data-ttu-id="8820a-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-170">Eliminar a fila de mensagens /</span><span class="sxs-lookup"><span data-stu-id="8820a-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="8820a-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-172">Observar mensagem</span><span class="sxs-lookup"><span data-stu-id="8820a-172">Peek Message</span></span></td> 
<td><span data-ttu-id="8820a-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-174">Fila ACL/metadados/estatísticas</span><span class="sxs-lookup"><span data-stu-id="8820a-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="8820a-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao serviço de fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-176">Propriedades do serviço fila</span><span class="sxs-lookup"><span data-stu-id="8820a-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="8820a-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao serviço de fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-178">Mensagem de actualização</span><span class="sxs-lookup"><span data-stu-id="8820a-178">Update Message</span></span></td> 
<td><span data-ttu-id="8820a-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao serviço de fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="8820a-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="8820a-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="8820a-181">Criar tabela</span><span class="sxs-lookup"><span data-stu-id="8820a-181">Create Table</span></span></td> 
<td><span data-ttu-id="8820a-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestão de concorrência com o Storage do Azure - exemplo de aplicação</a></span><span class="sxs-lookup"><span data-stu-id="8820a-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-183">Eliminar uma entidade/tabela</span><span class="sxs-lookup"><span data-stu-id="8820a-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="8820a-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabelas do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-185">Entidade de intercalação/INSERT/substituir</span><span class="sxs-lookup"><span data-stu-id="8820a-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="8820a-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestão de concorrência com o Storage do Azure - exemplo de aplicação</a></span><span class="sxs-lookup"><span data-stu-id="8820a-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-187">Entidades de consulta</span><span class="sxs-lookup"><span data-stu-id="8820a-187">Query Entities</span></span></td> 
<td><span data-ttu-id="8820a-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabelas do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-189">Tabelas de consulta</span><span class="sxs-lookup"><span data-stu-id="8820a-189">Query Tables</span></span></td> 
<td><span data-ttu-id="8820a-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabelas do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-191">Tabela ACL/propriedades</span><span class="sxs-lookup"><span data-stu-id="8820a-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="8820a-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introdução ao Armazenamento de Tabelas do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="8820a-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="8820a-193">Entidade de atualização</span><span class="sxs-lookup"><span data-stu-id="8820a-193">Update Entity</span></span></td> 
<td><span data-ttu-id="8820a-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestão de concorrência com o Storage do Azure - exemplo de aplicação</a></span><span class="sxs-lookup"><span data-stu-id="8820a-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="8820a-195">Biblioteca de exemplos de código do Azure</span><span class="sxs-lookup"><span data-stu-id="8820a-195">Azure Code Samples library</span></span>

<span data-ttu-id="8820a-196">biblioteca de exemplo completo de Olá tooview, aceda toohello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteca, o que inclui exemplos de armazenamento do Azure que pode transferir e executar localmente.</span><span class="sxs-lookup"><span data-stu-id="8820a-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="8820a-197">Biblioteca do código de exemplo de Olá fornece código de exemplo no formato. zip.</span><span class="sxs-lookup"><span data-stu-id="8820a-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="8820a-198">Em alternativa, pode procurar e clonar o repositório do GitHub Olá para cada amostra.</span><span class="sxs-lookup"><span data-stu-id="8820a-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="8820a-199">Obter guias de introdução</span><span class="sxs-lookup"><span data-stu-id="8820a-199">Getting started guides</span></span>

<span data-ttu-id="8820a-200">Veja Olá seguintes guias se pretender para instruções sobre como tooinstall e começar a utilizar com Olá bibliotecas de cliente de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8820a-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="8820a-201">Introdução ao serviço Blob do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="8820a-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="8820a-202">Introdução ao serviço de fila do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="8820a-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="8820a-203">Introdução ao serviço de tabela do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="8820a-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="8820a-204">Introdução ao serviço de ficheiros do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="8820a-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="8820a-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8820a-205">Next steps</span></span>

<span data-ttu-id="8820a-206">Para informações sobre amostras para outros idiomas:</span><span class="sxs-lookup"><span data-stu-id="8820a-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="8820a-207">Java: [exemplos de armazenamento do Azure utilizando Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="8820a-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="8820a-208">Todos os outros idiomas: [exemplos de armazenamento do Azure](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="8820a-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
