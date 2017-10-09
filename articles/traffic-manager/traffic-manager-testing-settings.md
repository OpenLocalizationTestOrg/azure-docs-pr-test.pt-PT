---
title: "definições do Gestor de tráfego do Azure aaaVerify | Microsoft Docs"
description: "Este artigo irá ajudá-lo a verificar as definições do Gestor de tráfego"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>Verifique as definições do Gestor de tráfego

tootest as definições do Gestor de tráfego, terá de toohave vários clientes em várias localizações, a partir da qual pode executar os testes. Em seguida, coloque pontos finais de Olá do perfil do Traffic Manager para baixo um de cada vez.

* Defina Olá valor de TTL do DNS baixa que as alterações propagarem rapidamente (por exemplo, 30 segundos).
* Sabe Olá endereços IP dos seus serviços em nuvem do Azure e Web sites no perfil de Olá que estiver a testar.
* Utilize as ferramentas que permitem-lhe resolver um endereço IP de tooan de nome DNS e apresentar esse endereço.

Está a verificar toosee que os nomes DNS Olá resolver endereços tooIP de pontos finais de Olá no seu perfil. os nomes de Olá devem resolver de forma consistente com o método de encaminhamento de tráfego de Olá definido no Olá perfil do Traffic Manager. Pode utilizar ferramentas de Olá como **nslookup** ou **aprofundar** tooresolve nomes DNS.

Olá exemplos seguintes ajudá-lo testar o perfil do Traffic Manager.

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>Verifique o perfil do Traffic Manager utilizar nslookup e ipconfig no Windows

1. Abra uma linha de comandos do Windows PowerShell ou um comando como administrador.
2. Tipo `ipconfig /flushdns` tooflush Olá cache de resolução DNS.
3. Digite `nslookup <your Traffic Manager domain name>`. Por exemplo, Olá os seguintes comandos verificações Olá nome de domínio com o prefixo de Olá *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    Resultado típico mostra Olá seguintes informações:

    + Olá nome DNS e endereço IP do servidor DNS de Olá a ser acedidas tooresolve este nome de domínio do Traffic Manager.
    + nome de domínio do Traffic Manager Olá que escreveu na linha de comandos Olá após "nslookup" e o domínio do Traffic Manager de Olá toowhich Olá IP endereço resolve. endereço IP segundo Olá é Olá toocheck de um importantes. Deve corresponder a um público endereço IP virtual (VIP) para um dos serviços de cloud Olá ou Web sites Olá perfil do Traffic Manager estiver a testar.

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>Como o método de encaminhamento de tráfego de ativação pós-falha de Olá tootest

1. Deixe todos os pontos finais cópias de segurança.
2. Utilizar um único cliente, o pedido resolução de DNS para o nome de domínio da empresa utilizando nslookup ou um utilitário semelhante.
3. Certifique-se de que Olá resolver o endereço IP corresponde ao ponto final de primário Olá.
4. Traga a sua primário endpoint ou remova Olá monitorização de ficheiros para que o Gestor de tráfego pensa que Olá aplicação estiver em baixo.
5. Aguarde Olá DNS Time-to-Live (TTL) do perfil do Traffic Manager Olá plus dois minutos adicionais. Por exemplo, se o TTL de DNS é de 300 segundos (5 minutos), tem de aguardar durante sete minutos.
6. Esvaziar a DNS cliente pedido e a cache de resolução de DNS com nslookup. No Windows, pode esvaziar a cache DNS com o comando do Olá ipconfig /flushdns.
7. Certifique-se de que Olá resolver o ponto final secundário corresponde de endereço IP.
8. Repita o processo de Olá, desativar por sua vez a cada ponto final. Certifique-se de que Olá DNS devolve o endereço IP Olá do ponto final de seguinte Olá na lista de Olá. Quando todos os pontos finais estão inativos, deve obter o endereço IP de Olá do ponto final de primário Olá novamente.

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>Como tootest Olá ponderado método de encaminhamento de tráfego

1. Deixe todos os pontos finais cópias de segurança.
2. Utilizar um único cliente, o pedido resolução de DNS para o nome de domínio da empresa utilizando nslookup ou um utilitário semelhante.
3. Certifique-se de que Olá resolver o endereço IP corresponde a um dos seus pontos finais.
4. Esvaziar a cache do cliente DNS e repita os passos 2 e 3 para cada ponto final. Deverá ver endereços IP diferentes para cada um dos seus pontos finais.

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>Como o método de encaminhamento de tráfego de desempenho de Olá tootest

tooeffectively testar um método de encaminhamento de tráfego de desempenho, tem de ter os clientes localizados em diferentes partes de Olá mundo. Pode criar os clientes em diferentes regiões do Azure que podem ser utilizado tootest os serviços. Se tiver uma rede global, pode iniciar sessão tooclients em outras partes do Olá mundo remotamente e executar os testes a partir daí.

Em alternativa, existem livre baseada na web pesquisa de DNS e aprofundar serviços disponíveis. Algumas destas ferramentas conceder Olá resolução do nome DNS do capacidade toocheck de várias localizações em torno Olá mundo. Efetue uma pesquisa no "Pesquisa de DNS" para obter exemplos. Serviços de terceiros como Gomez ou da keynote //Build podem ser utilizado tooconfirm que os perfis de estão a distribuir o tráfego, conforme esperado.

## <a name="next-steps"></a>Passos seguintes

* [Sobre os métodos de encaminhamento de tráfego do Gestor de tráfego](traffic-manager-routing-methods.md)
* [Considerações de desempenho para o Gestor de Tráfego](traffic-manager-performance-considerations.md)
* [Resolução de problemas do estado degradado do Gestor de Tráfego](traffic-manager-troubleshooting-degraded.md)
