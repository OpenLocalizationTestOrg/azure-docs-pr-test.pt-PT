---
title: "aaaConfigure Olá FMLE codificador toosend uma transmissão em fluxo em direto | Microsoft Docs"
description: "Este tópico mostra como tooconfigure Olá Flash suporte de dados em direto codificador (FMLE) codificador toosend um canais de tooAMS de fluxo de velocidade de transmissão única que estão ativado para live encoding."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a>Utilizar Olá FMLE codificador toosend uma transmissão em fluxo em direto
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elementar em direto](media-services-configure-elemental-live-encoder.md)
> * [Transcodificadores](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

Este tópico mostra como tooconfigure Olá [codificador em direto de Flash multimédia](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) codificador toosend tooAMS canais ativados para live encoding de fluxo de velocidade de transmissão única. Para obter mais informações, consulte [trabalhar com canais que é tooPerform ativado em direto Encoding com Media Services do Azure](media-services-manage-live-encoder-enabled-channels.md).

Este tutorial mostra como toomanage dos Media Services do Azure (AMS) com a ferramenta Explorador de serviços de suporte de dados do Azure (AMSE). Esta ferramenta é executada apenas em PCs Windows. Se estiver no Mac ou Linux, utilize Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).

Tenha em atenção que este tutorial descreve AAC a utilizar. No entanto, FMLE não suporta AAC por predefinição. Terá de toopurchase um plug-in para codificação AAC tais como MainConcept: [Plug-in do AAC](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)

## <a name="prerequisites"></a>Pré-requisitos
* [Criar uma conta de Media Services do Azure](media-services-portal-create-account.md)
* Certifique-se existe um ponto de final de transmissão em fluxo em execução. Para obter mais informações, consulte [gerir transmissão em fluxo pontos finais numa conta de Media Services](media-services-portal-manage-streaming-endpoints.md)
* Instale a versão mais recente do Olá do Olá [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) ferramenta.
* Inicie a ferramenta Olá e ligar conta tooyour AMS.

## <a name="tips"></a>Sugestões
* Sempre que possível, utilize uma ligação de internet hardwired.
* Uma boa regra prática ao determinar os requisitos de largura de banda é Olá toodouble de forma de transmissão em fluxo. Embora não seja um requisito obrigatório, irá ajudar a mitigar o impacto de Olá congestionamento de rede.
* Quando utilizar o software com base no codificadores, feche enviados quaisquer programas desnecessários.

## <a name="create-a-channel"></a>Criar um canal
1. Na ferramenta AMSE de Olá, navegue toohello **em direto** separador e o botão direito do rato clique na área de canal de Olá. Selecione **canal de criar...** no menu Olá.

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. Especifique um nome de canal, Olá campo de descrição é opcional. Em definições de canal, selecione **padrão** para Olá opção Live Encoding, com Olá entrada protocolo definido demasiado**RTMP**. Pode deixar a todas as outras definições conforme está.

    Certifique-se de que Olá **início Olá novo canal agora** está selecionada.

3. Clique em **criar canal**.

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> canal de Olá pode demorar até 20 minutos toostart.
>
>

Enquanto está a iniciar o canal de Olá pode [configurar codificador Olá](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).

> [!IMPORTANT]
> Tenha em atenção que a faturação é iniciada assim que o canal entra no estado pronto. Para obter mais informações, consulte [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a>Configurar o codificador FMLE Olá
Este tutorial hello são utilizadas seguintes definições de saída. rest Olá desta secção descreve os passos de configuração mais detalhadamente.

**Vídeo**:

* Codec: 264
* Perfil: Alta (nível 4.0)
* Velocidade de transmissão: kbps 5000
* Keyframe: 2 segundos (60 segundos)
* Taxa de moldura: 30

**Áudio**:

* O codec: AAC (LC)
* Velocidade de transmissão: kbps 192
* Frequência de amostragem: kHz 44.1

### <a name="configuration-steps"></a>Passos de configuração
1. Navegue toohello que interface Flash Live codificador de multimédia (FMLE) na máquina de Olá a ser utilizada.

    interface de Olá é uma página principal de definições. Tome nota dos seguintes Olá recomendados definições tooget começar a transmissão em fluxo utilizando FMLE.

   * Formato: Taxa de moldura 264: 30.00
   * Tamanho de entrada: 1280 x 720
   * Taxa de bits: Kbps de 5000 (pode ser ajustado com base no limitações de rede)  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     Quando utilizar entrelaçadas origens, volte a marca de verificação Olá "Deinterlace" opção
2. Selecione Olá chave inglesa ícone seguinte tooFormat, devem ser estas definições adicionais:

   * Perfil: principal
   * Nível: 4.0
   * Frequência de Keyframe: segundos de 2

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. Definir Olá seguinte definição de áudio importante:

   * Formato: AAC
   * Frequência de amostragem: Hz 44100
   * Velocidade de transmissão: Kbps 192

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. Obter o URL de entrada do canal de Olá na ordem tooassign-do toohello FMLE **RTMP Endpoint**.

    Navegue ferramenta AMSE de back-toohello e verificar estado de conclusão de canal de Olá. Depois do Estado de Olá foi alterado de **inicial** demasiado**executar**, pode obter o URL de entrada Olá.

    Quando o canal de Olá está em execução, clique com o botão direito do rato em nome do canal Olá, navegue para baixo toohover através de **tooclipboard do URL de entrada de cópia** e, em seguida, selecione **primário URL de entrada**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. Colar estas informações no Olá **FMS URL** campo da secção de saída Olá e atribuir um nome de fluxo.

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    Para fins de redundância adicional, repita estes passos com Olá secundário URL de entrada.
6. Selecione **Ligar**.

> [!IMPORTANT]
> Antes de clicar em **Connect**, **tem** Certifique-se de que o canal de Olá está pronto.
> Além disso, certifique-se de que não tooleave Olá canal no estado pronto sem uma entrada contribuição feed durante um período superior > 15 minutos.
>
>

## <a name="test-playback"></a>Reprodução de teste

Navegue ferramenta AMSE de toohello e clique com o botão direito do rato em Olá canal toobe testado. No menu de Olá, coloque o cursor sobre **Olá reprodução pré-visualização** e selecione **com o Azure Media Player**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

Se o fluxo de Olá aparece no leitor de Olá, o codificador de Olá foi tooAMS tooconnect está corretamente configurada.

Se é recebido um erro, o canal Olá terá toobe reposição codificador as definições e ajustadas. Consulte Olá [resolução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientações.  

## <a name="create-a-program"></a>Criar um programa
1. Depois de reprodução de canal é confirmada, crie um programa. Em Olá **em direto** separador ferramenta AMSE de Olá, com o botão direito clique na área de programa Olá e selecione **criar um novo programa**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. Nome do programa de Olá e, se necessário, ajuste Olá **duração da janela de arquivo** (as horas de too4 predefinições). Também pode especificar uma localização de armazenamento ou deixe como a predefinição de Olá.  
3. Verifique Olá **agora iniciar Olá programa** caixa.
4. Clique em **criar programa**.  

    >[!NOTE]
    >Criação de programa demora menos tempo que a criação do canal.
        
5. Depois de executa o programa de Olá, confirme reprodução clicando com o botão direito do rato em programa Olá e navegar demasiado**reprodução Olá programas** e, em seguida, selecionar **com o Azure Media Player**.  
6. Depois de confirmar, o botão direito do rato em novamente o programa de Olá e selecione **copiar Olá URL de saída tooClipboard** (ou obter estas informações de Olá **definições e as informações do programa** opção do menu de Olá).

fluxo Olá está agora pronto toobe incorporado num leitor ou tooan distribuída a público-alvo live visualização.  

## <a name="troubleshooting"></a>Resolução de problemas
Consulte Olá [resolução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientações.

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
