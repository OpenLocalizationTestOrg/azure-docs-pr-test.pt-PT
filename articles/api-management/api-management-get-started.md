---
title: aaaManage sua primeira API na API Management do Azure | Microsoft Docs
description: "Saiba como toocreate APIs, adicionar operações e começar a utilizar com a API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Gerir a sua primeira API na API Management do Azure
## <a name="overview"> </a>Descrição geral
Este guia mostra como tooquickly começar a utilizar a API Management do Azure e efetuar a primeira chamada de API.

## <a name="concepts"> </a>O que é a Gestão de API do Azure?
Pode utilizar qualquer back-end de API Management do Azure tootake e iniciar um programa de API totalmente funcional com base no mesmo.

Os cenários comuns incluem:

* **Proteção da infraestrutura móvel** mediante o controlo de acesso com chaves de API, prevenção de ataques DoS através da utilização de limitação ou utilização de políticas de segurança avançadas como a validação de token JWT.
* **Ativação de ecossistemas de parceiros ISV** , oferecendo integração rápida dos parceiros através de programação de Olá portal e a criação de um toodecouple fachada de API de implementações internas que não são ripe para consumo de parceiro.
* **Executar um programa de API interno** por oferecer uma localização centralizada para Olá organização toocommunicate sobre a disponibilidade de Olá e mais recentes alterações tooAPIs, controlo de acesso com base em contas organizacionais, todos os com base num canal seguro entre Olá gateway da API e Olá back-end.

sistema de Olá é constituído por Olá os seguintes componentes:

* Olá **gateway da API** é o ponto final de Olá que:
  
  * Aceita as chamadas de API e encaminha-os de back-ends de tooyour.
  * Verifica as chaves de API, os tokens JWT, os certificados e outras credenciais.
  * Impõe quotas de utilização e limites de velocidade.
  * Transforma a API no momento de Olá sem modificações no código.
  * Coloca em cache as respostas de back-end, quando estão configuradas.
  * Regista metadados de chamadas para fins de análise.
* Olá **portal do publicador** é a interface administrativa olá onde configurou o seu programa de API. Utilize-o para:
  
  * Definir ou importar o esquema de API.
  * Integrar APIs em produtos.
  * Configure políticas como quotas ou transformações nas APIs de Olá.
  * Obter conhecimentos aprofundados a partir da análise.
  * Gerir utilizadores.
* Olá **portal do programador** serve como Olá principal presença na web para os programadores, onde podem:
  
  * Ler a documentação da API.
  * Experimente uma API através da consola interativa Olá.
  * Criar uma conta e subscrever tooget API chaves.
  * Aceder a análises sobre a sua própria utilização.

## <a name="create-service-instance"> </a>Criar uma instância da Gestão de API
> [!NOTE]
> toocomplete neste tutorial, precisa de uma conta do Azure. Se não tiver uma conta, pode criar uma conta gratuita em apenas alguns minutos. Para obter mais detalhes, consulte [Azure Free Trial (Avaliação Gratuita do Azure)][Azure Free Trial].
> 
> 

Olá primeiro passo para trabalhar com a API Management é toocreate uma instância de serviço. Inicie sessão no toohello [Portal do Azure] [ Azure Portal] e clique em **novo**, **Web + móvel**, **API Management**.

![Nova instância da API Management][api-management-create-instance-menu]

Para **nome**, especifique um toouse de nome de subdomínio exclusivo para o URL do serviço Olá.

Escolha Olá pretendido **subscrição**, **grupo de recursos** e **localização** para a instância de serviço.

Introduza **Contoso Lda.** para Olá **nome da organização**e introduza o seu endereço de e-mail no Olá **E-Mail do administrador** campo.

> [!NOTE]
> Este endereço de correio eletrónico é utilizado para obter notificações do sistema de gestão de API de Olá. Para obter mais informações, consulte [como tooconfigure notificações e modelos de e-mail na API Management do Azure][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![Novo serviço da API Management][api-management-create-instance-step1]

As instâncias do serviço de API Management estão disponíveis em três camadas: Programador, Standard e Premium.

> [!NOTE]
> Olá camada de programador destina-se a desenvolvimento, teste e piloto programas de API em que a elevada disponibilidade não é uma preocupação. No Olá padrão e camadas Premium, pode dimensionar a sua toohandle de contagem de unidade reservada mais tráfego. camadas de Olá Standard e Premium fornecem o serviço de gestão de API com Olá mais potência de processamento e o desempenho. Pode concluir este tutorial utilizando qualquer camada. Para obter mais informações sobre as camadas de Gestão de API, consulte [Preços da Gestão de API][API Management pricing].
> 
> 

Clique em **criar** toostart aprovisionamento a instância de serviço.

![Novo serviço da API Management][api-management-instance-created]

Uma vez criada a instância de serviço Olá, o passo seguinte Olá é toocreate ou importar uma API.

## <a name="create-api"> </a>Importar uma API
Uma API consiste num conjunto de operações que podem ser invocadas a partir de uma aplicação cliente. Operações de API são efetuados tooexisting web.

Pode criar APIs (e adicionar operações) manualmente ou pode importá-las. Neste tutorial, iremos importar Olá API para um serviço de web de Calculadora exemplo fornecido pela Microsoft e alojado no Azure.

> [!NOTE]
> Para obter orientações sobre como criar uma API e adição manual de operações, consulte [como toocreate APIs](api-management-howto-create-apis.md) e [como tooadd operações tooan API](api-management-howto-add-operations.md).
> 
> 

As APIs são configuradas a partir do portal do publicador Olá. tooreach, clique em **portal do publicador** da barra de ferramentas do Olá serviço.

![Portal do publicador][api-management-management-console]

Calculadora de Olá tooimport API, clique em **APIs** de Olá **API Management** menu Olá à esquerda e, em seguida, clique em **API de importação**.

![Botão Importar API][api-management-import-api]

Execute os seguintes passos tooconfigure Olá API de calculadora de Olá:

1. Clique em **de URL**, introduza **http://calcapi.cloudapp.net/calcapi.json** para Olá **URL de documento de especificação** texto caixa e clique em Olá **Swagger**  botão de opção.
2. Tipo **calc** para Olá **sufixo do URL da API Web** caixa de texto.
3. Clique na Olá **produtos (opcionais)** caixa e escolha **Starter**.
4. Clique em **guardar** tooimport Olá API.

![Adicionar nova API][api-management-import-new-api]

> [!NOTE]
> A **API Management** suporta atualmente a versão 1.2 e 2.0 do documento Swagger para importação. Embora a [Especificação Swagger 2.0](http://swagger.io/specification) declare que as propriedades `host`, `basePath` e `schemes` são opcionais, o documento Swagger 2.0 **DEVE** conter essas propriedades; caso contrário, não será importado. 
> 
> 

Depois de Olá API for importada, hello página de resumo para a API de Olá é apresentada no portal do publicador Olá.

![Resumo da API][api-management-imported-api-summary]

Olá secção API tem vários separadores. Olá **resumo** separador apresenta métricas e informações sobre Olá API básicas. Olá [definições](api-management-howto-create-apis.md#configure-api-settings) separador utilizada tooview e editar Olá configuração é para uma API. Olá [operações](api-management-howto-add-operations.md) separador é operações Olá toomanage utilizados da API. Olá **segurança** separador pode ser tooconfigure utilizada a autenticação de gateway para o servidor de back-end Olá, utilizando a autenticação básica ou [autenticação de certificados mútuos](api-management-howto-mutual-certificates.md)e tooconfigure [ autorização do utilizador através da utilização de OAuth 2.0](api-management-howto-oauth2.md).  Olá **problemas** separador é problemas de tooview utilizados comunicados pelos programadores Olá que estão a utilizar as suas APIs. Olá **produtos** separador é produtos de Olá tooconfigure utilizados que contêm esta API.

Por predefinição, cada instância daAPI Management é fornecida com dois produtos de exemplo:

* **Inicial**
* **Ilimitado**

Neste tutorial, Olá API de calculadora básica foi adicionada toohello produto de arranque quando Olá API foi importada.

Na ordem toomake chamadas tooan API, os programadores têm primeiro de subscrever tooa produto que lhes dá acesso tooit. Os programadores podem subscrever tooproducts no portal de programador hello, ou os administradores podem subscrever tooproducts os programadores no portal do publicador Olá. É um administrador, uma vez que criou instância da API Management Olá no Olá passos anteriores no tutorial Olá, pelo que já são tooevery subscrito produto por predefinição.

## <a name="call-operation"></a>Chamar uma operação a partir do portal de programador Olá
As operações podem ser chamadas diretamente a partir do portal do programador Olá, que fornece uma maneira conveniente tooview e operações de Olá de uma API de teste. Este passo do tutorial, irá chamar Olá API de calculadora básica **adicionar dois números inteiros** operação. Clique em **portal do programador** a partir do menu de Olá em Olá principais direita do portal do publicador Olá.

![Portal do programador][api-management-developer-portal-menu]

Clique em **APIs** do menu superior Olá e, em seguida, clique em **calculadora básica** toosee Olá operações disponíveis.

![Portal do programador][api-management-developer-portal-calc-api]

Tenha em atenção as descrições de exemplo de Olá e os parâmetros que foram importados juntamente com Olá API e operações, que proporcionam documentação para programadores de Olá que irá utilizar esta operação. Estas descrições também podem ser adicionadas quando as operações são adicionadas manualmente.

Olá toocall **adicionar dois números inteiros** operação, clique em **experimente**.

![Experimente][api-management-developer-portal-calc-api-console]

Pode introduzir alguns valores para parâmetros de Olá ou mantenha as predefinições de Olá e, em seguida, clique em **enviar**.

![HTTP Get][api-management-invoke-get]

Após uma operação ser invocada, o portal do programador Olá apresenta Olá **estado de resposta**, Olá **cabeçalhos de resposta**e quaisquer **conteúdo da resposta**.

![Resposta][api-management-invoke-get-response]

## <a name="view-analytics"> </a>Ver análise
análise de tooview da calculadora básica, comutador back toohello portal do publicador ao selecionar **gerir** a partir do menu de Olá em Olá principais à direita do portal de programador Olá.

![Gerir][api-management-manage-menu]

Olá vista predefinida para o portal do publicador Olá é Olá **Dashboard**, que fornece uma descrição geral da sua instância da API Management.

![Dashboard][api-management-dashboard]

Rato de Olá paire sobre gráfico Olá para **calculadora básica** toosee métricas específicas de Olá da utilização de Olá do Olá API para um determinado período de tempo.

> [!NOTE]
> Se não vir quaisquer linhas no gráfico, mudar o portal do Programador de back-toohello e efetue algumas chamadas à API de Olá, aguarde alguns instantes e, em seguida, voltar toohello dashboard.
> 
> 

Clique em **ver detalhes** tooview Olá página de resumo Olá API, incluindo uma versão maior das métricas de Olá apresentado.

![Análise][api-management-mouse-over]

![Resumo][api-management-api-summary-metrics]

Para métricas e relatórios detalhados, clique em **análise** de Olá **API Management** menu Olá esquerda.

![Descrição geral][api-management-analytics-overview]

Olá **análise** secção tem Olá seguintes quatro separadores:

* **Rapidamente** fornece utilização global e métricas de estado de funcionamento, bem como Olá principais programadores, principais produtos, as principais APIs e operações superiores.
* **Utilização** fornece uma visão detalhada das chamadas à API e da largura de banda, incluindo uma representação geográfica.
* **Estado de funcionamento** concentra-se em códigos de estado, taxas de êxito de colocação em cache, tempos de resposta e tempos de resposta da API e do serviço.
* **Atividade** fornece relatórios detalhados sobre a atividade específica do Olá por programador, produto, API e operação.

## <a name="next-steps"> </a>Passos seguintes
* Saiba como demasiado[proteger a sua API com limites de velocidade](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
