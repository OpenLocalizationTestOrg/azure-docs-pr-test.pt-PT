---
title: "Descrição geral de instantâneos de partilha de ficheiros do Azure (pré-visualização) | Microsoft Docs"
description: "Um instantâneo de partilha é uma versão só de leitura de uma partilha de ficheiros do Azure que é executada num ponto no tempo, como uma forma de fazer cópias de segurança da partilha."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2018
ms.author: renash
ms.openlocfilehash: c309804f33fc0e5b2091e18dfe5fe3c9849a2709
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/19/2018
---
# <a name="overview-of-share-snapshots-for-azure-files-preview"></a>Descrição geral de instantâneos de partilha de ficheiros do Azure (pré-visualização)
Ficheiros do Azure fornece a capacidade para criar instantâneos de partilha de partilhas de ficheiros. Partilha de instantâneos (pré-visualização) capturam o estado de partilha neste ponto no tempo. Neste artigo, vamos descrever que capacidades fornecem de instantâneos de partilha e como pode tirar partido dos mesmos no seu caso de utilização personalizada.


## <a name="when-to-use-share-snapshots"></a>Quando utilizar instantâneos de partilha

### <a name="protection-against-application-error-and-data-corruption"></a>Proteção contra danos nos dados e de erro de aplicação

As aplicações que utilizam partilhas de ficheiros efetuar operações como escrita, ler, armazenamento, a transmissão e processamento. Se uma aplicação está configurada incorretamente ou se é apresentado um erro não intencional, substituição acidental ou danos podem acontecer alguns blocos. Para ajudar a proteger contra estes cenários, pode tirar um instantâneo da partilha antes de implementar o novo código de aplicação. Se é apresentado um erro de erros ou aplicação com a nova implementação, pode voltar atrás para uma versão anterior dos seus dados em que a partilha de ficheiros. 

### <a name="protection-against-accidental-deletions-or-unintended-changes"></a>Proteção contra eliminações acidentais ou não intencional de alterações

Imagine que está a trabalhar num ficheiro de texto numa partilha de ficheiros. Depois de fechar o ficheiro de texto, perderá a capacidade de anular as alterações. Nestes casos, em seguida, terá de recuperar uma versão anterior do ficheiro. Pode utilizar instantâneos de partilha para recuperar versões anteriores do ficheiro se acidentalmente tiver mudado ou eliminado.

### <a name="general-backup-purposes"></a>Fins de cópia de segurança gerais

Depois de criar uma partilha de ficheiros, pode criar um instantâneo de partilha da partilha de ficheiros para utilizá-lo para cópia de segurança de dados periodicamente. Uma partilha de instantâneos, quando executada periodicamente, ajuda a manter as versões anteriores de dados que podem ser utilizadas para a requisitos futuros de auditoria ou de recuperação após desastre.

## <a name="capabilities"></a>Capacidades

Um instantâneo de partilha é uma cópia de ponto no tempo só de leitura dos seus dados. Pode criar, eliminar e gerir instantâneos utilizando a API REST. Capacidades também estão disponíveis no portal do Azure, CLI do Azure e biblioteca de clientes. 

Pode ver os instantâneos de uma partilha utilizando a REST API e o SMB. Pode obter a lista das versões do diretório ou ficheiro e podem montar uma versão específica diretamente como uma unidade. 

Depois de criar um instantâneo de partilha,-lo pode ser ler, copiar, ou eliminada, mas não modificado. Não é possível copiar um instantâneo de partilha completa para outra conta de armazenamento. Tem de fazer nesse ficheiro pelo ficheiro, utilizando o AzCopy ou de outros mecanismos de cópia.

Capacidade de instantâneos de partilha é fornecida ao nível da partilha de ficheiros. Obtenção é fornecida ao nível dos ficheiros individuais, para permitir a restaurar ficheiros individuais. Pode restaurar uma partilha de ficheiro completo através de SMB, a API REST, o portal, a biblioteca de clientes ou ferramentas da CLI do PowerShell.

Um instantâneo de partilha de uma partilha de ficheiros é idêntico para a partilha de ficheiros de base. A única diferença é que um **DateTime** valor é acrescentado à partilha de URI para indicar a hora em que a partilha de instantâneo. Por exemplo, se uma partilha de ficheiros URI http://storagesample.core.file.windows.net/myshare, o instantâneo de partilha URI é semelhante a:
```
http://storagesample.core.file.windows.net/myshare?snapshot=2011-03-09T01:42:34.9360000Z
```

Instantâneos de partilha são mantidas até que estes sejam eliminados explicitamente. Um instantâneo de partilha não é possível outlive a partilha de ficheiros de base. Pode enumerar os instantâneos associados a partilha de ficheiros de base para controlar os instantâneos atuais. 

Quando cria um instantâneo de partilha de uma partilha de ficheiros, nas propriedades do sistema da partilha de ficheiros são copiados para o instantâneo de partilha com os mesmos valores. Os ficheiros de base e metadados da partilha de ficheiros também são copiadas para o instantâneo de partilha, a menos que especifique metadados separado para a partilha de instantâneo quando a criar.

Não é possível eliminar uma partilha que tenha instantâneos de partilha, a menos que a elimine primeiro todos os instantâneos de partilha.


## <a name="space-usage"></a>Utilização de espaço 

Os instantâneos de partilha são incrementais natureza. Apenas os dados que foi alterado após o instantâneo de partilha mais recente é guardado. Isto minimiza o tempo necessário para criar o instantâneo de partilha e guarda os custos de armazenamento. Qualquer operação de escrita para o objeto ou propriedade ou metadados de operação de atualização é contabilizada na direção "conteúdo alterado" e está armazenada no instantâneo de partilha. 

Para poupar espaço, pode eliminar o instantâneo de partilha para o período de quando o volume de alterações foi mais elevado.

Apesar de instantâneos de partilha são guardados incrementalmente, é necessário manter apenas o instantâneo de partilha mais recente para restaurar a partilha. Quando eliminar um instantâneo de partilha, apenas os dados exclusivos para esse instantâneo de partilha são removidos. Instantâneos Active Directory contenham todas as informações que precisa para procurar e restaurar os dados (desde o momento em que a partilha de instantâneo) para a localização original ou uma localização alternativa. Pode restaurar ao nível do item.

Instantâneos não contam para o limite de partilha de 5 TB. Não há nenhum limite para a quantidade de instantâneos de partilha de espaço ocupam no total. Limites de conta de armazenamento ainda são aplicáveis.

## <a name="limits"></a>Limites

O número máximo de instantâneos de partilha de ficheiros do Azure permite hoje é 200. Depois de instantâneos de partilha de 200, tem de eliminar instantâneos de partilha anteriores para criar campanhas novas. 

Não há nenhum limite para as chamadas simultâneas para criação de instantâneos de partilha. Não há nenhum limite para a quantidade de espaço que a partilha de instantâneos de uma partilha de ficheiros específica podem consumir. 

## <a name="copying-data-back-to-a-share-from-share-snapshot"></a>Copiar dados para uma partilha de instantâneo de partilha

Operações de cópia que envolvem ficheiros e partilham instantâneos siga estas regras:

Pode copiar ficheiros individuais num instantâneo de partilha de ficheiros através de para a partilha de base ou qualquer outra localização. Pode restaurar uma versão anterior de um ficheiro ou restaurar a partilha de ficheiro completo ao copiar o ficheiro ao ficheiro do instantâneo de partilha. O instantâneo de partilha não é promovido a partilha de base. 

O instantâneo de partilha permanece intacto depois de copiar, mas a partilha de ficheiros de base é substituída por uma cópia dos dados que estavam disponíveis no instantâneo de partilha. Todos os a contagem de ficheiros restaurada para "alterar o conteúdo."

Pode copiar um ficheiro num instantâneo partilha para um destino com um nome diferente. O ficheiro de destino resultante é um ficheiro gravável e não um instantâneo de partilha.

Quando um ficheiro de destino é substituído por uma cópia, todos os instantâneos partilha associados ao ficheiro de destino original permaneçam intactos.

## <a name="general-best-practices"></a>Melhores práticas gerais 

Quando estiver a executar a infraestrutura no Azure, automatizar as cópias de segurança para recuperação de dados sempre que possível. Ações automatizadas são mais fiáveis do que processos manuais, ajudando a melhorar a proteção de dados e a capacidade de recuperação. Pode utilizar a API REST, o SDK do cliente ou para a automatização de script.

Antes de implementar o Programador de instantâneo de partilha, pondere cuidadosamente as definições de retenção para evitar incorrer em custos desnecessários e frequência de instantâneos de partilha.

Instantâneos de partilha fornecem apenas uma proteção ao nível dos ficheiros. Partilha de instantâneos não impedem eliminações fat mas numa conta de armazenamento ou de partilha de ficheiros. Para ajudar a proteger uma conta de armazenamento de eliminações acidentais, pode bloquear a conta de armazenamento ou o grupo de recursos.

## <a name="next-steps"></a>Passos Seguintes
* [Trabalhar com instantâneos de partilha](storage-how-to-use-files-snapshots.md)
* [Partilhar o instantâneo FAQ](storage-files-faq.md)

