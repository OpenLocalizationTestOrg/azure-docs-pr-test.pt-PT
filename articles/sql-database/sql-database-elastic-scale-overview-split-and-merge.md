---
title: aaaMoving dados entre bases de dados de nuvem de escalamento horizontal | Microsoft Docs
description: "Explica como toomanipulate shards e mover dados através de um serviço alojado automática utilizando elástico da base de dados APIs."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>Mover dados entre bases de dados de nuvem aumentadas horizontalmente
Se for um Software como um programador de serviço e subitamente a sua aplicação sofre a pedido imenso, terá de crescimento de Olá tooaccommodate. Para adicionar mais bases de dados (shards). Como redistribuir Olá dados toohello novas bases de dados sem perturbar a integridade dos dados de Olá? Olá utilize **ferramenta de intercalação de divisão** dados toomove restrita toohello novas bases de dados de bases de dados.  

ferramenta de intercalação de divisão de Olá é executada como um serviço web do Azure. Um administrador ou programador utiliza Olá ferramenta toomove shardlets (dados a partir de um ID de partição horizontal) entre bases de dados diferentes (shards). ferramenta de Olá utiliza partições horizontais mapa gestão toomaintain Olá serviço metadados da base de dados e certifique-se consistente mapeamentos.

![Descrição geral][1]

## <a name="download"></a>Transferência
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>Documentação
1. [Tutorial de ferramenta de intercalação de divisão de base de dados elástica](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Configuração de segurança de divisão de intercalação](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [Considerações de segurança de divisão de intercalação](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [Gestão de mapas de partições horizontais](sql-database-elastic-scale-shard-map-management.md)
5. [Migrar tooscale-out de bases de dados existente](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [Ferramentas de base de dados elástica](sql-database-elastic-scale-introduction.md)
7. [Glossário de ferramentas de base de dados elástico](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>Porquê utilizar a ferramenta de intercalação de divisão de Olá?
**Flexibilidade**

As aplicações precisam de toostretch flexivelmente se para além dos limites de Olá de uma única base de dados de BD SQL do Azure. Utilize dados de toomove Olá ferramenta como toonew necessários bases de dados, mantendo o integridade.

**Dividir toogrow** 

Terá de tooincrease geral crescimento explosive de toohandle de capacidade. toodo, crie capacidade adicional por dados de Olá de fragmentação e distribui-lo em bases de dados de forma incremental mais até que as necessidades de capacidade são verdadeiras. Este é um exemplo de prime Olá 'Dividir' funcionalidade. 

**Intercalar tooshrink**

Capacidade tem de reduzir devido toohello natureza sazonais de uma empresa. Olá ferramenta permite, reduzir verticalmente unidades de escala toofewer quando abrandar de negócio. funcionalidade de 'merge' Olá no Olá serviço de intercalação de divisão do dimensionamento elástico aborda este requisito. 

**Gerir hotspots movendo shardlets**

Com múltiplos inquilinos por base de dados, alocação de Olá de shardlets tooshards pode levar toocapacity constrangimentos no algumas shards. É necessário voltar a atribuir shardlets ou movendo toonew shardlets ocupado ou menos shards sobreutilizados. 

## <a name="concepts--key-features"></a>Conceitos e as principais funcionalidades
**Serviços alojados de cliente**

Olá divisão-intercalação é fornecida como um serviço alojado de cliente. Tem de implementar e alojar o serviço de Olá na sua subscrição do Microsoft Azure. pacote de Olá, transferir a partir do NuGet contém um toocomplete de modelo de configuração com as informações de Olá para a sua implementação específica. Consulte Olá [tutorial de divisão de intercalação](sql-database-elastic-scale-configure-deploy-split-and-merge.md) para obter mais detalhes. Uma vez que o serviço de Olá é executado na sua subscrição do Azure, pode controlar e configurar a maioria dos aspetos de segurança do serviço de Olá. modelo predefinido de Olá inclui Olá opções tooconfigure SSL, autenticação de cliente baseada em certificados, a encriptação de credenciais armazenadas, DoS guarding e restrições de IP. Pode encontrar mais informações sobre Olá aspetos de segurança no Olá seguinte documento [configuração de segurança de divisão de intercalação](sql-database-elastic-scale-split-merge-security-configuration.md).

predefinição de Olá implementado execuções de serviço com um trabalho e uma função da web. Cada utiliza o tamanho da A1 VM de Olá na Cloud Services do Azure. Enquanto que não pode modificar estas definições quando implementar o pacote de Olá, pode alterá-los após uma implementação com êxito no Olá a executar o serviço em nuvem, (através do portal do Azure Olá). Tenha em atenção de que essa função de trabalho Olá não deve ser configurada para a mais do que uma única instância por motivos de técnicos. 

**Integração de mapa de partições horizontais**

serviço de intercalação de divisão de Olá interage com o mapa de partições horizontais Olá da aplicação Olá. Quando utilizar toosplit do serviço de intercalação de divisão de Olá ou intervalos de intercalação ou toomove shardlets entre shards, o serviço de Olá mantém automaticamente Olá mapa de partições horizontais se toodate. toodo por isso, o serviço de Olá liga toohello partições horizontais mapa Gestor da base de dados da aplicação Olá e mantém intervalos e mapeamentos como progresso de divisão/intercalação/mover pedidos. Isto garante que mapa de partições horizontais Olá apresenta sempre uma vista atualizada quando são acontecimentos operações de intercalação de divisão. As operações de movimento de intercalação e shardlet dividir, são implementadas por mover um lote de shardlets de partições horizontais partições horizontais Olá origem toohello destino. Durante a Olá shardlet movimento operação Olá shardlets requerente toohello lote atual está marcada como offline no mapa de partições horizontais Olá e está disponível para ligações de encaminhamento de dados dependentes utilizando Olá **OpenConnectionForKey** API. 

**Ligações de shardlet consistente**

Quando é iniciado o movimento de dados para um lote novo de shardlets, qualquer mapa de partições horizontais fornecido dados dependentes encaminhamento ligações toohello partições horizontais armazenar Olá shardlet são desativadas e subsequentes ligações do mapa de partições horizontais Olá toohello APIs estes shardlets estão bloqueadas enquanto movimento de dados de Olá está em curso no inconsistências tooavoid de ordem. Ligações tooother shardlets no Olá partições horizontais mesmo também irão obter desativados, mas serão concluída com êxito novamente imediatamente da repetição. Depois de batch de Olá for movido, Olá shardlets estão marcados online novamente para partições horizontais de destino Olá e dados de origem Olá são removidos do Olá origem de partição horizontal. serviço de Olá atravessa estes passos para cada lote até que todos os shardlets terem sido movidos. Isto irá originar a operações de eliminação de ligação tooseveral decorrer Olá de concluir a operação intercalação/divisão/movimentação Olá.  

**Gerir a disponibilidade de shardlet**

Limitar a ligação de Olá o cancelamento toohello lote atual de shardlets conforme mencionado acima restringe o âmbito de Olá do lote de tooone de indisponibilidade de shardlets cada vez. Isto é preferencial através de uma abordagem onde partições horizontais completa de Olá permanecerá offline para todos os respetivos shardlets Olá durante uma operação de intercalação ou divisão. tamanho de Olá do batch, definido como número de Olá de shardlets distintos toomove cada vez, é um parâmetro de configuração. Pode ser definido para cada operação de divisão e intercalação consoante as necessidades de disponibilidade e o desempenho da aplicação Olá. Tenha em atenção que o intervalo de Olá que está a ser bloqueado no mapa de partições horizontais Olá pode ser superior ao tamanho de lote de Olá especificado. Isto acontece porque o serviço de Olá escolhe o tamanho do intervalo de Olá, de forma a que o número real de Olá dos valores de chave de fragmentação nos dados de Olá aproximadamente corresponde ao tamanho do lote Olá. Isto é importante tooremember em particular para chaves de fragmentação sparsely povoada. 

**Armazenamento de metadados**

serviço de intercalação de divisão de Olá utiliza um toomaintain de base de dados, o estado e tookeep registos durante o processamento do pedido. utilizador Olá cria esta base de dados na sua subscrição e fornece a cadeia de ligação de Olá-lo no ficheiro de configuração de Olá para implementação do serviço Olá. Os administradores da organização do utilizador Olá também podem ligar toothis tooinvestigate e o progresso de pedido de tooreview de base de dados informações sobre potenciais falhas de detalhado.

**Deteção de fragmentação**

serviço de intercalação de divisão de Olá distingue entre (1) a tabelas, as tabelas de referência (2) e (3) normais tabelas. semântica de Olá de uma operação de intercalação/divisão/movimentação dependem do tipo Olá da tabela de Olá utilizado e é definida do seguinte modo: 

* **Tabelas em partição horizontal**: as operações de movimentação, intercalação e divisão movem shardlets de partições horizontais tootarget de origem. Após a conclusão bem-sucedida da Olá pedir global, esses shardlets já não estão presentes na origem de Olá. Tenha em atenção que as tabelas de destino Olá têm tooexist em partição horizontal de destino Olá e não pode conter os dados no Olá destino intervalo tooprocessing anterior da operação de Olá. 
* **As tabelas de referência**: as tabelas de referência, divisão Olá, intercalar e mover operações copiar dados de Olá de Olá origem toohello destino ID de partição horizontal. Tenha em atenção, no entanto, de que nenhuma alteração ocorre em partição horizontal do destino de Olá para uma determinada tabela se qualquer linha já se encontra presente nesta tabela no destino Olá. a tabela de Olá tem toobe vazia para qualquer referência tabela cópia operação tooget processado.
* **Outras tabelas**: outras tabelas podem estar presentes no Olá origem ou destino de Olá de uma operação de divisão e intercalação. serviço de intercalação de divisão de Olá disregards estas tabelas para o movimento de dados ou operações de cópia. Tenha em atenção, no entanto, que pode interferir com estas operações em caso de restrições.

informações de Olá numa referência vs tabelas em partição horizontal são fornecidas pelo Olá **SchemaInfo** APIs no mapa de partições horizontais Olá. Olá seguinte o exemplo ilustra a utilização de Olá destas APIs numa determinada partição horizontal mapa manager objeto smm: 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

Olá tabelas 'region' e 'nation' estão definidas como tabelas de referência e serão copiados com operações de divisão/intercalação/mover. 'Cliente' e 'ordens' por sua vez são definidas como tabelas em partição horizontal. C_CUSTKEY e O_CUSTKEY servem como chave de fragmentação Olá. 

**Integridade referencial**

o serviço de intercalação de divisão de Olá analisa as dependências entre tabelas e utiliza as operações de Olá toostage relações de chave primária de chave externa para mover as tabelas de referência e shardlets. Em geral, as tabelas de referência são copiadas primeiro por ordem de dependência, em seguida, shardlets são copiados por ordem das respetivas dependências em cada lote. Isto é necessário para que as restrições de FK-PK em partição horizontal de destino Olá são cumpridas como dados novos Olá chega. 

**Consistência de mapa de partições horizontais e Eventual conclusão**

Na presença de Olá de falhas, o serviço de intercalação de divisão de Olá retoma operações após qualquer falha e visa toocomplete qualquer nos pedidos de progresso. No entanto, poderão existir situações irrecuperáveis, por exemplo, quando Olá destino ID de partição horizontal for roubado ou comprometido para além de reparação. Esses circunstâncias, alguns shardlets que foram deveria toobe movido podem continuar tooreside no Olá origem de partição horizontal. serviço Olá garante que os mapeamentos de shardlet apenas são atualizados após Olá necessário dos dados copiados com êxito toohello destino. Shardlets apenas são eliminados na origem de Olá depois de todos os seus dados tem sido copiados toohello destino e mapeamentos correspondente Olá foram atualizados com êxito. operação de eliminação de Olá ocorre em segundo plano de Olá enquanto o intervalo de Olá já se encontra online em partição horizontal de destino Olá. serviço de intercalação de divisão de Olá garante sempre correcção de mapeamentos de Olá armazenados no mapa de partições horizontais Olá.

## <a name="hello-split-merge-user-interface"></a>interface de utilizador de intercalação de divisão de Olá
pacote de serviço de intercalação de divisão de Olá inclui uma função de trabalho e uma função da web. função da web Olá é utilizado toosubmit pedidos de divisão de intercalação de uma forma interativa. componentes principais do Olá de interface de utilizador Olá são os seguintes:

* Tipo de operação: o tipo de operação de Olá é um botão de opção que controla o tipo de Olá da operação efetuada pelo serviço de Olá para este pedido. Pode escolher entre divisão Olá, intercalar e mover cenários. Também pode cancelar uma operação anteriormente submetida. Pode utilizar a divisão, intercalar e mover pedidos para o intervalo de partição horizontal maps. ID de partição horizontal lista mapeia apenas operações de movimentação de suporte.
* Mapa de partições horizontais: Olá seguinte secção pedido parâmetros abrange informações sobre o mapa de partições horizontais Olá e base de dados de Olá que aloja o mapa de partições horizontais. Em particular, terá de nome de Olá tooprovide do servidor de base de dados do Azure SQL Olá e Olá shardmap de alojamento de base de dados, credenciais tooconnect toohello ID de partição horizontal mapear a base de dados e Olá, finalmente, o nome do mapa de partições horizontais Olá. Atualmente, a operação de Olá só aceita um único conjunto de credenciais. Estas credenciais têm permissões suficientes toohave tooperform altera o mapa de partições horizontais toohello, bem como os dados do utilizador toohello no shards Olá.
* Intervalo de origem (de divisão e intercalação): uma operação de divisão e intercalação processa um intervalo utilizando a respetiva chave baixa e alta. toospecify uma operação com um unbounded elevado valor de chave, verificação Olá "chave superior é máximo" da caixa de verificação e deixe o campo de chave elevada Olá em branco. Olá intervalo valores de chave que especificou não não corresponde a necessidade de tooprecisely um mapeamento e os respetivos limites no seu mapa de partições horizontais. Se não especificar quaisquer limites de intervalo em todos os serviço Olá irá inferir intervalo mais próximo Olá por si automaticamente. Pode utilizar Olá GetMappings.ps1 PowerShell script tooretrieve Olá atuais mapeamentos de um mapa de partições horizontais indicado.
* Comportamento de origem de divisão (divisão): para operações de divisão, definir o intervalo de origem do Olá ponto toosplit Olá. Para tal, fornecendo a chave de fragmentação olá onde pretende Olá divide toooccur. Botão de opção utilizar Olá Especifique se pretende Olá inferior parte Olá toomove de intervalo (excluindo Olá dividir a chave) ou se pretende Olá parte superior toomove (incluindo Olá divisão chave).
* Origem Shardlet (mover): operações são diferentes da divisão de mover ou operações de intercalação não necessitam de uma origem de Olá toodescribe intervalo. Uma origem para mover simplesmente identificada pelo valor da chave de fragmentação Olá que planeia toomove.
* Destino de partições horizontais (divisão): uma vez que forneceu informações de Olá na origem de Olá da operação de divisão, terá de toodefine onde pretende Olá dados toobe copiados tooby com servidor de BD SQL do Azure de Olá e nome de base de dados para o destino de Olá.
* Intervalo de destino (intercalação): operações de intercalação mover shardlets tooan existente ID de partição horizontal. Identificar o ID de partição horizontal existente Olá fornecendo limites de intervalo de Olá do intervalo existente Olá que pretende que sejam toomerge com.
* Tamanho do lote: controlos de tamanho de lote Olá Olá diversas shardlets passará offline num momento durante o movimento de dados de Olá. Este é um valor inteiro em que pode utilizar valores mais pequenos quando são toolong confidenciais períodos de indisponibilidade para shardlets. Valores maiores aumentará Olá tempo de um determinado shardlet mas offline poderão melhorar o desempenho.
* Id da operação (Cancelar): Se tiver uma operação em curso que não são necessários, pode cancelar a operação de Olá ao fornecer o respetivo ID de operação neste campo. Pode obter o ID de operação de Olá da tabela de estado de pedido de Olá (consulte a secção 8.1) ou da saída de Olá no browser olá onde submeter o pedido de Olá.

## <a name="requirements-and-limitations"></a>Requisitos e limitações
implementação atual do Olá do serviço de intercalação de divisão de Olá é requerente toohello os seguintes requisitos e limitações: 

* shards Olá necessário tooexist e estar registados no mapa de partições horizontais Olá antes de uma operação de intercalação de divisão nestes shards pode ser efetuada. 
* serviço de Olá não criar tabelas ou outros objetos de base de dados automaticamente como parte das suas operações. Isto significa que Olá esquema para a todas as tabelas e tabelas de referência tem tooexist de operação de intercalação/divisão/movimentação do Olá destino partições horizontais tooany anterior. Tabelas em partição horizontal em particular são necessária toobe vazio no intervalo de olá onde shardlets novo são toobe adicionado por uma operação de intercalação/divisão/mover. Caso contrário, a operação de Olá falhará verificação de consistência inicial Olá Olá destino ID de partição horizontal. Tenha em atenção que os dados de referência só foi copiados esteja tabela de referência de Olá vazia e que não existem nenhum consistência ação garante também com operações de escrita simultâneos tooother regard em tabelas de referência de Olá. Recomendamos esta: ao executar operações de divisão/intercalação, não existem outras operações de escrita de efetuar alterações toohello as tabelas de referência.
* serviço de Olá baseia-se na identidade de linha estabelecida através de um índice exclusivo ou uma chave que inclui o desempenho de chave tooimprove Olá fragmentação e fiabilidade para shardlets grandes. Isto permite que os dados do serviço toomove para Olá granularidade melhorar, mesmo que apenas Olá fragmentação valor da chave. Isto ajuda a quantidade máxima de Olá tooreduce de espaço de registo e de bloqueios que são necessários durante a operação de Olá. Considere a criação de um índice exclusivo ou uma chave primária, incluindo a chave de fragmentação de Olá numa determinada tabela, se quiser toouse nessa tabela com pedidos de divisão/intercalação/mover. Por motivos de desempenho, a chave de fragmentação Olá deve ser Olá à esquerda coluna chave Olá ou o índice de Olá.
* Decorrer Olá de processamento de pedidos, alguns dados shardlet podem existir no origem Olá e Olá destino ID de partição horizontal. Isto é necessário tooprotect contra falhas durante o movimento de shardlet Olá. Olá integração da divisão de intercalação com o mapa de partições horizontais Olá assegura que as ligações através de Olá dados dependentes encaminhamento APIs utilizando Olá **OpenConnectionForKey** método no mapa de partições horizontais Olá não vir quaisquer Estados intermédios inconsistentes. No entanto, quando ligação toohello origem ou Olá destino shards sem utilizar Olá **OpenConnectionForKey** método, Estados intermédios inconsistentes poderão estar visíveis quando são acontecimentos divisão/intercalação/mover pedidos. Estas ligações podem mostrar resultados parciais ou duplicados, consoante a temporização de Olá ou a ligação de Olá subjacente do Olá partições horizontais. Esta limitação atualmente inclui ligações de Olá graças à escala elástica várias-Shard-consultas.
* base de dados para o serviço de intercalação de divisão de Olá Olá metadados não tem de ser partilhada entre diferentes funções. Por exemplo, uma função do serviço de intercalação de divisão de Olá em execução no modo de transição tem toopoint tooa diferentes de metadados da base de dados de função de produção Olá.

## <a name="billing"></a>Faturação
serviço de intercalação de divisão de Olá é executado como um serviço em nuvem na sua subscrição do Microsoft Azure. Por conseguinte para serviços em nuvem são aplicáveis encargos tooyour instância do serviço de Olá. A menos que frequentemente efetuar operações de divisão/intercalação/mover, recomendamos a que eliminar o serviço de nuvem de divisão de intercalação. Que guarda os custos para executar ou implementados instâncias de serviço de nuvem. Pode voltar a implementar e iniciar a configuração prontamente passíveis de execução sempre que necessário tooperform dividir ou operações de intercalação. 

## <a name="monitoring"></a>Monitorização
### <a name="status-tables"></a>Tabelas de estado
Olá divisão intercalação serviço fornece Olá **RequestStatus** tabela na base de dados do Olá metadados arquivo para a monitorização de pedidos concluídos e contínuas. tabela de Olá apresenta uma lista de uma linha para cada pedido de divisão de intercalação que foi submetido toothis instância do serviço de intercalação de divisão de Olá. Proporciona Olá seguintes informações para cada pedido:

* **Timestamp**: Olá hora e data quando o pedido de Olá foi iniciado.
* **OperationId**: um GUID que identifica exclusivamente o pedido de Olá. Este pedido também pode ser utilizados toocancel Olá operação enquanto está ainda em curso.
* **Estado**: Olá estado actual do pedido de Olá. Para pedidos em curso, também lista Olá fase atual no qual Olá é pedido.
* **CancelRequest**: um sinalizador que indica se Olá pedido foi cancelado.
* **Progresso**: uma estimativa de percentagem de conclusão da operação de Olá. Um valor de 50 indica que a operação de Olá é aproximadamente 50% concluída.
* **Detalhes**: valor de um XML que fornece um relatório de progresso mais detalhado. relatório de progresso Olá é atualizado periodicamente como conjuntos de linhas são copiados do tootarget de origem. Em caso de falhas ou exceções, esta coluna também inclui informações mais detalhadas sobre falhas de Olá.

### <a name="azure-diagnostics"></a>Diagnóstico do Azure
serviço de intercalação de divisão de Olá utiliza baseado no Azure SDK 2.5 de monitorização e diagnóstico do diagnóstico do Azure. Controlar a configuração de diagnósticos de Olá, conforme explicado aqui: [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](../cloud-services/cloud-services-dotnet-diagnostics.md). Olá pacote de transferência inclui duas configurações de diagnóstico - uma para a função da web Olá e um Olá na função de trabalho. Estas configurações de diagnóstico para o serviço de Olá siga orientação Olá da [Noções básicas do serviço de nuvem no Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649). Inclui Olá definições toolog contadores de desempenho, os registos IIS, registos de eventos do Windows e registos de eventos da aplicação de divisão de intercalação. 

## <a name="deploy-diagnostics"></a>Implementar o diagnóstico
tooenable monitorização e diagnóstico utilizando a configuração de diagnóstico de Olá para Olá trabalho funções da web e fornecidas pelo pacote NuGet de Olá, execute Olá os seguintes comandos com o Azure PowerShell: 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

Pode encontrar mais informações sobre como tooconfigure e implementar as definições de diagnóstico aqui: [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](../cloud-services/cloud-services-dotnet-diagnostics.md). 

## <a name="retrieve-diagnostics"></a>Obter um diagnóstico
Pode aceder facilmente o diagnóstico de Olá Explorador de servidores do Visual Studio no Olá Azure parte da árvore Explorador de servidores de Olá. Abra uma instância do Visual Studio e, na barra de menus Olá clique vista e o Explorador de servidores. Clique em Olá ícone do Azure tooconnect tooyour subscrição do Azure. Em seguida, navegue tooAzure -> armazenamento -> <your storage account> -> tabelas-WADLogsTable >. Para obter mais informações, consulte [navegação nos recursos de armazenamento com o Explorador de servidores](http://msdn.microsoft.com/library/azure/ff683677.aspx). 

![WADLogsTable][2]

Olá WADLogsTable realçado na figura Olá acima contém Olá detalhado de eventos do registo de aplicação do serviço de divisão de intercalação Olá. Tenha em atenção que Olá predefinido a configuração de Olá transferido pacote é adaptado para uma implementação de produção. Por conseguinte o intervalo de Olá que contadores e os registos são solicitados de instâncias de serviço Olá é grande (5 minutos). Para desenvolvimento e teste, inferior Olá intervalo ao ajustar as definições de diagnóstico de Olá de web de Olá ou tooyour de função de trabalho Olá tem. Faça duplo clique na função de Olá no Olá Explorador de servidores do Visual Studio (consultar acima) e, em seguida, ajustar Olá período transferência na caixa de diálogo Olá para definições de configuração de diagnósticos de Olá: 

![Configuração][3]

## <a name="performance"></a>Desempenho
Em geral, um melhor desempenho é toobe esperado de Olá superior, mais escalões de serviço performant na SQL Database do Azure. Superiores alocações de e/s, CPU e memória para os escalões de serviço superiores Olá beneficiam cópia em massa de Olá e eliminar as operações que Olá utiliza o serviço de divisão de intercalação. Por esse motivo, aumente a camada de serviços de Olá apenas para essas bases de dados durante um período definido, limitado de tempo.

serviço de Olá também efetua consultas de validação como parte do respetivas operações normais. Estas consultas de validação verificar inesperada presença de dados no intervalo de destino Olá e certifique-se de que nenhuma operação de intercalação/divisão/movimentação inicia a partir de um estado consistente. Estas consultas de todos os funcionar através de intervalos de chaves de fragmentação definidos pelo âmbito de Olá Olá da operação do e tamanho de lote Olá fornecidas como parte da definição de pedido de Olá. Estas consultas melhor efetuar quando é de um índice que tem a chave de fragmentação Olá Olá coluna à esquerda. 

Além disso, uma propriedade de exclusividade com a chave de fragmentação Olá como coluna à esquerda Olá permitirá Olá serviço toouse uma abordagem otimizada que limita o consumo de recursos em termos de memória e espaço de registo. Esta propriedade de exclusividade é necessário toomove tamanhos de dados de grandes dimensões (normalmente acima 1GB). 

## <a name="how-tooupgrade"></a>Como tooupgrade
1. Siga os passos Olá [implementar um serviço de divisão de intercalação](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
2. Altere o ficheiro de configuração do serviço de nuvem para os implementação de divisão de intercalação tooreflect Olá novo os parâmetros de configuração. Um novo parâmetro necessário é Olá obter informações sobre Olá certificado utilizado para encriptação. Uma forma fácil toodo trata toocompare Olá novo modelo ficheiro de configuração de transferência de Olá contra a sua configuração existente. Certifique-se de que adicionar Olá as definições de "DataEncryptionPrimaryCertificateThumbprint" e "DataEncryptionPrimary" para o web Olá e função de trabalho de Olá.
3. Antes de implementar Olá tooAzure de atualização, certifique-se de que todas as operações de intercalação divisão atualmente em execução tem concluído. Pode facilmente fazê-consultar Olá RequestStatus e PendingWorkflows tabelas na base de dados de metadados de intercalação de divisão de Olá para pedidos em curso.
4. Atualize a implementação de serviço de nuvem existente para a divisão de intercalação na sua subscrição do Azure com o novo pacote de Olá e o ficheiro de configuração de serviço atualizado.

Não é necessário tooprovision uma nova base de dados de metadados de intercalação de divisão tooupgrade. nova versão de Olá automaticamente irá atualizar o metadados da base de dados toohello nova versão existente. 

## <a name="best-practices--troubleshooting"></a>Melhores práticas e resolução de problemas
* Definir um inquilino de teste e exercer as operações de divisão/intercalação/mover mais importantes com inquilino de teste de Olá entre várias partições horizontais. Certifique-se de que todos os metadados está definido corretamente no seu mapa de partições horizontais e que as operações de Olá não violam restrições ou chaves externas.
* Tamanho de dados do inquilino de teste do Keep Olá acima Olá tamanho máximo de dados do seu inquilino maior tooensure não tiver com tamanho dos dados relacionados com problemas. Isto ajuda-o a avaliar um limite superior no tempo de Olá demora toomove um único inquilino à volta. 
* Certifique-se de que o esquema permite eliminações. serviço de intercalação de divisão de Olá requer Olá capacidade tooremove dados Olá origem de partição horizontal depois dos dados de Olá foi copiado com êxito toohello destino. Por exemplo, **eliminar acionadores** pode impedir que o serviço de Olá eliminar dados de Olá na origem de Olá e pode provocar toofail de operações.
* chave de fragmentação Olá deve ser uma coluna à esquerda Olá na sua chave primária ou a definição de índice exclusivo. Garante que Olá obter o melhor desempenho para Olá consultas de validação de intercalação ou divisão e para Olá real movimento e a eliminação operações de dados que operam sempre em intervalos de chaves de fragmentação.
* Colocar o serviço de divisão de intercalação no Centro de dados e a região de olá onde residem as bases de dados. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png

