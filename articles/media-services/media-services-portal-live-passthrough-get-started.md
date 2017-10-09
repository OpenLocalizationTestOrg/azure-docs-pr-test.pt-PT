---
title: "fluxo de aaaLive com codificadores no local utilizando Olá portal do Azure | Microsoft Docs"
description: "Este tutorial explica Olá passos da criação de um canal que está configurado para uma entrega pass-through."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>Como tooperform em direto de transmissão em fluxo no local codificadores utilizando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Este tutorial explica passos para Olá Olá toocreate portal do Azure a utilizar um **canal** que está configurado para uma entrega pass-through. 

## <a name="prerequisites"></a>Pré-requisitos
Olá, são tutorial de Olá toocomplete necessário:

* Uma conta do Azure. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Uma conta dos Media Services. toocreate uma conta de Media Services, consulte [como tooCreate uma conta de Media Services](media-services-portal-create-account.md).
* Uma câmara Web. Por exemplo, [codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).

É altamente recomendável Olá tooreview seguintes artigos:

* [Azure Media Services RTMP Support and Live Encoders (Suporte RTMP dos Serviços de Multimédia do Azure e Codificadores em Direto)](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Overview of Live Streaming using Azure Media Services (Descrição Geral da Transmissão em Fluxo em Direto com os Serviços de Multimédia do Azure)](media-services-manage-channels-overview.md)
* [Transmissão em fluxo em direto com codificadores no local que criam transmissões com velocidade de transmissão múltipla](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>Cenário comum de transmissão em fluxo em direto
Olá passos seguintes descrevem as tarefas envolvidas na criação de aplicações de transmissão em fluxo em direto comuns que utilizam canais que estão configurados para entrega pass-through. Este tutorial mostra como toocreate e gerir um canal pass-through e eventos em direto.

>[!NOTE]
>Certifique-se Olá a partir das quais pretende toostream conteúdo de ponto final de transmissão em fluxo no Olá **executar** estado. 
    
1. Ligue um computador de tooa câmara de vídeo. Iniciar e configurar um codificador em direto no local que produza um RTMP com velocidade de transmissão múltipla ou uma transmissão em fluxo MP4 fragmentada. Para obter mais informações, consulte [Suporte RTMP dos Media Services do Azure e Codificadores em Direto](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Este passo também pode ser realizado depois de criar o Canal.
2. Criar e iniciar um Canal pass-through.
3. URL de inserção de obter Olá canal. 
   
    URL de inserção de Olá é utilizado pelo Olá codificador em direto toosend Olá fluxo toohello canal.
4. Obter o URL de pré-visualização do canal de Olá. 
   
    Utilize este tooverify de URL que o canal está a receber corretamente em fluxo em direto Olá.
5. Crie um evento/programa em direto. 
   
    Quando utilizar hello portal do Azure, criar um evento em direto também cria um recurso. 

6. Inicie Olá. o evento/programa quando estiver pronto toostart de transmissão em fluxo e o arquivamento.
7. Opcionalmente, o codificador em direto Olá pode ser assinalado toostart um anúncio. anúncio de Olá é inserido no fluxo de saída Olá.
8. Pare Olá. o evento/programa sempre que pretender toostop de transmissão em fluxo e arquivar o evento de Olá.
9. Eliminar Olá. o evento/programa (e, opcionalmente, elimine o elemento de Olá).     

> [!IMPORTANT]
> Reveja [transmissão em fluxo em direto com codificadores no local que criar fluxos de transmissão múltipla](media-services-live-streaming-with-onprem-encoders.md) toolearn sobre conceitos e considerações relacionadas com a transmissão em fluxo toolive com codificadores no local e canais pass-through.
> 
> 

## <a name="tooview-notifications-and-errors"></a>tooview notificações e erros
Se pretender tooview notificações e erros produzidos por Olá portal do Azure, clique no ícone de notificação de Olá.

![Notificações](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>Criar e iniciar eventos e canais pass-through
Um canal está associado a eventos/programas que permitem a publicação de Olá toocontrol e armazenamento de segmentos numa transmissão em fluxo em direto. Os canais gerem eventos. 

Pode especificar Olá número de horas que pretende tooretain Olá registada conteúdo para o programa de Olá por definição Olá **janela de arquivo** comprimento. Este valor pode ser definido a partir de um mínimo de máximo de tooa de 5 minutos de 25 horas. Duração da janela de arquivo dita também Olá período de tempo máximo os clientes podem recuar a partir da posição atual em direto Olá. Eventos podem ser executados durante período de tempo especificado Olá, mas o conteúdo que se situe atrás da duração da janela Olá é continuamente descartado. Este valor desta propriedade também determina o cliente de Olá quanto possam crescer manifestos.

Cada evento está associado a um elemento. evento de Olá toopublish, tem de criar um localizador OnDemand para o recurso de Olá associado. Ter este localizador permite toobuild um URL de transmissão em fluxo que pode fornecer tooyour clientes.

Um canal suporta até toothree eventos a executar em simultâneo para que possa criar vários arquivos do Olá mesmo fluxo de entrada. Isto permite-lhe toopublish e arquivar diferentes partes de um evento conforme necessário. Por exemplo, o requisito comercial será tooarchive 6 horas de um programa mas toobroadcast apenas últimos 10 minutos. tooaccomplish isto, terá de programas em execução em simultâneo de dois toocreate. Um programa está definido tooarchive 6 horas do evento de Olá mas Olá programa não está publicado. Olá outro programa está definido tooarchive durante 10 minutos e este programa está publicado.

Não deve reutilizar os eventos em direto existentes. Em vez disso, crie e inicie um novo evento para cada evento.

Inicie o evento de Olá quando estiver pronto toostart de transmissão em fluxo e o arquivamento. Pare o programa de Olá sempre que pretender toostop de transmissão em fluxo e arquivar o evento de Olá. 

conteúdo toodelete arquivado, pare e eliminar o evento de Olá e, em seguida, elimine o elemento associado Olá. Não é possível eliminar um recurso que é utilizado por um evento; evento de Olá deve ser eliminado primeiro. 

Mesmo depois de parar e eliminar o evento de Olá, Olá utilizadores seria capaz de toostream seu conteúdo arquivado como um vídeo a pedido, desde que não a eliminar o recurso de Olá.

Se pretender Olá tooretain arquivado conteúdo, mas não o tiver disponível para transmissão em fluxo, elimine Olá localizador de transmissão em fluxo.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse Olá portal toocreate um canal
Esta secção mostra como toouse Olá **criação rápida** opção toocreate um canal pass-through.

Para obter mais detalhes sobre canais pass-through, veja [Transmissão em fluxo em direto com codificadores no local que criam transmissões em fluxo com velocidade de transmissão múltipla](media-services-live-streaming-with-onprem-encoders.md).

1. No Olá [portal do Azure](https://portal.azure.com/), selecione a sua conta de Media Services do Azure.
2. No Olá **definições** janela, clique em **transmissão em direto**. 
   
    ![Introdução](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    Olá **a transmissão em fluxo em direto** surge a janela.
3. Clique em **criação rápida** toocreate um canal pass-through com Olá RTMP protocolo de inserção.
   
    Olá **criar um novo canal** surge a janela.
4. Dê um nome de canal novo Olá e clique em **criar**. 
   
    Esta ação cria um canal pass-through com Olá protocolo de inserção RTMP.

## <a name="create-events"></a>Criar eventos
1. Selecione um toowhich de canal que pretende tooadd um evento.
2. Prima o botão **Evento em Direto**.

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>Obter URLs de inserção
Depois de Olá canal seja criado, pode obter os URLs que irá fornecer o codificador em direto toohello de inserção. codificador Olá utiliza estes URLs tooinput uma transmissão em fluxo em direto.

![Criado](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>Evento de Olá veja
evento de Olá toowatch, clique em **veja** no Olá Olá Azure portal ou a cópia do URL de transmissão em fluxo e utilizar um leitor da sua preferência. 

![Criado](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

Evento em direto automaticamente obter conteúdo de convertida tooon a pedido quando parado.

## <a name="clean-up"></a>Limpeza
Para obter mais detalhes sobre canais pass-through, veja [Transmissão em fluxo em direto com codificadores no local que criam transmissões em fluxo com velocidade de transmissão múltipla](media-services-live-streaming-with-onprem-encoders.md).

* Um canal pode ser parado apenas quando todos os eventos/programas no canal Olá foram parados.  Depois de Olá canal esteja parado, não é cobrado qualquer custo. Quando tiver toostart-la novamente, pode ter hello mesmo URL de inserção por isso não terá de tooreconfigure o codificador.
* Um canal pode ser eliminado apenas quando todos os eventos em direto no canal Olá tem sido eliminados.

## <a name="view-archived-content"></a>Ver conteúdo arquivado
Mesmo depois de parar e eliminar o evento de Olá, Olá utilizadores seria capaz de toostream seu conteúdo arquivado como um vídeo a pedido, desde que não a eliminar o recurso de Olá. Não é possível eliminar um recurso que é utilizado por um evento; evento de Olá deve ser eliminado primeiro. 

Selecione os recursos de toomanage **definição** e clique em **ativos**.

![Elementos](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>Passo seguinte
Rever os percursos de aprendizagem dos Serviços de Multimédia

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

