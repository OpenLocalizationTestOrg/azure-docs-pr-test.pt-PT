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
# <a name="how-toouse-service-management-from-python"></a>Como toouse gestão de serviço do Python
Este guia mostra como tooprogrammatically efetuar tarefas de gestão comuns do serviço do Python. Olá **ServiceManagementService** a classe de Olá [Azure SDK para Python](https://github.com/Azure/azure-sdk-for-python) suporta acesso programático toomuch Olá serviço relacionadas com a gestão da funcionalidade do que está disponível no Olá [Portal clássico do azure] [ management-portal] (tais como **criar, atualizar e eliminar serviços em nuvem, implementações, os serviços de gestão de dados e as máquinas virtuais**). Esta funcionalidade pode ser útil na criação de aplicações que necessitam de gestão do acesso programático tooservice.

## <a name="WhatIs"></a>Que é o serviço de gestão
Olá API da gestão de serviço fornece acesso programático toomuch da funcionalidade de gestão de serviço Olá disponível através de Olá [portal clássico do Azure][management-portal]. Olá, Azure SDK para Python permite-lhe toomanage os seus serviços em nuvem e contas de armazenamento.

API de gestão de serviços de Olá toouse, terá de demasiado[criar uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"></a>Conceitos
Olá, Azure SDK para Python encapsula num wrapper Olá [API de gestão de serviços do Azure][svc-mgmt-rest-api], que é uma API REST. Todas as operações API são executadas sobre SSL e mutuamente autenticadas utilizando certificados X.509 v3. serviço de gestão de Olá poderão ser acedido a partir do dentro de um serviço em execução no Azure ou diretamente através de Olá Internet a partir de qualquer aplicação que pode enviar um pedido HTTPS e receber uma resposta HTTPS.

## <a name="Installation"></a>Instalação
Todas as funcionalidades de Olá descritas neste artigo estão disponíveis no Olá `azure-servicemanagement-legacy` pacote, o que pode instalar através do pip. Para obter mais informações sobre a instalação (por exemplo, se for novo tooPython), consulte este artigo: [instalar o Python e Olá SDK do Azure](../python-how-to-install.md)

## <a name="Connect"></a>Como: ligar tooservice gestão
ponto final de serviço de gestão do tooconnect toohello, terá do ID de subscrição do Azure e um certificado de gestão válido. Pode obter o ID de subscrição através de Olá [portal clássico do Azure][management-portal].

> [!NOTE]
> É, agora, os certificados de possíveis toouse criados com OpenSSL quando em execução no Windows.  Requer o Python 2.7.4 ou posterior. Recomendamos que os utilizadores toouse OpenSSL em vez de. pfx, desde o suporte para certificados, provavelmente, serão removidos no futuro Olá. pfx.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Certificados de gestão no Mac/Windows/Linux (OpenSSL)
Pode utilizar [OpenSSL](http://www.openssl.org/) toocreate o certificado de gestão.  Precisa, efetivamente, toocreate dois certificados, uma para o servidor de Olá (um `.cer` ficheiro) e outra para o cliente de Olá (um `.pem` ficheiro). Olá toocreate `.pem` de ficheiros, execute:

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Olá toocreate `.cer` de certificado, execute:

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Para obter mais informações sobre os certificados do Azure, consulte [descrição geral de certificados para serviços de nuvem do Azure](cloud-services-certs-create.md). Para obter uma descrição completa dos parâmetros de OpenSSL, consulte a documentação de Olá em [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

Depois de criar estes ficheiros, terá de Olá tooupload `.cer` ficheiro tooAzure através de ação de "Carregar" Olá do separador de "Definições" Olá de Olá [portal clássico do Azure][management-portal], e terá de nota toomake do onde guardou Olá `.pem` ficheiro.

Após obter o ID de subscrição, criou um certificado e carregado Olá `.cer` tooAzure de ficheiro, pode ligar o ponto final de gestão do Azure toohello transferindo o id de subscrição de Olá e Olá caminho toohello `.pem` ficheiro demasiado**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

No Olá anterior exemplo, `sms` é um **ServiceManagementService** objeto. Olá **ServiceManagementService** classe é Olá classe principal utilizada toomanage serviços do Azure.

### <a name="management-certificates-on-windows-makecert"></a>Certificados de gestão no Windows (MakeCert)
Pode criar um certificado de gestão autoassinado na sua máquina utilizando `makecert.exe`.  Abra um **linha de comandos do Visual Studio** como um **administrador** e utilizar Olá comando a seguir, substituindo *AzureCertificate* com o nome do certificado Olá gostaria de toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

comando de Olá cria Olá `.cer` de ficheiros e instala-o no Olá **pessoais** arquivo de certificados. Para obter mais informações, consulte [descrição geral de certificados para serviços de nuvem do Azure](cloud-services-certs-create.md).

Depois de ter criado o certificado de Olá, terá de Olá tooupload `.cer` ficheiro tooAzure através de ação de "Carregar" Olá do separador de "Definições" Olá de Olá [portal clássico do Azure][management-portal].

Após obter o ID de subscrição, criou um certificado e carregado Olá `.cer` tooAzure de ficheiro, pode ligar o ponto final de gestão do Azure toohello pela transmissão do id de subscrição de Olá e a localização de Olá do certificado de Olá no seu **Pessoais** arquivo de certificados demasiado**ServiceManagementService** (novamente, substitua *AzureCertificate* com o nome de Olá do seu certificado):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

No Olá anterior exemplo, `sms` é um **ServiceManagementService** objeto. Olá **ServiceManagementService** classe é Olá classe principal utilizada toomanage serviços do Azure.

## <a name="ListAvailableLocations"></a>Como: lista de localizações disponíveis
localizações de Olá toolist que estão disponíveis para o alojamento de serviços, utilize Olá **lista\_localizações** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

Quando criar um serviço em nuvem ou um serviço de armazenamento terá tooprovide uma localização válida. Olá **lista\_localizações** método sempre devolve uma lista atualizada das localizações de Olá atualmente disponíveis. A partir desta redação, as localizações de Olá disponíveis são:

* Europa Ocidental
* Europa do Norte
* Sudeste Asiático
* Ásia Oriental
* EUA Central
* EUA Centro-Norte
* E.U.A. Centro-Sul
* EUA Oeste
* EUA Leste
* Leste do Japão
* Oeste do Japão
* Sul do Brasil
* Leste da Austrália
* Sudeste da Austrália

## <a name="CreateCloudService"></a>Como: criar um serviço em nuvem
Quando cria uma aplicação e executá-lo no Azure, código de Olá e a configuração em conjunto são denominados um Azure [serviço em nuvem] [ cloud service] (conhecido como um *serviço alojado* em versões anteriores Versões do Azure). Olá **criar\_alojado\_serviço** método permite-lhe toocreate um novo serviço alojado, fornecendo um nome de serviço alojado (que tem de ser exclusivo no Azure), uma etiqueta (automaticamente codificado toobase64), um a descrição e uma localização.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

Pode listar todos os serviços de Olá alojado para a sua subscrição com Olá **lista\_alojado\_serviços** método:

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Se quiser tooget informações sobre um determinado serviço alojado, pode fazê-transferindo toohello de nome de serviço Olá alojado **obter\_alojado\_serviço\_propriedades** método:

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

Depois de criar um serviço em nuvem, pode implementar o serviço de toohello código com Olá **criar\_implementação** método.

## <a name="DeleteCloudService"></a>Como: eliminar um serviço em nuvem
Pode eliminar um serviço em nuvem através da transmissão toohello de nome de serviço Olá **eliminar\_alojado\_serviço** método:

    sms.delete_hosted_service('myhostedservice')

Antes de poder eliminar um serviço, todas as implementações do serviço de Olá tem de ser eliminadas primeiro. (Consulte [como: eliminar uma implementação](#DeleteDeployment) para obter mais informações.)

## <a name="DeleteDeployment"></a>Como: eliminar uma implementação
toodelete uma implementação, utilize Olá **eliminar\_implementação** método. Olá exemplo seguinte mostra como toodelete uma implementação com o nome `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"></a>Como: criar um serviço de armazenamento
A [serviço de armazenamento](../storage/common/storage-create-storage-account.md) dá-lhe acesso tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabelas](../cosmos-db/table-storage-how-to-use-python.md), e [filas](../storage/queues/storage-python-how-to-use-queue-storage.md). toocreate um serviço de armazenamento, precisa de um nome para o serviço de Olá (entre 3 e 24 carateres em minúsculas e exclusivo no Azure), uma descrição, uma etiqueta (cópia de segurança too100 carateres, automaticamente codificado toobase64) e uma localização. Olá seguinte exemplo mostra como toocreate um armazenamento service ao especificar uma localização.

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

Tenha em atenção na Olá anterior exemplo estado Olá dos Olá **criar\_armazenamento\_conta** operação pode ser obtida através da transmissão de resultado de Olá devolvido pelo **criar\_armazenamento \_conta** toohello **obter\_operação\_estado** método.  

Pode listar as contas de armazenamento e as respetivas propriedades com Olá **lista\_armazenamento\_contas** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"></a>Como: eliminar um serviço de armazenamento
Pode eliminar um serviço de armazenamento através da transmissão toohello de nome de serviço de armazenamento Olá **eliminar\_armazenamento\_conta** método. Eliminar um serviço de armazenamento elimina todos os dados armazenados no serviço de Olá (blobs, tabelas e filas).

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"></a>Como: lista de sistemas operativos disponíveis
toolist Olá os sistemas operativos que estão disponíveis para o alojamento de serviços, utilize Olá **lista\_operativo\_sistemas** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

Em alternativa, pode utilizar Olá **lista\_operativo\_sistema\_famílias** método, o que grupos de sistemas de operativos Olá por família:

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"></a>Como: criar uma imagem de sistema operativo
tooadd um repositório de imagens do sistema operativo imagem toohello, utilize Olá **adicionar\_SO\_imagem** método:

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

imagens de sistema operativo de Olá toolist que estão disponíveis, utilize Olá **lista\_SO\_imagens** método. Inclui todas as imagens de plataforma e imagens do utilizador:

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

## <a name="DeleteVMImage"></a>Como: eliminar uma imagem do sistema operativo
toodelete uma imagem do utilizador, utilize Olá **eliminar\_SO\_imagem** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"></a>Como: criar uma máquina virtual
toocreate uma máquina virtual, terá primeiro toocreate um [serviço em nuvem](#CreateCloudService).  Em seguida, criar a implementação da máquina virtual Olá utilizando Olá **criar\_virtual\_máquina\_implementação** método:

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

## <a name="DeleteVM"></a>Como: eliminar uma máquina virtual
toodelete uma máquina virtual, tem primeiro de eliminar implementação Olá utilizando Olá **eliminar\_implementação** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

o serviço em nuvem Olá, em seguida, pode ser eliminado utilizando Olá **eliminar\_alojado\_serviço** método:

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Como: Criar uma Máquina Virtual a partir de uma imagem capturada Máquina Virtual
toocapture uma imagem de VM, tem primeiro de chamar Olá **capturar\_vm\_imagem** método:

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

Em seguida, toomake certificar de que tem capturada com êxito a imagem de Olá, utilize Olá **lista\_vm\_imagens** api e certifique-se a imagem é apresentada nos resultados de Olá:

    images = sms.list_vm_images()

toofinally criar máquina virtual de Olá utilizando a imagem capturada Olá, utilize Olá **criar\_virtual\_máquina\_implementação** método como anteriormente, mas, desta vez passar Olá vm_image_name em vez disso,

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

mais informações sobre como toolearn como toocapture uma Máquina Virtual do Linux, consulte [como tooCapture uma Máquina Virtual Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

mais informações sobre como toolearn como toocapture Máquina Virtual do Windows, consulte [como tooCapture Máquina Virtual do Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá da gestão de serviço, pode aceder ao hello [documentação de referência da API de completa para Olá SDK Python do Azure](http://azure-sdk-for-python.readthedocs.org/) e efetuar complexas tarefas facilmente toomanage a aplicação de python.

Para obter mais informações, consulte Olá [Centro para programadores do Python](/develop/python/).

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
