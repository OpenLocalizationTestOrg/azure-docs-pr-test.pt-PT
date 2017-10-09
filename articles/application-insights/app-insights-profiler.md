---
title: aaaProfiling em direto de web apps do Azure com o Application Insights | Microsoft Docs
description: "Identifica o caminho de acesso frequente Olá no seu código de servidor web com um gerador de perfis de requisitos de espaço insuficiente."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Criação de perfis de aplicações web do Azure em direto com o Application Insights

*Esta funcionalidade do Application Insights está GA para serviços de aplicações e na pré-visualização da computação.*

Saber quanto tempo é gasto a cada método na sua aplicação web em direto utilizando a ferramenta de criação de perfis de Olá [Azure Application Insights](app-insights-overview.md). Mostra-lhe perfis de detalhado de pedidos em direto que foram processados pela sua aplicação e realça Olá 'frequente path' que está a utilizar Olá mais tempo. Seleciona automaticamente os exemplos que tenham tempos de resposta diferentes. gerador de perfis de Olá utiliza a sobrecarga de toominimize várias técnicas.

Olá gerador de perfis atualmente funciona para o ASP.NET web aplicações em execução nos serviços de aplicações do Azure, no mínimo Olá Basic escalão de preço. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Ativar o gerador de perfis de Olá

[Instale o Application Insights](app-insights-asp-net.md) no seu código. Se já estiver instalado, certifique-se de que tem a versão mais recente Olá. (toodo isto, clique no projeto no Explorador de soluções e escolha pacotes NuGet gerir. Selecione as atualizações e todos os pacotes de atualização.) Implemente novamente a sua aplicação.

*Com o ASP.NET Core? [Verifique aqui](#aspnetcore).*

No [https://portal.azure.com](https://portal.azure.com), abra o recurso do Application Insights Olá para a sua aplicação web. Abra **desempenho** e clique em **ativar o gerador de perfis do Application Insights...** .

![Clique em Olá ativar faixa de gerador de perfis][enable-profiler-banner]

Em alternativa, pode sempre clicar **configurar** tooview Estado, ativar ou desativar Olá gerador de perfis.

![No painel de desempenho de Olá, clique em configurar][performance-blade]

Aplicações Web que estão configuradas com o Application Insights estão listadas no painel de configurar. Siga o agente de gerador de perfis de Olá do instruções tooinstall se for necessário. Se não existe nenhuma aplicação web ainda está configurada com o Application Insights, clique em *adicionar aplicações ligadas*.

Olá utilize *ativar o gerador de perfis* ou *desativar o gerador de perfis* botões no Olá configurar painel toocontrol Olá gerador de perfis em todas as suas aplicações web ligado.



![Configurar o painel][linked app services]

toostop ou a reinicialização Olá gerador de perfis para uma instância de serviço de aplicações individuais, pode encontrá-la **no Olá recurso do App Service**, na **trabalhos Web**. toodelete-lo, procure em **extensões**.

![Desativar o gerador de perfis para das tarefas da web][disable-profiler-webjob]

Recomendamos que tenha Olá gerador de perfis ativada em todos os seus web apps toodiscover qualquer desempenho emite logo que possível.

Se utilizar a aplicação de web WebDeploy toodeploy alterações tooyour, certifique-se de que excluir Olá **App_Data** pasta seja eliminado durante a implementação. Caso contrário, hello ficheiros da extensão do gerador de perfis será eliminado quando implementa tooAzure de aplicação web de Olá seguinte.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Utilizar o gerador de perfis com as VMs do Azure e recursos de computação (pré-visualização)

Quando lhe [ativar Application Insights para serviços de aplicações do Azure em tempo de execução](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), o gerador de perfis está automaticamente disponível. (Se ativou Application Insights para o recurso de Olá, poderá ser necessário tooupdate toohello lates versão através do Olá **configurar** assistente.)

Não existe um [versão de pré-visualização do Olá gerador de perfis para os recursos de computação do Azure](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>Limites

retenção de dados do Olá predefinido é de 5 dias. Máximo de 10 GB ingerido por dia.

Não há sem encargos durante o serviço do gerador de perfis de Olá. A aplicação web tem de estar alojada no Olá, pelo menos, o escalão básico dos serviços de aplicações.

## <a name="viewing-profiler-data"></a>Visualizar dados do gerador de perfis

Abra o painel de desempenho de Olá e desloque-se para baixo a lista de operações toohello.




![Painel de informações de desempenho de aplicações coluna de exemplos][performance-blade-examples]

Olá as colunas na tabela de Olá são:

* **Contagem** -Olá diversas estes pedidos no intervalo de tempo de Olá do painel de Olá.
* **Mediana** -tempo normal Olá a aplicação demora toorespond tooa pedido. Metade de todas as respostas foram mais rápida do que isto.
* **percentil 95th** 95% das respostas foram mais rápida do que isto. Se desta figura é muito diferente do valor mediano de Olá, poderá existir um problema intermitente faça com a sua aplicação. (Ou pode ser explicado por uma funcionalidade de estrutura como colocação em cache)
* **Exemplos** -um ícone indica que o gerador de perfis Olá tem capturar rastreios de pilha para esta operação.

Clique em Explorador de rastreio de Olá ícone tooopen Olá exemplos. Olá explorer mostra alguns exemplos que Olá gerador de perfis foi capturado, classificados por tempo de resposta.

Selecione tooshow um exemplo de uma divisão de nível de código de tempo gasto em execução Olá pedido.

![Explorador de rastreio do Application Insights][trace-explorer]

**Mostrar caminho frequente** abre Olá maior nó de folha ou, pelo menos, algo fechar. Na maioria dos casos, este nó será estrangulamento do desempenho tooa adjacente.



* **Etiqueta**: nome de Olá da função de Olá ou eventos. árvore de Olá mostra uma combinação de código e os eventos que ocorreram (por exemplo, eventos SQL e http). evento superior Olá representa Olá geral duração do pedido.
* **Decorrido**: intervalo de tempo de Olá entre o início de Olá da operação de Olá e de fim de Olá.
* **Quando**: mostra quando Olá função/evento estava a ser executado nas funções de tooother de relação.

## <a name="how-tooread-performance-data"></a>Como os dados de desempenho de tooread

O gerador de perfis do Microsoft service utiliza uma combinação de amostragem método instrumentação tooanalyze Olá desempenho e da sua aplicação.
Quando a coleção de detalhado está em curso, exemplos de gerador de perfis de serviço Olá ponteiro de instrução de cada de CPU da máquina de Olá em cada milissegundo.
Cada amostra captura pilha de chamadas de conclusão de Olá do thread de Olá atualmente em execução, fornecer informações úteis e detalhadas sobre o que se thread estava a fazer em ambos alta e baixa níveis de abstração. Gerador de perfis de serviço também recolhe outros eventos, tais como eventos de mudança de contexto, eventos TPL e correlação de atividade do conjunto de threads eventos tootrack e causality.

a pilha de chamadas de Olá apresentada na vista de linha cronológica de Olá é resultado Olá Olá acima amostragem e instrumentação. Porque cada amostra captura pilha de chamadas de conclusão de Olá do thread de Olá, inclui código da estrutura de .NET Olá, bem como outras estruturas que referenciar.

### <a id="jitnewobj"></a>Alocação de objeto (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1`são funções de programa auxiliar no interior do .NET framework que aloca a memória a partir da área dinâmica para dados geridos. `clr!JIT\_New`é invocada quando existe um objeto é alocado. `clr!JIT\_Newarr1`é invocada quando é atribuída uma matriz de objetos. Estas duas funções são, normalmente, muito rápidas em devem tomar relativamente pequeno período de tempo. Se vir `clr!JIT\_New` ou `clr!JIT\_Newarr1` demorar uma quantidade substancial de tempo na sua linha cronológica, é uma indicação de que o código de Olá pode ser alocar muitos objetos e consumir quantidade significativa de memória.

### <a id="theprestub"></a>Carregar código (`clr!ThePreStub`)
`clr!ThePreStub`é uma função de programa auxiliar no interior do .NET framework que prepara Olá código tooexecute Olá pela primeira vez. Isto inclui normalmente, mas não limitado a, compilação JIT (apenas no tempo). Para cada método c#, `clr!ThePreStub` deve ser invocado no máximo uma vez durante a duração de Olá de um processo.

Se vir `clr!ThePreStub` demora quantidade significativa de tempo de um pedido, indica esse pedido é Olá primeiro um que executa a esse método e tempo Olá tooload de tempo de execução do .NET framework que o método é significativo. Pode considerar um processo de warm-up que executa a que parte do código Olá antes dos utilizadores aceder ao mesmo ou considere executar NGen no seu assemblagens.

### <a id="lockcontention"></a>Bloquear contenção (`clr!JITutil\_MonContention` ou `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`ou `clr!JITutil\_MonEnterWorker` indicar o thread actual Olá está a aguardar um toobe bloqueio lançada. Isto normalmente aparece quando executar uma c# bloqueio instrução, invocar o método Monitor.Enter ou invocar um método com o atributo Methodimploptions. Contenção ocorre normalmente quando o thread A adquire um bloqueio e thread B tenta Olá tooacquire mesmo de bloqueio antes de thread A versões-lo.

### <a id="ngencold"></a>Carregar código (`[COLD]`)
Se o nome do método Olá contém `[COLD]`, tais como `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, significa que runtime do Olá .NET framework está a executar o código que não está otimizado por <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">orientado por perfil otimização</a> para Olá pela primeira vez. Para cada método, deve agora mostrar cópias de segurança no máximo uma vez durante a duração de Olá do processo de Olá.

Se carregar código demora bastante tempo para um pedido, ele indica esse pedido é Olá primeiro um tooexecute Olá servirem parte do método Olá. Pode considerar um transfira segurança processo que executa a que parte do código Olá antes dos utilizadores aceder ao mesmo.

### <a id="httpclientsend"></a>Enviar o pedido HTTP
Métodos, tais como `HttpClient.Send` indicar o código de Olá está a aguardar um toocomplete de pedido HTTP.

### <a id="sqlcommand"></a>Operação de base de dados
Método como SqlCommand.Execute indica o código de Olá está a aguardar um toocomplete de operação de base de dados.

### <a id="await"></a>A aguardar (`AWAIT\_TIME`)
`AWAIT\_TIME`indica o código de Olá está a aguardar outro toocomplete de tarefas. Esta situação ocorre normalmente com c# 'await' da instrução. Quando executa o código de Olá um c# 'await', hello thread unwinds e devolve o conjunto de threads do toohello controlo e não há nenhum thread que está bloqueado aguardar Olá 'await' toofinish. No entanto, logicamente Olá thread que foi Olá await é 'Bloqueado' aguardar Olá operação toocomplete. O `AWAIT\_TIME` indica o tempo de Olá bloqueado aguardar Olá toocomplete de tarefas.

### <a id="block"></a>Tempo bloqueado
`BLOCKED_TIME`indica o código de Olá está a aguardar outro toobe recursos disponível, tais como a aguardar que um objeto de sincronização, aguardar um toobe thread disponível, ou aguardar toofinish um pedido.

### <a id="cpu"></a>Tempo de CPU
Olá CPU está ocupado executar instruções Olá.

### <a id="disk"></a>Tempo de disco
aplicação Olá está a efetuar operações de disco.

### <a id="network"></a>Tempo da rede
aplicação Olá está a efetuar operações de rede.

### <a id="when"></a>Quando coluna
Esta é uma visualização de como exemplos, INCLUSIVE Olá recolhidos para um nó variam ao longo do tempo. Olá total do intervalo do pedido de Olá está dividido em 32 registos de tempo e exemplos de inclusive Olá para esse nó são acumulados para esses registos 32. Cada registo, em seguida, é representado como uma barra cuja altura representa um valor expandido. Para nós marcado `CPU_TIME` ou `BLOCKED_TIME`, ou onde existe uma relação óbvias de consumir um recurso (cpu, disco, thread), Olá barra representa consumir um destes recursos Olá durante período de tempo do que o registo. Para estas métricas, pode obter superior a 100% consumir recursos de vários. Por exemplo, se em média utilizar duas CPUs, ao longo de um intervalo, em seguida, pode obter 200%.


## <a id="troubleshooting"></a>Resolução de Problemas

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Como saber se o gerador de perfis do Application Insights está em execução?

gerador de perfis de Olá é executado como um trabalho web contínua na aplicação Web. Pode abrir o recurso de aplicação Web de Olá no https://portal.azure.com e verificar o estado de "ApplicationInsightsProfiler" no painel de WebJobs Olá. Se não está em execução, abra **registos** toofind mais informações.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>Por que motivo não consigo encontrá qualquer exemplos de pilha apesar do gerador de perfis de Olá está em execução?

Seguem-se algumas coisas, que pode verificar.

1. Certifique-se do plano do serviço Web App escalão básico e superior.
2. Certifique-se a aplicação Web com o Application Insights SDK 2.2 Beta e acima ativada.
3. Certifique-se a que sua aplicação Web tem definição de APPINSIGHTS_INSTRUMENTATIONKEY Olá com Olá mesma chave de instrumentação utilizada pelo Application Insights SDK.
4. Certifique-se a sua aplicação Web está em execução no .net Framework 4.6.
5. Se se tratar de uma aplicação ASP.NET Core, também verifique [Olá necessário dependências](#aspnetcore).

Depois de iniciado o gerador de perfis de Olá, há um período curto warm-up quando o gerador de perfis de Olá recolhe ativamente várias rastreios de desempenho. Depois disso, o gerador de perfis de Olá recolhendo rastreios de desempenho de dois minutos em cada hora.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>Estava a utilizar o gerador de perfis de serviço de Azure. Que tooit happened?  

Quando ativa o gerador de perfis do Application Insights, o agente do gerador de perfis de serviço de Azure está desativada.

### <a id="double-counting"></a>Valor de duplo contando em threads paralelas

Olá alguns casos métrica do tempo total no Visualizador de pilha Olá é superior a duração real da Olá de pedido de Olá.

Isto pode acontecer quando existem duas ou mais threads associadas a um pedido, a funcionar em paralelo. tempo total de threads de Olá, em seguida, é maior do que o tempo decorrido de Olá. Em muitos casos, um thread pode aguardar a resposta de Olá outro toocomplete. Olá Visualizador tenta toodetect isto e omitir espera desinteressantes Olá, mas errs no lado de Olá de mostrar demasiada em vez de omitindo que podem ser informações críticas.  

Quando vir threads paralelas nos seus rastreios, terá de toodetermine que threads estão a aguardar para que possa determinar caminho crítico de Olá para pedido de Olá. Na maioria dos casos, o thread de Olá que rapidamente ficar num Estado de espera é simplesmente aguardar Olá outros threads. Concentrar-se no Olá outras pessoas e ignorar o tempo de Olá em threads em espera Olá.

### <a id="issue-loading-trace-in-viewer"></a>Não existem dados de criação de perfis

1. Se os dados de Olá que está a tentar tooview com mais de duas semanas, tente limitar o filtro de tempo e tente novamente.

2. Verificação de proxies ou uma firewall não ter bloqueado toohttps://gateway.azureserviceprofiler.net acesso.

3. Verifique que Olá Application Insights é a chave de instrumentação que está a utilizar na sua aplicação Olá mesmo como Olá tiver ativado a criação de perfis com o recurso do Application Insights. chave de Olá está normalmente nas Applicationinsights, mas também pode ser encontrado na Web. config ou o App. config.

### <a name="error-report-in-hello-profiling-viewer"></a>Relatório de erros no Visualizador de criação de perfis de Olá

Um pedido de suporte do portal de Olá de ficheiros. Inclua Olá ID de correlação da mensagem de erro de saudação.

## <a name="manual-installation"></a>Instalação manual

Quando configura o gerador de perfis de Olá, hello seguintes atualizações que são efetuadas definições da aplicação Web toohello. Pode fazê-las pessoalmente manualmente se o seu ambiente necessitar, por exemplo, se a aplicação for executada no ambiente de serviço de aplicações do Azure (ASE):

1. No painel de controlo de aplicação web Olá, abra as definições.
2. Definir ".Net Framework versão" toov4.6.
3. Definir tooOn "Always On".
4. Adicionar definição de aplicação "__APPINSIGHTS_INSTRUMENTATIONKEY__" e o conjunto Olá valor toohello a mesma chave de instrumentação utilizado pelo Olá SDK.
5. Abrir as ferramentas avançadas.
6. Clique em "Ir" tooopen Olá Kudu Web site.
7. No Web site do Kudu Olá, selecione "As extensões de Site".
8. Instalar "__Application Insights__" da galeria.
9. Reinicie a aplicação de web de Olá.

## <a id="aspnetcore"></a>Suporte de núcleo de ASP.NET

Aplicação de ASP.NET Core tem tooinstall 2.1.0-beta6 de pacote Microsoft.ApplicationInsights.AspNetCore Nuget ou superior toowork com Olá gerador de perfis. Já não suportamos versões inferiores Olá após 27/6/2017.

## <a name="next-steps"></a>Passos seguintes

* [Trabalhar com o Application Insights no Visual Studio](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
