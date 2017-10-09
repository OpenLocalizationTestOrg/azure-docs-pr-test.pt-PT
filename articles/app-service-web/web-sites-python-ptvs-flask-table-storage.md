---
title: aaaFlask e armazenamento de tabelas do Azure no Azure com ferramentas do Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas do Python para Visual Studio toocreate uma aplicação web Flask que armazena dados no Table Storage do Azure e implemente-as Web Apps tooAzure App Service."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Flask e Table Storage do Azure no Azure com ferramentas do Python 2.2 para Visual Studio
Neste tutorial, iremos utilizar [ferramentas do Python para Visual Studio] toocreate uma simples aplicação web utilizando um dos modelos de exemplo Olá PTVS de consulta. Este tutorial também está disponível como uma [vídeo](https://www.youtube.com/watch?v=qUtZWtPwbTk).

aplicação de web de inquérito Olá define uma abstração para o repositório de, pelo que pode facilmente mudar entre diferentes tipos de repositórios (dentro da memória, armazenamento de tabelas do Azure, MongoDB).

Iremos irá aprender como de conta toocreate um Storage do Azure, como a tooconfigure Olá toouse de aplicação web Table Storage do Azure e como toopublish Olá aplicação web demasiado[Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Consulte Olá [Centro para programadores do Python] para consultar mais artigos que abrangem o desenvolvimento de aplicações Web de serviço de aplicação do Azure com a PTVS utilizando Bottle, Flask e Django as estruturas web, com os serviços de MongoDB, Table Storage do Azure, MySQL e base de dados SQL. Embora este artigo incida no App Service, os passos de Olá são semelhantes quando desenvolver [Cloud Services do Azure].

## <a name="prerequisites"></a>Pré-requisitos
* Visual Studio 2015
* [Ferramentas do Python 2.2 para Visual Studio]
* [ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio]
* [Ferramentas do Azure SDK para VS 2015]
* [Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="create-hello-project"></a>Criar Olá projeto
Nesta secção, vamos criar um projeto do Visual Studio utilizando um modelo de exemplo. Vamos criar um ambiente virtual e instalar pacotes necessários. Em seguida, será executado aplicação Olá localmente utilizando o repositório de dentro da memória Olá predefinido.

1. No Visual Studio, selecione **Ficheiro**, **Novo Projeto**.
2. Olá, modelos de projeto de Olá [ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio] estão disponíveis em **Python**, **amostras**. Selecione **inquéritos Flask Web Project** e clique em OK toocreate projeto de Olá.
   
     ![Caixa de Diálogo Novo Projeto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. Será pedido tooinstall de pacotes externos. Selecione **Instalar num ambiente virtual**.
   
     ![Caixa de Diálogo de Pacotes Externos](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. Selecione **Python 2.7** ou **Python 3.4** como o interpretador base Olá.
   
     ![Caixa de Diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. Confirme que a aplicação de Olá funciona premindo `F5`. Por predefinição, a aplicação Olá utiliza um repositório de memória que não necessita de qualquer configuração. Todos os dados é perdida quando o servidor de web de Olá está parado.
6. Clique em **Criar inquérito de exemplo**, em seguida, clique num inquérito e votar.
   
     ![Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Criar uma conta de armazenamento do Azure
operações de armazenamento toouse, precisa de uma conta de armazenamento do Azure. Pode criar uma conta de armazenamento, seguindo estes passos.

1. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com/).
2. Clique em Olá **novo** ícone na parte superior do Olá esquerda do Portal de Olá, em seguida, clique em **dados + armazenamento** > **conta de armazenamento**. Clique em **criar**, em seguida, atribua um nome exclusivo de conta de armazenamento de Olá e crie um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para o mesmo.
   
      ![Criação rápida](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    Quando tiver sido criada a conta de armazenamento Olá, Olá **notificações** botão será flash um verde **êxito** e painel de conta de armazenamento a Olá está aberta tooshow que pertence toohello novo recurso do grupo criar.
3. Clique em Olá **chaves de acesso** parte no painel de conta de armazenamento a Olá. Tome nota do nome da conta Olá e Olá chave1.
   
      ![Chaves](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    Vamos precisar este tooconfigure informações projeto na secção seguinte, Olá.

## <a name="configure-hello-project"></a>Configurar Olá projeto
Nesta secção, iremos irá configurar a nossa conta de armazenamento do Olá do aplicação toouse que acabamos de criar. Iremos ver como as definições de ligação de tooobtain do Olá Portal do Azure. Em seguida, iremos irá executar aplicação Olá localmente.

1. No Visual Studio, clique com o botão direito no nó do projeto no Explorador de soluções e selecione **propriedades**. Clique em Olá **depurar** separador.
   
     ![Definições de depuração do projeto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. Definir Olá valores de variáveis de ambiente de que a aplicação Olá **comando do servidor de depuração**, **ambiente**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Isto irá definir variáveis de ambiente de Olá quando que **iniciar depuração**. Se quiser Olá variáveis toobe definido quando a **iniciar sem depuração**, Olá conjunto mesmo valores em **executar comando de servidor** bem.
   
   Em alternativa, pode definir variáveis de ambiente utilizando Olá painel de controlo do Windows. Esta é uma opção melhor se pretender tooavoid armazenar credenciais no código fonte / ficheiro de projeto. Tenha em atenção que, terá de toorestart Visual Studio para Olá nova ambiente valores toobe toohello disponíveis aplicação.
3. código de Olá que implementa o repositório do Olá Table Storage do Azure está a ser **models/azuretablestorage.py**. Consulte Olá [documentação] para obter mais informações sobre como toouse serviço tabela do Python.
4. Executar a aplicação Olá com `F5`. Os inquéritos criados com **Criar inquérito de exemplo** e dados de Olá submetidos por voto serão serializados na Table Storage do Azure.
   
   > [!NOTE]
   > Olá ambiente Virtual do Python 2.7 pode causar uma quebra de exceção no Visual Studio.  Prima `F5` toocontinue ao carregar o projeto web de Olá.
   > 
   > 
5. Procurar toohello **sobre** tooverify de página que Olá aplicação está a utilizar Olá **Table Storage do Azure** repositório.
   
     ![Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Explorar Olá Table Storage do Azure
É fácil tooview e editar as tabelas do storage utilizando Cloud Explorer no Visual Studio. Nesta secção iremos utilizar o Explorador de servidores tooview Olá do conteúdo das tabelas de aplicação Olá inquérito.

> [!NOTE]
> Isto requer toobe de ferramentas do Microsoft Azure instalada, que estão disponíveis como parte da Olá [Azure SDK para .NET].
> 
> 

1. Abra **Cloud Explorer**. Expanda **contas do Storage**, a conta de armazenamento, em seguida, **tabelas**.
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Faça duplo clique no Olá **inquéritos** ou **escolhas** conteúdo de Olá tooview da tabela de Olá na janela de documento, bem como adicionar/remover/editar entidades de tabela.
   
     ![Resultados da consulta de tabela](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publicar Olá web app tooAzure do serviço de aplicações
Olá SDK .NET do Azure fornece uma forma fácil toodeploy sua tooAzure de aplicação web do serviço de aplicações.

1. No **Explorador de soluções**, faça duplo clique no nó do projeto de Olá e selecione **publicar**.
   
     ![Caixa de Diálogo Publicar Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Clique em **Web Apps do Microsoft Azure**.
3. Clique em **novo** toocreate uma nova aplicação web.
4. Preencha Olá seguintes campos e clique em **criar**.
   
   * **Nome da Aplicação Web**
   * **Plano do Serviço de Aplicações**
   * **Grupo de recursos**
   * **Região**
   * Deixe **servidor de base de dados** definido demasiado**nenhuma base de dados**
5. Aceite todas as outras predefinições e clique em **Publicar**.
6. O browser abrirá automaticamente toohello web publicada aplicação. Se procurar toohello sobre página, verá que utiliza Olá **dentro da memória** repositório, não Olá **Table Storage do Azure** repositório.
   
   Isto acontece porque as variáveis de ambiente de Olá não são definidas na instância do Olá Web Apps no App Service do Azure, para que utiliza os valores predefinidos de Olá especificados no **settings.py**.

## <a name="configure-hello-web-apps-instance"></a>Configurar a instância de Web Apps Olá
Nesta secção, iremos irá configurar variáveis de ambiente para a instância de Web Apps Olá.

1. No [Portal do Azure](https://portal.azure.com), abra o painel da aplicação web Olá clicando **procurar** > **serviços aplicacionais** > nome da aplicação web.
2. No painel da sua aplicação web, clique em **todas as definições**, em seguida, clique em **definições da aplicação**.
3. Desloque para baixo toohello **as definições de aplicação** secção e definir valores de Olá para **REPOSITÓRIO\_nome**, **armazenamento\_nome** e  **ARMAZENAMENTO\_chave** conforme descrito em Olá **projeto de Olá configurar** secção acima.
   
     ![Definições de aplicação](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Clique em **Guardar**. Após ter recebido notificações Olá que foram aplicadas alterações de Olá, clique em **procurar** Olá Web principal no painel da aplicação.
5. Deverá ver o trabalho de aplicação web de Olá conforme esperado, utilizando Olá **Table Storage do Azure** repositório.
   
   Parabéns!
   
     ![Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a>Passos seguintes
Siga estes toolearn ligações mais sobre as ferramentas do Python para Visual Studio, Flask e Table Storage do Azure.

* [Documentação das Ferramentas do Python para Visual Studio]
  * [Projetos Web]
  * [Projetos do Serviço em Nuvem]
  * [Depuração Remota no Microsoft Azure]
* [Documentação do flask]
* [Armazenamento do Azure]
* [Azure SDK for Python] (Azure SDK para Python)
* [Como tooUse Olá o serviço de armazenamento de tabela do Python]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Centro para programadores do Python]: /develop/python/
[Cloud Services do Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentação]:../cosmos-db/table-storage-how-to-use-python.md
[Como tooUse Olá o serviço de armazenamento de tabela do Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK para .NET]: http://azure.microsoft.com/downloads/ (Azure SDK para .NET)
[ferramentas do Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas do Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do Azure SDK para VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentação das Ferramentas do Python para Visual Studio]: http://aka.ms/ptvsdocs
[Documentação do flask]: http://flask.pocoo.org/
[Depuração Remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do Serviço em Nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Armazenamento do Azure]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK for Python]: https://github.com/Azure/azure-sdk-for-python (Azure SDK para Python)
