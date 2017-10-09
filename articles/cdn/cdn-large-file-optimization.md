---
title: "Otimização de transferência de ficheiro aaaLarge através de Olá rede de entrega de conteúdos do Azure"
description: "Otimização de transferências de ficheiros grandes explicado em profundidade"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Otimização de transferência de ficheiros grandes através de Olá rede de entrega de conteúdos do Azure

Tamanhos de ficheiro de conteúdo a entregar através de Olá Internet continuam toogrow devido a funcionalidade de tooenhanced, gráficos melhorados e conteúdo multimédia formatado. Este crescimento é suscitada pelo departamento por vários fatores: penetração banda larga, maior dispositivos de armazenamento económico, ampla aumento de definição de alta vídeo e ligado à Internet dispositivos (IoT). Um mecanismo de entrega rápidos e eficientes para ficheiros grandes é crítico tooensure uma experiência de consumidor enjoyable e uniforme.

Entrega de ficheiros grandes tem vários desafios. Em primeiro lugar, toodownload de tempo médio de Olá um ficheiro grande pode ser significativa porque as aplicações poderão não transferir todos os dados sequencialmente. Em alguns casos, as aplicações podem transferir Olá última parte um ficheiro antes da primeira parte do Olá. Quando é pedida apenas uma pequena quantidade de um ficheiro ou um utilizador interrompe uma transferência, transferências de Olá podem falhar. transferência de Olá também pode sofrer um atraso de até após Olá rede de entrega de conteúdos (CDN) obtém ficheiro completo hello do servidor de origem Olá. 

Segundo, latência Olá entre a máquina de um utilizador e o ficheiro de Olá determina a velocidade Olá que podem visualizar conteúdo. Além disso, problemas de congestionamento e a capacidade de rede também afetar o débito. As distâncias maiores entre servidores e os utilizadores criar adicionais oportunidades de toooccur de perda de pacotes, reduz a qualidade. redução de Olá da qualidade causado por débito limitado e perda de pacotes aumento pode aumentar o tempo de espera de Olá para um toofinish de transferência de ficheiros. 

Terceira, muitos ficheiros grandes não são fornecidos na sua totalidade. Os utilizadores poderão cancelar uma halfway através de transferência ou veja apenas Olá primeiro alguns minutos de um MP4 longo vídeo. Por conseguinte, as empresas de entrega de software e suportes de dados pretendem toodeliver apenas Olá parte um ficheiro que é pedido. Distribuição eficiente Olá pedida partes reduz o tráfego de saída hello do servidor de origem Olá. Distribuição eficiente também reduz a memória de Olá e pressão de e/s no servidor de origem Olá. 

Agora, Olá rede entrega de conteúdos do Azure da Akamai oferece uma funcionalidade que fornece ficheiros grandes eficientemente toousers em globo Olá à escala. funcionalidade de Olá reduz as latências dado que reduz a carga de Olá nos servidores de origem de Olá. Esta funcionalidade está disponível com o escalão de preço do Olá Standard da Akamai.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>Configurar uma entrega de toooptimize de ponto final CDN de ficheiros grandes

Pode configurar a entrega de toooptimize de ponto final CDN para ficheiros grandes através de Olá portal do Azure. Também pode utilizar os APIs REST ou qualquer um dos Olá cliente SDKs toodo isto. Olá passos seguintes mostram processo Olá através de Olá portal do Azure.

1. tooadd um novo ponto final, Olá **perfil da CDN** página, selecione **Endpoint**.

    ![Novo ponto final](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. No Olá **otimizado para** na lista pendente, selecione **transferências de ficheiros grandes**.

    ![Otimização de ficheiros grandes selecionada](./media/cdn-large-file-optimization/02_Creating.png)


Depois de criar o ponto final de CDN Olá, aplica-se as otimizações de ficheiros grandes Olá para todos os ficheiros que correspondem a determinados critérios. Olá seguinte secção descreve este processo.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Otimizar a entrega de ficheiros grandes com Olá rede de entrega de conteúdos do Azure da Akamai

Ativa a funcionalidade de tipo de otimização de ficheiros grandes Olá na rede otimizações e configurações toodeliver ficheiros grandes mais rápida e mais responsively. Entrega de web geral com Akamai coloca em cache de ficheiros apenas abaixo 1.8 GB e o túnel (não cache) ficheiros de cópia de segurança too150 GB. Otimização de ficheiros grandes coloca em cache de ficheiros de cópia de segurança too150 GB.

A otimização de ficheiros grandes está em vigor quando forem satisfeitas determinadas condições. As condições incluem como funciona o servidor de origem Olá tamanhos de Olá e tipos de ficheiros de Olá que são pedidos. Antes de obtemos para obter detalhes sobre estes assuntos, deve compreender como funciona a otimização de Olá. 

### <a name="object-chunking"></a>Objeto de agrupamento 

Olá rede entrega de conteúdos do Azure da Akamai utiliza uma técnica chamada objeto de agrupamento. Quando é pedido um ficheiro grande, Olá CDN obtém partes mais pequenas do ficheiro de Olá de origem Olá. Depois do servidor de limite/POP do CDN Olá recebe um pedido de ficheiro completo ou intervalo de bytes, verifica se o tipo de ficheiro hello é suportado para esta otimização. Também verifica se o tipo de ficheiro Olá cumpre os requisitos de tamanho de ficheiro Olá. Se o tamanho do ficheiro Olá for superior a 10 MB, Olá CDN edge pedidos Olá ficheiro do servidor de origem do Olá em segmentos de 2 MB. 

Depois de segmento de Olá chega Olá CDN edge, tem em cache e servidos imediatamente toohello utilizador. Olá CDN e segmentos de seguinte Olá prefetches em paralelo. Este obtenção prévia assegura que o conteúdo de Olá permanece um segmento à frente das utilizador Olá, o que reduz a latência. Este processo continua até Olá todo ficheiro é transferido (se requerido), todos os intervalos de byte estão disponíveis (se requerido), ou cliente Olá termina ligação Olá. 

Para obter mais informações sobre o pedido de intervalo de bytes de Olá, consulte [RFC 7233](https://tools.ietf.org/html/rfc7233).

Olá CDN coloca em cache quaisquer segmentos como que está a ser recebidos. ficheiro completo Olá não tem toobe em cache na cache CDN Olá. Os pedidos subsequentes para intervalos de bytes ou ficheiro Olá são servidos de Olá cache da CDN. Se nem todos os segmentos de Olá são colocadas em cache no Olá CDN, obtenção prévia é utilizado toorequest segmentos da origem de Olá. Esta otimização baseia-se na capacidade de Olá de pedidos de intervalo de bytes de toosupport de servidor de origem de Olá. _Se o servidor de origem Olá não suporta pedidos de intervalo de bytes, esta otimização não está em vigor._ 

### <a name="caching"></a>Colocação em cache
Otimização de ficheiros grandes utiliza tempos de expiração de colocação em cache predefinido diferente da entrega de web geral. -Distingue entre a colocação em cache positivos e negativos colocação em cache baseado em códigos de resposta HTTP. Se o servidor de origem Olá Especifica uma hora de expiração através de uma cache-control ou expira o cabeçalho de resposta Olá, Olá CDN honra esse valor. Quando não especifica a origem de Olá e ficheiro Olá corresponde a condições de tipo e o tamanho de Olá para este tipo de otimização, Olá CDN utiliza os valores predefinidos de Olá para a otimização de ficheiros grandes. Caso contrário, Olá CDN utiliza as predefinições para a entrega de web geral.


|    | Web geral | Otimização de ficheiros grandes 
--- | --- | --- 
A colocação em cache: positivo <br> HTTP 200, 203, 300, <br> 301, 302 e 410 | 7 dias |1 dia  
A colocação em cache: negativo <br> HTTP 204, 305, 404, <br> e 405 | Nenhuma | 1 segundo 

### <a name="deal-with-origin-failure"></a>Lidar com falha de origem

comprimento de limite de tempo de leitura de origem Olá aumenta de dois segundos para minutos tootwo de entrega de web geral para o tipo de otimização Olá ficheiros grandes. Este aumento contas para tooavoid de tamanhos de ficheiro maior do Olá uma ligação de tempo limite prematuro.

Quando uma ligação exceder o tempo limite, Olá CDN repete um número de vezes antes de enviar um cliente de toohello de erro "504 - tempo limite do Gateway". 

### <a name="conditions-for-large-file-optimization"></a>Condições para a otimização de ficheiros grandes

Olá, a tabela seguinte lista o conjunto de Olá de critérios toobe satisfeito para a otimização de ficheiros grandes:

Condição | Valores 
--- | --- 
Tipos de ficheiro suportados | 3G 2 3gp, asf, avi, bz2, dmg,. exe, f4v, flv, <br> GZ hdp, iso, jxr, m4v, mkv, mov, mp4, <br> MPEG mpg, mts, pkg, qt, rm, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, zip  
Tamanho mínimo do ficheiro | 10 MB 
Tamanho máximo do ficheiro | 150 GB 
Características de servidor de origem | Tem de suportar pedidos de intervalo de bytes 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Otimizar a entrega de ficheiros grandes com Olá rede de entrega de conteúdos do Azure da Verizon

Olá rede entrega de conteúdos do Azure da Verizon fornece ficheiros grandes sem um limite no tamanho do ficheiro. Funcionalidades adicionais estão ativadas pelo fornecimento de toomake predefinidas de ficheiros grandes mais rapidamente.

### <a name="complete-cache-fill"></a>Preenchimento da cache concluída

Olá predefinido cache concluída preenchimento funcionalidade permite-Olá CDN toopull um ficheiro para a cache de Olá quando um pedido inicial é abandonado ou perdido. 

Preenchimento da cache completa é mais útil para grandes ativos. Normalmente, os utilizadores não transferirem-los de toofinish de início. Utilizam transferência progressiva. comportamento predefinido de Olá força Olá edge servidor tooinitiate uma obtenção de fundo do elemento de Olá do servidor de origem Olá. Posteriormente, asset Olá está na cache local do servidor edge Olá. Depois de objeto completo Olá na cache de Olá, o servidor edge de Olá satisfaz intervalo de bytes pedidos toohello CDN de objeto em cache Olá.

comportamento predefinido de Olá pode ser desativado através do motor de regras de Olá no Olá escalão Premium da Verizon.

### <a name="peer-cache-fill-hot-filing"></a>Arquivo de acesso frequente de preencher a cache ponto a ponto

funcionalidade de arquivo de acesso frequente de preenchimento de cache ponto a ponto predefinidos Olá utiliza um algoritmo proprietário sofisticado. Utiliza edge adicional com base na largura de banda de servidores de colocação em cache e pedidos de cliente de toofulfill métricas para objetos de grandes, altamente populares os pedidos de agregação. Esta funcionalidade impede uma situação em que grande número de pedidos adicionais é enviado por servidor de origem do utilizador tooa. 

### <a name="conditions-for-large-file-optimization"></a>Condições para a otimização de ficheiros grandes

funcionalidades de otimização de Olá da Verizon estão ativadas por predefinição. Existem não existem limites no tamanho máximo do ficheiro. 

## <a name="additional-considerations"></a>Considerações adicionais

Considere Olá os seguintes aspetos adicionais para este tipo de otimização.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Rede de entrega de conteúdos do Azure da Akamai

- Olá segmentação processo gera o servidor de origem toohello pedidos adicionais. No entanto, hello global volume de dados enviados origem Olá é muito menor. Os resultados das secções no melhor as características de colocação em cache no Olá CDN.

- Memória e pressão de e/s são reduzidos na origem de Olá porque partes mais pequenas do ficheiro de Olá são entregues.

- Para segmentos na cache em Olá CDN, existem não existem pedidos adicionais toohello origem até expira o conteúdo de Olá ou é expulsos da cache de Olá.

- Os utilizadores podem efetuar intervalo toohello CDN os pedidos e está a ser tratadas como qualquer ficheiro normal. Otimização só se aplica se é um tipo de ficheiro válido e o intervalo de bytes de Olá entre 10 MB e 150 GB. Se o tamanho de ficheiro médio Olá pedido for inferior a 10 MB, pode querer toouse entrega de geral web em vez disso.

### <a name="azure-content-delivery-network-from-verizon"></a>Rede de entrega de conteúdos do Azure da Verizon

tipo de otimização de entrega de web geral Olá pode proporcionar ficheiros grandes.
