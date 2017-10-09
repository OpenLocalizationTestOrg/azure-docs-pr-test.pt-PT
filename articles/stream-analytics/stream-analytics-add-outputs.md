---
title: produz aaaHow tooconfigure dados para tarefas do Stream Analytics | Microsoft Docs
description: "Configure as saídas para tarefas do Stream Analytics | Learning segmento de caminho."
keywords: "dados de saída, movimento de dados"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>Como os dados de tooconfigure produz para tarefas do Stream Analytics

Tarefas do Stream Analytics do Azure podem ser ligado tooone ou mais saídas de dados, que definem um receptor de dados existente do ligação tooan. Como a tarefa de Stream Analytics processa e transformações de dados de entrada, um fluxo de eventos de saída de dados é escrito na saída da tarefa tooyour.

Saídas de dados do Stream Analytics podem ser toosource utilizado dashboards de em tempo real ou alertas, fluxos de trabalho de movimento de dados de Acionador ou simplesmente os dados de arquivo para o processamento de lote mais tarde. Do Stream Analytics tem integração de primeira classe com vários serviços do Azure, que estão documentados em detalhe aqui.

uma tarefa de Stream Analytics tooyour saída tooadd:

1. No Olá [portal do Azure](https://portal.azure.com), abra o seu trabalho e clique em **saídas** e, em seguida, clique em **adicionar** no painel de saídas Olá que aparece.
   
    ![Adicione saídas](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Forneça um nome amigável para esta saída no Olá **Alias de saída** caixa. Este nome pode ser utilizado na consulta da tarefa mais tarde no toorefer toohello saída.  
   
    Preencha o resto Olá Olá necessário ligação propriedades tooconnect tooyour saída.  Estes campos variam consoante o tipo de resultado e estão definidos em detalhe aqui.  
   
    ![Escolha o tipo de movimento de dados](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. Dependendo do tipo de saída Olá, poderá ser necessário toospecify como dados de Olá são serializados ou formatados. definições de serialização específica de Olá para cada tipo de saída estão documentadas aqui.
   
    Preencha o resto Olá Olá ligação necessárias propriedades tooconnect tooyour da origem de dados. Estes campos variam consoante o tipo de entrada e de origem e estão definidos em detalhe no Olá [artigo Criar tarefa](stream-analytics-create-a-job.md).  

> [!Note]
>
> Qualquer tarefa adicionada toohello do elemento de saída, tem de existir antes de Olá a tarefa foi iniciada e eventos de iniciar o fluxo. Por exemplo, se utilizar o Blob storage como resultado, a tarefa de Olá não criará uma conta do storage automaticamente. Tem de toobe criado por utilizador Olá antes Olá ASA a tarefa foi iniciada.
> 
 

## <a name="get-help"></a>Obter ajuda
Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

