---
title: aaaConfiguring Python com as Web Apps do Azure App Service
description: "Este tutorial descreve as opções de criação e configuração de um servidor Web básico aplicação Python compatível do Gateway Interface (WSGI) no Web Apps do Azure App Service."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="699c3-103">Configurar o Python com as Web Apps do App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="699c3-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="699c3-104">Este tutorial descreve as opções de criação e configuração de uma aplicação básica para o Web Server Gateway Interface (WSGI) em conformidade Python no [Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="699c3-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="699c3-105">Descreve as funcionalidades adicionais de implementação de Git, tais como o ambiente virtual e a instalação do pacote com o ficheiro requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="699c3-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="699c3-106">Bottle, Django ou Flask?</span><span class="sxs-lookup"><span data-stu-id="699c3-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="699c3-107">Olá, Azure Marketplace contém modelos para estruturas de Olá Bottle, Django e Flask.</span><span class="sxs-lookup"><span data-stu-id="699c3-107">hello Azure Marketplace contains templates for hello Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="699c3-108">Se estiver a desenvolver sua primeira aplicação web no App Service do Azure, ou não estiver familiarizado com o Git, recomendamos que siga um destes tutoriais, que incluem instruções passo a passo para a criação de uma aplicação de trabalho a partir da Galeria de Olá utilizando a implementação de Git do Windows ou Mac:</span><span class="sxs-lookup"><span data-stu-id="699c3-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from hello gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="699c3-109">Criar web apps com Bottle</span><span class="sxs-lookup"><span data-stu-id="699c3-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="699c3-110">Criar web apps com o Django</span><span class="sxs-lookup"><span data-stu-id="699c3-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="699c3-111">Criar web apps com Flask</span><span class="sxs-lookup"><span data-stu-id="699c3-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="699c3-112">Criação da aplicação Web no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="699c3-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="699c3-113">Este tutorial assume uma existente do Azure subscrição e acesso toohello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="699c3-113">This tutorial assumes an existing Azure subscription and access toohello Azure Portal.</span></span>

<span data-ttu-id="699c3-114">Se não tiver uma aplicação web existente, pode criar um Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="699c3-114">If you do not have an existing web app, you can create one from hello [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="699c3-115">Clique no botão novo Olá no canto superior esquerdo de Olá, em seguida, clique em **Web + móvel** > **aplicação Web**.</span><span class="sxs-lookup"><span data-stu-id="699c3-115">Click hello NEW button in hello top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="699c3-116">Publicação de Git</span><span class="sxs-lookup"><span data-stu-id="699c3-116">Git Publishing</span></span>
<span data-ttu-id="699c3-117">Configurar a publicação de Git para a sua aplicação web recentemente criada ao seguir as instruções de Olá em [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="699c3-117">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="699c3-118">Este tutorial utiliza o Git toocreate, gerir e publicar o nosso tooAzure de aplicação web Python do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="699c3-118">This tutorial uses Git toocreate, manage, and publish our Python web app tooAzure App Service.</span></span>

<span data-ttu-id="699c3-119">Depois de publicação de Git configurada, um repositório de Git será criado e associado à sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="699c3-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="699c3-120">URL do repositório de Olá será apresentada e henceforth pode ser utilizados toopush dados da nuvem de toohello de ambiente de desenvolvimento local Olá.</span><span class="sxs-lookup"><span data-stu-id="699c3-120">hello repository's URL will be displayed and can henceforth be used toopush data from hello local development environment toohello cloud.</span></span> <span data-ttu-id="699c3-121">toopublish aplicações através do Git, certifique-se também é instalado um cliente do Git e utilize Olá instruções fornecidas toopush sua tooAzure de conteúdo de aplicação de web do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="699c3-121">toopublish applications via Git, make sure a Git client is also installed and use hello instructions provided toopush your web app content tooAzure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="699c3-122">Descrição Geral da Aplicação</span><span class="sxs-lookup"><span data-stu-id="699c3-122">Application Overview</span></span>
<span data-ttu-id="699c3-123">Nas secções seguintes Olá, Olá os seguintes ficheiros é criado.</span><span class="sxs-lookup"><span data-stu-id="699c3-123">In hello next sections, hello following files are created.</span></span> <span data-ttu-id="699c3-124">Estes devem ser colocados na raiz de Olá do repositório de Git Olá.</span><span class="sxs-lookup"><span data-stu-id="699c3-124">They should be placed in hello root of hello Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="699c3-125">Processador WSGI</span><span class="sxs-lookup"><span data-stu-id="699c3-125">WSGI Handler</span></span>
<span data-ttu-id="699c3-126">WSGI é uma norma de Python descrita através de [PEP 3333](http://www.python.org/dev/peps/pep-3333/) definir uma interface entre o servidor de web de Olá e Python.</span><span class="sxs-lookup"><span data-stu-id="699c3-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between hello web server and Python.</span></span> <span data-ttu-id="699c3-127">Fornece uma interface padronizada para escrever várias aplicações web e estruturas com o Python.</span><span class="sxs-lookup"><span data-stu-id="699c3-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="699c3-128">Estruturas de web do Python populares utilizam atualmente WSGI.</span><span class="sxs-lookup"><span data-stu-id="699c3-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="699c3-129">Oferece de Web Apps do App Service do Azure que suporta para qualquer estruturas; Além disso, utilizadores avançados podem ainda criar os seus próprios, desde que o processador personalizado Olá segue diretrizes de especificação de WSGI Olá.</span><span class="sxs-lookup"><span data-stu-id="699c3-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as hello custom handler follows hello WSGI specification guidelines.</span></span>

<span data-ttu-id="699c3-130">Eis um exemplo de um `app.py` que define um processador personalizado:</span><span class="sxs-lookup"><span data-stu-id="699c3-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="699c3-131">Pode executar esta aplicação localmente com `python app.py`, em seguida, procure demasiado`http://localhost:5555` no seu browser.</span><span class="sxs-lookup"><span data-stu-id="699c3-131">You can run this application locally with `python app.py`, then browse too`http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="699c3-132">Ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="699c3-132">Virtual Environment</span></span>
<span data-ttu-id="699c3-133">Embora a aplicação de exemplo de Olá acima não requer quaisquer pacotes externos, é provável que a aplicação irá necessitar de algumas.</span><span class="sxs-lookup"><span data-stu-id="699c3-133">Although hello example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="699c3-134">toohelp gerir as dependências de pacote externo, implementação de Git do Azure suporta a criação de Olá dos ambientes virtuais.</span><span class="sxs-lookup"><span data-stu-id="699c3-134">toohelp manage external package dependencies, Azure Git deployment supports hello creation of virtual environments.</span></span>

<span data-ttu-id="699c3-135">Quando o Azure Deteta um ficheiro requirements.txt na raiz de Olá do repositório de Olá, este cria automaticamente um ambiente virtual com o nome `env`.</span><span class="sxs-lookup"><span data-stu-id="699c3-135">When Azure detects a requirements.txt in hello root of hello repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="699c3-136">Isto só ocorre na primeira implementação de hello, ou durante a implementação de após Olá runtime do Python selecionada foi alterada.</span><span class="sxs-lookup"><span data-stu-id="699c3-136">This only occurs on hello first deployment, or during any deployment after hello selected Python runtime has changed.</span></span>

<span data-ttu-id="699c3-137">Provavelmente pretenderá toocreate um ambiente virtual localmente para o desenvolvimento, mas não incluí-la no seu repositório de Git.</span><span class="sxs-lookup"><span data-stu-id="699c3-137">You will probably want toocreate a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="699c3-138">Gestão de Pacotes</span><span class="sxs-lookup"><span data-stu-id="699c3-138">Package Management</span></span>
<span data-ttu-id="699c3-139">Os pacotes listados em requirements.txt são instalados automaticamente no ambiente virtual Olá através do pip.</span><span class="sxs-lookup"><span data-stu-id="699c3-139">Packages listed in requirements.txt will be installed automatically in hello virtual environment using pip.</span></span> <span data-ttu-id="699c3-140">Isto ocorre em todas as implementações, mas o pip saltará a instalação se um pacote já está instalado.</span><span class="sxs-lookup"><span data-stu-id="699c3-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="699c3-141">Exemplo `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="699c3-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="699c3-142">Versão do Python</span><span class="sxs-lookup"><span data-stu-id="699c3-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="699c3-143">Exemplo `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="699c3-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="699c3-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="699c3-144">Web.config</span></span>
<span data-ttu-id="699c3-145">Terá de toocreate um toospecify do ficheiro Web. config como servidor de Olá deve processar pedidos.</span><span class="sxs-lookup"><span data-stu-id="699c3-145">You'll need toocreate a web.config file toospecify how hello server should handle requests.</span></span>

<span data-ttu-id="699c3-146">Tenha em atenção que se tiver um ficheiro de x.y. config no seu repositório, em que corresponde ao x.y Olá selecionados runtime do Python, em seguida, Azure automaticamente vai copiar ficheiro adequado do Olá como Web. config.</span><span class="sxs-lookup"><span data-stu-id="699c3-146">Note that if you have a web.x.y.config file in your repository, where x.y matches hello selected Python runtime, then Azure will automatically copy hello appropriate file as web.config.</span></span>

<span data-ttu-id="699c3-147">Olá exemplos de Web. config seguintes dependem de um script de proxy do ambiente virtual, que está descrito na secção seguinte, Olá.</span><span class="sxs-lookup"><span data-stu-id="699c3-147">hello following web.config examples rely on a virtual environment proxy script, which is described in hello next section.</span></span>  <span data-ttu-id="699c3-148">Funcionam com o processador WSGI Olá utilizado no exemplo de Olá `app.py` acima.</span><span class="sxs-lookup"><span data-stu-id="699c3-148">They work with hello WSGI handler used in hello example `app.py` above.</span></span>

<span data-ttu-id="699c3-149">Exemplo `web.config` para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="699c3-149">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="699c3-150">Exemplo `web.config` para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="699c3-150">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="699c3-151">Ficheiros estáticos irão ser processados pelo servidor de web de Olá diretamente, sem passar código Python, para um melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="699c3-151">Static files will be handled by hello web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="699c3-152">No Olá acima exemplos, localização Olá de ficheiros estáticos de Olá no disco deve corresponder à localização de Olá no URL Olá.</span><span class="sxs-lookup"><span data-stu-id="699c3-152">In hello above examples, hello location of hello static files on disk should match hello location in hello URL.</span></span> <span data-ttu-id="699c3-153">Isto significa que um pedido para `http://pythonapp.azurewebsites.net/static/site.css` irá servir o ficheiro de Olá no disco em `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="699c3-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve hello file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="699c3-154">`WSGI_ALT_VIRTUALENV_HANDLER`é aqui que pode especificar o processador WSGI Olá.</span><span class="sxs-lookup"><span data-stu-id="699c3-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify hello WSGI handler.</span></span> <span data-ttu-id="699c3-155">No Olá acima exemplos, tem `app.wsgi_app` porque o processador de Olá é uma função com o nome `wsgi_app` no `app.py` na pasta raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="699c3-155">In hello above examples, it's `app.wsgi_app` because hello handler is a function named `wsgi_app` in `app.py` in hello root folder.</span></span>

<span data-ttu-id="699c3-156">`PYTHONPATH`pode ser personalizado, mas se instalar todas as suas dependências no ambiente virtual Olá especificando-los no requirements.txt, não deverá ser preciso toochange-lo.</span><span class="sxs-lookup"><span data-stu-id="699c3-156">`PYTHONPATH` can be customized, but if you install all your dependencies in hello virtual environment by specifying them in requirements.txt, you shouldn't need toochange it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="699c3-157">Proxy de ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="699c3-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="699c3-158">Olá seguinte script é o processador WSGI tooretrieve utilizados Olá, ativar erros de registo e de ambiente virtuais no Olá.</span><span class="sxs-lookup"><span data-stu-id="699c3-158">hello following script is used tooretrieve hello WSGI handler, activate hello virtual environment and log errors.</span></span> <span data-ttu-id="699c3-159">É concebida toobe genérico e utilizada sem modificações.</span><span class="sxs-lookup"><span data-stu-id="699c3-159">It is designed toobe generic and used without modifications.</span></span>

<span data-ttu-id="699c3-160">Conteúdo do `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="699c3-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="699c3-161">Personalizar a implementação de Git</span><span class="sxs-lookup"><span data-stu-id="699c3-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="699c3-162">Resolução de problemas - Instalação do Pacote</span><span class="sxs-lookup"><span data-stu-id="699c3-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="699c3-163">Resolução de problemas - Ambiente Virtual</span><span class="sxs-lookup"><span data-stu-id="699c3-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="699c3-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="699c3-164">Next steps</span></span>
<span data-ttu-id="699c3-165">Para obter mais informações, consulte Olá [Centro para programadores do Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="699c3-165">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="699c3-166">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="699c3-166">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="699c3-167">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="699c3-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="699c3-168">O que mudou</span><span class="sxs-lookup"><span data-stu-id="699c3-168">What's changed</span></span>
* <span data-ttu-id="699c3-169">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="699c3-169">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

