---
title: "aplicação web de aaaPython com o Django no VM Linux do Azure | Microsoft Docs"
description: "Saiba como toohost a com base em Django web de aplicação no Azure através de uma VM com Linux."
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="4f013-103">Aplicação de web Django Olá, mundo numa VM com Linux</span><span class="sxs-lookup"><span data-stu-id="4f013-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f013-104">Windows</span><span class="sxs-lookup"><span data-stu-id="4f013-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="4f013-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="4f013-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="4f013-106">Este tutorial mostra como toohost um Web site baseado em Django no Linux em Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="4f013-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="4f013-107">Tutorial de Olá, partimos sem experiência anterior com o Azure.</span><span class="sxs-lookup"><span data-stu-id="4f013-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="4f013-108">Quando concluir o tutorial Olá, pode ter uma aplicação Django com base em cópia de segurança e em execução na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="4f013-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="4f013-109">Aprenda a:</span><span class="sxs-lookup"><span data-stu-id="4f013-109">Learn how to:</span></span>

* <span data-ttu-id="4f013-110">Configure uma máquina virtual do Azure de toohost Django.</span><span class="sxs-lookup"><span data-stu-id="4f013-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="4f013-111">Embora este tutorial explica como toodo isto para **Linux**, pode fazê-lo hello mesmo para uma VM do Windows Server alojado no Azure.</span><span class="sxs-lookup"><span data-stu-id="4f013-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="4f013-112">Crie uma nova aplicação Django no Linux.</span><span class="sxs-lookup"><span data-stu-id="4f013-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="4f013-113">tutorial de Olá mostra como toobuild um básico Olá, mundo aplicação web.</span><span class="sxs-lookup"><span data-stu-id="4f013-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="4f013-114">aplicação Olá está alojada numa máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f013-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="4f013-115">Olá seguinte captura de ecrã mostra aplicação Olá concluída:</span><span class="sxs-lookup"><span data-stu-id="4f013-115">hello following screenshot shows hello completed application:</span></span>

![Uma janela do browser apresenta a página Olá, mundo Olá no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="4f013-117">Criar e configurar uma máquina virtual do Azure de toohost Django</span><span class="sxs-lookup"><span data-stu-id="4f013-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="4f013-118">toocreate uma máquina virtual do Azure com Olá distribuição Ubuntu Server 14.04 LTS, consulte [criar uma máquina virtual Linux no portal do Azure de Olá](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f013-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4f013-119">Também pode escolher a autenticação de palavra-passe em vez de utilizar uma chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="4f013-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="4f013-120">tooedit Olá rede segurança grupo tooallow entrada HTTP tráfego tooport 80, consulte [criar grupos de segurança de rede no portal do Azure de Olá](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4f013-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="4f013-121">(Opcional) Por predefinição, a nova máquina virtual não tem um nome de domínio completamente qualificado (FQDN).</span><span class="sxs-lookup"><span data-stu-id="4f013-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="4f013-122">toocreate uma VM com um FQDN, consulte [criar um FQDN no Olá portal do Azure para uma VM do Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f013-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4f013-123">Este passo não é necessário para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4f013-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="4f013-124"><a id="setup"></a>Configurar o ambiente de desenvolvimento de Olá</span><span class="sxs-lookup"><span data-stu-id="4f013-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="4f013-125">Se precisar de tooinstall Python ou quiser bibliotecas de cliente toouse Olá, consulte Olá [guia de instalação do Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="4f013-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="4f013-126">Olá Ubuntu Linux VM tem o Python 2.7 pré-instalado, mas não são fornecidos com Apache ou Django.</span><span class="sxs-lookup"><span data-stu-id="4f013-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="4f013-127">Concluir Olá os seguintes passos tooconnect tooyour VM e instalar o Apache e Django:</span><span class="sxs-lookup"><span data-stu-id="4f013-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="4f013-128">Abra uma nova janela de Terminal.</span><span class="sxs-lookup"><span data-stu-id="4f013-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="4f013-129">tooconnect toohello VM do Azure, introduza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="4f013-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="4f013-130">Se não tiver criado um FQDN, pode ligar utilizando o endereço IP público Olá que é apresentado na máquina virtual de Olá resumo no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f013-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="4f013-131">tooinstall Django, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4f013-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="4f013-132">tooinstall Apache com mod wsgi, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4f013-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="4f013-133">Criar uma nova aplicação Django</span><span class="sxs-lookup"><span data-stu-id="4f013-133">Create a new Django app</span></span>
1. <span data-ttu-id="4f013-134">toouse SSH tooaccess a sua VM, a janela de Terminal aberto Olá que utilizou no Olá anterior a secção.</span><span class="sxs-lookup"><span data-stu-id="4f013-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="4f013-135">toocreate um novo projeto do Django, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4f013-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="4f013-136">Olá `django-admin.py` script gera uma estrutura básica para Web sites baseados em Django:</span><span class="sxs-lookup"><span data-stu-id="4f013-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="4f013-137">`helloworld/manage.py`ajuda-o a alojar o início e paragem que aloja o Web site baseado em Django.</span><span class="sxs-lookup"><span data-stu-id="4f013-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="4f013-138">`helloworld/helloworld/settings.py`tem Django definições para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="4f013-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="4f013-139">`helloworld/helloworld/urls.py`tem o código de mapeamento de Olá entre cada URL e a vista.</span><span class="sxs-lookup"><span data-stu-id="4f013-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="4f013-140">No diretório de /var/www/helloworld/helloworld Olá, crie um novo ficheiro designado views.py.</span><span class="sxs-lookup"><span data-stu-id="4f013-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="4f013-141">Este ficheiro tem uma vista de Olá que compõe a página de "Olá mundo" Olá.</span><span class="sxs-lookup"><span data-stu-id="4f013-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="4f013-142">No seu editor de código, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4f013-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="4f013-143">Substitua Olá conteúdo de Olá urls.py ficheiro Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4f013-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="4f013-144">Configurar o Apache</span><span class="sxs-lookup"><span data-stu-id="4f013-144">Set up Apache</span></span>
1. <span data-ttu-id="4f013-145">Na pasta de /etc/apache2/sites-available/helloworld.conf Olá, crie um ficheiro de configuração de anfitrião virtual Apache.</span><span class="sxs-lookup"><span data-stu-id="4f013-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="4f013-146">Definir Olá conteúdo toohello os seguintes valores.</span><span class="sxs-lookup"><span data-stu-id="4f013-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="4f013-147">Substitua *yourVmName* com o nome real do Olá da máquina de Olá estiver a utilizar (por exemplo, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="4f013-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="4f013-148">tooactivate Olá site Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4f013-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="4f013-149">toorestart Apache, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4f013-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="4f013-150">Carregar a página Olá Web no browser:</span><span class="sxs-lookup"><span data-stu-id="4f013-150">Load hello webpage in your browser:</span></span>
   
   ![Uma janela do browser apresenta a página Olá, mundo Olá no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="4f013-152">Encerre a máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="4f013-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="4f013-153">Quando tiver terminado com este tutorial, recomendamos que encerre ou remover Olá VM do Azure que criou para o tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="4f013-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="4f013-154">Esta ação liberta recursos para outros tutoriais e pode evitar incorrer em custos de utilização do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f013-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

