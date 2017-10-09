---
title: pesquisa de registo do aaaUpgrading Log Analytics do Azure toonew | Microsoft Docs
description: "idioma de consulta de análise de registos nova Olá é quase aqui e pode participar em pré-visualização pública Olá.  Este artigo descreve Olá entre as vantagens do novo idioma de Olá e como tooconvert sua área de trabalho."
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
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Atualizar a sua pesquisa de registo de toonew de área de trabalho do Log Analytics do Azure

> [!NOTE]
> Idioma de consulta de análise de registos nova atualização toohello é demasiado tempo a dar atualmente opcional[atualizem num novo idioma de Olá](https://go.microsoft.com/fwlink/?linkid=856078).  

idioma de consulta de análise de registos nova Olá, e também terá tooupgrade tootake vantajoso área de trabalho do mesmo.  Este artigo descreve Olá entre as vantagens do novo idioma de Olá e como tooconvert sua área de trabalho.  Se não escolher tooupgrade agora, a área de trabalho irá continuar toooperate semelhante à foi sempre, mas será automaticamente convertido numa data posterior.  Receberá muito tempo e notificação quando essa data está definida.

Este artigo fornece detalhes sobre o idioma de nova Olá e o processo de atualização de Olá.

## <a name="why-hello-new-language"></a>Por que motivo Olá novo idioma?
Compreendemos que existe tensão em qualquer transição, e apenas, não são alterar idioma de consulta Olá experimentar Olá do mesmo.  Existem várias razões pelas quais esta alteração irá fornecer valor significativa tooour clientes de análise de registos.

- **Simples mas potentes.** o idioma novo Olá é mais fácil toounderstand e tooSQL semelhante com construções mais como linguagem natural a linguagem de legado Olá.
- **Idioma piping completa.**  novo idioma de Olá tem mais extensas capacidades piping idioma Olá de legado.  Praticamente todos os resultados podem ser direcionado tooanother comando toocreate consultas mais complexas que foram anteriormente possíveis.
- **Extrações de campo de hora de pesquisa.**  novo idioma de Olá suporta campos de tempo de execução calculado mais avançados que o idioma de legado Olá.  Pode utilizar cálculos complexos para campos expandidos e, em seguida, utilize os campos de Olá calculado para os comandos adicionais, incluindo associações e agregações.
- **Associações avançadas.**  novo idioma de Olá fornece associações mais avançadas que idioma legado Olá, incluindo tabelas toojoin de capacidade de Olá em vários campos, utilize associações internas e externas e associar nos campos expandidos.
- **As funções de data/hora.**  novo idioma de Olá tem mais avançadas funções de data/hora que idioma legado Olá.
- **Análise de inteligente.**  novo idioma de Olá tem avançadas padrões de tooevaluate algoritmos nos conjuntos de dados e comparar diferentes conjuntos de dados.
- **Portal de análise avançada.**  Olá portal da análise avançadas oferece funcionalidades de Analysis Services não está disponíveis no portal de análise de registos de Olá incluindo múltiplas edição de consultas, visualizações adicionais e diagnóstico avançado.
- **Consistência com outras aplicações.**  Olá novo idioma e Olá Portal de análise avançadas já são utilizados para análise no Application Insights.  Implementar para análise de registos fornece a consistência entre os serviços do Azure.
- **Melhor integração com o Power BI.** Consultas de idioma novo Olá podem ser exportado tooPower BI Desktop, pelo que pode utilizar as respetivas capacidades de transformação de dados avançados.
- **Muito mais.** Consulte toohello [idioma de consulta de análise do Azure registo](https://docs.loganalytics.io) site para obter detalhes completos e tutoriais no idioma Olá de novo.


## <a name="when-can-i-upgrade"></a>Quando posso atualizar?
atualização Olá será revertida em todas as regiões do Azure, de modo poderão estar disponível em algumas regiões antes de outros utilizadores.  Terá de saber quando a sua área de trabalho está disponível toobe atualizado quando vir a faixa de Olá roxa em Olá parte superior da sua área de trabalho inviting tooupgrade.

![Atualização 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>O que acontece durante a atualização?
Quando converter sua área de trabalho, qualquer pesquisas guardadas, regras de alertas e vistas que criou com Olá estruturador de vistas são automaticamente convertidos toohello novo idioma.  Incluído em soluções de procura não é convertida automaticamente, mas está em vez disso, convertidos no momento de Olá quando abri-los.  Este é completamente transparente tooyou.

## <a name="can-i-go-back-after-i-upgrade"></a>Posso aceda novamente após atualizo?
Quando atualizar, foi efetuada uma cópia de segurança completa da sua área de trabalho que inclui um instantâneo de vistas, regra de alerta e pesquisas guardadas todos os.  Isto permite que toorestore sua área de trabalho antiga se deve mais tarde pretendidos ao nível.

toorestore sua área de trabalho legada, aceda demasiado**definições** na sua área de trabalho e, em seguida, **atualizar resumo**.  Em seguida, pode selecionar a opção de Olá demasiado**restaurar a área de trabalho legacy**.  

![Restaurar legado](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>Como efetuar a atualização de Olá?
Pode atualizar a sua área de trabalho quando vir a faixa de Olá roxa, Olá parte superior do portal de Olá.  

1.  Iniciar o processo de atualização de Olá clicando na faixa do Olá roxa que indica que **saber mais e atualizar**.<br>![Atualização 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Leia Olá obter informações adicionais sobre a atualização Olá na página de informações de atualização de Olá.<br>![Atualização 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  Clique em **atualizar agora** atualização de Olá toostart.<br>![Atualização 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Uma caixa de notificação no canto superior direito Olá mostra o estado de Olá.<br>![Atualização 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  Já está!  Abordar toohave de página de pesquisa de registo toohello uma vista de olhos a área de trabalho atualizada.<br>![Atualização 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Se ocorrer um problema que faz com que toofail atualização Olá, pode aceder toohello [fórum de discussão](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) e publicar a sua pergunta ou [criar um pedido de suporte](../azure-supportability/how-to-create-azure-support-request.md) de Olá portal do Azure.

## <a name="how-do-i-learn-hello-new-language"></a>Como posso saber novo idioma de Olá?
Uma vez que é utilizada por vários serviços Criámos uma [documentação do site externo toohost Olá](https://docs.loganalytics.io/) para o idioma Olá de novo.  Isto inclui tutoriais, amostras e toohelp uma referência completa que pensar toospeed. Pode percorrer um tutorial Olá novo idioma [introdução às consultas](https://go.microsoft.com/fwlink/?linkid=856078) e aceder a referência de linguagem Olá em [langauge de consulta de análise de registos](https://go.microsoft.com/fwlink/?linkid=856079).  

Se já estiver familiarizado com Olá legado Log Analytics consultar idioma apesar, em seguida, pode utilizar o conversor de idioma Olá adicionada como parte da atualização de Olá tooyour área de trabalho.

Basta escrevê na sua consulta legada e, em seguida, clique em **converter** toosee Olá traduzido versão.  Pode, em seguida, um clique Olá pesquisa botão toorun Olá pesquisa ou copiar e colar Olá convertido consulta toouse algures pessoa, tais como uma regra de alerta.

![Conversor de idioma](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>Passos seguintes
- Veja uma [tutorial num novo idioma de Olá](https://go.microsoft.com/fwlink/?linkid=856078).
- Percorrer um [tutorial sobre como utilizar o portal de registo de pesquisa de Olá](log-analytics-log-search-log-search-portal.md) com novo idioma de consulta Olá.
- Obter uma introdução toohello novo [portal da análise avançadas](https://go.microsoft.com/fwlink/?linkid=856587).
