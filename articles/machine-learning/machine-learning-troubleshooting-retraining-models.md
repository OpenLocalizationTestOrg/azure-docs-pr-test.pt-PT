---
title: "serviço web de aaaTroubleshoot reparametrização um clássico do Azure Machine Learning | Microsoft Docs"
description: "Identificar e corrigir encontrou de problemas comuns quando são reparametrização modelo Olá para um serviço Web do Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Resolução de problemas Olá reparametrização de um serviço Web clássico do Azure Machine Learning
## <a name="retraining-overview"></a>Reparametrização descrição geral
Ao implementar uma experimentação preditiva como um serviço web classificação é um modelo estático. Modelo de Olá tem toobe retrained como novos dados ficarem disponíveis ou quando consumidor Olá de Olá API tem os seus próprios dados. 

Para instruções completas de Olá reparametrização o processo de um serviço Web clássico, consulte [reparametrização dos Machine Learning modelos através de programação](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>Reparametrização processo
Quando precisar de tooretrain Olá serviço Web, tem de adicionar algumas partes adicionais:

* Um serviço Web implementado de Olá experimentação de preparação. experimentação Olá tem de ter um **saída de serviço Web** módulo ligado resultado toohello Olá **preparar modelo** módulo.  
  
    ![Anexe o modelo de formação do toohello de saída do Olá web service.][image1]
* Um novo ponto final adicionado tooyour da classificação de serviço Web.  Pode adicionar ponto final de Olá programaticamente com o código de exemplo de Olá referenciado no Olá Machine Learning reparametrização dos modelos programáticos do tópico ou através de Olá portal clássico do Azure.

Em seguida, pode utilizar Olá c# código de exemplo do modelo de tooretrain de página de ajuda API do serviço de Olá, formação Web. Depois de o ter avaliado resultados Olá e estiver satisfeito com os mesmos, atualizar modelo treinado Olá da classificação de serviço web utilizando Olá novo ponto final que adicionou.

Com todas as partes de Olá no local, passos principais Olá tem de ter o modelo de Olá tooretrain são:

1. Chamar Olá serviço Web de formação: chamada de Olá é toohello serviço de execução de lote (BES), não Olá serviço de resposta de pedido (RRS). Pode utilizar Olá c# código de exemplo na chamada de Olá de toomake de página de ajuda de Olá API. 
2. Localizar os valores de Olá de Olá *BaseLocation*, *RelativeLocation*, e *SasBlobToken*: estes valores são apresentados no resultado de Olá da sua toohello chamada formação Web Serviço. 
   ![Mostrar resultado Olá Olá reparametrização valores de exemplo e Olá BaseLocation, RelativeLocation e SasBlobToken.][image6]
3. Atualização Olá adicionado ponto final de Olá a classificação de serviço web com Olá novo modelo de preparação: utilizando o código de exemplo de Olá fornecido no Olá Machine Learning reparametrização dos modelos através de programação, atualizar o ponto final de nova Olá adicionou toohello classificação modelo com Olá recentemente modelo treinado do Olá formação Web Service.

## <a name="common-obstacles"></a>Obstacles comuns
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Verifique toosee se tiver Olá, corrija o URL de correção
Olá URL de aplicar o PATCH de mensagens em fila estão a utilizar tem de ser Olá um associados Olá novo ponto final da classificação adicionou toohello da classificação de serviço Web. Existem diversas formas tooobtain Olá PATCH URL:

**Opção 1: X509securitytokenparameters**

Olá tooget corrigir PATCH URL:

1. Executar Olá [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de exemplo.
2. Da saída de Olá de AddEndpoint, determinar Olá *HelpLocation* valor e copie o URL de Olá.
   
   ![HelpLocation na saída de Olá de exemplo de addEndpoint Olá.][image2]
3. Cole o URL de Olá uma página tooa toonavigate de browser que fornece ligações de ajuda para Olá serviço Web.
4. Clique em Olá **atualização recursos** página de ajuda do ligação tooopen Olá patch.

**Opção 2: Utilizar Olá portal clássico do Azure**

1. Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Separador de Machine Learning Olá aberta. ![Separador leaning da máquina.][image4]
3. Clique no nome de área de trabalho, em seguida, **serviços Web**.
4. Clique em Olá serviço Web que estiver a trabalhar com a classificação. (Se não tiver modificado o nome predefinido de Olá do serviço web de Olá, vai terminar dentro de [classificação Exp]..)
5. Clique em **adicionar ponto final**.
6. Depois de é adicionado ponto final de Olá, clique em nome do ponto final Olá. Em seguida, clique em **atualização recursos** tooopen Olá página de ajuda de aplicação de patches.

> [!NOTE]
> Se tiver adicionado Olá endpoint toohello serviço Web de formação em vez de Olá preditiva serviço Web, receberá Olá seguinte erro ao clicar em Olá **atualização recursos** ligação: Lamentamos, mas esta funcionalidade não é suportada ou está disponível neste contexto. Este serviço Web tem não existem recursos atualizáveis. Iremos desculpa pelo incómodo do Olá e a trabalhar para melhorar este fluxo de trabalho.
> 
> 

![Dashboard de ponto final de novo.][image3]

página de ajuda de PATCH Olá contém Olá PATCH URL tem de utilizar e fornece o código de exemplo, pode utilizar toocall-lo.

![URL de patch.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Verifique toosee que estão a atualizar o ponto final de classificação corretos Olá
* Não aplicar o patch Olá serviço Web de formação: operação de patch Olá deve ser executada no Olá da classificação de serviço Web.
* Não aplicar o patch ponto final predefinido de Olá no serviço Web: tem de efetuar a operação de patch de Olá no Olá nova classificação de ponto final do serviço Web que adicionou.

Pode verificar o ponto final do Web service Olá está ativada por Olá visitando o portal clássico do Azure. 

> [!NOTE]
> Lembre-se de que está a adicionar o ponto final de Olá toohello serviço Web preditiva, Olá formação Web Service. Se tiver implementado corretamente uma formação e um serviço Web preditiva, deverá ver dois serviços Web separados listados. Olá preditiva serviço Web deve terminar com "[exp preditiva.]".
> 
> 

1. Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Separador de Machine Learning Olá aberta. ![Machine learning área de trabalho da IU.][image4]
3. Selecione a sua área de trabalho.
4. Clique em **serviços Web**.
5. Selecione o seu serviço Web preditiva.
6. Certifique-se de que o novo ponto final foi adicionado o serviço Web de toohello.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Verifique a área de trabalho de Olá que o serviço web está a ser tooensure está numa região corretos Olá
1. Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Selecione o Machine Learning a partir do menu de Olá.
   ![Machine learning região da IU.][image4]
3. Certifique-se a localização de Olá da sua área de trabalho.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
