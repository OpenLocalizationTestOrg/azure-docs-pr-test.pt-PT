---
title: "aaaUse moderna de cópia de segurança de armazenamento com o servidor de cópia de segurança do Azure v2 | Microsoft Docs"
description: "Saiba mais sobre as novas funcionalidades Olá no servidor de cópia de segurança do Azure v2. Este artigo descreve como tooupgrade a instalação do servidor de cópia de segurança."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Adicionar armazenamento tooAzure v2 do servidor de cópia de segurança

V2 de servidor do Backup do Azure é fornecido com o System Center 2016 proteção Manager moderna cópia de segurança do armazenamento de dados. Armazenamento de cópia de segurança moderna oferece poupança de armazenamento de 50 por cento, cópias de segurança que são armazenamento três vezes, mais rápido e eficiente. Também proporciona armazenamento com suporte para a carga de trabalho. 

> [!NOTE]
> toouse moderna armazenamento de cópia de segurança, tem de executar v2 do servidor de cópia de segurança no Windows Server 2016. Se executar o servidor de cópia de segurança v2 numa versão anterior do Windows Server, servidor de cópia de segurança do Azure não é possível tirar partido do armazenamento de cópia de segurança moderna. Em vez disso, o que protege cargas de trabalho como acontece com o servidor de cópia de segurança v1. Para obter mais informações, consulte a versão do servidor de cópia de segurança Olá [matriz proteção](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Volumes no servidor de cópia de segurança v2

Cópia de segurança servidor v2 aceita volumes de armazenamento. Quando adiciona um volume, o servidor de cópia de segurança formata Olá volume tooResilient sistema de ficheiros (ReFS), que necessita de armazenamento de cópia de segurança moderna. tooadd um volume e tooexpand-lo mais tarde se for necessário, sugerimos que utilize este fluxo de trabalho:

1.  Configure o servidor de cópia de segurança v2 numa VM.
2.  Crie um volume num disco virtual num agrupamento de armazenamento:
    1.  Adicione um agrupamento de armazenamento do disco tooa e criar um disco virtual com o esquema simples.
    2.  Adicione quaisquer discos adicionais e expandir disco virtual Olá.
    3.  Crie volumes no disco virtual Olá.
3.  Adicione Olá volumes tooBackup servidor.
4.  Configure o armazenamento com suporte para a carga de trabalho.

## <a name="create-a-volume-for-modern-backup-storage"></a>Criar um volume de armazenamento de cópia de segurança moderna

Com o servidor de cópia de segurança v2 volumes como armazenamento de disco pode ajudar a manter o controlo sobre o armazenamento. Um volume pode ser um único disco. No entanto, se quiser armazenamento tooextend Olá futuras, crie um volume fora de um disco que criou, utilizando os espaços de armazenamento. Isto pode ajudar a se pretender o volume de Olá tooexpand para armazenamento de cópia de segurança. Esta secção oferece melhores práticas para criar um volume com esta configuração.

1. No Gestor de servidor, selecione **File and Storage Services** > **Volumes** > **agrupamentos de armazenamento**. Em **discos físicos**, selecione **novo agrupamento de armazenamento**. 

    ![Criar um novo agrupamento de armazenamento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. No Olá **tarefas** caixa pendente, selecione **novo disco Virtual**.

    ![Adicionar um disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Selecione o agrupamento de armazenamento Olá e, em seguida, selecione **adicionar disco físico**.

    ![Adicionar um disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Selecione o disco físico Olá e, em seguida, selecione **expandir disco Virtual**.

    ![Expandir disco virtual Olá](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Selecione o disco virtual Olá e, em seguida, selecione **Novo Volume**.

    ![Crie um novo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. No Olá **selecione Olá servidor e disco** caixa de diálogo, o servidor de Olá selecione e o disco novo Olá. Em seguida, selecione **seguinte**.

    ![Selecione o servidor de Olá e o disco](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Adicione armazenamento em disco volumes tooBackup servidor

tooadd um tooBackup de volume de servidor, no Olá **gestão** painel, reanalisar armazenamento Olá e, em seguida, selecione **adicionar**. É apresentada uma lista de todos os Olá volumes disponíveis toobe adicionado para armazenamento de servidor de cópia de segurança. Depois de volumes disponíveis são adicionadas toohello lista de volumes selecionados, pode conceder-lhes toohelp um nome amigável geri-los. Estes volumes tooReFS pelo servidor de cópia de segurança pode utilizar os benefícios de Olá de armazenamento de cópia de segurança moderna, selecione de tooformat **OK**.

![Adicionar a Volumes disponíveis](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Configurar o armazenamento com suporte para a carga de trabalho

Com o armazenamento com suporte para a carga de trabalho, pode selecionar os volumes de Olá preferentially armazenam determinados tipos de cargas de trabalho. Por exemplo, pode definir volumes dispendiosas que suportam um número elevado de operações de entrada/saída por segundo (IOPS) toostore apenas Olá cargas de trabalho que necessitam de cópias de segurança frequentes, elevado volume. Um exemplo é o SQL Server com registos de transações. Outras cargas de trabalho que são uma cópia de segurança com menos frequência, como VMs, podem ser feitas toolow custo volumes.

### <a name="update-dpmdiskstorage"></a>Atualização DPMDiskStorage

Pode configurar o armazenamento com suporte para a carga de trabalho utilizando o cmdlet do PowerShell Olá Update-DPMDiskStorage, que atualiza as propriedades de Olá de um volume no agrupamento de armazenamento Olá num servidor do Data Protection Manager.

Sintaxe:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Olá seguinte captura de ecrã mostra Olá atualização DPMDiskStorage cmdlet na janela do PowerShell Olá.

![Olá DPMDiskStorage de atualização de comando na janela do PowerShell Olá](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

alterações de Olá efetuadas através do PowerShell são refletidas no Olá consola do administrador do servidor de cópia de segurança.

![Discos e volumes de Olá consola do administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Passos seguintes
Depois de instalar o servidor de cópia de segurança, saiba como tooprepare seu servidor, ou começar a proteger uma carga de trabalho.

- [Preparar as cargas de trabalho do servidor de cópia de segurança](backup-azure-microsoft-azure-backup.md)
- [Utilizar o servidor de cópia de segurança tooback configurar um servidor VMware](backup-azure-backup-server-vmware.md)
- [Utilizar o servidor de cópia de segurança tooback cópias de segurança do SQL Server](backup-azure-sql-mabs.md)

