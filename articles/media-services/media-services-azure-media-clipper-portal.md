---
title: Utilize o Recortador de Media Services do Azure no Portal do | Microsoft Docs
description: "Criar aplicações de clips utilizando Recortador de suporte de dados do Azure do Portal do Azure"
services: media-services
keywords: "Clip; subclip codificação; suporte de dados"
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: 1deca68cd6a61ede7536c4d5544036a10c54209b
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/07/2017
---
# <a name="create-clips-with-azure-media-clipper-in-the-portal"></a>Criar aplicações de clips com Recortador de suporte de dados do Azure no portal
Pode utilizar o Recortador de suporte de dados do Azure no portal para criar aplicações de clips de recursos nas suas contas de serviços de suporte de dados. Para começar a utilizar, navegue até à sua conta de media services no portal. Em seguida, selecione o **Subclip** separador.

No **Subclip** separador, tiver a capacidade para iniciar a aplicações de clips de composição. No portal, o Recortador carrega MP4s de velocidade de transmissão única MP4s de transmissão múltipla, arquivos e em direto que são publicados com um localizador de transmissão em fluxo válido. Anular a publicação de recursos não estão carregados.

O Recortador está atualmente em pré-visualização pública. Para aceder a Recortador no portal do Azure, aceda a este [página pré-visualização pública](https://portal.azure.com/?feature.subclipper=true).

A imagem seguinte ilustra a página de destino Recortador na sua conta de media services: ![Recortador de suporte de dados do Azure no portal do Azure](media/media-services-azure-media-clipper-portal/media-services-azure-media-clipper-portal.png)

## <a name="producing-clips"></a>Aplicações de clips de produção
Para criar um clip, arraste e largue um recurso para a interface clip. Se os tempos de marca são conhecidos, pode introduzi-las manualmente na interface do. Caso contrário, o elemento de reprodução ou arraste o playhead para localizar o marca-in pretendido e Escalamento de marca de tempo. Se não for fornecido um tempo de marca- ou marca, o clip inicia a partir do início ou continua o fim do recurso de entrada, respetivamente.

Para navegar com moldura precisão/GOP precisão, utilize os botões de moldura direta/GOP direta ou frame-com versões anteriores/GOP-com versões anteriores. Para recorte contra vários recursos, arraste e largue a vários recursos na interface do clip a partir do painel de seleção de elemento. Pode selecionar e reordenar ativos na interface para a ordem pretendida. O painel de seleção de elemento fornece a duração de recurso, tipo e metadados de resolução para cada recurso. Quando a concatenar vários recursos em conjunto, considere a resolução de origem de cada ficheiro de entrada. Se as resoluções de origem diferirem, inferior de resolução de entrada é upscaled para satisfazer a resolução do elemento de resolução máxima. Para pré-visualizar a saída da tarefa de recorte, selecione o botão de pré-visualização e o clip reproduz a partir dos tempos de marca selecionado.

## <a name="producing-dynamic-manifest-filters"></a>Produzir o manifesto de filtros dinâmicos
[Filtros de manifesto dinâmicos](https://azure.microsoft.com/blog/dynamic-manifest/) descrevem um conjunto de regras com base nos atributos de manifesto e a linha cronológica de recurso. Estas regras determinam a forma como o ponto final de transmissão em fluxo manipula listas de reprodução de saída (manifesto). O filtro pode ser utilizado para alterar os segmentos são transmissão em fluxo para reprodução. Os filtros produzidos pelo Recortador são filtros locais e que são específicos para o elemento de origem. Ao contrário das aplicações de clips compostas, os filtros não são elementos novo e não necessitam de uma tarefa de codificação para produzir. Podem ser rapidamente criadas através do [.NET SDK](https://docs.microsoft.com/azure/media-services/media-services-dotnet-dynamic-manifest) ou [REST API](https://docs.microsoft.com/azure/media-services/media-services-rest-dynamic-manifest), no entanto, estão apenas GOP corretas. Normalmente, ativos codificados para transmissão em fluxo têm um tamanho de GOP de dois segundos.

Para criar um filtro de manifesto dinâmico, navegue para o **ativos** separador e selecione o elemento pretendido. Selecione o **Subclip** botão para menu superior. Selecione o filtro de manifesto dinâmico pois o modo de recorte no menu de definições avançadas. Em seguida, pode seguir o mesmo processo para produzir um clip composto para criar o filtro. Filtros só podem ser produzidos a partir de um único recurso.

A imagem seguinte ilustra o Recortador no modo de filtro de manifesto dinâmica no portal do Azure: ![Recortador de suporte de dados do Azure em modo de filtro de manifesto dinâmica no portal do Azure](media/media-services-azure-media-clipper-portal/media-services-azure-media-clipper-filter.PNG)

## <a name="submitting-clipping-jobs"></a>Submeter tarefas de recorte
Quando tiver terminado de composição o clip, selecione o botão para submeter tarefa para iniciar a tarefa de recorte correspondente ou chamada de manifesto dinâmica.

## <a name="next-steps"></a>Passos seguintes
Para começar a utilizar o Recortador de suporte de dados do Azure, leia o [introdução](media-services-azure-media-clipper-getting-started.md) artigo para obter detalhes sobre como implementar o widget.