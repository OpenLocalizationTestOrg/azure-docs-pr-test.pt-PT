---
title: aaaIntroduction tooAzure armazenamento de BLOBs | Microsoft Docs
description: "Introdução tooAzure armazenamento de BLOBs"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="b1f38-103">Armazenamento de tooBlob de introdução</span><span class="sxs-lookup"><span data-stu-id="b1f38-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="b1f38-104">Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados de objetos não estruturados, tais como texto ou dados binários, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b1f38-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="b1f38-105">Pode utilizar os dados do Blob storage tooexpose publicamente toohello mundo ou toostore dados da aplicação em privado.</span><span class="sxs-lookup"><span data-stu-id="b1f38-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="b1f38-106">Utilizações comuns do armazenamento de Blobs:</span><span class="sxs-lookup"><span data-stu-id="b1f38-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="b1f38-107">Servir imagens ou documentos diretamente tooa browser</span><span class="sxs-lookup"><span data-stu-id="b1f38-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="b1f38-108">Armazenamento de ficheiros para acesso distribuído</span><span class="sxs-lookup"><span data-stu-id="b1f38-108">Storing files for distributed access</span></span>
* <span data-ttu-id="b1f38-109">Transmissão de áudio e vídeo</span><span class="sxs-lookup"><span data-stu-id="b1f38-109">Streaming video and audio</span></span>
* <span data-ttu-id="b1f38-110">Armazenamento de dados de cópia de segurança e restauro, recuperação após desastre e arquivo</span><span class="sxs-lookup"><span data-stu-id="b1f38-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="b1f38-111">Armazenamento de dados para análise por um serviço no local ou alojado no Azure</span><span class="sxs-lookup"><span data-stu-id="b1f38-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="b1f38-112">Conceitos do serviço Blob</span><span class="sxs-lookup"><span data-stu-id="b1f38-112">Blob service concepts</span></span>

<span data-ttu-id="b1f38-113">Olá serviço Blob contém Olá os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="b1f38-113">hello Blob service contains hello following components:</span></span>

![Arquitetura de blob](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="b1f38-115">**Conta de armazenamento:** todas as acesso tooAzure armazenamento é feito através de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b1f38-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="b1f38-116">Esta conta de armazenamento pode ser um **conta do storage para fins gerais** ou um **conta de armazenamento de BLOBs** que é especializada para armazenar objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="b1f38-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="b1f38-117">Consulte [About Azure storage accounts (Acerca das contas de armazenamento do Azure)](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b1f38-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="b1f38-118">**Contentor:** um contentor fornece um agrupamento de um conjunto de blobs.</span><span class="sxs-lookup"><span data-stu-id="b1f38-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="b1f38-119">Todos os blobs tem de estar num contentor.</span><span class="sxs-lookup"><span data-stu-id="b1f38-119">All blobs must be in a container.</span></span> <span data-ttu-id="b1f38-120">Uma conta pode conter um número ilimitado de contentores.</span><span class="sxs-lookup"><span data-stu-id="b1f38-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="b1f38-121">Um contentor pode armazenar um número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="b1f38-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="b1f38-122">Tenha em atenção que o nome do contentor Olá tem de ser em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b1f38-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="b1f38-123">**Blob:** um ficheiro de qualquer tipo e tamanho.</span><span class="sxs-lookup"><span data-stu-id="b1f38-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="b1f38-124">O Storage do Azure oferece três tipos de blobs: blobs de blocos, blobs de páginas e blobs de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="b1f38-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="b1f38-125">Os *blobs de blocos* são ideais para armazenar ficheiros de texto ou binários, como documentos e ficheiros multimédia.</span><span class="sxs-lookup"><span data-stu-id="b1f38-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="b1f38-126">*Blobs de acréscimo* são semelhantes tooblock blobs em que estes são constituídos por blocos, mas são otimizados para operações de acréscimo, sendo pois úteis para cenários de registo.</span><span class="sxs-lookup"><span data-stu-id="b1f38-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="b1f38-127">Pode conter um blob de bloco única cópia de segurança too50, 000 blocos de cópia de segurança too100 MB cada, para um tamanho total ligeiramente superior 4.75 TB (100 MB X 50 000).</span><span class="sxs-lookup"><span data-stu-id="b1f38-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="b1f38-128">Pode conter um blob de acréscimo única cópia de segurança too50, 000 blocos de cópia de segurança too4 MB cada, para um tamanho total ligeiramente superior a 195 GB (4 MB X 50 000).</span><span class="sxs-lookup"><span data-stu-id="b1f38-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="b1f38-129">*Blobs de páginas* pode ser segurança too1 TB de tamanho e são mais eficientes para operações de leitura/escrita frequentes.</span><span class="sxs-lookup"><span data-stu-id="b1f38-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="b1f38-130">Máquinas virtuais do Azure utiliza os blobs de páginas como discos de dados e SO.</span><span class="sxs-lookup"><span data-stu-id="b1f38-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="b1f38-131">Para obter detalhes sobre os nomes dos contentores e dos blobs, veja [Naming and Referencing Containers, Blobs, and Metadata (Nomenclatura e Referência de Contentores, Blobs e Metadados)](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="b1f38-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1f38-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b1f38-132">Next steps</span></span>

* [<span data-ttu-id="b1f38-133">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b1f38-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="b1f38-134">Introdução ao Blob storage através do .NET</span><span class="sxs-lookup"><span data-stu-id="b1f38-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)