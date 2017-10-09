---
title: "aaaAzure Mobile Engagement guia de introdução com melhores práticas"
description: "Guia de Introdução para o Azure Mobile Engagement e Melhores práticas para a integração"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement – Guia de Introdução com Melhores Práticas
## <a name="overview"></a>Descrição geral
**ecrã móveis Olá é um espaço muito movimentado:** 2013, um estudo localizar no dispositivo móvel médio de Olá tinha 27 aplicações instaladas. Em geral, os utilizadores gastaram 30 horas por mês nas suas aplicações. A maior parte deste período de tempo foi despendida nas redes sociais e em jogos (cerca de 20 horas). Em 2014, Olá mercado Android tinha cerca de 1,5 milhões de aplicações para utilizadores toochoose do. Olá Apple store continha aproximadamente 1,2 milhões de aplicações. A utilização de aplicações móveis continua a aumentar, à medida que os programadores competem neste mercado em crescimento. 

utilizador do Olá médio móveis irá instalar e desinstalar aplicações frequentemente, consoante as mudanças de interesses e nas experiências na aplicação. Ordem toodetermine Olá foi efetuada com êxito uma aplicação, torna-se vital tooknow mais do que apenas quantos utilizadores instalarem a aplicação. É importante tooknow quão útil é a sua aplicação e se está a ser alterar tendência de utilização. Olá seguintes perguntas tornam-se importantes:

* São os seus utilizadores a partir toofind sua aplicação desinteressante ou obsoleta? 
* Quantos utilizadores deixaram de utilizar a aplicação totalmente? 
* A tendência das compras na aplicação está em ascendência ou em decadência?
* Os utilizadores falham toocomplete fluxos de trabalho devido a problemas com a aplicação Olá ou à falta de interesse? 
* Pode manter a sua aplicação útil e relevante ao enviar tooyour conteúdo novo utilizador base? 
* Este conteúdo novo seria Olá mesmo para todos os utilizadores ou direcionada para os segmentos de utilizadores com base no comportamento na sua aplicação? 

Respostas tooquestions semelhante toothese pode ajudar a aumentar a vida Olá e as receitas provenientes da sua aplicação. Também podem ajudar a definir e a reter a sua base de utilizadores. 

Suporte de dados relacionados com aplicações tendem toohave algumas de retenção mais elevada de Olá entre os utilizadores. Um motivo para isto é que proporcionam constantemente toousers conteúdo raiz. A adoção precoce de notificações push úteis direcionadas tooa segmento de utilizadores tende toohave um impacto elevado na retenção da aplicação. 

programa do Azure Mobile Engagement Olá é concebida toohelp expandir a vida Olá e a retenção da sua aplicação, fornecendo um método toogather e analisar informações detalhadas sobre a utilização de Olá da sua aplicação. Irá ajudá-lo a classificar toobehavior de acordo com a base de utilizadores e criar campanhas direcionadas na entrega de notificações push e mensagens na aplicação tooidentified segmentos de utilizadores. Os indicadores chave de desempenho (KPI) medem quão ativos são os seus utilizadores com os diferentes aspetos da sua aplicação. O Azure Mobile Engagement fornece os métodos de Olá terá toodetermine estes KPIs. Ajuda a aumentar Olá retorno do investimento (ROI) ao fornecer a infraestrutura de Olá é necessário o tooincrease engagement com a sua aplicação móvel. 

Olá tooget de ordem mais fora do Azure Mobile Engagement, terá de toostart com um plano de envolvimento bem estruturado. O plano irá ajudá-lo a identificar os dados de granulares Olá, terá de toosegment capaz de toobe ao utilizador base. Isto pode ser baseado no comportamento e nas experiências na aplicação. Por ordem para a sua toobe plano com êxito, é uma melhor tooclearly de prática definir Olá KPI que irá medir os objetivos de Olá da sua aplicação. Com indicadores de desempenho claramente definidos, pode incorporar facilmente lógica necessária às Olá sua toocollect bem detalhada dados da aplicação que irá utilizar tooanalyze e avaliar os KPIs. Este tópico é um guia de melhores práticas para definir Olá KPIs que irá utilizar com o seu plano de envolvimento. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>Passo 1: Definir o seu modelo BET do KPIs toofit Olá
Definir corretamente KPIs pode ser toocomplete uma tarefa difícil. As aplicações concebidas para as diferentes indústrias têm as suas próprias informações específicas e objetivos. Isto poderá confundir sua abordagem tooconfuse. toohelp evitar esta situação, objetivos e KPIs devem ser classificados em três categorias principais: **negócio**, **Engagement**, e **técnica**. Este é o que apelidamos Olá **modelo BET**.

Um bom plano geralmente terá objetivos com Olá KPIs que medem os sucessos Olá em cada uma das seguintes categorias do modelo BET de Olá de Olá.

#### <a name="business-kpis"></a>KPIs de Empresas
KPIs de empresas devem ser Olá toobuild de parte mais fácil. Provavelmente já os definiu de alguma forma quando planeou a sua aplicação móvel. Geralmente, estes KPIs ajudam a medir as receitas e o ROI da sua aplicação. Olá lista seguinte fornece alguns exemplos de KPIs de empresas que pode ajudar a orientá-lo ao definir os indicadores de desempenho:

* KPIs de Empresas de Comunicação Social
  * Número de Anúncios clicados
  * Número de visitas de página por utilizador
  * Número de subscrições atuais
* KPIs de Empresas de Jogos
  * Número de compras na aplicação
  * Receita média por utilizador (ARPU)
  * Tempo despendido por sessão
  * Dias jogados e nível atual no jogo
* KPIs de Empresas de Comércio Eletrónico
  * Dias de utilização da aplicação
  * Receita média por utilizador (ARPU)
  * Montante médio no carrinho durante a finalização da compra
  * Categoria de produto para a maioria das vistas e compras
* KPIs de Empresas da Banca e de Seguros
  * Número de contas
  * Funcionalidades ativadas
  * Páginas de oferta visitadas
  * Alertas clicados ou ativados       

#### <a name="engagement-kpis"></a>KPIs de Envolvimento
Um KPI de envolvimento é um envolvimento do desempenho indicador toomeasure Olá dos utilizadores. As tendências nesta área ajudam a determinar a retenção de Olá da sua aplicação. Seguem-se alguns indicadores de desempenho de exemplo para este tipo de KPI:

* Utilizadores ativos nos Olá últimos 7 dias
* Contagem de utilizadores Inativos para Olá últimos 7 dias
* Contagem de utilizadores que não tenham utilizado a aplicação Olá dentro de 30 dias  

Alguns fatores externos óbvios podem influenciar os indicadores nesta área. Por exemplo, pode considerar um toobe de dispositivos móveis com um utilizador de todas as vezes. Isto pode ou não ser verdade. Uma aplicação de jogos poderá tendem toohave uma utilização superior de férias, quando um jogador pode jogar mais ao trabalho ou na escola.   

Bem definidos KPIs nesta categoria devem ajudá-lo a medir a relação de Olá entre a sua aplicação e os seus clientes.

#### <a name="technical-kpis"></a>KPIs Técnicos
Os indicadores de desempenho nesta categoria ajudam a determinar se a sua aplicação está a ter um comportamento correto, se está a bloquear ou a falhar. Estes indicadores podem medir o estado de funcionamento de Olá da sua aplicação e determinar os problemas de usabilidade que poderão impedir que os utilizadores com aplicação Olá. As informações recolhidas para esta categoria também podem conter informações de desempenho que seriam relevantes toomarketing equipas. dados de Olá também podem ser úteis para resolução de problemas por IT e toohelp de equipas de suporte identificar erros não relatados. 

Seguem-se alguns exemplos de KPIs Técnicos:

* Informações e contagens de exceções não processadas ou processadas 
* Carimbo de data/hora da última falha
* Último botão clicado ou última página visitada
* Utilização da memória da aplicação Olá
* Velocidade de fotogramas da aplicação
* Versão do SO que Olá aplicação está em execução no
* Versão da aplicação

Definir o desempenho da aplicação estes KPIs toohelp medidas e identificar potenciais erros. Estes indicadores devem ajudar a reduzir o tempo de Olá que terá toodeliver uma correção para os seus clientes. Também o podem ajudar a definir um segmento de utilizadores que tenha encontrado um determinado problema. Pode utilizar o que utilizador segmentação toocreate campanhas toodeliver as notificações relativas a correções disponíveis e potenciais promoções toohelp recuperar a satisfação do cliente. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Exercício 1 do Manual: Criar o dashboard de KPI
Quando definir a sua estratégia de marketing, os KPIs devem apresentar uma perspetiva para cada um dos seus objetivos principais. Devem ser pontos de dados claramente definidos que permitirá toocollect informações essenciais toomonitor o comportamento da aplicação e Olá do utilizador final de Olá.

Criar um dashboard KPI que contém Olá informações indicadas abaixo

1. Quais são Olá KPIs para a aplicação Olá?
2. Que pontos de dados posso utilizar toorepresent cada KPI?
3. Onde estão localizados estes dados para a minha aplicação (ou seja, ecrã, definições, sistema...)?
4. Posso reproduzir uma sequência de Envolvimento para este KPI?

Pode utilizar Olá **criador de KPI** folha de cálculo no nosso [modelo do manual de comunicação social de suporte de dados] [ Media Playbook link] para obter exemplos e orientação.

## <a name="step-2-your-engagement-program"></a>Passo 2: o Seu Programa de Envolvimento
Um programa Mobile Engagement excelente deve ser considerado um componente essencial da sua aplicação. Isto deve sem dúvida incluir um programa de boas-vindas excelente que seja executado para um utilizador durante Olá primeiros dias de utilização da aplicação. Isto tende toohave um efeito muito positivo no engagement e a retenção da sua aplicação. Existem estudos que demonstraram que maioria Olá de paragem de utilizadores utilizando um Olá aplicação primeiros dias após a instalação. Pretende toostrive toomeet ou exceder cliente expectativa despertar o interesse numa fase inicial enquanto utilizador Olá ainda está concentrado na sua aplicação. Certifique-se de que está presente valor da chave Olá e os benefícios da sua aplicação tooyour clientes. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

As notificações push são Olá melhor abordagem tooearly ações de envolvimento com utilizadores de dispositivos móveis. No entanto, deve ter muito cuidado quando segmentar os utilizadores para notificações push. Isto acontece porque se um utilizador sentir que está a receber spam ou notificações desinteressantes, pode ter um efeito grave. Com poucos cliques, um utilizador pode eliminar a sua aplicação nunca tooreturn. Olá utilizador deve receber altamente personalizada na aplicação valor em vez de spam genérico.

Assim que os utilizadores estejam ativamente envolvidos, em seguida, o programa de envolvimento pode ajudar a potenciar outros aspetos da aplicação Olá.

Por exemplo, pode configurar uma campanha que solicita a sua toorate de utilizadores ativos a aplicação. Uma vez que este segmento de utilizadores Olá mais ativo e tem Olá mais experiência com a aplicação, é expectável que toogive hello mais atribuam a classificação. Depois de ter uma classificação da aplicação elevado, pode ajudar a unidade de transferência de orgânico Olá da sua aplicação, bem como reduzir os custos de aquisição de cliente novo.

#### <a name="engagement-sequence"></a>Sequência de Envolvimento
Um Programa de Envolvimento global inclui diversas sequências de envolvimento. Cada sequência visa tooreach vários objetivos.

###### <a name="life-push-sequence"></a>Sequência de push de vida
os objetivos de Olá para uma sequência de push de vida são diferentes consoante Olá ciclo de vida do envolvimento do utilizador de Olá com aplicação Olá. Um utilizador específico pode ser novo, inativo ou muito ativo. Em diferentes fases do ciclo de vida do envolvimento, os utilizadores podem tirar partido do seu conteúdo novo sob a forma de Olá de toodocumentation sugestões ou ligações. 

Por exemplo um novo utilizador poderá precisar de ajudar a obter tooan orientado por aplicação ou beneficiar de um novo utilizador incentivo semelhante toohello seguir Olá pela primeira vez que iniciar a aplicação Olá...

*"Estamos satisfeitos por estar toohave que carregar! Lembre-se toologin tooget a 1. º mês gratuito! "*

###### <a name="behavioral-push-sequence"></a>Sequência push comportamental
sequência push comportamental de Olá visa utilização tooincrease com base no comportamento do utilizador recolhido para a aplicação Olá.  

Por exemplo, um utilizador muito ativo de uma aplicação de futebol gestão poderá beneficiar americano com Olá seguinte notificação push...

*“Jorge, é um verdadeiro adepto de futebol americano! Iniciar sessão na secção do tooour da NFL e tenha acesso gratuito toohello SuperBowl!"*

###### <a name="alerting-push-sequence"></a>Sequência de push de alerta
Os utilizadores vão gostar de notícias relevantes focadas nos seus interesses. Uma sequência push de alerta melhora o envolvimento ao enviar alertas com base nos interesses que um utilizador demonstrou claramente. Isto pode ser explícito quando um utilizador seleciona os seus próprios interesses na aplicação Olá. Foi também possível determinar implicitamente com base nos dados recolhidos durante a interação do utilizador com a aplicação Olá.

Por exemplo, utilizador de Olá de uma aplicação de comércio eletrónico pode comprar regularmente uma marca específica de café que captou com um KPI de empresas. Olá alerta seguinte pode melhorar envolvimento deste utilizador com a aplicação Olá.

*"Olá Vitor, uma das suas marcas favoritas de café estará no venda 25% Olá primeira semana de Setembro de 2015. Valorizamo-lo como um cliente e Queríamos toomake se de que tinha conhecimento."*

###### <a name="rentention-push-sequence"></a>Sequência push de retenção
Esta sequência objetivos tooretain aos utilizadores que utilizam um toohelp de campanhas de notificações push repetitivas unidade um hábito regular de envolvimento com a aplicação Olá. Isto pode ajudar a aumentar a retenção da aplicação, se o utilizador de Olá gostar interações Olá. 

Por exemplo, o utilizador Olá de uma aplicação relacionada desporto pode receber Olá seguinte notificação push semanal com base nas Olá equipas favoritas:

*"Para uma oportunidade toowin 200 pontos, Vote se Olá Nova Iorque Yankees será win vencem o jogo desta semana contra os Toronto Blue Jays!"*

#### <a name="hello-3w-approach"></a>abordagem dos 3q de Olá
Envolver-se Olá diferentes sequências de push irá ajudá-lo com os utilizadores finais. No entanto, ainda tem abordagem do toouse Olá dos 3q para personalizar as notificações. Olá abordagem dos 3q deve abordar quem, quê e quando em cada notificação. Se satisfizer claramente estas três perguntas, as suas notificações devem estar adequadamente direcionadas para o envolvimento.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>Quem: Olá segmento de utilizadores que irão receber mensagens
Enviar aos utilizadores de tooyour notificações deve ser considerado um canal de comunicação muito sensível. Certifique-se as notificações de Olá que procure o segmento de utilizadores de tooa toosend toohello bem âmbito interesses desse segmento de utilizadores. Uma notificação incorretamente encaminhada é muito provável toohave um efeito negativo num utilizador. O utilizador pode considerá-la spam esquerda aplicação tooyour a ser desinstalada. 

Utilize uma combinação de critérios específicos técnicos e comportamentais quando definir os segmentos de utilizadores que irão receber notificações. Um exemplo simples que define um segmento de utilizadores pode ser semelhante toohello a seguinte instrução:

"Todos os utilizadores que executaram Olá uma aplicação móvel para Olá pela primeira vez há 3 dias e visitaram a página de início de sessão de Olá duas vezes sem de facto concluir um início de sessão".

Essa instrução ajuda a identificar os dados de Olá terá toocollect toosupport um cenário específico.

###### <a name="what-hello-message-that-you-will-send"></a>O que: mensagem de saudação que vai enviar
**Tom**

Nas ações de envolvimento utilize um tom que se adeque aos seus utilizadores segmentados. Esta é sem dúvida tooconnect uma boa forma aos seus utilizadores finais e promover o interesse de um utilizador na sua aplicação. 

**Redirecionamento**

Uma notificação push pode ser utilizada para mais do que abrir aplicação Olá. Se hello mensagem de notificação fornece um contexto, tal como notícias de difusão ou uma promoção de um produto, esta ligação avançada de Maio de notificação diretamente toohello com o botão direito conteúdo na aplicação Olá. toosupport, tem de criar um URL de aplicação do esquema toolet Olá gerir redirecionamento Olá. Quando estiver a trabalhar nas suas sequências de envolvimento, este é um passo importante que não pode ser esquecido.

O redirecionamento também pode ser gerido noutros sistemas. Por exemplo, com um URL de ação é possível tooredirect os utilizadores finais toomany outros sistemas, incluindo Olá seguinte:

* Um site
* Uma caixa de correio com e-mail já configurado
* Uma caixa de SMS
* Um serviço de marcação
* Diretamente toohello loja de aplicações para classificar a aplicação Olá. 

Isto proporciona muitas oportunidades os utilizadores finais de tooengage e criar regras automáticas os desempenhos de tooimprove.

**Formato/Conteúdo**

Diferentes tipos e formatos de Notificação push:

1. **Anúncios** : permite-lhe toousers de mensagens de publicidade toosend em diferentes momentos (fora da aplicação, na aplicação ou em qualquer altura).
2. **Inquérito** : ativado toogather informações dos utilizadores finais ao colocar-lhes perguntas. As respostas ficam então disponíveis quando criar critérios dos utilizadores finais de tootarget.
3. **Pushes de dados** : permite-lhe toosend um binários ou base64 ficheiro tooupdate Olá aplicação de dados. informações de Olá contidas num push de dados são enviadas tooyour aplicação toopersonalize Olá experiência dos utilizadores na sua aplicação. A aplicação tem de toobe concebido toosupport Olá dados num push de dados.
4. **Os mosaicos (apenas Windows Phone)** : ativada toouse Olá Push notificação serviço Microsoft (MPNS) toosend notificação Push nativo que contém dados de XML (suportados desde SDK versão 0.9.0. payload final do Olá para mosaicos não pode exceder os 32 kilobytes.). é apresentada a mensagem de saudação diretamente no mosaico do seu painel.
5. **Vista Web** : uma vista Web é um pop-up que contém conteúdo Web. Este pop-up aparece quando o utilizador final de Olá tiver clicado na notificação push de Olá. Uma vista web permite-lhe toohave mais interação com o utilizador final de Olá.

> [!NOTE]
> Certifique-se de que está a enviar como notificações push de conteúdo de Olá está em conformidade com a plataforma de respetivos Olá (iOS, Android, Windows) diretrizes para desenvolver aplicações e enviar notificações push.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>Quando: Olá temporização da sua campanha
Quando é Olá melhor tempo tooactivate uma campanha ao acionar notificações push? Deverá ser manual ou automática? Deverá ser recorrente? Ao determinar momento Olá ou frequência é essencial tooengage utilizadores com Olá obter os melhores resultados. Para cada cenário e sequência de envolvimento, tem de especificar quando será Olá melhor tempo toosend notificações push. Seguem-se alguns exemplos possíveis:

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

Se vai enviar muitas notificações diariamente, tem de ter em consideração que os utilizadores podem interpretar as suas comunicações como spam. 

O Azure Mobile Engagement fornece duas formas toohelp evitar as suas comunicações sejam interpretadas como spam. Em primeiro lugar, utilize tooensure de segmentação detalhada bem, fazê-lo Olá de destino não mesmos utilizadores. Além disso, o Azure Mobile Engagement oferece uma funcionalidade de “quota”. Esta funcionalidade pode limitar as notificações enviadas para uma campanha. Por exemplo, definir uma too5 de quota predefinida por semana irá garantir que um utilizador incluído como parte do segmento de utilizadores de campanha Olá recebe não mais de 5 notificações nessa semana.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Exercício 2 do Manual: criar o seu programa de envolvimento
Passe algum tempo a resumir os seus objetivos e definir as campanhas Olá esperar tooplay utilizar sequências específicas. Certifique-se de que aplica as notificações do Olá dos 3q abordagem toohello nas suas campanhas. 

Olá utilize **programa de envolvimento** folha de cálculo em Olá [modelo do manual de comunicação social de suporte de dados] [ Media Playbook link] para obter exemplos e orientação.

## <a name="step-3-app-integration"></a>Passo 3: integração de aplicações
#### <a name="create-a-tag-plan"></a>Criar um plano de etiquetas
toointegrate Azure Mobile Engagement na sua aplicação, terá de toocreate um plano de etiquetas. plano de etiquetas de Olá é fundamental para Olá projeto Olá. Define Olá relação entre as especificações de marketing, fluxo de trabalho de Olá da aplicação Olá, dados e de Olá etiquetas reais recolhidos na aplicação de Olá toomeasure KPIs. Indica que análises poderá toosee no portal de Olá. Também ajuda a definir segmentos de utilizadores e enviar tooengage de notificações push direcionadas para os utilizadores finais. Assim que tiver o plano de etiquetas de Olá definido, adicionar Olá código toointegrate na sua aplicação é simple utilizar Olá Azure Mobile Engagement SDK.

Um plano de etiquetas não deve etiquetar tudo numa aplicação. Deve incluir apenas dados de etiquetas que façam parte da sua estratégia Mobile Engagement. Provavelmente, isto será diferente consoante as aplicações. Olá [modelo do manual de comunicação social de suporte de dados] [ Media Playbook link] fornecida pelo Azure Mobile Engagement ajuda a cria um plano de etiquetas com um determinado método. Olá utilize **plano de etiquetas** planear a folha de cálculo como um guia toobuilding a etiqueta.

Ao definir uma secção de etiquetas na folha de cálculo de Olá, seja muito específico. Isto é muito importante tooavoid confusões. Detalhe cada cenário esperado no qual cada etiqueta será enviada. Inclua Olá nome da atividade de olá onde cada etiqueta é incorporada. Isto deverá todos ser incluído em Olá **informativo** fazem parte da folha de cálculo de Olá. folha de cálculo de plano de etiqueta de Olá deve ter Olá uma referência principal para a verificação de teste. 

No Olá **dados toocollect** secção, a equipa de programação deve encontrar os tipos de Olá, nomes, valores e pares chave/valor de informações adicionais necessárias para cada etiqueta que será incorporado na aplicação Olá.

É recomendável rever o plano de etiquetas de Olá com todas as equipas associadas ao projeto Olá. Efetue as correções necessárias e certifique-se de que tudo está preparado para as equipas de marketing e de programação.

Olá **declaração do trabalho** folha de cálculo pode ser guia toohelp utilizadas todas as pessoas envolvidas no projeto Olá.

#### <a name="data-types"></a>Tipos de Dados
Estes são tipos comuns de suporte de dados pelo Azure Mobile Engagement.

###### <a name="devices-and-users"></a>Dispositivos e utilizadores
O Azure Mobile Engagement identifica os utilizadores através da geração de um identificador exclusivo para cada dispositivo. Este identificador é designado identificador do dispositivo hello (ou deviceid). Este é gerado de tal forma que todas as aplicações em execução em que a partilha de dispositivo mesmo Olá o mesmo identificador de dispositivo.

###### <a name="sessions-and-activities"></a>Sessões e atividades
Uma sessão é uma instância da aplicação Olá que está a ser executada por um utilizador. Olá sessão abrange utilizador Olá inicia a aplicação Olá, até que este deixa de tempo de Olá.

Uma atividade é um agrupamento lógico de um conjunto de ações de aplicação Olá pode fazer durante uma sessão. É normalmente um ecrã específico na aplicação Olá, mas pode ser que qualquer coisa definida pela lógica Olá da aplicação Olá. No mínimo, deve etiquetar cada ecrã ou Atividade para a sua aplicação. Isto permitirá toounderstand Olá caminho do utilizador.

###### <a name="events"></a>Eventos
Os eventos são utilizados tooreport interação do utilizador com a aplicação Olá. Podem ser ações instantâneas, como a partilha de conteúdo ou a execução de um vídeo. Marcação de eventos irá fornecer-lhe coleções de dados que mostram como os utilizadores interagem com a aplicação Olá. 

###### <a name="jobs"></a>Tarefas
As tarefas são utilizadas tooreport ações que têm uma duração. Alguns exemplos incluem:

* Execução de chamadas de API
* Apresentar a hora dos anúncios
* Duração das tarefas em segundo plano 
* Duração do processo de compra
* Visualizar um vídeo

###### <a name="errors"></a>Erros
Erros são detetados pela aplicação Olá tooreport utilizados. Por exemplo, ações incorretas do utilizador ou falhas de chamadas de API.

###### <a name="application-information"></a>Informações da aplicação
Informações de aplicação (App-Info) são utilizadas tootag dados relacionados com a experiência do utilizador tooa com uma aplicação. Este é gerado pelo interação de um utilizador com a aplicação Olá. 

Para uma chave de app-info indicado, Azure Mobile Engagement apenas mantém um registo dos valor de Olá mais recente (nenhum histórico). Informações da aplicação revelam o estado de Olá da sua aplicação ou os utilizadores finais. Por exemplo Olá-início de sessão do Estado, ou grupo de produtos favorito de um utilizador.

###### <a name="crash-data"></a>Dados de falhas
Dados de falhas recolhidos automaticamente pelo SDK do Mobile Engagement de Olá falhas da aplicação de relatórios não processadas pela aplicação Olá. Por exemplo, uma exceção não processada que ocorra.

###### <a name="extra-data"></a>Dados adicionais
É possível melhorar com parâmetros eventos, erros, atividades e tarefas. Este é um programador pode fornecer como dados específicos da aplicação Olá de informações adicionais. Isto é importante para definir uma segmentação detalhada. 

Por exemplo, valor de Olá de uma etiqueta de "artigo" permitirá que os utilizadores finais toosegment com base em quem visualizou esse artigo específico. No entanto, isso pode não ser suficiente. Poderá ser melhor se essa mesma etiqueta de “artigo” também incluir informações adicionais, tais como “notícias_categoria” dentro de uma atividade. Isto seria útil toodetermine Olá dinamicamente as categorias favoritas do utilizador Olá. 

As informações adicionais são comunicadas como um par chave/valor. Exemplo de Olá para esta aplicação de suporte de dados, informações adicionais Olá para "notícias_categoria" seria valor Olá dessa categoria. Por exemplo, “desporto”, “economia” ou “política”.

#### <a name="tag-and-sdk-integration"></a>Integração de etiquetas e do SDK
Para instruções passo a passo para integrar hello Azure Mobile Engagement SDK na sua aplicação, siga Olá [integração do SDK do Engagement](mobile-engagement-windows-store-integrate-engagement.md) documentação no Web site Azure. Escolha a plataforma de destino de ligações de Olá na parte superior de Olá dessa página.

Recomendamos que crie projetos para duas aplicações assentes no Azure Mobile Engagement. Uma para desenvolvimento e testes e Olá para testes de produção. A equipa de TI pode então transitar dos teste tooproduction de teste, quando os testes de aceitação de utilizadores do Olá são efetuada com êxito.

#### <a name="user-acceptance-testing-uat"></a>Testes de aceitação de utilizadores (UAT)
Os testes de aceitação de utilizadores (UAT) servem para se certificar de que tudo está a funcionar devidamente. Os fluxos de trabalho podem ser concluídos e reunir todos os dados necessários com base no seu plano de etiquetas:

* As informações de etiquetagem devem ser implementados de acordo com toodocumented conceitos AZME
* Todas as informações de que necessita estão recolhidas (incluindo Valor de informações adicionais, Valor de informações da aplicação)
* Coincide de acordo com tooyout plano de etiquetas
* Não existem etiquetas enviadas em duplicado

Testar exaustivamente todos os tipos de Olá de comportamentos de notificações que ter incorporado na sua aplicação

* Anúncios, Inquéritos, Pushes de dados fora da aplicação e dentro da aplicação
* Vistas de texto/Web
* Atualização do destaque, Categorias

#### <a name="setup"></a>Configurar
Configurar o Azure Mobile Engagement é muito simples. Toda a documentação Olá relacionadas com a interface de utilizador toohello está disponível no Web site do Azure Mobile Engagement Olá, [como toonavigate Olá interface de utilizador](mobile-engagement-user-interface-home.md).

Recomenda-se que comece por configurar funções corretas Olá e associações de função para utilizadores Olá do seu projeto. Isto ajuda a gerir a plataforma de toohello acesso adequado para todos os utilizadores. As suas funções podem incluir:

* Administradores
* Programadores
* Visualizadores 

Posteriormente:

* Registe o tootest deviceID no seu próprio dispositivo.
* Aceda a definições de toohello da sua conta e configure gráficos de toohave Olá fuso horário e a hora de entrega de notificação definido para o seu fuso horário.
* Aceda a definições de toohello da sua aplicação e registe Olá "App-info" precisa de tootarget pelo utilizador final no alcance.

Para mais informações sobre como toorun push sua primeira campanha de notificações, consulte [como tooget iniciado utilizando e gerir pushes tooreach enviados aos utilizadores finais de tooyour](mobile-engagement-how-tos.md).

## <a name="conclusion"></a>Conclusão
Os Programas de Envolvimento são iterativos e deve melhorar continuamente os seus à medida que experimenta o que funciona melhor com a sua aplicação. 

Inicialmente, enquanto programar experiências com o engagement estratégias não tentam toobuild uma estratégia de envolvimento global completa. Adotar uma abordagem de passo a passo que identifica os KPIs e como tooleverage-los. A estratégia de envolvimento será exclusiva para cada aplicação.

Depois de ter programado alguma experiência, pode considerar adicionar Olá programas de envolvimento tooyour os seguintes:

* Controlo: adquire utilizadores e provavelmente define origens de recolha de dados. Do Azure mobile Engagement pode ser origens de recolha de toodata ligado. Permite-lhe os desempenhos de toomonitor de cada origem. Estas informações serão interessante toomaximize o investimento em aquisições. 
* Teste A/B: trata-se de uma parte essencial do programa de Envolvimento. Cada aplicação tem as suas próprias especificações. Com o teste A/B, pode melhorar o seu programa de envolvimento.
* Geolocalização: esta é uma grande oportunidade para as marcas. Funcionalidade de toothis Obrigado pode alcançar no sítio certo Olá e hora. Recomendamos que confirme que se recolheu dados suficientes comportamento de utilizador final antes de iniciar toouse geolocalização.
* Push de dados: o push de dados é um push invisível. O push de dados permite personalizar a sua aplicação com base no comportamento do utilizador final. Por exemplo, se um segmento de utilizadores consulta frequentemente produtos de alta, o proprietário da aplicação Olá pode enviar um push de dados que irá personalizar a respetiva home page com conteúdo de alta.

## <a name="next-steps"></a>Passos Seguintes
* [Criar uma conta do Azure Mobile Engagement](mobile-engagement-create.md).
* Visite [definir a sua estratégia de Mobile Engagement](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn mais sobre como definir a estratégia de Mobile Engagement.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
