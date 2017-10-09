---
title: "os registos de aaaVisualizing fluxo do grupo de segurança de rede do Azure com Power BI | Microsoft Docs"
description: "Esta página descreve o modo de fluxo NSG toovisualize registo com o Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Registos de fluxo do grupo de segurança de rede visualizing com o Power BI

Os registos de fluxo do grupo de segurança de rede permitem-lhe tooview informações sobre o tráfego IP de entrada e de saída nos grupos de segurança de rede. Estes registos de fluxo mostram saídos e entrados fluxos numa base por regra, Olá fluxo de Olá NIC se aplica, informações de 5 cadeias de identificação sobre o fluxo de Olá (origem/destino IP, porta de origem/destino, protocolo), e se o tráfego de Olá foi permitido ou negado.

Pode ser difícil toogain insights no registo de dados ao pesquisar manualmente os ficheiros de registo Olá do fluxo. Neste artigo, fornecemos toovisualize uma solução, o fluxo de mais recente regista e obter informações sobre o tráfego na sua rede.

## <a name="scenario"></a>Cenário

No seguinte cenário de Olá, mas ligar conta de armazenamento toohello de ambiente de trabalho do Power BI que configurou como sink Olá relativamente aos nossos dados NSG fluxo de registo. Depois de ligar iremos tooour conta de armazenamento, o Power BI transfere e analisa Olá registos tooprovide uma representação visual de tráfego de Olá que é registado por grupos de segurança de rede.

Os visuais Olá fornecidos no modelo de Olá que pode examinar a utilizar:

* Talkers superiores
* Dados de fluxo de série de tempo por decisão direção e regra
* Fluxos pelo endereço MAC de Interface de rede
* Fluxos por NSG e regra
* Fluxos por porta de destino

modelo de Olá fornecido é editável por isso pode modificá-lo tooadd novos dados, os visuais, ou editar consultas toosuit às suas necessidades.

## <a name="setup"></a>Configurar

Antes de começar, tem de ter rede segurança grupo fluxo o registo ativado num ou vários grupos de segurança de rede na sua conta. Para obter instruções sobre como ativar a segurança de rede flua registos, consulte o seguinte artigo de toohello: [registo tooflow de introdução para grupos de segurança de rede](network-watcher-nsg-flow-logging-overview.md).

Tem de ter também o cliente do ambiente de trabalho do Power BI de Olá instalado no seu computador e suficientemente Liberte espaço no sua máquina toodownload e carga Olá dados de registo que existe na sua conta do storage.

![Diagrama de Visio][1]

### <a name="steps"></a>Passos

1. Transfira e abra Olá seguir o modelo do Power BI de Olá aplicações de ambiente de trabalho do Power BI [modelo os registos de fluxo de PowerBI de observador de rede](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Introduza os parâmetros de consulta Olá necessário
    1. **StorageAccountName** – Especifica toohello nome da conta de armazenamento de Olá fluxo NSG Olá que contêm os registos que teria como tooload e visualizar.
    1. **NumberOfLogFiles** – Especifica Olá número de ficheiros de registo que teria como toodownload e visualizar no Power BI. Por exemplo, se for especificado 50, Olá 50 ficheiros de registo mais recentes. Desativar temos 2 NSGs ativada e configurada toosend NSG fluxo registos toothis conta, em seguida, hello últimas 25 horas de registos pode ser visualizadas.

    ![principal do Power BI][2]

1. Introduza Olá chave de acesso para a sua conta de armazenamento. Pode encontrar chaves de acesso válido ao navegar no Olá Azure portal e selecionar a conta do storage de tooyour **chaves de acesso** a partir do menu de definições de Olá. Clique em **Connect** aplicar as alterações.

    ![chaves de acesso][3]

    ![chave de acesso 2][4]

4.  Os registos são transferir e analisá-la e pode agora utilizar visuais pré-criadas Olá.

## <a name="understanding-hello-visuals"></a>Compreender os visuais de Olá

Fornecida Olá modelo são um conjunto de elementos visuais que ajudam a fazer sentido de Olá dados de registo de fluxo de NSG. Olá imagens que se seguem mostram um exemplo de dashboard que Olá aspeto quando preenchida com dados. A seguir Vamos examinar cada visual em maior detalhe 

![Power BI][5]
 
Talkers de principais de Olá mostra visual Olá IPs que iniciou Olá a maioria das ligações através de Olá período especificado. o tamanho das caixas de Olá Olá corresponde toohello número relativo de ligações. 

![toptalkers][6]

Olá gráficos de séries de tempo seguinte mostram Olá número de fluxos período Olá. gráfico superior Olá é segmentado por direcção do fluxo de Olá e Olá inferior é segmentado por decisão Olá efetuada (permitir ou negar). Este visual, pode examinar as tendências de tráfego ao longo do tempo e detetar qualquer picos anormais ou recusar no tráfego ou segmentação do tráfego.

![flowsoverperiod][7]

Olá gráficos seguintes mostram Olá fluxos por interface de rede com Olá superior segmentados por direcção do fluxo e Olá inferior segmentados por decisão efetuada. Com esta informação, pode obter informações acerca da que as suas VMs comunicados Olá tooothers relativo a maioria das e se o tráfego tooa VM específica está a ser permitido ou negado.

![flowspernic][8]

Olá gráfico do anel roda a seguir mostra uma análise detalhada do fluxos por porta de destino. Com esta informação, pode ver portas de destino Olá utilizado mais frequentemente utilizadas numa Olá especificado período.

![anel][9]

Olá seguinte gráfico de barras mostra Olá fluxo por NSG e da regra. Com estas informações, pode ver Olá NSGs responsáveis por Olá mais tráfego e repartição Olá de tráfego de num NSG pela regra.

![barchart][10]
 
Olá seguintes gráficos informativa apresentar informações sobre NSGs Olá presente nos registos de Olá, Olá número de fluxos capturadas ao longo do período de Olá e a data de Olá de registo mais antigo Olá capturada. Estas informações dão-lhe uma ideia dos quais os NSGs estão a ser registado e Olá intervalo de datas dos fluxos.

![infochart1][11]

![infochart2][12]

Este modelo inclui Olá seguintes tooallow segmentações de dados tooview únicos Olá dados que é mais interessado em. Pode filtrar os grupos de recursos, os NSGs e regras. Também pode filtrar as informações de 5 cadeias de identificação, a decisão e a hora de Olá registo Olá foi escrito.

![segmentações de dados][13]

## <a name="conclusion"></a>Conclusão

Iremos mostrou neste cenário que ao utilizar registos de fluxo de grupo de segurança de rede fornecidos por observador de rede e o Power BI, iremos são toovisualize consegue e compreender o tráfego de Olá. Utilizar o modelo de Olá fornecido, o Power BI transfere registos Olá diretamente a partir do armazenamento e processa-los localmente. Modelo do tempo que demora tooload Olá varia consoante o número de Olá de ficheiros pedida e tamanho total dos ficheiros transferidos.

Pode toocustomize livre este modelo para as suas necessidades. Existem várias formas de várias que pode utilizar o Power BI com o fluxo de registos de grupo de segurança rede. 

## <a name="notes"></a>Notas

* Os registos por predefinição são armazenados no`https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * Se outros dados existem noutro diretório Olá toopull de consultas e processamento de dados de Olá têm de ser modificados.

* modelo de Olá fornecido não é recomendado para utilização com mais de 1 GB de registos.

* Se tiver uma grande quantidade de registos, recomendamos que estiver a investigar uma solução utilizando outro arquivo de dados como o Data Lake ou SQL server.

## <a name="next-steps"></a>Passos Seguintes

Saiba como toovisualize o fluxo de NSG regista com Olá Elastick pilha, visitando [visualizar tooand de padrões de tráfego de rede da sua VMs utilizando ferramentas open source](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
