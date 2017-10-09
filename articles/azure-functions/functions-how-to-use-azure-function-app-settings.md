---
title: "aaaConfigure as definições de aplicação de função do Azure | Microsoft Docs"
description: "Saiba como tooconfigure do Azure funcionar as definições de aplicação."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>Como toomanage uma aplicação de função Olá portal do Azure 

As funções do Azure, uma aplicação de função fornece o contexto de execução de Olá para as suas funções individuais. Comportamentos de aplicação de função aplicam funções tooall alojadas por uma aplicação de função especificada. Este tópico descreve como tooconfigure e gerir as suas aplicações de função no Olá portal do Azure.

toobegin, aceda toohello [portal do Azure](http://portal.azure.com) e iniciar sessão tooyour conta do Azure. Na barra de pesquisa de Olá, Olá parte superior do portal de Olá, escreva o nome de Olá da sua aplicação de função e selecione-o na lista de Olá. Depois de selecionar a sua aplicação de função, consulte Olá seguinte página:

![Descrição geral da aplicação de função no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>Separador de definições de aplicação de função

![Função descrição geral da aplicação no Olá portal do Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Olá **definições** separador é onde pode atualizar a versão de runtime de funções de Olá utilizado pela sua aplicação de função. Também é onde irá gerir Olá anfitrião as chaves utilizadas toorestrict HTTP acesso tooall funções alojadas pelo Olá aplicação de função.

As funções suporta o alojamento de consumo e planos de alojamento do serviço de aplicações. Para obter mais informações, consulte [plano de serviço correto Olá escolha para as funções do Azure](functions-scale.md). Para melhor previsão no plano de consumo Olá, funções permite-lhe limitar a utilização de plataforma, definindo uma quota de utilização diária, em gigabytes segundos. Assim que for atingida a quota de utilização diária Olá, a aplicação de função Olá está parada. Uma aplicação de função parada devido a atingir Olá gastos quota pode ser reativada da Olá mesmo contexto como estabelecer Olá diariamente gastos quota. Consulte Olá [das funções do Azure a página de preços](http://azure.microsoft.com/pricing/details/functions/) para obter detalhes sobre faturação.   

## <a name="platform-features-tab"></a>Separador de funcionalidades de plataforma

![Separador de funcionalidades de plataforma de aplicação de função.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

Aplicações de função executados na e são mantidas, pela plataforma do App Service do Azure de Olá. Como tal, as aplicações de função tem acesso toomost das funcionalidades de Olá da plataforma de alojamento na web principal do Azure. Olá **funcionalidades da plataforma** separador é onde o acesso Olá muitas funcionalidades de Olá plataforma de serviço de aplicações que pode utilizar nas suas aplicações de função. 

> [!NOTE]
> Nem todas as funcionalidades do serviço de aplicações estão disponíveis quando uma aplicação de função é executada no plano de alojamento de consumo de Olá.

resto Olá este tópico centra-se nos Olá seguintes funcionalidades do App Service no Olá portal do Azure que são úteis para as funções:

+ [Editor de serviço de aplicações](#editor)
+ [Definições da aplicação](#settings) 
+ [Console](#console)
+ [Ferramentas Avançadas (Kudu)](#kudu)
+ [Opções de implementação](#deployment)
+ [CORS](#cors)
+ [Autenticação](#auth)
+ [Definição da API](#swagger)

Para obter mais informações sobre como toowork com definições de serviço de aplicações, consulte [configurar definições de serviço de aplicações do Azure](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>Editor de serviço de aplicações

| | |
|-|-|
| ![Aplicação de função de editor do serviço de aplicações.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Olá editor do serviço de aplicações é um editor no portal avançado que pode utilizar os ficheiros de configuração do toomodify JSON e ficheiros de código igual. Escolha esta opção inicia um separador de browser separados com um editor de básico. Isto permite-lhe toointegrate com o código de execução e depuração do repositório de Git do Olá e modificar as definições de aplicação de função. Deste editor fornece um ambiente de desenvolvimento avançado para as suas funções comparada ao painel de aplicação de função do Olá predefinido.    |

![Olá editor do serviço de aplicações](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Definições da aplicação

| | |
|-|-|
| ![Definições de aplicação de aplicação de função.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | Olá do serviço de aplicações **definições da aplicação** painel é onde pode configurar e gerir versões framework, depuração remota, as definições de aplicação e as cadeias de ligação. Quando integrar a sua aplicação de função com outros serviços de terceiros e do Azure, pode modificar essas definições aqui. |

![Configurar as definições da aplicação](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Consola do

| | |
|-|-|
| ![Consola de aplicação de função na Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | consola no portal de Olá é uma ferramenta de programador ideal quando preferir toointeract com a sua aplicação de função a partir da linha de comandos Olá. Comandos comuns incluem o diretório e criação de ficheiros e navegação, bem como executar scripts e ficheiros batch. |

![Consola de aplicação de função](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Ferramentas Avançadas (Kudu)

| | |
|-|-|
| ![Aplicação de função Kudu no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Olá ferramentas avançadas para o serviço de aplicações (também conhecido como Kudu) fornecem acesso tooadvanced funcionalidades administrativas da sua aplicação de função. Do Kudu, gerir as informações do sistema, as definições de aplicação, as variáveis de ambiente, as extensões de site, os cabeçalhos de HTTP e variáveis de servidor. Também pode iniciar **Kudu** navegando toohello SCM o ponto final para a aplicação de função, como`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Configurar o Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Opções de implementação

| | |
|-|-|
| ![Opções de implementação de aplicação de função no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | As funções permite-lhe desenvolver o seu código de função no seu computador local. Em seguida, pode carregar o tooAzure de projeto de aplicação de função local. Além disso tootraditional carregamento FTP, as funções permite-lhe implementar a aplicação de função utilizando soluções de integração contínua popular, como o GitHub, VSTS, Dropbox, Bitbucket e outras pessoas. Para obter mais informações, consulte [a implementação contínua para as funções do Azure](functions-continuous-deployment.md). tooupload manualmente utilizando o FTP ou de local Git, terá também [configurar as suas credenciais de implementação](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Aplicação de função CORS no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | execução de código malicioso tooprevent nos seus serviços, blocos de serviço de aplicações chama tooyour função aplicações a partir de origens externas. As funções suporta recursos de várias origens de partilha toolet (CORS), definir uma "lista branca" de permitido origens a partir da qual as suas funções podem aceitar pedidos remotos.  |

![Configurar a aplicação de função CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Autenticação

| | |
|-|-|
| ![Autenticação de aplicação de função no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | Quando as funções de utilizam um acionador HTTP, pode exigir chamadas toofirst ser autenticado. Serviço de aplicações suporta a autenticação do Azure Active Directory e inicie sessão com fornecedores de redes sociais, como o Facebook, a Microsoft e o Twitter. Para obter detalhes sobre a configuração de fornecedores de autenticação específicas, consulte [descrição geral da autenticação do App Service do Azure](../app-service/app-service-authentication-overview.md). |

![Configurar a autenticação para uma aplicação de função](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>Definição da API

| | |
|-|-|
| ![API de aplicação de função swagger de definição de Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | As funções suporta Swagger tooallow clientes toomore consumir facilmente as funções acionadas por HTTP. Para obter mais informações sobre como criar definições de API com Swagger, visite [introdução à API Apps, ASP.NET e Swagger no Azure](../app-service-api/app-service-api-dotnet-get-started.md). Também pode utilizar os Proxies de funções toodefine uma único superfície de API para várias funções. Para obter mais informações, consulte [trabalhar com os Proxies de funções do Azure](functions-proxies.md). |

![Configurar a API da aplicação de função](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Passos seguintes

+ [Configurar as definições do App Service do Azure](../app-service-web/web-sites-configure.md)
+ [Implementação contínua para Funções do Azure](functions-continuous-deployment.md)



