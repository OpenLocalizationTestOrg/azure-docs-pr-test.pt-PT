---
title: aaaDjango e a SQL Database no Azure com ferramentas do Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas do Python para Visual Studio toocreate uma aplicação web Django que armazena dados numa instância de base de dados SQL e implemente-as Web Apps tooAzure App Service."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>O Django e a Base de Dados SQL no Azure com Ferramentas do Python 2.2 para Visual Studio
Neste tutorial, iremos utilizar [ferramentas do Python para Visual Studio] toocreate uma simples aplicação web utilizando um dos modelos de exemplo Olá PTVS de consulta. Este tutorial também está disponível como uma [vídeo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Vamos aprender como toouse uma base de dados do SQL Server alojado no Azure, como tooconfigure Olá toouse de aplicação web uma base de dados do SQL Server e como toopublish Olá aplicação web demasiado[Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Consulte Olá [Centro para programadores do Python] para consultar mais artigos que abrangem o desenvolvimento de aplicações Web de serviço de aplicação do Azure com a PTVS utilizando Bottle, Flask e Django as estruturas web, com os serviços de armazenamento de tabelas do Azure, MySQL e base de dados SQL. Embora este artigo incida no App Service, os passos de Olá são semelhantes quando desenvolver [Cloud Services do Azure].

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2015
* [Python 2.7 de 32 bits]
* [Ferramentas do Python 2.2 para Visual Studio]
* [ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio]
* [Ferramentas do Azure SDK para VS 2015]
* Django 1.9 ou posterior

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
>
>

## <a name="create-hello-project"></a>Criar Olá projeto
Nesta secção, vamos criar um projeto do Visual Studio utilizando um modelo de exemplo. Vamos criar um ambiente virtual e instalar pacotes necessários. Vamos criar uma base de dados local utilizando o sqlite. Em seguida, iremos irá executar localmente Olá web app.

1. No Visual Studio, selecione **Ficheiro**, **Novo Projeto**.
2. Olá, modelos de projeto de Olá [ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio] estão disponíveis em **Python**, **amostras**. Selecione **projeto de Web Django de inquérito** e clique em OK toocreate projeto de Olá.

     ![Caixa de Diálogo Novo Projeto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Será pedido tooinstall de pacotes externos. Selecione **Instalar num ambiente virtual**.

     ![Caixa de Diálogo de Pacotes Externos](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Selecione **Python 2.7** como o interpretador base Olá.

     ![Caixa de Diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. No **Explorador de soluções**, faça duplo clique no nó do projeto de Olá e selecione **Python**e, em seguida, selecione **migrar o Django**.  Em seguida, selecione **Criar Superutilizador do Django**.
6. Isto irá abrir uma consola de gestão do Django e criar uma base de dados do sqlite na pasta do projeto de Olá. Siga as indicações de Olá toocreate um utilizador.
7. Confirme que a aplicação de Olá funciona premindo <kbd>F5</kbd>.
8. Clique em **início de sessão** na barra de navegação de Olá na parte superior do Olá.

     ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Introduza as credenciais de Olá utilizador Olá que criou quando sincronizou a base de dados de Olá.

     ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Clique em **Criar Inquérito de Exemplo**.

      ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Clique num inquérito e vote.

      ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Criar uma Base de Dados SQL
Para a base de dados de Olá, vamos criar uma base de dados SQL do Azure.

Pode criar uma base de dados, seguindo estes passos.

1. Iniciar sessão Olá [Portal do Azure].
2. Na Olá parte inferior do painel de navegação de Olá, clique em **novo**. , clique em **dados + armazenamento** > **base de dados SQL**.
3. Configurar Olá nova base de dados do SQL Server ao criar um novo grupo de recursos e selecione Olá localização adequada para a mesma.
4. Assim que for criado Olá base de dados do SQL Server, clique em **abrir no Visual Studio** no painel da base de dados de Olá.
5. Clique em **configurar a firewall**.
6. No Olá **as definições da Firewall** painel, adicionar uma regra de firewall com **IP inicial** e **IP final** definir toohello endereço IP público do seu computador de desenvolvimento. Clique em **Guardar**.

   Isto permitirá que o servidor de base de dados de toohello ligações do seu computador de desenvolvimento.
7. No painel da base de dados de Olá, clique **propriedades**, em seguida, clique em **Mostrar cadeias de ligação de base de dados**.
8. Utilizar o Olá cópia botão tooput Olá valor **ADO.NET** na área de transferência Olá.

## <a name="configure-hello-project"></a>Configurar Olá projeto
Nesta secção, iremos irá configurar a nossa web app toouse Olá base de dados SQL que acabamos de criar. Também vamos instalá adicionais Python pacotes necessários toouse SQL as bases de dados com o Django. Em seguida, iremos irá executar localmente Olá web app.

1. No Visual Studio, abra **settings.py**, de Olá *ProjectName* pasta. Cole temporariamente a cadeia de ligação de Olá num editor de Olá. cadeia de ligação de Olá está neste formato:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Editar definição de Olá de `DATABASES` toouse Olá os valores acima.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. No Explorador de soluções, em **ambientes do Python**, faça duplo clique no ambiente virtual Olá e selecione **Instalar pacote do Python**.
2. Instalar o pacote de Olá `pyodbc` utilizando **pip**.

     ![Caixa de diálogo de pacotes de Python instalar](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Instalar o pacote de Olá `django-pyodbc-azure` utilizando **pip**.

     ![Caixa de diálogo de pacotes de Python instalar](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. No **Explorador de soluções**, faça duplo clique no nó do projeto de Olá e selecione **Python**e, em seguida, selecione **migrar o Django**.  Em seguida, selecione **Criar Superutilizador do Django**.

   Esta ação irá criar tabelas de Olá da base de dados do SQL Server Olá que criámos na secção anterior Olá. Siga Olá pede toocreate um utilizador, que não tem o utilizador de Olá toomatch na base de dados do sqlite Olá criado na primeira secção de Olá.
5. Executar a aplicação Olá com `F5`. Os inquéritos criados com **Criar inquérito de exemplo** e dados de Olá submetidos por voto serão serializados na base de dados do Olá SQL.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publicar Olá web app tooAzure do serviço de aplicações
Olá SDK .NET do Azure fornece uma forma fácil toodeploy tooAzure de aplicação web a web Apps do App Service Web.

1. No **Explorador de soluções**, faça duplo clique no nó do projeto de Olá e selecione **publicar**.

     ![Caixa de Diálogo Publicar Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Clique em **Web Apps do Microsoft Azure**.
3. Clique em **novo** toocreate uma nova aplicação web.
4. Preencha Olá seguintes campos e clique em **criar**.

   * **Nome da Aplicação Web**
   * **Plano do Serviço de Aplicações**
   * **Grupo de recursos**
   * **Região**
   * Deixe **servidor de base de dados** definido demasiado**nenhuma base de dados**
5. Aceite todas as outras predefinições e clique em **Publicar**.
6. O browser abrirá automaticamente toohello web publicada aplicação. Deverá ver o trabalho de aplicação web de Olá conforme esperado, utilizando Olá **SQL** base de dados alojada no Azure.

   Parabéns!

     ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Passos seguintes
Siga estes toolearn ligações mais sobre as ferramentas do Python para Visual Studio, Django e a SQL Database.

* [Documentação das Ferramentas do Python para Visual Studio]
  * [Projetos Web]
  * [Projetos do Serviço em Nuvem]
  * [Depuração Remota no Microsoft Azure]
* [Documentação do Django]
* [Base de Dados SQL]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Centro para programadores do Python]: /develop/python/
[Cloud Services do Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Portal do Azure]: https://portal.azure.com
[ferramentas do Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas do Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do Azure SDK para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentação das Ferramentas do Python para Visual Studio]: http://aka.ms/ptvsdocs
[Depuração Remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do Serviço em Nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentação do Django]: https://www.djangoproject.com/
[Base de Dados SQL]: /documentation/services/sql-database/
