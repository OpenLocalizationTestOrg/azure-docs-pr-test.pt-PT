---
title: "aaaHow tooCreate v1 um ambiente de serviço de aplicações"
description: "Descrição do fluxo de criação de um v1 de ambiente de serviço de aplicações"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>Como tooCreate v1 um ambiente de serviço de aplicações 

> [!NOTE]
> Este artigo é sobre Olá v1 de ambiente de serviço de aplicações. Há uma versão mais recente Olá ambiente de serviço de aplicações que é mais fácil toouse e é executada na infraestrutura mais poderosa. toolearn mais informações sobre a nova versão de Olá começar a utilizar Olá [introdução toohello ambiente de serviço de aplicações](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Descrição geral
Olá ambiente de serviço de aplicações (ASE) é uma opção de serviço Premium do serviço de aplicações do Azure que fornece uma capacidade de configuração avançada que não está disponível no carimbos de data / Olá multi-inquilino. funcionalidade de ASE Olá essencialmente implementa Olá App Service do Azure numa rede virtual do cliente. toogain uma maior compreensão das capacidades de Olá oferecida pelo ambientes do App Service ler Olá [o que é um ambiente de serviço de aplicações] [ WhatisASE] documentação.

### <a name="before-you-create-your-ase"></a>Antes de criar o seu ASE
É importante toobe em consideração aspetos Olá que não pode alterar. Os aspetos que não é possível alterar sobre o ASE depois de criado são:

* Localização
* Subscrição
* Grupo de Recursos
* VNet utilizado
* Sub-rede utilizada 
* Tamanho da sub-rede

Quando escolher uma VNet e especificar uma sub-rede, certifique-se de é suficientemente grande tooaccomodate qualquer crescimento futuro. 

### <a name="creating-an-app-service-environment-v1"></a>Criar uma aplicação do serviço ambiente v1
toocreate v1 um ambiente de serviço de aplicações tem de toosearch Olá Azure Marketplace para ***v1 de ambiente de serviço de aplicações***, ou acedendo através do novo -> Web + Mobile -> ambiente de serviço de aplicações. toocreate um ASEv1:

1. Forneça o nome de Olá da sua ASE. nome de Olá especificado para Olá ASE será utilizado para aplicações de Olá criadas no Olá ASE. Se o nome do Olá ASE é appsvcenvdemo, em seguida, o nome de subdomínio Olá seria. *appsvcenvdemo.p.azurewebsites.net*. Se, por conseguinte, criou uma aplicação com o nome *mytestapp* , em seguida, seria possível endereçável em *mytestapp.appsvcenvdemo.p.azurewebsites.net*. Não é possível utilizar o espaço em branco no nome de Olá da sua ASE. Se utilizar carateres maiúsculos no nome de Olá, o nome de domínio Olá será versão em minúsculas total Olá com esse nome. Se utilizar um ILB, em seguida, o nome da sua ASE não é utilizado na sua subdomínio mas em vez disso, é explicitamente indicado durante a criação de ASE
   
    ![][1]
2. Selecione a sua subscrição. subscrição de Olá utilizada para a sua ASE também é Olá um que todas as aplicações em que ASE serão criadas com. Não é possível colocar o seu ASE numa VNet que está a ser outra subscrição
3. Selecione ou especifique um novo grupo de recursos. grupo de recursos de Olá utilizado para a sua ASE tem Olá mesmo que é utilizado para a sua VNet. Se selecionar uma VNet já existente, em seguida, seleção de grupo de recursos de Olá para sua ASE será tooreflect atualizada da sua VNet.
   
    ![][2]
4. Certifique-as com as suas seleções de rede Virtual e a localização. Pode escolher toocreate uma nova VNet ou selecione uma VNet já existente. Se selecionar uma nova VNet, em seguida, pode especificar um nome e localização. Olá nova VNet terá Olá endereço intervalo 192.168.250.0/23 e uma sub-rede designada **predefinido** que está definida como 192.168.250.0/24. Pode também simplesmente selecionar um pré-existente clássico ou do VNet do Resource Manager. Olá a seleção do tipo de VIP determina se o ASE pode ser acedido diretamente partir Olá internet (externa) ou se utiliza um balanceador de carga interno (ILB). mais sobre os mesmos ler toolearn [através de um balanceador de carga interno com um ambiente de serviço de aplicações][ILBASE]. Se selecionar um tipo de VIP de externo, em seguida, pode selecionar é criado com a quantos sistema de Olá de endereços IP externos para fins IPSSL. Se selecionar interno, em seguida, terá de subdomínio de Olá toospecify que irá utilizar o seu ASE. ASEs podem ser implementados em redes virtuais que utilizam *ou* intervalos de endereços públicos, *ou* RFC1918 espaços de endereços (ou seja, endereços privados). Ordem toouse uma rede virtual com um intervalo de endereços públicos, terá toocreate Olá VNet antecedência. Quando seleciona uma VNet já existente, terá de toocreate uma nova sub-rede durante a criação de ASE. **Não é possível utilizar uma sub-rede previamente criada no portal de Olá. Pode criar ASE com uma sub-rede pré-existente se criar a sua ASE utilizando um modelo do resource manager.** toocreate ASE a partir de um modelo utilizar informações de Olá aqui [criar um ambiente de serviço de aplicações a partir do modelo] [ ILBAseTemplate] e aqui, [criar um ambiente de serviço de aplicações do ILB a partir do modelo] [ASEfromTemplate].

### <a name="details"></a>Detalhes
ASE é criado com termina de front-2 e 2 Workers. Olá front-termina atuar como pontos finais HTTP/HTTPS Olá e enviar tráfego toohello funcionários que são funções de Olá que alojam as suas aplicações. Pode ajustar a quantidade de Olá após a criação de ASE e pode ainda configurar regras de dimensionamento automático nestes agrupamentos de recursos. Para obter mais detalhes em torno de dimensionamento manual, gestão e monitorização de um ambiente de serviço de aplicação aceda aqui: [como tooconfigure um ambiente de serviço de aplicações][ASEConfig] 

Pode existir apenas Olá um ASE na sub-rede Olá utilizado pelo Olá ASE. Não é possível utilizar a sub-rede de Olá para tudo o que não sejam Olá ASE

### <a name="after-app-service-environment-v1-creation"></a>Após a criação do ambiente de serviço de aplicações v1
Após a criação de ASE pode ajustar:

* Quantidade de front-termina (mínimo: 2)
* Quantidade de trabalhadores (mínimo: 2)
* Quantidade de endereços IP disponíveis para IP SSL
* Os tamanhos de recursos utilizados por Olá termina Front ou trabalhadores de computação (o tamanho mínimo de Front-End é P2)

Existem mais detalhes em torno do manual de dimensionamento, gestão e monitorização dos ambientes do App Service aqui: [como tooconfigure um ambiente de serviço de aplicações][ASEConfig] 

Para obter informações sobre o dimensionamento automático é um guia aqui: [como dimensionamento automático de tooconfigure para um ambiente de serviço de aplicações][ASEAutoscale]

Não existem dependências adicionais que não estão disponíveis para personalização, tais como a base de dados de Olá e armazenamento. Estes são processadas pelo Azure e são fornecidos com o sistema de Olá. Olá sistema armazenamento suporta a cópia de segurança too500 GB para Olá todo ambiente de serviço de aplicações e a base de dados de Olá é ajustada pelo Azure, conforme necessário para a escala de Olá do sistema de Olá.

## <a name="getting-started"></a>Introdução
Todos os artigos e como-a para ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).

tooget começar v1 de ambiente de serviço de aplicações, consulte [introdução toohello v1 de ambiente de serviço de aplicações][WhatisASE]

Para obter mais informações sobre a plataforma do App Service do Azure de Olá, consulte [App Service do Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
