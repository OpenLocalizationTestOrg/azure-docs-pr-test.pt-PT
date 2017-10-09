---
title: aaaDeploy, chamar e autenticar as APIs web e REST APIs de Azure Logic Apps | Microsoft Docs
description: "Implementar, autenticar e chamar web APIs e REST APIs em fluxos de trabalho para integrações de sistema com Azure Logic Apps"
keywords: "Web APIs, REST APIs, conectores, fluxos de trabalho, integrações de sistema, autenticar"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Implementar, chamar e autenticar APIs personalizadas que os conectores para aplicações lógicas

Depois de [criar APIs personalizadas](./logic-apps-create-api-app.md) que fornecer ações ou acionadores toouse na lógica de fluxos de trabalho de aplicações, tem de implementar as suas APIs antes de poder chamá-los. E embora pode chamar qualquer API a partir de uma aplicação lógica, para melhor experiência de Olá, adicione [metadados do Swagger](http://swagger.io/specification/) que descreve a API operações e parâmetros. Este ficheiro Swagger ajuda a sua API funcionar melhor e mais facilmente integrar com logic apps.

Pode implementar as suas APIs como [aplicações web](../app-service-web/app-service-web-overview.md), mas a considerar implementar as suas APIs como [das API apps](../app-service-api/app-service-api-apps-why-best-platform.md), que pode fazer com que a tarefa mais fácil quando criar, alojar e consumir APIs na nuvem de Olá e no local. Toochange não tem qualquer código na sua APIs – basta implementar a aplicação de API de tooan de código. Pode alojar as suas APIs em [App Service do Azure](../app-service/app-service-value-prop-what-is.md), um plataforma-como-um-serviço (PaaS) que fornece uma das formas mais dimensionáveis, mais fácil e prática de Olá para alojar a API da oferta.

tooauthenticate chamadas de logic apps tooyour APIs, pode definir cópias de segurança do Azure Active Directory no Olá portal do Azure, para que não tenha tooupdate seu código. Em alternativa, pode exigir e impor a autenticação através de código da API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Implementar a sua API como uma aplicação web ou aplicação API

Antes de poder chamar a API personalizada a partir de uma aplicação lógica, implemente a sua API como uma aplicação web ou tooAzure de aplicação de API do serviço de aplicações. Além disso, toomake o documento Swagger ser lido pelo Olá Designer de aplicação lógica, definir as propriedades da definição Olá API e ative [recursos de várias origens (CORS) de partilha](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) para a sua aplicação web ou aplicação API.

1. No portal do Azure Olá, selecione a aplicação web ou aplicação API.

2. No painel de Olá que abre-se, em **API**, escolha **definição da API**. Conjunto Olá **localização de definição de API** toohello URL para o ficheiro swagger.json.

   Normalmente, o URL de Olá aparece neste formato:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Ficheiro de tooSwagger de ligação para a API personalizada](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. Em **API**, escolha **CORS**. Definir políticas CORS Olá para **permitido origens** demasiado**'*'** (permitir todos os).

   Esta definição permite pedidos a partir do Designer de aplicação lógica.

   ![Permitir pedidos de API do Designer de aplicação lógica tooyour personalizada](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Para obter mais informações, consulte estes artigos:

* [Adicionar metadados do Swagger para as APIs de web ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Implementar o ASP.NET web APIs tooAzure do serviço de aplicações](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Chamar a API personalizada da lógica de fluxos de trabalho da aplicação

Depois de configurar as propriedades da definição Olá API e CORS, acionadores e ações a API personalizada devem ficar disponíveis para tooinclude no seu fluxo de trabalho de aplicação lógica. 

*  tooview Olá Web sites que tenham Swagger URLs, pode procurar os Web sites subscrição Olá Designer de aplicações lógicas.

*  ações disponíveis tooview e entradas por apontar um documento Swagger, utilize Olá [HTTP + Swagger ação](../connectors/connectors-native-http-swagger.md).

*  toocall qualquer API, incluindo as APIs que não têm ou expor um documento Swagger, pode criar um pedido sempre com Olá [ação HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Autenticar chamadas tooyour personalizado API

Pode proteger chamadas tooyour API personalizada nas seguintes formas:

* [Sem alterações de código](#no-code): proteger a sua API com [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) através do portal do Azure Olá, por isso, não tem tooupdate código ou Reimplementar a sua API.

  > [!NOTE]
  > Por predefinição, a autenticação do Azure AD Olá ativassem no portal do Azure de Olá não fornece autorização detalhada. Por exemplo, esta autenticação bloqueia toojust sua API, um inquilino específico, não tooa utilizador específico ou aplicação. 

* [Atualizar o código da API](#update-code): proteger a sua API através da imposição [autenticação de certificado](#certificate), [autenticação básica](#basic), ou [autenticação do Azure AD](#azure-ad-code) através de código.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Autenticar chamadas tooyour API sem alterar o código

Eis os passos gerais de Olá para que este método:

1. Criar dois [identidades de aplicação do Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): um para a sua aplicação lógica e um para a sua aplicação web (ou a aplicação API).

2. tooauthenticate chamadas tooyour API, utilizar credenciais de Olá (ID de cliente e segredo) para Olá [principal de serviço](../app-service-api/app-service-api-dotnet-service-principal-auth.md) que está associada a Olá identidade da aplicação do Azure AD para a sua aplicação lógica.

3. Inclua aplicação Olá IDs na sua definição de aplicação lógica.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Parte 1: Criar uma identidade de aplicação do Azure AD para a sua aplicação lógica

A aplicação lógica utiliza este tooauthenticate de identidade de aplicação do Azure AD no Azure AD. Só tem tooset se esta identidade de uma vez para o seu diretório. Por exemplo, pode escolher toouse Olá a mesma identidade para todas as suas logic apps, mesmo que pode criar identidades únicas de cada aplicação lógica. Pode configurar estas identidades no portal do Azure, de Olá [portal clássico do Azure](#app-identity-logic-classic), ou utilize [PowerShell](#powershell).

**Criar a identidade da aplicação Olá para a sua aplicação lógica no Olá portal do Azure**

1. No Olá [portal do Azure](https://portal.azure.com "https://portal.azure.com"), escolha **do Azure Active Directory**. 

2. Confirme que é no Olá mesmo diretório que a sua aplicação web ou aplicação API.

   > [!TIP]
   > tooswitch diretórios, clique em seu perfil e selecione outro diretório. Em alternativa, escolha **descrição geral** > **diretório comutador**.

3. No menu de diretório Olá, sob **gerir**, escolha **registos de aplicação** > **novo registo de aplicação**.

   > [!TIP]
   > Por predefinição, a lista de registos de aplicações de Olá mostra todos os registos de aplicação no seu diretório. tooview apenas seja os registos de aplicações, caixa de pesquisa de toohello seguinte, selecione **as minhas aplicações**. 

   ![Criar novo registo de aplicação](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Dê um nome a sua identidade de aplicação, deixe **tipo de aplicação** definido demasiado**aplicação Web / API**, forneça um exclusivo cadeia formatada como um domínio para **URL de início de sessão**e escolha  **Criar**.

   ![Forneça um nome e início de sessão no URL para a identidade da aplicação](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   a identidade da aplicação Olá que criou para a sua aplicação lógica agora é apresentado na lista de registos de aplicações de Olá.

   ![Identidade da aplicação para a sua aplicação lógica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Na lista de registos de aplicação Olá, selecione a sua identidade de aplicação nova. Copie e guarde Olá **ID da aplicação** toouse como Olá "ID de cliente" para a sua aplicação lógica na parte 3.

   ![Copie e guarde o ID da aplicação para a aplicação lógica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Se as definições de identidade da aplicação não estão visíveis, escolha **definições** ou **todas as definições**.

7. Em **acesso à API**, escolha **chaves**. Em **Descrição**, forneça um nome para a sua chave. Em **expira**, selecione uma duração para a sua chave.

   chave de Olá que estiver a criar atua como da identidade da aplicação Olá "secreta" ou palavra-passe para a sua aplicação lógica.

   ![Crie uma chave para a identidade de aplicação lógica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Na barra de ferramentas Olá, escolha **guardar**. Em **valor**, agora é apresentada a sua chave. 
**Certifique-se de que toocopy e guardar a chave de** para utilização posterior porque a chave de Olá está oculto quando deixar painel chaves Olá.

   Quando configura a sua aplicação lógica em parte 3, especifique esta chave como Olá "secreta" ou a palavra-passe.

   ![Copie e guarde a chave para utilizar mais tarde](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Criar a identidade da aplicação Olá para a sua aplicação lógica no Olá portal clássico do Azure**

1. No portal clássico do Azure de Olá, escolha [ **do Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Selecione Olá mesmo diretório que utiliza para a sua aplicação web ou aplicação API.

3. No Olá **aplicações** separador, escolha **adicionar** em Olá parte inferior da página Olá.

4. Dê um nome a sua identidade da aplicação e escolha **seguinte** (seta para a direita).

5. Em **as propriedades da aplicação**, forneça um exclusivo cadeia formatada como um domínio para **URL de início de sessão** e **URI de ID de aplicação**e escolha **concluída** (marca de verificação).

6. No Olá **configurar** separador, copie e guarde Olá **ID de cliente** para sua toouse de aplicação lógica na parte 3.

7. Em **chaves**, abra Olá **selecione duração** lista. Selecione uma duração para a sua chave.

   chave de Olá que estiver a criar atua como da identidade da aplicação Olá "secreta" ou palavra-passe para a sua aplicação lógica.

8. Em Olá parte inferior da página Olá, escolha **guardar**. Poderá ter toowait alguns segundos.

9. Em **chaves**, certifique-se de que toocopy e guardar a chave de Olá que aparece. 

   Quando configura a sua aplicação lógica em parte 3, especifique esta chave como Olá "secreta" ou a palavra-passe.

Para obter mais informações, saiba como demasiado [configurar o início de sessão de Azure Active Directory de toouse de aplicação do serviço de aplicações](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Criar a identidade da aplicação Olá para a sua aplicação lógica no PowerShell**

Pode efetuar esta tarefa através do Azure Resource Manager com o PowerShell. No PowerShell, execute estes comandos:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Certifique-se de que toocopy Olá **ID do inquilino** Olá GUID para o seu inquilino do Azure AD, **ID da aplicação**e Olá palavra-passe que utilizou.

Para obter mais informações, saiba como demasiado [criar um principal de serviço com o PowerShell tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Parte 2: Criar uma identidade de aplicação do Azure AD para a sua aplicação web ou aplicação API

Se já estiver implementada a sua aplicação web ou aplicação API, pode ativar a autenticação e criar a identidade da aplicação Olá no Olá portal do Azure. Caso contrário, pode [ativar a autenticação quando implementar com um modelo Azure Resource Manager](#authen-deploy). 

**Criar a identidade da aplicação Olá e ativar a autenticação no Olá portal do Azure para as aplicações implementadas**

1. No Olá [portal do Azure](https://portal.azure.com "https://portal.azure.com"), localize e selecione a sua aplicação web ou aplicação API. 

2. Em **definições**, escolha **autenticação/autorização**. Em **autenticação do serviço de aplicações**, ativar a autenticação **no**. Em **fornecedores de autenticação**, escolha **do Azure Active Directory**.

   ![Ativar a autenticação](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Agora crie uma identidade de aplicação para a sua aplicação web ou aplicação API, conforme mostrado aqui. No Olá **definições do Azure Active Directory** painel, defina **modo de gestão** demasiado**Express**. Escolha **criar nova aplicação AD**. Dê um nome a sua identidade da aplicação e escolha **OK**. 

   ![Criar a identidade da aplicação para a sua aplicação web ou aplicação API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. No Olá **autenticação / painel autorização**, escolha **guardar**.

Agora tem de localizar o ID de cliente Olá e ID de inquilino para a identidade da aplicação Olá associado à sua aplicação web ou aplicação API. Utilize estes IDs de parte 3. Para continuar com estes passos para Olá portal do Azure ou [portal clássico do Azure](#find-id-classic).

**Encontrar o ID de cliente da identidade da aplicação e ID de inquilino para a sua aplicação web ou aplicação API no Olá portal do Azure**

1. Em **fornecedores de autenticação**, escolha **do Azure Active Directory**. 

   ![Escolha "Do Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. No Olá **definições do Azure Active Directory** painel, defina **modo de gestão** demasiado**avançadas**.

3. Olá cópia **ID de cliente**e guarde este GUID para utilização na parte 3.

   > [!TIP] 
   > Se **ID de cliente** e **Url do emissor** não aparecer, tente atualizar Olá portal do Azure e repita o passo 1.

4. Em **Url do emissor**, copie e guarde hello apenas o GUID para parte 3. Também pode utilizar este GUID na sua aplicação web ou modelo de implementação da aplicação API, se necessário.

   Este GUID é o GUID do seu inquilino específico ("ID do inquilino") e deve aparecer neste URL:`https://sts.windows.net/{GUID}`

5. Sem guardar as alterações, feche Olá **definições do Azure Active Directory** painel.

<a name="find-id-classic"></a>

**Encontrar o ID de cliente da identidade da aplicação e ID de inquilino para a sua aplicação web ou aplicação API no Olá portal clássico do Azure**

1. No portal clássico do Azure de Olá, escolha [ **do Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Selecione o diretório de Olá que utiliza para a sua aplicação web ou aplicação API.

3. No Olá **pesquisa** caixa, localize e selecione a identidade da aplicação Olá para a sua aplicação web ou aplicação API.

4. No Olá **configurar** separador, Olá cópia **ID de cliente**e guarde este GUID para utilização na parte 3.

5. Depois de obter o ID de cliente Olá, na parte inferior de Olá de Olá **configurar** separador, escolha **ver pontos finais**.

6. Copie o URL de Olá para **documento de metadados de Federação**e procure toothat URL.

7. No documento de metadados de Olá que se abre, determinar a raiz de Olá **EntityDescriptor ID** elemento, que tem um **entityID** atributo neste formulário:`https://sts.windows.net/{GUID}` 

      Olá GUID neste atributo é o GUID do seu inquilino específico (ID de inquilino).

8. Copie o ID do inquilino Olá e guarde este ID para utilização na parte 3 e também toouse na sua aplicação web ou modelo de implementação da aplicação API, se necessário.

Para obter mais informações, consulte estes tópicos:

* [Autenticação de utilizador para API apps no App Service do Azure](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Autenticação e autorização no serviço de aplicações do Azure](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Ativar a autenticação quando implementar com um modelo Azure Resource Manager**

Tem ainda de criar uma identidade de aplicação do Azure AD para a sua aplicação web ou aplicação API que difere da identidade de aplicação Olá para a sua aplicação lógica. passos seguintes toocreate Olá a identidade da aplicação, siga Olá anterior na parte 2 de Olá portal do Azure. Também pode seguir passos Olá parte 1, mas certifique-se de que toouse a aplicação web ou da aplicação API real `https://{URL}` para **URL de início de sessão** e **URI de ID de aplicação**. A partir destes passos, tem toosave ambos os cliente Olá ID e o ID de inquilino para utilizar no modelo de implementação da aplicação e também para parte 3.

> [!NOTE]
> Quando cria a identidade da aplicação Olá do Azure AD para a sua aplicação web ou aplicação API, tem de utilizar Olá portal do Azure ou portal clássico do Azure, em vez do PowerShell. Olá PowerShell commandlet não configurar permissões de Olá necessário toosign utilizadores para um Web site.

Depois de obter o ID de cliente de Olá e ID do inquilino, inclua estes IDs como um subresource da sua aplicação web ou aplicação API no seu modelo de implementação:

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically implementar uma aplicação web em branco e uma aplicação lógica, juntamente com a autenticação do Azure Active Directory, [vista Olá modelo completo aqui](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), ou clique em **implementar tooAzure** aqui:

[![Implementar tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>Parte 3: Preencher a secção de autorização de Olá na sua aplicação lógica

modelo anterior Olá já tem esta secção de autorização, configurar, mas se estiver a criar diretamente aplicação de lógica de Olá, tem de incluir secção de autorização completa Olá.

Abra a definição da aplicação lógica na vista de código, aceda toohello **HTTP** secção de ação, localizar Olá **autorização** secção e incluir esta linha:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Elemento | Descrição |
| ------- | ----------- |
| Inquilino |Olá GUID para o inquilino Olá do Azure AD |
| público-alvo |Necessário. Olá GUID para o recurso de destino Olá que pretende que o tooaccess - Olá ID de cliente de identidade da aplicação Olá para a sua aplicação web ou aplicação API |
| ID de cliente |Olá GUID para o cliente de Olá que pedem acesso - Olá ID de cliente de identidade da aplicação Olá para a sua aplicação lógica |
| segredo |Necessário. chave de Olá ou palavra-passe de identidade da aplicação Olá para cliente Olá que está a solicitar o token de acesso de Olá |
| tipo |tipo de autenticação de Olá. Para a autenticação de ActiveDirectoryOAuth, o valor de Olá é `ActiveDirectoryOAuth`. |

Por exemplo:

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Chamadas de API seguras através de código

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Autenticação de certificados

toovalidate Olá os pedidos recebidos da sua aplicação de lógica tooyour aplicação de web ou aplicação API, pode utilizar certificados de cliente. Saiba tooset se o seu código [como autenticação mútua do TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

No Olá **autorização** secção, incluir esta linha: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Elemento | Descrição |
| ------- | ----------- |
| tipo |Necessário. tipo de autenticação de Olá. Para certificados de cliente SSL, Olá valor tem de ser `ClientCertificate`. |
| palavra-passe |Necessário. Olá palavra-passe para aceder ao certificado de cliente Olá (ficheiro PFX) |
| PFX |Necessário. Com codificação Base64 conteúdo de certificado de cliente Olá (ficheiro PFX) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Autenticação básica

toovalidate pedidos recebidos da sua aplicação de lógica tooyour aplicação de web ou aplicação API, pode utilizar a autenticação básica, tais como um nome de utilizador e palavra-passe. Autenticação básica é um padrão comum e pode utilizar esta autenticação em qualquer toobuild idioma utilizado a aplicação web ou aplicação API.

No Olá **autorização** secção, incluir esta linha:

`{"type": "basic", "username": "username", "password": "password"}`.

| Elemento | Descrição |
| --- | --- |
| tipo |Necessário. tipo de autenticação de Olá. Para a autenticação básica, Olá valor tem de ser `Basic`. |
| o nome de utilizador |Necessário. Olá nome de utilizador para autenticação |
| palavra-passe |Necessário. Olá palavra-passe para autenticação |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Autenticação do Active Directory do Azure através de código

Por predefinição, a autenticação do Azure AD Olá ativassem no portal do Azure de Olá não fornece autorização detalhada. Por exemplo, esta autenticação bloqueia toojust sua API, um inquilino específico, não tooa utilizador específico ou aplicação. 

aplicação de lógica toorestrict API acesso tooyour através de código, extraia o cabeçalho de Olá que tem Olá um token web JSON (JWT). Verificar a identidade do emissor Olá e rejeitar pedidos que não correspondem.

Além disso, vai tooimplement esta autenticação inteiramente no seu próprio código e não utilize Olá portal do Azure, saiba como demasiado [autenticar com o Active Directory no local na sua aplicação do Azure](../app-service-web/web-sites-authentication-authorization.md).

toocreate uma identidade de aplicação para a sua aplicação lógica e utilizar essa identidade toocall sua API, tem de seguir passos anteriores Olá.

## <a name="next-steps"></a>Passos seguintes

* [Verificar o desempenho da aplicação lógica com alertas e registos de diagnóstico](logic-apps-monitor-your-logic-apps.md)