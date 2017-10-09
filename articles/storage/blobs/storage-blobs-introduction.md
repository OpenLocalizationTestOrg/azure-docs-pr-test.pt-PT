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
# <a name="introduction-tooblob-storage"></a>Armazenamento de tooBlob de introdução

Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados de objetos não estruturados, tais como texto ou dados binários, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS. Pode utilizar os dados do Blob storage tooexpose publicamente toohello mundo ou toostore dados da aplicação em privado.

Utilizações comuns do armazenamento de Blobs:

* Servir imagens ou documentos diretamente tooa browser
* Armazenamento de ficheiros para acesso distribuído
* Transmissão de áudio e vídeo
* Armazenamento de dados de cópia de segurança e restauro, recuperação após desastre e arquivo
* Armazenamento de dados para análise por um serviço no local ou alojado no Azure

## <a name="blob-service-concepts"></a>Conceitos do serviço Blob

Olá serviço Blob contém Olá os seguintes componentes:

![Arquitetura de blob](./media/storage-blobs-introduction/blob1.png)

* **Conta de armazenamento:** todas as acesso tooAzure armazenamento é feito através de uma conta de armazenamento. Esta conta de armazenamento pode ser um **conta do storage para fins gerais** ou um **conta de armazenamento de BLOBs** que é especializada para armazenar objetos/blobs. Consulte [About Azure storage accounts (Acerca das contas de armazenamento do Azure)](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para obter mais informações.

* **Contentor:** um contentor fornece um agrupamento de um conjunto de blobs. Todos os blobs tem de estar num contentor. Uma conta pode conter um número ilimitado de contentores. Um contentor pode armazenar um número ilimitado de blobs. Tenha em atenção que o nome do contentor Olá tem de ser em minúsculas.

* **Blob:** um ficheiro de qualquer tipo e tamanho. O Storage do Azure oferece três tipos de blobs: blobs de blocos, blobs de páginas e blobs de acréscimo.
  
    Os *blobs de blocos* são ideais para armazenar ficheiros de texto ou binários, como documentos e ficheiros multimédia. *Blobs de acréscimo* são semelhantes tooblock blobs em que estes são constituídos por blocos, mas são otimizados para operações de acréscimo, sendo pois úteis para cenários de registo. Pode conter um blob de bloco única cópia de segurança too50, 000 blocos de cópia de segurança too100 MB cada, para um tamanho total ligeiramente superior 4.75 TB (100 MB X 50 000). Pode conter um blob de acréscimo única cópia de segurança too50, 000 blocos de cópia de segurança too4 MB cada, para um tamanho total ligeiramente superior a 195 GB (4 MB X 50 000).
  
    *Blobs de páginas* pode ser segurança too1 TB de tamanho e são mais eficientes para operações de leitura/escrita frequentes. Máquinas virtuais do Azure utiliza os blobs de páginas como discos de dados e SO.
  
    Para obter detalhes sobre os nomes dos contentores e dos blobs, veja [Naming and Referencing Containers, Blobs, and Metadata (Nomenclatura e Referência de Contentores, Blobs e Metadados)](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).

## <a name="next-steps"></a>Passos seguintes

* [Criar uma conta de armazenamento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Introdução ao Blob storage através do .NET](storage-dotnet-how-to-use-blobs.md)