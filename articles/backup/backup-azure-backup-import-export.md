---
title: "aaaAzure cópia de segurança - cópia de segurança Offline ou através de propagação inicial Olá serviço importar/exportar do Azure | Microsoft Docs"
description: "Saiba como cópia de segurança do Azure permite-lhe toosend dados fora da rede de Olá utilizando o serviço de importação/exportação do Azure Olá. Este artigo explica Olá offline seeding dos dados de cópia de segurança inicial Olá através do serviço Olá exportar de importação do Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Fluxo de trabalho de cópias de segurança offline no Azure Backup
Cópia de segurança do Azure tem vários resulta numa eficiência incorporada que guardam os custos de armazenamento e de rede durante Olá iniciais cópias de segurança completas de tooAzure de dados. As cópias de segurança completas iniciais normalmente transferem grandes quantidades de dados e necessitam de mais largura de banda quando comparado com toosubsequent cópias de segurança que são transferidos só, como Olá deltas/incrementais. Cópia de segurança do Azure comprime cópias de segurança inicial Olá. Através do processo de Olá de propagação offline, cópia de segurança do Azure pode utilizar discos tooupload Olá comprimido inicial de dados de cópia de segurança offline tooAzure.  

Olá offline seeding o processo de cópia de segurança do Azure está totalmente integrado com Olá [serviço importar/exportar do Azure](../storage/common/storage-import-export-service.md) que permite-lhe tootransfer dados tooAzure através da utilização de discos. Se tiver terabytes (TBs) de dados de cópia de segurança iniciais que necessita de toobe transferido através de uma rede de latência alta e baixa largura de banda, pode utilizar Olá offline seeding fluxo de trabalho tooship Olá cópia de segurança inicial num ou mais unidades de disco rígido tooan datacenter do Azure. Este artigo fornece uma descrição geral dos passos de Olá que conclua este fluxo de trabalho.

## <a name="overview"></a>Descrição geral
Com Olá offline seeding capacidade de cópia de segurança do Azure e importar/exportar do Azure, é simples tooupload Olá dados offline tooAzure através da utilização de discos. Em vez de transferir a cópia inicial completa de Olá rede Olá, dados de cópia de segurança de Olá são escritos tooa *localização de transição*. Localização de transição Olá cópia toohello esteja concluída, utilizando a ferramenta de importação/exportação do Azure Olá, estes dados são escritos tooone ou SATA mais unidades, dependendo da quantidade de Olá de dados. Estas unidades são eventualmente fornecido toohello mais próximo do datacenter do Azure.

Olá [da cópia de segurança do Azure (e mais tarde) de atualização de Agosto de 2016](http://go.microsoft.com/fwlink/?LinkID=229525) inclui Olá *ferramenta de preparação de disco do Azure*, com o nome AzureOfflineBackupDiskPrep, que:

* Ajuda-o a preparar a unidades de importação do Azure utilizando a ferramenta de importação/exportação do Azure Olá.
* Cria automaticamente uma tarefa de importação do Azure para Olá serviço importar/exportar do Azure no Olá [portal clássico do Azure](https://manage.windowsazure.com) como toocreating oposição ao hello mesmo manualmente com versões anteriores do Backup do Azure.

Após a conclusão do carregamento de Olá do Olá tooAzure de dados de cópia de segurança, cópias de segurança do Azure copia o Cofre de cópias de segurança Olá dados de cópia de segurança toohello e Olá cópias de segurança incrementais.

> [!NOTE]
> Olá toouse ferramenta de preparação de disco do Azure, certifique-se de que instalou a atualização de Agosto de 2016 Olá da cópia de segurança do Azure (ou posterior) e executar todos os passos de Olá de fluxo de trabalho Olá com o mesmo. Se estiver a utilizar uma versão antiga do Backup do Azure, pode preparar a unidade SATA Olá utilizando a ferramenta de importação/exportação do Azure de Olá conforme detalhado nas secções posteriores deste artigo.
>
>

## <a name="prerequisites"></a>Pré-requisitos
* [Familiarize-se com o fluxo de trabalho do Olá do Azure para importar/exportar](../storage/common/storage-import-export-service.md).
* Antes de iniciar o fluxo de trabalho Olá, certifique-se seguinte Olá:
  * Foi criado um cofre de cópia de segurança do Azure.
  * As credenciais do cofre tiverem sido transferidas.
  * agente de cópia de segurança do Azure Olá foi instalado no cliente do Windows Server/Windows ou servidor do System Center Data Protection Manager e o computador de Olá está registado no Cofre de cópia de segurança do Azure Olá.
* [Transferir as definições de ficheiros de publicação do Azure Olá](https://manage.windowsazure.com/publishsettings) no computador de Olá partir do qual planeia tooback dos seus dados.
* Prepare uma localização de transição, que pode ser uma partilha de rede ou o disco adicional no computador de Olá. Olá localização de transição é armazenamento transitório e é utilizado temporariamente durante este fluxo de trabalho. Certifique-se de que Olá localização de transição tem suficiente toohold de espaço em disco a cópia inicial. Por exemplo, se estiver a tentar tooback configurar um servidor de ficheiros de 500 GB, certifique-se essa área de transição de Olá menos de 500 GB. (Uma quantidade menor é utilizada devida toocompression.)
* Certifique-se de que está a utilizar uma unidade suportada. Apenas 2,5 polegada SSD ou 2,5 ou 3.5 polegadas SATA II/III interno unidades de disco rígido são suportados para utilização com Olá serviço de importação/exportação. Pode utilizar unidades de disco rígido segurança too10 TB. Verifique Olá [documentação do serviço do Azure para importar/exportar](../storage/common/storage-import-export-service.md#hard-disk-drives) para Olá conjunto mais recente de unidades Olá serviço suporta.
* Ativar o BitLocker Olá computador toowhich escritor de unidade SATA Olá está ligado.
* [Transferir a ferramenta de importação/exportação do Azure Olá](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) escritor de unidade SATA toowhich Olá toohello computador está ligado. Este passo não é necessário se tiver transferido e instalado Olá Agosto de 2016 atualização da cópia de segurança do Azure (ou posterior).

## <a name="workflow"></a>Fluxo de trabalho
informações de Olá nesta secção ajuda-o a concluir o fluxo de trabalho de cópia de segurança offline de Olá, para que os dados podem ser fornecidos tooan datacenter do Azure e carregada tooAzure armazenamento. Se tiver dúvidas sobre o serviço de importação de Olá ou em qualquer aspeto do processo de Olá, consulte Olá [descrição geral do serviço de importação](../storage/common/storage-import-export-service.md) documentação referenciada anteriormente.

### <a name="initiate-offline-backup"></a>Iniciar a cópia de segurança offline
1. Quando agendar uma cópia de segurança, verá Olá seguinte ecrã (no Windows Server, o cliente do Windows ou o System Center Data Protection Manager).

    ![Ecrã de importação](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    Eis ecrã correspondente Olá no System Center Data Protection Manager: <br/>
    ![Ecrã de importação do DPM](./media/backup-azure-backup-import-export/dpmoffline.png)

    Descrição de Olá de entradas de Olá é o seguinte:

    * **Localização de transição**: Olá armazenamento temporário localização toowhich Olá cópia de segurança inicial é escrita. Isto pode ser num computador local ou uma partilha de rede. Se o computador de cópia de Olá e o computador de origem são diferentes, recomendamos que especifica o caminho de rede completa Olá de Olá localização de transição.
    * **Nome da tarefa de importação do Azure**: Olá número exclusivo que importar do Azure Backup do Azure e do serviço controlam transferência Olá de dados enviados no tooAzure de discos.
    * **Definições de publicação do Azure**: ficheiro um XML que contém informações sobre o perfil de subscrição. Também contém as credenciais seguras que estão associadas a sua subscrição. Pode [transferir ficheiro Olá](https://manage.windowsazure.com/publishsettings). Fornecer Olá caminho local toohello publicar o ficheiro de definições.
    * **ID de subscrição do Azure**: Olá ID de subscrição do Azure para a subscrição de olá onde pretende que a tarefa de importação do Azure de Olá tooinitiate. Se tiver várias subscrições do Azure, utilize Olá ID de subscrição de Olá que pretende que o tooassociate com a tarefa de importação de Olá.
    * **Conta de armazenamento do Azure**: conta de armazenamento de tipo clássico Olá no Olá fornecido a subscrição do Azure que será associada a tarefa de importação do Azure Olá.
    * **Contentor de armazenamento do Azure**: nome de Olá do blob de armazenamento de destino Olá no Olá conta do storage do Azure onde os dados desta tarefa são importados.

    > [!NOTE]
    > Se tiver registado tooan o servidor dos serviços de recuperação do Azure do Cofre de Olá [portal do Azure](https://portal.azure.com) para as suas cópias de segurança e não existem numa subscrição do fornecedor de solução em nuvem (CSP), pode ainda criar uma conta de armazenamento de tipo clássico de Olá Portal do Azure e utilizá-la para o fluxo de trabalho do Olá cópia de segurança offline.
    >
    >

     Guardar todas as informações neste porque necessita de tooentê-lo novamente nos seguintes passos. Apenas Olá *localização de transição* é necessário se utilizar discos de Olá de tooprepare de ferramenta de preparação de disco do Azure de Olá.    
2. Concluir o fluxo de trabalho Olá e, em seguida, selecione **cópia de segurança agora** na cópia de Olá cópia de segurança do Azure gestão consola tooinitiate Olá-cópia de segurança offline. cópia de segurança inicial Olá é escrito na área de transição de toohello como parte deste passo.

    ![Cópia de segurança agora](./media/backup-azure-backup-import-export/backupnow.png)

    fluxo de trabalho do toocomplete Olá correspondente no System Center Data Protection Manager, clique com botão direito Olá **grupo de proteção**e, em seguida, escolha Olá **criar ponto de recuperação** opção. Em seguida, escolha o Olá **proteção Online** opção.

    ![Agora cópia de segurança do DPM](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Depois de concluída a operação de Olá, Olá localização de transição está pronto toobe utilizado para a preparação de disco.

    ![Progresso da cópia de segurança](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>Preparar uma unidade SATA e criar uma tarefa de importação do Azure, utilizando a ferramenta de preparação de disco do Azure de Olá
a ferramenta de preparação de disco do Azure Olá está disponível no diretório de instalação do agente de serviços de recuperação Olá (atualizar de Agosto de 2016 e posterior) no seguinte caminho de Olá.

   *\Microsoft* *azure* *recuperação* *serviços* * Agent\Utils\*

1. Aceda toohello diretório e Olá cópia **AzureOfflineBackupDiskPrep** computador cópia tooa de diretório no qual Olá toobe unidades preparado estão montados. Certifique-se a seguinte Olá com o computador de cópia de toohello regard:

    * Olá cópia computador pode aceder Olá localização para o fluxo de trabalho de offline seeding Olá de teste utilizando o mesmo caminho que foi fornecido no Olá de rede de Olá **iniciar cópia de segurança offline** fluxo de trabalho.
    * O BitLocker estiver ativado no computador de Olá.
    * computador Olá pode aceder a Olá portal do Azure.

    Se necessário, computador de cópia de Olá pode Olá igual ao computador de origem Olá.
2. Abra uma linha de comandos elevada no computador de cópia de Olá com o diretório da ferramenta de preparação de disco do Azure Olá como diretório atual Olá e execute Olá os seguintes comandos:

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | Parâmetro | Descrição |
    | --- | --- |
    | s:&lt;*caminho de localização de transição*&gt; |Entrada obrigatória que tenha utilizado tooprovide Olá caminho toohello localização que introduziu no Olá de transição **iniciar cópia de segurança offline** fluxo de trabalho. |
    | p:&lt;*tooPublishSettingsFile de caminho*&gt; |Entrada opcional que tenha utilizado tooprovide Olá caminho toohello **definições de publicação do Azure** ficheiro que introduziu no Olá **iniciar cópia de segurança offline** fluxo de trabalho. |

    > [!NOTE]
    > Olá &lt;caminho tooPublishSettingFile&gt; valor é obrigatório quando o computador de cópia de Olá e o computador de origem são diferentes.
    >
    >

    Quando executar o comando de Olá, ferramenta Olá pedidos de seleção de Olá da tarefa de importação do Azure Olá que corresponde ao toohello unidades que precisam de toobe preparado. Se apenas uma tarefa de importação único está associada a Olá fornecido a localização de transição, verá um ecrã semelhante Olá um que se segue.

    ![Entrada de ferramenta de preparação de disco do Azure](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Introduza a letra de unidade de Olá sem Olá à direita vírgula para disco montado Olá que pretende que tooprepare para tooAzure de transferência. Indique confirmação para a formatação Olá da unidade de Olá quando lhe for pedido.

    ferramenta de Olá, em seguida, começa disco de Olá tooprepare com dados de cópia de segurança de Olá. Poderá ser necessário tooattach discos adicionais quando lhe for pedido pela ferramenta de Olá no caso de Olá fornecido disco tem espaço suficiente para dados de cópia de segurança de Olá. <br/>

    No final de Olá de execução da ferramenta de Olá com êxito, um ou mais discos que forneceu estão preparados para tooAzure de envio. Além disso, uma tarefa de importação com o nome de Olá fornecida durante Olá **iniciar cópia de segurança offline** fluxo de trabalho é criado no Olá portal clássico do Azure. Por fim, Olá ferramenta apresenta Olá envio endereço toohello datacenter do Azure onde os discos de Olá têm toobe fornecido e Olá a tarefa de importação do ligação toolocate Olá no Olá portal clássico do Azure.

    ![Preparação de disco do Azure completa](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. Incorporadas Olá discos toohello endereço essa ferramenta Olá fornecida e manter Olá controlo número para consulta futura.<br/>

5. Quando acede toohello associar essa ferramenta Olá apresentada, consulte conta de armazenamento do Azure Olá que especificou no Olá **iniciar cópia de segurança offline** fluxo de trabalho. Aqui, pode ver a tarefa de importação de Olá criado recentemente na Olá **importar/EXPORTAR** separador Olá da conta de armazenamento.

    ![Tarefa de importação criada](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. Clique em **informações de envio** na parte inferior de Olá de Olá página tooupdate seu contacto detalhes conforme mostrado no seguinte ecrã de Olá. A Microsoft utiliza este tooship informações sua tooyou back discos depois Olá importar tarefa estiver concluída.

    ![Informações de contacto](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Introduza Olá envio detalhes no seguinte ecrã de Olá. Fornecer Olá **operadora de entrega** e **controlo número** detalhes que correspondem a discos de toohello que vem incluído toohello datacenter do Azure.

    ![Informações de envio](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>Fluxo de trabalho Olá concluída
Após a conclusão da tarefa de importação de Olá, dados de cópia de segurança iniciais estão disponíveis na sua conta de armazenamento. Olá agente dos serviços de recuperação, em seguida, conteúdo de Olá cópias dos dados Olá este Cofre de cópia de segurança de toohello de conta ou dos serviços de recuperação cofre, optando-se aplicável. No tempo de cópia de segurança Olá agendado o próximo, o agente de cópia de segurança do Azure Olá efetua cópia de segurança incremental Olá através de cópia de segurança inicial Olá.

> [!NOTE]
> Olá seguintes secções aplicam-se toousers de versões anteriores do Backup do Azure, que não têm a ferramenta de preparação de disco do Azure de toohello de acesso.
>
>

### <a name="prepare-a-sata-drive"></a>Preparar uma unidade SATA
1. Transferir Olá [ferramenta de importação/exportação do Microsoft Azure](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) toohello computador de cópia. Certifique-se de que Olá localização de transição é acessível a partir do computador Olá no qual planeia toorun conjunto seguinte de Olá de comandos. Se necessário, computador de cópia de Olá pode Olá igual ao computador de origem Olá.

2. Deszipe o ficheiro de WAImportExport.zip Olá. Execute a ferramenta de WAImportExport Olá, que formata a unidade SATA Olá, escreve a unidade SATA Olá dados de cópia de segurança toohello e encripta-lo. Antes de executar Olá comando a seguir, certifique-se de que o BitLocker estiver ativado no computador de Olá. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Se instalou a atualização de Agosto de 2016 Olá da cópia de segurança do Azure (ou posterior), certifique-se de que Olá localização que introduziu de transição é Olá igual ao hello um Olá **cópia de segurança agora** ecrã e contém ficheiros AIB e BLOBs de Base.
    >
    >

| Parâmetro | Descrição |
| --- | --- |
| /j: <*JournalFile*> |Olá caminho toohello diário de alterações o ficheiro. Cada unidade tem de ter exatamente um ficheiro de diário de alterações. ficheiros do diário de alterações de Olá não devem ser numa unidade de destino de Olá. extensão de ficheiro do diário de alterações de Olá é .jrn e é criado como parte da execução deste comando. |
| formado: <*SessionId*> |ID de sessão de Olá identifica uma sessão de cópia. É utilizado tooensure recuperação exata de uma sessão de cópia interrompida. Os ficheiros que são copiados numa sessão de cópia são armazenados num diretório com o nome após o ID de sessão de Olá na unidade de destino Olá. |
| /SK: <*StorageAccountKey*> |chave da conta Olá para Olá conta toowhich Olá os dados de armazenamento é importado. Olá de toobe do chave necessidades de Olá igual ao foi introduzido durante a criação do grupo de proteção/política de cópia de segurança. |
| / BlobType |tipo de Olá de blob. Este fluxo de trabalho for bem sucedida apenas se **PageBlob** está especificado. Isto não é a opção predefinida de Olá e deve ser mencionado neste comando. |
| /t: <*TargetDriveLetter*> |letra de unidade de Olá sem Olá à direita vírgula da unidade de disco rígido Olá destino para a sessão de cópia atual de Olá. |
| /Format |unidade do Olá opção tooformat Olá. Especificar este parâmetro quando precisa de unidade de Olá toobe formatado; caso contrário, omita-lo. Antes de ferramenta Olá formatos unidade Olá pede ao utilizador uma confirmação da consola de Olá. toosuppress Olá confirmação, especifique o parâmetro de /silentmode Olá. |
| / encriptar |unidade do Olá opção tooencrypt Olá. Quando a unidade de Olá ainda não foi encriptada com BitLocker e as suas necessidades toobe encriptado pela ferramenta de Olá de especificar este parâmetro. Se a unidade de Olá já foi encriptada com BitLocker, omita este parâmetro, especifique o parâmetro de /bk Olá e fornecer a chave do BitLocker existente Olá. Se especificar o parâmetro de /format Olá, tem também de especificar Olá / encriptar o parâmetro. |
| /srcdir: <*SourceDirectory*> |diretório de origem Olá que contém ficheiros toobe copiados toohello unidade de destino. Certifique-se de que nome do diretório especificado Olá tem um caminho completo em vez de relativo. |
| /dstdir: <*DestinationBlobVirtualDirectory*> |Olá caminho toohello destino diretório virtual na sua conta do storage do Azure. Estar toouse se os nomes dos contentores válidos quando especificar diretórios virtuais do destino Olá ou blobs. Tenha em atenção que os nomes dos contentores têm de estar em minúsculas.  Este nome de contentor deve ser Olá que introduziu durante a criação do grupo de proteção/política de cópia de segurança. |

> [!NOTE]
> Na pasta de WAImportExport Olá que captura Olá informações todo do fluxo de trabalho Olá, é criado um ficheiro de diário de alterações. É necessário este ficheiro quando cria uma tarefa de importação no Olá portal do Azure.
>
>

  ![Saída do PowerShell](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Criar uma tarefa de importação no Olá portal do Azure
1. Aceda a conta de armazenamento tooyour no Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **importar/exportar**e, em seguida, **criar tarefa de importação** no painel de tarefas Olá.

    ![Separador Olá portal do Azure para importar/exportar](./media/backup-azure-backup-import-export/azureportal.png)

2. No passo 1 do Assistente de Olá, indicam que preparou a unidade e de que tem o ficheiro de diário de alterações de disco Olá disponível.

3. No passo 2 do Assistente de Olá, forneça as informações de contacto para Olá quem é responsável por esta tarefa de importação.

4. No passo 3, carregar ficheiros do diário de unidade Olá que obteve na secção anterior Olá.

5. Passo 4, introduza um nome descritivo para a tarefa de importação de Olá que introduziu durante a criação do grupo de proteção/política de cópia de segurança. nome de Olá que introduziu pode conter apenas letras minúsculas, números, hífenes e carateres de sublinhado, tem de começar com uma letra e não pode conter espaços. nome de Olá que escolher é utilizado tootrack as tarefas enquanto estiverem em curso e depois de serem resolvidos.

6. Em seguida, selecione a região de centro de dados da lista de Olá. região do Centro de dados de Olá indica Olá o Centro de dados e o endereço toowhich tem de enviar o pacote.

    ![Selecione a região do Centro de dados](./media/backup-azure-backup-import-export/dc.png)

7. No passo 5, selecione a retorno operadora Olá lista e introduza o seu número de conta operadora. A Microsoft utiliza esta conta tooship a unidades de fazer uma cópia tooyou depois de concluída a tarefa de importação.

8. Envie Olá disco e introduza Olá número tootrack Olá Estado shipment Olá de controlo. Depois do disco de Olá chega no Centro de dados de Olá, é copiado toohello conta de armazenamento e estado de Olá é atualizado.

    ![Estado concluído](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>Fluxo de trabalho Olá concluída
Depois de dados de cópia de segurança inicial Olá estão disponíveis na sua conta de armazenamento, hello agente dos serviços de recuperação do Microsoft Azure copia o conteúdo de Olá dos dados de Olá deste cofre de cópia de segurança de toohello de conta ou um cofre dos serviços de recuperação, o que for aplicável. Na agenda seguinte Olá tempo de cópia de segurança, Olá agente de cópia de segurança do Azure efetua a cópia de segurança incremental Olá através de cópia de segurança inicial Olá.

## <a name="next-steps"></a>Passos seguintes
* Para quaisquer perguntas sobre o fluxo de trabalho do Olá importar/exportar do Azure, consulte demasiado[utilizar Olá importação/exportação do Microsoft Azure service tootransfer dados tooBlob armazenamento](../storage/common/storage-import-export-service.md).
* Consulte a secção de cópia de segurança offline toohello da cópia de segurança do Azure Olá [FAQ](backup-azure-backup-faq.md) para quaisquer perguntas sobre o fluxo de trabalho Olá.
