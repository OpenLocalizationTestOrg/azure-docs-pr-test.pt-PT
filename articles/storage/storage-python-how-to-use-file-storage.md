---
title: aaaDevelop para o File storage do Azure com o Python | Microsoft Docs
description: "Saiba como aplicações de Python toodevelop e serviços que utilizam toostore de armazenamento de ficheiros do Azure de ficheiros de dados."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Desenvolver para o File storage do Azure com o Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Acerca deste tutorial
Este tutorial demonstrar Noções básicas de Olá da utilização de aplicações do Python toodevelop ou serviços que utilizam dados de ficheiros de toostore de armazenamento de ficheiros do Azure. Neste tutorial, iremos criar uma aplicação de consola simples e Mostrar como tooperform ações básicas com o storage do Python e ficheiros do Azure:

* Criar partilhas de ficheiros do Azure
* Criar diretórios
* Enumerar ficheiros e diretórios numa partilha de ficheiros do Azure
* Carregar, transferir e eliminar um ficheiro

> [!Note]  
> Porque o File storage do Azure pode ser acedido através de SMB, é possível toowrite aplicações simples que aceder à partilha de ficheiros do Azure Olá utilizando Olá padrão e/s de Python classes e funções. Este artigo descreve como toowrite aplicações que utilizam Olá Azure armazenamento Python SDK, que utiliza Olá [File storage do Azure REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure armazenamento de ficheiros.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurar a sua aplicação toouse File storage do Azure
Adicione o seguinte de Olá perto Olá parte superior do ficheiro de origem qualquer Python no qual pretende tooprogrammatically acesso Storage do Azure.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Configurar uma ligação tooAzure armazenamento de ficheiros 
Olá `FileService` objeto permite-lhe trabalhar com partilhas, diretórios e ficheiros. Olá código seguinte cria um `FileService` utilizando Olá chave conta do storage conta e o nome do objeto. Substitua `<myaccount>` e `<mykey>` com o nome da conta e a chave.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Criar uma partilha de ficheiros do Azure
No seguinte exemplo de código de Olá, pode utilizar um `FileService` partilha de Olá de toocreate objeto se não existir.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Criar um diretório
Também pode organizar armazenamento colocando os ficheiros secundárias diretórios em vez de ter todos eles no diretório de raiz de Olá. File storage do Azure permite-lhe toocreate como muitos diretórios como a sua conta irá permitem. código de Olá abaixo irá criar um subdiretório com o nome **sampledir** no diretório de raiz de Olá.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar ficheiros e diretórios numa partilha de ficheiros do Azure
ficheiros de Olá toolist e diretórios numa partilha, utilize Olá **lista\_diretórios\_e\_ficheiros** método. Este método devolve um gerador de dimensões. Olá seguinte código produz Olá **nome** de cada ficheiro e diretório numa partilha toohello consola.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Carregar um ficheiro 
Ficheiros do Azure partilha contém em Olá muito menos, um diretório de raiz, onde podem residir os ficheiros. Nesta secção, irá aprender como tooupload um ficheiro a partir do armazenamento local para Olá raiz do diretório de uma partilha.

toocreate um ficheiro e os dados de carregamento, utilize Olá `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text` métodos. Estes são os métodos de alto nível que executam Olá necessário segmentação quando o tamanho de Olá dos dados de Olá exceder 64 MB.

`create_file_from_path`carregamentos Olá conteúdos de um ficheiro do caminho especificado Olá e `create_file_from_stream` carregamentos Olá conteúdo a partir de um fluxo/ficheiro já está aberto. `create_file_from_bytes`carrega uma matriz de bytes, e `create_file_from_text` carregamentos Olá especificado de valor de texto utilizando Olá especificado codificação (as predefinições tooUTF-8).

Olá exemplo seguinte carrega conteúdo Olá Olá **sunset.png** ficheiro para Olá **myfile** ficheiro.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Transferir um ficheiro
utilizar dados toodownload partir de um ficheiro `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, ou `get_file_to_text`. Estes são os métodos de alto nível que executam Olá necessário segmentação quando o tamanho de Olá dos dados de Olá exceder 64 MB.

Olá exemplo seguinte demonstra utilizando `get_file_to_path` conteúdo Olá toodownload Olá **myfile** de ficheiros e armazená-las toohello **fora sunset.png** ficheiro.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Eliminar um ficheiro
Por fim, toodelete um ficheiro, chamar `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu como toomanipulate File storage do Azure com o Python, siga estas toolearn ligações mais.

* [Centro para Programadores do Python](/develop/python/)
* [API REST dos Serviços do Armazenamento do Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Armazenamento do Microsoft Azure SDK para Python](https://github.com/Azure/azure-storage-python)