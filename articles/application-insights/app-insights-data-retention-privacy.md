---
title: "aaaData retenção e armazenamento no Azure Application Insights | Microsoft Docs"
description: "Declaração de política de retenção e privacidade"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Recolha de dados, retenção e armazenamento no Application Insights


Quando instala [Azure Application Insights] [ start] SDK na sua aplicação, envia telemetria sobre o toohello de aplicação na nuvem. Naturalmente, os programadores responsável pretendem tooknow exatamente os dados que são enviados, o que acontece toohello dados e como se podem manter o controlo do mesmo. Em especial, foi possível enviar os dados confidenciais, onde é que está armazenada e como protegem é? 

Primeira, resposta curto Olá:

* módulos de telemetria padrão de Olá executados "Box Olá" são serviço de toohello toosend pouco provável dados confidenciais. telemetria de Olá está preocupada com carga, métricas de desempenho e a utilização, relatórios de exceções e outros dados de diagnóstico. dados de utilizador principal de Olá visíveis nos relatórios de diagnóstico Olá são URLs; mas a sua aplicação em qualquer dos casos não deve colocar os dados confidenciais em texto simples num URL.
* Pode escrever o código que envia telemetria personalizada adicionais toohelp que com diagnóstico e utilização de monitorização. (Este extensibilidade é uma funcionalidade excelente do Application Insights). Seria possível que, por erro, toowrite este código, para que inclui pessoal e outros dados confidenciais. Se a aplicação funciona com esses dados, deve aplicar um código Olá de detalhado revisão processos tooall escrita.
* Ao desenvolver e testar a sua aplicação, é fácil tooinspect que estão a ser enviado pelo Olá SDK. dados de Olá aparecem no Olá depuração windows de saída do browser e Olá IDE. 
* dados de Olá são mantidos em [Microsoft Azure](http://azure.com) servidores no Olá EUA ou Europa. (Mas a aplicação pode ser executado em qualquer local). O Azure tem [segurança forte processa e cumpre uma vasta gama de normas de conformidade](https://azure.microsoft.com/support/trust-center/). Só tem e a sua designada equipa têm acesso tooyour dados. Os funcionários da Microsoft podem ter restringido a acesso tooit apenas em circunstâncias limitadas específicas com o conhecimento do utilizador. São encriptado em trânsito, apesar de não estiver em servidores de Olá.

rest Olá deste artigo elaborates mais detalhadamente nestes respostas. Foi concebido toobe autónomo, para que pode apresentar-toocolleagues que não fazem parte da sua equipa de imediato.

## <a name="what-is-application-insights"></a>O que é o Application Insights?
[Azure Application Insights] [ start] é um serviço fornecido pela Microsoft que o ajuda a melhorar o desempenho de Olá e facilidade de utilização da sua aplicação em direto. Monitoriza a aplicação tempo Olá está em execução, durante os testes e depois de ter publicado ou implementado. Application Insights cria gráficos e tabelas que mostram, por exemplo, as horas do dia que obtém a maior parte dos utilizadores, como a aplicação Olá reativo está e como também servido por qualquer externos de serviços que depende. Se existirem falhas, falhas ou problemas de desempenho, pode procurar dados de telemetria de Olá em causa de Olá toodiagnose de detalhe. E serviço Olá irá enviar-lhe e-mails se existirem quaisquer alterações na disponibilidade de Olá e o desempenho da sua aplicação.

Na ordem tooget esta funcionalidade, instala um Application Insights SDK na sua aplicação, que passa a fazer parte do seu código. Quando a aplicação está em execução, Olá SDK monitoriza a conclusão da operação e envia o serviço de Application Insights toohello de telemetria. Este é um serviço em nuvem alojado pela [Microsoft Azure](http://azure.com). (Mas Application Insights funciona para quaisquer aplicações, não apenas os que estão alojados no Azure).

![Olá SDK na sua aplicação envia telemetria toohello serviço Application Insights.](./media/app-insights-data-retention-privacy/01-scheme.png)

Olá serviço Application Insights armazena e analisa a telemetria de Olá. análise de Olá toosee ou de pesquisa através de Olá armazenados telemetria, iniciar sessão tooyour conta do Azure e o recurso do Application Insights Olá aberto para a sua aplicação. Também pode aceder a partilha toohello dados com outros membros da sua equipa ou com os subscritores do Azure especificados.

Pode fazer com que dados exportados a partir do Olá serviço Application Insights, por exemplo tooa base de dados ou tooexternal ferramentas. Fornecer cada ferramenta com uma chave especial que obteve do serviço de Olá. pode ser revogado chave Olá, se necessário. 

SDKs do Application Insights estão disponíveis para uma variedade de tipos de aplicação: web serviços alojados no seus próprios servidores J2EE ou ASP.NET, ou no Azure; clientes Web - ou seja, código de Olá em execução numa página web; aplicações de ambiente de trabalho e serviços; aplicações de dispositivos, como o Windows Phone, iOS e Android. Enviam telemetria toohello mesmo serviço.

## <a name="what-data-does-it-collect"></a>Os dados que-recolhe?
### <a name="how-is-hello-data-is-collected"></a>Como é dados Olá é recolhidas?
Existem três origens de dados:

* Olá SDK, que integrar com a sua aplicação ou [no desenvolvimento](app-insights-asp-net.md) ou [em tempo de execução](app-insights-monitor-performance-live-website-now.md). Existem SDKs diferentes para tipos de aplicação diferente. Há também um [SDK para páginas web](app-insights-javascript.md), que carrega para browser Olá do utilizador final, juntamente com a página Olá.
  
  * Cada SDK tem um número de [módulos](app-insights-configuration-with-applicationinsights-config.md), que utilizam diferentes técnicas toocollect os diferentes tipos de telemetria.
  * Se instalar Olá SDK de desenvolvimento, pode utilizar o toosend API sua própria telemetria, módulos de padrão de toohello de adição. Esta telemetria personalizada pode incluir quaisquer dados que pretende toosend.
* Em alguns servidores web, também existem agentes que são executados em conjunto com a aplicação Olá e enviar telemetria sobre a CPU, memória e ocupação da rede. Por exemplo, as VMs do Azure, anfitriões de Docker, e [J2EE servidores](app-insights-java-agent.md) pode ter desses agentes.
* [Testes de disponibilidade](app-insights-monitor-web-app-availability.md) processos são executados pela Microsoft que enviam pedidos tooyour web app em intervalos regulares. resultados de Olá são enviados toohello serviço de Application Insights.

### <a name="what-kinds-of-data-are-collected"></a>Os tipos de dados são recolhidos?
categorias principais Olá são:

* [Telemetria do servidor de Web](app-insights-asp-net.md) -pedidos de HTTP.  URI, o pedido de Olá tooprocess de tempo decorrido, o código de resposta, o endereço IP do cliente. Id de sessão.
* [Páginas Web](app-insights-javascript.md) -contagens de sessões, utilizador e página. Tempos de carregamento de página. Exceções. Chamadas AJAX.
* Desempenho contadores - memória, CPU, e/s, ocupação da rede.
* Cliente e servidor contexto - SO, região, tipo de dispositivo, browser, resolução do ecrã.
* [Exceções](app-insights-asp-net-exceptions.md) e falhas - **capturas da pilha**, criar id, o tipo de CPU. 
* [Dependências](app-insights-asp-net-dependencies.md) -chama tooexternal serviços como o REST, SQL, AJAX. URI ou cadeia de ligação, duração, com êxito, o comando.
* [Testes de disponibilidade](app-insights-monitor-web-app-availability.md) -duração de teste e os passos, as respostas.
* [Registos de rastreio](app-insights-asp-net-trace-logs.md) e [telemetria personalizada](app-insights-api-custom-events-metrics.md) - **nada código no seu registos ou telemetria**.

[Mais detalhadamente](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>Como posso verificar o que é recolhido?
Se estiver a desenvolver aplicações Olá com o Visual Studio, execute a aplicação Olá no modo de depuração (F5). telemetria de Olá é apresentado na janela de resultados de Olá. A partir daí, pode copiá-lo e formate-o como JSON para inspecção fácil. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

Há também uma vista mais legível na janela de diagnóstico de Olá.

Para páginas web, abra a janela de depuração do seu browser.

![Premir a tecla F12 e abra o separador de Olá de rede.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>Posso escrever telemetria do código toofilter Olá antes de ser enviada?
Isto seria possível escrevendo um [Plug-in de processador de telemetria](app-insights-api-filtering-sampling.md).

## <a name="how-long-is-hello-data-kept"></a>Quanto tempo são dados Olá mantidos?
Pontos de dados não processados (ou seja, os itens que pode consultar na análise e inspecionar na pesquisa) são mantidos durante a cópia de segurança too90 dias. Se precisar de dados de tookeep superior que, pode utilizar [a exportação contínua](app-insights-export-telemetry.md) toocopy-tooa conta de armazenamento.

Dados agregados (ou seja, contagens, médias e outros dados estatísticos que visualiza no Explorador de métrica) são retidos num intervalo de 1 minuto 90 dias.

## <a name="who-can-access-hello-data"></a>Quem pode aceder a dados Olá?
dados de Olá estão visível tooyou e, se tiver uma conta de organização, os membros do agrupamento. 

Podem ser exportado pelo utilizador e os membros da equipa e pode ser copiado tooother localizações e transmitido tooother pessoas.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>Que does Microsoft fazem com informações de Olá a minha aplicação envia tooApplication Insights?
A Microsoft utiliza os dados de Olá apenas na ordem tooprovide Olá serviço tooyou.

## <a name="where-is-hello-data-held"></a>Onde estão contidos dados Olá?
* No Olá EUA ou Europa. Pode selecionar a localização de Olá quando cria um novo recurso do Application Insights. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>Significa que a minha aplicação tem toobe alojada no Olá EUA ou Europa?
* Não. A aplicação pode executar em qualquer local, na suas própria anfitriões no local ou no Olá na nuvem.

## <a name="how-secure-is-my-data"></a>Qual é o como protegem os meus dados?
Application Insights é um serviço do Azure. As políticas de segurança descritas Olá [segurança do Azure, privacidade e conformidade documento técnico](http://go.microsoft.com/fwlink/?linkid=392408).

dados de Olá são armazenados nos servidores do Microsoft Azure. Para contas do Olá Portal do Azure, as restrições de conta são descritas nas Olá [documento de segurança do Azure, privacidade e conformidade](http://go.microsoft.com/fwlink/?linkid=392408).

Aceder a dados tooyour pela equipa da Microsoft é restrita. Iremos aceder aos seus dados apenas com a sua permissão e se é necessário toosupport a utilização do Application Insights. 

Dados agregados em todas as aplicações de todos os nossos clientes (por exemplo, taxas de dados e o tamanho médio de rastreios) são utilizado tooimprove Application Insights.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>Telemetria de outra pessoa pode interferir com os meus dados do Application Insights?
Foi enviam a conta de tooyour telemetria adicionais utilizando a chave de instrumentação Olá, que pode ser encontrado no código Olá das suas páginas web. Com a dados suficientes adicionais, métricas não corretamente representaria desempenho e a utilização da sua aplicação.

Se partilhar código com outros projetos, lembre-se tooremove sua chave de instrumentação.

## <a name="is-hello-data-encrypted"></a>Dados de Olá são encriptados?
Não dentro de servidores de Olá neste momento.

Todos os dados são encriptados são transmitidos entre centros de dados.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>Dados de Olá são encriptados em trânsito dos servidores de informações de tooApplication a minha aplicação?
Sim, iremos utilizar https toosend dados toohello portal a partir do quase todos os SDKs, incluindo servidores web, dispositivos e páginas web HTTPS. Exceção de apenas Olá é os dados enviados a partir de páginas de web HTTP simples. 

## <a name="personally-identifiable-information"></a>Informações de identificação pessoal
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>Foi informação identificativa (PII) enviado tooApplication Insights?
Sim, é possível. 

Como orientação geral:

* Telemetria mais standard (ou seja, telemetria enviada sem que escrever qualquer código) não inclui PII explícita. No entanto, poderá ser possível tooidentify indivíduos por inferência de uma coleção de eventos.
* Mensagens de exceção e rastreio podem conter PII
* Telemetria personalizada - ou seja, chamadas como TrackEvent escreve no código utilizando rastreios de registo ou a API de Olá - pode conter quaisquer dados que escolher.

tabela de Olá no final deste documento Olá contém descrições detalhadas mais Olá dados recolhidos.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>Pude responsável por complying com as leis e regulamentos no regard tooPII?
Sim. É o tooensure de responsabilidade coleção Olá e a utilização de dados de Olá está em conformidade com as leis e regulamentos e com Olá Microsoft Online Services termos.

Deve informar os seus clientes adequadamente sobre dados de Olá que recolhe da sua aplicação e como Olá dados são utilizados.

#### <a name="can-my-users-turn-off-application-insights"></a>Podem os meus utilizadores desativar Application Insights?
Não diretamente. Não, fornecemos um comutador que os utilizadores podem operar tooturn desativar Application Insights.

No entanto, pode implementar este tipo uma funcionalidade na sua aplicação. Olá todos os SDKs incluem uma definição de API que desativa a coleção de telemetria. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>A minha aplicação está a recolher inadvertidamente informações confidenciais. Application Insights limpar estes dados, de modo não é mantido?
Application Insights não filtrar ou eliminar os seus dados. Deve gerir dados Olá adequadamente e evitar o envio de tooApplication esses dados Insights.

## <a name="data-sent-by-application-insights"></a>Dados enviados pelo Application Insights
Olá SDKs variam entre plataformas e existem tem vários componentes que podem instalar. (Consulte demasiado[Application Insights - descrição geral][start].) Cada componente envia dados diferentes.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>Classes de dados enviados em cenários diferentes
| A acção | Classes de dados recolhidos (consulte a tabela seguinte) |
| --- | --- |
| [Adicione o projeto web do Application Insights SDK tooa .NET][greenbrown] |ServerContext<br/>Inferido<br/>Contadores de desempenho<br/>Pedidos<br/>**Exceções**<br/>Sessão<br/>utilizadores |
| [Instalar o Monitor de estado no IIS][redfield] |Dependências<br/>ServerContext<br/>Inferido<br/>Contadores de desempenho |
| [Adicionar a aplicação web do Application Insights SDK tooa Java][java] |ServerContext<br/>Inferido<br/>Pedir<br/>Sessão<br/>utilizadores |
| [Adicionar página de tooweb JavaScript SDK][client] |ClientContext <br/>Inferido<br/>Página<br/>ClientPerf<br/>AJAX |
| [Definir propriedades predefinidas][apiproperties] |**Propriedades** em todos os eventos padrão e personalizados |
| [Chamada TrackMetric][api] |Valores numéricos<br/>**Propriedades** |
| [Chamada controlar *][api] |Nome do evento<br/>**Propriedades** |
| [Chamada TrackException][api] |**Exceções**<br/>Captura de pilha<br/>**Propriedades** |
| SDK não é possível recolher dados. Por exemplo: <br/> -Não é possível aceder aos contadores de desempenho<br/> -exceção no inicializador de telemetria |Diagnóstico SDK |

Para [SDKs para outras plataformas][platforms], consulte os respetivos documentos.

#### <a name="hello-classes-of-collected-data"></a>classes de Olá dos dados recolhidos
| Classe de dados recolhidos | Inclui (não uma lista exaustiva) |
| --- | --- |
| **Propriedades** |**Quaisquer dados - determinados pelo seu código** |
| DeviceContext |ID IP, região, o modelo de dispositivo, rede, o tipo de rede, o nome OEM, resolução do ecrã, instância de função, o nome de função, o tipo de dispositivo |
| ClientContext |SO, região, idioma, rede, resolução de janela |
| Sessão |id de sessão |
| ServerContext |Nome da máquina, região, OS dispositivos, sessão de utilizador, contexto de utilizador, a operação |
| Inferido |geolocalização do endereço IP, timestamp, SO, browser |
| Métricas |O nome da métrica e valor |
| Eventos |Nome de evento e o valor |
| PageViews |Nome de URL e página ou o nome de ecrã |
| Desempenho do cliente |Nome do URL/página, tempo de carregamento do browser |
| AJAX |Chamadas HTTP a partir da página web tooserver |
| Pedidos |URL, a duração, código de resposta |
| Dependências |Tipo (SQL Server, HTTP,...), a cadeia de ligação ou URI, sincronização/async, duração, sucesso, instrução de SQL (com o Monitor de estado) |
| **Exceções** |Tipo de **mensagem**, chamar pilhas, ficheiros e a linha número, o id da thread de origem |
| Falhas |Id do processo, o id de processo principal, id de thread de falhas; patch de aplicação, id, compilação;  tipo de exceção, endereço, reason; ocultos símbolos e regista, endereços de início e de fim binários, nome binário e caminho, tipo de cpu |
| Rastreio |**Mensagem** e nível de gravidade |
| Contadores de desempenho |Tempo do processador, memória disponível, taxa de pedidos, taxa de exceção, bytes privados do processo, a taxa de e/s, duração de pedido, comprimento da fila de pedido |
| Disponibilidade |Código de resposta do teste Web, a duração de cada passo de teste, nome de teste, timestamp, sucesso, tempo de resposta, localização de teste |
| Diagnóstico SDK |Exceção ou mensagem de rastreio |

Pode [desactivar alguns dos dados de Olá editando Applicationinsights][config]

## <a name="credits"></a>Créditos
Este produto inclui dados de GeoLite2 criados por MaxMind, disponível a partir do [http://www.maxmind.com](http://www.maxmind.com).



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

