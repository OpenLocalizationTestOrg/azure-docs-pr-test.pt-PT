---
title: "definições de ReliableDictionaryActorStateProvider aaaChange no Azure micro-serviços | Microsoft Docs"
description: "Saiba mais sobre a configuração de atores com monitorização de estado do Azure Service Fabric do tipo ReliableDictionaryActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Configurar Reliable Actors – ReliableDictionaryActorStateProvider
Pode modificar a configuração predefinida Olá ReliableDictionaryActorStateProvider alterando o ficheiro de settings.xml Olá gerado na raiz do pacote de Visual Studio Olá na pasta de configuração de Olá para ator especificado Olá.

Olá Azure Service Fabric runtime procura os nomes de secção predefinidas no ficheiro de settings.xml Olá e consome valores de configuração de Olá ao criar Olá subjacente componentes runtime.

> [!NOTE]
> Efetue **não** eliminar ou modificar os nomes de secção Olá de Olá seguintes configurações no ficheiro de settings.xml Olá que é gerado no Olá solução do Visual Studio.
> 
> 

Existem também definições globais que afetam a configuração de Olá de ReliableDictionaryActorStateProvider.

## <a name="global-configuration"></a>Configuração global
configuração global Olá é especificada no manifesto do cluster Olá para cluster Olá em Olá KtlLogger secção. Permite que a configuração de Olá partilhado registo localização e tamanho plus Olá global limites de memória utilizada pelo registo de Olá. Tenha em atenção que as alterações no manifesto do cluster Olá afetam todos os serviços que utilizam ReliableDictionaryActorStateProvider e reliable services com monitorização de estado.

manifesto do cluster Olá é um único ficheiro XML que contém as definições e configurações que se aplicam tooall nós e serviços em cluster Olá. ficheiro de Olá é normalmente denominado ClusterManifest.xml. Pode ver manifesto do cluster Olá para o cluster utilizando o comando do powershell Olá Get ServiceFabricClusterManifest.

### <a name="configuration-names"></a>Nomes de configuração
| Nome | Unidade | Valor predefinido | Observações |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Quilobytes |8388608 |Número mínimo de KB tooallocate no modo de kernel para registador Olá escrever o conjunto de memória de memória intermédia. Este conjunto de memória é utilizado para colocar em cache as informações de estado antes de escrever toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Quilobytes |Sem Limite |Olá de toowhich de tamanho máximo registador conjunto de memória de memória intermédia de escrita pode crescer. |
| SharedLogId |GUID |"" |Especifica um toouse GUID exclusivo para identificar o Olá partilhado ficheiro de registo predefinido utilizado por todos os serviços fiáveis em todos os nós no cluster de Olá que não especificam Olá SharedLogId na respetiva configuração específica do serviço. Se não for especificado SharedLogId, em seguida, SharedLogPath deve ser também especificado. |
| SharedLogPath |Nome de caminho completamente qualificado |"" |Especifica o caminho completamente qualificado olá onde Olá partilhados utilizado por todos os serviços fiáveis em todos os nós no cluster de Olá que não especificam Olá SharedLogPath na respetiva configuração específica do serviço de ficheiro de registo. No entanto, se SharedLogPath for especificado, em seguida, SharedLogId deve ser também especificado. |
| SharedLogSizeInMB |Megabytes |8192 |Especifica o número de Olá de MB de espaço em disco toostatically alocar para o registo de Olá partilhado. valor de Olá tem de ser 2048 ou superior. |

### <a name="sample-cluster-manifest-section"></a>Secção de manifesto do cluster de exemplo
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>Observações
registo de Olá tem um conjunto de memória atribuída de memória de kernel não paginadas que está disponível tooall serviços fiável num nó para a colocação em cache dados de estado antes de serem escritas registo dedicado toohello associado a réplica de serviço fiável de Olá global. tamanho do conjunto de Olá é controlado pelas definições de WriteBufferMemoryPoolMaximumInKB e Olá WriteBufferMemoryPoolMinimumInKB. WriteBufferMemoryPoolMinimumInKB especifica ambos Olá tamanho inicial deste conjunto de memória e pode diminuir Olá mais baixo tamanho toowhich Olá agrupamento de memória. WriteBufferMemoryPoolMaximumInKB é pode aumentar Olá maior tamanho toowhich Olá agrupamento de memória. Cada réplica fiável de serviço que é aberta pode aumentar o tamanho de Olá do conjunto de memória de Olá por um período de sistema determinado segurança tooWriteBufferMemoryPoolMaximumInKB. Se existir mais de pedido de memória do agrupamento de memória que está disponível no Olá, pedidos de memória irão sofrer um atraso de até que a memória está disponível. Por conseguinte, se o conjunto de memória da memória intermédia de escrita de Olá é demasiado pequeno para uma configuração específica, em seguida, o desempenho poderá diminuir.

definições de SharedLogId e SharedLogPath Olá são sempre utilizadas toodefine em conjunto Olá GUID e localização para a predefinição de Olá partilhado registo para todos os nós do cluster de Olá. registo partilhado do Olá predefinido é utilizado para todos os serviços fiáveis que não especificam as definições de Olá em settings.xml Olá para serviço específico Olá. Para melhor desempenho, os ficheiros de registo partilhado devem ser colocados em discos que são utilizados apenas para a contenção de tooreduce de ficheiro de registo Olá partilhado.

SharedLogSizeInMB Especifica a quantidade de Olá de toopreallocate de espaço em disco para o registo partilhado Olá de predefinição em todos os nós.  Não é necessário SharedLogId e SharedLogPath toobe especificado por ordem para toobe SharedLogSizeInMB especificado.

## <a name="replicator-security-configuration"></a>Configuração de segurança do replicador
Configurações de segurança do replicador são canal de comunicação de Olá toosecure utilizado que é utilizado durante a replicação. Isto significa que os serviços não é possível ver o tráfego de replicação entre si, de dados, garantindo que Olá efetuada elevados também é segurados.
Por predefinição, uma secção de configuração de segurança vazio impede a segurança da replicação.

### <a name="section-name"></a>Nome de secção
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuração do replicador
Configurações do replicador são replicador de Olá tooconfigure utilizado que é responsável por verificar o estado de fornecedor de estado de Ator Olá altamente fiável ao replicar e a persistência de estado de Olá localmente.
configuração predefinida de Olá é gerada pelo modelo de Visual Studio Olá e deve suffice. Esta secção aborda as configurações adicionais que são replicador de Olá tootune disponíveis.

### <a name="section-name"></a>Nome de secção
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nomes de configuração
| Nome | Unidade | Valor predefinido | Observações |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Segundos |0.015 |Período de tempo para o replicador Olá em aguarda secundária de Olá depois de receber uma operação antes de devolver um toohello confirmação primário. Outro toobe confirmações enviado para operações de processamento dentro deste intervalo são enviadas como uma resposta. |
| ReplicatorEndpoint |N/D |Sem predefinição - parâmetro necessário |Endereço IP e porta Olá replicador principal/secundário irão utilizar toocommunicate com outros os replicadores no conjunto de réplicas Olá. Isto deverá referenciar um ponto de final de recursos TCP no manifesto do serviço de Olá. Consulte demasiado[recursos do serviço do manifesto](service-fabric-service-manifest-resources.md) tooread mais sobre como definir os recursos de ponto final no manifesto do serviço. |
| MaxReplicationMessageSize |Bytes |50 MB |Tamanho máximo de dados de replicação que podem ser transmitidos numa única mensagem. |
| MaxPrimaryReplicationQueueSize |Número de operações |8192 |Número máximo de operações em fila primário Olá. Uma operação é libertada cópias de segurança depois do replicador primário Olá recebe uma confirmação dos de replicadores secundário Olá todos os. Este valor tem de ser superior a 64 e uma potência de 2. |
| MaxSecondaryReplicationQueueSize |Número de operações |16384 |Número máximo de operações em fila secundária Olá. Uma operação é libertada cópias de segurança depois de efetuar o seu estado de elevada disponibilidade através de persistência. Este valor tem de ser superior a 64 e uma potência de 2. |
| CheckpointThresholdInMB |MB |200 |Quantidade de espaço no ficheiro de registo após o qual o estado de Olá é checkpointed. |
| MaxRecordSizeInKB |KB |1024 |Tamanho maior de registo que Olá replicador pode escrever no registo de Olá. Este valor tem de ser um múltiplo de 4 e superior a 16. |
| OptimizeLogForLowerDiskUsage |Valor booleano |VERDADEIRO |Quando verdadeiro, o registo de Olá está configurado para que hello ficheiros de registo dedicado da réplica é criado utilizando um ficheiro disperso NTFS. Isto reduz a utilização do espaço em disco real Olá para o ficheiro de Olá. Se for FALSO, é criado o ficheiro de Olá com alocações fixas, que fornecem o melhor desempenho de escrita Olá. |
| SharedLogId |GUID |"" |Especifica um toouse guid exclusivo para identificar o Olá partilhado ficheiro de registo utilizado com esta réplica. Normalmente, os serviços não devem utilizar esta definição. No entanto, se SharedLogId for especificado, em seguida, SharedLogPath deve ser também especificado. |
| SharedLogPath |Nome de caminho completamente qualificado |"" |Especifica o caminho completamente qualificado olá onde Olá partilhado ficheiro de registo desta réplica será criado. Normalmente, os serviços não devem utilizar esta definição. No entanto, se SharedLogPath for especificado, em seguida, SharedLogId deve ser também especificado. |

## <a name="sample-configuration-file"></a>Ficheiro de configuração de exemplo
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```

## <a name="remarks"></a>Observações
parâmetro de BatchAcknowledgementInterval Olá controla a latência de replicação. Um valor de '0' resulta num Olá menor latência possível, custo Olá de débito (como mais mensagens de confirmação tem de ser enviadas e processadas, cada que contém menos confirmações).
Olá maior valor Olá BatchAcknowledgementInterval, Olá Olá superior global débito de replicação, custo Olá de latência de operação superior. Isto traduz diretamente toohello latência de consolidações de transações.

quantidade de Olá do Olá CheckpointThresholdInMB parâmetro controlos de espaço em disco que Olá replicador pode utilizar informações de estado de toostore no ficheiro de registo dedicado da réplica Olá. Aumentar este valor mais alto tooa que predefinido Olá pode resultar em tempos mais rápidos de reconfiguração quando uma nova réplica é adicionada toohello conjunto. Isto acontece devido a transferência de estado parcial toohello que decorre devido a disponibilidade de toohello do histórico mais operações no registo de Olá. Isto pode aumentar potencialmente a hora da recuperação de uma réplica Olá após uma falha.

Se definir OptimizeForLowerDiskUsage tootrue, espaço do ficheiro de registo será excessiva aprovisionado para que as réplicas Active Directory podem armazenar mais informações de Estado nos respetivos ficheiros de registo, enquanto réplicas Inativas irão utilizar menos espaço em disco. Isto torna possível toohost mais réplicas num nó. Se definir OptimizeForLowerDiskUsage toofalse, informações de estado de Olá são escritas toohello ficheiros de registo mais rapidamente.

definição de MaxRecordSizeInKB Olá define o tamanho máximo do Olá de um registo que pode ser escrito pelo replicador Olá no ficheiro de registo Olá. Na maioria dos casos, tamanho de 1024-KB registo Olá predefinido é o ideal. No entanto, se o serviço Olá é causar a maior parte de toobe de itens de dados de informações de estado de Olá, este valor poderá ter toobe aumentada. Não há pouca benefício tomar MaxRecordSizeInKB inferior a 1024, como registos mais pequenos utilizam apenas espaço de Olá necessário para registo mais pequeno Olá. Esperamos que este valor teria toobe alterado apenas em casos raros.

definições de SharedLogId e SharedLogPath Olá são sempre utilizada toomake em conjunto uma utilização de serviço um registo partilhado separado do registo partilhado do Olá predefinido para o nó de Olá. Para melhor eficiência, como muitos serviços possível devem especificar Olá mesmo partilhado registo. Ficheiros de registo partilhado devem ser colocados em discos que são utilizados apenas para o ficheiro de registo partilhado Olá, tooreduce contenção de movimento head. Esperamos que estes valores teria toobe alterado apenas em casos raros.

