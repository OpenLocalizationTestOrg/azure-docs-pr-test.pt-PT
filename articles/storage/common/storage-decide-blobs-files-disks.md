---
title: aaaDeciding quando toouse Azure Blobs, ficheiros do Azure ou os discos de dados do Azure
description: "Saiba mais sobre Olá diferentes formas toostore dados e de acesso no Azure toohelp que decidir qual toouse de tecnologia."
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
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: cd43abde43daf33dd7c43aa2696a9c8d5cd19612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>Decidir quando toouse Azure Blobs, ficheiros do Azure ou os discos de dados do Azure

Microsoft Azure fornece várias funcionalidades no armazenamento do Azure para armazenar e aceder aos seus dados na nuvem de Olá. Este artigo abrange os ficheiros do Azure, Blobs e discos de dados e é concebida toohelp escolha entre estas funcionalidades.

## <a name="scenarios"></a>Cenários

Olá a tabela seguinte compara os ficheiros, Blobs e discos de dados e mostra os cenários de exemplo adequadas para cada.

| Funcionalidade | Descrição | Quando toouse |
|--------------|-------------|-------------|
| **Ficheiros do Azure** | Fornece uma interface SMB, bibliotecas de cliente e um [REST interface](/rest/api/storageservices/file-service-rest-api) que permita o acesso a partir de qualquer lugar toostored ficheiros. | Pretende demasiado "de comparação de precisão e deslocar" uma nuvem de toohello de aplicação que já utiliza Olá nativo sistema APIs tooshare dados de ficheiros entre ele e outras aplicações em execução no Azure.<br/><br/>Pretende toostore desenvolvimento e depuração ferramentas que necessitam de toobe acedido a partir de várias máquinas virtuais. |
| **Blobs do Azure** | Fornece bibliotecas de cliente e um [REST interface](/rest/api/storageservices/blob-service-rest-api) que permite que os dados não estruturados demasiado ser armazenadas e aceder a uma grande escala em blobs de blocos. | Pretende que a aplicação toosupport de transmissão em fluxo e cenários de acesso aleatório.<br/><br/>Pretende toobe tooaccess capaz de dados da aplicação em qualquer lugar. |
| **Discos de dados do Azure** | Fornece bibliotecas de cliente e um [REST interface](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) que lhe permite toobe dados armazenados e acedido a partir de um disco rígido virtual anexado de forma permanente. | Pretende toolift e deslocar aplicações que utilizam tooread APIs do sistema de ficheiros nativo e escrever toopersistent os discos de dados.<br/><br/>Pretende toostore dados que não é necessário toobe acedido a partir do disco de Olá toowhich do Olá exteriores máquina virtual estão ligados. |

## <a name="comparison-files-and-blobs"></a>Comparação: Ficheiros e os Blobs

Olá, a tabela seguinte compara os ficheiros do Azure com Blobs do Azure.  
  
||||  
|-|-|-|  
|**Atributo**|**Blobs do Azure**|**Ficheiros do Azure**|  
|Opções de durabilidade|LRS, ZRS, GRS (e RA-GRS para maior disponibilidade)|LRS, GRS|  
|Acessibilidade|APIs REST|APIs REST<br /><br /> O SMB 2.1 e o SMB 3.0 (sistema de ficheiros padrão APIs)|  
|Conectividade|APIs REST em todo o mundo|APIs REST - em todo o mundo<br /><br /> O SMB 2.1 – numa região<br /><br /> O SMB 3.0 – em todo o mundo|  
|Pontos Finais|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Diretórios|Espaço de nomes simples|Objetos de diretório verdadeiro|  
|Sensibilidade maiúsculas e minúsculas de nomes|Sensíveis a maiúsculas e minúsculas|Às maiúsculas e minúsculas, mas preservam maiúsculas|  
|Capacidade|Cópia de segurança too500 contentores de TB|Partilhas de ficheiros de 5 TB|  
|Débito|Cópia de segurança too60 MB/s por BLOBs de blocos|Cópia de segurança too60 MB/s por partilha|  
|Tamanho do objeto|Cópia de segurança too200 blob de bloco/GB|Cópia de segurança too1TB/ficheiro|  
|Capacidade cobrada|Com base em bytes escritos|Com base no tamanho de ficheiro|  
|Bibliotecas de cliente|Vários idiomas|Vários idiomas|  
  
## <a name="comparison-files-and-data-disks"></a>Comparação: Ficheiros e discos de dados

Ficheiros do Azure complementam os discos de dados do Azure. Um disco de dados só pode ser anexado tooone Máquina Virtual do Azure a uma hora. Os discos de dados são VHDs-format armazenados em blobs de páginas no armazenamento do Azure e são utilizados pelos dados do Olá máquina virtual toostore durável. Partilhas de ficheiros nos ficheiros do Azure podem ser acedidas no Olá mesma forma como o disco local Olá é acedido (utilizando APIs do sistema de ficheiros nativo) e pode ser partilhado entre várias máquinas virtuais.  
 
Olá, a tabela seguinte compara os ficheiros do Azure com discos de dados do Azure.  
 
||||  
|-|-|-|  
|**Atributo**|**Discos de dados do Azure**|**Ficheiros do Azure**|  
|Âmbito|Máquina virtual tooa exclusivo|Acesso partilhado entre várias máquinas virtuais|  
|Instantâneos e de cópia|Sim|Não|  
|Configuração|Ligado durante o arranque da máquina virtual de Olá|Ligado depois Olá virtual ser iniciada|  
|Autenticação|Incorporado|Configurar com utilização net|  
|Limpeza|Automática|Manual|  
|Acesso através de REST|Não não possível aceder a ficheiros dentro do Olá VHD|Armazenado numa partilha de ficheiros podem ser acedidos|  
|Tamanho máx.|Disco de 1 TB|Ficheiro de 5 TB de partilha de ficheiros e 1 TB dentro da partilha|  
|IOps de 8KB máx.|500 IOps|1000 IOps|  
|Débito|Cópia de segurança too60 MB/s por disco|Cópia de segurança too60 MB/s por partilha de ficheiros|  

## <a name="next-steps"></a>Passos seguintes

Quando a tomar decisões sobre a forma como os dados são armazenados e aceder, deve também considerar os custos de Olá envolvidos. Para obter mais informações, consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/).
  
Algumas funcionalidades do SMB não são aplicáveis toohello nuvem. Para obter mais informações, consulte [funcionalidades não são suportadas pelo Olá serviço Azure ficheiros](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Para mais informações sobre os discos de dados, consulte [gestão de discos e imagens](../../virtual-machines/windows/about-disks-and-vhds.md) e [como tooAttach tooa um disco de dados Máquina Virtual do Windows](../../virtual-machines/windows/classic/attach-disk.md).
