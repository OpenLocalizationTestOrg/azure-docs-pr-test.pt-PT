---
title: "aaaHow API (Python) - guia de funcionalidades de gestão de serviço Olá toouse"
description: "Saiba como tooprogrammatically efetuar tarefas de gestão comuns do serviço do Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="3ad9f-103">Como toouse gestão de serviço do Python</span><span class="sxs-lookup"><span data-stu-id="3ad9f-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="3ad9f-104">Este guia mostra como tooprogrammatically efetuar tarefas de gestão comuns do serviço do Python.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="3ad9f-105">Olá **ServiceManagementService** a classe de Olá [Azure SDK para Python](https://github.com/Azure/azure-sdk-for-python) suporta acesso programático toomuch Olá serviço relacionadas com a gestão da funcionalidade do que está disponível no Olá [Portal clássico do azure] [ management-portal] (tais como **criar, atualizar e eliminar serviços em nuvem, implementações, os serviços de gestão de dados e as máquinas virtuais**).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="3ad9f-106">Esta funcionalidade pode ser útil na criação de aplicações que necessitam de gestão do acesso programático tooservice.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="3ad9f-107"><a name="WhatIs"></a>Que é o serviço de gestão</span><span class="sxs-lookup"><span data-stu-id="3ad9f-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="3ad9f-108">Olá API da gestão de serviço fornece acesso programático toomuch da funcionalidade de gestão de serviço Olá disponível através de Olá [portal clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="3ad9f-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="3ad9f-109">Olá, Azure SDK para Python permite-lhe toomanage os seus serviços em nuvem e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="3ad9f-110">API de gestão de serviços de Olá toouse, terá de demasiado[criar uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="3ad9f-111"><a name="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="3ad9f-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="3ad9f-112">Olá, Azure SDK para Python encapsula num wrapper Olá [API de gestão de serviços do Azure][svc-mgmt-rest-api], que é uma API REST.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="3ad9f-113">Todas as operações API são executadas sobre SSL e mutuamente autenticadas utilizando certificados X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="3ad9f-114">serviço de gestão de Olá poderão ser acedido a partir do dentro de um serviço em execução no Azure ou diretamente através de Olá Internet a partir de qualquer aplicação que pode enviar um pedido HTTPS e receber uma resposta HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="3ad9f-115"><a name="Installation"></a>Instalação</span><span class="sxs-lookup"><span data-stu-id="3ad9f-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="3ad9f-116">Todas as funcionalidades de Olá descritas neste artigo estão disponíveis no Olá `azure-servicemanagement-legacy` pacote, o que pode instalar através do pip.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="3ad9f-117">Para obter mais informações sobre a instalação (por exemplo, se for novo tooPython), consulte este artigo: [instalar o Python e Olá SDK do Azure](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="3ad9f-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="3ad9f-118"><a name="Connect"></a>Como: ligar tooservice gestão</span><span class="sxs-lookup"><span data-stu-id="3ad9f-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="3ad9f-119">ponto final de serviço de gestão do tooconnect toohello, terá do ID de subscrição do Azure e um certificado de gestão válido.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="3ad9f-120">Pode obter o ID de subscrição através de Olá [portal clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="3ad9f-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="3ad9f-121">É, agora, os certificados de possíveis toouse criados com OpenSSL quando em execução no Windows.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="3ad9f-122">Requer o Python 2.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="3ad9f-123">Recomendamos que os utilizadores toouse OpenSSL em vez de. pfx, desde o suporte para certificados, provavelmente, serão removidos no futuro Olá. pfx.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="3ad9f-124">Certificados de gestão no Mac/Windows/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="3ad9f-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="3ad9f-125">Pode utilizar [OpenSSL](http://www.openssl.org/) toocreate o certificado de gestão.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="3ad9f-126">Precisa, efetivamente, toocreate dois certificados, uma para o servidor de Olá (um `.cer` ficheiro) e outra para o cliente de Olá (um `.pem` ficheiro).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="3ad9f-127">Olá toocreate `.pem` de ficheiros, execute:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="3ad9f-128">Olá toocreate `.cer` de certificado, execute:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="3ad9f-129">Para obter mais informações sobre os certificados do Azure, consulte [descrição geral de certificados para serviços de nuvem do Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="3ad9f-130">Para obter uma descrição completa dos parâmetros de OpenSSL, consulte a documentação de Olá em [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="3ad9f-131">Depois de criar estes ficheiros, terá de Olá tooupload `.cer` ficheiro tooAzure através de ação de "Carregar" Olá do separador de "Definições" Olá de Olá [portal clássico do Azure][management-portal], e terá de nota toomake do onde guardou Olá `.pem` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="3ad9f-132">Após obter o ID de subscrição, criou um certificado e carregado Olá `.cer` tooAzure de ficheiro, pode ligar o ponto final de gestão do Azure toohello transferindo o id de subscrição de Olá e Olá caminho toohello `.pem` ficheiro demasiado**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="3ad9f-133">No Olá anterior exemplo, `sms` é um **ServiceManagementService** objeto.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="3ad9f-134">Olá **ServiceManagementService** classe é Olá classe principal utilizada toomanage serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="3ad9f-135">Certificados de gestão no Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="3ad9f-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="3ad9f-136">Pode criar um certificado de gestão autoassinado na sua máquina utilizando `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="3ad9f-137">Abra um **linha de comandos do Visual Studio** como um **administrador** e utilizar Olá comando a seguir, substituindo *AzureCertificate* com o nome do certificado Olá gostaria de toouse.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="3ad9f-138">comando de Olá cria Olá `.cer` de ficheiros e instala-o no Olá **pessoais** arquivo de certificados.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="3ad9f-139">Para obter mais informações, consulte [descrição geral de certificados para serviços de nuvem do Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="3ad9f-140">Depois de ter criado o certificado de Olá, terá de Olá tooupload `.cer` ficheiro tooAzure através de ação de "Carregar" Olá do separador de "Definições" Olá de Olá [portal clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="3ad9f-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="3ad9f-141">Após obter o ID de subscrição, criou um certificado e carregado Olá `.cer` tooAzure de ficheiro, pode ligar o ponto final de gestão do Azure toohello pela transmissão do id de subscrição de Olá e a localização de Olá do certificado de Olá no seu **Pessoais** arquivo de certificados demasiado**ServiceManagementService** (novamente, substitua *AzureCertificate* com o nome de Olá do seu certificado):</span><span class="sxs-lookup"><span data-stu-id="3ad9f-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="3ad9f-142">No Olá anterior exemplo, `sms` é um **ServiceManagementService** objeto.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="3ad9f-143">Olá **ServiceManagementService** classe é Olá classe principal utilizada toomanage serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="3ad9f-144"><a name="ListAvailableLocations"></a>Como: lista de localizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="3ad9f-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="3ad9f-145">localizações de Olá toolist que estão disponíveis para o alojamento de serviços, utilize Olá **lista\_localizações** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="3ad9f-146">Quando criar um serviço em nuvem ou um serviço de armazenamento terá tooprovide uma localização válida.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="3ad9f-147">Olá **lista\_localizações** método sempre devolve uma lista atualizada das localizações de Olá atualmente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="3ad9f-148">A partir desta redação, as localizações de Olá disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="3ad9f-149">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="3ad9f-149">West Europe</span></span>
* <span data-ttu-id="3ad9f-150">Europa do Norte</span><span class="sxs-lookup"><span data-stu-id="3ad9f-150">North Europe</span></span>
* <span data-ttu-id="3ad9f-151">Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="3ad9f-151">Southeast Asia</span></span>
* <span data-ttu-id="3ad9f-152">Ásia Oriental</span><span class="sxs-lookup"><span data-stu-id="3ad9f-152">East Asia</span></span>
* <span data-ttu-id="3ad9f-153">EUA Central</span><span class="sxs-lookup"><span data-stu-id="3ad9f-153">Central US</span></span>
* <span data-ttu-id="3ad9f-154">EUA Centro-Norte</span><span class="sxs-lookup"><span data-stu-id="3ad9f-154">North Central US</span></span>
* <span data-ttu-id="3ad9f-155">E.U.A. Centro-Sul</span><span class="sxs-lookup"><span data-stu-id="3ad9f-155">South Central US</span></span>
* <span data-ttu-id="3ad9f-156">EUA Oeste</span><span class="sxs-lookup"><span data-stu-id="3ad9f-156">West US</span></span>
* <span data-ttu-id="3ad9f-157">EUA Leste</span><span class="sxs-lookup"><span data-stu-id="3ad9f-157">East US</span></span>
* <span data-ttu-id="3ad9f-158">Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="3ad9f-158">Japan East</span></span>
* <span data-ttu-id="3ad9f-159">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="3ad9f-159">Japan West</span></span>
* <span data-ttu-id="3ad9f-160">Sul do Brasil</span><span class="sxs-lookup"><span data-stu-id="3ad9f-160">Brazil South</span></span>
* <span data-ttu-id="3ad9f-161">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="3ad9f-161">Australia East</span></span>
* <span data-ttu-id="3ad9f-162">Sudeste da Austrália</span><span class="sxs-lookup"><span data-stu-id="3ad9f-162">Australia Southeast</span></span>

## <span data-ttu-id="3ad9f-163"><a name="CreateCloudService"></a>Como: criar um serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="3ad9f-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="3ad9f-164">Quando cria uma aplicação e executá-lo no Azure, código de Olá e a configuração em conjunto são denominados um Azure [serviço em nuvem] [ cloud service] (conhecido como um *serviço alojado* em versões anteriores Versões do Azure).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="3ad9f-165">Olá **criar\_alojado\_serviço** método permite-lhe toocreate um novo serviço alojado, fornecendo um nome de serviço alojado (que tem de ser exclusivo no Azure), uma etiqueta (automaticamente codificado toobase64), um a descrição e uma localização.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="3ad9f-166">Pode listar todos os serviços de Olá alojado para a sua subscrição com Olá **lista\_alojado\_serviços** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="3ad9f-167">Se quiser tooget informações sobre um determinado serviço alojado, pode fazê-transferindo toohello de nome de serviço Olá alojado **obter\_alojado\_serviço\_propriedades** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="3ad9f-168">Depois de criar um serviço em nuvem, pode implementar o serviço de toohello código com Olá **criar\_implementação** método.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="3ad9f-169"><a name="DeleteCloudService"></a>Como: eliminar um serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="3ad9f-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="3ad9f-170">Pode eliminar um serviço em nuvem através da transmissão toohello de nome de serviço Olá **eliminar\_alojado\_serviço** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="3ad9f-171">Antes de poder eliminar um serviço, todas as implementações do serviço de Olá tem de ser eliminadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="3ad9f-172">(Consulte [como: eliminar uma implementação](#DeleteDeployment) para obter mais informações.)</span><span class="sxs-lookup"><span data-stu-id="3ad9f-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="3ad9f-173"><a name="DeleteDeployment"></a>Como: eliminar uma implementação</span><span class="sxs-lookup"><span data-stu-id="3ad9f-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="3ad9f-174">toodelete uma implementação, utilize Olá **eliminar\_implementação** método.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="3ad9f-175">Olá exemplo seguinte mostra como toodelete uma implementação com o nome `v1`.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="3ad9f-176"><a name="CreateStorageService"></a>Como: criar um serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3ad9f-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="3ad9f-177">A [serviço de armazenamento](../storage/common/storage-create-storage-account.md) dá-lhe acesso tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabelas](../cosmos-db/table-storage-how-to-use-python.md), e [filas](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="3ad9f-178">toocreate um serviço de armazenamento, precisa de um nome para o serviço de Olá (entre 3 e 24 carateres em minúsculas e exclusivo no Azure), uma descrição, uma etiqueta (cópia de segurança too100 carateres, automaticamente codificado toobase64) e uma localização.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="3ad9f-179">Olá seguinte exemplo mostra como toocreate um armazenamento service ao especificar uma localização.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="3ad9f-180">Tenha em atenção na Olá anterior exemplo estado Olá dos Olá **criar\_armazenamento\_conta** operação pode ser obtida através da transmissão de resultado de Olá devolvido pelo **criar\_armazenamento \_conta** toohello **obter\_operação\_estado** método.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="3ad9f-181">Pode listar as contas de armazenamento e as respetivas propriedades com Olá **lista\_armazenamento\_contas** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="3ad9f-182"><a name="DeleteStorageService"></a>Como: eliminar um serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3ad9f-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="3ad9f-183">Pode eliminar um serviço de armazenamento através da transmissão toohello de nome de serviço de armazenamento Olá **eliminar\_armazenamento\_conta** método.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="3ad9f-184">Eliminar um serviço de armazenamento elimina todos os dados armazenados no serviço de Olá (blobs, tabelas e filas).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="3ad9f-185"><a name="ListOperatingSystems"></a>Como: lista de sistemas operativos disponíveis</span><span class="sxs-lookup"><span data-stu-id="3ad9f-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="3ad9f-186">toolist Olá os sistemas operativos que estão disponíveis para o alojamento de serviços, utilize Olá **lista\_operativo\_sistemas** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="3ad9f-187">Em alternativa, pode utilizar Olá **lista\_operativo\_sistema\_famílias** método, o que grupos de sistemas de operativos Olá por família:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="3ad9f-188"><a name="CreateVMImage"></a>Como: criar uma imagem de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="3ad9f-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="3ad9f-189">tooadd um repositório de imagens do sistema operativo imagem toohello, utilize Olá **adicionar\_SO\_imagem** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="3ad9f-190">imagens de sistema operativo de Olá toolist que estão disponíveis, utilize Olá **lista\_SO\_imagens** método.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="3ad9f-191">Inclui todas as imagens de plataforma e imagens do utilizador:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="3ad9f-192"><a name="DeleteVMImage"></a>Como: eliminar uma imagem do sistema operativo</span><span class="sxs-lookup"><span data-stu-id="3ad9f-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="3ad9f-193">toodelete uma imagem do utilizador, utilize Olá **eliminar\_SO\_imagem** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="3ad9f-194"><a name="CreateVM"></a>Como: criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3ad9f-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="3ad9f-195">toocreate uma máquina virtual, terá primeiro toocreate um [serviço em nuvem](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="3ad9f-196">Em seguida, criar a implementação da máquina virtual Olá utilizando Olá **criar\_virtual\_máquina\_implementação** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="3ad9f-197"><a name="DeleteVM"></a>Como: eliminar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3ad9f-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="3ad9f-198">toodelete uma máquina virtual, tem primeiro de eliminar implementação Olá utilizando Olá **eliminar\_implementação** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="3ad9f-199">o serviço em nuvem Olá, em seguida, pode ser eliminado utilizando Olá **eliminar\_alojado\_serviço** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="3ad9f-200">Como: Criar uma Máquina Virtual a partir de uma imagem capturada Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="3ad9f-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="3ad9f-201">toocapture uma imagem de VM, tem primeiro de chamar Olá **capturar\_vm\_imagem** método:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="3ad9f-202">Em seguida, toomake certificar de que tem capturada com êxito a imagem de Olá, utilize Olá **lista\_vm\_imagens** api e certifique-se a imagem é apresentada nos resultados de Olá:</span><span class="sxs-lookup"><span data-stu-id="3ad9f-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="3ad9f-203">toofinally criar máquina virtual de Olá utilizando a imagem capturada Olá, utilize Olá **criar\_virtual\_máquina\_implementação** método como anteriormente, mas, desta vez passar Olá vm_image_name em vez disso,</span><span class="sxs-lookup"><span data-stu-id="3ad9f-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="3ad9f-204">mais informações sobre como toolearn como toocapture uma Máquina Virtual do Linux, consulte [como tooCapture uma Máquina Virtual Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3ad9f-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="3ad9f-205">mais informações sobre como toolearn como toocapture Máquina Virtual do Windows, consulte [como tooCapture Máquina Virtual do Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3ad9f-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="3ad9f-206"><a name="What's Next"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3ad9f-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="3ad9f-207">Agora que aprendeu as noções básicas de Olá da gestão de serviço, pode aceder ao hello [documentação de referência da API de completa para Olá SDK Python do Azure](http://azure-sdk-for-python.readthedocs.org/) e efetuar complexas tarefas facilmente toomanage a aplicação de python.</span><span class="sxs-lookup"><span data-stu-id="3ad9f-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="3ad9f-208">Para obter mais informações, consulte Olá [Centro para programadores do Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="3ad9f-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
