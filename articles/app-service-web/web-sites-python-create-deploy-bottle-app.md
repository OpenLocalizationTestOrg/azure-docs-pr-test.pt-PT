---
title: "aplicações web de aaaPython com Bottle no Azure"
description: "Um tutorial que explica toorunning uma aplicação web do Python nas Web Apps do Azure App Service."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a>Criar web apps com Bottle no Azure
Este tutorial descreve como tooget iniciado a executar o Python nas Web Apps do Azure App Service. As Web Apps fornecem um alojamento gratuito e uma implementação rápida e pode utilizar o Python! Olá, como a sua aplicação cresce, pode mudar de alojamento toopaid e também pode integrar com todos os outros serviços do Azure.

Irá criar uma aplicação web utilizando a estrutura de web Bottle Olá (ver versões alternativas deste tutorial para [Django](web-sites-python-create-deploy-django-app.md) e [Flask](web-sites-python-create-deploy-flask-app.md)). Irá criar aplicação web de Olá Olá Azure Marketplace, configurar a implementação de Git e clonar o repositório de Olá localmente. Em seguida, irá executar a aplicação web de Olá localmente, efetuar alterações, consolidar e emiti-las demasiado[Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Olá tutorial mostra como toodo esta do Windows ou Mac/Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* Windows, Mac ou Linux
* Python 2.7 ou 3.4
* setuptools, pip, virtualenv (apenas no Python 2.7)
* Git
* [Ferramentas do Python 2.2 para Visual Studio][Ferramentas do Python 2.2 para Visual Studio] (PTVS) – Nota: Isto é opcional

**Nota**: de momento, a publicação do TFS não é suportada para projetos Python.

### <a name="windows"></a>Windows
Se ainda não tiver o Python 2.7 ou 3.4 instalado (32 bits), recomendamos que instale o [Azure SDK para Python 2.7] ou o [Azure SDK para Python 3.4] utilizando o Instalador de Plataforma Web. Esta ação instala a versão de 32 bits de Olá do Python, setuptools, pip, virtualenv, etc. (o Python de 32 bits é o que é instalado em máquinas de anfitrião do Azure de Olá). Em alternativa, pode obter o Python de [python.org].

Para Git, recomendamos o [Git para Windows] ou o [GitHub para Windows]. Se utilizar o Visual Studio, pode utilizar o suporte de Git Olá integrado.

Também recomendamos que instale as [Ferramentas do Python 2.2 para Visual Studio]. Isto é opcional, mas se tiver [Visual Studio], incluindo Olá livre Visual Studio Community 2013 ou Visual Studio Express 2013 para a Web, em seguida, isto irá dar-lhe um excelente IDE do Python.

### <a name="maclinux"></a>Mac/Linux
Já deve ter Python e Git já instalado, mas certifique-se de que tem o Python 2.7 ou 3.4.

## <a name="web-app-creation-on-hello-azure-portal"></a>Criação da aplicação Web no Olá Portal do Azure
Olá primeiro passo na criação da sua aplicação é toocreate Olá web app através de Olá [Portal do Azure](https://portal.azure.com).  

1. Inicie sessão no Portal do Azure de Olá e clique em Olá **novo** botão no canto inferior esquerdo Olá. 
2. Na caixa de pesquisa de Olá, escreva "python".
3. Nos resultados de pesquisa de Olá, selecione **Bottle**, em seguida, clique em **criar**.
4. Configure Olá nova Bottle aplicação, tais como criar um novo plano de serviço de aplicações e um novo grupo de recursos para o mesmo. Em seguida, clique em **Criar**.
5. Configurar a publicação de Git para a sua aplicação web recentemente criada ao seguir as instruções de Olá em [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Descrição Geral da Aplicação
### <a name="git-repository-contents"></a>Conteúdo do repositório de Git
Eis uma descrição geral dos ficheiros de Olá, encontrará no repositório de Git inicial Olá, que iremos clonar na secção seguinte, Olá.

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

Origens principais para a aplicação Olá. Consiste em 3 páginas (índice, acerca de, contacto) com um esquema do modelo global.  O conteúdo estático e os scripts incluem arranque, jquery, modernizr e responder.

    \app.py

Suporte de servidor de desenvolvimento local. Utilize esta aplicação de Olá toorun localmente.

    \BottleWebProject.pyproj
    \BottleWebProject.sln

Os ficheiros de projeto para utilização com as [Ferramentas do Python para Visual Studio].

    \ptvs_virtualenv_proxy.py

Proxy do IIS para ambientes virtuais e suporte de depuração remota do PTVS.

    \requirements.txt

Pacotes externos necessários para esta aplicação. script de implementação de Olá irá instalar os pacotes de Olá listados neste ficheiro através do pip.

    \web.2.7.config
    \web.3.4.config

Ficheiros de configuração do IIS. script de implementação de Olá vai utilizar x.y. config adequado de Olá e copiá-lo como Web. config.

### <a name="optional-files---customizing-deployment"></a>Ficheiros opcionais - personalizar a implementação
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Ficheiros opcionais - runtime do Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Ficheiros adicionais no servidor
Alguns ficheiros existem no servidor de Olá, mas não foram adicionados toohello repositório de git. Estes são criados pelo script de implementação de Olá.

    \web.config

Ficheiro de configuração do IIS. Criado a partir de web.x.y.config em todas as implementações.

    \env\

Ambiente virtual do Python. Se um ambiente virtual compatível ainda não existir na aplicação web de Olá, criados durante a implementação.  Os pacotes listados em requirements.txt são instalados pelo pip, mas o pip saltará a instalação se Olá pacotes já estiverem instalados.

Olá 3 secções seguintes descrevem como tooproceed com Olá web desenvolvimento de aplicações em 3 ambientes diferentes:

* Windows, com as Ferramentas do Python para Visual Studio
* Windows, com linha de comandos
* Mac/Linux, com linha de comandos

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Web App desenvolvimento – Windows – ferramentas do Python para Visual Studio
### <a name="clone-hello-repository"></a>Repositório de Olá clone
Em primeiro lugar, clone o repositório de Olá utilizando o url de Olá fornecido no Olá Portal do Azure. Para obter mais informações, consulte [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).

Abra o ficheiro de solução de Olá (. sln) que está incluído na raiz de Olá do repositório de Olá.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a>Criar ambiente virtual
Agora, vamos criar um ambiente virtual para o desenvolvimento local. Clique com o botão direito do rato em **Ambientes do Python** e selecione **Adicionar Ambiente Virtual...**.

* Certifique-se de nome de Olá do ambiente de Olá `env`.
* Selecione o interpretador base Olá. Certifique-se toouse Olá a mesma versão do Python selecionada para a sua aplicação web (no runtime.txt ou Olá **definições da aplicação** painel da sua aplicação web no Portal do Azure de Olá).
* Certifique-se de pacotes de toodownload e a instalação da opção Olá está marcada.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

Clique em **Criar**. Isto irá criar ambiente virtual Olá e instalar dependências listadas no requirements.txt.

### <a name="run-using-development-server"></a>Executar com o servidor de desenvolvimento
Prima F5 toostart depuração e o seu browser abrirá automaticamente página toohello executar localmente.

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

Pode definir pontos de interrupção nas origens Olá, utilize Olá janelas, etc. Consulte Olá [ferramentas do Python para Visual Studio documentação] para obter mais informações sobre Olá várias funcionalidades.

### <a name="make-changes"></a>Efetuar alterações
Agora, pode experimentar efetuando alterações toohello aplicação origens e/ou modelos.

Depois de ter testado as suas alterações, confirmá-las toohello repositório de Git:

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a>Instalar mais pacotes
A aplicação pode ter dependências que ultrapassam o Python e Bottle.

É possível instalar pacotes adicionais através do pip. tooinstall um pacote, clique com botão direito no ambiente virtual Olá e selecione **Instalar pacote do Python**.

Por exemplo, tooinstall Olá Azure SDK para Python, que permite-lhe aceder tooAzure armazenamento, o service bus e outros serviços do Azure, introduza `azure`:

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

Clique com o botão direito no ambiente virtual Olá e selecione **gerar requirements.txt** tooupdate requirements.txt.

Em seguida, confirme o repositório de Git do Olá alterações toorequirements.txt toohello.

### <a name="deploy-tooazure"></a>Implementar tooAzure
tootrigger uma implementação, clique em **sincronização** ou **Push**. A sincronização envia e recebe.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

primeira implementação de Olá irá demorar algum tempo, irá criar um ambiente virtual, instalar pacotes, etc.

Visual Studio não mostra o progresso de Olá da implementação de Olá. Se gostaria de saída de Olá tooreview, consulte a secção de Olá no [resolução de problemas - implementação](#troubleshooting-deployment).

Procure toohello Azure URL tooview as suas alterações.

## <a name="web-app-development---windows---command-line"></a>A linha de comandos - Windows - desenvolvimento da aplicação Web
### <a name="clone-hello-repository"></a>Repositório de Olá clone
Em primeiro lugar, clone repositório de Olá utilizando o URL de Olá fornecido no Portal do Azure de Olá e adicione Olá repositório do Azure como um remoto. Para obter mais informações, consulte [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Criar ambiente virtual
Vamos criar um novo ambiente virtual para fins de desenvolvimento (não o adicione toohello repositório). Ambientes virtuais no Python não são relocalizáveis, pelo que cada programador que trabalha na aplicação Olá irá criar os seus próprios localmente.

Certifique-se toouse Olá a mesma versão do Python selecionada para a sua aplicação web (no runtime.txt ou Olá painel Definições da aplicação para a sua aplicação web no Olá Portal do Azure)

Para Python 2.7:

    c:\python27\python.exe -m virtualenv env

Para Python 3.4:

    c:\python34\python.exe -m venv env

Instale quaisquer pacotes externos exigidos pela sua aplicação. Pode utilizar o ficheiro requirements.txt de Olá na raiz de Olá de pacotes de Olá Olá repositório tooinstall num ambiente virtual:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Executar com o servidor de desenvolvimento
Pode iniciar a aplicação Olá num servidor de desenvolvimento com Olá os seguintes comandos:

    env\scripts\python app.py

consola de Olá irá apresentar URL Olá e porta Olá server escuta a para:

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

Em seguida, abra o seu URL de toothat do web browser.

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a>Efetuar alterações
Agora, pode experimentar efetuando alterações toohello aplicação origens e/ou modelos.

Depois de ter testado as suas alterações, confirmá-las toohello repositório de Git:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalar mais pacotes
A aplicação pode ter dependências que ultrapassam o Python e Bottle.

É possível instalar pacotes adicionais através do pip. Por exemplo, tooinstall Olá Azure SDK para Python, que dá-lhe aceder tooAzure armazenamento, o service bus e outros serviços do Azure, o tipo:

    env\scripts\pip install azure

Certifique-se de que tooupdate requirements.txt:

    env\scripts\pip freeze > requirements.txt

Consolide alterações de Olá:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Implementar tooAzure
tootrigger uma implementação, Olá push altera tooAzure:

    git push azure master

Irá ver o resultado de Olá do script de implementação de Olá, incluindo a criação do ambiente virtual, instalação de pacotes e criação de Web. config.

Procure toohello Azure URL tooview as suas alterações.

## <a name="web-app-development---maclinux---command-line"></a>Implementação da aplicação Web – Mac/Linux – linha de comandos
### <a name="clone-hello-repository"></a>Repositório de Olá clone
Em primeiro lugar, clone repositório de Olá utilizando o URL de Olá fornecido no Portal do Azure de Olá e adicione Olá repositório do Azure como um remoto. Para obter mais informações, consulte [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Criar ambiente virtual
Vamos criar um novo ambiente virtual para fins de desenvolvimento (não o adicione toohello repositório). Ambientes virtuais no Python não são relocalizáveis, pelo que cada programador que trabalha na aplicação Olá irá criar os seus próprios localmente.

Certifique-se toouse Olá a mesma versão do Python selecionada para a sua aplicação web (no runtime.txt ou Olá painel de definições da aplicação da sua aplicação web no Portal do Azure de Olá).

Para Python 2.7:

    python -m virtualenv env

Para Python 3.4:

    python -m venv env
ou pyvenv env

Instale quaisquer pacotes externos exigidos pela sua aplicação. Pode utilizar o ficheiro requirements.txt de Olá na raiz de Olá de pacotes de Olá Olá repositório tooinstall num ambiente virtual:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Executar com o servidor de desenvolvimento
Pode iniciar a aplicação Olá num servidor de desenvolvimento com Olá os seguintes comandos:

    env/bin/python app.py

consola de Olá irá apresentar URL Olá e porta Olá server escuta a para:

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

Em seguida, abra o seu URL de toothat do web browser.

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a>Efetuar alterações
Agora, pode experimentar efetuando alterações toohello aplicação origens e/ou modelos.

Depois de ter testado as suas alterações, confirmá-las toohello repositório de Git:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Instalar mais pacotes
A aplicação pode ter dependências que ultrapassam o Python e Bottle.

É possível instalar pacotes adicionais através do pip. Por exemplo, tooinstall Olá Azure SDK para Python, que dá-lhe aceder tooAzure armazenamento, o service bus e outros serviços do Azure, o tipo:

    env/bin/pip install azure

Certifique-se de que tooupdate requirements.txt:

    env/bin/pip freeze > requirements.txt

Consolide alterações de Olá:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Implementar tooAzure
tootrigger uma implementação, Olá push altera tooAzure:

    git push azure master

Irá ver o resultado de Olá do script de implementação de Olá, incluindo a criação do ambiente virtual, instalação de pacotes e criação de Web. config.

Procure toohello Azure URL tooview as suas alterações.

## <a name="troubleshooting---package-installation"></a>Resolução de problemas - Instalação do Pacote
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Resolução de problemas - Ambiente Virtual
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Passos Seguintes
Siga estes toolearn ligações mais informações sobre Bottle e das ferramentas do Python para Visual Studio: 

* [Documentação de Bottle]
* [ferramentas do Python para Visual Studio documentação]

Para obter informações sobre como utilizar o Table Storage do Azure e MongoDB:

* [Bottle e MongoDB no Azure com ferramentas do Python para Visual Studio]
* [Bottle e Table Storage do Azure no Azure com ferramentas do Python para Visual Studio]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Bottle e MongoDB no Azure com ferramentas do Python para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle e Table Storage do Azure no Azure com ferramentas do Python para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[Azure SDK para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git para Windows]: http://msysgit.github.io/
[GitHub para Windows]: https://windows.github.com/
[Ferramentas do Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas do Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[ferramentas do Python para Visual Studio documentação]: http://aka.ms/ptvsdocs 
[Documentação de Bottle]: http://bottlepy.org/docs/dev/index.html

