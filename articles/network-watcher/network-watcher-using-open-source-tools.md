---
title: "aaaVisualize padrões de tráfego de rede com o observador de rede do Azure e ferramentas open source | Microsoft Docs"
description: "Esta página descreve como os pacotes de observador de rede toouse capturar com Capanalysis toovisualize tráfego padrões tooand das suas VMs."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Visualizar tooand de padrões de tráfego de rede da sua VMs utilizando ferramentas open source

Capturas de pacotes contêm dados de rede que lhe permitem tooperform forenses de rede e de inspeção de pacotes aprofundada. Existem abre-se muitas ferramentas de origem que pode utilizar tooanalyze pacote capturas toogain informações sobre a sua rede. Uma ferramenta deste tipo é CapAnalysis, uma ferramenta de visualização de captura de pacotes de código aberto. Visualizar dados de captura de pacotes é uma forma útil tooquickly derivar conhecimentos aprofundados acerca do padrões e anomalias dentro da sua rede. Visualizações também fornecem um meio de partilhar estas informações de forma facilmente consumíveis.

Observador de rede do Azure fornece que Olá toocapture capacidade captura de dados importantes, permitindo-lhe tooperform pacote na sua rede. Neste artigo, fornecemos instruções de como toovisualize e obter conhecimentos aprofundados sobre pacote captura utilizar CapAnalysis com o observador de rede.

## <a name="scenario"></a>Cenário

Tiver uma aplicação web simples implementada numa VM no Azure pretender toouse open source para ferramentas toovisualize respetivo tooquickly de tráfego de rede identificar padrões de fluxo e qualquer anomalias possíveis. Com o observador de rede, pode obter uma captura de pacotes do seu ambiente de rede e armazene-o diretamente na sua conta de armazenamento. CapAnalysis, em seguida, pode inserir Olá captura de pacotes diretamente a partir do blob de armazenamento Olá e visualizar o respetivo conteúdo.

![cenário][1]

## <a name="steps"></a>Passos

### <a name="install-capanalysis"></a>Instalar CapAnalysis

tooinstall CapAnalysis numa máquina virtual, pode consultar as instruções de oficial toohello https://www.capanalysis.net/ca/how-to-install-capanalysis aqui.
Ordem CapAnalysis acedem remotamente aos, precisamos tooopen porta 9877 na sua VM ao adicionar uma nova regra de segurança de entrada. Para obter mais informações sobre como criar regras nos grupos de segurança de rede, consulte demasiado[criar regras num NSG existente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). Assim que a regra de Olá foi adicionada com êxito, deve ser capaz de tooaccess CapAnalysis do`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Utilize a sessão de captura de um pacote de toostart de observador de rede do Azure

Observador de rede permite-lhe toocapture pacotes tootrack o tráfego que entra e sai de uma máquina virtual. Pode consultar as instruções toohello em [capturas de pacotes de gerir com o observador de rede](network-watcher-packet-capture-manage-portal.md) toostart uma sessão de captura de pacotes. Nesta captura de pacotes pode ser armazenada num toobe de blob de armazenamento acedido por CapAnalysis.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Carregar um tooCapAnalysis de captura de pacotes
Diretamente pode carregar uma captura de pacotes executada por observador de rede utilizando o separador de "Importação de URL" Olá e fornecer um blob de armazenamento de toohello ligação onde está armazenada a captura de pacotes hello.

Quando fornecer um tooCapAnalysis de ligação, certifique-se tooappend um URL SAS do blob de armazenamento token toohello.  toodo, navegue tooShared assinatura de acesso da conta de armazenamento Olá, designar Olá permitido permissões e prima toocreate de botão Olá SAS de gerar um token. Em seguida, pode acrescentar este URL de blob de armazenamento de captura do SAS token toohello pacotes.

Olá URL resultante será algo semelhante ao seguinte: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Capturas de pacotes analisa

CapAnalysis oferece várias opções toovisualize a captura de pacotes, cada análise fornecer numa perspetiva de diferentes. Com estas resumos visual, pode compreender as tendências de tráfego de rede e rapidamente detetar qualquer atividade invulgar. Algumas destas funcionalidades são mostradas nas Olá lista a seguir:

1. Tabelas de fluxo

    Este oferece tabela Olá a lista de fluxos de dados do pacote Olá, Olá carimbo de hora associado Olá fluxos e Olá vários protocolos associados às fluxo Olá, bem como o IP de origem e de destino.

    ![página de fluxo de capanalysis][5]

1. Descrição geral do protocolo

    Este painel permite-lhe tooquickly Consulte distribuição Olá de tráfego de rede através de Olá vários protocolos e localizações geográficas.

    ![Descrição geral do protocolo de capanalysis][6]

1. Estatísticas

    Este painel permite estatísticas de tráfego de rede tooview – bytes enviados e recebidos a partir de origem e destino IPs, fluxos para cada um dos Olá origem e de destino IPs, o protocolo utilizado para vários fluxos e a duração de Olá dos fluxos.

    ![estatísticas de capanalysis][7]

1. geomap

    Este painel fornece-lhe uma vista de mapa de tráfego de rede, cores dimensionamento toohello volume de tráfego de cada país. Pode selecionar países realçado tooview as estatísticas de fluxo adicionais, tais como a proporção Olá de dados enviados e recebidos IPs desse país.

    ![geomap][8]

1. Filtros

    CapAnalysis fornece um conjunto de filtros para análise rápida de pacotes específicos. Por exemplo, pode escolher dados de Olá toofilter pelo protocolo toogain específico conhecimentos aprofundados acerca desse subconjunto de tráfego.

    ![filtros][11]

    Visite [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn mais sobre as capacidades de todos os CapAnalysis.

## <a name="conclusion"></a>Conclusão

Funcionalidade de captura de pacotes do observador de rede permite-lhe forenses de rede do toocapture Olá dados tooperform necessário e compreender melhor o tráfego de rede. Neste cenário, iremos mostrou como capturas de pacotes do observador de rede podem facilmente ser integradas com ferramentas de visualização de open source. Utilizando ferramentas open source, tais como capturas de pacotes de toovisualize CapAnalysis, é possível efetuar a inspeção de pacotes aprofundada e identificar rapidamente as tendências dentro do seu tráfego de rede.

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre os registos de fluxo NSG, visite [os registos de NSG fluxo](network-watcher-nsg-flow-logging-overview.md)

Saiba como toovisualize o fluxo de NSG regista com o Power BI, visitando [visualizar NSG flui registos com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
