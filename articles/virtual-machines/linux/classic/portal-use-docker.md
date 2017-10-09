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
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Utilizar Olá Docker extensão da VM com Olá portal clássico do Azure
> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

[Docker](https://www.docker.com/) é uma das Olá mais populares abordagens de Virtualização que utiliza [Linux contentores](http://en.wikipedia.org/wiki/LXC) em vez de máquinas virtuais como uma forma de isolando os dados e computação em recursos partilhados. Pode utilizar a extensão de VM de Docker Olá gerido pelo [agente Linux do Azure] toocreate uma VM de Docker que aloja qualquer número de contentores para as suas aplicações no Azure.

> [!NOTE]
> Este tópico descreve como toocreate uma VM a partir do Docker Olá portal clássico do Azure. toosee como toocreate uma VM de Docker na linha de comandos Olá, consulte [como toouse Olá Docker extensão da VM do Olá Interface de linha de comandos do Azure (CLI do Azure)]. toosee um debate de alto nível de contentores e as vantagens, consulte Olá [Whiteboard de nível elevado de Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Criar uma nova VM a partir de Olá Galeria de imagem
primeiro passo de Olá necessita de uma VM do Azure a partir de uma imagem de Linux que suporte Olá extensão da VM Docker, utilizando uma imagem de Ubuntu 14.04 LTS de Olá imagem galeria como uma imagem de servidor de exemplo e ambiente de trabalho do Ubuntu 14.04 como um cliente. No portal de Olá, clique em **+ novo** no Olá na parte inferior esquerda canto toocreate uma nova instância VM e selecione uma imagem de Ubuntu 14.04 LTS seleções Olá disponíveis ou a Olá concluir Galeria de imagem, conforme mostrado abaixo.

> [!NOTE]
> Atualmente, apenas Ubuntu 14.04 LTS imagens mais recentes de Julho de 2014 suportam Olá Docker extensão da VM.
> 
> 

![Criar uma nova imagem de Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Criar certificados de Docker
Depois de Olá que VM foi criada, certifique-se de que o Docker está instalado no computador cliente. (Para obter mais informações, consulte [instruções de instalação do Docker](https://docs.docker.com/installation/#installation).)

Criar ficheiros de certificado e chave para a comunicação de Docker demasiado de acordo com a Olá[Docker em execução com https] e colocá-los no Olá  **`~/.docker`**  diretório no computador cliente.

> [!NOTE]
> Olá Docker extensão da VM no portal de Olá atualmente exige credenciais que são codificados em base64.
> 
> 

Na linha de comandos Olá, utilize  **`base64`**  ou outro favorito codificação tópicos da ferramenta toocreate com codificação base64. Fazê-lo com um conjunto simples de ficheiros de certificado e a chave poderá ter um aspeto semelhante toothis:

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

## <a name="add-hello-docker-vm-extension"></a>Adicionar Olá Docker extensão da VM
tooadd Olá Docker extensão da VM, localize a instância de VM de Olá que criou e desloque para baixo demasiado**extensões** e clique no mesmo toobring configurar extensões de VM, conforme mostrado abaixo.

> [!NOTE]
> Esta funcionalidade é suportada apenas o portal de pré-visualização Olá: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Adicionar uma extensão
Clique em Olá **+ adicionar** toodisplay Olá extensões possíveis das VMS, pode adicionar toothis VM.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Selecione Olá Docker extensão da VM
Escolha Olá extensão de VM de Docker, aparece a descrição de Docker Olá e ligações importantes, e, em seguida, clique em **criar** no procedimento de instalação do Olá inferior toobegin Olá.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Adicione o certificado e ficheiros de chave:
Nos campos de formulário Olá, introduza Olá com codificação base64 as versões do seu certificado da AC, o certificado de servidor e a chave de servidor, conforme mostrado no Olá gráfico a seguir.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Tenha em atenção que (tal como no Olá anterior a imagem) Olá 2376 é preenchido por predefinição. Pode introduzir qualquer ponto final aqui, mas o passo seguinte Olá serão tooopen segurança Olá correspondente ao ponto final. Se alterar a predefinição de Olá, certifique-se de que tooopen segurança Olá correspondente ao ponto final no passo seguinte Olá.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Adicionar Olá ponto final de comunicação do Docker
Ao visualizar o grupo de recursos de Olá que criou, selecione o grupo de segurança de rede associado à VM de Olá e clique em **regras de segurança de entrada** tooview Olá regras conforme mostrado aqui.

![](media/portal-use-docker/AddingEndpoint.png)

Clique em **+ adicionar** tooadd outra regra e no caso de predefinição Olá, introduza um nome para o ponto final de Olá (neste exemplo, **Docker**) e 2376 'destino intervalo de portas'. Definir a apresentação de valor de protocolo de Olá **TCP**e clique em **OK** regra de Olá toocreate.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Testar o cliente de Docker e anfitriões de Docker do Azure
Localize e copie o nome de Olá do domínio da VM e, na linha de comandos Olá do computador cliente, tipo `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (onde *dockerextension* é substituído pela Olá subdomínio para a VM).

resultado de Olá deve aparecer toothis semelhante:

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

Depois de concluir Olá os passos acima, tem agora um anfitrião de Docker totalmente funcional com uma VM do Azure, toobe ligado tooremotely a partir de outros clientes.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passos seguintes
Está pronto toogo toohello [Guia do utilizador Docker] e utilizar a VM de Docker. Se quiser tooautomate criar anfitriões de Docker em VMs do Azure através da interface de linha de comandos, consulte [como toouse Olá Docker extensão da VM do Olá Interface de linha de comandos do Azure (CLI do Azure)]

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
