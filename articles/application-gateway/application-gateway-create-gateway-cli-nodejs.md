---
title: "aaaCreate um Gateway de aplicação do Azure - CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como toocreate um Gateway de aplicação utilizando Olá 1.0 CLI do Azure no Resource Manager"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Criar um gateway de aplicação utilizando Olá CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modelo do Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [CLI do Azure 1.0](application-gateway-create-gateway-cli.md)
> * [CLI 2.0 do Azure](application-gateway-create-gateway-cli.md)
> 
> 

O Application Gateway do Azure é um balanceador de carga de 7 camadas. Fornece ativação pós-falha, pedidos HTTP de encaminhamento de desempenho entre diferentes servidores, quer estejam na nuvem de Olá ou no local. Gateway de aplicação tem Olá seguintes funcionalidades de entrega de aplicações: carregar sondas de estado de funcionamento personalizado de balanceamento, afinidade de sessão com base em cookies e descarga de Secure Sockets Layer (SSL), HTTP e suporte para vários sites.

## <a name="prerequisite-install-hello-azure-cli"></a>Pré-requisito: Instalar Olá CLI do Azure

Olá tooperform os passos neste artigo, terá de demasiado[instalar Olá Interface de linha de comandos do Azure para Mac, Linux e Windows (CLI do Azure)](../xplat-cli-install.md) e terá de demasiado[iniciar sessão tooAzure](../xplat-cli-connect.md). 

> [!NOTE]
> Se não tiver uma conta do Azure, é necessário um. Subscreva [uma avaliação gratuita aqui](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Cenário

Neste cenário, saiba como toocreate um gateway de aplicação utilizando Olá portal do Azure.

Neste cenário irão:

* Crie um gateway de aplicação médias com duas instâncias.
* Crie uma rede virtual denominada ContosoVNET com um bloco CIDR reservado de 10.0.0.0/16.
* Crie uma sub-rede denominada subnet01 que utiliza 10.0.0.0/28 como bloco CIDR.

> [!NOTE]
> Pesquisas de configuração adicional do gateway de aplicação Olá, incluindo o estado de funcionamento personalizado, os endereços do conjunto de back-end e regras adicionais são configurados após a configuração do gateway de aplicação Olá e não durante a implementação inicial.

## <a name="before-you-begin"></a>Antes de começar

Gateway de aplicação do Azure requer a sua própria sub-rede. Ao criar uma rede virtual, certifique-se de que deixe suficiente toohave de espaço de endereço várias sub-redes. Depois de implementar uma sub-rede de tooa do gateway de aplicação, os gateways de aplicação apenas adicionais são toobe capaz de adicionado toohello sub-rede.

## <a name="log-in-tooazure"></a>Inicie sessão no tooAzure

Abra Olá **linha de comandos do Microsoft Azure**e inicie sessão. 

```azurecli-interactive
azure login
```

Depois de escrever Olá anterior exemplo, é fornecido um código. Navegue toohttps://aka.ms/devicelogin um processo de início de sessão do browser toocontinue Olá.

![o início de sessão do cmd que mostra dispositivos][1]

No browser Olá, introduza o código de Olá que recebeu. São tooa redirecionada-página sessão.

![código de tooenter do browser][2]

Assim que foi introduzido um código de Olá tem sessão iniciada, fechar Olá browser toocontinue com cenário Olá.

![sessão iniciada com êxito][3]

## <a name="switch-tooresource-manager-mode"></a>Comutador tooResource modo Manager

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de Olá

Antes de criar o gateway de aplicação Olá, o gateway de aplicação Olá toocontain é criado um grupo de recursos. seguinte Olá mostra comandos Olá.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Criar uma rede virtual

Após criar o grupo de recursos de Olá, uma rede virtual é criada para o gateway de aplicação Olá.  No seguinte exemplo de Olá, espaço de endereços de Olá foi como 10.0.0.0/16 como definido no Olá precedente notas de cenário.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Criar uma sub-rede

Depois de criar rede virtual Olá, é adicionada uma sub-rede de gateway de aplicação Olá.  Se planear toouse o gateway de aplicação com uma aplicação web alojadas no Olá mesmo virtual de rede como gateway de aplicação Olá, ser tooleave se tenha espaço suficiente para outra sub-rede.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Criar gateway de aplicação Olá

Assim que a rede virtual Olá e sub-rede são criados, pré-requisitos Olá Olá gateway de aplicação estão concluídos. Além de um. pfx exportado anteriormente certificado e Olá palavra-passe Olá certificado são necessários para Olá seguinte passo: endereços IP de Olá utilizados para o back-end de Olá são endereços IP de Olá para o servidor de back-end. Estes valores podem ser ambos IPs privados numa rede virtual Olá, os ips públicos ou nomes de domínio totalmente qualificados para os servidores de back-end.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Para obter uma lista de parâmetros que podem ser fornecidos durante a criação do executar Olá os seguintes comandos: **criar gateway de aplicação de rede do azure – ajudar**.

Este exemplo cria um gateway de aplicação básico com as predefinições para o serviço de escuta de Olá, conjunto back-end, as definições http de back-end e regras. Pode modificar estas definições toosuit a implementação depois de aprovisionamento de Olá é efetuada com êxito.
Se já tiver a sua aplicação web definida com o conjunto de back-end Olá no Olá precedente passos, uma vez criados, o balanceamento de carga é iniciada.

## <a name="next-steps"></a>Passos seguintes

Saiba como o estado de funcionamento personalizado toocreate sondas, visitando [criar uma sonda do Estado de funcionamento personalizado](application-gateway-create-probe-portal.md)

Saiba como tooconfigure descarga de SSL e de desencriptação de SSL dispendiosa do tirar Olá desativado seus servidores web, visitando [configurar a descarga de SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
