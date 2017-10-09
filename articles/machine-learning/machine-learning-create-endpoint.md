---
title: "pontos finais do serviço de Web aaaCreating no Machine Learning | Microsoft Docs"
description: "A criação de pontos finais do serviço Web no Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Criar Pontos Finais
> [!NOTE]
>  Este tópico descreve tooa aplicável técnicas **clássico** serviço Web do Machine Learning.
> 
> 

Quando criar serviços Web que propor tooyour reencaminhar clientes, terá de tooprovide modelos de formação tooeach cliente que são experimentação toohello ainda ligado do qual Olá Web o serviço foi criado. Além disso, quaisquer atualizações toohello experimentação deve ser aplicadas seletivamente tooan endpoint sem substituir personalizações Olá.

tooaccomplish, o Azure Machine Learning permite-lhe toocreate vários pontos finais para um serviço Web implementado. Cada ponto final no serviço Web de Olá independentemente é resolvido, limitado e gerido. Cada ponto final é uma chave exclusiva de autorização e de URL que pode distribuir tooyour clientes.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Adicionar pontos finais tooa Web serviço
Existem três formas tooadd um tooa ponto final de serviço Web.

* Através de Programação
* Através do portal de serviços Web do Azure Machine Learning Olá
* Embora Olá portal clássico do Azure

Assim que for criado o ponto final de Olá, pode consumi-lo através de APIs síncronas, batch APIs e folhas de cálculo do excel. Além disso tooadding pontos finais através deste IU, também pode utilizar Olá APIs de gestão do ponto final tooprogrammatically adicionar pontos finais.

> [!NOTE]
> Se tiver adicionado os pontos finais adicionais toohello serviço Web, não é possível eliminar o ponto final do Olá predefinido.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Adicionar um ponto final através de programação
Pode adicionar um serviço Web do ponto final tooyour através de programação utilizando Olá [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de exemplo.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Adicionar um ponto final com o portal de serviços Web do Azure Machine Learning Olá
1. No Machine Learning Studio, na coluna de navegação esquerdo Olá, clique em serviços Web.
2. Na parte inferior de Olá do dashboard de serviço Web de Olá, clique em **gerir pontos finais**. portal de serviços Web do Azure Machine Learning Olá abre a página de pontos finais de toohello para Olá serviço Web.
3. Clique em **Novo**.
4. Escreva um nome e descrição para o ponto final de nova Olá. Os nomes de ponto final tem de ser 24 caráter ou menos de comprimento e devem ser constituídos por europeus minúsculas ou números. Selecione o nível de registo Olá e se os dados de exemplo estão ativados. Para obter mais informações sobre o registo, consulte [ativar o registo de serviços Web do Machine Learning](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Adicionar um ponto final com Olá portal clássico do Azure
1. Inicie sessão no toohello [portal clássico do Azure](http://manage.windowsazure.com), clique em **Machine Learning** na coluna esquerda Olá. Clique em área de trabalho de Olá que contém o serviço Web de Olá no qual está interessado.
   
    ![Navegue tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. Clique em **serviços Web**.
   
    ![Navegue tooWeb serviços](./media/machine-learning-create-endpoint/figure-2.png)
3. Clique em serviço Web de Olá estiver interessado na lista de Olá toosee de pontos finais disponíveis.
   
    ![Navegue tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. Na Olá parte inferior da página Olá, clique em **adicionar ponto final**. Escreva um nome e uma descrição, certifique-se de que existem não existem pontos finais com Olá mesmo nome neste serviço Web. Deixe o nível de limitação de Olá com o respetivo valor predefinido, salvo se tiver requisitos especiais. toolearn mais informações sobre limitação, consulte [Dimensionar pontos finais da API](machine-learning-scaling-webservice.md).
   
    ![Criar o ponto final](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Passos Seguintes
[Como tooconsume um serviço Web do Azure Machine Learning](machine-learning-consume-web-services.md).

