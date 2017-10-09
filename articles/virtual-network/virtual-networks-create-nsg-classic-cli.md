---
title: "aaaHow toocreate NSGs no modo clássico utilizando Olá CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate e implementar NSGs no modo clássico com Olá CLI do Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a>Como os NSGs toocreate (clássico) na Olá CLI do Azure
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo abrange o modelo de implementação clássica Olá. Também pode [criar NSGs no modelo de implementação do Resource Manager Olá](virtual-networks-create-nsg-arm-cli.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

comandos de CLI do Azure de exemplo de Olá abaixo esperam num ambiente simple já criado com base no cenário de Olá acima. Se pretender que os comandos de Olá toorun como são apresentados neste documento, primeiro criar ambiente de teste de Olá por [criar uma VNet](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Como toocreate Olá NSG para sub-rede do front-end Olá
toocreate com o nome de um NSG denominado **NSG-front-end** com base no cenário de Olá acima, siga os passos de Olá abaixo.

1. Se nunca tiver utilizado a CLI do Azure, consulte o artigo [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md) e siga as instruções de Olá toohello ponto onde poderá selecionar a sua conta do Azure e a subscrição de cópia de segurança.
2. Executar Olá  **`azure config mode`**  comando tooswitch tooclassic modo, conforme mostrado abaixo.
   
        azure config mode asm
   
    Resultado esperado:
   
        info:    New mode is asm
3. Executar Olá  **`azure network nsg create`**  comando toocreate um NSG.
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    Resultado esperado:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Parâmetros:
   
   * **-l (ou --location)**. Região do Azure onde hello novo NSG será criado. Para o nosso cenário *westus*.
   * **-n (ou --name)**. Nome para Olá novo NSG. Para o nosso cenário *NSG-front-end*.
4. Executar Olá  **`azure network nsg rule create`**  comando toocreate uma regra que permite acesso tooport 3389 (RDP) de Olá Internet.
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    Resultado esperado:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    Parâmetros:
   
   * **-a (ou - nsg-name)**. Nome do NSG Olá no qual Olá regra será criada. Para o nosso cenário *NSG-front-end*.
   * **-n (ou --name)**. Nome da nova regra de Olá. Para o nosso cenário *rdp regra*.
   * **-c (ou - ação)**. Nível de acesso para a regra de Olá (negar ou permitir).
   * **-p (ou - protocol)**. Protocolo (Tcp, Udp ou *) para a regra de Olá.
   * **-r (ou - tipo)**. Direção de ligação (entrada ou saída).
   * **-y (ou - prioridade)**. Prioridade da regra de Olá.
   * **-f (ou - prefixo de endereço de origem)**. Prefixo de endereço de origem no CIDR ou utilizando etiquetas predefinidas.
   * **-o (ou - intervalo de portas de origem)**. Porta de origem ou intervalo de portas.
   * **-e (ou - prefixo de endereço de destino)**. Prefixo de endereço de destino no CIDR ou utilizando etiquetas predefinidas.
   * **-u (ou - intervalo de portas de destino)**. Porta de destino ou intervalo de portas.
5. Executar Olá  **`azure network nsg rule create`**  comando toocreate uma regra que permite acesso tooport 80 (HTTP) de Olá Internet.
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    Putput esperado:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. Executar Olá  **`azure network nsg subnet add`**  comando toolink Olá NSG toohello front-end sub-rede.
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    Resultado esperado:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Como toocreate Olá NSG para Olá novamente terminar sub-rede
toocreate com o nome de um NSG denominado *NSG-back-end* com base no cenário de Olá acima, siga os passos de Olá abaixo.

1. Executar Olá  **`azure network nsg create`**  comando toocreate um NSG.
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    Resultado esperado:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Parâmetros:
   
   * **-l (ou --location)**. Região do Azure onde hello novo NSG será criado. Para o nosso cenário *westus*.
   * **-n (ou --name)**. Nome para Olá novo NSG. Para o nosso cenário *NSG-front-end*.
2. Executar Olá  **`azure network nsg rule create`**  comando toocreate uma regra que permite acesso tooport 1433 (SQL) da sub-rede do front-end de Olá.
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    Resultado esperado:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. Executar Olá  **`azure network nsg rule create`**  comando toocreate uma regra que nega toohello de acesso à Internet.
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    Putput esperado:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. Executar Olá  **`azure network nsg subnet add`**  comando toolink Olá NSG toohello novamente sub-rede de fim.
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    Resultado esperado:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

