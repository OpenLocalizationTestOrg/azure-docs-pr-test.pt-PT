---
title: "aaaTroubleshooting diagnósticos do Azure | Microsoft Docs"
description: "Resolva problemas quando utiliza o diagnóstico do Azure em Virtual Machines do Azure, Service Fabric ou serviços em nuvem."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Resolução de problemas de diagnóstico do Azure
Resolução de problemas informações relevantes toousing diagnósticos do Azure. Para obter mais informações sobre o diagnóstico do Azure, consulte [descrição geral do Azure Diagnostics](azure-diagnostics.md).

## <a name="logical-components"></a>Componentes lógicos
**O iniciador de plug-in de diagnóstico (DiagnosticsPluginLauncher.exe)**: inicia a extensão de diagnóstico do Azure Olá. Funciona como entrada Olá processo ponto.

**Plug-in de diagnóstico (DiagnosticsPlugin.exe)**: processo principal que é iniciado pelo iniciador Olá acima e configura o agente de monitorização de Olá, inicia-lo e gere o seu período de duração. 

**Agente de monitorização (MonAgent\*.exe processos)**: estes processos Olá em massa do trabalho Olá; ou seja, monitorização, a coleção e a transferência de dados de diagnóstico Olá.  

## <a name="logartifact-paths"></a>Caminhos de registo/artefactos
Seguem-se os registos de Olá caminhos toosome importantes e de artefactos. Vamos manter referenciando toothese em todo o restante documento Olá Olá:
### <a name="cloud-services"></a>Serviços Cloud
| Artefactos | Caminho |
| --- | --- |
| **Ficheiro de configuração de diagnósticos do Azure** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versão > \Config.txt |
| **Ficheiros de registo** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versão > \ |
| **Arquivo local para dados de diagnóstico** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Tables |
| **Ficheiro de configuração do agente de monitorização** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Pacote de extensão de diagnóstico do Azure** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<versão > |
| **Caminho do utilitário de recolha de registo** | %SystemDrive%\Packages\GuestAgent\ |
| **Ficheiro de registo MonAgentHost** | C:\Resources\Directory\<CloudServiceDeploymentID >.\< RoleName >. DiagnosticStore\WAD0107\Configuration\MonAgentHost.. log de < seq_num > |

### <a name="virtual-machines"></a>Virtual Machines
| Artefactos | Caminho |
| --- | --- |
| **Ficheiro de configuração de diagnósticos do Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versão > \RuntimeSettings |
| **Ficheiros de registo** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versão > \Logs\ |
| **Arquivo local para dados de diagnóstico** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Tables |
| **Ficheiro de configuração do agente de monitorização** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Configuration\MaConfig.xml |
| **Ficheiro de estado** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<versão > \Status |
| **Pacote de extensão de diagnóstico do Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion >|
| **Caminho do utilitário de recolha de registo** | C:\WindowsAzure\Packages |
| **Ficheiro de registo MonAgentHost** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion > \WAD0107\Configuration\MonAgentHost. < seq_num >. log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>Dados métricos não mostram no portal do Azure
Diagnóstico do Azure fornece um bunch de métricos dados, que podem ser apresentados no portal do Azure. Se tiver problemas com a ver estes dados no portal, a conta de armazenamento de diagnóstico de Olá de verificação -> WADMetrics\* tabela toosee se existem registos de métrica correspondente Olá. Aqui, Olá PartitionKey da tabela de Olá é Olá ID de recurso de máquina virtual ou o conjunto de dimensionamento da máquina virtual e Olá RowKey é o nome da métrica Olá ou seja, nome do contador de desempenho.

Se o ID de recurso Olá estiver incorreto, verifique a configuração de diagnósticos -> métricas -> ResourceId toosee se o ID de recurso Olá está definido corretamente.

Se não houver nenhum dado para métrica específica Olá, verifique a configuração de diagnósticos -> PerformanceCounter toosee se a métrica de Olá (contador de desempenho) está incluída. Iremos ativar Olá os seguintes contadores por predefinição.
- \Processor(_Total)\% Processor Time
- \Memory\Available Bytes
- \ASP.NET aplicações (__Total__) \Requests/Sec
- \ASP.NET aplicações (__Total__) \Errors totais/seg
- \ASP.NET\Requests colocados em fila
- \ASP.NET\Requests rejeitados
- \Processor(w3wp)\% de tempo do processador
- Bytes de \Private \Process (w3wp)
- \Process(WaIISHost)\% de tempo do processador
- Bytes de \Private \Process (WaIISHost)
- \Process(WaWorkerHost)\% de tempo do processador
- Bytes de \Private \Process (WaWorkerHost)
- \Memory\Page falhas por segundo
- \.Memória NET CLR (_Global_)\% tempo na GC
- \LogicalDisk (c) \Disk escrita Bytes/seg
- \Disk \LogicalDisk (c) Bytes lidos/seg
- \LogicalDisk (d:) \Disk escrita Bytes/seg
- \Disk \LogicalDisk (d:) Bytes lidos/seg

Se a configuração de Olá está definida corretamente, mas não podem ver dados métricos Olá, siga as diretrizes de Olá, abaixo, para investigação adicional Olá.


## <a name="azure-diagnostics-is-not-starting"></a>Diagnóstico do Azure não está a iniciar
Observe **DiagnosticsPluginLauncher.log** e **DiagnosticsPlugin.log** ficheiros de registo de ficheiros a partir da localização de Olá de Olá fornecida acima para obter informações sobre o motivo falha diagnostics toostart. 

Se estes registos indicam `Monitoring Agent not reporting success after launch`, significa que ocorreu uma falha ao iniciar MonAgentHost.exe. Procure os registos de Olá que na localização de Olá indicada para `MonAgentHost log file` na secção de Olá acima.

a última linha de Olá Olá dos ficheiros de registo contém o código de saída Olá.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Se encontrar um **negativo** código de saída, consulte toohello [tabela de código de saída](#azure-diagnostics-plugin-exit-codes) no Olá [referências](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Dados de diagnóstico são não tem sessão iniciada tooAzure do armazenamento
Determine se não existem dados está a ser mostrada cópias de segurança ou apenas alguns dos dados de Olá é não ser apresentado.

### <a name="diagnostics-infrastructure-logs"></a>Registos de infraestrutura de diagnóstico
Os registos de infraestrutura de diagnóstico é onde quaisquer erros que é executada para os registos de diagnóstico do azure. Certifique-se de que ativou ([como?](#how-to-check-diagnostics-extension-configuration)) captura dos registos de diagnóstico infraestrutura na configuração do seu e rapidamente Procure quaisquer erros relevantes que apareçam na Olá `DiagnosticInfrastructureLogsTable` tabela na sua conta de armazenamento configurados.

### <a name="no-data-is-showing-up"></a>Não existem dados está a ser mostrada cópias de segurança
causa mais comum de Olá de dados de eventos totalmente em falta é informações da conta de armazenamento definidas incorretamente.

Solução: Corrija a configuração de diagnósticos e reinstalar o diagnóstico.

Se a conta de armazenamento Olá está corretamente configurado e remoto ambiente de trabalho na máquina de Olá e faça se DiagnosticsPlugin.exe e MonAgentCore.exe estão em execução. Se não estiverem a executar, siga [diagnósticos do Azure não está a iniciar](#azure-diagnostics-is-not-starting). Se estiver a executar processos Olá, avance demasiado[dados obter capturadas localmente](#is-data-getting-captured-locally) e seguir este guia a partir daí no.

### <a name="part-of-hello-data-is-missing"></a>Parte dos dados de Olá está em falta
Se estiver a obter alguns dados, mas não a outros. Isto significa que a recolha de dados de Olá / pipeline de transferência está definida corretamente. Siga subsecções Olá aqui toonarrow baixo que problema Olá é:
#### <a name="is-collection-configured"></a>A coleção é configurada: 
Diagnóstico de configuração contém a parte Olá que dá instruções para um determinado tipo de toobe dados recolhido. [Reveja a configuração](#how-to-check-diagnostics-extension-configuration) toomake certificar-se de que não procura dados não tiver configurado para a coleção.
#### <a name="is-hello-host-generating-data"></a>É anfitrião Olá gerar dados:
- **Contadores de desempenho**: Abra perfmon e verifique o contador de Olá.
- **Registos de rastreio**: ambiente de trabalho remoto para Olá VM e adicione o ficheiro de configuração de uma aplicação de toohello de TextWriterTraceListener.  Consulte http://msdn.microsoft.com/library/sk36c28t.aspx tooset se o serviço de escuta do Olá texto.  Certifique-se de que Olá `<trace>` elemento tem `<trace autoflush="true">`.<br />
Se não vir os registos de rastreio gerados, siga [mais sobre o rastreio registos em falta](#more-about-trace-logs-missing).
- **Rastreios ETW**: ambiente de trabalho remoto para Olá VM e instalar PerfView.  PerfView executar ficheiro -> utilizador comando -> escuta etwprovder1, etwprovider2, etc.  Tenha em atenção que Olá escuta comando maiúsculas e minúsculas e não pode ser espaços entre a lista de valores separados por vírgulas de Olá de fornecedores ETW.  Se o comando de Olá falhar toorun, pode clicar em Olá 'Log' botão Olá inferior direito da Olá Perfview ferramenta toosee que foi tentada toorun e o resultado de Olá era.  Partindo do princípio de entrada de Olá está correta, em seguida, uma nova janela será destaque cópias de segurança e dentro de alguns segundos irá começar a ver os rastreios ETW.
- **Registos de eventos**: ambiente de trabalho remoto para Olá VM. Abra `Event Viewer` e certifique-se de que existem eventos Olá.
#### <a name="is-data-getting-captured-locally"></a>Dados obter capturados localmente:
Em seguida certifique-se dados Olá obter capturados localmente.
dados de Olá são armazenados localmente na `*.tsf` ficheiros em [arquivo local do Olá para dados de diagnóstico](#log-artifacts-path). Diferentes tipos de registos obterem recolhidos em diferentes `.tsf` ficheiros. nomes de Olá são os nomes das tabelas toohello semelhante no armazenamento do azure. Por exemplo `Performance Counters` obter recolhido em `PerformanceCountersTable.tsf`, registos de eventos obter recolhidos no `WindowsEventLogsTable.tsf`. Utilize as instruções Olá [Local de registo de extração](#local-log-extraction) secção ficheiros de recolha local tooopen Olá e certifique-se de que vê-los, obtendo recolhidos no disco.

Se não consulte os registos obter recolhidos localmente e tiver verificado que anfitrião Olá está a gerar dados, terá provavelmente de um problema de configuração. Reveja a configuração cuidadosamente quanto a secção adequada Olá. Reveja também configuração Olá gerada para MonitoringAgent [MaConfig.xml](#log-artifacts-path) e certifique-se de que existe algum secção descreverem a origem de registo relevantes Olá e que não há perda na tradução entre a configuração de diagnóstico do azure e a configuração do agente de monitorização.
#### <a name="is-data-getting-transferred"></a>Obter transferidos dados:
Se tiver verificado dados Olá obter capturados localmente, mas ainda não o vir na sua conta de armazenamento: 
- Primeiro e mais importante, certifique-se de que forneceu uma conta de armazenamento correta e que não tenham revertida através de chaves etc.for Olá fornecido a conta de armazenamento. Para serviços em nuvem, por vezes, Vemos que pessoas não atualizar os respetivos `useDevelopmentStorage=true`.
- Se especificar a conta de armazenamento está correta. Certifique-se que não tiver algumas restrições de rede que não permita que os componentes de Olá pontos finais de armazenamento pública tooreach. Uma forma toodo que é o ambiente de trabalho tooremote para Olá máquina e tente toowrite algo toohello mesmo armazenamento de contas por si.
- Por fim, pode tentar e ver que falha estão a ser reportados pelo agente de monitorização. Agente de monitorização escreve os seus registos `maeventtable.tsf` localizados em [arquivo local do Olá para dados de diagnóstico](#log-artifacts-path). Siga as instruções em [Local de registo de extração](#local-log-extraction) secção tooopen este ficheiro e tente e averiguar se existem `errors` com a indicação de ficheiros locais do falhas tooread ou escrever toostorage.

### <a name="capturing--archiving-logs"></a>Capturar / arquivo de registos
Ocorreu um erro através de Olá os passos acima, mas não foi possível descobrir o que estava incorreto e estão a ter em consideração contactar o suporte. Step-by-Olá primeira coisa que poderão pedir que é toocollect registos do seu computador. Pode poupar tempo ao fazer esse por si. Executar Olá `CollectGuestLogs.exe` utilitário em [caminho do utilitário de recolha de registo](#log-artifacts-path) e gera um ficheiro zip com todos os registos do azure relevantes no Olá mesma pasta.

## <a name="diagnostics-data-tables-not-found"></a>Não foram encontradas tabelas de dados de diagnóstico
tabelas de Olá no armazenamento do Azure que contém eventos ETW são denominadas utilizando Olá seguinte código:

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Segue-se um exemplo:

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
Que gera 4 tabelas:

| Evento | Nome da tabela |
| --- | --- |
| fornecedor = "prov1" &lt;id de evento = "1" /&gt; |WADEvent + MD5("prov1") + "1" |
| fornecedor = "prov1" &lt;id de evento = "2" eventDestination = "dest1" /&gt; |WADdest1 |
| fornecedor = "prov1" &lt;DefaultEvents /&gt; |WADDefault+MD5("prov1") |
| fornecedor = "prov2" &lt;DefaultEvents eventDestination = "dest2" /&gt; |WADdest2 |

## <a name="references"></a>Referências

### <a name="how-toocheck-diagnostics-extension-configuration"></a>Como toocheck configuração de extensão de diagnóstico
Olá toocheck de forma mais fácil a configuração de extensão é toonavigate toohttp://resources.azure.com, navegue toohello service virtual de nuvem ou máquina na qual Olá extensão de diagnóstico do Azure (IaaSDiagnostics / PaaDiagnostics) está em causa.

Em alternativa, ambiente de trabalho remoto na máquina de Olá e consulte o ficheiro de configuração de diagnósticos do Azure de Olá descrito na secção adequada Olá [aqui](#log-artifacts-path).

Na ou procure maiúsculas **Microsoft.Azure.Diagnostics** , em seguida, para Olá **xmlCfg** ou **WadCfg** campo. 

Em caso de máquinas virtuais, se o campo de WadCfg Olá estiver presente, significa Olá config é no JSON. Se o campo de xmlCfg Olá estiver presente, significa Olá config é em XML e é codificado em base64. Terá de demasiado[descodificar-](http://www.bing.com/search?q=base64+decoder) toosee Olá XML que foi carregada pelo diagnóstico.

Para a função de serviço em nuvem, se escolher a configuração de Olá do disco, os dados de Olá são codificação base64 pelo que terá demasiado[descodificar-](http://www.bing.com/search?q=base64+decoder) toosee Olá XML que foi carregada pelo diagnóstico.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Códigos de saída de plug-in de diagnóstico do Azure
o plug-in de Olá devolve Olá os seguintes códigos de saída:

| Código de saída | Descrição |
| --- | --- |
| 0 |Êxito. |
| -1 |Erro genérico. |
| -2 |Ficheiro de rcf Olá tooload não é possível.<p>Este erro interno só deverá acontecer se o iniciador de plug-in de agente de convidados Olá é invocada manualmente, incorretamente, num Olá VM. |
| -3 |Não é possível carregar o ficheiro de configuração de diagnósticos de Olá.<p><p>Solução: Causado por um ficheiro de configuração não passar na validação de esquema. solução de Olá é tooprovide um ficheiro de configuração que está em conformidade com o esquema de Olá. |
| -4 |Outra instância do Olá diagnóstico de agente de monitorização já está a utilizar o diretório de recursos locais de Olá.<p><p>Solução: Especifique um valor diferente para **LocalResourceDirectory**. |
| -6 |Iniciador de plug-in de agente de convidados Olá tentativa de diagnóstico de toolaunch com uma linha de comandos inválidos.<p><p>Este erro interno só deverá acontecer se o iniciador de plug-in de agente de convidados Olá é invocada manualmente, incorretamente, num Olá VM. |
| -10 |Plug-in de diagnóstico de Olá terminado com uma exceção não processada. |
| -11 |o agente convidado Olá foi processo de Olá toocreate não é possível responsável por iniciar e monitorização Olá agente de monitorização.<p><p>Solução: Verifique se os recursos de sistema suficientes disponíveis toolaunch novos processos.<p> |
| -101 |Argumentos inválidos ao chamar Olá Plug-in do diagnóstico.<p><p>Este erro interno só deverá acontecer se o iniciador de plug-in de agente de convidados Olá é invocada manualmente, incorretamente, num Olá VM. |
| -102 |o processo de plug-in de Olá é não é possível tooinitialize próprio.<p><p>Solução: Verifique se os recursos de sistema suficientes disponíveis toolaunch novos processos. |
| -103 |o processo de plug-in de Olá é não é possível tooinitialize próprio. Especificamente é objeto de registo de Olá toocreate não é possível.<p><p>Solução: Verifique se os recursos de sistema suficientes disponíveis toolaunch novos processos. |
| -104 |Não é possível tooload Olá rcf o ficheiro fornecido pelo agente de convidados Olá.<p><p>Este erro interno só deverá acontecer se o iniciador de plug-in de agente de convidados Olá é invocada manualmente, incorretamente, num Olá VM. |
| -105 |Olá Plug-in do diagnóstico não é possível abrir o ficheiro de configuração de diagnósticos de Olá.<p><p>Este erro interno só deverá acontecer se o plug-in de diagnóstico de Olá é invocada manualmente, incorretamente, num Olá VM. |
| -106 |Não é possível ler o ficheiro de configuração de diagnósticos de Olá.<p><p>Solução: Causado por um ficheiro de configuração não passar na validação de esquema. Por isso, a solução de Olá é tooprovide um ficheiro de configuração que está em conformidade com o esquema de Olá. Consulte [como toocheck configuração de extensão de diagnóstico](#how-to-check-diagnostics-extension-configuration). |
| -107 |Olá recursos diretório passagem toohello agente de monitorização é inválido.<p><p>Este erro interno só deverá acontecer se Olá agente de monitorização é invocada manualmente, incorretamente, num Olá VM.</p> |
| -108 |Não é possível tooconvert Olá diagnóstico ficheiro de configuração no ficheiro de configuração do agente de monitorização de Olá.<p><p>Este erro interno só deverá acontecer se o plug-in de diagnóstico de Olá manualmente é invocada com um ficheiro de configuração inválida. |
| -110 |Erro de configuração de diagnósticos de geral.<p><p>Este erro interno só deverá acontecer se o plug-in de diagnóstico de Olá manualmente é invocada com um ficheiro de configuração inválida. |
| -111 |Agente de monitorização de Olá toostart não é possível.<p><p>Solução: Certifique-se de que estão disponíveis recursos de sistema suficientes. |
| -112 |Erro geral |

### <a name="local-log-extraction"></a>Extração de registo de local
Olá, agente de monitorização recolhe registos e artefactos como `.tsf` ficheiros. `.tsf`o ficheiro não é legível, mas pode converter para um `.csv` da seguinte forma: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Um novo ficheiro chamado `<relevantLogFile>.csv` serão criados na Olá mesmo caminho como Olá correspondente `.tsf` ficheiro.

**Tenha em atenção**: só terá toorun este utilitário contra o ficheiro de tsf principal Olá (por exemplo, PerformanceCountersTable.tsf). Olá que acompanha os ficheiros (por exemplo, PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf etc.) automaticamente serão processados.

### <a name="more-about-trace-logs-missing"></a>Mais informações sobre os registos de rastreio em falta

**Nota:** principalmente aplica-se os serviços de toocloud só, a menos que tiver configurado Olá DiagnosticsMonitorTraceListener uma aplicação em execução na sua VM do IaaS. 

- Certifique-se de que Olá que diagnosticmonitortracelistener está configurado no Web. config de Olá ou App. config.  Este é configurado por predefinição no projetos do serviço em nuvem, mas alguns clientes comente-out que fará com que toonot de declarações de rastreio de Olá podem ser recolhidas pelo diagnóstico. 
- Se os registos não são obter escritos do método de OnStart ou execute Olá Certifique-se Olá que diagnosticmonitortracelistener consta Olá Config.  Por predefinição é em Web. config de Olá, mas que só se aplica a toocode em execução numa w3wp.exe; por isso terá no App. config toocapture rastreios em execução no WaIISHost.exe.
- Certifique-se de que está a utilizar Diagnostics.Trace.TraceXXX em vez de Diagnostics.Debug.WriteXXX.  Olá declarações de depuração serão removidas de uma versão de lançamento.
- Certifique-se de código Olá compilado tem realmente linhas de Diagnostics.Trace Olá (utilize tooverify Refletor, ildasm ou ILSpy).  Comandos Diagnostics.Trace são removidos a partir do binário de Olá compilado a menos que utilize o símbolo de compilação condicional Olá rastreio.  Se utilizar o projeto do msbuild toobuild Olá, em seguida, este é um toorun problemas comuns no.

## <a name="known-issues-and-mitigations"></a>Problemas conhecidos e atenuações
Aqui está uma lista dos problemas conhecidos com mitigações conhecidos:

**1. o .NET 4.5 dependência:**

WAD tem uma dependência de tempo de execução no framework .NET 4.5 ou superior. Momento Olá de escrever este, todas as máquinas aprovisionadas para serviços em nuvem, bem como todos os oficiais do azure base imagens da Máquina Virtual tem o .NET 4.5 ou superior instalado. É possível ainda contudo tooland numa situação em que tenta toorun WAD num computador que não tem o .NET 4.5 ou superior. Isto acontece quando criar a sua máquina retire uma imagem do antiga ou instantâneo; ou colocar o seu próprio disco personalizado.

Isto geralmente manifestos como um código de saída **255** quando em execução DiagnosticsPluginLauncher.exe. Falha de acontece devido a exceção de toohello não processada: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Atenuação:** instalar o .NET 4.5 ou superior no seu computador.

**2. Dados de contadores de desempenho disponíveis no armazenamento, mas não é possível mostrar no portal**

Experiência do portal de máquinas virtuais mostra alguns contadores de desempenho por predefinição. Se não VI-los e sabe dados Olá é gerados porque se encontra disponível em armazenamento. Verifique:
- Se os dados no armazenamento Olá tem nomes de contador em inglês. Se os nomes de contador Olá não estão em inglês, gráfico de métrico portal não será capaz de toorecognize-lo.
- Se estiver a utilizar os carateres universais (\*) nos nomes de contador de desempenho, portal Olá não será capaz de toocorrelate Olá configurado e recolhidos contador.

**Mitigação**: alterar tooEnglish de idioma da máquina de Olá para contas de sistema. Painel de controlo -> região -> Administração -> definições de cópia -> desmarque "de boas-vindas do ecrã e o sistema de contas", para que o idioma personalizado Olá não é aplicada toosystem conta. Certifique-se também que não utilizar os carateres universais se pretender que o portal toobe sua experiência de consumo primário.
