---
title: "aaaUsing Docker extensão da VM para Linux | Microsoft Docs"
description: "Descreve Docker e extensões de máquinas virtuais do Azure Olá, e como toocreate máquinas de virtuais do Azure através de anfitriões de docker Olá CLI do Azure no modelo de implementação clássica."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="65182-103">Utilizar Olá Docker extensão da VM com Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="65182-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="65182-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="65182-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="65182-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="65182-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="65182-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="65182-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="65182-107">[Docker](https://www.docker.com/) é uma das Olá mais populares abordagens de Virtualização que utiliza [Linux contentores](http://en.wikipedia.org/wiki/LXC) em vez de máquinas virtuais como uma forma de isolando os dados e computação em recursos partilhados.</span><span class="sxs-lookup"><span data-stu-id="65182-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="65182-108">Pode utilizar a extensão de VM de Docker Olá gerido pelo [agente Linux do Azure] toocreate uma VM de Docker que aloja qualquer número de contentores para as suas aplicações no Azure.</span><span class="sxs-lookup"><span data-stu-id="65182-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="65182-109">Este tópico descreve como toocreate uma VM a partir do Docker Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="65182-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="65182-110">toosee como toocreate uma VM de Docker na linha de comandos Olá, consulte [como toouse Olá Docker extensão da VM do Olá Interface de linha de comandos do Azure (CLI do Azure)].</span><span class="sxs-lookup"><span data-stu-id="65182-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="65182-111">toosee um debate de alto nível de contentores e as vantagens, consulte Olá [Whiteboard de nível elevado de Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="65182-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="65182-112">Criar uma nova VM a partir de Olá Galeria de imagem</span><span class="sxs-lookup"><span data-stu-id="65182-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="65182-113">primeiro passo de Olá necessita de uma VM do Azure a partir de uma imagem de Linux que suporte Olá extensão da VM Docker, utilizando uma imagem de Ubuntu 14.04 LTS de Olá imagem galeria como uma imagem de servidor de exemplo e ambiente de trabalho do Ubuntu 14.04 como um cliente.</span><span class="sxs-lookup"><span data-stu-id="65182-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="65182-114">No portal de Olá, clique em **+ novo** no Olá na parte inferior esquerda canto toocreate uma nova instância VM e selecione uma imagem de Ubuntu 14.04 LTS seleções Olá disponíveis ou a Olá concluir Galeria de imagem, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="65182-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="65182-115">Atualmente, apenas Ubuntu 14.04 LTS imagens mais recentes de Julho de 2014 suportam Olá Docker extensão da VM.</span><span class="sxs-lookup"><span data-stu-id="65182-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Criar uma nova imagem de Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="65182-117">Criar certificados de Docker</span><span class="sxs-lookup"><span data-stu-id="65182-117">Create Docker Certificates</span></span>
<span data-ttu-id="65182-118">Depois de Olá que VM foi criada, certifique-se de que o Docker está instalado no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="65182-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="65182-119">(Para obter mais informações, consulte [instruções de instalação do Docker](https://docs.docker.com/installation/#installation).)</span><span class="sxs-lookup"><span data-stu-id="65182-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="65182-120">Criar ficheiros de certificado e chave para a comunicação de Docker demasiado de acordo com a Olá[Docker em execução com https] e colocá-los no Olá  **`~/.docker`**  diretório no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="65182-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="65182-121">Olá Docker extensão da VM no portal de Olá atualmente exige credenciais que são codificados em base64.</span><span class="sxs-lookup"><span data-stu-id="65182-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="65182-122">Na linha de comandos Olá, utilize  **`base64`**  ou outro favorito codificação tópicos da ferramenta toocreate com codificação base64.</span><span class="sxs-lookup"><span data-stu-id="65182-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="65182-123">Fazê-lo com um conjunto simples de ficheiros de certificado e a chave poderá ter um aspeto semelhante toothis:</span><span class="sxs-lookup"><span data-stu-id="65182-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="65182-124">Adicionar Olá Docker extensão da VM</span><span class="sxs-lookup"><span data-stu-id="65182-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="65182-125">tooadd Olá Docker extensão da VM, localize a instância de VM de Olá que criou e desloque para baixo demasiado**extensões** e clique no mesmo toobring configurar extensões de VM, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="65182-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="65182-126">Esta funcionalidade é suportada apenas o portal de pré-visualização Olá: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="65182-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="65182-127">Adicionar uma extensão</span><span class="sxs-lookup"><span data-stu-id="65182-127">Add an Extension</span></span>
<span data-ttu-id="65182-128">Clique em Olá **+ adicionar** toodisplay Olá extensões possíveis das VMS, pode adicionar toothis VM.</span><span class="sxs-lookup"><span data-stu-id="65182-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="65182-129">Selecione Olá Docker extensão da VM</span><span class="sxs-lookup"><span data-stu-id="65182-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="65182-130">Escolha Olá extensão de VM de Docker, aparece a descrição de Docker Olá e ligações importantes, e, em seguida, clique em **criar** no procedimento de instalação do Olá inferior toobegin Olá.</span><span class="sxs-lookup"><span data-stu-id="65182-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="65182-131">Adicione o certificado e ficheiros de chave:</span><span class="sxs-lookup"><span data-stu-id="65182-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="65182-132">Nos campos de formulário Olá, introduza Olá com codificação base64 as versões do seu certificado da AC, o certificado de servidor e a chave de servidor, conforme mostrado no Olá gráfico a seguir.</span><span class="sxs-lookup"><span data-stu-id="65182-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="65182-133">Tenha em atenção que (tal como no Olá anterior a imagem) Olá 2376 é preenchido por predefinição.</span><span class="sxs-lookup"><span data-stu-id="65182-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="65182-134">Pode introduzir qualquer ponto final aqui, mas o passo seguinte Olá serão tooopen segurança Olá correspondente ao ponto final.</span><span class="sxs-lookup"><span data-stu-id="65182-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="65182-135">Se alterar a predefinição de Olá, certifique-se de que tooopen segurança Olá correspondente ao ponto final no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="65182-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="65182-136">Adicionar Olá ponto final de comunicação do Docker</span><span class="sxs-lookup"><span data-stu-id="65182-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="65182-137">Ao visualizar o grupo de recursos de Olá que criou, selecione o grupo de segurança de rede associado à VM de Olá e clique em **regras de segurança de entrada** tooview Olá regras conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="65182-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="65182-138">Clique em **+ adicionar** tooadd outra regra e no caso de predefinição Olá, introduza um nome para o ponto final de Olá (neste exemplo, **Docker**) e 2376 'destino intervalo de portas'.</span><span class="sxs-lookup"><span data-stu-id="65182-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="65182-139">Definir a apresentação de valor de protocolo de Olá **TCP**e clique em **OK** regra de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="65182-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="65182-140">Testar o cliente de Docker e anfitriões de Docker do Azure</span><span class="sxs-lookup"><span data-stu-id="65182-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="65182-141">Localize e copie o nome de Olá do domínio da VM e, na linha de comandos Olá do computador cliente, tipo `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (onde *dockerextension* é substituído pela Olá subdomínio para a VM).</span><span class="sxs-lookup"><span data-stu-id="65182-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="65182-142">resultado de Olá deve aparecer toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="65182-142">hello result should appear similar toothis:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="65182-143">Depois de concluir Olá os passos acima, tem agora um anfitrião de Docker totalmente funcional com uma VM do Azure, toobe ligado tooremotely a partir de outros clientes.</span><span class="sxs-lookup"><span data-stu-id="65182-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="65182-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="65182-144">Next steps</span></span>
<span data-ttu-id="65182-145">Está pronto toogo toohello [Guia do utilizador Docker] e utilizar a VM de Docker.</span><span class="sxs-lookup"><span data-stu-id="65182-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="65182-146">Se quiser tooautomate criar anfitriões de Docker em VMs do Azure através da interface de linha de comandos, consulte [como toouse Olá Docker extensão da VM do Olá Interface de linha de comandos do Azure (CLI do Azure)]</span><span class="sxs-lookup"><span data-stu-id="65182-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[como toouse Olá Docker extensão da VM do Olá Interface de linha de comandos do Azure (CLI do Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agente Linux do Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[Docker em execução com https]:http://docs.docker.com/articles/https/
[Guia do utilizador Docker]:https://docs.docker.com/userguide/
