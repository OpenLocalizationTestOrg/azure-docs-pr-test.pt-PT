---
title: aaaExporting um tooPowerApps alojado no Azure API e a Microsoft Flow | Microsoft Docs
description: "Descrição geral de como tooexpose uma API alojada no App Service tooPowerApps e Microsoft Flow"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Exportar um tooPowerApps alojado no Azure API e a Microsoft Flow

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Criar conectores personalizados para PowerApps e Microsoft Flow

[PowerApps](https://powerapps.com) é um serviço para criar e utilizar aplicações empresariais personalizadas que ligar tooyour dados e a trabalham entre plataformas. [Microsoft Flow](https://flow.microsoft.com) torna tooautomate fácil fluxos de trabalho e os processos de negócios entre os seus serviços e aplicações favoritas. PowerApps e Microsoft Flow vêm com uma variedade de origens de toodata conectores incorporados, tais como o Office 365, Dynamics 365, Salesforce e muito mais. No entanto, os utilizadores também precisam de origens de dados de capacidade tooleverage toobe e APIs que está a ser criadas pela respetiva organização.

Da mesma forma, os programadores que pretendem tooexpose das respetivas APIs de mais amplamente dentro Olá organização poderá querer toomake respetivo tooPowerApps disponíveis APIs e Microsoft Flow utilizadores. Este tópico mostra como tooexpose uma API criada com o App Service do Azure ou as funções do Azure tooPowerApps e Flow Microsoft. [App Service do Azure](https://azure.microsoft.com/services/app-service/) é uma oferta de plataforma-como-um-serviço que permite aos programadores tooquickly e facilmente web de nível empresarial de compilação, móveis e aplicações API. [As funções do Azure](https://azure.microsoft.com/services/functions/) é uma solução baseada em eventos computação sem servidor que permite-lhe o código de autor tooquickly que possam reagir tooother partes do sistema e escala com base no pedido.

toolearn mais informações sobre estes serviços, consulte:
- [PowerApps orientado Learning](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Fluxo de Microsoft orientado Learning](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [O que é o Serviço de Aplicações?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [O que é das funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Partilha uma definição de API

APIs, muitas vezes, são descritas utilizando um [OpenAPI documento](https://www.openapis.org/) (algumas vezes referido tooas um documento de "Swagger"). Contém todas Olá informações sobre as operações que estão disponíveis e como os dados de Olá devem ser estruturados. PowerApps e Microsoft Flow podem criar conectores personalizados para qualquer documento OpenAPI 2.0. Depois de um conetor personalizado é criado, pode ser utilizado no exatamente Olá mesma forma que um dos Olá conectores incorporados e rapidamente pode ser integrada numa aplicação.

Azure App Service e as funções do Azure têm [suporte incorporado](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) para criar, alojar e gerir um documento de OpenAPI. Ordem toocreate um conetor personalizado para um web, móveis, a API ou a aplicação de função, PowerApps e fluxo necessário toobe dada uma cópia da definição de Olá.

> [!NOTE]
> Porque está a ser utilizada uma cópia da definição da API de Olá, PowerApps e Microsoft Flow não imediatamente saberá sobre atualizações ou última alterações toohello aplicação. Se é disponibilizada uma nova versão da API de Olá, estes passos devem ser repetidos para versão Olá de novo. 

tooprovide PowerApps e Flow Microsoft com a definição da API de Olá alojado para a sua aplicação, siga estes passos:

1. Abra Olá [Portal do Azure](https://portal.azure.com) e navegue tooyour aplicação do serviço de aplicações ou funções do Azure.

    Se utilizar o App Service do Azure, selecione **definição da API** da lista de definições de Olá. 
    
    Se utilizar as funções do Azure, selecione a sua aplicação de função e, em seguida, escolha **funcionalidades da plataforma**e, em seguida, **definição da API**. Também pode optar por tooopen Olá **definição da API (pré-visualização)** separador em vez disso.

2. Se tiver sido fornecida uma definição de API, verá um **exportar tooPowerApps + Microsoft Flow** botão. Clique neste processo de exportação do botão toobegin Olá.

3. Selecione Olá **exportação modo**. Isto determina passos Olá, terá de toofollow toocreate um conector. App Service oferece duas opções para fornecer PowerApps e Flow Microsoft com a definição da API:

    **Express** Olá, permite criar Olá personalizado conector a partir no portal do Azure. Requer que Olá atual utilizador com sessão iniciada tem conectores de toocreate permissão no ambiente de destino Olá. Este é Olá abordagem recomendada se este requisito pode ser cumprido. Se utilizar este modo, siga Olá [Express exportação](#express) instruções abaixo.

    **Manual** permite exportar uma cópia do Olá API definiton que possam ser importado Olá PowerApps ou Microsoft Flow portais. Este é Olá abordagem recomendada se hello utilizador Olá com conectores de toocreate de permissão e de utilizador do Azure são diferentes pessoas ou se precisar de conector Olá toobe criado no outro inquilino. Se utilizar este modo, siga Olá [Manual exportação e importação](#manual) instruções abaixo.

<a name="express"></a>
## <a name="express-export"></a>Exportação rápida

Nesta secção, irá criar um novo conector personalizado do dentro Olá portal do Azure. Tem de ter sessão iniciada em Olá inquilino toowhich desejar tooexport e tem de ter permissão toocreate um conetor personalizado no ambiente de destino Olá.

1. Selecione o ambiente de Olá na qual gostaria de conector de Olá toocreate. Em seguida, forneça um nome para o conetor personalizado.

2. Se a definição da API inclui quaisquer definições de segurança, estes serão ser realçadas no passo #2. Se necessário, forneça segurança Olá detalhes de configuração necessitam acesso de utilizadores toogrant tooyour API. Para obter mais informações, consulte [autenticação](#auth) abaixo. 

3. Clique em **OK** toocreate seu conector personalizado.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Manual exportação e importação

Na ordem toocreate um conetor personalizado para um web, móveis, a API ou a aplicação de função, serão necessários dois passos:

1. [Ao obter a definição da API Olá do serviço de aplicações ou funções do Azure](#export)
2. [Importar definição de API de Olá para PowerApps e Microsoft Flow](#import)

É possível que estes dois passos necessário toobe levada a cabo por separado indivíduos numa organização, como um utilizador especificado pode não ter permissão tooperform ambas as ações. Neste caso, um programador, que tem acesso de contribuinte toohello aplicação do serviço de aplicações ou funções do Azure terá de definição de Olá API tooobtain (um único ficheiro JSON) ou um tooit de ligação. Será, em seguida, precisam de tooprovide esse PowerApps ou Microsoft Flow proprietário tooa de definição. Esse proprietário pode utilizar o conector personalizado do Olá metadados toocreate Olá.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>Ao obter a definição da API Olá do serviço de aplicações ou funções do Azure

Nesta secção, irá exportar a definição da API para a API de serviço de aplicações, toobe utilizado mais tarde no portal de PowerApps ou Microsoft Flow Olá Olá.

1. Pode escolher tooeither **transferir definição Olá API** ou **obtenha uma ligação**. Que escolher, o resultado de Olá será fornecido na secção seguinte, Olá. Selecione uma destas opções e siga as instruções de Olá.
 
2. Se a definição da API inclui quaisquer definições de segurança, estes serão ser realçadas no passo #2. Durante a importação, PowerApps e Microsoft Flow irão detetar estes e solicita a informações de segurança. Recolha Olá credenciais tooeach relacionados definição para utilização na secção seguinte, Olá. Para obter mais informações, consulte [autenticação](#auth) abaixo. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>Importar definição de API de Olá para PowerApps e Microsoft Flow

Nesta secção, irá criar um conetor personalizado no PowerApps e Flow Microsoft utilizando a definição de Olá API que obteve anteriormente. Conectores personalizados são partilhados entre Olá dois serviços, pelo que necessita apenas de definição de Olá tooimport uma vez. Para obter mais informações sobre conectores personalizadas, consulte [registar e utilizar conectores personalizados no PowerApps] e [registar e utilizar conectores personalizados no Microsoft Flow].

1. Abra Olá [portal web do Powerapps](https://web.powerapps.com) ou Olá [portal web do Microsoft Flow](https://flow.microsoft.com/)e iniciar sessão. 

2. Clique em Olá **definições** botão (ícone de engrenagem Olá) no canto superior direito de Olá da página Olá e selecione **conectores personalizada**. 

3. Clique em **criar conector personalizado**.

4. No Olá **geral** separador, forneça um nome para a API e, em seguida, carregue a definição de OpenAPI Olá ou cole o URL de metadados de Olá. Clique em **continuar**.

4. No Olá **segurança** separador, se for pedido tooprovide detalhes de autenticação, introduza valores Olá obtidos na secção anterior Olá. Caso contrário, avance toohello próximo passo.

5. No Olá **definições** separador, todas as operações de Olá definidas no seu ficheiro OpenAPI são povoadas de automática. Se a todas as operações necessárias são definidas, pode aceder toohello próximo passo. Caso contrário, pode adicionar e modificar operações aqui.

6. Clique em **criar conector**. Se quiser tootest chamadas de API, aceda toohello próximo passo.

7. No Olá **teste** separador, criar uma ligação, selecione uma operação tootest e introduza todos os dados necessários para a operação de Olá.

8. Clique em **testar operação**.


<a name="auth"></a>
## <a name="authentication"></a>Autenticação

PowerApps e Microsoft Flow suportam nativamente o uma coleção de fornecedores de identidade que podem ser utilizado toolog os utilizadores do seu conector personalizado. Se a sua API requer autenticação, certifique-se de que é capturado como uma _definição de segurança_ no seu documento OpenAPI. Durante a exportação, terá de valores de configuração de tooprovide permitem PowerApps uma ação de início de sessão do Microsoft Flow tooperform.

Esta secção inclui os tipos de autenticação de Olá que são suportados pelo fluxo rápida Olá: chave de API, Azure Active Directory e genérico OAuth 2.0. Para obter uma lista completa de fornecedores e as credenciais de Olá requer que cada um, consulte [registar e utilizar conectores personalizados no PowerApps] e [registar e utilizar conectores personalizados no Microsoft Flow].

### <a name="api-key"></a>Chave de API
Quando é utilizada este esquema de segurança, os utilizadores de Olá do seu conector serão chave do pedido tooprovide Olá quando criam uma ligação. Pode fornecer um toohelp do nome da chave de API-lhes saber qual a chave é necessária. Para as funções do Azure, normalmente, será uma das chaves de anfitrião Olá, que abrangem várias funções dentro da aplicação de função Olá.

### <a name="azure-active-directory"></a>Azure Active Directory
Quando configurar um conector personalizado que requer o início de sessão do AAD, são necessários dois registos de aplicações do AAD: uma API de back-end de Olá toomodel e um conector de Olá toomodel PowerApps e fluxo.

A API deve ser configurado toowork com registo primeiro Olá e este será já ser Tratado se utilizou Olá [aplicação serviço de autenticação/autorização](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) funcionalidade.

Terá de toomanually criar registo de segundo Olá conector Olá, utilizando os passos de Olá abrangidos [adicionar uma aplicação AAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Olá registo tem toohave delegado acesso tooyour API e um URL de resposta de `https://msmanaged-na.consent.azure-apim.net/redirect`. Consulte [neste exemplo](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) para obter mais detalhes, substituindo a sua API para Olá do Azure Resource Manager.

Olá, os seguintes valores de configuração é necessário:
- **ID de cliente** -Olá ID de cliente do seu conector registo do AAD
- **Segredo do cliente** -segredo do cliente Olá do seu conector registo do AAD
- **URL de início de sessão** - hello base URL para o AAD. No Azure público, normalmente, será `https://login.windows.net`.
- **ID de inquilino** -Olá ID Olá inquilino toobe utilizado para início de sessão Olá. Isto deve ser "comum" ou Olá ID do inquilino Olá no qual Olá conector está a ser criado.
- **URL de recurso** -Olá URL de recursos de registo do AAD de back-end da API

> [!IMPORTANT]
> Se outra pessoa importar definição de Olá API PowerApps e Flow Microsoft como parte do fluxo de Olá manual, terá de tooprovide-los com o segredo de cliente e o ID de cliente de Olá **de registo do conetor Olá**, bem como o URL de recurso de Olá da sua API. Certifique-se de que estes segredos são geridos de forma segura. **Não partilhe credenciais de segurança de Olá de Olá API próprio.**

### <a name="generic-oauth-20"></a>Genérico OAuth 2.0
suporte de OAuth 2.0 genérico Olá permite-lhe toointegrate com qualquer fornecedor de OAuth 2.0. Isto permite-lhe toobring em qualquer fornecedor personalizado que não é suportado nativamente.

Olá, os seguintes valores de configuração é necessário:
- **ID de cliente** -Olá ID de cliente OAuth 2.0
- **Segredo do cliente** -segredo do cliente Olá OAuth 2.0
- **URL de autorização** -Olá URL de autorização do OAuth 2.0
- **URL do token** -Olá URL do token OAuth 2.0
- **Atualizar o URL** -Olá URL de atualização de OAuth 2.0



[registar e utilizar conectores personalizados no PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[registar e utilizar conectores personalizados no Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/
