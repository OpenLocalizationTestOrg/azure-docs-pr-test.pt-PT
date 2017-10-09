---
title: "aaaHow tooperform em direto de transmissão em fluxo através de fluxos de transmissão múltipla toocreate de Media Services do Azure com Olá portal do Azure | Microsoft Docs"
description: "Este tutorial explica-lhe como Olá passos da criação de um canal que recebe um velocidade de transmissão única em fluxo em direto e a codifica toomulti transmissão em fluxo utilizando Olá portal do Azure."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>Como tooperform em direto transmissão em fluxo utilizando toocreate de Media Services do Azure e múltipla fluxos com Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Este tutorial explica Olá passos de criação de um **canal** que recebe um velocidade de transmissão única em fluxo em direto e a codifica toomulti transmissão em fluxo.

> [!NOTE]
> Para obter mais informações concetuais tooChannels relacionados que estão ativados para live encoding, consulte [em direto de transmissão em fluxo através de fluxos de transmissão múltipla toocreate de Media Services do Azure](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a>Cenário Comum de Transmissão em Fluxo em Direto
Olá seguem-se passos gerais referentes à criação de aplicações comuns de transmissão em fluxo em direto.

> [!NOTE]
> Atualmente, Olá máximo recomendado duração de um evento em direto é de 8 horas. Contacte amslived através de Microsoft.com se precisar de toorun um canal durante períodos de tempo mais longos.
> 
> 

1. Ligue um computador de tooa câmara de vídeo. Inicie e configure um codificador em direto no local que possa enviar uma transmissão em fluxo das Olá seguintes protocolos: RTMP, transmissão em fluxo uniforme ou RTP (MPEG-TS). Para obter mais informações, consulte [Suporte RTMP dos Media Services do Azure e Codificadores em Direto](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Este passo também pode ser realizado depois de criar o Canal.
2. Crie e inicie um Canal. 
3. URL de inserção de obter Olá canal. 
   
    URL de inserção de Olá é utilizado pelo Olá codificador em direto toosend Olá fluxo toohello canal.
4. Obter o URL de pré-visualização do canal de Olá. 
   
    Utilize este tooverify de URL que o canal está a receber corretamente em fluxo em direto Olá.
5. Crie um evento/programa (que também irá criar um elemento). 
6. Publica o evento de Olá (que criará um localizador OnDemand para o elemento associado Olá).    
7. Inicie o evento de Olá quando estiver pronto toostart de transmissão em fluxo e o arquivamento.
8. Opcionalmente, o codificador em direto Olá pode ser assinalado toostart um anúncio. anúncio de Olá é inserido no fluxo de saída Olá.
9. Pare o evento de Olá sempre que pretender toostop de transmissão em fluxo e arquivar o evento de Olá.
10. Eliminar o evento de Olá (e, opcionalmente, elimine o elemento de Olá).   

## <a name="in-this-tutorial"></a>Neste tutorial
Neste tutorial, Olá portal do Azure é Olá tooaccomplish utilizados seguintes tarefas: 

1. Criar um canal que é ativada tooperform em direto codificação.
2. Get Olá URL de inserção na ordem toosupply-toolive codificador. Codificador em direto Olá utilizará esta sequência do URL tooingest Olá para Olá canal.
3. Crie um evento/programa (e um elemento).
4. Publicar Olá elemento e obter URLs de transmissão em fluxo.  
5. Reproduzir os conteúdos.
6. Faça a limpeza.

## <a name="prerequisites"></a>Pré-requisitos
Olá seguem-se tutorial de Olá toocomplete necessária.

* toocomplete neste tutorial, precisa de uma conta do Azure. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. 
  Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Uma conta dos Media Services. toocreate uma conta de Media Services, consulte [criar conta](media-services-portal-create-account.md).
* Uma câmara Web e um codificador que possa enviar uma transmissão de velocidade de transmissão única.

## <a name="create-a-channel"></a>Criar um canal
1. No Olá [portal do Azure](https://portal.azure.com/), selecione serviços de suporte de dados e, em seguida, clique no nome da sua conta dos Media Services.
2. Selecione **Transmissão em Direto**.
3. Selecione **Criação personalizada**. Esta opção permitir-lhe-á criar um canal que está ativado para codificação em direto.
   
    ![Criar um canal](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. Clique em **Definições**.
   
   1. Escolha Olá **Live Encoding** tipo de canal. Este tipo Especifica que pretende que toocreate um canal ativado para live encoding. Que significa Olá velocidade de transmissão única entrada fluxo enviado toohello canal e codificado como uma sequência de transmissão múltipla utilizando as definições do codificador em direto. Para obter mais informações, consulte [em direto de transmissão em fluxo através de fluxos de transmissão múltipla toocreate de Media Services do Azure](media-services-manage-live-encoder-enabled-channels.md). Clique em OK.
   2. Especifique o nome de um canal.
   3. Clique em OK em Olá parte inferior do ecrã de Olá.
5. Selecione Olá **inserção** separador.
   
   1. Nesta página, pode selecionar um protocolo de transmissão em fluxo. Para Olá **Live Encoding** são do tipo de canal, opções de protocolo válido:
      
      * MP4 fragmentado de velocidade de transmissão única (Transmissão em Fluxo Uniforme)
      * RTMP de velocidade transmissão única
      * RTP (MPEG-TS): Transmissão de Fluxo de Transporte de MPEG-2 sobre RTP.
        
        Para obter explicações detalhadas sobre cada protocolo, consulte [em direto de transmissão em fluxo através de fluxos de transmissão múltipla toocreate de Media Services do Azure](media-services-manage-live-encoder-enabled-channels.md).
        
        Não pode alterar a opção de protocolo de Olá ao hello canal ou seus eventos/programas associados estão em execução. Se necessitar de protocolos diferentes, deve criar canais separados para cada protocolo de transmissão em fluxo.  
   2. Pode aplicar a restrição de IP Olá de inserção. 
      
       Pode definir Olá IP endereços que são permitidos tooingest um canal toothis vídeo. Os endereços IP permitidos podem ser especificados como um endereço IP único (por exemplo,  "10.0.0.1"), um intervalo IP com um endereço IP e uma máscara sub-rede CIDR (por exemplo "10.0.0.1/22") ou um intervalo IP com um endereço IP e uma máscara sub-rede de ponto decimal (por exemplo, '10.0.0.1(255.255.252.0)').
      
       Se não for especificado qualquer endereço IP e não existir nenhuma definição de regra, então, não será permitido qualquer endereço IP. tooallow qualquer endereço IP, crie uma regra e defina 0.0.0.0/0.
6. No Olá **pré-visualização** separador, aplicar a restrição de IP na pré-visualização Olá.
7. No Olá **codificação** separador, especifique a predefinição de codificação Olá. 
   
    Olá, atualmente, apenas o sistema é a predefinição, pode selecionar **720p**. toospecify um personalizado predefinido, abra um pedido de suporte da Microsoft. Em seguida, introduza o nome de Olá do Olá predefinição criada para si. 

> [!NOTE]
> Atualmente, o arranque do canal Olá pode demorar até too30 minutos. A reposição do canal pode demorar até too5 minutos.
> 
> 

Assim que tiver criado o canal de Olá, pode clicar em canal de Olá e selecione **definições** onde pode ver as configurações dos canais. 

Para obter mais informações, consulte [em direto de transmissão em fluxo através de fluxos de transmissão múltipla toocreate de Media Services do Azure](media-services-manage-live-encoder-enabled-channels.md).

## <a name="get-ingest-urls"></a>Obter URLs de inserção
Depois de Olá canal seja criado, pode obter os URLs que irá fornecer o codificador em direto toohello de inserção. codificador Olá utiliza estes URLs tooinput uma transmissão em fluxo em direto.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>Criar e gerir eventos
### <a name="overview"></a>Descrição geral
Um canal está associado a eventos/programas que permitem a publicação de Olá toocontrol e armazenamento de segmentos numa transmissão em fluxo em direto. Os canais gerem eventos/programas. Olá relação canal e o programa é muito semelhante tootraditional suporte de dados em que um canal tem uma transmissão em fluxo constante de conteúdo e um programa é confinada toosome excedeu o tempo limite de evento nesse canal.

Pode especificar Olá número de horas que pretende tooretain Olá registada conteúdo para o evento de Olá por definição Olá **janela de arquivo** comprimento. Este valor pode ser definido a partir de um mínimo de máximo de tooa de 5 minutos de 25 horas. Duração da janela de arquivo dita também Olá período de tempo máximo os clientes podem recuar a partir da posição atual em direto Olá. Eventos podem ser executados durante período de tempo especificado Olá, mas o conteúdo que se situe atrás da duração da janela Olá é continuamente descartado. Este valor desta propriedade também determina o cliente de Olá quanto possam crescer manifestos.

Cada evento está associado a um Elemento. recurso do evento de Olá toopublish tem de criar um localizador OnDemand para Olá associados. Ter este localizador irá permitir toobuild um URL de transmissão em fluxo que pode fornecer tooyour clientes.

Um canal suporta até toothree eventos a executar em simultâneo para que possa criar vários arquivos do Olá mesmo fluxo de entrada. Isto permite-lhe toopublish e arquivar diferentes partes de um evento conforme necessário. Por exemplo, o requisito comercial será tooarchive 6 horas de um evento, mas toobroadcast apenas últimos 10 minutos. tooaccomplish isto, terá de toocreate dois em simultâneo com o evento. Um evento está definido tooarchive 6 horas do evento de Olá mas Olá programa não está publicado. Olá outro evento é conjunto tooarchive durante 10 minutos e este está publicado.

Não deve reutilizar programas existentes para novos eventos. Em vez disso, crie e inicie um novo programa para cada evento.

Inicie um evento/programa quando estiver pronto toostart de transmissão em fluxo e o arquivamento. Pare o evento de Olá sempre que pretender toostop de transmissão em fluxo e arquivar o evento de Olá. 

conteúdo toodelete arquivado, pare e eliminar o evento de Olá e, em seguida, elimine o elemento associado Olá. Não é possível eliminar um recurso que é utilizado pelo evento Olá; evento de Olá deve ser eliminado primeiro. 

Mesmo depois de parar e eliminar o evento de Olá, Olá utilizadores seria capaz de toostream seu conteúdo arquivado como um vídeo a pedido, desde que não a eliminar o recurso de Olá.

Se pretender Olá tooretain arquivado conteúdo, mas não o tiver disponível para transmissão em fluxo, elimine Olá localizador de transmissão em fluxo.

### <a name="createstartstop-events"></a>Criar/iniciar/parar eventos
Assim que tiver o fluxo de Olá que fluem para canal Olá pode começar a Olá transmissão em fluxo de eventos através da criação de um elemento, programa e localizador de transmissão em fluxo. Isto irá arquivar fluxo Olá e torná-lo tooviewers disponível através de Olá ponto final de transmissão em fluxo. 

>[!NOTE]
>Quando a sua conta de AMS é criada um **predefinido** ponto final de transmissão em fluxo é adicionada a conta de tooyour no Olá **parado** estado. toostart transmissão em fluxo o conteúdo e tomar partido do empacotamento dinâmico e a encriptação dinâmica, Olá ponto final transmissão a partir do qual pretende que o conteúdo de toostream tem toobe no Olá **executar** estado. 

Existem eventos de toostart duas formas: 

1. De Olá **canal** página, prima **evento em direto** tooadd um novo evento.
   
    Especifique: nome do evento, nome do elemento, janela de arquivo e opção de encriptação.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    Se marcou **publicar este evento em direto agora** opção estiver marcada, Olá de evento Olá URLs de publicação será criado.
   
    Pode premir **iniciar**, sempre que são eventos de Olá toostream pronto.
   
    Depois de iniciar o evento de Olá, pode premir **veja** toostart reprodução Olá conteúdo.
2. Em alternativa, pode utilizar um atalho e premir **aceda Live** botão Olá **canal** página. Isto irá criar um Elemento de predefinição, Programa e Localizador de Transmissão em Fluxo.
   
    eventos de Olá é denominado **predefinido** e definir a janela de arquivo de Olá too8 horas.

Pode ver Olá eventos publicados do Olá **evento em direto** página. 

Se clicar em **Off Air**, parará todos os eventos em direto. 

## <a name="watch-hello-event"></a>Evento de Olá veja
evento de Olá toowatch, clique em **veja** no Olá Olá Azure portal ou a cópia do URL de transmissão em fluxo e utilizar um leitor da sua preferência. 

![Criado](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

Evento em direto converte automaticamente o conteúdo a pedido tooon de eventos quando parado.

## <a name="clean-up"></a>Limpeza
Se terminar a transmissão em fluxo de eventos e quiser tooclean recursos Olá aprovisionados anteriormente, siga Olá procedimento a seguir.

* Termine o fluxo de Olá do codificador Olá.
* Pare o canal de Olá. Depois Olá canal esteja parado, não será cobrado qualquer custo. Quando tiver toostart-la novamente, pode ter hello mesmo URL de inserção por isso não terá de tooreconfigure o codificador.
* Pode parar o ponto final de transmissão em fluxo, a menos que queira arquivo de Olá tooprovide toocontinue do seu evento em direto como um fluxo a pedido. Se o canal de Olá está no estado parado, não será cobrado qualquer custo.

## <a name="view-archived-content"></a>Ver conteúdo arquivado
Mesmo depois de parar e eliminar o evento de Olá, Olá utilizadores seria capaz de toostream seu conteúdo arquivado como um vídeo a pedido, desde que não a eliminar o recurso de Olá. Não é possível eliminar um recurso que é utilizado por um evento; evento de Olá deve ser eliminado primeiro. 

Selecione os recursos de toomanage **definição** e clique em **ativos**.

![Elementos](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>Considerações
* Atualmente, Olá máximo recomendado duração de um evento em direto é de 8 horas. Contacte amslived através de Microsoft.com se precisar de toorun um canal durante períodos de tempo mais longos.
* Certifique-se Olá de transmissão em fluxo ponto final a partir das quais pretende toostream o conteúdo no Olá **executar** estado.

## <a name="next-step"></a>Passo seguinte
Rever os percursos de aprendizagem dos Serviços de Multimédia

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

