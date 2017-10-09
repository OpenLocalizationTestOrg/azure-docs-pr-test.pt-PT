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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Aplicação de web Django Olá, mundo numa VM com Linux
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Este tutorial mostra como toohost um Web site baseado em Django no Linux em Azure Virtual Machines. Tutorial de Olá, partimos sem experiência anterior com o Azure. Quando concluir o tutorial Olá, pode ter uma aplicação Django com base em cópia de segurança e em execução na nuvem de Olá.

Aprenda a:

* Configure uma máquina virtual do Azure de toohost Django. Embora este tutorial explica como toodo isto para **Linux**, pode fazê-lo hello mesmo para uma VM do Windows Server alojado no Azure. 
* Crie uma nova aplicação Django no Linux.

tutorial de Olá mostra como toobuild um básico Olá, mundo aplicação web. aplicação Olá está alojada numa máquina virtual do Azure.

Olá seguinte captura de ecrã mostra aplicação Olá concluída:

![Uma janela do browser apresenta a página Olá, mundo Olá no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Criar e configurar uma máquina virtual do Azure de toohost Django

1. toocreate uma máquina virtual do Azure com Olá distribuição Ubuntu Server 14.04 LTS, consulte [criar uma máquina virtual Linux no portal do Azure de Olá](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Também pode escolher a autenticação de palavra-passe em vez de utilizar uma chave pública SSH.
2. tooedit Olá rede segurança grupo tooallow entrada HTTP tráfego tooport 80, consulte [criar grupos de segurança de rede no portal do Azure de Olá](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Opcional) Por predefinição, a nova máquina virtual não tem um nome de domínio completamente qualificado (FQDN).  toocreate uma VM com um FQDN, consulte [criar um FQDN no Olá portal do Azure para uma VM do Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Este passo não é necessário para concluir este tutorial.

## <a id="setup"></a>Configurar o ambiente de desenvolvimento de Olá
> [!NOTE]
> Se precisar de tooinstall Python ou quiser bibliotecas de cliente toouse Olá, consulte Olá [guia de instalação do Python](../../python-how-to-install.md).

Olá Ubuntu Linux VM tem o Python 2.7 pré-instalado, mas não são fornecidos com Apache ou Django. Concluir Olá os seguintes passos tooconnect tooyour VM e instalar o Apache e Django:

1. Abra uma nova janela de Terminal.
2. tooconnect toohello VM do Azure, introduza Olá os seguintes comandos. Se não tiver criado um FQDN, pode ligar utilizando o endereço IP público Olá que é apresentado na máquina virtual de Olá resumo no Olá portal do Azure.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, introduza Olá os seguintes comandos:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache com mod wsgi, introduza Olá os seguintes comandos:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Criar uma nova aplicação Django
1. toouse SSH tooaccess a sua VM, a janela de Terminal aberto Olá que utilizou no Olá anterior a secção.
2. toocreate um novo projeto do Django, introduza Olá os seguintes comandos:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Olá `django-admin.py` script gera uma estrutura básica para Web sites baseados em Django:
   
   * `helloworld/manage.py`ajuda-o a alojar o início e paragem que aloja o Web site baseado em Django.
   * `helloworld/helloworld/settings.py`tem Django definições para a sua aplicação.
   * `helloworld/helloworld/urls.py`tem o código de mapeamento de Olá entre cada URL e a vista.
3. No diretório de /var/www/helloworld/helloworld Olá, crie um novo ficheiro designado views.py. Este ficheiro tem uma vista de Olá que compõe a página de "Olá mundo" Olá. No seu editor de código, introduza Olá os seguintes comandos:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Substitua Olá conteúdo de Olá urls.py ficheiro Olá os seguintes comandos:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Configurar o Apache
1. Na pasta de /etc/apache2/sites-available/helloworld.conf Olá, crie um ficheiro de configuração de anfitrião virtual Apache. Definir Olá conteúdo toohello os seguintes valores. Substitua *yourVmName* com o nome real do Olá da máquina de Olá estiver a utilizar (por exemplo, *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. tooactivate Olá site Olá utilize os seguintes comandos:
   
       $ sudo a2ensite helloworld
3. toorestart Apache, utilize Olá os seguintes comandos:
   
       $ sudo service apache2 reload
4. Carregar a página Olá Web no browser:
   
   ![Uma janela do browser apresenta a página Olá, mundo Olá no Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Encerre a máquina virtual do Azure
Quando tiver terminado com este tutorial, recomendamos que encerre ou remover Olá VM do Azure que criou para o tutorial Olá. Esta ação liberta recursos para outros tutoriais e pode evitar incorrer em custos de utilização do Azure.

