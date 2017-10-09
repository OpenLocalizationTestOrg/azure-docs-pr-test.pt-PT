---
title: aaaHost um Ruby no Web site Rails de uma VM com Linux | Microsoft Docs
description: "Configurar e alojar um Ruby no Web site baseado em Rails no Azure através de uma máquina virtual Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="86020-103">Aplicação Web Ruby on Rails numa VM do Azure</span><span class="sxs-lookup"><span data-stu-id="86020-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="86020-104">Este tutorial mostra como toohost um Ruby no Web site de Rails no Azure através de uma máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="86020-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="86020-105">Este tutorial foi validado utilizando Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="86020-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="86020-106">Se utilizar uma distribuição diferente do Linux, poderá ser necessário toomodify Olá passos tooinstall Rails.</span><span class="sxs-lookup"><span data-stu-id="86020-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86020-107">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="86020-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="86020-108">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="86020-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="86020-109">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="86020-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="86020-110">Criar uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="86020-110">Create an Azure VM</span></span>
<span data-ttu-id="86020-111">Comece por criar uma VM do Azure com uma imagem de Linux.</span><span class="sxs-lookup"><span data-stu-id="86020-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="86020-112">toocreate Olá VM, pode utilizar Olá portal do Azure ou Olá Interface de linha de comandos do Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="86020-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="86020-113">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="86020-113">Azure portal</span></span>
1. <span data-ttu-id="86020-114">Inicie sessão em Olá [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="86020-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="86020-115">Clique em **novo**, em seguida, escreva "Ubuntu Server 14.04" na caixa de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="86020-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="86020-116">Clique em entrada Olá devolvida pela pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="86020-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="86020-117">Olá modelo de implementação, selecione **clássico**, em seguida, clique em "Criar".</span><span class="sxs-lookup"><span data-stu-id="86020-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="86020-118">No painel de noções básicas de Olá, fornecer valores para os campos de Olá necessário: nome (para Olá VM), nome de utilizador, tipo de autenticação e credenciais correspondentes Olá, subscrição do Azure, grupo de recursos e localização.</span><span class="sxs-lookup"><span data-stu-id="86020-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Criar uma nova imagem de Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="86020-120">Depois de Olá VM é aprovisionado, clique no nome da VM Olá e, em **pontos finais** no Olá **definições** categoria.</span><span class="sxs-lookup"><span data-stu-id="86020-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="86020-121">Localizar o ponto final SSH Olá, listado na **autónomo**.</span><span class="sxs-lookup"><span data-stu-id="86020-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Ponto final predefinido](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="86020-123">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="86020-123">Azure CLI</span></span>
<span data-ttu-id="86020-124">Siga os passos Olá [criar com uma Máquina Virtual a executar Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="86020-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="86020-125">Depois de Olá VM é aprovisionado, pode obter o ponto final de SSH Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="86020-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="86020-126">Instalar Ruby Rails</span><span class="sxs-lookup"><span data-stu-id="86020-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="86020-127">Utilize o SSH tooconnect toohello VM.</span><span class="sxs-lookup"><span data-stu-id="86020-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="86020-128">A partir da sessão SSH Olá, utilize Olá os seguintes comandos tooinstall Ruby no Olá VM:</span><span class="sxs-lookup"><span data-stu-id="86020-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="86020-129">instalação de Olá pode demorar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="86020-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="86020-130">Quando estiver concluída, utilize Olá tooverify de comando que é instalado Ruby os seguintes:</span><span class="sxs-lookup"><span data-stu-id="86020-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="86020-131">Seguinte Olá de utilização de comandos tooinstall Rails:</span><span class="sxs-lookup"><span data-stu-id="86020-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="86020-132">Utilize Olá – não rdoc e – tooskip sinalizadores ri não instalar documentação de Olá, que é mais rápido.</span><span class="sxs-lookup"><span data-stu-id="86020-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="86020-133">Este comando, provavelmente, irá demorar muito tempo tooexecute, para adicionar Olá -V irá apresentar informações sobre o progresso da instalação Olá.</span><span class="sxs-lookup"><span data-stu-id="86020-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="86020-134">Criar e executar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="86020-134">Create and run an app</span></span>
<span data-ttu-id="86020-135">Enquanto continuam a ser registados através de SSH, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="86020-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="86020-136">Olá [novo](http://guides.rubyonrails.org/command_line.html#rails-new) comando cria uma nova aplicação Rails.</span><span class="sxs-lookup"><span data-stu-id="86020-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="86020-137">Olá [servidor](http://guides.rubyonrails.org/command_line.html#rails-server) comando inicia Olá servidor web WEBrick que vem com Rails.</span><span class="sxs-lookup"><span data-stu-id="86020-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="86020-138">(Para utilização em produção, seria provavelmente pretende toouse um servidor diferente, tal como Unicorn ou Passenger.)</span><span class="sxs-lookup"><span data-stu-id="86020-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="86020-139">Deverá ver o seguinte de toohello semelhante de saída.</span><span class="sxs-lookup"><span data-stu-id="86020-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="86020-140">Adicionar um ponto final</span><span class="sxs-lookup"><span data-stu-id="86020-140">Add an endpoint</span></span>
1. <span data-ttu-id="86020-141">Aceda toohello [portal do Azure] [https://portal.azure.com] e selecione a VM.</span><span class="sxs-lookup"><span data-stu-id="86020-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="86020-142">Selecione **pontos finais** no Olá **definições** ao longo da página de Olá Olá limite esquerdo.</span><span class="sxs-lookup"><span data-stu-id="86020-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="86020-143">Clique em **adicionar** em Olá parte superior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="86020-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="86020-144">No Olá **adicionar ponto final** diálogo página, introduza Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="86020-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="86020-145">**Nome**: HTTP</span><span class="sxs-lookup"><span data-stu-id="86020-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="86020-146">**Protocolo**: TCP</span><span class="sxs-lookup"><span data-stu-id="86020-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="86020-147">**Porta pública**: 80</span><span class="sxs-lookup"><span data-stu-id="86020-147">**Public port**: 80</span></span>
   * <span data-ttu-id="86020-148">**Porta privada**: 3000</span><span class="sxs-lookup"><span data-stu-id="86020-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="86020-149">**Endereço de instalador de plataforma de vírgula flutuante**: desativado</span><span class="sxs-lookup"><span data-stu-id="86020-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="86020-150">**Lista de controlo de acesso - ordem**: 1001 ou outro valor que define a prioridade Olá desta regra de acesso.</span><span class="sxs-lookup"><span data-stu-id="86020-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="86020-151">**Lista de controlo de acesso - nome**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="86020-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="86020-152">**Lista de controlo de acesso - ação**: permitir</span><span class="sxs-lookup"><span data-stu-id="86020-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="86020-153">**Lista de controlo de acesso - sub-rede remota**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="86020-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="86020-154">Este ponto final possui uma porta pública 80 que irá encaminhar tráfego toohello porta privada de 3000, onde servidor de Rails Olá está a escutar.</span><span class="sxs-lookup"><span data-stu-id="86020-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="86020-155">regra de lista de controlo de acesso de Olá permite tráfego público na porta 80.</span><span class="sxs-lookup"><span data-stu-id="86020-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![novo ponto final](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="86020-157">Clique em OK toosave Olá endpoint.</span><span class="sxs-lookup"><span data-stu-id="86020-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="86020-158">Deve apresentada uma mensagem que indica **guardar ponto final de máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="86020-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="86020-159">Assim que esta mensagem desaparece, o ponto final de Olá está ativa.</span><span class="sxs-lookup"><span data-stu-id="86020-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="86020-160">Pode agora testar a aplicação ao navegar toohello o nome DNS da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86020-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="86020-161">Web site de Olá deve aparecer semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="86020-161">hello website should appear similar toohello following:</span></span>

    ![página de rails predefinida][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="86020-163">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="86020-163">Next steps</span></span>
<span data-ttu-id="86020-164">Neste tutorial, fez a maior parte dos passos de Olá manualmente.</span><span class="sxs-lookup"><span data-stu-id="86020-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="86020-165">Num ambiente de produção, teria de escrever a sua aplicação no computador de desenvolvimento e implementá-la toohello VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="86020-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="86020-166">Além disso, a maioria dos ambientes de produção alojam a aplicação de Rails de Olá juntamente com outro processo do servidor, tais como o Apache ou NginX, os identificadores de pedem de encaminhamento toomultiple instâncias da aplicação de Rails Olá e que serve recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="86020-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="86020-167">Para obter mais informações, consulte http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="86020-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="86020-168">toolearn mais informações sobre Ruby no Rails, visite Olá [Ruby no Rails guias][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="86020-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="86020-169">toouse serviços do Azure da sua aplicação Ruby, consulte:</span><span class="sxs-lookup"><span data-stu-id="86020-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="86020-170">[Armazenar dados não estruturados com blobs][blobs]</span><span class="sxs-lookup"><span data-stu-id="86020-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="86020-171">[Pares chave/valor de arquivo com tabelas][tables]</span><span class="sxs-lookup"><span data-stu-id="86020-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="86020-172">[Servir conteúdo de largura de banda alta com Olá rede de entrega de conteúdo][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="86020-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
