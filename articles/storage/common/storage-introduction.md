---
title: aaaIntroduction tooAzure armazenamento | Microsoft Docs
description: "Introdução tooAzure armazenamento, armazenamento de dados da Microsoft na nuvem de Olá."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Introdução tooMicrosoft Storage do Azure

O Armazenamento do Microsoft Azure é um serviço cloud gerido da Microsoft que oferece armazenamento de elevada disponibilidade, seguro, duradouro, dimensionável e redundante. A Microsoft trata da manutenção e lida com os problemas críticos por si. 

O Armazenamento do Azure consiste em três serviços de dados: Armazenamento de Blobs, Armazenamento de Ficheiros e Armazenamento de Filas. O blob storage suporta armazenamento standard e premium, com o armazenamento premium utilizando apenas SSDs para possíveis de desempenho mais rápido Olá. Outra funcionalidade é armazenamento esporádico, permitindo-lhe toostorage grandes quantidades de dados raramente acedidos para um custo mais baixo.

Neste artigo, pode obter informações sobre seguinte Olá:
* Serviços de armazenamento do Azure Olá
* tipos de Olá de contas de armazenamento
* Aceder a blobs, filas e ficheiros
* Encriptação
* Replicação 
* Transferir dados para dentro ou fora do armazenamento
* Olá muitos bibliotecas de cliente de armazenamento disponíveis. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Introdução às Olá dos serviços de armazenamento do Azure

toouse qualquer um dos serviços de Olá fornecida pelo armazenamento do Azure – armazenamento de BLOBs, armazenamento de ficheiros e armazenamento de filas – tem primeiro de criar uma conta de armazenamento e, em seguida, pode transferir os dados de/para um serviço específico nessa conta de armazenamento. 

## <a name="blob-storage"></a>Armazenamento de blobs

Os blobs são, essencialmente, ficheiros semelhantes aos que armazena no seu computador (ou tablet, dispositivo móvel, etc.). Podem ser imagens, ficheiros do Microsoft Excel, ficheiros HTML, discos rígidos virtuais (VHDs), macrodados, como registos, cópias de segurança de bases de dados -- podem ser qualquer coisa, no fundo. Os BLOBs são armazenados em contentores que são toofolders semelhantes. 

Após o armazenamento de ficheiros no Blob storage, pode aceder aos mesmos partir de qualquer local no mundo de Olá utilizando URLs, Olá REST interface ou uma das bibliotecas de cliente de armazenamento de Azure SDK Olá. As bibliotecas de clientes de armazenamento estão disponíveis para muitas linguagens, incluindo Node.js, Java, PHP, Ruby, Python e .NET. 

Existem três tipos de blobs - blobs de blocos, blobs de acréscimo e blobs de páginas (utilizados para ficheiros VHD).

* Os blobs de blocos são ficheiros comum de toohold utilizadas cópias de segurança tooabout 4.7 TB. 
* Os blobs de páginas são ficheiros de acesso aleatório toohold utilizadas cópias de segurança too8 TB de tamanho. Estes são utilizados para ficheiros VHD Olá que apoiam a VMs.
* Acrescentar blobs são constituídos por blocos como Olá blobs de blocos, mas estão otimizados para operações de acréscimo. Estes são utilizados para ações como toohello informações mesmo blob o registo de várias VMs.

Para grandes conjuntos de dados onde as restrições de rede se carregar ou transferir o armazenamento de dados tooBlob através de transmissão Olá irreal pode enviar um conjunto de unidades de disco rígido tooMicrosoft tooimport ou exportar dados diretamente a partir do Centro de dados de Olá. Consulte [utilizar Olá serviço de importação/exportação do Microsoft Azure tooTransfer dados tooBlob armazenamento](../storage-import-export-service.md).

## <a name="file-storage"></a>Armazenamento de ficheiros

Olá serviço de ficheiros do Azure permite-lhe tooset segurança partilhas de ficheiros de rede altamente disponível que possa ser acedida através do protocolo Server Message Block (SMB) Olá padrão. Ficheiros com o que significa que podem partilhar várias VMs Olá mesmo com acesso de escrita e leitura. Também pode ler ficheiros de Olá utilizando a interface REST de Olá ou bibliotecas de cliente do armazenamento de Olá. 

Única coisa que distingue File storage do Azure dos ficheiros numa partilha de ficheiros empresarial é que pode aceder aos ficheiros de Olá partir de qualquer local no mundo Olá utilizando um URL que aponta toohello ficheiro e inclui um token de assinatura (SAS) de acesso partilhado. Pode gerar SAS tokens; permitem asset privada do tooa acesso específico durante um período de tempo específico. 

As partilhas de ficheiros podem ser utilizadas para inúmeros cenários comuns: 

* Muitas aplicações no local utilizam partilhas de ficheiros. Esta funcionalidade torna mais fácil toomigrate essas aplicações que partilham tooAzure de dados. Se montar hello toohello de partilha de ficheiros mesmo unidade letra Olá no local utiliza de aplicação, parte Olá da sua aplicação que acede a partilha de ficheiros de Olá deve funcionar com alterações mínimas, se aplicável.

* Os ficheiros de configuração podem ser armazenados numa partilha de ficheiros e acedidos a partir de múltiplas VMs. Ferramentas e utilitários utilizados pelos programadores vários num grupo podem ser armazenados numa partilha de ficheiros, garantindo que everybody pode encontrá-los, e que utilizam Olá a mesma versão.

* Os registos de diagnóstico, métricas e informações de estado de falha são apenas três exemplos de dados que podem ser escritos na partilha de ficheiros tooa e processados ou analisados mais tarde.

A este tempo, a autenticação baseada no Active Directory e o acesso não são suportadas listas de controlo (ACLs), mas estará em altura no Olá futura. Olá credenciais da conta de armazenamento são utilizados tooprovide autenticação para partilha de ficheiros de toohello de acesso. Isto significa que qualquer pessoa com partilha de Olá montada terão a partilha de toohello de acesso de leitura/escrita completa.

## <a name="queue-storage"></a>Armazenamento de filas

Olá serviço fila do Azure é utilizadas mensagens toostore e obter. Fila de mensagens pode ser segurança too64 KB de tamanho e uma fila pode conter milhões de mensagens. As filas são geralmente utilizados toostore listas de toobe de mensagens processados de forma assíncrona. 

Por exemplo, imagine que pretende que as imagens de tooupload capaz de toobe clientes e pretende toocreate miniaturas para cada imagem. Pode ter o cliente Aguarde que as miniaturas de Olá toocreate ao carregar as imagens de Olá. Uma alternativa seria toouse uma fila. Quando o cliente de Olá conclui o carregamento, escreva uma fila de toohello de mensagens. Em seguida, ter uma função do Azure obter a mensagem de saudação da fila de Olá e para criar miniaturas Olá. Cada uma das partes de Olá deste processamento pode ser ampliada separadamente, dando-lhe mais controlo quando otimização-lo para a sua utilização.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Table Storage
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
O Armazenamento de Tabelas Standard do Azure faz agora parte do Cosmos DB. Também disponível estão as Tabelas Premium do armazenamento de Tabelas do Azure, que oferece tabelas otimizadas para débito, distribuição global e índices secundários automáticos. toolearn mais e tente terminar nova experiência de premium Olá, consulte [BD do Azure Cosmos: API de tabela](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>Armazenamento em disco

equipa de armazenamento do Azure Olá também detém discos, que inclui todos os Olá gerido e capacidades de não gerido disco utilizadas pelas máquinas virtuais. Para obter mais informações sobre estas funcionalidades, consulte Olá [documentação do serviço de computação](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Tipos de contas de armazenamento 

Esta tabela mostra Olá vários tipos de contas do storage e quais os objetos que podem ser utilizados com cada um.

|**Tipo de conta de armazenamento**|**Standard para fins gerais**|**Premium para fins gerais**|**Armazenamento de blobs, camadas de acesso frequente e esporádico**|
|-----|-----|-----|-----|
|**Serviços suportados**| Serviços de Blob, Ficheiro e Fila | Serviço Blob | Serviço Blob|
|**Tipos de blobs suportados**|Blobs de blocos, blobs de páginas e blobs de acréscimo | Blobs de páginas | Blobs de blocos e blobs de acréscimo|

### <a name="general-purpose-storage-accounts"></a>Contas de armazenamento para fins gerais

Existem dois tipos de contas de armazenamento para fins gerais. 

#### <a name="standard-storage"></a>Armazenamento Standard 

Olá mais amplamente utilizada contas de armazenamento são contas de armazenamento standard, que podem ser utilizadas para todos os tipos de dados. Contas de armazenamento Standard utilizam dados do suporte de dados torção toostore.

#### <a name="premium-storage"></a>Armazenamento Premium

O Armazenamento Premium disponibiliza armazenamento de elevado desempenho para blobs de páginas, que são essencialmente utilizados para ficheiros VHD. Contas de armazenamento Premium utilizam dados de toostore SSD. A Microsoft recomenda utilizar o Armazenamento Premium em todas as suas VMs.

### <a name="blob-storage-accounts"></a>Contas de Armazenamento de blobs

conta de armazenamento de BLOBs de Olá é uma conta de armazenamento especializado utilizado toostore blobs de blocos e blobs de acréscimo. Não pode armazenar blobs de páginas nestas contas, pelo que não pode armazenar ficheiros VHD. Estas contas permitem-lhe tooset um tooHot de camada de acesso ou útil; é possível alterar a camada de Olá em qualquer altura. 

camada de acesso frequente de Olá é utilizada para os ficheiros que são acedidos com frequência – paga um custo mais elevado para armazenamento, mas custo de Olá de aceder a blobs Olá é muito inferior. Para blobs armazenados na camada de acesso esporádico Olá, paga um custo mais elevado para aceder aos blobs Olá, mas o custo de Olá de armazenamento é muito inferior.

## <a name="accessing-your-blobs-files-and-queues"></a>Aceder a blobs, ficheiros e filas

Cada conta de armazenamento tem duas chaves de autenticação, sendo que pode ser utilizada qualquer uma destas para realizar qualquer operação. Existem duas chaves, pelo que pode implementar através de Olá ocasionalmente chaves tooenhance segurança. É fundamental que estas chaves seja mantida segura porque permite que os respetivos posse, juntamente com o nome da conta Olá, dados de tooall acesso ilimitado na conta do storage Olá. 

Esta secção procura dois conta de armazenamento do Olá toosecure formas e os respetivos dados. Para obter informações detalhadas sobre como proteger a sua conta de armazenamento e os dados, consulte Olá [manual de segurança de armazenamento do Azure](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Proteger o acesso a contas de toostorage utilizar o Azure AD

Os dados de armazenamento do toosecure uma forma acesso tooyour são controlar o acesso toohello chaves de conta de armazenamento. Com o Gestor de recursos do controlo de acesso baseado em funções (RBAC), pode atribuir funções toousers, grupos ou aplicações. Estas funções estão associadas tooa conjunto específico de ações que são permitidas ou não permitido. Conta de armazenamento do toogrant acesso tooa através do RBAC processa apenas operações de gestão de Olá para essa conta de armazenamento, tal como alterar a camada de acesso de Olá. Não é possível utilizar objetos de toodata do RBAC toogrant acesso como uma partilha de ficheiro ou contentor específico. No entanto, pode utilizar o RBAC toogrant acesso toohello armazenamento chaves de conta, que, em seguida, podem ser utilizado tooread Olá dos objetos de dados. 

### <a name="securing-access-using-shared-access-signatures"></a>Utilizar assinaturas de acesso partilhado para proteger o acesso 

Pode utilizar assinaturas de acesso partilhado e armazenados toosecure de políticas de acesso os objetos de dados. Uma assinatura de acesso partilhado (SAS) é uma cadeia contendo um token de segurança que pode ser anexados toohello URI para um recurso que lhe permite objetos de armazenamento do toodelegate acesso toospecific e restrições de toospecify, tais como o intervalo de data/hora Olá de acesso e permissões. Esta funcionalidade tem extensas capacidades. Para obter informações detalhadas, consulte demasiado[através de acesso partilhado assinaturas (SAS)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Tooblobs acesso público

Olá serviço Blob permite-lhe tooprovide acesso público tooa contentor e os respetivos blobs ou um blob específico. Quando indicar que um contentor ou um blob é público, todas as pessoas podem lê-lo anonimamente. Não é necessária autenticação. Um exemplo de quando seria aconselhável toodo trata quando tiver um site que está a utilizar imagens, vídeo ou documentos a partir do Blob storage. Para obter mais informações, consulte [gerir o acesso de leitura anónimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Encriptação

Existem alguns dos tipos básicos de encriptação disponíveis Olá dos serviços de armazenamento. 

### <a name="encryption-at-rest"></a>Encriptação inativa 

Pode ativar a encriptação de serviço de armazenamento (SSE) em qualquer serviço de ficheiros de Olá (pré-visualização) ou Olá serviço Blob para uma conta de armazenamento do Azure. Se estiver ativada, todos os dados escritos serviço específico toohello é encriptado antes de escrita. Ao ler dados Olá, é desencriptado antes de que devolvido. 

### <a name="client-side-encryption"></a>Encriptação do lado do cliente

Olá bibliotecas de cliente de armazenamento têm métodos pode chamar tooprogrammatically encriptar dados antes de a enviar entre a transmissão Olá de Olá tooAzure de cliente. São armazenados encriptados, o que significa que também estão encriptados quando estão inativos. Ao ler dados de Olá novamente, desencriptar informações Olá depois de recebê-lo. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Encriptação em trânsito com Partilhas de Ficheiros do Azure

Veja [Utilizar Assinaturas de Acesso Partilhado (SAS)](../storage-dotnet-shared-access-signature-part-1.md) para obter mais informações sobre assinaturas de acesso partilhado. Consulte [gerir o acesso de leitura anónimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md) e [autenticação para Olá dos serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx) para obter mais informações sobre a conta de armazenamento de tooyour acesso seguro.

Para obter mais detalhes sobre como proteger a sua conta de armazenamento e a encriptação, consulte Olá [manual de segurança de armazenamento do Azure](storage-security-guide.md).

## <a name="replication"></a>Replicação

Ordem tooensure que os seus dados são duráveis, armazenamento do Azure tem Olá capacidade tookeep (e a gerir) várias cópias dos seus dados. Estas cópias são denominadas “réplicas” ou, por vezes, “redundância”. Vai selecionar o tipo de replicação quando configurar a sua conta de armazenamento. Na maioria dos casos, esta definição pode ser modificada depois de configurar a conta de armazenamento Olá. 

Todas as contas de armazenamento têm o **armazenamento localmente redundante (LRS)**. Isto significa três cópias dos seus dados são geridas pelo armazenamento do Azure no Centro de dados de Olá especificado quando a conta de armazenamento de Olá foi configurada. Quando as alterações são consolidar tooone copiar, hello outras duas cópias são atualizadas antes da devolução com êxito. Isto significa que os três réplicas de Olá sempre são sincronizadas. Além disso, Olá três cópias residirem em domínios de falhas separada e atualizar domínios, que significa que os dados estão disponíveis mesmo se falha um nó de armazenamento que contém os dados ou é colocado offline toobe atualizado. 

**Armazenamento localmente redundante (LRS)**

Tal como explicado anteriormente, com o LRS, tem três cópias dos seus dados num único datacenter. Isto processa problema Olá de dados se tornar indisponível se um nó de armazenamento falha ou é colocado offline toobe atualizada, mas não Olá maiúsculas e minúsculas de um centro de dados completo se tornar indisponível.

**Armazenamento com redundância de zona (ZRS)**

Armazenamento com redundância de zona (ZRS) mantém três cópias locais Olá dos seus dados, bem como outro conjunto de três cópias dos seus dados. Olá segundo conjunto de três cópias é replicado de forma assíncrona entre centros de dados dentro de uma ou duas regiões. Tenha em conta que o ZRS só está disponível nos blobs de blocos em contas de armazenamento de fins gerais. Além disso, depois de ter criado a sua conta do storage e selecionado o ZRS, não é possível convertê-lo toouse tooany outro tipo de replicação ou vice-versa.

As contas ZRS proporcionam uma durabilidade mais alta do que o LRS, mas não têm métricas nem capacidade de criação de relatórios. 

**Armazenamento georredundante (GRS)**

Armazenamento georredundante (GRS) mantém três cópias locais Olá dos seus dados numa região primária e outro conjunto de três cópias dos seus dados numa região secundária a centenas de quilómetros região primária Olá. O evento de uma falha na região primária Olá Olá, o Storage do Azure serão ativadas pós-falha região secundária toohello. 

**Armazenamento georredundante com acesso de leitura (RA-GRS)** 

Armazenamento georredundante com acesso de leitura é exatamente como GRS, exceto que, obter dados de toohello de acesso de leitura na localização secundária Olá. Se o Datacenter primário Olá fique temporariamente indisponível, pode continuar a dados de Olá tooread da localização secundária Olá. Isto pode ser muito útil. Por exemplo, pode ter uma aplicação web que muda para o modo só de leitura e de pontos de cópia de secundário toohello, permitindo algumas acesso, apesar das atualizações não estão disponíveis. 

> [!IMPORTANT]
> Pode alterar a forma como os dados são replicados depois de ter sido criada a sua conta do storage, a menos que tenha especificado o ZRS quando criou a conta de Olá. No entanto, tenha em atenção que pode implicar uma transferência de dados de uma única adicionais custo se mudar do LRS tooGRS ou RA-GRS.
>

Para obter mais informações sobre a replicação, veja [Azure Storage replication](storage-redundancy.md) (Replicação do Armazenamento do Azure).

Para informações de recuperação após desastre, consulte [que toodo se ocorrer uma falha de armazenamento do Azure](storage-disaster-recovery-guidance.md).

Para obter um exemplo de como tooleverage RA-GRS tooensure elevada disponibilidade de armazenamento, consulte [conceber altamente disponível aplicações utilizando RA-GRS](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transferência de dados tooand do armazenamento do Azure

Pode utilizar os dados de ficheiros e Olá AzCopy utilitário da linha de comandos toocopy blob dentro da sua conta do storage ou em contas de armazenamento. Consulte uma das seguintes Olá artigos de ajuda:

* [Transfer data with AzCopy for Windows](storage-use-azcopy.md) (Transferir dados com AzCopy para Windows)
* [Transfer data with AzCopy for Linux](storage-use-azcopy-linux.md) (Transferir dados com AzCopy para Linux)

AzCopy é desenvolvida com Olá [biblioteca de movimento de dados do Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), que está atualmente disponível na pré-visualização.

Olá serviço importar/exportar do Azure pode ser utilizadas tooimport ou exportação grandes quantidades de dados de blob tooor da sua conta de armazenamento. Preparar e correio várias unidades de disco rígido tooan Datacenter do Azure, onde são transferidos dados Olá do unidades de disco rígido Olá e enviar a fazer uma cópia de unidades de disco rígido Olá tooyou. Para mais informações sobre Olá serviço de importação/exportação, consulte [utilizar Olá serviço de importação/exportação do Microsoft Azure tooTransfer dados tooBlob armazenamento](../storage-import-export-service.md).

## <a name="pricing"></a>Preços

Para obter informações detalhadas sobre preços do Storage do Azure, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>APIs de armazenamento, bibliotecas e ferramentas
É possível aceder aos recursos do Storage do Azure por qualquer idioma que consiga efetuar pedidos de HTTP/HTTPS. Além disso, o Storage do Azure oferece bibliotecas de programação para vários idiomas populares. Estas bibliotecas simplificam muitos aspetos do trabalho com o Storage do Azure ao processar detalhes como a invocação síncrona e assíncrona, a criação de batches de operações, a gestão de exceções, as tentativas automáticas, o comportamento operacional, etc. As bibliotecas estão atualmente disponíveis para Olá seguintes idiomas e plataformas, com outros no pipeline de Olá:

### <a name="azure-storage-data-services"></a>Serviços de dados do Armazenamento do Azure
* [API REST dos Serviços de Armazenamento](/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1) (Biblioteca de Clientes de Armazenamento para .NET)
* [Biblioteca de Clientes de Armazenamento para C++](https://github.com/Azure/azure-storage-cpp)
* [Biblioteca de Clientes de Armazenamento do Azure para Java/Android](https://azure.microsoft.com/develop/java/)
* [Biblioteca de Clientes de Armazenamento para Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Biblioteca de Clientes de Armazenamento para PHP](https://azure.microsoft.com/develop/php/)
* [Biblioteca de Clientes de Armazenamento para Python](https://azure.microsoft.com/develop/python/)
* [Biblioteca de Clientes de Armazenamento para Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0) (Cmdlets do Armazenamento para PowerShell)
* [Storage Commands for CLI 2.0](/cli/azure/storage) (Comandos do Armazenamento para a CLI 2.0)

## <a name="next-steps"></a>Passos seguintes

* [Learn more about Blob storage](../blobs/storage-blobs-introduction.md) (Saiba mais sobre o Armazenamento de blobs)
* [Learn more about File storage](../storage-files-introduction.md) (Saiba mais sobre o Armazenamento de ficheiros)
* [Learn more about Queue storage](../queues/storage-queues-introduction.md) (Saiba mais sobre o Armazenamento de filas)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Para administradores
* [Using Azure PowerShell with Azure Storage (Utilizar o Azure PowerShell com o Armazenamento do Azure)](storage-powershell-guide-full.md)
* [Utilizar a CLI do Azure com o Armazenamento do Azure](../storage-azure-cli.md)

### <a name="for-net-developers"></a>Para programadores do .NET
* [Introdução ao armazenamento de Blobs do Azure através do .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Introdução ao armazenamento de Tabelas do Azure através do .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Introdução ao Armazenamento de filas do Azure através do .NET](../storage-dotnet-how-to-use-queues.md)
* [Introdução ao Armazenamento de Ficheiros do Azure no Windows](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Para orogramadores de Java/Android
* [Como toouse Blob storage do Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Como toouse Table storage do Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Como toouse armazenamento de filas do Java](../storage-java-how-to-use-queue-storage.md)
* [Como toouse File storage do Java](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Para programadores de Node.js
* [Como toouse Blob storage do Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Como toouse Table storage do Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Como toouse armazenamento de filas do Node.js](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Para programadores de PHP
* [Como toouse Blob storage do PHP](../blobs/storage-php-how-to-use-blobs.md)
* [Como toouse Table storage do PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Como toouse armazenamento de filas do PHP](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Para programadores de Ruby
* [Como toouse Blob storage do Ruby](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [Como toouse Table storage do Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [Como toouse armazenamento de filas do Ruby](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Para programadores de Python
* [Como toouse Blob storage do Python](../blobs/storage-python-how-to-use-blob-storage.md)
* [Como toouse Table storage do Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Como toouse armazenamento de filas do Python](../storage-python-how-to-use-queue-storage.md)   
* [Como toouse File storage do Python](../storage-python-how-to-use-file-storage.md) 
-->