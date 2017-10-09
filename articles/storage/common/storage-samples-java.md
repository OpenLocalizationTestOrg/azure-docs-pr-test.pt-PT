---
title: Exemplos de armazenamento de aaaAzure utilizando Java | Microsoft Docs
description: "Ver, transferir e executar o código de exemplo e aplicações para o Storage do Azure. Introdução aos exemplos de ficheiros, tabelas, filas e blobs utilizando bibliotecas de cliente de armazenamento de Java Olá de deteção."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="4a44d-104">Exemplos de armazenamento do Azure utilizando Java</span><span class="sxs-lookup"><span data-stu-id="4a44d-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="4a44d-105">Índice de exemplo de Java</span><span class="sxs-lookup"><span data-stu-id="4a44d-105">Java sample index</span></span>

<span data-ttu-id="4a44d-106">Olá tabela seguinte fornece uma descrição geral dos nossos exemplos de cenários de repositório e Olá abrangidas cada amostra.</span><span class="sxs-lookup"><span data-stu-id="4a44d-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="4a44d-107">Clique em Olá ligações tooview Olá correspondente código de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4a44d-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="4a44d-108">Ponto Final</span><span class="sxs-lookup"><span data-stu-id="4a44d-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="4a44d-109">Cenário</span><span class="sxs-lookup"><span data-stu-id="4a44d-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="4a44d-110">Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="4a44d-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="4a44d-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="4a44d-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="4a44d-112">Blob de acréscimo</span><span class="sxs-lookup"><span data-stu-id="4a44d-112">Append Blob</span></span></td> 
<td><span data-ttu-id="4a44d-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-114">Blob de bloco</span><span class="sxs-lookup"><span data-stu-id="4a44d-114">Block Blob</span></span></td>
<td><span data-ttu-id="4a44d-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-116">Encriptação do Lado do Cliente</span><span class="sxs-lookup"><span data-stu-id="4a44d-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="4a44d-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Como começar a encriptação do lado do cliente do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-118">Copiar Blob</span><span class="sxs-lookup"><span data-stu-id="4a44d-118">Copy Blob</span></span></td>
<td><span data-ttu-id="4a44d-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-120">Criar contentor</span><span class="sxs-lookup"><span data-stu-id="4a44d-120">Create Container</span></span></td>
<td><span data-ttu-id="4a44d-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-122">Eliminar o Blob</span><span class="sxs-lookup"><span data-stu-id="4a44d-122">Delete Blob</span></span></td>
<td><span data-ttu-id="4a44d-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-124">Eliminar o contentor</span><span class="sxs-lookup"><span data-stu-id="4a44d-124">Delete Container</span></span></td>
<td><span data-ttu-id="4a44d-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-126">Blob metadados/propriedades/estatísticas</span><span class="sxs-lookup"><span data-stu-id="4a44d-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="4a44d-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-128">ACL/metadados/as propriedades do contentor</span><span class="sxs-lookup"><span data-stu-id="4a44d-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="4a44d-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-130">Obter intervalos de página</span><span class="sxs-lookup"><span data-stu-id="4a44d-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="4a44d-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Exemplo de testes de BLOBs de páginas</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-132">Concessão de contentor do Blob</span><span class="sxs-lookup"><span data-stu-id="4a44d-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="4a44d-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-134">Lista/contentor do Blob</span><span class="sxs-lookup"><span data-stu-id="4a44d-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="4a44d-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-136">Blob de página</span><span class="sxs-lookup"><span data-stu-id="4a44d-136">Page Blob</span></span></td>
<td><span data-ttu-id="4a44d-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="4a44d-138">SAS</span><span class="sxs-lookup"><span data-stu-id="4a44d-138">SAS</span></span></td>
<td><span data-ttu-id="4a44d-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Exemplo de testes SAS</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="4a44d-140">Propriedades do Serviço</span><span class="sxs-lookup"><span data-stu-id="4a44d-140">Service Properties</span></span></td>
<td><span data-ttu-id="4a44d-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="4a44d-142">Blob de instantâneo</span><span class="sxs-lookup"><span data-stu-id="4a44d-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="4a44d-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="4a44d-144"><b>Ficheiro</b></span><span class="sxs-lookup"><span data-stu-id="4a44d-144"><b>File</b></span></span></td>
<td><span data-ttu-id="4a44d-145">Criar partilhas/diretórios/ficheiros</span><span class="sxs-lookup"><span data-stu-id="4a44d-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="4a44d-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="4a44d-147">Eliminar diretórios/partilhas/ficheiros</span><span class="sxs-lookup"><span data-stu-id="4a44d-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="4a44d-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-149">Propriedades/metadados do diretório</span><span class="sxs-lookup"><span data-stu-id="4a44d-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="4a44d-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-151">Transferir ficheiros</span><span class="sxs-lookup"><span data-stu-id="4a44d-151">Download Files</span></span></td> 
<td><span data-ttu-id="4a44d-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-153">Ficheiro de metadados/propriedades/métricas</span><span class="sxs-lookup"><span data-stu-id="4a44d-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="4a44d-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-155">Propriedades do serviço de ficheiro</span><span class="sxs-lookup"><span data-stu-id="4a44d-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="4a44d-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-157">Lista de diretórios e ficheiros</span><span class="sxs-lookup"><span data-stu-id="4a44d-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="4a44d-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="4a44d-159">Listar partilhas</span><span class="sxs-lookup"><span data-stu-id="4a44d-159">List Shares</span></span></td> 
<td><span data-ttu-id="4a44d-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="4a44d-161">Partilhar metadados/propriedades/estatísticas</span><span class="sxs-lookup"><span data-stu-id="4a44d-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="4a44d-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao serviço de ficheiros do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="4a44d-163"><b>Fila</b></span><span class="sxs-lookup"><span data-stu-id="4a44d-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="4a44d-164">Adicionar mensagem</span><span class="sxs-lookup"><span data-stu-id="4a44d-164">Add Message</span></span></td> 
<td><span data-ttu-id="4a44d-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Exemplos de biblioteca de cliente de Java de armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-166">Encriptação do Lado do Cliente</span><span class="sxs-lookup"><span data-stu-id="4a44d-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="4a44d-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Exemplos de biblioteca de cliente de Java de armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-168">Criar filas</span><span class="sxs-lookup"><span data-stu-id="4a44d-168">Create Queues</span></span></td> 
<td><span data-ttu-id="4a44d-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao serviço de fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-170">Eliminar a fila de mensagens /</span><span class="sxs-lookup"><span data-stu-id="4a44d-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="4a44d-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao serviço de fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-172">Observar mensagem</span><span class="sxs-lookup"><span data-stu-id="4a44d-172">Peek Message</span></span></td> 
<td><span data-ttu-id="4a44d-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao serviço de fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-174">Fila ACL/metadados/estatísticas</span><span class="sxs-lookup"><span data-stu-id="4a44d-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="4a44d-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introdução ao serviço de fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-176">Propriedades do serviço fila</span><span class="sxs-lookup"><span data-stu-id="4a44d-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="4a44d-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introdução ao serviço de fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-178">Mensagem de actualização</span><span class="sxs-lookup"><span data-stu-id="4a44d-178">Update Message</span></span></td> 
<td><span data-ttu-id="4a44d-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao serviço de fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="4a44d-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="4a44d-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="4a44d-181">Criar tabela</span><span class="sxs-lookup"><span data-stu-id="4a44d-181">Create Table</span></span></td> 
<td><span data-ttu-id="4a44d-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao serviço de tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-183">Eliminar uma entidade/tabela</span><span class="sxs-lookup"><span data-stu-id="4a44d-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="4a44d-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao serviço de tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-185">Entidade de intercalação/INSERT/substituir</span><span class="sxs-lookup"><span data-stu-id="4a44d-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="4a44d-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Exemplos de biblioteca de cliente de Java de armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-187">Entidades de consulta</span><span class="sxs-lookup"><span data-stu-id="4a44d-187">Query Entities</span></span></td> 
<td><span data-ttu-id="4a44d-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao serviço de tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-189">Tabelas de consulta</span><span class="sxs-lookup"><span data-stu-id="4a44d-189">Query Tables</span></span></td> 
<td><span data-ttu-id="4a44d-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao serviço de tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-191">Tabela ACL/propriedades</span><span class="sxs-lookup"><span data-stu-id="4a44d-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="4a44d-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Introdução ao serviço de tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="4a44d-193">Entidade de atualização</span><span class="sxs-lookup"><span data-stu-id="4a44d-193">Update Entity</span></span></td> 
<td><span data-ttu-id="4a44d-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Exemplos de biblioteca de cliente de Java de armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="4a44d-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="4a44d-195">Biblioteca de exemplos de código do Azure</span><span class="sxs-lookup"><span data-stu-id="4a44d-195">Azure Code Samples library</span></span>

<span data-ttu-id="4a44d-196">biblioteca de exemplo completo de Olá tooview, aceda toohello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteca, o que inclui exemplos de armazenamento do Azure que pode transferir e executar localmente.</span><span class="sxs-lookup"><span data-stu-id="4a44d-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="4a44d-197">Biblioteca do código de exemplo de Olá fornece código de exemplo no formato. zip.</span><span class="sxs-lookup"><span data-stu-id="4a44d-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="4a44d-198">Em alternativa, pode procurar e clonar o repositório do GitHub Olá para cada amostra.</span><span class="sxs-lookup"><span data-stu-id="4a44d-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="4a44d-199">Obter guias de introdução</span><span class="sxs-lookup"><span data-stu-id="4a44d-199">Getting started guides</span></span>

<span data-ttu-id="4a44d-200">Veja Olá seguintes guias se pretender para instruções sobre como tooinstall e começar a utilizar com Olá bibliotecas de cliente de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a44d-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="4a44d-201">Introdução ao serviço Blob do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="4a44d-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="4a44d-202">Introdução ao serviço de fila do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="4a44d-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="4a44d-203">Introdução ao serviço de tabela do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="4a44d-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="4a44d-204">Introdução ao serviço de ficheiros do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="4a44d-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="4a44d-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4a44d-205">Next steps</span></span>

<span data-ttu-id="4a44d-206">Para informações sobre amostras para outros idiomas:</span><span class="sxs-lookup"><span data-stu-id="4a44d-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="4a44d-207">.NET: [exemplos de armazenamento do azure através do .NET](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="4a44d-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="4a44d-208">Todos os outros idiomas: [exemplos de armazenamento do Azure](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="4a44d-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
