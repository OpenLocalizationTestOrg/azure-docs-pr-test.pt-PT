---
title: aaaInstall StorSimple adaptador para o SharePoint | Microsoft Docs
description: "Descreve como tooinstall e configurar ou remover Olá adaptador StorSimple para SharePoint num farm de servidores do SharePoint."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Instalar e configurar Olá StorSimple adaptador para o SharePoint
## <a name="overview"></a>Descrição geral
Olá StorSimple adaptador para o SharePoint é um componente que lhe permite fornecer flexíveis de armazenamento do Microsoft Azure StorSimple e farms de servidores de tooSharePoint de proteção de dados. Pode utilizar Olá adaptador toomove objeto grande binário (BLOB) conteúdo Olá do SQL Server bases de dados de conteúdo toohello Microsoft Azure StorSimple híbridos na nuvem dispositivo de armazenamento.

Olá StorSimple adaptador para o SharePoint funciona como um fornecedor de armazenamento de BLOBS remoto (RBS) e utiliza Olá toostore da funcionalidade de armazenamento de BLOBS do SQL Server remoto não estruturado conteúdo do SharePoint (no formato Olá BLOBs) num servidor de ficheiros que é copiado por um dispositivo StorSimple.

> [!NOTE]
> Olá StorSimple adaptador para o SharePoint suporta o SharePoint Server 2010 remoto BLOB de armazenamento (RBS). Não suporta a SharePoint Server 2010 externo BLOB de armazenamento (EBS).


* Olá toodownload StorSimple adaptador para o SharePoint, vá demasiado[StorSimple adaptador para o SharePoint] [ 1] no Olá Microsoft Download Center.
* Para informações sobre o planeamento de RBS e RBS limitações, aceda demasiado[decidir toouse RBS no SharePoint 2013] [ 2] ou [planear RBS (SharePoint Server 2010)] [3].

Olá rest desta descrição geral descreve brevemente função Olá de Olá StorSimple adaptador para o SharePoint e Olá capacidade do SharePoint e limites de desempenho que deve ter em consideração antes de instalar e configurar o adaptador de Olá. Depois de rever estas informações, aceda demasiado[adaptador StorSimple para a instalação do SharePoint](#storsimple-adapter-for-sharepoint-installation) toobegin configurar adaptador Olá.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>Placa StorSimple para os benefícios do SharePoint
Num site do SharePoint, conteúdo é armazenado como dados de BLOBS não estruturados num ou mais bases de dados conteúdos. Por predefinição, estas bases de dados estão alojados em computadores que executam o SQL Server e estão localizados num farm de servidores do SharePoint Olá. Os bLOBs rapidamente podem aumentar de tamanho, consumir grandes quantidades de armazenamento no local. Por este motivo, é aconselhável toofind solução de outro armazenamento menos dispendioso. O SQL Server proporciona uma tecnologia chamada remoto Blob de armazenamento (RBS) que lhe permite armazenar o conteúdo do BLOB no sistema de ficheiros de Olá, fora da base de dados do Olá do SQL Server. RBS, BLOBs podem residir no sistema de ficheiros de Olá Olá no computador no qual está a executar o SQL Server ou podem ser armazenados no sistema de ficheiros de Olá noutro computador do servidor.

RBS requer que utilize um fornecedor RBS, tais como Olá StorSimple adaptador para o SharePoint, tooenable RBS no SharePoint. Olá StorSimple adaptador para o SharePoint funciona com RBS, permitindo-lhe mover servidor tooa de BLOBs uma cópia de segurança pelo sistema de Microsoft Azure StorSimple Olá. Microsoft Azure StorSimple, em seguida, armazena dados de BLOBS de Olá localmente ou numa nuvem Olá, com base na utilização. Os bLOBs que são muito ativos (normalmente referidos tooas camada 1 ou os dados) residirem localmente. Menos dados do Active Directory e os dados de arquivo residem na nuvem de Olá. Depois de ativar RBS numa base de dados de conteúdos, qualquer novo conteúdo BLOB criado no SharePoint armazenado no dispositivo do StorSimple Olá e não na base de dados de conteúdo de Olá.

implementação do Microsoft Azure StorSimple Olá de RBS fornece Olá seguintes vantagens:

* Ao mover BLOB tooa conteúdo servidor separado, pode reduzir Olá carga de consulta no SQL Server, que pode melhorar a capacidade de resposta do SQL Server. 
* Azure StorSimple utiliza o tamanho dos dados tooreduce eliminação de duplicados e compressão.
* Azure StorSimple fornece proteção de dados em forma de Olá de locais e instantâneos de nuvem. Além disso, se colocar Olá própria base de dados no dispositivo do StorSimple Olá, para fazer uma cópia de segurança da base de dados conteúdo Olá e os BLOBs em conjunto de forma consistente com a falha. (O dispositivo toohello do conteúdo da base de dados Olá mover só é suportado para dispositivos de série 8000 do StorSimple de Olá. Esta funcionalidade não é suportada para a série de Olá 5000 ou 7000.)
* Azure StorSimple inclui funcionalidades de recuperação de desastre, incluindo a ativação pós-falha, a recuperação de ficheiros e de volume (incluindo a recuperação de teste) e restauro rápido de dados.
* Pode utilizar o software de recuperação de dados, tais como Kroll Ontrack PowerControls, com instantâneos StorSimple BLOB tooperform ao nível do item de recuperação de dados de conteúdo do SharePoint. (Este software de recuperação de dados é uma compra separada).
* Olá StorSimple adaptador para o SharePoint plugs no portal de Administração Central do SharePoint Olá, permitindo-lhe toomanage solução completa de SharePoint partir de uma localização central.

Mover o sistema de ficheiros de conteúdo toohello BLOB pode fornecer outras reduções de custos e benefícios. Por exemplo, utilizar RBS pode reduzir a necessidade de Olá de armazenamento de camada 1 dispendioso e porque diminui-base de dados de conteúdo Olá, RBS pode reduzir o número de Olá das bases de dados necessário num farm de servidores do SharePoint Olá. No entanto, outros fatores, tais como os limites de tamanho de base de dados e a quantidade de Olá de conteúdo não RBS, também podem afetar os requisitos de armazenamento. Para obter mais informações sobre os custos de Olá e vantagens de utilizar RBS, consulte [planear RBS (SharePoint Foundation 2010)] [ 4] e [decidir toouse RBS no SharePoint 2013] [ 5].

### <a name="capacity-and-performance-limits"></a>Limites de capacidade e o desempenho
Antes de considerar que utilizar RBS na sua solução do SharePoint, deve ter conhecimento de desempenho de Olá testado e limites de capacidade do SharePoint Server 2010 e o SharePoint Server 2013 e inter-relação entre estes limites tooacceptable desempenho. Para obter mais informações, consulte [limites de Software e os limites para SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).

Reveja o seguinte Olá antes de configurar RBS:

* Certifique-se de que esse tamanho total de Olá de Olá conteúdo (tamanho de Olá de uma base de dados de conteúdo) mais o tamanho de Olá dos BLOBs externalized associados não excede o limite de tamanho RBS Olá suportado pelo SharePoint. Este limite é de 200 GB. 
  
    **base de dados de conteúdo de toomeasure e o tamanho do BLOB**
  
  1. Execute esta consulta no Olá WFE de Administração Central. Iniciar Olá Shell de gestão do SharePoint e, em seguida, introduza Olá seguintes do Windows PowerShell comando tooget Olá o tamanho das bases de dados de conteúdo Olá:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Este passo obtém o tamanho de Olá da base de dados de conteúdo Olá no disco Olá.
  2. Execute uma das seguintes consultas SQL no SQL Server Management Studio na caixa hello do servidor SQL em cada base de dados de conteúdo de Olá e adicione o número de toohello Olá resultado obtido no passo 1.
     
     No SharePoint 2013 conteúdos as bases de dados, introduza:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     No SharePoint 2010 conteúdos as bases de dados, introduza:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Este passo obtém o tamanho de Olá de Olá BLOBs que tenham sido externalized.
* Recomendamos que armazene todo o conteúdo BLOB e a base de dados localmente no dispositivo do StorSimple Olá. o dispositivo StorSimple Olá é um cluster de dois nós para elevada disponibilidade. Colocar as bases de dados de conteúdo Olá e os BLOBs no dispositivo do StorSimple Olá fornece elevada disponibilidade.
  
    Utilize tradicional do SQL Server migração melhores práticas toomove Olá da base de dados de conteúdo toohello dispositivo StorSimple. Mova a base de dados de Olá apenas depois de todo o conteúdo BLOB da base de dados de Olá foi movido toohello partilha de ficheiros através de RBS. Se optar por dispositivo do StorSimple toohello toomove Olá conteúdo da base de dados, recomendamos que configurar o armazenamento de base de dados de conteúdo de Olá no dispositivo Olá como um volume primário.
* No Microsoft Azure StorSimple, se utilizar volumes em camadas, não é possível tooguarantee conteúdo armazenado localmente no dispositivo do StorSimple Olá não será tooMicrosoft em camadas armazenamento na nuvem do Azure. Por conseguinte, recomendamos a utilização de volumes do StorSimple afixado localmente em conjunto com RBS do SharePoint. Isto irá garantir que todo o conteúdo BLOB permanece localmente no dispositivo do StorSimple Olá, não sendo tooMicrosoft movida do Azure.
* Se não armazenar bases de dados de conteúdo Olá no dispositivo do StorSimple Olá, utilize tradicionais do SQL Server elevada disponibilidade melhores práticas que suportam RBS. Clustering do SQL Server suporta RBS, ao SQL Server espelhamento não. 

> [!WARNING]
> Se não tiver ativado RBS, não recomendamos mover o dispositivo StorSimple de toohello à base de dados de conteúdo Olá. Esta é uma configuração untested.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>Placa StorSimple para a instalação do SharePoint
Antes de poder instalar Olá StorSimple adaptador para o SharePoint, tem de configurar o dispositivo StorSimple Olá e certifique-se de que o farm de servidores do SharePoint Olá e instâncias do SQL Server cumprem todos os pré-requisitos. Este tutorial descreve os requisitos de configuração, bem como dos procedimentos para instalar e atualizar Olá StorSimple adaptador para o SharePoint.

## <a name="configure-prerequisites"></a>Configurar os pré-requisitos
Antes de poder instalar Olá StorSimple adaptador para o SharePoint, certifique-se de que o dispositivo StorSimple Olá, farm do SharePoint server e as instâncias do SQL Server cumprem os seguintes pré-requisitos de Olá.

### <a name="system-requirements"></a>Requisitos de sistema
Olá StorSimple adaptador para o SharePoint funciona com Olá seguinte hardware e software:

* Sistema de operativo suportado – Windows Server 2008 R2 SP1, Windows Server 2012 ou Windows Server 2012 R2
* Versões suportadas do SharePoint – SharePoint Server 2010 ou SharePoint Server 2013
* Versões suportadas do SQL Server – SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition ou SQL Server 2012 Enterprise Edition
* Suportado dispositivos StorSimple série 8000 do StorSimple, séries StorSimple 7000 ou série de StorSimple 5000.

### <a name="storsimple-device-configuration-prerequisites"></a>Pré-requisitos de configuração do dispositivo StorSimple
o dispositivo StorSimple Olá é um dispositivo de bloco e como tal requer um servidor de ficheiros no qual os dados de Olá podem ser alojados. Recomendamos que utilize um servidor separado, em vez de um servidor existente do farm do SharePoint Olá. Este servidor de ficheiros tem de ser no Olá mesma rede de área local (LAN) como computador do SQL Server Olá que alojam Olá conteúdo bases de dados.

> [!TIP]
> * Se configurar o farm do SharePoint para elevada disponibilidade, deve implementar o servidor de ficheiros de Olá para elevada disponibilidade também.
> * Se armazenar a base de dados de conteúdo Olá no dispositivo do StorSimple Olá, utilize as melhores práticas de elevada disponibilidade tradicional que suportam RBS. Clustering do SQL Server suporta RBS, ao SQL Server espelhamento não. 


Certifique-se de que o dispositivo StorSimple está configurado corretamente e que toosupport volumes adequados a implementação de SharePoint estiver configurado e acessível a partir do computador do SQL Server. Aceda demasiado[implementar o dispositivo StorSimple no local](storsimple-8000-deployment-walkthrough-u2.md) se ainda não tiver implementado e configurado o dispositivo StorSimple. Tenha em atenção o endereço IP de Olá do dispositivo do StorSimple Olá; precisará dele durante adaptador StorSimple para a instalação do SharePoint.

Além disso, certifique-se que toobe de volume Olá utilizado para BLOB externalization cumpre Olá os seguintes requisitos:

* volume de Olá deve ser formatado com um tamanho de unidade de alocação de 64 KB.
* O front-end (WFE) da web e servidores de aplicações tem de ser capaz de tooaccess volume de Olá através de um caminho de convenção de Nomenclatura Universal (UNC).
* farm de servidores do SharePoint Olá tem de ser configurado toowrite toohello volume.

> [!NOTE]
> Depois de instalar e configurar o adaptador de Olá, todos os externalization do BLOB tem percorrer o dispositivo StorSimple Olá (dispositivo Olá irá apresentar Olá volumes tooSQL servidor e gerir as camadas de armazenamento Olá). Não é possível utilizar quaisquer outros elementos para externalization de BLOB.


Se planear toouse Snapshot Manager do StorSimple tootake instantâneos de Olá BLOB e da base de dados dados, ser se tooinstall Snapshot Manager do StorSimple no servidor de base de dados de Olá, para que possa utilizar Olá tooimplement do serviço SQL Writer Olá Windows cópia sombra de volumes Serviço (VSS).

> [!IMPORTANT]
> Snapshot Manager do StorSimple não suporta Olá escritor de VSS do SharePoint e não pode assumir instantâneos consistentes com aplicações dos dados do SharePoint. Num cenário de SharePoint, o Snapshot Manager do StorSimple fornece apenas cópias de segurança consistentes com falhas.


## <a name="sharepoint-farm-configuration-prerequisites"></a>Pré-requisitos de configuração de farm do SharePoint
Certifique-se de que o farm de servidores do SharePoint está corretamente configurado, da seguinte forma:

* Verifique se o farm do SharePoint server está em bom estado de funcionamento e verifique Olá seguinte:
* Todos os SharePoint WFE e servidores de aplicação, registados no farm de Olá estão em execução e podem ser executar o ping do servidor de Olá no qual irá instalar Olá StorSimple adaptador para o SharePoint.
* Olá serviço de temporizador do SharePoint (SPTimerV3 ou SPTimerV4) está em execução em cada servidor WFE e o servidor de aplicações.
* Olá SharePoint Timer service tanto o agrupamento de aplicações do IIS Olá sob a qual está a executar o site de Administração Central do SharePoint de Olá tem privilégios administrativos.
* Certifique-se de que o Internet Explorer avançada contexto de segurança (IE ESC) está desativado. Siga estes passos toodisable IE ESC:
  
  1. Feche todas as instâncias do Internet Explorer.
  2. Inicie Olá Gestor de servidor.
  3. No painel esquerdo Olá, clique em **servidor Local**.
  4. No Olá com o botão direito painel, em seguida demasiado**configuração de segurança avançada do IE**, clique em **no**.
  5. Em **administradores**, clique em **desativar**.
  6. Clique em **OK**.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Remoto pré-requisitos de armazenamento de BLOBS (RBS)
Certifique-se de que está a utilizar uma versão suportada do SQL Server. Apenas hello versões seguintes são suportado e consegue toouse RBS:

* SQL Server 2008 Enterprise Edition
* Edição do SQL Server 2008 R2 Enterprise
* SQL Server 2012 Enterprise Edition

Podem ser externalized bLOBs no apenas os volumes que Olá dispositivo StorSimple apresenta tooSQL servidor. Não existem outros destinos para externalization BLOBS são suportados.

Quando tiver terminado de todos os passos de configuração de pré-requisitos, aceda demasiado[Olá instalar adaptador StorSimple para SharePoint](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>Instalar Olá StorSimple adaptador para o SharePoint
Utilize Olá os seguintes passos tooinstall Olá StorSimple adaptador para o SharePoint. Se estiver a reinstalar o software de Olá, consulte o artigo [atualizar ou reinstalar Olá StorSimple adaptador para o SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). tempo de Olá necessário para a instalação de Olá depende do número total de Olá de bases de dados do SharePoint no farm do SharePoint server.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>Configurar RBS
Depois de instalar Olá StorSimple adaptador para o SharePoint, configure RBS conforme descrito em Olá procedimento a seguir.

> [!TIP]
> Olá StorSimple adaptador para o SharePoint plugs na página de Administração Central do SharePoint Olá, permitindo RBS toobe ativado ou desativado em cada base de dados de conteúdo no farm do SharePoint Olá. No entanto, ativando ou desativando RBS na base de dados de conteúdo Olá faz com que uma reposição do IIS, que, consoante a configuração do farm, momentaneamente pode interromper disponibilidade Olá Olá SharePoint web front-end (WFE). (Fatores como Olá utilização de um balanceador de carga de front-end, Olá atual servidor carga de trabalho e assim sucessivamente, podem limitar ou eliminar este interrupção) tooprotect utilizadores de uma interrupção, recomendamos que ativar ou desativar RBS apenas durante uma janela de manutenção planeada.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Configurar a recolha de lixo
Quando os objetos são eliminados do site do SharePoint, estes não são automaticamente eliminados do Olá RBS arquivo de volume. Em vez disso, um assíncrono, o programa de manutenção em segundo plano elimina órfãos os BLOBs do armazenamento de ficheiros de Olá. Os administradores de sistema podem agendar este processo toorun periodicamente ou podem iniciá-lo, sempre que necessário.

Este programa de manutenção (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) é instalado automaticamente em todos os servidores SharePoint WFE e servidores de aplicações quando ativar RBS. programa de Olá está instalado no Olá seguinte localização: *unidade de arranque*: \Programas\Microsoft SQL remoto Blob Storage 10.50\Maintainer\

Para obter informações sobre como configurar e utilizar o programa de manutenção de Olá, consulte [manter RBS no SharePoint Server 2013][8].

> [!IMPORTANT]
> programa do Olá RBS responsável pela manutenção é intensiva de recursos. Deve agendá-la toorun apenas durante períodos de atividade ligeira no farm do SharePoint Olá.


### <a name="delete-orphaned-blobs-immediately"></a>Eliminar BLOBs órfãos imediatamente
Se precisar de BLOBs de toodelete órfã imediatamente, pode utilizar Olá seguir instruções. Tenha em atenção que estas instruções são um exemplo de como isto pode ser feito um ambiente do SharePoint 2013 com Olá os seguintes componentes:

* nome de base de dados de conteúdo de Olá é WSS_Content.
* nome do SQL Server Olá é SHRPT13 SQL12\SHRPT13.
* nome da aplicação web Olá é SharePoint – 80.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Atualizar ou reinstalar Olá StorSimple adaptador para o SharePoint
Utilizar Olá SharePoint server tooupgrade procedimento a seguir e, em seguida, reinstale o adaptador do StorSimple para atualização SharePoint ou toosimply ou reinstale adaptador Olá um farm de servidores do SharePoint existente.

> [!IMPORTANT]
> Rever Olá seguintes informações antes de tentar tooupgrade o software do SharePoint e/ou a atualização ou reinstalar Olá StorSimple adaptador para o SharePoint:
> 
> * Quaisquer ficheiros que foram anteriormente movidos tooexternal armazenamento através de RBS não estarão disponível até que a reinstalação de Olá estiver concluída e Olá funcionalidade RBS seja ativada de novo. utilizador toolimit afeta, executar qualquer atualização ou reinstalação durante uma janela de manutenção planeada.
> * tempo de Olá necessário para Olá atualização/reinstalação pode variar, dependendo do número total de Olá de bases de dados do SharePoint num farm de servidores do SharePoint Olá.
> * Após a conclusão da atualização/reinstalação de Olá, terá de tooenable RBS para bases de dados de conteúdo Olá. Consulte [configurar RBS](#configure-rbs) para obter mais informações.
> * Se estiver a configurar RBS para um farm do SharePoint que tem um número muito elevado de bases de dados (superior a 200), Olá **Administração Central do SharePoint** página poderá tempo limite. Se isso ocorrer, atualize a página Olá. Isto não afeta o processo de configuração de Olá.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>Placa StorSimple para remoção do SharePoint
Olá procedimentos a seguir descreve como toomove Olá BLOBs fazer cópias de bases de dados do SQL Server de toohello conteúdos e, em seguida, desinstalar Olá StorSimple adaptador para o SharePoint. 

> [!IMPORTANT]
> Tiver bases de dados no Olá BLOBs back toohello conteúdos toomove antes de desinstalar o software de adaptador de Olá.


### <a name="before-you-begin"></a>Antes de começar
Recolha Olá seguintes informações antes de mover dados Olá fazer uma cópia toohello conteúdos bases de dados e iniciar o processo de remoção do adaptador de Olá:

* Olá nomes de todas as bases de dados Olá para o qual RBS está ativado
* caminho UNC Olá de Olá configurado o arquivo de BLOB

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Mover Olá BLOBs back toohello conteúdos bases de dados
Antes de desinstalar Olá StorSimple adaptador para o software do SharePoint, deve migrar todas Olá BLOBs que foram externalized back toohello conteúdos bases de dados. Se tentar toouninstall Olá StorSimple adaptador para o SharePoint antes de mover todos os Olá BLOBs back toohello conteúdos bases de dados, verá Olá seguir a mensagem de aviso.

![Mensagem de aviso](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove Olá BLOBs back toohello conteúdos as bases de dados
1. Transferir a cada um dos objetos de Olá externalized.
2. Abra Olá **Administração Central do SharePoint** página e procurar demasiado**definições do sistema**.
3. Em **Azure StorSimple**, clique em **configurar adaptador do StorSimple**.
4. No Olá **configurar adaptador do StorSimple** página, clique em Olá **desativar** no botão abaixo cada Olá conteúdo bases de dados que pretende que o tooremove externo do armazenamento de BLOBS. 
5. Eliminar objetos Olá do SharePoint e, em seguida, volte a carregá-los.

Em alternativa, pode utilizar Olá Microsoft` RBS Migrate()` cmdlet do PowerShell incluído com o SharePoint. Para obter mais informações, consulte [migrar conteúdo ou a sair RBS](https://technet.microsoft.com/library/ff628255.aspx).

Depois de mover Olá BLOBs back toohello conteúdo da base de dados, vá toohello próximo passo: [desinstalação do adaptador de Olá](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Desinstalar o adaptador de Olá
Depois de mover bases de dados de BLOBs toohello anterior do SQL Server conteúdos Olá, utilize um dos Olá seguintes opções toouninstall Olá StorSimple adaptador para o SharePoint.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>placa Olá de toouninstall programa toouse Olá instalação
1. Utilize uma conta com privilégios de administrador toolog no servidor do toohello web front-end (WFE).
2. Faça duplo clique Olá StorSimple adaptador para o installer do SharePoint. Olá Assistente de configuração é iniciado.
   
    ![Assistente de configuração](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. Clique em **Seguinte**. Olá seguir página é apresentada.
   
    ![Página do Assistente para remover o programa de configuração](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Clique em **remover** processo de remoção de Olá tooselect. Olá seguir página é apresentada.
   
    ![Página de confirmação do Assistente de configuração](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Clique em **remover** remoção de Olá tooconfirm. Olá seguinte página de progresso é apresentado.
   
    ![Página de progresso do Assistente de configuração](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Quando a remoção de Olá estiver concluída, é apresentada a página de conclusão de Olá. Clique em **concluir** tooclose Olá Assistente de configuração.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>adaptador de Olá toouse Olá painel de controlo toouninstall
1. Abra o painel de controlo de Olá e, em seguida, clique em **programas e funcionalidades**.
2. Selecione **StorSimple adaptador para o SharePoint**e, em seguida, clique em **desinstalação**.

## <a name="next-steps"></a>Passos seguintes
[Saiba mais sobre StorSimple](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
