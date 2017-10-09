---
title: "aaaCortana manual de comunicação social Intelligence solução modelo para prever a pedido de energia | Microsoft Docs"
description: "Um modelo de solução com o Microsoft Cortana Intelligence que ajuda a prever a pedido para uma empresa de utilitário de energia."
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>Manual de modelo do Cortana Intelligence solução para prever a pedido de energia
## <a name="executive-summary"></a>Resumo Executivo
No Olá passado alguns anos, Internet das coisas (IoT), as origens de energia alternativo e macrodados intercalado oportunidades vasta toocreate no utilitário Olá e o domínio de energia. Em Olá mesmo tempo, o utilitário de Olá e o setor de energia todo Olá tem visto consumo pelo com os consumidores pedir o seu trabalho melhor formas toocontrol a sua utilização de energia. Por conseguinte, Olá utilitário e grelha inteligente empresas são na necessidade excelente tooinnovate e renovar próprios. Além disso, muitos grelhas de ativação e utilitários são se tornar toomaintain desatualizado e é muito dispendiosa e gerir. Durante o último ano Olá, equipa Olá tem estado a trabalhar num número de ações de envolvimento dentro do domínio de energia Olá. Durante estas ações de envolvimento, encontrámos muitos casos, no qual Olá utilitários ou ISVs (os fabricantes independentes de Software) tem sido à procura para previsão para o pedido de energia futuras. Estes previsões desempenham um papel importante na respetiva atuais e futura da empresa e ficam foundation Olá vários casos de utilização. Estes incluem previsão da carga de energia de curto e longo prazo, comerciais, balanceamento de carga, otimização de grelha etc. Métodos de análise avançadas (AA) como o Machine Learning (ML) e de macrodados são ativadores principais Olá para produzir previsões exatas e fiáveis.  

Este manual de comunicação social, iremos juntar negócio Olá e diretrizes analíticas necessárias para o desenvolvimento com êxito e implementação de procura de energia previsão solução. Podem ajudar a estas diretrizes propostos utilitários, cientistas de dados e engenheiros de dados no estabelecer soluções totalmente operacionalizadas, baseado na nuvem, a pedido de previsão. Para as empresas que estão a iniciar os macrodados e journey análises avançadas, tal uma solução pode representar seed inicial do Olá na respetiva estratégia a longo prazo grelha inteligente.

> [!TIP]
> toodownload um diagrama que fornece uma descrição geral da arquitetura deste modelo, consulte [arquitetura de modelo de solução do Cortana Intelligence para prever a pedido de energia](cortana-analytics-architecture-demand-forecasting-energy.md).  
> 
> 

## <a name="overview"></a>Descrição geral
Este documento abrange Olá business, dados e aspetos técnicos da utilização do Cortana Intelligence e no específica do Azure Machine Learning (AML) para implementação de Olá e a implementação de soluções de previsão de energia. documento de Olá consiste em três partes principais:  

1. Noções sobre empresas  
2. Compreensão de dados  
3. Implementação técnica

Olá **compreensão de negócio** parte destaca Olá toounderstand de necessidades do negócio aspeto um e considere toomaking anterior uma decisão de investimento. Explica como tooqualify Olá problema empresarial no tooensure mão Análise Preditiva e a aprendizagem são realmente eficaz e aplicável. obter documento de Olá explica Olá Noções básicas do machine learning e como é utilizado tooaddress previsão de energia problemas. -Descreve os pré-requisitos de Olá e critérios de qualificação Olá de um caso de utilização. Alguns exemplo utilizar casos e cenário de negócio cenários também são fornecidos.

Os dados são ingredient principal do Olá para qualquer solução de aprendizagem. Olá **dados compreender** parte deste documento abrange alguns aspetos importantes da dados Olá. -Descreve o tipo Olá dos dados que é necessária para a previsão de energia, requisitos de qualidade de dados e, normalmente, existem que origens de dados. Também vamos explicar como dados não processados Olá são funcionalidades de dados de tooprepare utilizados que, na verdade, unidade Olá modelação parte.

Olá terceiro parte documento Olá abrange Olá **implementação técnica** aspeto de uma solução. Engenharia da funcionalidade e modelação são núcleo Olá do processo de ciência de dados de Olá e, por conseguinte, estão a ser abordados em detalhe. Abrange conceito de Olá de serviços web, que são um vehicle importante para a implementação de nuvem das soluções de Análise Preditiva. Podemos também descrevem uma arquitetura típica de uma solução de operacionalizado ponto-a-ponto.

Além disso, o documento de Olá inclui o material de referência que pode utilizar toogain mais compreensão do domínio Olá e tecnologia.

É importante toonote que não pretendemos toocover neste documento Olá mais profundo dados ciência processo, os aspetos de matemática e técnicos. Estes detalhes podem ser encontrados na [documentação do Azure ML](http://azure.microsoft.com/services/machine-learning/) e [blogues](http://blogs.microsoft.com/blog/tag/azure-machine-learning/).

### <a name="target-audience"></a>Público-alvo
Olá público-alvo para este documento é empresariais e técnicos técnicos que gostaria de dados de conhecimento toogain e compreensão do Machine Learning com base em soluções e como estas estão a ser utilizadas especificamente dentro do domínio de previsão de energia Olá.

Cientistas de dados também podem beneficiar de ler este documento toogain uma melhor compreensão do processo de nível elevado de Olá que unidades Olá implementação de uma solução de previsão de energia. Também pode ser utilizado tooestablish uma linha de base de um bom ponto de partida para obter mais informações detalhadas e avançadas material neste contexto.

### <a name="industry-trends"></a>Tendências de setor
No Olá passado alguns anos, IoT, origens de energia alternativo e macrodados intercalado oportunidades vasta toocreate no utilitário Olá e o espaço de energia. Em Olá mesmo tempo, o utilitário de Olá e setores de energia todo Olá tem visto consumo pelo com os consumidores pedir o seu trabalho melhor formas toocontrol a sua utilização de energia.

Muitos utilitário e de empresas de energia inteligente tem sido pioneering Olá [grelha inteligente](https://en.wikipedia.org/wiki/Smart_grid) ao implementar um número de utilização casos que tornam a utilização de dados de Olá gerados pela grelha Olá. Muitos casos de utilização está centrada características de inerente Olá de produção de eletricidade no: não é possível ser acumulado nem reservados armazenada como o inventário. Por isso, o que é produzido tem de ser utilizado. Utilitários de que pretende toobecome mais eficiente do que precisam de consumo de energia tooforecast simplesmente porque que irá conceder-lhes maior capacidade demasiado**equilibrar procura e oferta**, impedindo wastage de energia, **reduzir greenhouse gás emission**e controlar os custos.

Quando se fala dos custos, há outro aspeto importante, o que é o preço. Novo power de tootrade capacidades entre utilitários ter colocado numa excelente precisa demasiado**previsão pedido futuro e preços futuros de eletricidade**. Isto pode ajudar as empresas determinar os volumes de produção.

Quando utilizamos word Olá 'inteligente', mas, na verdade, consulte tooa grelha que pode saber mais e, em seguida, fazer predições. Pode antecipa sazonais alterações no consumo, bem como **previr situações de sobrecarga temporária e ajustar automaticamente para a mesma**. Por remotamente regular consumo (com a ajuda de Olá destes medidores inteligentes), podem ser processadas situações de sobrecarga localizada. **Ao prever primeiro e, em seguida, agir**, grelha Olá torna-se mais inteligentes ao longo do tempo.

Para o resto deste documento incidirá numa família específica de casos de utilização que abrangem a previsão de futuro, Olá curta e longa duração pedido de energia. Iremos tem estado a trabalhar nas seguintes áreas para alguns meses e ter adquirido alguns dados de conhecimento e skill permitem-nos resultados de nível tooproduce da indústria. Outros casos de utilização vai ser abordados bem documento Olá no Olá quase futuro.

## <a name="business-understanding"></a>Compreensão Empresarial
### <a name="business-goals"></a>Objetivos de negócio
Olá **demonstração de energia** objetivo é toodemonstrate uma análise preditiva típica e aprendizagem de solução que pode ser implementada num intervalo de tempo muito curto. Especificamente, o nosso foco atual é ativar soluções de previsão de energia a pedido para que o valor de negócio pode ser realizado e aproveitado após rapidamente. informações Olá este manual de comunicação social podem ajudar cliente Olá realizar Olá os seguintes objetivos:

* Solução baseada na toovalue curto período de tempo de aprendizagem
* Capacidade tooexpand um tooother caso de utilização piloto utilizar casos ou âmbito mais amplo tooa com base na respetiva necessidade de negócio
* Obter rapidamente conhecimento do produto Cortana Intelligence Suite

Com estes objetivos em mente, este manual de comunicação social visa a entrega de negócio Olá e conhecimentos técnicos que irão ajudar a alcançar estes objetivos.

### <a name="power-load-and-demand-forecasting"></a>Carga de energia e prever a pedido
Dentro do setor de energia Olá, podem existir várias formas em que a pedido previsão pode ajudar a resolver problemas de negócio crítico. Na verdade, de previsão pedido pode ser considerada foundation Olá vários núcleos casos de utilização no setor Olá. Em geral, podemos considerar dois tipos de previsões de pedido de energia: curto e longo prazo. Cada um deles pode servem um objetivo diferente e utilizar uma abordagem diferente. Olá a principal diferença entre Olá duas é a Olá horizon, que significa Olá intervalo de tempo para Olá futura para o qual podemos seria previsão de previsão.

#### <a name="short-term-load-forecasting"></a>A curto prazo carga previsão
Dentro do contexto de Olá de procura de energia, a curto prazo carregar previsão (STLF) está definido como Olá agregados carga é prevista no Olá quase futuro em várias partes da grelha de Olá (ou grelha Olá como um todo). Neste contexto, a curto prazo é definido toobe horizon de tempo dentro do intervalo de Olá de horas too24 de 1 hora. Em alguns casos, um horizon de 48 horas também é possível. Por conseguinte, STLF é muito comum num cenário de utilização operacional da grelha de Olá. Seguem-se alguns exemplos de STLF orientadas por casos de utilização:

* Procura e oferta balanceamento
* Suporte de comercial de energia
* Efetuar mercado (preço de energia definição)
* Otimização de operacional de grelha
* [Resposta a pedido](https://en.wikipedia.org/wiki/Demand_response)
* Pico de previsão a pedido
* Gestão de lado de pedido
* Balanceamento de carga e a prevenção de sobrecarga
* Longo prazo previsão de carga
* Deteção de anomalias e de falhas
* Curtailment/nivelamento das horas de ponta 

Modelo STLF baseiam-se principalmente no Olá perto anteriores (últimos dias ou semanas) os dados de consumo e utilize previstosm temperatura como uma previsão da receita importante. Obter temperatura exata previsão para Olá hora seguinte e cópia de segurança too24 horas se está a tornar inferior de um desafio dias agora. Estes modelos são menos sensíveis tooseasonal padrões ou tendências de consumo de longo prazo.

Soluções SLTF também são toogenerate provável elevado volume de chamadas de predição (pedidos de serviço), uma vez que estão a ser invocados numa base horária e em alguns casos, mesmo com maior frequência. Também é muito comum toosee implantation, onde cada substation individuais ou transformador é representada como um modelo de autónomo e, por conseguinte, volume Olá de predição pedidos são maiores.

#### <a name="long-term-load-forecasting"></a>Longo prazo previsão de carga
o objetivo de Olá de longo prazo carga previsão (LTLF) é a pedido de energia tooforecast com um horizon tempo vão de meses de toomultiple 1 semana (e, em alguns casos, para um número de anos). Este intervalo de horizon principalmente é aplicável para o planeamento e casos de utilização do investimento.

Para cenários de longa duração, é importante toohave dados de alta qualidade que abrange um intervalo de vários anos (mínimo 3 anos). Estes modelos normalmente extrair padrões de sazonalidade de dados históricos Olá e utilizar predicators externos, tais como meteorologia e climático padrões.

É importante tooclarify hello mais Olá previsão horizon é, poderá ser Olá menos previsão exata Olá. Consequentemente, é importante tooproduce previsão alguns intervalos de confiança, juntamente com Olá real que lhe permita humans variação de possíveis Olá toofactor no respetivo processo de planeamento.

Uma vez que o cenário de consumo de Olá para LTLF principalmente está a planear, iremos pode esperar muito inferiores volumes de predição (como em comparação com tooSTLF). É, normalmente, poderá ver estas predições incorporadas nas ferramentas de visualização, tais como o Excel ou do Power BI e ser invocados manualmente pelo utilizador Olá.

### <a name="short-term-vs-long-term-prediction"></a>Curto prazo vs. Predição de longo prazo
Olá, a tabela seguinte compara STLF e LTLF no relativamente toohello mais importantes atributos:

| Atributo | Previsão da carga de curto prazo | Previsão da carga de longo prazo |
| --- | --- | --- |
| Previsão Horizon |Das horas de too48 1 hora |1 too6 meses ou mais |
| Granularidade de dados |Por Hora |Hora ou diária |
| Casos de utilização típica |<ul><li>A pedido/alimentação balanceamento</li><li>Escolha a hora de previsão</li><li>Resposta a pedido</li></ul> |<ul><li>De longo prazo planeamento</li><li>Planeamento de recursos de grelha</li><li>Planeamento de recursos</li></ul> |
| Predictors típicas |<ul><li>Dia ou semana</li><li>Hora do dia</li><li>Temperatura por hora</li></ul> |<ul><li>Último mês do ano</li><li>Dia do mês</li><li>Temperatura de longo prazo e climático</li></ul> |
| Intervalo de dados históricos |Dois toothree anos de dados |Cinco too10 anos de dados |
| Precisão típica |MAPE * de 5% ou inferior |MAPE * de 25% ou inferior |
| Frequência de previsão |Produzidos de hora a hora ou a cada 24 horas |Produzidos depois mensal, trimestral ou anuais |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) – significa erros percentagem média

Como podem ser vistos desta tabela, é importante bastante toodistinguish entre Olá curto e longo prazo de Olá previsão cenários como estas representam as necessidades de negócio diferentes e poderão ter de implementação diferentes e padrões de consumo.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>Caso de utilização de exemplo 1: eSmart sistemas – otimização de sobrecarga
Uma função importante de um [grelha inteligente](https://en.wikipedia.org/wiki/Smart_grid) toodynamically e constantemente otimizar e ajustar Olá alterar os padrões de consumo. Consumo de energia pode ser afetado por alterações de curto prazo que principalmente são causadas por flutuações de temperatura (*por exemplo,*, maior potência de é utilizada para a condição de ar ou aquecimento). AT Olá mesmo tempo, o power consumo também é deve influenciado pelos tendências de longo prazo. Estes podem incluir efeitos sazonalidade, feriados national, longo prazo crescimento de consumo e até mesmo económico fatores, tais como o índice de consumidor, o preço de petróleo e GDP.

Neste caso de utilização, [eSmart](http://www.esmartsystems.com/) pretendia solução de toodeploy uma conta baseada na nuvem que lhe permite prever propensity Olá de uma situação de sobrecarga em qualquer substation determinado da grelha de Olá. Em particular, eSmart pretendia substations tooidentify que estão provavelmente toooverload dentro Olá hora seguinte, por isso uma ação imediata foi tomada tooavoid ou resolver nessa situação.

Um exata e rápido efetuar predição requer a implementação de três modelos preditivos:

* Modelo de prazo longo que permite previsão de consumo de energia em cada substation durante Olá seguinte algumas semanas ou meses
* Modelo de curto prazo, que permite a predição de sobrecarga situação em que um determinado substation durante Olá hora seguinte
* Modelo de temperatura que fornece a previsão de temperatura futura ao longo de vários cenários

o objetivo do modelo de longa duração Olá Olá é substations de Olá toorank pelo respetivo toooverload propensity (fornecido a respetiva capacidade de transmissão de energia) durante a Olá próximas semanas ou meses. Isto permite a criação de uma lista de curto período de substations serviria como entrada para a predição de curta duração Olá Olá. Como temperatura é uma previsão da receita importante para o modelo de longa duração Olá, é uma necessidade tooconstantly produzir cenário multi relativos à temperatura previsões e feed-los como entrada para o modelo de longa duração toohello. curta Olá previsão, em seguida, é invocado toopredict que substation está toooverload provável sobre Olá hora seguinte.

modelos de curto e longo prazo Olá são implementados individualmente por cada substation. Por conseguinte, Olá execução práticas estes modelos exige um vasto conjunto orchestration. se encontra dedicado para cada hora do dia de Olá toogain exatidão da previsão superior Olá curto prazo, um modelo mais granular. Todos os estes modelos são executados a cada hora e concluir a execução dentro de alguns minutos tooallow suficientes tempo toorespond e tome medidas preventivo, se necessário. Esta coleção de modelos onde permanece atualizada por reparametrização periodical utilizando os dados mais recentes Olá.

Podem encontrar mais informações sobre este caso de utilização [aqui](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945).

#### <a name="use-case-qualification-criteria--prerequisites"></a>Utilizar critérios de qualificação maiúsculas – pré-requisitos
segurança de principal de Olá do Cortana Intelligence é no respetivo toodeploy de capacidade de elevado desempenho e dimensionamento machine learning centrado em soluções. É concebida toosupport milhares das predições que são executados em simultâneo. Pode dimensionar automaticamente toomeet um padrão de consumo de alteração. Foco uma solução por conseguinte, é precisão e o desempenho de capacidade de cálculo. Por exemplo, uma empresa de utilitário está interessada em produção a pedido de energia exata previsão para Olá hora seguinte e para cada hora do dia de Olá. No Olá por outro lado, mas é menos interessadas em resposta a Olá pergunta sobre por que razão a pedido de Olá é toobe prevista à (próprio modelo de Olá tratará do que).

Consequentemente, é importante toorealize que nem todos os casos de utilização e problemas empresariais possam ser resolvidos de forma eficaz a aprendizagem a utilizar.

Cortana Intelligence e de aprendizagem não foi possível altamente eficazes no resolver um problema empresarial fornecido quando forem cumprida Olá os seguintes critérios:

* Olá problema empresarial no mão é **preditiva** natureza. Um exemplo de cenário de utilização preditiva é uma empresa de utilitário que gostaria que a carga de energia toopredict um determinado substation durante Olá hora seguinte. No Olá por outro lado, analisar e classificação controladores de procura histórica seria **descritivo** natureza e, por conseguinte, menos aplicável.
* Há um eliminar **caminho de ação** toobe executada uma vez predição Olá está disponível. Por exemplo, prever uma sobrecarga num substation durante Olá hora seguinte pode acionar uma ação proativa de reduzir a carga que está associada esse substation e, potencialmente, impedindo uma sobrecarga.
* caso de utilização de Olá representa um **típico tipo de problema** forma que quando resolvidos pode pave Olá forma toosolving outros casos de utilização semelhante.
* Pode definir cliente Olá **objetivos quantitativos e qualitativa** toodemonstrate uma implementação de solução concluída com êxito. Por exemplo, um objetivo quantitativo boa para previsão de pedido de energia seria o limiar de precisão necessária Olá (*por exemplo,*, cópia de segurança too5 é permitido o erro %) ou quando prever sobrecarga substation, em seguida, precisão Olá (taxa de positivos true) e devolução de chamada (extensão de positivos verdadeiros) deve ser acima de um determinado limiar. Estes objetivos devem ser derivados de objetivos de negócio do cliente Olá.
* Há um eliminar **o cenário de integração** com o fluxo de trabalho da empresa Olá empresariais. Por exemplo, previsão da carga Olá substation pode ser integrada no Olá grelha controlo tooallow sobrecarga prevenção as atividades do centro.
* o cliente de Olá tem toouse pronto **dados com qualidade suficiente** toosupport Olá utilizar as maiúsculas e minúsculas (ver mais na secção seguinte, Olá, **qualidade dos dados**, neste manual de comunicação social).
* Olá arquitetura de centrado em dados de nuvem Adote o cliente ou **aprendizagem baseado na nuvem**, incluindo do Azure ML e outros componentes do Cortana Intelligence Suite.
* cliente de Olá é disposto tooestablish **um fluxo de dados do fim tooend** que instalações Olá entrega de dados numa nuvem Olá numa base contínua e está dispostas demasiado**operacionalizar** Olá solução.
* cliente de Olá está pronto demasiado**dedicar recursos** que irá ser ativamente envolvidos durante a implementação piloto inicial de Olá, para que os dados de conhecimento e propriedade da solução de Olá podem ser transferidos toohello cliente após com êxito conclusão.
* recurso de cliente Olá deve ser um **professional dados intruso qualificado**, preferencialmente, uma scientist de dados.

Qualificação de um caso de utilização com base no Olá os critérios acima pode significativamente melhorar as taxas de êxito de Olá de um caso de utilização e estabelecer uma boa beachhead para implementação Olá casos de utilização futura.

### <a name="cloud-based-solutions"></a>Soluções baseadas na nuvem
Cortana Intelligence Suite no Azure é um ambiente integrado que reside na nuvem de Olá. implementação de Olá de uma solução de análise avançadas num ambiente de nuvem detém vantagens significativas para empresas e no Olá mesmo tempo pode significar que alteração grande para as empresas que ainda utilize no local soluções de TI. Dentro do setor de energia Olá, há uma tendência clara da migração gradual operações na nuvem do Olá. Esta tendência fica manualmente no manualmente, juntamente com o desenvolvimento de Olá de grelha inteligente Olá conforme mencionado acima, no **tendências da indústria**. Como este manual de comunicação social concentra-se numa solução baseada na nuvem no domínio de energia Olá, é importante tooexplain vantagens de Olá e outras considerações de implementação de uma solução baseada na nuvem.

Talvez hello maior partido de uma solução baseada na nuvem é Olá custo. Como uma solução utilizam componentes de implementação de nuvem, não os custos de compromisso ou os custos de componente de COGS (custo de bens vendida) associados ao mesmo. Isto significa que existe tooinvest sem necessidade de hardware, software e manutenção IT, e, por conseguinte, não há uma redução substancial no risco de negócio.

Outra vantagem importante é Olá custo pay as you go estrutura das soluções baseado na nuvem. Servidores baseados na nuvem para armazenamento ou de informática podem ser implementadas e dimensionados de forma just-como-necessário. Isto representa Olá partido de eficácia de custo de uma solução baseada na nuvem.

Por fim, há sem necessidade de investir no desenvolvimento de infraestrutura futuras ou manutenção IT como tudo isto faz parte da oferta de baseado na nuvem Olá. a extensão toothat, Cortana Intelligence Suite inclui Olá melhor nos serviços de classe e mantém evolução de mapa da estrada. Novas funcionalidades, componentes e as capacidades estão constantemente a ser introduzidas e evoluem.

Para uma empresa que está a iniciar a transição para a nuvem de Olá, são altamente Recomendamos tootake uma abordagem gradual através da implementação do mapa da estrada uma nuvem migração. Acreditamos que para utilitários e as empresas no domínio de energia Olá, casos de utilização de Olá que são debatidos neste manual de comunicação social representam uma oportunidade para testes de implementação no soluções de Análise Preditiva na nuvem de Olá excelente.

#### <a name="business-case-justification-considerations"></a>Considerações de negócios justificação maiúsculas
Em muitos casos, o cliente Olá pode estar interessado em efetuar uma justificação de negócio para um caso de utilização especificado em que uma solução baseada na nuvem e o Machine Learning são componentes importantes. Ao contrário de uma solução no local, no caso de Olá de uma solução baseada na nuvem, Olá componente de custo de compromisso é o mínimo e máximo de elementos de custo de Olá está associados a utilização real. Quando se trata toodeploying uma previsão Cortana Intelligence Suite as soluções de energia, vários serviços podem ser integrados com uma estrutura de custo único comuns. Por exemplo, as bases de dados (*por exemplo,*, SQL Azure) podem ser utilizados toostore Olá não processados dados e, em seguida, para previsões Olá real do Azure ML é utilizado toohost Olá prever serviços. Neste exemplo, Olá custo estrutura pode incluir o armazenamento e componentes transacionais.

No Olá por outro lado, um deve ter uma boa compreensão de valor de negócio Olá de operativo de um pedido de energia (curto ou longo prazo) de previsão. Na verdade, é importante toorealize Olá negócio valor cada operação de previsão. Por exemplo, com precisão previsão próximas 24 horas a carga de energia para Olá pode impedir overproduction ou pode ajudar a evitar sobrecargas na grelha de Olá e isto pode ser quantified em termos de reduções financeiras numa base diária.

Uma fórmula básica para calcular o benefício de financeiros Olá de procura previsão solução seria: ![solução de previsão básica fórmula para calcular o benefício de financeiros Olá de procura](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Uma vez que o Cortana Intelligence Suite fornece um modelo de preços pay as you go, não é necessário para incorrer numa fórmula de toothis de componente de custo fixo. Esta fórmula pode ser calculada numa base diária, mensais ou anuais.

É possível encontrar atual Cortana Intelligence Suite e planos de preços do Azure ML [aqui](http://azure.microsoft.com/pricing/details/machine-learning/).

### <a name="solution-development-process"></a>Processo de desenvolvimento da solução
ciclo de desenvolvimento de Olá de um pedido de energia previsão solução, normalmente, envolve 4 fases, em todos os que se utilize baseado na nuvem tecnologias e serviços no Olá Cortana Intelligence Suite.

Esta situação é ilustrada no Olá diagrama a seguir:

![Ciclo de grelha inteligente](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

Olá parágrafo a seguir descreve este processo 4 passo:

1. **Recolha de dados** – avançadas qualquer solução de análise com base se baseia nos dados (consulte **compreensão de dados**). Especificamente, quando se trata de análise toopredictive e previsão, precisamos de fluxo em curso e dinâmico de dados. No caso de Olá de previsão a pedido de energia, estes dados podem ser obtidos diretamente a partir de medidores inteligentes ou já agregados numa base de dados no local. Podemos também dependem de outras origens de dados, tais como meteorologia e temperatura externas. Este fluxo contínuo de dados deve ser orquestrado, agendado e armazenado. [O Azure Data Factory](http://azure.microsoft.com/services/data-factory/) (ADF) é a nossa workhorse principal para realizar esta tarefa.
2. **Modelação** – previsões de energia exata e fiável, um tem desenvolver (formação) e manter um modelo excelente que faz com que a utilização de dados históricos Olá e extrai Olá significativo e padrões preditivos nos Olá dados. área Olá do Machine Learning (ML) tem sido crescer rapidamente com algoritmos mais avançados que está a ser desenvolvidos regularmente. Azure ML Studio fornece uma experiência de utilizador excelente que ajuda a utilizar Olá mais avançadas algoritmos de ML dentro de um fluxo de trabalho completa. Esse fluxo de trabalho é ilustrado no diagrama de fluxo de intuitivo e inclui a preparação de dados de Olá, extração de funcionalidade, modelação e avaliação de modelo. utilizador Olá pode solicitar em centenas de vários modelos que estão incluídos neste ambiente. Ao final Olá nesta fase, um scientist dados terão um modelo de trabalho que é completamente avaliado e pronto para a implementação.
   
   Olá seguinte diagrama é uma ilustração de um fluxo de trabalho normal:
   
   ![Modelação de fluxo de trabalho](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **Implementação** – com um modelo de trabalho em execução, Olá passo seguinte consiste em implementação. Aqui modelo Olá é convertido para um serviço web que expõe uma API RESTful que pode ser invocado em simultâneo através de Olá Internet a partir de vários clientes de consumo. Azure ML fornece uma forma simple de implementar um modelo diretamente a partir de Olá Azure ML Studio com um único clique do botão para um. processo de implementação de todo Olá acontece sob definições avançadas de Olá. Esta solução pode dimensionar o consumo de Olá necessário toomeet.
4. **Consumo** – nesta fase, iremos, na verdade, de tornar a utilização de Olá predições tooproduce do modelo de previsão. consumo de Olá pode conduzido a partir de uma aplicação de utilizador (*por exemplo,*, dashboard) ou diretamente a partir de um sistema operacional, tais como a pedido/forneça balanceamento de sistema ou uma solução de otimização de grelha. Podem ser orientadas por vários casos de utilização de um único modelo.

## <a name="data-understanding"></a>Dados de conhecimento
Após que abrangem considerações sobre o negócio Olá (consulte **compreensão de negócio**) de um pedido de energia previsão solução, mas é agora toodiscuss prontos Olá parte de dados. Qualquer solução de Análise Preditiva baseia-se em dados fiáveis. Para a previsão de pedido de energia, precisamos de dados de consumo histórico com vários níveis de granularidade. Os dados históricos são utilizados como Olá raw material. -Vai sofrer uma análise cuidada no qual Olá scientist dados identifiquem predictors (também referida tooas funcionalidades) que podem ser colocados num modelo que eventualmente irá gerar previsões Olá necessário.

No rest Olá desta secção, vamos descrever Olá vários passos e considerações para compreender os dados de Olá e como toobring-tooa de formulário utilizável.

### <a name="hello-model-development-cycle"></a>Olá ciclo de desenvolvimento do modelo
Produzir boa previsão modelos requer alguma preparação cuidada e planeamento. Interrompendo baixo Olá modelação processo em vários passos e concentrar-se num único passo num momento pode melhorar significativamente o resultado Olá processo completo de Olá.

Olá diagrama seguinte ilustra como o processo de modelação de Olá foi ser dividido em vários passos:

![Ciclo de desenvolvimento do modelo](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

Como podem ser vistos Olá ciclo de consiste seis passos:

* Formulação do problema
* Ingestão de dados e exploração de dados
* Preparação de dados e de engenharia da funcionalidade
* Modelação
* Modelo de avaliação
* Desenvolvimento

Resto Olá desta secção irão dita passos individuais Olá e tooconsider de itens em cada passo.

### <a name="problem-formulation"></a>Problema formulação
Iremos pode considerar formulação de problema Olá à medida que hello mais crítico passo um necessidades tooimplementing anterior tootake qualquer solução de Análise Preditiva. Aqui iremos seria transformar Olá problema empresarial e decompor-toospecific elementos que possam ser resolvidos através da utilização de dados e técnicas de modelação. É um problema de Olá tooformulate boa prática como um conjunto de questões Gostaríamos tooanswer. Eis algumas questões possíveis que podem ser aplicáveis dentro do âmbito de Olá de previsão a pedido de energia:

* O que é a carga de Olá era esperado um substation individuais no Olá seguinte hora ou dia?
* Em que altura do dia de Olá meu grelha verificará picos de procura?
* Qual é a probabilidade meu grelha toosustain Olá esperado pico de carga?
* Quanto energia deve gerar Olá energia estação durante a cada hora do dia de Olá?

Formulating estas perguntas nos permite toofocus na obtenção de dados à direita Olá e implementar uma solução que é completamente alinhada com o problema de negócio de Olá em questão. Além disso, vamos, em seguida, pode definir alguns as métricas-chave que nos permitem desempenho de Olá tooevaluate do modelo de Olá. Por exemplo, como exata deve Olá previsão possível e que é o intervalo de Olá de erro que ainda seja aceitável por empresas Olá?

### <a name="data-sources"></a>Origens de Dados
grelha de inteligente moderna Olá recolhe dados de várias partes e dos componentes de grelha Olá. Estes dados representam diferentes aspetos da operação de Olá e a utilização de Olá de grelha de energia Olá. Dentro do âmbito de Olá do pedido de energia Olá previsão, iremos são limitar o debate Olá nas origens de dados que refletem o consumo de pedido real Olá. Uma origem importante de consumo de energia são medidores inteligentes. Utilitários à volta de globo Olá são implementar rapidamente medidores inteligentes para os seus consumidores. Medidores inteligentes registam o consumo de energia real de Olá e reencaminham constantemente este utilitário de back toohello de dados da empresa. Dados são recolhidos e enviados, o intervalo fixo, entre a cada hora too1 5 minutos. Mais avançados medidores inteligentes podem ser programados remotamente toocontrol e equilíbrio Olá consumo real de dentro de um núcleo. Dados de medição inteligente é relativamente fiáveis e incluem um carimbo de data / hora. Isso permite uma ingredient importante para o pedido de previsão. Dados de medição podem ser agregados (summed) em vários níveis na topologia de grelha Olá: transformador, substation, região, *etc*. Iremos pode, em seguida, escolha toobuild de nível de agregação de Olá necessário um modelo de previsão para o mesmo. Por exemplo, se a empresa do utilitário de Olá seria como tooforecast futuras de carga em cada um dos respetivos substations de grelha, em seguida, dados todos os medidores podem ser agregados para cada substation individuais e utilizados como uma entrada para Olá modelo de previsão. Iremos Consulte toosmart medidores como uma origem de dados interno.

Uma previsão de pedido de energia fiável será também dependem de outras origens de dados externas. Um fator importante que afeta o consumo de energia é Meteorologia hello, ou mais precisamente temperatura de Olá. Os dados históricos mostram forte correlação entre a temperatura externa e consumo de energia. Durante dias summer frequente, certifique-consumidores utilizar do respetivos conditioners ondas eletromagnéticas e durante a ativação Inverno Olá heating sistemas. Uma origem fiável de históricos temperatures na localização de grelha Olá, por conseguinte, é chave. Além disso, também precisamos de previsão exata de temperatura como uma previsão da receita do consumo de energia.

Também podem ajudar na criação de modelos de previsão de pedido de energia a outras origens de dados externas. Estes podem incluir a longo prazo climático alterações, índices económico (*por exemplo,*, GDP) entre outros. Neste documento, não irá incluir estes outras origens de dados.

### <a name="data-structure"></a>Estrutura de dados
Depois de identificar Olá necessário origens de dados, vamos seria como tooensure que os dados não processados que tenham sido recolhidos incluem Olá corrigir as funcionalidades de dados. modelo de previsão toobuild uma procura fiável, seria precisamos tooensure Olá dados recolhidos incluem elementos de dados que podem ajudar a prever a pedido de futuras Olá. Seguem-se alguns requisitos básicos que dizem respeito à estrutura de dados de Olá (esquema) de dados não processados Olá.

dados não processados Olá é composta por linhas e colunas. Cada medida é representada como uma única linha de dados. Cada linha de dados inclui várias colunas (também referida tooas funcionalidades ou campos).

1. **Carimbo de hora** – campo de carimbo de Olá representa a hora real Olá quando medida Olá foi registada. -Deve estar em conformidade com um dos formatos de data/hora comuns Olá. Data e hora partes devem ser incluídas. Na maioria dos casos, não é necessário para Olá tempo toobe registadas até Olá segundo nível de granularidade. É importante toospecify Olá fuso horário em que os dados de Olá são registados.
2. **ID de medidor** -este campo identifica medição Olá ou dispositivo de medida Olá. É uma variável categórico e pode ser uma combinação de dígitos e carateres.
3. **Valor de consumo** – trata-se de consumo real de Olá num determinado momento data /. consumo de Olá pode ser medido em kWh (kilowatt-hour) ou qualquer outro preferencial unidades. É importante toonote Olá unidade de medida tem de permanecer consistente entre todas as medidas nos dados de Olá. Em alguns casos, pode ser fornecido consumo mais 3 fases de energia. Nesse caso, seria necessário toocollect todas as fases de consumo independentes Olá.
4. **Temperatura** – temperatura Olá normalmente é recolhida a partir de uma origem independente. No entanto, deve ser compatível com os dados de consumo de Olá. Deve incluir um timestamp, tal como descrito acima, que irão permiti-toobe sincronizada com os dados de consumo real de Olá. valor de temperatura de Olá pode ser especificada em graus Celsius ou Fahrenheit, mas deve permanecer consistente em todos os valores.
5. **Localização –** campo de localização de Olá está normalmente associado ao local de olá onde foram recolhidos dados de temperatura Olá. Pode ser representado como um número de código postal ou no formato (lat/longa) de latitude/longitude.

Olá tabelas a seguir mostra exemplos de um formato de dados de consumo e temperatura boa:

| **Data** | **Tempo** | **ID de medidor** | **Fase 1** | **Fase 2** | **Fase 3** |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Data** | **Tempo** | **Localização** | **Temperatura** |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24.4 |
| 7/1/2015 |10:00:01 |11242 |24.4 |
| 7/1/2015 |10:00:02 |11242 |24.5 |

Como podem ser vistos acima, este exemplo inclui 3 valores diferentes para consumo associado 3 fases de energia. Além disso, tenha em atenção que os campos de data e hora de Olá são separados, no entanto também podem ser combinados numa única coluna. Neste caso, a coluna de localização de Olá é representada num formato de código postal de 5 dígitos e temperatura Olá num formato grau Celsius.

### <a name="data-format"></a>Formato de dados
Cortana Intelligence Suite pode suportar Olá mais comuns os formatos de dados como CSV, TSV, JSON, *etc*. É importante que esse formato de dados de Olá permanece consistente Olá completo para ciclo de vida do projeto de Olá.

### <a name="data-ingestion"></a>Ingestion de Dados
Uma vez que a previsão de pedido de energia é prever a constantemente e frequentemente, iremos tem de garantir que os dados não processados Olá é fluir através de um processo de ingestão de dados sólida e fiável. processo de ingestão Olá tem de garantir que os dados não processados Olá estão disponíveis para Olá previsão processo momento Olá necessário. Que indica que a frequência de ingestão de dados de Olá deve ser maior Olá frequência de previsão.

Por exemplo: se a nossa pedido previsão solução irá gerar uma nova previsão às 8:00 numa base diária, em seguida, temos tooensure que todos os dados de Olá que tenham sido recolhidos durante a última Olá tem sido totalmente ingerida até esse ponto de 24 horas e tem tooeven incluem Olá última hora dos dados.

Na ordem tooaccomplish, Cortana Intelligence Suite oferece várias formas toosupport um processo de ingestão de dados fiável. Isto será mais abordado em Olá **implementação** secção deste documento.

### <a name="data-quality"></a>Qualidade de dados
origem de dados não processados de Olá que é necessária para efetuar a previsão de procura fiável e precisa tem de cumprir critérios de qualidade alguns dados básicos. Apesar de métodos de análises avançados podem ser utilizado toocompensate para algum problema de qualidade de dados possível, ainda temos tooensure que iremos são cruzamento entre alguns limiar de qualidade de base de dados quando a ingestão de dados de novo. Seguem-se algumas considerações que dizem respeito à qualidade de dados não processados:

* **Falta o valor** -Isto refere-se toohello situação quando medida específica não foi recolhida. requisito básico Olá aqui é que Olá em falta a taxa de valor não deve ser superior a 10% durante qualquer período de tempo especificado. No caso que um valor único está em falta-deve ser indicado através da utilização de um valor predefinido (por exemplo: '9999') e não '0', que pode ser uma medida válido.
* **Precisão medida** – valor real do Olá de consumo ou temperatura deve ser registada com precisão. Medidas incorretas produzirá previsões incorretas. Normalmente, erro de medida Olá deve ser inferior ao valor de true de toohello relativo de 1%.
* **Hora da medida** – é necessário que timestamp real de Olá dos dados de Olá recolhidos não será desvio por mais de 10 segundos toohello relativo verdadeiro hora medida real Olá.
* **Sincronização** – quando estão a ser utilizadas várias origens de dados (*por exemplo,*, consumo e temperatura), tem de garantir que não existem sem sincronização de hora problemas entre eles. Isto significa que tempo Olá diferença entre timestamp Olá recolhido quaisquer dois independente das origens de dados não deve exceder mais de 10 segundos.
* **Latência** - conforme mencionado acima, no **ingestão de dados**, estamos dependentes de um processo de fluxo e ingestão de dados fiável. toocontrol que tem garantimos que iremos controlar latência de dados de Olá. Isto é especificado como diferença de tempo de Olá entre tempo Olá que foi feita a medida real Olá e a hora de Olá em que foi carregada na Olá armazenamento Cortana Intelligence Suite e está pronto a utilizar. Para a carga de curto prazo, previsão latência total de Olá não deve ser superior a 30 minutos. Carga de longo prazo previsão latência total de Olá não deve ser maior que 1 dia.

### <a name="data-preparation-and-feature-engineering"></a>Preparação de dados e de engenharia da funcionalidade
Depois de dados não processados Olá foi ingeridos (consulte **ingestão de dados**) e foi em segurança armazenada, está pronto toobe processado. Olá fase de preparação de dados é basicamente a dados não processados Olá e converter (transformar, reformulação) para um formulário para Olá modelação fase. Que pode incluir operações simples como a coluna de dados não processados Olá conforme está com o respetivo valor de medida real, valores normalizados, operações mais complexas, tais como [tempo lagging](https://en.wikipedia.org/wiki/Lag_operator)e outros. Olá recém-criado colunas de dados são referidos tooas dados funcionalidades e o processo de Olá de gerar estes é engenharia da funcionalidade de tooas referenciado. Por fim Olá deste processo seria temos um novo conjunto de dados que tem sido derivado de dados não processados Olá e pode ser utilizado para a modelação. Além disso, a fase de preparação de dados de Olá deve tootake care of valores em falta (consulte **qualidade dos dados**) bem como compensá-los. Em alguns casos, iremos também terá de toonormalize Olá dados tooensure que todos os valores são representados no Olá a mesma escala.

Nesta secção, que iremos lista algumas das funcionalidades dados comuns Olá que estão incluídas no energia Olá a pedido previsão modelos.

**Tempo suscitada pelo departamento de funcionalidades:** estas funcionalidades são derivadas de dados de data/timestamp Olá. Estes são extraídos e convertidos categórico funcionalidades como:

* Hora do dia – esta é a hora de Olá do dia de Olá que aceita valores de 0 too23
* Dia da semana – Isto representa o dia de Olá da semana de Olá e aceita valores de 1 (Domingo) too7 (Sábado)
* Dia do mês – Isto representa a data real Olá e pode demorar valores entre 1 too31
* Mês do ano – Isto representa o mês Olá e aceita valores de 1 (Janeiro) too12 (Dezembro)
* Fim de semana – esta é uma funcionalidade do valor binário que aceita valores de Olá 0 em dias da semana ou 1 para o fim de semana
* Feriado - esta é uma funcionalidade do valor binário que aceita valores de Olá 0 para um dia regular ou 1 para um feriado
* Termos de Fourier – Olá Fourier termos são ponderações que são derivadas de Olá timestamp e são utilizados toocapture Olá sazonalidade (cycles) nos dados de Olá. Uma vez que vamos pode ter vários seasons nos nossos dados temos vários Fourier termos. Por exemplo, valores de pedido podem ter anuais, semanais e diários seasons/ciclos que resultará em termos de Fourier 3.

**Funcionalidades de medida independente:** funcionalidades independentes Olá incluem todos os elementos de dados de Olá que Gostaríamos toouse como predictors no nosso modelo. Aqui iremos excluir funcionalidade dependentes de Olá que seria precisamos toopredict.

* Funcionalidade de desfasamento – estes são tempo desviado valores de procura real Olá. Por exemplo, as funcionalidades de desfasamento 1 armazena valor de pedido de Olá Olá toohello relativo de hora anterior (partindo do princípio de dados por hora) timestamp atual. Da mesma forma, vamos adicionar desfasamento 2, lag 3, *etc*. combinação real de Olá desfasamento de funcionalidades de que são utilizados são determinadas durante a fase de modelação de Olá durante a avaliação de resultados de modelo Olá.
* De longo prazo tendências – esta funcionalidade representa crescimento linear do Olá no pedido entre anos.

**Funcionalidade dependente:** funcionalidade dependentes Olá é a coluna de dados de Olá que Gostaríamos toopredict nosso modelo. Com [supervisionado aprendizagem](https://en.wikipedia.org/wiki/Supervised_learning), é necessário para primeiro preparar o modelo de Olá utilizar funcionalidades dependentes Olá (que também é referido tooas etiquetas). Isto permite padrões de Olá Olá modelo toolearn nos dados de Olá associados com funcionalidade dependentes Olá. Em termos de energia previsão queremos normalmente a pedido real do toopredict Olá e, por isso, vamos utilizá-lo como funcionalidade dependentes Olá.

**Processamento de valores em falta:** durante a fase de preparação de dados de Olá, seria precisamos toodetermine Olá melhor estratégia toohandle valores em falta. Isto é principalmente utilizando Olá várias análises [os métodos de imputation dados](https://en.wikipedia.org/wiki/Imputation_\(statistics\)). No caso de Olá de procura de energia previsão, iremos normalmente impute valores em falta utilizando média móvel anterior disponíveis dos pontos de dados.

**Dados de normalização:** normalização de dados é outro tipo de transformação que é utilizado toobring previsão de todos os dados numéricos, tais como a pedido para um dimensionamento semelhante. Isto normalmente ajuda a melhorar a precisão do modelo Olá e a precisão. É, normalmente, isto seria feito, dividindo valor real Olá por intervalo Olá dos dados de Olá.
Isto irá reduzir o valor original Olá verticalmente para um intervalo mais pequeno, normalmente, entre -1 e 1.

## <a name="modeling"></a>Modelação
Olá modelação fase é onde ocorre conversão de Olá dos dados de Olá para um modelo. No Olá core deste processo existe avançado algoritmos de procurar dados históricos de Olá (dados de formação), extrair padrões e criar um modelo. Esse modelo pode ser mais tarde toopredict utilizado em novos dados não foi o modelo de Olá toobuild utilizados.

Assim que tivermos um trabalho fiável o modelo que pode, em seguida, utilizá-la tooscore novos dados estruturados tooinclude Olá necessário funcionalidades (X). Olá, processo de classificação faz com que a utilização de Olá persistente modelo (objeto de fase de preparação de Olá) e prever a variável de destino Olá, que é a designação Ŷ.

### <a name="demand-forecasting-modeling-techniques"></a>Previsão técnicas de modelação de pedido
No caso de Olá de procura, iremos tornar de previsão a utilização de dados históricos, que estão ordenados por hora. É, geralmente, consulte toodata que inclui a dimensão de hora Olá como [série de tempo](https://en.wikipedia.org/wiki/Time_series). objetivo Olá no tempo modelação de série está na altura de toofind relacionadas com tendências, sazonalidade, auto-correlação (correlação ao longo do tempo) e formular os para um modelo.

Nos últimos anos algoritmos avançados foram previsão de série de tempo de tooaccommodate desenvolvida e tooimprove precisão de previsão. Resumidamente, vamos discutir alguns deles aqui.

> [!NOTE]
> Esta secção não se pretendido toobe utilizada como uma máquina de aprendizagem e a descrição geral de previsão, mas em vez disso, como um curto inquérito de modelação técnicas que são frequentemente utilizadas para a pedido de previsão. Para obter mais informações e material educational sobre previsão de série de tempo, recomendamos vivamente o livro online Olá [previsão: princípios e prática](https://www.otexts.org/book/fpp).
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA (média móvel)**](https://www.otexts.org/fpp/6/2)
Média móvel é um dos Olá primeiro analíticos técnicas que foi utilizado para a previsão de série de tempo e ainda é uma das técnicas Olá normalmente utilizada a partir de hoje. Também é foundation Olá para mais avançadas técnicas de previsão. Com média iremos são previsão ponto de dados seguinte Olá por uma média através de pontos mais recentes Olá K, onde K indica que a ordem de Olá de Olá média.

técnica de média móvel Olá tem efeito Olá de suavização Olá previsão e, por conseguinte, não poderá processar volatility bem grande nos dados de Olá.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**ETS (Suavização exponencial)**](https://www.otexts.org/fpp/7/5)
Suavização exponencial (ETS) é uma família de vários métodos que utilizam uma média ponderada recentes de pontos de dados no ponto de dados ordem toopredict Olá seguinte. ideia Olá é ponderações superiores tooassign toomore valores e diminuir gradualmente este importância para os valores de medida mais antigos. Existem vários métodos diferentes com esta família, algumas delas incluem processamento de sazonalidade nos dados de Olá como [método sazonais Holt Winters](https://www.otexts.org/fpp/7/5).

Alguns destes métodos também pesar sazonalidade Olá dos dados de Olá.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA (automática regressão integrado mover média)**](https://www.otexts.org/fpp/8)
Auto regressão integrada mover médio (ARIMA) é outra família dos métodos que é normalmente utilizada para a previsão de série de tempo. Praticamente combina os métodos de regressão automática com média. Métodos de regressão automática utilizam modelos de regressão, efetuando os valores de séries de tempo anterior na ordem toocompute Olá próximo data ponto. Métodos ARIMA também se aplicam os métodos de diferenciação que incluem a calcular a diferença de Olá entre pontos de dados e a utilização dos mesmos em vez do valor de medida original Olá. Por fim, ARIMA também utilizam Olá mover médias técnicas que são analisadas acima. combinação de Olá de todos estes métodos de várias formas é que construções Olá família dos métodos ARIMA.

ETS e ARIMA são amplamente utilizado hoje para previsão de pedido de energia e muitos outros problemas de previsão. Em muitos casos estes são combinados resultados muito exata toodeliver.

**Regressão múltipla geral** modelos de regressão pode ser mais importante modelação abordagem Olá dentro do domínio Olá do machine learning e estatísticas. No contexto de Olá de série de tempo, podemos utilizar valores de futuras regressão toopredict Olá (*por exemplo,*, de procura). Regressão iremos tirar uma combinação de linear de predictors Olá e saber o peso de Olá (também referida tooas coefficients) desses predictors durante o processo de preparação de Olá. o objetivo de Olá é tooproduce uma linha de regressão será previsão nosso valor previsto. Os métodos de regressão são adequados quando variável de destino Olá é numérico e, por conseguinte, também se adequa a previsão de série de tempo. Há uma grande variedade de métodos de regressão, incluindo modelos de regressão muito simples, como [regressão Linear](https://en.wikipedia.org/wiki/Linear_regression) e mais avançadas aqueles como árvores de decisões, [aleatório florestas](https://en.wikipedia.org/wiki/Random_forest), [Neural Redes](https://en.wikipedia.org/wiki/Artificial_neural_network)e elevada árvores de decisões.

Construir a pedido de energia previsão como um problema de regressão proporciona muita flexibilidade na seleção de funcionalidades nossos dados que podem ser combinadas de dados de série de tempo de pedido real Olá e fatores externos, como temperatura. Obter mais informações sobre as funcionalidades de Olá selecionado são abordados na Olá engenharia da funcionalidade (consulte **preparação de dados e de engenharia da funcionalidade**) secção este manual de comunicação social.

Da nossa experiência com a implementação e a implementação do piloto de previsões de pedido de energia, ter Descobrimos que hello modelos de regressão avançadas que estão disponíveis no Azure ML tendem tooproduce Olá obter os melhores resultados e iremos tornar utilizar deles.

## <a name="model-evaluation"></a>Modelo de avaliação
Avaliação do modelo tem um papel fundamental na Olá **ciclo de desenvolvimento de modelo**. Neste passo, vamos ver para validar o modelo de Olá e o desempenho com dados de vida real. Durante o passo de modelação de Olá utilizamos uma parte de dados disponíveis Olá de Olá modelo de preparação. Durante a fase de avaliação de Olá iremos tirar resto Olá modelo de Olá Olá dados tootest. Praticamente significa que podemos são feeding Olá novos dados do modelo que tenham sido restructured e contém Olá mesmo funcionalidades como o conjunto de dados do Olá formação. No entanto, durante o processo de validação de Olá, vamos utilizar a variável de destino do Olá modelo toopredict Olá em vez de fornecer a variável de destino disponíveis Olá. É, muitas vezes, consulte toothis processo como modelo de classificação. Vamos, em seguida, utilizará valores de destino verdadeiro Olá e compará-los com Olá prever aqueles. objetivo Olá aqui é toomeasure e minimizar o erro de previsão Olá, que significa que a diferença de Olá entre predições Olá e valor de true Olá. Quantifying medida de erro Olá é a chave, uma vez que vamos seria como modelo de Olá toofine otimizar e validar se o erro de Olá, na verdade, está a diminuir. Modelo de Olá fine-Tuning pode ser feito ao modificar os parâmetros de modelo que controlam Olá learning processo ou adicionando ou removendo as funcionalidades de dados (referido tooas [parâmetros paramétrico](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). Praticamente que significa que podemos poderá precisar tooiterate entre engenharia de funcionalidade Olá, modelação de e modelo várias vezes as fases de avaliação até que estamos a nível de toohello necessário tooreduce capaz de Olá erro.

É importante tooemphasis que o erro de previsão Olá nunca serão zero como existe nunca é um modelo que perfeitamente possível prever a cada resultado. No entanto, há um determinado magnitude erro que é aceitável por empresas Olá. Durante o processo de validação de Olá, gostaríamos tooensure que nosso erro de previsão do modelo no Olá nível ou melhor tolerância de negócio Olá nível. Consequentemente, é importante de ciclo de nível de Olá tooset de erro de tolerable Olá no início Olá Olá durante Olá **problema formulação** fase.

### <a name="typical-evaluation-techniques"></a>Técnicas de avaliação típica
Existem várias formas em que a predição de erro pode ser medido e quantified. Nesta secção incidirá debate Olá na série de tootime relevantes de técnicas de avaliação e no específicas para a pedido de energia previsão.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE representa significa erro percentagem absoluto. Com MAPE iremos são informática diferença Olá entre cada ponto previsto e o valor real Olá esse ponto. Vamos, em seguida, quantificar os erros de Olá por ponto calculando proporção Olá do valor real do Olá diferença toohello relativo. No último passo, vamos médio estes valores. fórmula matemática Olá utilizada para MAPE é seguinte Olá:

![A fórmula MAPE](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*onde A<sub>t</sub> é o valor real do Olá, F<sub>t</sub> é Olá valor previsto e n é Olá previsão horizon.*

## <a name="deployment"></a>Implementação
Assim que podemos ter nailed baixo Olá modelação fase e validar o desempenho do modelo de Olá estamos toogo pronto para a fase de implementação de Olá. Neste contexto, implementação significa ativar cliente Olá modelo de Olá tooconsume executando predições reais no mesmo escala maior. conceito de Olá de implementação é a chave no Azure ML, uma vez que o nosso objetivo principal é tooconstantly invocar predições como toojust oposição ao obter conhecimentos aprofundados de Olá dos dados de Olá. fase de implementação de Olá faz parte de olá onde iremos ativar Olá modelo toobe consumido em grande escala.

Dentro do contexto de Olá de procura de energia previsão, o nosso objetivo é tooinvoke contínua e periódica previsões garantindo que novos dados estão disponíveis para o modelo de Olá e esse Olá previstos são enviados dados cliente consumo toohello back.

### <a name="web-services-deployment"></a>Implementação de serviços Web
bloco modular implementável principal por Olá no Azure ML é serviço de web de Olá. Este é Olá mais eficaz forma tooenable consumo de um modelo preditivo na nuvem de Olá. serviço Web de Olá encapsula modelo Olá e encapsula na wrapper cópias de segurança com um [RESTful](http://www.restapitutorial.com/) API (Application Programming Interface). Olá API pode ser utilizado como parte de qualquer código de cliente conforme ilustrado no diagrama de Olá abaixo.

![Estamos a implementação de serviço e o consumo de](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

Como podem ser vistos, o serviço web de Olá está implementado na nuvem do Cortana Intelligence Suite de Olá e pode ser invocado ao longo do respetivo exposta ponto final da REST API. Um tipo diferente de clientes em vários domínios pode invocar o serviço de Olá através de Olá Web API em simultâneo. Também pode dimensionar o serviço web de Olá para suportar a milhares de chamadas em simultâneo.

### <a name="a-typical-solution-architecture"></a>Uma arquitetura de solução típica
Quando implementar um pedido de energia previsão solução, estamos interessados em implementar uma solução de tooend ponto que vai mais além do serviço de web de predição de Olá e facilita o fluxo de dados completo de Olá. No momento de Olá que iremos invocar uma previsão novo seria precisamos toomake se que esse modelo Olá sejam fornecido com as funcionalidades de dados atualizados. Implica que esse Olá recentemente recolhidos dados não processados constantemente ingeridos, processados e transformados a funcionalidade necessária Olá definido no modelo que Olá foi criado. AT Olá mesmo tempo, iremos pretende toomake Olá previstos dados disponíveis para Olá terminar o consumo de clientes. Um exemplo dados de ciclo de fluxo (ou o pipeline de dados) é ilustrado no diagrama de Olá abaixo:

![Pedido de energia previsão tooEnd de fim do fluxo de dados](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

Estes são os passos de Olá que ocorrer como parte do ciclo de previsão Olá de energia a pedido:

1. Milhões de medidores de dados implementado constantemente geraram os dados de consumo de energia em tempo real.
2. Estes dados está a ser recolhidos e carregada para um repositório de nuvem (*por exemplo,*, Blob do Azure).
3. Antes de ser processado, dados não processados Olá são tooa agregados substation ou nível regional como definido por empresas Olá.
4. processamento de funcionalidade Olá (consulte **preparação de dados e a funcionalidade de processamento**), em seguida, é efetuada e o modelo de dados de Olá de produz que é necessários para de preparação ou de classificação – Olá funcionalidade conjunto de dados são armazenados numa base de dados (*por exemplo,*, SQL Azure).
5. Olá novamente formação serviço é invocado Olá toore formação previsão modelo – que atualizar a versão do modelo de Olá é persistente para que possa ser utilizado por Olá da classificação de serviço web.
6. Olá da classificação de serviço web é invocada com base numa agenda que se adequa a frequência de previsão Olá necessário.
7. Olá previstos os dados são armazenados numa base de dados que pode ser acedido pelo cliente de consumo Olá final.
8. o cliente de consumo de Olá obtém previsões Olá, aplica-se-lo novamente numa grelha Olá e consome-lo em conformidade com o caso de utilização de Olá necessário.

É importante toonote que este ciclo completo é totalmente automatizado e é executada com base numa agenda. orquestração de todo Olá deste ciclo de dados pode ser feita utilizando ferramentas como [do Azure Data Factory](http://azure.microsoft.com/services/data-factory/).

### <a name="end-tooend-deployment-architecture"></a>Terminar tooEnd arquitetura de implementação
Na ordem toopractically implementar uma solução de previsão de pedido de energia no Cortana Intelligence, precisamos tooensure que componentes de Olá necessário são estabelecidos e corretamente configurados.

Olá diagrama seguinte ilustra uma arquitetura de Intelligence Cortana com base típica que implementa e orquestra Olá ciclo de fluxo de dados que está descrito acima:

![Terminar tooEnd arquitetura de implementação](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Para obter mais informações sobre cada um dos componentes de Olá e arquitetura todo Olá Consulte toohello modelo de solução de energia.

