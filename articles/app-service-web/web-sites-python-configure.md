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
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Configurar o Python com as Web Apps do App Service do Azure
Este tutorial descreve as opções de criação e configuração de uma aplicação básica para o Web Server Gateway Interface (WSGI) em conformidade Python no [Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Descreve as funcionalidades adicionais de implementação de Git, tais como o ambiente virtual e a instalação do pacote com o ficheiro requirements.txt.

## <a name="bottle-django-or-flask"></a>Bottle, Django ou Flask?
Olá, Azure Marketplace contém modelos para estruturas de Olá Bottle, Django e Flask. Se estiver a desenvolver sua primeira aplicação web no App Service do Azure, ou não estiver familiarizado com o Git, recomendamos que siga um destes tutoriais, que incluem instruções passo a passo para a criação de uma aplicação de trabalho a partir da Galeria de Olá utilizando a implementação de Git do Windows ou Mac:

* [Criar web apps com Bottle](web-sites-python-create-deploy-bottle-app.md)
* [Criar web apps com o Django](web-sites-python-create-deploy-django-app.md)
* [Criar web apps com Flask](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Criação da aplicação Web no Portal do Azure
Este tutorial assume uma existente do Azure subscrição e acesso toohello Portal do Azure.

Se não tiver uma aplicação web existente, pode criar um Olá [Portal do Azure](https://portal.azure.com).  Clique no botão novo Olá no canto superior esquerdo de Olá, em seguida, clique em **Web + móvel** > **aplicação Web**.

## <a name="git-publishing"></a>Publicação de Git
Configurar a publicação de Git para a sua aplicação web recentemente criada ao seguir as instruções de Olá em [tooAzure de implementação de Git Local do serviço de aplicações](app-service-deploy-local-git.md). Este tutorial utiliza o Git toocreate, gerir e publicar o nosso tooAzure de aplicação web Python do serviço de aplicações.

Depois de publicação de Git configurada, um repositório de Git será criado e associado à sua aplicação web. URL do repositório de Olá será apresentada e henceforth pode ser utilizados toopush dados da nuvem de toohello de ambiente de desenvolvimento local Olá. toopublish aplicações através do Git, certifique-se também é instalado um cliente do Git e utilize Olá instruções fornecidas toopush sua tooAzure de conteúdo de aplicação de web do serviço de aplicações.

## <a name="application-overview"></a>Descrição Geral da Aplicação
Nas secções seguintes Olá, Olá os seguintes ficheiros é criado. Estes devem ser colocados na raiz de Olá do repositório de Git Olá.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>Processador WSGI
WSGI é uma norma de Python descrita através de [PEP 3333](http://www.python.org/dev/peps/pep-3333/) definir uma interface entre o servidor de web de Olá e Python. Fornece uma interface padronizada para escrever várias aplicações web e estruturas com o Python. Estruturas de web do Python populares utilizam atualmente WSGI. Oferece de Web Apps do App Service do Azure que suporta para qualquer estruturas; Além disso, utilizadores avançados podem ainda criar os seus próprios, desde que o processador personalizado Olá segue diretrizes de especificação de WSGI Olá.

Eis um exemplo de um `app.py` que define um processador personalizado:

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

Pode executar esta aplicação localmente com `python app.py`, em seguida, procure demasiado`http://localhost:5555` no seu browser.

## <a name="virtual-environment"></a>Ambiente virtual
Embora a aplicação de exemplo de Olá acima não requer quaisquer pacotes externos, é provável que a aplicação irá necessitar de algumas.

toohelp gerir as dependências de pacote externo, implementação de Git do Azure suporta a criação de Olá dos ambientes virtuais.

Quando o Azure Deteta um ficheiro requirements.txt na raiz de Olá do repositório de Olá, este cria automaticamente um ambiente virtual com o nome `env`. Isto só ocorre na primeira implementação de hello, ou durante a implementação de após Olá runtime do Python selecionada foi alterada.

Provavelmente pretenderá toocreate um ambiente virtual localmente para o desenvolvimento, mas não incluí-la no seu repositório de Git.

## <a name="package-management"></a>Gestão de Pacotes
Os pacotes listados em requirements.txt são instalados automaticamente no ambiente virtual Olá através do pip. Isto ocorre em todas as implementações, mas o pip saltará a instalação se um pacote já está instalado.

Exemplo `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>Versão do Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

Exemplo `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
Terá de toocreate um toospecify do ficheiro Web. config como servidor de Olá deve processar pedidos.

Tenha em atenção que se tiver um ficheiro de x.y. config no seu repositório, em que corresponde ao x.y Olá selecionados runtime do Python, em seguida, Azure automaticamente vai copiar ficheiro adequado do Olá como Web. config.

Olá exemplos de Web. config seguintes dependem de um script de proxy do ambiente virtual, que está descrito na secção seguinte, Olá.  Funcionam com o processador WSGI Olá utilizado no exemplo de Olá `app.py` acima.

Exemplo `web.config` para Python 2.7:

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


Exemplo `web.config` para Python 3.4:

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


Ficheiros estáticos irão ser processados pelo servidor de web de Olá diretamente, sem passar código Python, para um melhor desempenho.

No Olá acima exemplos, localização Olá de ficheiros estáticos de Olá no disco deve corresponder à localização de Olá no URL Olá. Isto significa que um pedido para `http://pythonapp.azurewebsites.net/static/site.css` irá servir o ficheiro de Olá no disco em `\static\site.css`.

`WSGI_ALT_VIRTUALENV_HANDLER`é aqui que pode especificar o processador WSGI Olá. No Olá acima exemplos, tem `app.wsgi_app` porque o processador de Olá é uma função com o nome `wsgi_app` no `app.py` na pasta raiz de Olá.

`PYTHONPATH`pode ser personalizado, mas se instalar todas as suas dependências no ambiente virtual Olá especificando-los no requirements.txt, não deverá ser preciso toochange-lo.

## <a name="virtual-environment-proxy"></a>Proxy de ambiente virtual
Olá seguinte script é o processador WSGI tooretrieve utilizados Olá, ativar erros de registo e de ambiente virtuais no Olá. É concebida toobe genérico e utilizada sem modificações.

Conteúdo do `ptvs_virtualenv_proxy.py`:

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


## <a name="customize-git-deployment"></a>Personalizar a implementação de Git
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>Resolução de problemas - Instalação do Pacote
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Resolução de problemas - Ambiente Virtual
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte Olá [Centro para programadores do Python](/develop/python/).

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

