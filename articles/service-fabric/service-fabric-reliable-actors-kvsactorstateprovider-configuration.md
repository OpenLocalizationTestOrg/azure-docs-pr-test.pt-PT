---
title: "definições de KVSActorStateProvider aaaChange no Azure micro-serviços | Microsoft Docs"
description: "Saiba mais sobre a configuração de atores com monitorização de estado do Azure Service Fabric do tipo KVSActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Configurar Reliable Actors – KVSActorStateProvider
Pode modificar a configuração predefinida Olá KVSActorStateProvider alterando o ficheiro de settings.xml Olá que é gerado na raiz do pacote Microsoft Visual Studio Olá na pasta de configuração de Olá para ator especificado Olá.

Olá Azure Service Fabric runtime procura os nomes de secção predefinidas no ficheiro de settings.xml Olá e consome valores de configuração de Olá ao criar Olá subjacente componentes runtime.

> [!NOTE]
> Efetue **não** eliminar ou modificar os nomes de secção Olá de Olá seguintes configurações no ficheiro de settings.xml Olá que é gerado no Olá solução do Visual Studio.
> 
> 

## <a name="replicator-security-configuration"></a>Configuração de segurança do replicador
Configurações de segurança do replicador são canal de comunicação de Olá toosecure utilizado que é utilizado durante a replicação. Isto significa que os serviços não é possível ver uns dos outros tráfego de replicação, garantir que os dados de Olá efetuada elevados também estão segurados.
Por predefinição, uma secção de configuração de segurança vazio impede a segurança da replicação.

### <a name="section-name"></a>Nome de secção
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuração do replicador
Configurações do replicador configurar replicador Olá que é responsável por verificar o estado de fornecedor de estado de Ator Olá altamente fiável.
configuração predefinida de Olá é gerada pelo modelo de Visual Studio Olá e deve suffice. Esta secção aborda as configurações adicionais que são replicador de Olá tootune disponíveis.

### <a name="section-name"></a>Nome de secção
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nomes de configuração
| Nome | Unidade | Valor predefinido | Observações |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Segundos |0.015 |Período de tempo para o replicador Olá em aguarda secundária de Olá depois de receber uma operação antes de devolver um toohello confirmação primário. Outro toobe confirmações enviado para operações de processamento dentro deste intervalo são enviadas como uma resposta. |
| ReplicatorEndpoint |N/D |Sem predefinição - parâmetro necessário |Endereço IP e porta Olá replicador principal/secundário irão utilizar toocommunicate com outros os replicadores no conjunto de réplicas Olá. Isto deverá referenciar um ponto de final de recursos TCP no manifesto do serviço de Olá. Consulte demasiado[recursos do serviço do manifesto](service-fabric-service-manifest-resources.md) tooread mais sobre como definir os recursos de ponto final no manifesto do serviço de Olá. |
| RetryInterval |Segundos |5 |Período de tempo após o qual Olá replicador novamente transmite a mensagem se receber uma confirmação de uma operação. |
| MaxReplicationMessageSize |Bytes |50 MB |Tamanho máximo de dados de replicação que podem ser transmitidos numa única mensagem. |
| MaxPrimaryReplicationQueueSize |Número de operações |1024 |Número máximo de operações em fila primário Olá. Uma operação é libertada cópias de segurança depois do replicador primário Olá recebe uma confirmação dos de replicadores secundário Olá todos os. Este valor tem de ser superior a 64 e uma potência de 2. |
| MaxSecondaryReplicationQueueSize |Número de operações |2048 |Número máximo de operações em fila secundária Olá. Uma operação é libertada cópias de segurança depois de efetuar o seu estado de elevada disponibilidade através de persistência. Este valor tem de ser superior a 64 e uma potência de 2. |

## <a name="store-configuration"></a>Configuração do arquivo
Configurações de arquivo são utilizados tooconfigure Olá arquivo local que é utilizado toopersist Olá Estado que está a ser replicado.
configuração predefinida de Olá é gerada pelo modelo de Visual Studio Olá e deve suffice. Esta secção aborda as configurações adicionais que são arquivo local do Olá tootune disponíveis.

### <a name="section-name"></a>Nome de secção
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Nomes de configuração
| Nome | Unidade | Valor predefinido | Observações |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |milissegundos |200 |Define o máximo de Olá intervalo do arquivo local durável consolidações de criação de batches. |
| MaxVerPages |Número de páginas |16384 |número máximo de Olá de páginas de versão no local Olá armazena a base de dados. Determina o número máximo de Olá de transações pendentes. |

## <a name="sample-configuration-file"></a>Ficheiro de configuração de exemplo
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
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

