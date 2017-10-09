---
title: "aaaPortals para criação e edição de consultas de registo no Log Analytics do Azure | Microsoft Docs"
description: "Este artigo descreve os portais de Olá que pode utilizar toocreate Log Analytics do Azure e editar pesquisas de registo."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portais para criação e edição de consultas de registo no Log Analytics do Azure

> [!NOTE]
> Este artigo descreve os portais na análise de registos do Azure utilizando a linguagem de consulta Olá novo.  Pode saber mais sobre o novo idioma de Olá e obter Olá procedimento tooupgrade sua área de trabalho em [atualizar a sua pesquisa de registo de toonew de área de trabalho do Log Analytics do Azure](log-analytics-log-search-upgrade.md).  
>
> Se a sua área de trabalho não foi atualizado toohello novo idioma de consulta, devem consultar a demasiado[localizar dados através de pesquisas de registo na análise de registos](log-analytics-log-searches.md) para obter informações sobre a versão atual do Olá do portal de registo de pesquisa de Olá.

Utilizar pesquisas de registo numa variedade de locais em toda a dados do Log Analytics tooretrieve da área de trabalho Olá.  Para, efetivamente, criação e edição de consultas Ademais tooworking interativamente com devolveu dados entanto, tem duas opções são descritas abaixo.  

## <a name="log-search-portal"></a>Portal de pesquisa de registo
portal de registo de pesquisa de Olá é acessível a partir do portal do Azure de Olá ou o portal do OMS Olá.  É adequado para a criação de consultas básicas que podem ser criadas numa única linha.  portal de registo de pesquisa de Olá pode ser utilizado sem iniciar um portal externo e pode utilizá-la tooperform uma variedade de funções com pesquisas de registo, incluindo criar regras de alertas, criar grupos de computadores e exportar Olá os resultados da consulta de Olá.  

portal de registo de pesquisa de Olá fornece várias funcionalidades para editar a consulta de Olá sem ter um conhecimento completo de linguagem de consulta Olá.  Pode obter um resumo destas funcionalidades no [pesquisas de registo de criar na análise de registos do Azure com o portal de registo de pesquisa de Olá](log-analytics-log-search-log-search-portal.md).


![Portal de pesquisa de registo](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Portal da análise avançada
portal de análise avançadas Olá é um portal dedicado que fornece funcionalidade avançada não está disponível no portal de registo de pesquisa de Olá.  Funcionalidades incluem Olá capacidade tooedit uma consulta em várias linhas, seletivamente executar código, o Intellisense context confidencial e análise inteligente.  portal de análise avançadas Olá é mais adequado para conceber consultas complexas que estão a guardar como uma pesquisa de registo ou copiadas e coladas outros elementos de análise de registos.  Inicie o portal de análise avançadas Olá de uma ligação no portal de registo de pesquisa de Olá.

![Portal da análise avançada](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


Devido ao respetivas funcionalidades avançadas, normalmente, utilizará portal de análise avançadas Olá como a principal ferramenta para criação e edição de consultas.  Depois de ter determinado que a consulta de Olá funciona conforme esperado, em seguida, irá copiar e colá-lo noutro local, como o portal de registo de pesquisa de Olá ou estruturador de vistas.  Como o portal de análise avançadas Olá suporta consultas com várias linhas apesar, seguintes elementos terão tootake Olá em consideração quando copiar uma consulta de neste portal.

- Comentários tem de ser removidos da consulta de Olá antes tem copiados e colados para outra localização.  Pode comente uma linha por precedente-lo com duas barras (/ /).  Quando cole uma consulta de linha vários uma única linha, as quebras de linha são removidas.  Se os comentários são incluídos, todos os carateres após o comentário primeiro Olá são considerados parte dos comentários de Olá.


## <a name="next-steps"></a>Passos seguintes

- Percorrer um tutorial sobre como utilizar Olá [portal de registo de pesquisa](log-analytics-log-search-log-search-portal.md) ou Olá [portal da análise avançadas](https://go.microsoft.com/fwlink/?linkid=856587) toocreate consultas.
- Veja uma [tutorial sobre como escrever consultas](https://go.microsoft.com/fwlink/?linkid=856078) utilizando a linguagem de consulta Olá novo.
