---
title: "aaaUpgrade de Mobile Services tooAzure do serviço de aplicações - Node.js"
description: "Saiba como tooeasily atualizar a sua tooan de aplicação de Mobile Services aplicação do serviço de aplicações móveis"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Atualizar o seu tooApp de serviço do Node.js do Azure Mobile serviço existente
Serviço de aplicações móveis é uma nova forma toobuild aplicações móveis com o Microsoft Azure. toolearn mais, consulte [que são Mobile Apps?].

Este tópico descreve como tooupgrade uma aplicação de back-end Node.js existente de Mobile Services do Azure tooa aplicações do Mobile novo serviço de aplicações. Enquanto executa esta atualização, a aplicação de Mobile Services existente pode continuar toooperate.  Se precisar de tooupgrade uma aplicação de back-end Node.js, consulte demasiado[atualizar os Mobile Services do .NET](app-service-mobile-net-upgrading-from-mobile-services.md).

Quando um back-end móvel tooAzure atualizado do serviço de aplicações, tem tooall acesso funcionalidades do App Service e são cobrados de acordo com demasiado[preços do serviço de aplicações], não Mobile Services preços.

## <a name="migrate-vs-upgrade"></a>Migrar vs atualização
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> É recomendado que [efetuar uma migração](app-service-mobile-migrating-from-mobile-services.md) antes de avançar através de uma atualização. Desta forma, pode colocar ambas as versões da aplicação no Olá plano do mesmo App Service e implicar sem custos adicionais.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Melhoramentos no servidor de Mobile Apps Node.js SDK
Atualizar toohello novo [SDK de aplicações móveis](https://www.npmjs.com/package/azure-mobile-apps) fornece muitas melhorias, incluindo:

* Com base no Olá [Express framework](http://expressjs.com/en/index.html), hello novo SDK do nó é claro ponderação e foi concebido tookeep cópias de segurança com novas versões de nó como entram. Pode personalizar o comportamento da aplicação Olá com Express middleware.
* Melhorias de desempenho significativas em comparação com toohello SDK dos Mobile Services.
* Agora pode alojar um Web site, juntamente com o seu back-end móvel; da mesma forma, é fácil tooadd Olá SDK do Azure Mobile tooany express.v4 aplicação existente.
* Incorporado para o desenvolvimento de plataforma e local, Olá SDK de aplicações móveis pode ser desenvolvida e executar localmente em plataformas Windows, Linux e no OSX. Agora é fácil toouse comuns nó técnicas de programação, como em execução [Mocha](https://mochajs.org/) testa toodeployment anterior.

## <a name="overview"></a>Descrição geral básica de atualização
tooaid na atualização de um back-end Node.js, App Service do Azure tiver fornecido um pacote de compatibilidade.  Após a atualização, terá de um site de niew que pode ser implementado tooa novo site de serviço de aplicações.

cliente de Mobile Services Olá SDKs são **não** compatíveis com o servidor de aplicações móveis novo SDK do Olá. Na ordem tooprovide a continuidade do serviço para a sua aplicação, não deve de publicar o site de tooa de alterações clientes publicados atualmente a funcionar. Em vez disso, deve criar uma nova aplicação móvel que funciona como um duplicado. Pode colocar esta aplicação no Olá mesmo serviço de aplicações planear tooavoid incorrer em custos financeiros adicionais.

Em seguida, terá de duas versões da aplicação Olá: um que permanece Olá mesmo e funciona aplicações publicadas no caráter Olá e da versão de outro que pode, em seguida, atualizar e de destino com um novo cliente. Pode mover e testar o seu código ao seu ritmo, mas, deve certificar-se de que as correções de erros que efetuar obter tooboth aplicado. Depois de sentir que um número pretendido de aplicações de cliente no difundidas atualizado com a versão mais recente toohello, é possível eliminar a aplicação migrada original de Olá se pretendidos ao nível. -Não implicar quaisquer custos de monetários adicionais, se estiver alojado no Olá planear o mesmo serviço de aplicações que a sua aplicação móvel.

descrição completa do Olá para o processo de atualização de Olá é o seguinte:

1. Transferir o serviço de móvel do Azure (migrados) existente.
2. Converter Olá projeto tooan aplicação móvel do Azure utilizando o pacote de compatibilidade de Olá.
3. Corrija quaisquer diferenças (tais como definições de autenticação).
4. Implementar a sua tooa de projeto de aplicação móvel do Azure convertida novo serviço de aplicações.
5. Uma nova versão da aplicação cliente que utilize Olá nova aplicação móvel de versão.
6. (Opcional) Elimine a aplicação de serviço móvel migrado original.

A eliminação pode ocorrer quando não vir qualquer tráfego no seu serviço móvel migrado original.

## <a name="install-npm-package"></a>Instalar Olá pré-requisitos
Deve instalar o [nó] no seu computador local.  Deve também instalar pacote de compatibilidade de Olá.  Depois do nó estiver instalado, pode executar Olá seguinte comando a partir de um cmd nova ou a linha de comandos PowerShell:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a>Obter os Scripts de Mobile Services do Azure
* Inicie sessão no toohello [Portal do Azure].
* Utilizar **todos os recursos** ou **serviços aplicacionais**, localizar o site de Mobile Services.
* No site de Olá, clique em **ferramentas** -> **Kudu** -> **aceda** site do tooopen Olá Kudu.
* Clique em **consola de depuração** -> **PowerShell** consola de depuração de Olá tooopen.
* Navegue demasiado`site/wwwroot/App_Data/config` clicando em cada diretório por sua vez
* Clique em Olá transferência ícone seguinte toohello `scripts` diretório.

Isto irá transferir os scripts de Olá no formato ZIP.  Criar um novo diretório no seu computador local e Descompacte Olá `scripts.ZIP` ficheiros dentro do diretório de Olá.  Esta ação irá criar um `scripts` diretório.

## <a name="scaffold-app"></a>Estruturar Olá novo Mobile Apps do Azure back-end
Execute Olá os seguintes comandos do diretório de Olá que contém o diretório de scripts Olá:

```scaffold-mobile-app scripts out```

Esta ação irá criar um estruturado back-end do Mobile Apps do Azure no Olá `out` diretório.  Apesar de não ser obrigatório, é um Olá de toocheck boa ideia `out` diretório para um repositório de código de origem à sua escolha.

## <a name="deploy-ama-app"></a>Implementar o seu back-end do Mobile Apps do Azure
Durante a implementação, terá de seguinte de Olá toodo:

1. Criar uma nova aplicação móvel no Olá [Portal do Azure].
2. Executar Olá `createViews.sql` script na base de dados ligada.
3. Base de dados do Olá ligação que está ligado tooyour serviço móvel tooyour novo serviço de aplicações.
4. Ligar a outro toohello de recursos (por exemplo, os Hubs de notificação) novo serviço de aplicações.
5. Implemente Olá gerado código tooyour novo site.

### <a name="create-a-new-mobile-app"></a>Criar uma nova aplicação móvel
1. Inicie sessão no Olá [Portal do Azure].
2. Clique em **+NOVO** > **Web + Móvel** > **Aplicação Móvel** e indique um nome para o back-end da Aplicação Móvel.
3. Para Olá **grupo de recursos**, selecione um grupo de recursos existente ou crie um novo (utilizando Olá o mesmo nome que a sua aplicação.)

    Pode selecionar outro plano do Serviço de Aplicações ou criar um novo. Para obter mais informações sobre os planos de serviços aplicacionais e como toocreate um novo plano num preço diferente de camada e na localização pretendida, consulte [descrição geral dos planos do App Service do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Para Olá **plano do App Service**, plano predefinido de Olá (no Olá [escalão Standard](https://azure.microsoft.com/pricing/details/app-service/)) está selecionado. Pode ainda selecionar um plano diferente ou [criar um novo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). Olá definições do plano de serviço de aplicações determinam Olá [localização, as funcionalidades, custos e recursos de computação](https://azure.microsoft.com/pricing/details/app-service/) associados à aplicação.

    Depois de decidir o plano de Olá, clique em **criar**. Esta ação cria Olá back-end da aplicação móvel.

### <a name="run-createviewssql"></a>Executar CreateViews.SQL
aplicação estruturado Olá contém um ficheiro chamado `createViews.sql`.  Este script tem de ser executado na base de dados de destino.  cadeia de ligação de Olá da base de dados de destino de Olá pode ser obtida a partir do seu serviço móvel migrado de Olá **definições** painel em **cadeias de ligação**.  É denominado `MS_TableConnectionString`.

Pode executar este script do SQL Server Management Studio ou Visual Studio.

### <a name="link-hello-database-tooyour-app-service"></a>Olá ligação tooyour de base de dados do serviço de aplicações
Hiperligação Olá tooyour da base de dados existente do serviço de aplicações:

* No Olá [Portal do Azure], abra o serviço de aplicações.
* Selecione **todas as definições** -> **ligações de dados**.
* Clique em **+ adicionar**.
* Na lista pendente Olá, selecione **base de dados SQL**
* Em **base de dados SQL**, selecione a base de dados existente, em seguida, clique em **selecione**.
* Em **cadeia de ligação**, introduza Olá nome de utilizador e palavra-passe para a base de dados de Olá, em seguida, clique em **OK**.
* No Olá **adicione ligações de dados** painel, clique em **OK**.

Olá nome de utilizador e palavra-passe podem ser encontrados através da visualização Olá cadeia de ligação da base de dados de destino de Olá no seu serviço móvel migrados.

### <a name="set-up-authentication"></a>Configurar autenticação
Mobile Apps do Azure permite a autenticação do Azure Active Directory, Facebook, Google, Microsoft e Twitter tooconfigure no âmbito do serviço de Olá.  Autenticação personalizada terá toobe desenvolvida separadamente.  Consulte Olá [conceitos de autenticação] documentação e [início rápido de autenticação] documentação para obter mais informações.  

## <a name="updating-clients"></a>Atualizar clientes móveis
Depois de ter um back-end de aplicação móvel operacional, pode trabalhar numa nova versão da aplicação cliente que consome-lo. As Mobile Apps também inclui uma nova versão do cliente de Olá SDKs e semelhantes toohello atualização do servidor acima, terá de tooremove todas as referências toohello Mobile Services SDKs antes de instalar as versões de aplicações móveis.

Uma das alterações de principais de Olá entre versões Olá é que construtores Olá já não necessitam de uma chave de aplicação.
Agora simplesmente passa no URL Olá da sua aplicação móvel. Por exemplo, em clientes de .NET Olá, Olá `MobileServiceClient` construtor é agora:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

Pode ler sobre a instalação Olá novos SDKs e utilizar a estrutura nova de Olá através de ligações de Olá abaixo:

* [Versão Android 2.2 ou posterior](app-service-mobile-android-how-to-use-client-library.md)
* [versão 3.0.0 iOS ou posterior](app-service-mobile-ios-how-to-use-client-library.md)
* [O .NET (Windows/Xamarin) versão 2.0.0 ou posterior](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova versão 2.0 ou posterior](app-service-mobile-cordova-how-to-use-client-library.md)

Se a aplicação faz com que a utilização de notificações push, anote Olá instruções de registo específicos para cada plataforma, como foram algumas alterações existe bem.

Quando tiver Olá nova versão do cliente pronto, experimente contra o projeto de servidor atualizado. Depois de confirmar que funciona, pode de versão uma nova versão do seu toocustomers de aplicação. Eventualmente, depois dos seus clientes tem tido um tooreceive hipótese estas atualizações, pode eliminar Olá Mobile Services versão da sua aplicação. Neste momento, tiver atualizado completamente tooan aplicação do serviço de aplicações móveis com Olá mais recente das Mobile Apps SDK do servidor.

<!-- URLs. -->

[Portal do Azure]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[que são Mobile Apps?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[preços do serviço de aplicações]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[conceitos de autenticação]: ../app-service/app-service-authentication-overview.md
[início rápido de autenticação]: app-service-mobile-auth.md

[Portal do Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
