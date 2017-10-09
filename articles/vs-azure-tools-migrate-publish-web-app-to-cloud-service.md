---
title: "aaaHow tooMigrate e publicar uma aplicação Web tooan do serviço de nuvem do Azure a partir do Visual Studio | Microsoft Docs"
description: "Saiba como toomigrate e publicar o seu tooan de aplicação web serviço em nuvem do Azure utilizando o Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Como: migrar e publicar uma aplicação Web de tooan serviço de nuvem do Azure a partir do Visual Studio
Olá, tootake partido dos serviços de alojamento e a escalabilidade do Azure, poderá pretender toomigrate e publicar o serviço de nuvem do Azure de tooan de aplicação web. Pode executar uma aplicação web no Azure com a aplicação existente de tooyour alterações mínimas.

> [!NOTE]
> Este tópico é sobre a implementação de serviços de toocloud, não tooweb sites. Para obter informações sobre a implementação tooweb sites, consulte [implementar uma aplicação web no App Service do Azure](app-service-web/web-sites-deploy.md).
>
>

Para obter uma lista de modelos específicos que são suportadas para o Visual c# e Visual Basic, consulte a secção de Olá **suportados modelos de projeto** mais adiante neste tópico.

Tem de ativar primeiro a aplicação web do Azure a partir do Visual Studio. Olá seguinte ilustração mostra a aplicação web existente Olá passos chave toopublish adicionando toouse um projeto do Azure para a implementação. Este processo adiciona um projeto do Azure com a solução de tooyour de função de web de Olá necessário. Com base no tipo de Olá do projeto web que tem, propriedades do projeto Olá para assemblagens também são atualizadas se o pacote de serviço Olá requer assemblagens adicionais para a implementação.

![Publicar um tooMicrosoft de aplicação Web do Azure](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Olá **converter**, **converter tooAzure projeto de serviço em nuvem** comando é apresentado apenas para o projeto web de Olá na sua solução. Por exemplo, o comando de Olá não está disponível para um projeto do Silverlight na sua solução.
> Quando criar um pacote de serviço ou publicar a aplicação tooAzure, poderão ocorrer erros ou avisos. Estes avisos e erros podem ajudar a corrigir problemas antes de implementar tooAzure. Por exemplo, poderá receber um aviso sobre uma assemblagem em falta. Para obter mais informações sobre como tootreat quaisquer avisos como erros, consulte o artigo [configurar um projeto de serviço em nuvem do Azure com o Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Se criar a sua aplicação, executá-la localmente utilizando o emulador de computação de Olá ou publicá-lo tooAzure, poderá ver Olá seguir erro na Olá **lista de erros** janela: **Olá especificado caminho, nome de ficheiro, ou ambos são demasiado longos** . Este erro ocorre porque o comprimento do nome de projeto do Azure completamente qualificado Olá Olá é demasiado longo. o comprimento do nome do projeto Olá, incluindo o caminho completo do Olá, Olá não pode ser mais do que 146 carateres. Por exemplo, este é o nome de projeto completa Olá, incluindo o caminho de ficheiro para um projeto do Azure que é criado para uma aplicação Silverlight: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Poderá ter toomove a sua solução tooa outro diretório que tem um comprimento de Olá de tooreduce de caminho mais curto do nome de projeto completamente qualificado Olá.
>
>

toomigrate e publicar um tooAzure de aplicação web do Visual Studio, siga estes passos.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Ativar uma aplicação Web para tooAzure de implementação
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>tooenable uma aplicação web para tooAzure de implementação
1. tooenable a aplicação web para tooAzure de implementação, o menu de atalho Olá aberto para uma web na sua solução do projeto e escolha Adicionar projeto de implementação do Azure.

    Olá seguintes ações ocorre:

   * Um projeto do Azure chamado `<name of hello web project>.Azure` é adicionada toohello solução para a sua aplicação.
   * Uma função da web para o projeto web de Olá é adicionada toothis projeto do Azure.
   * Olá **Cópia Local** propriedade está definida tootrue para todas as assemblagens que são necessárias para MVC 2, MVC 3, MVC 4 e as aplicações de empresas do Silverlight. Esta ação adiciona o pacote de serviço de toohello estas assemblagens que é utilizado para a implementação.

   > [!IMPORTANT]
   > Se tiver outros assemblagens ou os ficheiros necessários para esta aplicação web, tem de definir manualmente as propriedades de Olá para estes ficheiros. Para obter informações sobre como tooset estas propriedades, consulte o artigo Olá secção **incluem ficheiros Olá pacote de serviço** posteriormente neste artigo.
   >
   > [!NOTE]
   > Se já existir uma função da web para um projeto web específico num projeto do Azure numa solução de Olá, **converter**, **converter tooAzure projeto de serviço em nuvem** não é apresentada no menu de atalho Olá para este projeto web .
   >
   >

   Se tiver vários projetos web na sua aplicação web e funções da web toocreate para cada projeto web, tem de efetuar os passos de Olá neste procedimento para cada projeto web. Esta ação cria projetos do Azure separados para cada função da web. Cada projeto web pode ser publicado em separado. Em alternativa, pode adicionar manualmente outra função tooan existente do Azure projeto web na sua aplicação web. toodo, menu de atalho Olá aberta para Olá **funções** no projeto do Azure, selecione **adicionar**, em seguida, **projeto de função da Web na solução**, escolha Olá projeto tooadd como uma web função e, em seguida, escolha Olá **OK** botão.

## <a name="use-an-azure-sql-database-for-your-application"></a>Utilizar uma base de dados SQL do Azure para a sua aplicação
Se tiver uma cadeia de ligação para a sua aplicação web que utiliza uma base de dados do SQL Server que está no local de Olá, tem de alterar este toouse de cadeia de ligação uma instância da base de dados do SQL Server que aloja do Azure em vez disso.

> [!IMPORTANT]
> A subscrição tem de ativar a toouse base de dados SQL. Se aceder à sua subscrição do Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), pode determinar os serviços que fornece a sua subscrição. Olá seguintes instruções aplicam-se toohello lançada [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885). Se estiver a utilizar Olá [portal do Azure](http://portal.microsoft.com), ignorar toohello próximo procedimento.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse uma instância de base de dados SQL a função da web para a cadeia de ligação
1. toocreate uma instância de base de dados SQL no Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), siga os passos de Olá Olá seguinte artigo: [criar um servidor de base de dados do SQL Server](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > Quando configurar regras de firewall de Olá na sua instância da base de dados do SQL Server, tem de selecionar Olá **permitir que outros serviços do Azure tooaccess este servidor** caixa de verificação.
   >
   >
2. toocreate uma instância de base de dados SQL toouse para a cadeia de ligação, siga os passos de Olá na secção seguinte Olá Olá seguinte artigo: [criar uma base de dados do SQL Server](http://go.microsoft.com/fwlink/?LinkId=225110).
3. toocopy Olá ADO.NET ligação cadeia toouse para a cadeia de ligação, execute Olá os seguintes passos no Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Escolha Olá **base de dados** botão e nó de Olá, em seguida, abra para a subscrição de Olá que utilizou toocreate a instância da base de dados do SQL Server.
   2. toodisplay Olá disponíveis as instâncias da base de dados do SQL Server, escolha Olá **bases de dados SQL** nós.
   3. Propriedades de Olá toodisplay da base de dados de Olá, selecione a Olá. Olá **propriedades** é apresentada a vista.

      > [!NOTE]
      > Se hello **propriedades** vista não aparece, poderá ser necessário tooopen Olá-lo utilizando o separador.
      >
      >
   4. cadeias de ligação do toodisplay Olá, escolha Olá botão de reticências (…) tooView seguinte.

      Olá **cadeias de ligação** é apresentada a caixa de diálogo.
   5. Olá toocopy cadeia de ligação do ADO.NET, realce o texto de Olá e escolha Olá Ctrl + C chaves.
   6. caixa de diálogo do tooclose Olá caixa, escolha Olá **fechar** botão.
4. ligação de Olá tooreplace uma cadeia no Olá Web. config ficheiro toouse esta instância de base de dados SQL, abra o ficheiro Web. config de Olá, realce a entrada de cadeia de ligação existente Olá e, em seguida, escolha as chaves de Ctrl + V Olá. cadeia de ligação existente Olá substitui o Olá cadeia de ligação do ADO.NET para a instância de Olá da base de dados do SQL Server.
5. Também tem de adicionar parâmetro Olá `MultipleActiveResultSets=True` toohello cadeia de ligação. cadeia de ligação de Olá deve ter Olá seguinte formato:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (Opcional) Uma cadeia de ligação do método alternativo toochanging Olá diretamente no ficheiro Web. config de Olá é tooadd uma secção dos ficheiros de transformação Web. config Olá, consoante a configuração de compilação de Olá que utilize toocreate seu pacote de serviço. Abra o ficheiro de Web.Debug.Config Olá ou ficheiro de Web.Release.Config Olá. Adicione Olá secção a seguir para este ficheiro:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Guardar ficheiro de Olá que é modificado e voltar a publicar a aplicação.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>Olá, toouse uma instância da base de dados do SQL Server utilizando o portal clássico do Azure
1. No Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), escolha o nó de bases de dados SQL Olá.

   * Se for apresentada a instância de Olá da base de dados do SQL Server que pretende que o toouse, escolha tooopen-lo.
   * Se ainda não criou quaisquer instâncias, escolha a ligação adequada Olá e, em seguida, criar uma instância.
2. Depois de abrir ou criar uma instância de base de dados, escolha Olá **cadeias de ligação** ligação.
3. Olá parte inferior da página Olá, escolha definições de firewall de tooconfigure de ligação de Olá e aceitar os valores predefinidos de Olá ou configurar os valores de Olá que precisa.
4. Copie a cadeia de ligação do ADO.NET Olá, cole-o seu ficheiro Web. config através de cadeia ligação antigo Olá para Olá no local da base de dados e ser tooadd se `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Publicar uma aplicação Web tooAzure
### <a name="toopublish-a-web-application-tooazure"></a>toopublish um tooAzure de aplicação Web
1. aplicação de Olá tootest no ambiente de desenvolvimento local Olá utilizando o emulador de computação do Azure Olá, o menu de atalho Olá aberta para Olá do Azure do projeto de função da web Olá e escolha **definir como projeto de arranque**. Em seguida, escolha **depurar**, **iniciar depuração** (teclado: **F5**).

    Olá **início Olá ambiente de depuração do Azure** é aberta a caixa de diálogo e aplicação Olá é iniciado no browser Olá. Para obter detalhes específicos sobre como toostart cada tipo de aplicação web no Olá emulador de computação, consulte a tabela de Olá nesta secção.
2. tooset dos serviços de Olá para sua tooAzure toopublish de aplicação, tem de ter uma conta Microsoft e uma subscrição do Azure. Olá utilize os passos em Olá seguinte tópico tooset dos seus serviços: [preparar toopublish ou implementar uma aplicação do Azure a partir do Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. toopublish Olá web aplicação tooAzure, abra o menu de atalho Olá para o projeto web de Olá e escolha **publicar tooAzure**.

    Olá **publicar aplicação Azure** é aberta a caixa de diálogo e Visual Studio inicia o processo de implementação de Olá. Para obter mais informações sobre como toopublish Olá aplicação, consulte a secção de Olá **publicar uma aplicação do Azure a partir do Visual Studio** no [publicação de um serviço em nuvem com as ferramentas do Azure de Olá](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > Também pode publicar a aplicação web Olá Olá projeto do Azure. toodo isto, abra o menu de atalho Olá para Olá projeto do Azure e escolha **publicar**.
   >
   >
4. progresso de Olá toosee da implementação de Olá, pode ver Olá **registo de atividade do Azure** janela. Este registo é automaticamente apresentado quando o processo de implementação de Olá é iniciado. Pode expandir o item de linha de Olá no registo de atividade Olá tooshow informações detalhadas, conforme mostrado na seguinte ilustração de Olá:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. Processo de implementação de Olá toocancel (opcional), abra o menu de atalho Olá para o item de linha de Olá no registo de atividade Olá e escolha **Cancelar e remover**. Isto interrompe o processo de implementação de Olá e elimina o ambiente de implementação de Olá a partir do Azure.

   > [!NOTE]
   > tooremove depois deste ambiente de implementação tiver sido implementado, tem de utilizar Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (Opcional) Depois das instâncias da função tem sido iniciado, Visual Studio mostra automaticamente de ambiente de implementação Olá Olá **computação do Azure** no nó **Cloud Explorer** ou **Explorador de servidores**. Aqui pode ver o estado Olá Olá individuais de instâncias de função.

    Olá ilustração seguinte mostra as instâncias de função de Olá no **Explorador de servidores** enquanto estiverem ainda em estado de inicialização de Olá:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess a sua aplicação após a implementação, escolha Olá seta seguinte tooyour implementação quando o estado **concluído** aparece no Olá **registo de atividade do Azure**. Esta ação apresenta Olá URL para a sua aplicação web no Azure. Consulte Olá para Olá obter detalhes sobre como toostart específicos de um tipo de aplicação web do Azure a tabela seguinte.

    Olá, a tabela seguinte lista Olá obter detalhes sobre como toostart aplicações do Azure ou toorun web ou depurar uma aplicação web localmente utilizando Olá emulador de computação do Azure:

   | Tipo de aplicação Web | Olá executar/depuração localmente, utilizando o emulador de computação | em execução no Azure |
   | --- | --- | --- |
   | Aplicação ASP.NET Web |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Selecione a hiperligação de URL Olá apresentada no Olá **implementação** separador para Olá **registo de atividade do Azure** tooload Olá início de página no browser Olá. |
   | Aplicação Web ASP.NET MVC 2 |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Selecione a hiperligação de URL Olá apresentada no Olá **implementação** separador para Olá **registo de atividade do Azure** tooload Olá início de página no browser Olá. |
   | Aplicação Web ASP.NET MVC 3 |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Selecione a hiperligação de URL Olá apresentada no Olá **implementação** separador para Olá **registo de atividade do Azure** tooload Olá início de página no browser Olá. |
   | Aplicação Web de MVC do ASP.NET 4 |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Selecione a hiperligação de URL Olá apresentada no Olá **implementação** separador para Olá **registo de atividade do Azure** tooload Olá início de página no browser Olá. |
   | Aplicação Web de ASP.NET vazio |Tem de adicionar uma página. aspx na sua aplicação que definir como página de início de Olá para o projeto web. Em seguida, na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Se tiver uma página. aspx na sua aplicação, escolha a hiperligação de URL Olá apresentada no Olá **implementação** separador para Olá **registo de atividade do Azure** e esta página é carregada no browser Olá. Se tiver uma página. aspx diferente, terá de toonavigate toothis página específica Olá segue o formato para o url a utilizar:`<url for deployment>/<name of page>.aspx` |
   | Aplicação Silverlight |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Página específica do toonavigate toohello é necessário para a sua aplicação Olá segue o formato para o url a utilizar:`<url for deployment>/<name of page>.aspx` |
   | Aplicação de negócio do Silverlight |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Página específica do toonavigate toohello é necessário para a sua aplicação Olá segue o formato para o url a utilizar:`<url for deployment>/<name of page>.aspx` |
   | Aplicação de navegação do Silverlight |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Página específica do toonavigate toohello é necessário para a sua aplicação Olá segue o formato para o url a utilizar:`<url for deployment>/<name of page>.aspx` |
   | Aplicação de serviço WCF |Tem de definir o ficheiro. svc Olá como Olá iniciar página para o seu projeto de serviço de WCF. Em seguida, na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |É necessário o ficheiro do toonavigate toohello svc para a sua aplicação Olá segue o formato para o url a utilizar:`<url for deployment>/<name of service file>.svc` |
   | Aplicação do serviço de fluxo de trabalho WCF |Tem de definir o ficheiro. svc Olá como Olá iniciar página para o seu projeto de serviço de WCF. Em seguida, na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |É necessário o ficheiro do toonavigate toohello svc para a sua aplicação Olá segue o formato para o url a utilizar:`<url for deployment>/<name of service file>.svc` |
   | Entidades dinâmico de ASP.NET |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |É necessário atualizar a cadeia de ligação de Olá (consulte a secção seguinte). É também necessário toonavigate toohello específico página para a sua aplicação Olá segue o formato para o url a utilizar:`<url for deployment>/<name of page>.aspx` |
   | TooSQL de Linq de dados dinâmicos do ASP.NET |Na barra de menus Olá, escolha **depurar**, **iniciar depuração** (teclado: escolha Olá **F5** chave.). |Tem de seguir passos deste procedimento Olá: utilizar uma SQL database do Azure para a sua aplicação (consulte a secção anterior deste tópico). É também necessário toonavigate toohello específico página para a sua aplicação Olá segue o formato para o url a utilizar:`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Atualizar uma cadeia de ligação para entidades dinâmico de ASP.NET
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate uma cadeia de ligação para entidades dinâmicos do ASP.NET
1. toocreate uma SQL database do Azure que pode ser utilizada para uma aplicação web de entidades dinâmicos do ASP.NET, siga os passos de Olá no procedimento de Olá **utilizar uma SQL database do Azure para a sua aplicação** anteriormente neste tópico.
2. Adicionar os campos que sejam necessárias para esta base de dados de Olá e tabelas de Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
3. cadeia de ligação de Olá para este tipo de aplicação tem Olá seguir o formato no ficheiro Web. config de Olá:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Olá atualização *connectionString* valor com Olá cadeia de ligação do ADO.NET para a base de dados do SQL Azure da seguinte forma:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. ficheiro de Web. config Olá toosave com alterações de Olá que efetuou toohello cadeia de ligação, na barra de menus Olá escolha **ficheiro**, **guardar o Web. config**.

## <a name="supported-project-templates"></a>Modelos de projeto suportados
toopublish um tooAzure de aplicação web, aplicação Olá tem de utilizar um dos modelos de projeto Olá para c# ou Visual Basic que está listado na tabela de Olá abaixo.

| Grupo de modelo de projeto | Modelo de projeto |
| --- | --- |
| Web |Aplicação ASP.NET Web |
| Web |Aplicação Web ASP.NET MVC 2 |
| Web |Aplicação Web ASP.NET MVC 3 |
| Web |Aplicação Web de ASP.NET MVC4 |
| Web |Aplicação Web de ASP.NET vazio |
| Web |Aplicação de Web vazio de ASP.NET MVC 2 |
| Web |Aplicação Web de entidades de dados dinâmico de ASP.NET |
| Web |ASP.NET dinâmica dados Linq tooSQL aplicação Web |
| Silverlight |Aplicação Silverlight |
| Silverlight |Aplicação de negócio do Silverlight |
| Silverlight |Aplicação de navegação do Silverlight |
| WCF |Aplicação de serviço WCF |
| WCF |Aplicação do serviço de fluxo de trabalho WCF |
| Fluxo de trabalho |Aplicação do serviço de fluxo de trabalho WCF |

## <a name="next-steps"></a>Passos Seguintes
Para obter mais informações sobre a publicação, consulte [preparar tooPublish ou implementar uma aplicação do Azure a partir do Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Consulte também [definição de cópia de segurança denominado credenciais de autenticação](vs-azure-tools-setting-up-named-authentication-credentials.md).
