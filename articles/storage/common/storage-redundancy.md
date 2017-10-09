---
title: "replicação aaaData no armazenamento do Azure | Microsoft Docs"
description: "Os dados na sua conta de armazenamento do Microsoft Azure são replicados para durabilidade e elevada disponibilidade. As opções de replicação incluem o armazenamento localmente redundante (LRS), o armazenamento com redundância de zona (ZRS), o armazenamento georredundante (GRS) e o armazenamento georredundante com acesso de leitura (RA-GRS)."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: ce48d1992fec7bd5ed32feb96b86bef88ca759df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Replicação do Storage do Azure

dados de Olá na sua conta de armazenamento é sempre do Microsoft Azure replicados tooensure durabilidade e elevada disponibilidade. Cópias de replicação Olá, os dados, quer dentro do mesmo centro de dados ou tooa segundo Centro de dados, consoante a que opção de replicação que escolher. Protege os dados de replicação e preserva a sua aplicação de tempo durante o evento Olá de falhas de hardware transitórias. Se os seus dados são replicados tooa segundo Centro de dados, está protegida contra uma falha catastrófica na localização principal Olá.

Replicação garante que a sua conta do storage cumpre Olá [contrato de nível de serviço (SLA) de armazenamento](https://azure.microsoft.com/support/legal/sla/storage/) mesmo em enfrentam Olá de falhas. Consulte Olá SLA para obter informações sobre o Storage do Azure garante para durabilidade e disponibilidade.

Quando cria uma conta de armazenamento, pode selecionar uma das seguintes opções de replicação de Olá:

* [Armazenamento localmente redundante (LRS)](#locally-redundant-storage)
* [Armazenamento com redundância de zona (ZRS)](#zone-redundant-storage)
* [Armazenamento georredundante (GRS)](#geo-redundant-storage)
* [Armazenamento georredundante com acesso de leitura (RA-GRS)](#read-access-geo-redundant-storage)

Armazenamento georredundante com acesso de leitura (RA-GRS) é a opção predefinida de Olá quando cria uma conta de armazenamento.

Olá, a tabela seguinte fornece uma descrição geral rápida das diferenças de Olá entre LRS, ZRS, GRS e RA-GRS, enquanto cada tipo de replicação em mais detalhe de endereço seções subsequentes.

| Estratégia de replicação | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Os dados são replicados em vários datacenters. |Não |Sim |Sim |Sim |
| Podem ler dados a partir de uma localização secundária, bem como localização primária Olá. |Não |Não |Não |Sim |
| Número de cópias dos dados mantidas em nós separados. |3 |3 |6 |6 |

Consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/) para informações sobre preços para as opções de redundância diferentes Olá.

> [!NOTE]
> Armazenamento Premium suporta armazenamento apenas localmente redundante (LRS). Para obter informações sobre o Premium Storage, consulte [Premium Storage: armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual de Azure](../storage-premium-storage.md).
>

## <a name="locally-redundant-storage"></a>Armazenamento localmente redundante
Armazenamento localmente redundante (LRS) replica os dados três vezes dentro de uma unidade de escala de armazenamento, que está alojado num centro de dados na região de Olá no qual criou a conta de armazenamento. Um pedido de escrita com êxito devolve apenas depois de ser escritos tooall três réplicas. Estas três réplicas de cada residirem em domínios de falhas separada e domínios de atualização na unidade de escala de um armazenamento.

Uma unidade de escala de armazenamento é uma coleção de bastidores de nós de armazenamento. Um domínio de falhas (DF) é um grupo de nós que representam uma unidade física de falha e pode ser considerada como nós pertencentes toohello mesmo bastidor físico. Um domínio de atualização (UD) é um grupo de nós que sejam atualizados em conjunto durante o processo de Olá de uma atualização do serviço (implementação). três réplicas de Olá são distribuídas por UDs e FDs dentro tooensure de unidade de escala de um armazenamento que os dados estão disponíveis mesmo se a falha de hardware afeta um bastidor único ou quando nós sejam atualizados durante uma implementação.

LRS é a opção de custo mais baixa Olá e oferece opções de tooother durabilidade em comparação comparada menos. O evento Olá de um desastre ao nível do Centro de dados (fire, sobrecarregar etc.) todas as réplicas de três poderão ser perdidas ou irrecuperável. Georreplicação redundante armazenamento (GRS) toomitigate este risco, é recomendado para a maioria das aplicações.

Armazenamento localmente redundante ainda pode ser preferível em determinados cenários:

* Fornece maior largura de banda máxima das opções de replicação de armazenamento do Azure.
* Se a aplicação armazena os dados que é possível facilmente reconstruir, poderá optar por LRS.
* Algumas aplicações são dados tooreplicating restrito apenas dentro de um país devido a requisitos de governação toodata. Pode ser uma região emparelhada noutro país. Para obter mais informações sobre os pares de região, consulte [regiões do Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Armazenamento com redundância de zona
Armazenamento com redundância de zona (ZRS) replica os dados de forma assíncrona entre centros de dados dentro de uma ou duas regiões na adição toostoring três réplicas semelhante tooLRS, deste modo, fornecendo uma durabilidade superior ao LRS. Os dados armazenados na ZRS são duráveis, mesmo se o datacenter primário Olá está indisponível ou irrecuperáveis.
Os clientes que pretendem toouse ZRS deverá ter em atenção que:

* O ZRS só está disponível para blobs de blocos em contas de armazenamento de objetivo geral e é suportada apenas em versões de serviço de armazenamento 2014-02-14 e posterior.
* Uma vez que a replicação assíncrona envolve um atraso, no evento Olá de um desastre local é possível que as alterações que não tenham sido ainda replicadas toohello secundário serão perdido se não não possível recuperar os dados de Olá de Olá primário.
* réplica Olá poderão não estar disponível até que a Microsoft inicia toohello de ativação pós-falha secundário.
* Não não possível converter as contas de ZRS posterior tooLRS ou GRS. Da mesma forma, uma conta existente do LRS ou GRS não é possível converter a conta ZRS tooa.
* Contas ZRS não tiverem as métricas ou capacidade de registos.

## <a name="geo-redundant-storage"></a>Armazenamento georredundante
Armazenamento georredundante (GRS) replica o dados tooa secundário região centenas de quilómetros região primária Olá. Se a sua conta do storage tiver GRS ativada, em seguida, os dados são duráveis mesmo em caso de Olá de uma falha regional completa ou de um desastre no qual Olá região primária não é recuperável.

Para uma conta de armazenamento com a GRS ativada, uma atualização é primeiro toohello consolidada primário região em que estes são replicados três vezes. Em seguida, a atualização Olá é replicada de forma assíncrona região secundária toohello, onde também são replicado três vezes.

Com a GRS, ambas as regiões de primária e secundária Olá gerir réplicas em vários domínios de falhas separada e atualizar domínios dentro de uma unidade de escala de armazenamento, conforme descrito com LRS.

Considerações:

* Uma vez que a replicação assíncrona envolve um atraso, o evento de um desastre regional, é possível que as alterações que ainda não ter sido replicadas Olá região secundária toohello serão perdido se não não possível recuperar os dados de Olá da região primária Olá.
* réplica Olá não está disponível, a menos que a Microsoft inicia a região secundária de toohello de ativação pós-falha. Se for Microsoft iniciar uma região secundária de toohello de ativação pós-falha, terá acesso de escrita e leitura dados toothat após a ativação pós-falha de Olá foi concluída. Para obter mais informações, consulte [orientações de recuperação após desastre](../storage-disaster-recovery-guidance.md). 
* Se uma aplicação quiser tooread a região secundária Olá, o utilizador Olá deverá ativar RA-GRS.

Quando cria uma conta de armazenamento, seleciona Olá região primária para a conta de Olá. região secundária Olá é determinado com base na região primária Olá e não pode ser alterada. Olá, a tabela seguinte mostra Olá emparelhamentos de região primária e secundária.

| Primária | Secundária |
| --- | --- |
| EUA Centro-Norte |EUA Centro-Sul |
| EUA Centro-Sul |EUA Centro-Norte |
| EUA Leste |EUA Oeste |
| EUA Oeste |EUA Leste |
| Este dos EUA 2 |EUA Central |
| EUA Central |Este dos EUA 2 |
| Europa do Norte |Europa Ocidental |
| Europa Ocidental |Europa do Norte |
| Sudeste Asiático |Ásia Oriental |
| Ásia Oriental |Sudeste Asiático |
| Leste da China |Norte da China |
| Norte da China |Leste da China |
| Leste do Japão |Oeste do Japão |
| Oeste do Japão |Leste do Japão |
| Sul do Brasil |EUA Centro-Sul |
| Leste da Austrália |Sudeste da Austrália |
| Sudeste da Austrália |Leste da Austrália |
| Índia do Sul |Índia Central |
| Índia Central |Índia do Sul |
| Índia Ocidental |Índia do Sul |
| Gov (US) - Iowa |Gov (US) - Virginia |
| Gov (US) - Virginia |Gov (US) - Texas |
| Gov (US) - Texas |Gov (US) - Arizona |
| Gov (US) - Arizona |Gov (US) - Texas |
| Canadá Central |Leste do Canadá |
| Leste do Canadá |Canadá Central |
| Reino Unido Oeste |Reino Unido Sul |
| Reino Unido Sul |Reino Unido Oeste |
| Alemanha Central |Alemanha Nordeste |
| Alemanha Nordeste |Alemanha Central |
| EUA Oeste 2 |EUA Centro-Oeste |
| EUA Centro-Oeste |EUA Oeste 2 |

Para obter informações atualizadas sobre regiões suportadas pelo Azure, consulte [regiões do Azure](https://azure.microsoft.com/regions/).

>[!NOTE]  
> Região secundária do US Virginia EUA é Texas us-nos. Anteriormente, US-nos Virginia utilizados Iowa us-nos de como uma região secundária. As contas do Storage ainda tirar partido dos EUA us Iowa como uma região secundária estão a ser migradas tooUS us Texas como uma região secundário;. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Armazenamento georredundante com acesso de leitura
Armazenamento georredundante com acesso de leitura (RA-GRS) maximiza a disponibilidade para a sua conta de armazenamento, fornecendo dados toohello de acesso só de leitura na localização secundária Olá, além disso toohello replicação em duas regiões fornecida pelo GRS.

Quando ativar dados de tooyour acesso só de leitura na região secundária Olá, os dados estão disponíveis um ponto final secundário, na adição toohello primário ponto final para a sua conta de armazenamento. ponto final secundário de Olá é o ponto de final primário toohello semelhante, mas acrescenta sufixo Olá `–secondary` toohello nome da conta. Por exemplo, se o ponto final principal para Olá serviço Blob é `myaccount.blob.core.windows.net`, em seguida, o ponto final secundário é `myaccount-secondary.blob.core.windows.net`. chaves de acesso de Olá para a sua conta de armazenamento são Olá mesmo para ambos Olá pontos finais primários e secundários.

Considerações:

* A aplicação tem toomanage o ponto final de interagir com ao utilizar o RA-GRS.
* Uma vez que a replicação assíncrona envolve um atraso, o evento de um desastre regional, é possível que as alterações que ainda não ter sido replicadas Olá região secundária toohello serão perdido se não não possível recuperar os dados de Olá da região primária Olá.
* Se o Microsoft inicia a região secundária de toohello de ativação pós-falha, terá acesso de escrita e leitura dados toothat após a ativação pós-falha de Olá foi concluída. Para obter mais informações, consulte [orientações de recuperação após desastre](../storage-disaster-recovery-guidance.md). 
* RA-GRS destina-se a fins de elevada disponibilidade. Para obter orientações de escalabilidade, reveja Olá [lista de verificação de desempenho](../storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. Como alterar o tipo de replicação Olá georreplicação da minha conta de armazenamento?

   Pode alterar o tipo de replicação Olá georreplicação da sua conta de armazenamento entre LRS, GRS, e RA-GRS utilizando Olá [portal do Azure](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) ou através de programação utilizando um dos nossos muitos clientes de armazenamento Bibliotecas. Tenha em atenção que as contas ZRS não podem ser convertida LRS ou GRS. Da mesma forma, uma conta existente do LRS ou GRS não é possível converter a conta ZRS tooa.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. Haverá qualquer tempo se alterar o tipo de replicação de Olá da minha conta de armazenamento?

   Não, haverá qualquer tempo.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. Haverá qualquer custo adicional se alterar o tipo de replicação de Olá da minha conta de armazenamento?

   Sim. Se mudar do LRS tooGRS (ou RA-GRS) para a sua conta de armazenamento, seria implicar um custo adicional de saída ao copiar dados existentes da localização secundária de toohello localização primária. Depois dos dados iniciais Olá são copiados não há nenhum outro encargos de saída adicionais para replicar dados Olá da localização de toosecondary primário Olá de georreplicação. detalhes de Olá para custos de largura de banda podem ser encontrados no Olá [página de preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/blobs/). Se mudar de GRS tooLRS, existe sem custos adicionais, mas os dados serão eliminados da localização secundária Olá.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. Como é que o RA-GRS-me pode ajudar?
   
   Armazenamento GRS fornece replicação dos seus dados de uma região secundária tooa principal que seja centenas de quilómetros região primária Olá. Esse caso, os seus dados são duráveis mesmo em caso de Olá de uma falha regional completa ou de um desastre no qual Olá região primária não é recuperável. Inclui o armazenamento RA-GRS isto e adiciona dados de Olá Olá capacidade tooread da localização secundária Olá. Para algumas ideias sobre como tooleverage esta capacidade, consulte demasiado[conceber altamente disponível aplicações utilizando o armazenamento RA-GRS](../storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. Existe alguma forma para me permitir toofigure saída quanto tempo demora tooreplicate os meus dados da região secundária do Olá toohello primário?
   
   Se estiver a utilizar o armazenamento RA-GRS, pode verificar Olá hora da última sincronização da sua conta de armazenamento. Hora da última sincronização é um valor de data/hora GMT; todas as escritas primárias antes de Olá hora da última sincronização tem sido escrita com êxito na localização secundária toohello, que significa que estão disponível toobe ler a partir da localização secundária Olá. Primário escreve após Olá hora da última sincronização pode ou não estar disponível para leituras ainda. Pode consultar este valor utilizando Olá [portal do Azure](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), ou através de programação utilizando Olá REST API ou um dos Olá bibliotecas de cliente de armazenamento. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. Como posso mudar a região secundária toohello se houver uma falha na região primária Olá?
   
   Consulte o artigo toohello [que toodo se ocorrer uma falha de armazenamento do Azure](../storage-disaster-recovery-guidance.md) para obter mais detalhes.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. O que é Olá RPO e RTO com a GRS?
   
   Objetivo de ponto de recuperação (RPO): Na GRS e RA-GRS, armazenamento Olá do serviço no modo assíncrono georreplicação-são replicados dados de Olá da localização secundária do Olá toohello primário. Se houver um desastre regional principais e uma ativação pós-falha tem toobe efetuada, alterações de delta recentes, que não foram georreplicação poderão perder-se. número de Olá de minutos de potenciais dados perdidos é tooas referenciado Olá RPO (o que significa que pode ser recuperado Olá ponto nos dados de toowhich tempo). Normalmente, temos um RPO menos de 15 minutos, apesar de não existe atualmente nenhum SLA em georreplicação quanto tempo demora.

   Objetivo de tempo de recuperação (RTO): Esta é uma medida de quanto demora-na ativação pós-falha de Olá toodo e voltar a conta de armazenamento Olá online se tivermos toodo uma ativação pós-falha. Olá tempo toodo Olá ativação pós-falha incluem o seguinte de Olá:
    * tempo de Olá, assume-nos tooinvestigate e determinar se estamos pode recuperar dados de Olá na localização primária Olá ou se é preciso toodo uma ativação pós-falha.
    * Conta de Olá de ativação pós-falha ao alterar Olá primária DNS entradas toopoint toohello localização secundária.

   Iremos tirar responsabilidade Olá de preservar os seus dados muito é importante que, de modo a se existir qualquer possibilidade de recuperar dados de Olá, iremos espere efetuar ativação pós-falha do Olá e concentrar-se na recuperação de dados de Olá na localização principal Olá. Olá futura, vamos planear tooallow tooprovide uma API tootrigger uma ativação pós-falha ao nível de uma conta, que, em seguida, permita toocontrol Olá RTO por si, mas este ainda não está disponível.
   
## <a name="next-steps"></a>Passos seguintes
* [Ao conceber aplicações altamente disponíveis a utilizar o armazenamento RA-GRS](../storage-designing-ha-apps-with-ragrs.md)
* [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Sobre as contas de armazenamento do Azure](../storage-create-storage-account.md)
* [Azure metas de desempenho e escalabilidade de armazenamento](storage-scalability-targets.md)
* [Armazenamento do Microsoft Azure redundância opções e acesso de leitura georreplicação armazenamento redundantes](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [Sosp - Storage do Azure: Um elevada serviço em nuvem armazenamento com consistência forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

