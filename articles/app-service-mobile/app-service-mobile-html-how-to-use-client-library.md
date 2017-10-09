---
title: "aaaHow tooUse Olá JavaScript SDK de Mobile Apps do Azure"
description: Como v tooUse para Mobile Apps do Azure
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>Como tooUse hello a biblioteca de cliente JavaScript para Mobile Apps do Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Este guia informa tooperform cenários comuns utilizando Olá mais recente [JavaScript SDK de Mobile Apps do Azure]. Se for novo tooAzure Mobile Apps, primeiro conclua [Azure Mobile Apps início rápido] toocreate um back-end e criar uma tabela. Neste guia, iremos focar-se sobre como utilizar o back-end móvel Olá nas aplicações Web HTML/JavaScript.

## <a name="supported-platforms"></a>Plataformas suportadas
Estamos a limitar browser suporte toohello atual e a última versões do Olá browsers principais: Google Chrome, o Microsoft Edge, o Microsoft Internet Explorer e o Mozilla Firefox.  Esperamos Olá SDK toofunction com qualquer browser relativamente moderna.

pacote de Olá é distribuído como um módulo de JavaScript Universal, para que suporta globais, AMD, e CommonJS formatos.

## <a name="Setup"></a>A configuração e pré-requisitos
Este guia pressupõe que criou um back-end com uma tabela. Este guia pressupõe que tabela Olá tem Olá mesmo esquema como tabelas Olá estes tutoriais.

Instalar Olá JavaScript SDK do Azure Mobile Apps pode ser feito através de Olá `npm` comando:

```
npm install azure-mobile-apps-client --save
```

biblioteca de Olá também pode ser utilizada como um módulo de ES2015, dentro de ambientes de CommonJS como Browserify e Webpack e como uma biblioteca AMD.  Por exemplo:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

Também pode utilizar uma versão de Olá SDK pré-criadas transferindo-a diretamente a partir do nosso CDN:

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Como: autenticar os utilizadores
App Service do Azure suporta autenticar e autorizar utilizadores de aplicações através de vários fornecedores de identidade externas: Facebook, Google, Account Microsoft e Twitter. Pode definir permissões de acesso de toorestrict tabelas para operações específicas tooonly autenticada utilizadores. Também pode utilizar a identidade de Olá utilizadores autenticados tooimplement das regras de autorização em scripts de servidor. Para obter mais informações, consulte Olá [introdução à autenticação] tutorial.

São suportados dois fluxos de autenticação: um fluxo de servidor e um fluxo de cliente.  fluxo de servidor Olá fornece a experiência de autenticação mais simples de Olá, como baseia-se na interface de autenticação de web do fornecedor de Olá. Olá fluxo de cliente permite para uma integração mais profunda com as capacidades específicas do dispositivo, tal como single-sign-on como depende SDKs específica do fornecedor.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Como: configurar o serviço de aplicações móveis para os URLs de redirecionamento externo.
Vários tipos de aplicações de JavaScript utilizam um toohandle de capacidade de loopback que flui de IU de OAuth.  Estas funcionalidades incluem:

* Executar o serviço localmente
* Utilizar recarregar em direto com Olá Ionic Framework
* Redirecionar tooApp serviço para a autenticação.

Executar localmente pode causar problemas, porque, por predefinição, a autenticação é apenas de serviço de aplicações configurado o acesso de tooallow de back-end da aplicação móvel. Utilize Olá ao executar o servidor de Olá localmente os seguintes passos toochange Olá autenticação de tooenable de definições do serviço de aplicações:

1. Inicie sessão no toohello [portal do Azure]
2. Navegue tooyour back-end da aplicação móvel.
3. Selecione **Explorador de recursos** no Olá **ferramentas de desenvolvimento** menu.
4. Clique em **aceda** Explorador de recursos de Olá tooopen de back-end da aplicação móvel num novo separador ou janela.
5. Expanda Olá **configuração** > **authsettings** nós para a sua aplicação.
6. Clique em Olá **editar** botão Editar tooenable do recurso de Olá.
7. Determinar Olá **allowedExternalRedirectUrls** elemento, que deve ser nulo. Adicione os URLs de uma matriz:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Substitua os URLs de Olá na matriz de Olá Olá URLs do seu serviço, que, neste exemplo, é `http://localhost:3000` para o serviço de exemplo de Node.js Olá local. Pode também utilizar `http://localhost:4400` Olá Ripple para ou de serviço outro URL, dependendo de como a aplicação está configurada.
8. Na Olá parte superior da página Olá, clique em **leitura/escrita**, em seguida, clique em **colocar** toosave as atualizações.

Também precisa de tooadd Olá mesmas loopback URLs toohello definições CORS da lista branca:

1. Navegue back toohello [portal do Azure].
2. Navegue tooyour back-end da aplicação móvel.
3. Clique em **CORS** no Olá **API** menu.
4. Introduza cada URL Olá vazio **origens permitidas** caixa de texto.  É criada uma nova caixa de texto.
5. Clique em **guardar**

Depois de atualizações de back-end de Olá, será capaz de toouse Olá loopback novos URLs na sua aplicação.

<!-- URLs. -->
[Azure Mobile Apps início rápido]: app-service-mobile-cordova-get-started.md
[introdução à autenticação]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portal do Azure]: https://portal.azure.com/
[JavaScript SDK de Mobile Apps do Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
