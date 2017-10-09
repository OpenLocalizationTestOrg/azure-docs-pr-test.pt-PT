---
title: "aplicação web aaaDjango uma VM do Azure do Windows Server | Microsoft Docs"
description: "Saiba como toohost um Web site baseado em Django no Azure através de uma VM do Windows Server 2012 R2 Datacenter com o modelo de implementação clássica Olá."
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Aplicação de web Django Olá, mundo numa VM do Windows

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [modelo de implementação clássica Azure Resource Manager e Olá](../../../resource-manager-deployment-model.md). Este artigo descreve o modelo de implementação clássica Olá. Recomendamos que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

Este tutorial mostra como toohost um Web site baseado em Django no Windows Server em Azure Virtual Machines. Tutorial de Olá, partimos sem experiência anterior com o Azure. Quando concluir o tutorial Olá, pode ter uma aplicação Django com base em cópia de segurança e em execução na nuvem de Olá.

Aprenda a:

* Configure uma máquina virtual do Azure de toohost Django. Embora este tutorial explica como toodo isto para **do Windows Server**, pode fazê-lo Olá mesmo para uma VM com Linux alojados no Azure.
* Crie uma nova aplicação Django no Windows.

tutorial de Olá mostra como toobuild um básico Olá, mundo aplicação web. aplicação Olá está alojada numa máquina virtual do Azure.

Olá seguinte captura de ecrã mostra aplicação Olá concluída:

![Uma janela do browser apresenta a página Olá, mundo Olá no Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Criar e configurar uma máquina virtual do Azure de toohost Django

1. toocreate uma máquina virtual do Azure com Olá distribuição do Windows Server 2012 R2 Datacenter, consulte [criar uma máquina virtual com o Windows hello portal do Azure](tutorial.md).
2. Definir o tráfego de porta 80 toodirect do Azure a partir da Olá web tooport 80 na máquina virtual de Olá:
   
   1. No portal do Azure Olá, aceda a toohello dashboard e selecione a máquina virtual recentemente criada.
   2. Clique em **Pontos finais** e, em seguida, clique em **Adicionar**.

     ![Adicionar um ponto final](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. No Olá **adicionar ponto final** página, para **nome**, introduza **HTTP**. Definir portas TCP de Olá públicas e privadas demasiado**80**.

     ![Introduza o nome e defina portas públicas e privadas](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. Clique em **OK**.
     
3. No dashboard de Olá, selecione a VM. toouse protocolo RDP (Remote Desktop Protocol) tooremotely início de sessão toohello recentemente criada a máquina virtual do Azure, clique em **Connect**.  

> [!IMPORTANT] 
> Olá seguir instruções partem do princípio de que iniciou a máquina virtual de toohello corretamente. Eles também partem do princípio de que está a emitir comandos na máquina virtual de Olá e não no computador local.

## <a id="setup"></a>Instalar o Python, Django e WFastCGI
> [!NOTE]
> toodownload utilizando o Internet Explorer, pode ter tooconfigure Internet Explorer **configuração de segurança avançada** definições. toodo, clique em **iniciar** > **ferramentas administrativas** > **Gestor de servidor** > **deservidorLocal**. Clique em **configuração de segurança avançada do IE**e, em seguida, selecione **desativar**.

1. Instalar versões mais recentes do Olá do Python 2.7 ou 3.4 Python do [python.org][python.org].
2. Instale pacotes de wfastcgi e django de Olá através do pip.
   
    Para Python 2.7, utilize Olá os seguintes comandos:
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Para Python 3.4, utilize Olá os seguintes comandos:
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>Instalar o IIS com FastCGI
* Instale serviços de informação Internet (IIS) com suporte de FastCGI. Esta ação poderá demorar vários minutos tooexecute.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Criar uma nova aplicação Django
1. Na C:\inetpub\wwwroot, toocreate um novo projeto do Django, introduza Olá os seguintes comandos:
   
   Para Python 2.7, utilize Olá os seguintes comandos:
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Para Python 3.4, utilize Olá os seguintes comandos:
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![resultado de Olá do comando de Olá New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Olá `django-admin` comandos gera uma estrutura básica para Web sites baseados em Django:
   
   * `helloworld\manage.py`ajuda-o a alojar o início e paragem que aloja o Web site baseado em Django.
   * `helloworld\helloworld\settings.py`tem Django definições para a sua aplicação.
   * `helloworld\helloworld\urls.py`tem o código de mapeamento de Olá entre cada URL e a vista.
3. No diretório de C:\inetpub\wwwroot\helloworld\helloworld Olá, crie um novo ficheiro designado views.py. Este ficheiro tem uma vista de Olá que compõe a página de "Olá mundo" Olá. No seu editor de código, introduza Olá os seguintes comandos:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Substitua Olá conteúdo de Olá urls.py ficheiro Olá os seguintes comandos:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>Configurar o IIS
1. No ficheiro de no applicationHost. config global Olá, desbloquear a secção de processadores de Olá.  Isto permite que o processador de Python do Web. config ficheiros toouse Olá. Adicione este comando:
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. Ative WFastCGI. Esta ação adiciona um ficheiro de no applicationHost. config global toohello aplicação, que se refere tooyour interpretador executável e Olá wfastcgi.py script do Python.
   
    No Python 2.7:
   
        C:\python27\scripts\wfastcgi-enable
   
    No Python 3.4:
   
        C:\python34\scripts\wfastcgi-enable
3. C:\inetpub\wwwroot\helloworld, crie um ficheiro Web. config. Olá, valor de Olá `scriptProcessor` atributo deve corresponder ao resultado Olá Olá precedente passo. Para obter mais informações sobre a definição de wfastcgi Olá, consulte [pypi wfastcgi][wfastcgi].
   
   No Python 2.7:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   No Python 3.4:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. Atualize a localização de Olá de Olá IIS predefinido toopoint toohello Django projeto pasta do Web site:
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Carregar a página Olá Web no browser.

![Uma janela do browser apresenta a página Olá, mundo Olá no Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Encerre a máquina virtual do Azure
Quando tiver terminado com este tutorial, recomendamos que encerre ou remover Olá VM do Azure que criou para o tutorial Olá. Esta ação liberta recursos para outros tutoriais e pode evitar incorrer em custos de utilização do Azure.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
