---
title: "aaaUsing Elasticsearch como um arquivo de rastreio de aplicação de Service Fabric | Microsoft Docs"
description: "Descreve como aplicações de Service Fabric podem utilizar toostore Elasticsearch e Kibana, índice e pesquisa através de rastreios de aplicações (registos)"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Armazenar Elasticsearch utilização como um rastreio de aplicação de Service Fabric
## <a name="introduction"></a>Introdução
Este artigo descreve como [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) as aplicações podem utilizar **Elasticsearch** e **Kibana** para armazenamento de aplicação de rastreio, a indexação e pesquisa. [Elasticsearch](https://www.elastic.co/guide/index.html) é um open source, distribuída e escalável em tempo real de procura e análise motor que é adequada para esta tarefa. Pode ser instalado no Windows e Linux máquinas de virtuais em execução no Microsoft Azure. Elasticsearch eficientemente pode processar *estruturados* rastreios produzidos utilizando tecnologias como **rastreio de eventos para o Windows (ETW)**.

ETW é utilizado pelo Service Fabric runtime toosource informações de diagnóstico (rastreios). É Olá recomendado demasiado as respetivas informações de diagnóstico de método para toosource de aplicações de Service Fabric. Utilizar Olá mesmo mecanismo permite a correlação entre os rastreios fornecido pelo runtime e fornecido por aplicação e torna mais fácil de resolução de problemas. Modelos de projeto de Service Fabric no Visual Studio incluem uma API de registo (com base no Olá .NET **EventSource** classe) que emite rastreios ETW por predefinição. Para obter uma descrição geral da aplicação de Service Fabric de rastreio utilizando a ETW, consulte o artigo [monitorização e diagnosticar os serviços de uma configuração de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Para os rastreios de Olá tooshow cópias de segurança no Elasticsearch, necessitam de toobe capturada em nós de cluster do Service Fabric Olá em tempo real (durante a execução da aplicação Olá) e enviados tooan Elasticsearch endpoint. Existem duas opções principais para capturar o rastreio:

* **Dentro do processo rastreio capturar**  
  aplicação Olá ou mais precisamente, processo de serviço, é responsável pelo envio de arquivo de rastreio de toohello Olá dados de diagnóstico (Elasticsearch).
* **Capturar fora do processo rastreio**  
  Um agente separado é capturar rastreios de processo do serviço de Olá ou os processos e enviando-as toohello arquivo de rastreio.

Abaixo, iremos descrevem como tooset segurança Elasticsearch no Azure, analisam os profissionais de Olá e contras para ambos capturar as opções e explicam como tooconfigure uma infraestrutura de serviço service toosend tooElasticsearch de dados.

## <a name="set-up-elasticsearch-on-azure"></a>Configurar Elasticsearch no Azure
Olá tooset de forma mais simples serviço de Elasticsearch Olá no Azure é efetuada através de [ **modelos Azure Resource Manager**](../azure-resource-manager/resource-group-overview.md). Um abrangentes [modelo de início rápido do Azure Resource Manager para Elasticsearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) está disponível a partir do repositório de modelos de início rápido do Azure. Este modelo utiliza contas de armazenamento separada para unidades de escala (grupos de nós). Também pode aprovisionar cliente separado e nós de servidor com configurações diferentes e vários números de discos de dados ligados.

Aqui, utilizamos o modelo de outro, denominado **ES MultiNode** de Olá [repositório de ferramentas de diagnóstico do Azure](https://github.com/Azure/azure-diagnostics-tools). Este modelo é mais fácil toouse e cria um cluster de Elasticsearch protegido através da autenticação básica de HTTP. Antes de continuar, transfira repositório Olá a partir do GitHub tooyour máquina (através da clonagem repositório Olá ou transferir um ficheiro zip). modelo de Olá ES MultiNode está localizado na pasta de Olá com Olá mesmo nome.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Preparar uma máquina toorun Elasticsearch scripts de instalação
Olá modelo de Olá MultiNode de ES de toouse de forma mais fácil é através de um script do PowerShell do Azure fornecido chamado `CreateElasticSearchCluster`. toouse este script, terá de módulos do PowerShell tooinstall e uma ferramenta chamado **openssl**. Olá esta última opção é necessária para criar uma chave SSH que pode ser utilizado tooadminister Elasticsearch cluster remotamente.

`CreateElasticSearchCluster`script foi concebido para facilidade de utilização com o modelo de Olá MultiNode de ES de um computador Windows. É possível toouse Olá modelo numa máquina não sejam Windows, mas esse cenário ultrapassa o âmbito Olá deste artigo.

1. Se ainda não instalou-los já, instalar [ **módulos do Azure PowerShell**](http://aka.ms/webpi-azps). Quando lhe for pedido, clique em **executar**, em seguida, **instalar**. O Azure PowerShell 1.3 ou mais recente é necessário.
2. Olá **openssl** ferramenta está incluída no distribuição Olá [ **Git para Windows**](http://www.git-scm.com/downloads). Se ainda não o tiver o feito, instale [Git para Windows](http://www.git-scm.com/downloads) agora. (opções de instalação predefinido Olá estão OK).
3. Partindo do princípio que Git tem sido instalado, mas não incluído no caminho do sistema de Olá, abra uma janela do Microsoft Azure PowerShell e execute Olá os seguintes comandos:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Substitua Olá `<Git installation folder>` com a localização do Git Olá no seu computador; é a predefinição de Olá **"C:\Programas\Microsoft Files\Git"**. Tenha em atenção o caráter de ponto e vírgula Olá início Olá do caminho primeiro Olá.
4. Certifique-se de que tem sessão iniciada no tooAzure (através de [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) e que selecionou subscrição Olá que deve ser utilizadas toocreate o cluster de pesquisa elástico. Pode verificar que subscrição correta está selecionada utilizar `Get-AzureRmContext` e `Get-AzureRmSubscription` cmdlets.
5. Se não tiver o feito, altere pasta Olá para toohello MultiNode de ES de diretório atual.

### <a name="run-hello-createelasticsearchcluster-script"></a>Executar script de CreateElasticSearchCluster Olá
Antes de executar o script de Olá, abra Olá `azuredeploy-parameters.json` de ficheiros e certifique-se ou forneça valores para parâmetros do script Olá. é fornecida Olá os seguintes parâmetros:

| Nome do Parâmetro | Descrição |
| --- | --- |
| dnsNameForLoadBalancerIP |nome de Olá que é utilizado toocreate Olá publicamente visível nome do DNS para o cluster de pesquisa elástico Olá (acrescentando nome de toohello fornecido de domínio do Olá região do Azure). Por exemplo, se este valor do parâmetro é "myBigCluster" e a região do Azure Olá escolhido está EUA oeste, o nome DNS resultante Olá para cluster Olá é myBigCluster.westus.cloudapp.azure.com. <br /><br />Este nome também serve como um nome de raiz para muitos artefactos associados ao cluster de pesquisa elástico Olá, tais como nomes de nó de dados. |
| adminUsername |nome de Olá da conta de administrador Olá para gerir o cluster de pesquisa elástico Olá (correspondentes chaves de SSH são geradas automaticamente). |
| dataNodeCount |número de Olá de nós no cluster de pesquisa elástico Olá. versão atual do Olá do script Olá não distinguir entre os nós de dados e consulta; todos os nós reproduzir ambas as funções. As predefinições too3 nós. |
| dataDiskSize |tamanho de Olá de discos de dados (em GB) que está alocado para cada nó de dados. Cada nó recebe 4 discos de dados, exclusivamente dedicado tooElastic serviço de pesquisa. |
| Região |nome de Olá da região do Azure onde o cluster de pesquisa elástico Olá deve estar localizado. |
| esUserName |Olá nome de utilizador do utilizador Olá que é configurado toohave-cluster acesso tooES (requerente tooHTTP a autenticação básica). Olá palavra-passe não faz parte do ficheiro de parâmetros e tem de ser fornecido quando `CreateElasticSearchCluster` script é invocado. |
| vmSizeDataNodes |Olá, tamanho de máquina virtual do Azure para nós de cluster de pesquisa elástico. As predefinições tooStandard_D2. |

Agora, está pronto toorun script de Olá. Emitir Olá os seguintes comandos:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

onde 

| Nome do parâmetro de script | Descrição |
| --- | --- |
| `<es-group-name>` |nome de Olá Olá do Azure do grupo de recursos que irá conter todos os recursos de cluster de pesquisa elástico. |
| `<azure-region>` |nome de Olá do Olá região do Azure onde o cluster de pesquisa elástico Olá deve ser criado. |
| `<es-password>` |Olá palavra-passe para o utilizador de pesquisa elástico Olá. |

> [!NOTE]
> Se obtiver um NullReferenceException do cmdlet Olá teste-AzureResourceGroup, ter esquecimento toolog no tooAzure (`Add-AzureRmAccount`).
> 
> 

Se obtiver um erro ao executar o script de Olá e determinar a que o erro de Olá foi causado por um valor de parâmetro de modelo errado, corrija o ficheiro de parâmetros de Olá e execute o script Olá novamente com um nome de grupo de recursos diferente. Também pode reutilizar Olá o mesmo nome de grupo de recursos e ter o script de Olá limpar Olá antigo adicionando Olá `-RemoveExistingResourceGroup` invocação de script de toohello de parâmetro.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Resultado da execução de script de CreateElasticSearchCluster Olá
Depois de executar Olá `CreateElasticSearchCluster` script, Olá seguir artefactos principais será criada. Para este exemplo partimos do princípio que utiliza o "myBigCluster" como valor Olá Olá `dnsNameForLoadBalancerIP` parâmetro e nessa região olá onde criou o cluster de Olá é EUA oeste.

| Artefactos | Nome, a localização e comentários |
| --- | --- |
| Chave SSH para a administração remota |ficheiro de myBigCluster.key (no diretório de Olá do qual Olá CreateElasticSearchCluster foi executado). <br /><br />Este ficheiro de chave pode ser utilizados tooconnect toohello admin nó e (através do nó de admin Olá) toodata nós num cluster de Olá. |
| Nó de Admin |myBigCluster admin.westus.cloudapp.azure.com <br /><br />Uma VM dedicada para administração remota do cluster Elasticsearch – Olá apenas um que permite ligações externas de SSH. Este é executado num Olá does da mesma rede virtual que todos os nós de cluster Elasticsearch Olá, mas não execute todos os serviços Elasticsearch. |
| Nós de dados |myBigCluster1... myBigCluster*N* <br /><br />Nós de dados que estejam a executar serviços Elasticsearch e Kibana. Pode ligar através de SSH tooeach nó, mas apenas através de nó de admin Olá. |
| Elasticsearch cluster |http://myBigCluster.westus.cloudapp.Azure.com/es/ <br /><br />Olá primário ponto final para o cluster de Elasticsearch Olá (sufixo de /es de Olá nota). É protegida pela autenticação HTTP básica (credenciais Olá foram Olá especificado esUserName/esPassword parâmetros de modelo de Olá ES MultiNode). cluster de Olá tem também Olá head Plug-in instalado (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) para a administração de cluster básico. |
| Serviço de Kibana |http://myBigCluster.westus.cloudapp.Azure.com <br /><br />Olá Kibana serviço está definida tooshow dados de Olá criado Elasticsearch cluster. É protegida pela Olá mesmas credenciais de autenticação como Olá cluster em si. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>Em processo versus fora do processo rastreio capturar
Na introdução de Olá, iremos mencionado duas formas fundamentais de recolha de dados de diagnóstico: dentro do processo e fora do processo. Cada um tem força da codificação e fragilidades.

Vantagens de Olá **dentro do processo rastreio capturar** incluem:

1. *Fácil configuração e implementação*
   
   * configuração de Olá de recolha de dados de diagnóstico é apenas fazem parte da configuração da aplicação Olá. É fácil tooalways a mantê-lo "sincronizadas" com Olá rest da aplicação Olá.
   * É fácil alcançável por aplicação ou serviço a configuração.
   * Normalmente, fora do processo rastreio capturar requer uma implementação separada e de configuração do agente diagnóstico Olá, que é uma tarefa extra administrativa e uma origem de potencial erros. tecnologia de agente específico de Olá, muitas vezes, permite apenas uma instância do agente de Olá por máquina virtual (nó). Isto significa que a configuração para a coleção de Olá da configuração de diagnóstico Olá é partilhada entre todas as aplicações e serviços em execução nesse nó.
2. *Flexibilidade*
   
   * Olá aplicação pode enviar dados Olá sempre que é necessário toogo, desde que não há uma biblioteca de cliente que suporta o sistema de armazenamento de dados de Olá visada. Nova sinks podem ser adicionados como pretendido.
   * Regras de captura, filtragem e agregação de dados complexas podem ser implementadas.
   * Capturar um rastreio de fora do processo, muitas vezes, é limitada pela Olá dados sinks que Olá suporta do agente. Alguns agentes são extensíveis.
3. *Aceder aos dados de aplicação de toointernal e contexto*
   
   * o subsistema de diagnóstico Olá em execução dentro do processo de serviço/aplicação Olá facilmente pode aumentar os rastreios de Olá com nível contextual das informações.
   * Abordagem, fora do processo de Olá, Olá devem ser enviados dados agente tooan através de algum mecanismo de comunicação entre processos, por exemplo, o rastreio de eventos para o Windows. Este mecanismo foi impõe limitações adicionais.

Vantagens de Olá **fora do processo rastreio capturar** incluem:

1. *Olá capacidade toomonitor Olá aplicações e recolher informações de falhas*
   
   * Capturar dentro do processo rastreio pode ser bem-sucedido se aplicação Olá falha toostart ou falhas. Um agente independente tem muito melhor oportunidade de captura fundamentais informações de resolução de problemas.<br /><br />
2. *Maturidade, robustez e desempenho comprovado*
   
   * Um agente desenvolvido por um fornecedor de plataforma (por exemplo, um agente do Microsoft Azure Diagnostics) foi requerente toorigorous luta proteção e de teste.
   * Com dentro do processo rastreio capturar, deve ter cuidado tooensure atividade Olá de envio de dados de diagnóstico de um processo de aplicação não interfere com tarefas principal da aplicação Olá ou apresentar problemas de temporização ou desempenho. Um agente de forma independente em execução é menos propenso problemas de toothese e está especificamente concebida toolimit respetivo impacto nos sistema Olá.

É possível toocombine e o benefício de ambas as abordagens. Realmente, poderá ser melhor solução de Olá para muitas aplicações.

Aqui, utilizamos Olá **Microsoft.Diagnostic.Listeners biblioteca** e Olá dentro do processo rastreio capturar os dados de toosend de um cluster de Elasticsearch de tooan de aplicação de Service Fabric.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Utilizar Olá os serviços de escuta biblioteca toosend dados de diagnóstico tooElasticsearch
biblioteca de Microsoft.Diagnostic.Listeners Olá faz parte de PartyCluster exemplo de aplicação de Service Fabric. toouse-lo:

1. Transferir [exemplo de PartyCluster Olá](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) a partir do GitHub.
2. Copiar Olá Microsoft.Diagnostics.Listeners Microsoft.Diagnostics.Listeners.Fabric projetos e (todo pastas) do Olá PartyCluster exemplo toohello solução pasta de diretório da aplicação Olá que deveria toosend Olá dados tooElasticsearch .
3. Abrir a solução de destino Olá, clique no nó de solução Olá Olá Explorador de soluções e escolha **adicionar projeto existente**. Adicione a solução de toohello Olá Microsoft.Diagnostics.Listeners projeto. Repetir Olá mesmo para o projeto de Microsoft.Diagnostics.Listeners.Fabric Olá.
4. Adicione uma referência de projecto da sua project(s) toohello dois adicionado projetos do serviço. (Cada serviço que deveria toosend dados tooElasticsearch deverá referenciar Microsoft.Diagnostics.EventListeners e Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![TooMicrosoft.Diagnostics.EventListeners de referências do projeto e bibliotecas de Microsoft.Diagnostics.EventListeners.Fabric][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Versão de disponibilidade geral de recursos de infraestrutura de serviço e o pacote Microsoft.Diagnostics.Tracing Nuget
As aplicações criadas com o lançamento de disponibilidade geral de recursos de infraestrutura de serviço (2.0.135, lançada 31 de Março de 2016) destino **.NET Framework 4.5.2**. Esta versão é a versão mais recente do Olá de Olá suportado pelo Azure no momento de Olá da versão de Olá GA do .NET Framework. Infelizmente, esta versão do framework Olá não possui determinadas APIs EventListener esse Olá Microsoft.Diagnostics.Listeners tem de biblioteca. Como são fortemente conjugados EventSource (componente de Olá base Olá de APIs de início de sessão em aplicações de recursos de infraestrutura de formulários) e EventListener, cada projeto que utiliza Olá Microsoft.Diagnostics.Listeners biblioteca tem de utilizar uma implementação alternativa de EventSource. Esta implementação é fornecida pela Olá **pacote Microsoft.Diagnostics.Tracing Nuget**, criados pela Microsoft. pacote de Olá é totalmente retrocompatível com EventSource incluído no framework Olá, pelo que não existem alterações de código devem ser necessárias que não sejam alterações de espaço de nomes referenciado.

toostart utilizando Olá Microsoft.Diagnostics.Tracing implementação da classe de EventSource Olá, siga estes passos para cada projeto de serviço que necessita de toosend dados tooElasticsearch:

1. Clique com o botão direito no projeto de serviço Olá e escolha **gerir pacotes Nuget**.
2. Comutador toohello nuget.org origem do pacote (se não estiver já selecionada) e procure "**Microsoft.Diagnostics.Tracing**".
3. Instalar Olá `Microsoft.Diagnostics.Tracing.EventSource` pacote (e as respetivas dependências).
4. Abra Olá **ServiceEventSource.cs** ou **ActorEventSource.cs** de ficheiros no seu projeto de serviço e substitua Olá `using System.Diagnostics.Tracing` directiva em cima de ficheiros de Olá com Olá `using Microsoft.Diagnostics.Tracing` diretiva.

Estes passos não será necessários uma vez Olá **.NET Framework 4.6** é suportada pelo Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>As instâncias de serviço de escuta de Elasticsearch e a configuração
Olá passo final para enviar dados de diagnóstico tooElasticsearch é toocreate uma instância de `ElasticSearchListener` e configurá-lo com dados de ligação de Elasticsearch. serviço de escuta de Olá captura automaticamente todos os eventos gerados através de classes de EventSource definidas no projeto de serviço Olá. Tem de toobe alive durante a duração de Olá do serviço de Olá, para Olá melhor colocar toocreate está no código de inicialização do serviço de Olá. Eis como o código de inicialização de Olá para um serviço sem monitorização de estado foi apresentada depois das alterações necessárias Olá (adições indicada nos comentários começadas `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Dados de ligação de Elasticsearch devem ser colocados numa secção separada no ficheiro de configuração do serviço de Olá (**PackageRoot\Config\Settings.xml**). nome de Olá da secção de Olá tem de corresponder valor toohello transmitido toohello `FabricConfigurationProvider` construtor, por exemplo:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Olá valores de `serviceUri`, `userName` e `password` correspondem endereço de ponto final de cluster de Elasticsearch toohello, Elasticsearch nome de utilizador e palavra-passe, respetivamente. `indexNamePrefix`é o prefixo de Olá para índices de Elasticsearch; biblioteca de Microsoft.Diagnostics.Listeners Olá cria um novo índice para os respetivos dados diariamente.

### <a name="verification"></a>Verificação
Já está! Agora, sempre que é executado o serviço de Olá, começa a enviar serviço de Elasticsearch rastreios toohello especificado na configuração de Olá. Pode verificar isto, Olá de abertura que kibana IU associada à instância de Elasticsearch de destino Olá. No nosso exemplo, o endereço de página Olá é http://myBigCluster.westus.cloudapp.azure.com/. Verifique se indexa com o prefixo de nome de Olá escolhido para Olá `ElasticSearchListener` instância, de facto, tiverem sido criados e preenchida com dados.

![Mostrar Kibana PartyCluster eventos da aplicação][2]

## <a name="next-steps"></a>Passos seguintes
* [Saber mais sobre como diagnosticar e monitorizar um serviço do Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
