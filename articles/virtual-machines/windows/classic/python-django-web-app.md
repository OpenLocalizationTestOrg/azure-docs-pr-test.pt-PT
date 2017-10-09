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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="46a59-103">Aplicação de web Django Olá, mundo numa VM do Windows</span><span class="sxs-lookup"><span data-stu-id="46a59-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="46a59-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [modelo de implementação clássica Azure Resource Manager e Olá](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="46a59-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="46a59-105">Este artigo descreve o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="46a59-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="46a59-106">Recomendamos que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="46a59-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="46a59-107">Este tutorial mostra como toohost um Web site baseado em Django no Windows Server em Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="46a59-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="46a59-108">Tutorial de Olá, partimos sem experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="46a59-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="46a59-109">Quando concluir o tutorial Olá, pode ter uma aplicação Django com base em cópia de segurança e em execução na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="46a59-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="46a59-110">Aprenda a:</span><span class="sxs-lookup"><span data-stu-id="46a59-110">Learn how to:</span></span>

* <span data-ttu-id="46a59-111">Configure uma máquina virtual do Azure de toohost Django.</span><span class="sxs-lookup"><span data-stu-id="46a59-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="46a59-112">Embora este tutorial explica como toodo isto para **do Windows Server**, pode fazê-lo Olá mesmo para uma VM com Linux alojados no Azure.</span><span class="sxs-lookup"><span data-stu-id="46a59-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="46a59-113">Crie uma nova aplicação Django no Windows.</span><span class="sxs-lookup"><span data-stu-id="46a59-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="46a59-114">tutorial de Olá mostra como toobuild um básico Olá, mundo aplicação web.</span><span class="sxs-lookup"><span data-stu-id="46a59-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="46a59-115">aplicação Olá está alojada numa máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="46a59-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="46a59-116">Olá seguinte captura de ecrã mostra aplicação Olá concluída:</span><span class="sxs-lookup"><span data-stu-id="46a59-116">hello following screenshot shows hello completed application:</span></span>

![Uma janela do browser apresenta a página Olá, mundo Olá no Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="46a59-118">Criar e configurar uma máquina virtual do Azure de toohost Django</span><span class="sxs-lookup"><span data-stu-id="46a59-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="46a59-119">toocreate uma máquina virtual do Azure com Olá distribuição do Windows Server 2012 R2 Datacenter, consulte [criar uma máquina virtual com o Windows hello portal do Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="46a59-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="46a59-120">Definir o tráfego de porta 80 toodirect do Azure a partir da Olá web tooport 80 na máquina virtual de Olá:</span><span class="sxs-lookup"><span data-stu-id="46a59-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="46a59-121">No portal do Azure Olá, aceda a toohello dashboard e selecione a máquina virtual recentemente criada.</span><span class="sxs-lookup"><span data-stu-id="46a59-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="46a59-122">Clique em **Pontos finais** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="46a59-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Adicionar um ponto final](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="46a59-124">No Olá **adicionar ponto final** página, para **nome**, introduza **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="46a59-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="46a59-125">Definir portas TCP de Olá públicas e privadas demasiado**80**.</span><span class="sxs-lookup"><span data-stu-id="46a59-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Introduza o nome e defina portas públicas e privadas](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="46a59-127">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="46a59-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="46a59-128">No dashboard de Olá, selecione a VM.</span><span class="sxs-lookup"><span data-stu-id="46a59-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="46a59-129">toouse protocolo RDP (Remote Desktop Protocol) tooremotely início de sessão toohello recentemente criada a máquina virtual do Azure, clique em **Connect**.</span><span class="sxs-lookup"><span data-stu-id="46a59-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="46a59-130">Olá seguir instruções partem do princípio de que iniciou a máquina virtual de toohello corretamente.</span><span class="sxs-lookup"><span data-stu-id="46a59-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="46a59-131">Eles também partem do princípio de que está a emitir comandos na máquina virtual de Olá e não no computador local.</span><span class="sxs-lookup"><span data-stu-id="46a59-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="46a59-132"><a id="setup"></a>Instalar o Python, Django e WFastCGI</span><span class="sxs-lookup"><span data-stu-id="46a59-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="46a59-133">toodownload utilizando o Internet Explorer, pode ter tooconfigure Internet Explorer **configuração de segurança avançada** definições.</span><span class="sxs-lookup"><span data-stu-id="46a59-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="46a59-134">toodo, clique em **iniciar** > **ferramentas administrativas** > **Gestor de servidor** > **deservidorLocal**.</span><span class="sxs-lookup"><span data-stu-id="46a59-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="46a59-135">Clique em **configuração de segurança avançada do IE**e, em seguida, selecione **desativar**.</span><span class="sxs-lookup"><span data-stu-id="46a59-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="46a59-136">Instalar versões mais recentes do Olá do Python 2.7 ou 3.4 Python do [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="46a59-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="46a59-137">Instale pacotes de wfastcgi e django de Olá através do pip.</span><span class="sxs-lookup"><span data-stu-id="46a59-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="46a59-138">Para Python 2.7, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46a59-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="46a59-139">Para Python 3.4, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46a59-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="46a59-140">Instalar o IIS com FastCGI</span><span class="sxs-lookup"><span data-stu-id="46a59-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="46a59-141">Instale serviços de informação Internet (IIS) com suporte de FastCGI.</span><span class="sxs-lookup"><span data-stu-id="46a59-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="46a59-142">Esta ação poderá demorar vários minutos tooexecute.</span><span class="sxs-lookup"><span data-stu-id="46a59-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="46a59-143">Criar uma nova aplicação Django</span><span class="sxs-lookup"><span data-stu-id="46a59-143">Create a new Django application</span></span>
1. <span data-ttu-id="46a59-144">Na C:\inetpub\wwwroot, toocreate um novo projeto do Django, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46a59-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="46a59-145">Para Python 2.7, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46a59-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="46a59-146">Para Python 3.4, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46a59-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![resultado de Olá do comando de Olá New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="46a59-148">Olá `django-admin` comandos gera uma estrutura básica para Web sites baseados em Django:</span><span class="sxs-lookup"><span data-stu-id="46a59-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="46a59-149">`helloworld\manage.py`ajuda-o a alojar o início e paragem que aloja o Web site baseado em Django.</span><span class="sxs-lookup"><span data-stu-id="46a59-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="46a59-150">`helloworld\helloworld\settings.py`tem Django definições para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="46a59-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="46a59-151">`helloworld\helloworld\urls.py`tem o código de mapeamento de Olá entre cada URL e a vista.</span><span class="sxs-lookup"><span data-stu-id="46a59-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="46a59-152">No diretório de C:\inetpub\wwwroot\helloworld\helloworld Olá, crie um novo ficheiro designado views.py.</span><span class="sxs-lookup"><span data-stu-id="46a59-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="46a59-153">Este ficheiro tem uma vista de Olá que compõe a página de "Olá mundo" Olá.</span><span class="sxs-lookup"><span data-stu-id="46a59-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="46a59-154">No seu editor de código, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46a59-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="46a59-155">Substitua Olá conteúdo de Olá urls.py ficheiro Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46a59-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="46a59-156">Configurar o IIS</span><span class="sxs-lookup"><span data-stu-id="46a59-156">Set up IIS</span></span>
1. <span data-ttu-id="46a59-157">No ficheiro de no applicationHost. config global Olá, desbloquear a secção de processadores de Olá.</span><span class="sxs-lookup"><span data-stu-id="46a59-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="46a59-158">Isto permite que o processador de Python do Web. config ficheiros toouse Olá.</span><span class="sxs-lookup"><span data-stu-id="46a59-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="46a59-159">Adicione este comando:</span><span class="sxs-lookup"><span data-stu-id="46a59-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="46a59-160">Ative WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="46a59-160">Activate WFastCGI.</span></span> <span data-ttu-id="46a59-161">Esta ação adiciona um ficheiro de no applicationHost. config global toohello aplicação, que se refere tooyour interpretador executável e Olá wfastcgi.py script do Python.</span><span class="sxs-lookup"><span data-stu-id="46a59-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="46a59-162">No Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="46a59-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="46a59-163">No Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="46a59-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="46a59-164">C:\inetpub\wwwroot\helloworld, crie um ficheiro Web. config.</span><span class="sxs-lookup"><span data-stu-id="46a59-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="46a59-165">Olá, valor de Olá `scriptProcessor` atributo deve corresponder ao resultado Olá Olá precedente passo.</span><span class="sxs-lookup"><span data-stu-id="46a59-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="46a59-166">Para obter mais informações sobre a definição de wfastcgi Olá, consulte [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="46a59-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="46a59-167">No Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="46a59-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="46a59-168">No Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="46a59-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="46a59-169">Atualize a localização de Olá de Olá IIS predefinido toopoint toohello Django projeto pasta do Web site:</span><span class="sxs-lookup"><span data-stu-id="46a59-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="46a59-170">Carregar a página Olá Web no browser.</span><span class="sxs-lookup"><span data-stu-id="46a59-170">Load hello webpage in your browser.</span></span>

![Uma janela do browser apresenta a página Olá, mundo Olá no Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="46a59-172">Encerre a máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="46a59-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="46a59-173">Quando tiver terminado com este tutorial, recomendamos que encerre ou remover Olá VM do Azure que criou para o tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="46a59-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="46a59-174">Esta ação liberta recursos para outros tutoriais e pode evitar incorrer em custos de utilização do Azure.</span><span class="sxs-lookup"><span data-stu-id="46a59-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
