---
title: erros de aaaTroubleshoot ao eliminar as contas do storage do Azure, contentores ou VHDs | Microsoft Docs
description: Resolver erros ao eliminar as contas do storage do Azure, contentores ou VHDs
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Resolver erros ao eliminar as contas do storage do Azure, contentores ou VHDs

Poderá receber erros quando tenta toodelete uma conta do storage do Azure, um contentor ou um disco rígido virtual (VHD) em Olá [portal do Azure](https://portal.azure.com). Este artigo fornece resolução orientações toohelp resolve Olá problema numa implementação do Azure Resource Manager.

Se este artigo não resolver o problema do Azure, visite Olá fóruns do Azure no [MSDN e Stack Overflow](https://azure.microsoft.com/support/forums/). Pode publicar o seu problema nestes fóruns ou too@AzureSupport no Twitter. Além disso, pode ficheiro um pedido de suporte do Azure ao selecionar **obter suporte** no Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Sintomas
### <a name="scenario-1"></a>Cenário 1
Quando tenta toodelete um VHD numa conta do storage numa implementação do Resource Manager, receberá Olá seguir a mensagem de erro:

**Falha ao blob toodelete 'vhds/BlobName.vhd'. Erro: Não existe atualmente uma concessão no blob Olá e não foi especificado nenhum ID de concessão no pedido de Olá.**

Este problema pode ocorrer porque uma máquina virtual (VM) tem uma concessão no Olá VHD que está a tentar toodelete.

### <a name="scenario-2"></a>Cenário 2
Quando tenta toodelete um contentor numa conta do storage numa implementação do Resource Manager, receberá Olá seguir a mensagem de erro:

**Falha ao contentor de armazenamento toodelete 'vhds'. Erro: Não existe atualmente uma concessão no contentor de Olá e não foi especificado nenhum ID de concessão no pedido de Olá.**

Este problema pode ocorrer porque o contentor de Olá tem uma imagem VHD que estiver bloqueada no estado de concessão de Olá.

### <a name="scenario-3"></a>Cenário 3
Quando tenta toodelete uma conta de armazenamento numa implementação do Resource Manager, receberá Olá seguir a mensagem de erro:

**Falha na conta de armazenamento toodelete 'StorageAccountName'. Erro: não é possível eliminar a conta de armazenamento Olá de devido tooits artefactos estão a ser utilizado.**

Este problema pode ocorrer porque a conta de armazenamento Olá contém uma imagem VHD que está no estado de concessão de Olá.

## <a name="solution"></a>Solução 
tooresolve estes problemas, tem de identificar Olá VHD que está a causar erro Olá e Olá associado à VM. Em seguida, anular a exposição Olá VHD de Olá VM (para os discos de dados) ou eliminar Olá VM que está a utilizar Olá VHD (discos do SO). Isto remove a concessão de Olá Olá VHD e permite que toobe eliminado. 

toodo, utilize um dos seguintes métodos de Olá:

### <a name="method-1---use-azure-storage-explorer"></a>Método 1 - utilizar o Explorador de armazenamento do Azure

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Passo 1 identificar Olá VHD que impedem a eliminação da conta de armazenamento Olá

1. Ao eliminar a conta de armazenamento Olá, receberá uma caixa de diálogo de mensagem, tais como o seguinte Olá: 

    ![mensagem ao eliminar a conta de armazenamento Olá](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Verifique Olá **disco URL** conta de armazenamento de Olá tooidentify e Olá VHD que impede a eliminar a conta de armazenamento de Olá. No seguinte exemplo de Olá, cadeia antes de Olá ". w" é o nome de conta do storage Olá, não sendo "SCCM2012-2015-08-28.vhd" nome do VHD Olá.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>Olá de eliminação do passo 2 VHD utilizando o Explorador de armazenamento do Azure

1. Transferir e instalar versão mais recente do Olá do [Explorador de armazenamento do Azure](http://storageexplorer.com/). Esta ferramenta é uma aplicação autónoma da Microsoft permite-lhe tooeasily trabalho com dados de armazenamento do Azure no Windows, macOS e Linux.
2. Abra o Explorador de armazenamento do Azure, selecione ![ícone de conta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) na barra de esquerdo Olá, selecione o seu ambiente do Azure e, em seguida, inicie sessão.

3. Selecione todas as subscrições ou subscrição Olá que contém a conta de armazenamento de Olá que pretende toodelete.

    ![Adicionar subscrição](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Aceda a conta de armazenamento de toohello que foi obtidas Olá disco URL anterior, selecione Olá **contentores de BLOBs** > **vhds** e procure Olá VHD que impede a conta de armazenamento de Olá de eliminação.
5. Se for encontrado Olá VHD, verifique Olá **nome da VM** Olá toofind de coluna VM que está a utilizar este VHD.

    ![Verificação de vm](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Remova concessão Olá Olá VHD utilizando o portal do Azure. Para obter mais informações, consulte [concessão de Olá remover de Olá VHD](#remove-the-lease-from-the-vhd). 

7. Aceda toohello Explorador de armazenamento do Azure, clique com o botão direito Olá VHD e, em seguida, selecione eliminar.

8. Elimine conta do storage Olá.

### <a name="method-2---use-azure-portal"></a>Método 2 - utiliza o portal do Azure 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Passo 1: Identificar Olá VHD que impedem a eliminação da conta de armazenamento Olá

1. Ao eliminar a conta de armazenamento Olá, receberá uma caixa de diálogo de mensagem, tais como o seguinte Olá: 

    ![mensagem ao eliminar a conta de armazenamento Olá](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Verifique Olá **disco URL** conta de armazenamento de Olá tooidentify e Olá VHD que impede a eliminar a conta de armazenamento de Olá. No seguinte exemplo de Olá, cadeia antes de Olá ". w" é o nome de conta do storage Olá, não sendo "SCCM2012-2015-08-28.vhd" nome do VHD Olá.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
3. No menu do Hub de Olá, selecione **todos os recursos**. Aceda a conta de armazenamento toohello e, em seguida, selecione **Blobs** > **vhds**.

    ![Captura de ecrã do portal de Olá, com a conta de armazenamento de Olá e contentor de "vhds" Olá realçado](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Localize Olá VHD que são obtidos a partir do URL de disco Olá anteriormente. Em seguida, determinar qual a VM está a utilizar Olá VHD. Normalmente, pode determinar que VM contém Olá VHD ao verificar o nome do Olá VHD:

VM no modelo de programação do Resource Manager

   * Discos de SO, geralmente, siga esta Convenção de nomenclatura: VMName-aaaa-MM-DD-HHMMSS.vhd
   * Os discos de dados, geralmente, siga esta Convenção de nomenclatura: VMName-aaaa-MM-DD-HHMMSS.vhd

VM no modelo de programação clássico

   * Discos de SO, geralmente, siga esta Convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * Os discos de dados, geralmente, siga esta Convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>Passo 2: Remover concessão Olá Olá VHD

[Remover a concessão de Olá Olá VHD](#remove-the-lease-from-the-vhd)e, em seguida, elimine a conta de armazenamento Olá.

## <a name="what-is-a-lease"></a>O que é uma concessão?
Uma concessão é um bloqueio que pode ser utilizados toocontrol-BLOBs acesso tooa (por exemplo, um VHD). Quando um blob é nos concessionados, apenas os proprietários de Olá de concessão de Olá podem aceder a BLOBs Olá. Uma concessão é importante para Olá seguintes motivos:

* Impede a danos nos dados se proprietários vários tente toowrite toohello mesma parte do blob de Olá na Olá mesmo tempo.
* Impede que o blob de Olá que está a ser eliminado se algo está ativamente a ser utilizado (por exemplo, uma VM).
* Impede que conta de armazenamento Olá que está a ser eliminado se algo está ativamente a ser utilizado (por exemplo, uma VM).

### <a name="remove-hello-lease-from-hello-vhd"></a>Remover a concessão de Olá Olá VHD
Se Olá VHD é um disco de SO, tem de eliminar concessão do Olá VM tooremove Olá:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. No Olá **Hub** menu, selecione **máquinas virtuais**.
3. Selecione Olá VM que contém uma concessão no Olá VHD.
4. Certifique-se de que nada está ativamente a utilizar máquinas virtuais de Olá e que que já não precisa de Olá máquina virtual.
5. Na parte superior de Olá de Olá **detalhes VM** painel, selecione **eliminar**e, em seguida, clique em **Sim** tooconfirm.
6. Olá VM deve ser eliminado, mas pode ser mantida Olá VHD. No entanto, Olá VHD já não deve ter uma concessão no mesmo. Pode demorar alguns minutos para Olá concessão toobe lançada. tooverify Olá concessão for lançada, visite demasiado**todos os recursos** > **nome da conta de armazenamento** > **Blobs**  >  **vhds**. No Olá **Blob propriedades** painel, Olá **estado de concessão** o valor deve ser **Unlocked**.

Se Olá VHD for um disco de dados, desanexe Olá VHD de concessão de Olá Olá VM tooremove:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. No Olá **Hub** menu, selecione **máquinas virtuais**.
3. Selecione Olá VM que contém uma concessão no Olá VHD.
4. Selecione **discos** no Olá **detalhes VM** painel.
5. Selecione o disco de dados de Olá que contém uma concessão no Olá VHD. Pode determinar que esteja anexado VHD no disco Olá verificando Olá URL de Olá VHD.
6. Determine com certainty nada ativamente está a utilizar o disco de dados de Olá.
7. Clique em **anulação de exposições** no Olá **disco detalhes** painel.
8. disco Olá agora deve ser desligado do Olá VM e Olá VHD já não deve ter uma concessão no mesmo. Pode demorar alguns minutos para Olá concessão toobe lançada. foi lançado tooverify Olá concessão, visite demasiado**todos os recursos** > **nome da conta de armazenamento** > **Blobs**  >  **vhds**. No Olá **Blob propriedades** painel, Olá **estado de concessão** o valor deve ser **Unlocked**.

## <a name="next-steps"></a>Passos seguintes
* [Eliminar uma conta de armazenamento](storage-create-storage-account.md#delete-a-storage-account)
* [Como toobreak Olá bloqueado concessão do blob storage no Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
