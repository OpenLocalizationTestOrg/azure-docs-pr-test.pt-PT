---
title: "aaaHow toouse armazenamento do Azure para cópia de segurança do SQL Server e de restauro | Microsoft Docs"
description: "Saiba como tooback cópias de segurança do SQL Server tooAzure armazenamento. Explica as vantagens de Olá da cópia de segurança de bases de dados SQL tooAzure armazenamento."
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>Utilizar o armazenamento do Azure para cópia de segurança do SQL Server e de restauro
## <a name="overview"></a>Descrição geral
A partir do SQL Server 2012 SP1 CU2, pode agora escrever cópias de segurança do SQL Server diretamente toohello serviço de armazenamento de Blobs do Azure. Pode utilizar este tooback funcionalidade cópia de segurança tooand restauro do serviço de Blob do Azure Olá com uma base de dados do SQL Server no local ou uma base de dados do SQL Server numa máquina virtual do Azure. Cópia de segurança toocloud oferece vantagens de disponibilidade, ilimitado georreplicação armazenamento fora das instalações e facilidade de migração de dados tooand da nuvem Olá. Pode emitir instruções de cópia de segurança ou RESTAURO utilizando Transact-SQL ou SMO.

SQL Server 2016 apresenta novas funcionalidades; Pode utilizar [instantâneo de ficheiro de cópia de segurança](http://msdn.microsoft.com/library/mt169363.aspx) tooperform quase instantânea cópias de segurança e restauros incredibly rápidos.

Este tópico explica por que razão poderá escolher toouse storage do Azure para cópias de segurança do SQL Server e, em seguida, descreve os componentes de Olá envolvidos. Pode utilizar recursos Olá fornecidos no fim de Olá do Olá artigo tooaccess instruções e toostart informações adicionais com este serviço as cópias de segurança do SQL Server.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>Vantagens de utilizar hello serviço Blob do Azure para cópias de segurança do SQL Server
Existem alguns desafios que enfrentam quando efetuar cópias de segurança do SQL Server. Estes desafios incluem a gestão de armazenamento, o risco de falha de armazenamento, o acesso a armazenamento toooff site e a configuração de hardware. Muitas destes desafios são resolvidas utilizando o serviço de arquivo de Blob do Azure Olá para cópias de segurança do SQL Server. Considere Olá seguintes vantagens:

* **Facilidade de utilização**: armazenar as cópias de segurança em blobs do Azure pode ser uma opção fora das instalações tooaccess conveniente, flexível e fácil. Scripts criar armazenamento fora das instalações, para as cópias de segurança do SQL Server podem ser tão fácil como modificar existentes/tarefas toouse Olá **tooURL de cópia de segurança** sintaxe. Armazenamento fora das instalações, normalmente, deve ser suficiente de tooprevent de localização de base de dados de produção Olá um desastre único que pode afetar Olá off-site e localizações de base de dados de produção. Ao escolher demasiado[georreplicação replicar de blobs do Azure](../../../storage/common/storage-redundancy.md), ter uma camada adicional de proteção no evento Olá de um desastre que pode afetar a região todo Olá.
* **Arquivo de cópia de segurança**: Olá serviço Blob Storage do Azure oferece uma banda toohello alternativo utilizado frequentemente melhor cópias de segurança do opção tooarchive. Armazenamento em banda pode necessitar transportes físico tooan fora das instalações das instalações e as medidas tooprotect Olá suporte de dados. Armazenar as cópias de segurança no armazenamento de Blobs do Azure fornece uma instantâneas, elevada disponibilidade e a opção de arquivar um durável.
* **Gerido hardware**: não há nenhuma sobrecarga da gestão de hardware com serviços do Azure. Serviços do Azure gerir hardware de Olá e fornecem georreplicação para redundância e proteção contra falhas de hardware.
* **Armazenamento ilimitado**: ao ativar uma blobs tooAzure direta de cópia de segurança, tem acesso toovirtually armazenamento ilimitado. Em alternativa, a cópia de segurança de disco de máquina virtual do Azure tooan tem limites com base no tamanho da máquina. Há um número de toohello de limite de discos pode anexar tooan máquina virtual do Azure para cópias de segurança. Este limite é 16 discos para uma instância extra grande e menos instâncias mais pequeno.
* **Disponibilidade de cópia de segurança**: cópias de segurança armazenadas em blobs do Azure estão disponíveis a partir de qualquer lugar e em qualquer altura e podem facilmente ser acedido para restauros tooeither um SQL Server no local ou outro SQL Server em execução na máquina de Virtual uma Azure sem precisar de Olá para a base de dados expor/anular exposição ou transferir e anexar Olá VHD.
* **Custo**: pague apenas pelo serviço de Olá que é utilizado. Pode ser económico como uma opção de arquivo fora das instalações de cópia de segurança. Consulte Olá [Calculadora de preços do Azure](http://go.microsoft.com/fwlink/?LinkId=277060 "Calculadora de preços")e Olá [preços do Azure artigo](http://go.microsoft.com/fwlink/?LinkId=277059 "preços artigo") para obter mais informações informações.
* **Instantâneos de armazenamento**: quando os ficheiros de base de dados são armazenados num blob do Azure e estiver a utilizar o SQL Server 2016, pode utilizar [instantâneo de ficheiro de cópia de segurança](http://msdn.microsoft.com/library/mt169363.aspx) tooperform quase instantânea cópias de segurança e restauros incredibly rápidos.

Para obter mais detalhes, consulte [cópia de segurança do SQL Server e de restauro com o serviço de armazenamento de Blobs do Azure](http://go.microsoft.com/fwlink/?LinkId=271617).

Olá duas secções a seguir apresenta o serviço de armazenamento de Blobs do Azure Olá, incluindo Olá necessário componentes do SQL Server. É componentes de Olá toounderstand importantes e os respetivos cópia de segurança do interação toosuccessfully utilização e restauro a partir do serviço de armazenamento de Blobs do Azure Olá.

## <a name="azure-blob-storage-service-components"></a>Componentes do serviço de armazenamento de Blobs do Azure
Olá seguintes componentes do Azure são utilizados quando efetuar cópias de segurança toohello serviço de armazenamento de Blobs do Azure.

| Componente | Descrição |
| --- | --- |
| **Conta de armazenamento** |conta de armazenamento Olá é Olá ponto para todos os serviços de armazenamento de partida. tooaccess um serviço de armazenamento de Blobs do Azure, primeiro crie uma conta de armazenamento do Azure. Para mais informações sobre o serviço de armazenamento de Blobs do Azure, consulte [como toouse Olá o serviço de armazenamento de Blobs do Azure](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **Contentor** |Um contentor fornece um agrupamento de um conjunto de blobs e pode armazenar um número ilimitado de Blobs. toowrite um tooan de cópia de segurança do SQL Server serviço Blob do Azure, tem de ter, pelo menos, recipiente-raiz Olá criado. |
| **Blob** |Um ficheiro de qualquer tipo e tamanho. Os BLOBs são endereçáveis utilizando Olá segue o formato de URL: **https://[storage account].blob.core.windows.net/[container]/[blob]**. Para mais informações sobre os Blobs de páginas, consulte [compreender blocos e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>Componentes de servidor do SQL Server
Olá seguintes componentes do SQL Server são utilizados quando a cópia de segurança toohello serviço de armazenamento de Blobs do Azure.

| Componente | Descrição |
| --- | --- |
| **URL** |Um URL especifica um ficheiro de cópia de segurança exclusiva do Uniform Resource Identifier (URI) tooa. URL de Olá é utilizado tooprovide Olá localização e nome do ficheiro de cópia de segurança Olá do SQL Server. Olá URL tem de apontar tooan real blob, não apenas um contentor. Se não existir blob Olá, é criado. Se um blob existente for especificado, cópia de segurança falha, a menos que Olá > a opção WITH FORMAT está especificada. Olá seguinte é um exemplo de URL Olá especificaria Olá comandos de cópia de segurança: **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**. HTTPS é recomendado, mas não é necessária. |
| **Credencial** |informações de Olá que é necessário tooconnect e autenticar o serviço de armazenamento de BLOBs de tooAzure são armazenadas como uma credencial.  Ordem de tooan de cópias de segurança do SQL Server toowrite Blob do Azure ou o restauro a partir do mesmo, tem de ser criada uma credencial do SQL Server. Para obter mais informações, consulte [credencial do servidor SQL](https://msdn.microsoft.com/library/ms189522.aspx). |

> [!NOTE]
> Se escolher toocopy e carregar um ficheiro de cópia de segurança de toohello serviço de armazenamento de Blobs do Azure, tem de utilizar um tipo de blob de página como a opção de armazenamento se estiver a planear toouse este ficheiro para operações de restauro. RESTAURO a partir de um tipo de blob de bloco irá falhar com um erro.
> 
> 

## <a name="next-steps"></a>Passos seguintes
1. Crie uma conta do Azure se ainda não tiver um. Se estiver a avaliar o Azure, considere Olá [avaliação gratuita](https://azure.microsoft.com/free/).
2. Em seguida, avance através de um dos seguintes tutoriais guiá-lo através da criação de uma conta de armazenamento e efetuar um restauro de Olá.
   
   * **SQL Server 2014**: [Tutorial: cópia de segurança do SQL Server 2014 e no serviço de armazenamento de Blobs do Azure do restauro tooMicrosoft](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx).
   * **SQL Server 2016**: [Tutorial: utilizar o serviço de armazenamento de Blobs do Microsoft Azure Olá com bases de dados do SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx)
3. Reveja a documentação adicional começadas [cópia de segurança do SQL Server e de restauro com o serviço de armazenamento de Blobs do Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

Se tiver quaisquer problemas, consulte o tópico de Olá [cópia de segurança do SQL Server tooURL melhores práticas e resolução de problemas](https://msdn.microsoft.com/library/jj919149.aspx).

Para outro servidor de SQL de cópia de segurança e opções de restauro, consulte [cópia de segurança e restaurar para o SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

