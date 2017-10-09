---
title: aaaBackup e restaurar para o SQL Server | Microsoft Docs
description: "Descreve as considerações de cópia de segurança e restauro de bases de dados do SQL Server em execução em máquinas de virtuais do Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Cópia de Segurança e Restauro para SQL Server em Máquinas Virtuais do Azure
## <a name="overview"></a>Descrição geral
Armazenamento do Azure mantém 3 cópias de cada proteção de tooguarantee de disco de VM do Azure contra perda de dados ou danos nos dados físico. Assim, ao contrário no local, não precisa de tooworry sobre estes. No entanto, deve ainda efetuar cópias de segurança sua tooprotect de bases de dados do SQL Server relativamente a erros de aplicações ou utilizadores (por exemplo, a inserção de dados incorreto ou eliminar uma tabela) e que está a ser capaz de toorestore tooa ponto no tempo.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Para o SQL Server em execução em VMs do Azure, pode utilizar a cópia de segurança nativa e restaurar técnicas utilizando discos ligados para destino Olá ficheiros de cópia de segurança de Olá. No entanto, não há limite toohello diversas discos pode anexar tooan máquina virtual do Azure, com base no Olá [tamanho de máquina virtual de Olá](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Também é custos de Olá tooconsider de gestão de disco.

A partir do SQL Server 2014, pode criar cópias de segurança e restaurar tooMicrosoft Blob storage do Azure. SQL Server 2016 também fornece melhoramentos para esta opção. Além disso, para os ficheiros de base de dados armazenados no armazenamento de Blobs do Microsoft Azure, SQL Server 2016 fornece uma opção de cópias quase instantânea de e para restauros rápidos utilizando instantâneos do Azure. Este artigo fornece uma descrição geral destas opções e informações adicionais que podem ser encontradas em [cópia de segurança do SQL Server e de restauro com o serviço de armazenamento de Blobs do Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Para ver um debate Olá as opções para efetuar uma cópia de segurança de bases de dados muito grandes, consulte [várias Terabyte SQL Server da base de dados cópia de segurança estratégias para o Azure Virtual Machines](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

as secções de Olá abaixo incluem informações específicas toohello as diferentes versões do SQL Server suportada numa máquina virtual do Azure.

## <a name="sql-server-virtual-machines"></a>Máquinas virtuais do SQL Server
Quando a instância do SQL Server está a executar uma Máquina Virtual no Azure, os ficheiros de base de dados já residem em discos de dados no Azure. Estes discos em direto no Blob storage do Azure. Por isso, Olá entre as razões para efetuar uma cópia de segurança das base de dados e Olá abordagens que tomar ligeiramente a alteração. Considere Olá seguinte. 

* Já não necessita de proteção tooprovide de cópias de segurança de base de dados do tooperform contra falhas de hardware ou de suportes de dados porque o Microsoft Azure fornece esta proteção como parte da Olá serviço Microsoft Azure.
* Ainda precisa de proteção de tooprovide de cópias de segurança do tooperform da base de dados relativamente a erros de utilizador ou para fins de registo, por motivos de regulamentação ou fins administrativos.
* Pode armazenar ficheiros de cópia de segurança de Olá diretamente no Azure. Para obter mais informações, consulte Olá seguintes secções que fornecem orientações para Olá diferentes versões do SQL Server.

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016 suporta [cópia de segurança e restaurar com blobs do Azure](https://msdn.microsoft.com/library/jj919148.aspx) funcionalidades encontrado no SQL Server 2014. Mas também inclui Olá seguintes melhoramentos:

| Melhoramento de 2016 | Detalhes |
| --- | --- |
| **Striping** |Quando efetuar cópias de segurança tooMicrosoft blob storage do Azure, SQL Server 2016 suporta a cópia de segurança toomultiple blobs tooenable cópia de segurança de bases de dados grandes, cópia de segurança máximo tooa 12.8 TB. |
| **Cópia de segurança de instantâneos** |Através da utilização de Olá de instantâneos do Azure, a cópia de segurança do instantâneo de ficheiro do SQL Server fornece quase instantânea cópias de segurança e restauros rápidos para ficheiros de base de dados armazenados com o serviço de armazenamento de Blobs do Azure Olá. Esta capacidade permite-lhe toosimplify as políticas de cópia de segurança e restauro. Instantâneo de ficheiro de cópia de segurança também suporta ponto de restauro de tempo. Para obter mais informações, consulte [cópias de segurança de instantâneos de ficheiros de base de dados no Azure](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx). |
| **Gerido agendamento de cópia de segurança** |Cópia de segurança do SQL Server gerida tooAzure suporta agora agendamentos personalizados. Para obter mais informações, consulte [tooMicrosoft de cópia de segurança do SQL Server gerida do Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Para obter um tutorial Olá das capacidades do SQL Server 2016 ao utilizar o Blob storage do Azure, consulte [Tutorial: utilizar o serviço de armazenamento de Blobs do Microsoft Azure Olá com bases de dados do SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 inclui Olá seguintes melhoramentos:

1. **Cópia de segurança e restauro tooAzure**:
   
   * *Cópia de segurança do SQL Server tooURL* tem agora suporte no SQL Server Management Studio. Olá opção tooback segurança tooAzure está agora disponível quando utilizar tarefas de cópia de segurança ou restauro ou o Assistente do plano de manutenção no SQL Server Management Studio. Para obter mais informações, consulte [tooURL de cópia de segurança do SQL Server](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *Servidor gerido cópia de segurança SQL tooAzure* tem novas funcionalidades que permite a gestão de cópia de segurança automatizada. Isto é especialmente útil para automatizar a gestão de cópia de segurança para as instâncias do SQL Server 2014 em execução numa máquina do Azure. Para obter mais informações, consulte [tooMicrosoft de cópia de segurança do SQL Server gerida do Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Cópia de segurança automatizada* fornece automatização adicionais tooautomatically ativar *tooAzure de cópia de segurança do SQL Server gerida* em todos os existentes e novas bases de dados para uma VM do SQL Server no Azure. Para obter mais informações, consulte o artigo [Cópia de Segurança Automatizada para o SQL Server nas Virtual Machines do Azure](virtual-machines-windows-sql-automated-backup.md).
   * Para obter uma descrição geral de todas as opções de Olá para tooAzure de cópia de segurança do SQL Server 2014, consulte [cópia de segurança do SQL Server e de restauro com o serviço de armazenamento de Blobs do Microsoft Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Encriptação**: SQL Server 2014 suporta a encriptação de dados ao criar uma cópia de segurança. Suporta vários algoritmos de encriptação e Olá utilizar osf um certificado ou chave assimétrica. Para obter mais informações, consulte [encriptação da cópia de segurança](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
Para obter informações detalhadas sobre a cópia de segurança do SQL Server e de restauro no SQL Server 2012, consulte [cópia de segurança e restauro de bases de dados (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx).

A partir do SQL Server 2012 SP1 a atualização cumulativa 2, pode fazer cópias de segurança tooand restauro de Olá serviço Blob Storage do Azure. Esta melhoria pode ser utilizado tooback segurança de bases de dados do SQL Server num SQL Server em execução numa máquina Virtual do Azure ou uma instância no local. Para obter mais informações, consulte [cópia de segurança do SQL Server e de restauro com o serviço de armazenamento de Blobs do Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Algumas das vantagens de Olá da utilização do serviço de armazenamento de Blobs do Azure Olá incluem Olá capacidade toobypass Olá 16 limite de disco para discos ligados, facilidade de gestão, disponibilidade direta de Olá da instância de tooanother Olá ficheiro de cópia de segurança de instância do SQL Server em execução numa do Azure máquina virtual ou uma instância no local para fins de recuperação de migração ou um desastre. Para obter uma lista completa dos benefícios toousing um serviço de armazenamento de Blobs do Azure para cópias de segurança do SQL Server, consulte Olá *vantagens* secção [cópia de segurança do SQL Server e de restauro com o serviço de armazenamento de Blobs do Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Para recomendações de melhores práticas e informações de resolução de problemas, consulte [cópia de segurança e restaurar as melhores práticas (serviço de armazenamento de Blobs do Azure)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx).

## <a name="sql-server-2008"></a>SQL Server 2008
Para a cópia de segurança do SQL Server e de restauro no SQL Server 2008 R2, consulte [cópia de segurança e restaurar bases de dados no SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

Para a cópia de segurança do SQL Server e de restauro no SQL Server 2008, consulte [cópia de segurança e restaurar bases de dados no SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Passos seguintes
Se estiver a planear a implementação do SQL Server numa VM do Azure, pode encontrar orientações aprovisionamento no Olá seguir o tutorial: [aprovisionamento de uma Máquina Virtual do SQL Server no Azure com o Azure Resource Manager](virtual-machines-windows-portal-sql-server-provision.md).

Apesar de cópia de segurança e restauro pode ser utilizado toomigrate os dados, existem potencialmente mais fácil dados migração caminhos tooSQL Server numa VM do Azure. Para ver um debate completo de opções de migração e as recomendações, consulte [migrar uma base de dados tooSQL Server numa VM do Azure](virtual-machines-windows-migrate-sql.md).

Rever outros [recursos para executar o SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

