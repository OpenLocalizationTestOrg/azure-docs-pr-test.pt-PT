---
title: "aaaCreate autónoma do cluster com as VMs do Azure com o Windows | Microsoft Docs"
description: "Saiba como toocreate e gerir um cluster do Service Fabric do Azure em máquinas virtuais do Azure com o Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Criar um cluster do Service Fabric autónomo três nó máquinas virtuais do Azure com o Windows Server
Este artigo descreve como toocreate um cluster baseado no Windows Azure máquinas virtuais (VMs), utilizando Olá instalador autónomo do Service Fabric para Windows Server. cenário de Olá é num caso especial de [criar e gerir um cluster em execução no Windows Server](service-fabric-cluster-creation-for-windows-server.md) onde são Olá VMs [VMs do Azure com o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json); no entanto, não estiver a criar [do Azure cluster do Service Fabric baseado na nuvem](service-fabric-cluster-creation-via-portal.md). distinção Olá nos seguintes este padrão é esse cluster do Service Fabric Olá autónomo criado pelo Olá os seguintes passos completamente gerido por si, enquanto Olá clusters do Azure Service Fabric baseado na nuvem são geridos e atualizado pela Olá Service Fabric fornecedor de recursos.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Cluster do passos toocreate Olá autónomo
1. Inicie sessão toohello portal do Azure e criar um novo Datacenter do Windows Server 2012 R2 ou VM do Windows Server 2016 Centro de dados num grupo de recursos. Artigo de Olá leitura [criar uma VM do Windows no portal do Azure de Olá](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais detalhes.
2. Adicionar alguns toohello VMs mais mesmo grupo de recursos. Certifique-se de que cada um dos Olá VMs tem Olá mesmo nome de utilizador de administrador e palavra-passe quando o criou. Depois de criada, deve ver todas as três VMs no Olá mesma rede virtual.
3. Ligar tooeach de Olá VMs balanceado, desligando Olá Firewall do Windows utilizando Olá [Gestor de servidores, o dashboard do servidor Local](https://technet.microsoft.com/library/jj134147.aspx). Isto garante que o tráfego de rede Olá pode comunicar entre máquinas Olá. Enquanto máquina tooeach ligado, obter o endereço IP de Olá, abrir uma linha de comandos e digitar `ipconfig`. Em alternativa, pode ver Olá IP endereço de cada máquina no portal de Olá, selecionando o recurso de rede virtual Olá Olá grupo de recursos e a verificação de interfaces de rede de Olá criadas para cada uma destas máquinas.
4. Ligue tooone de Olá VMs e teste que pode enviar ping Olá as outras duas VMs com êxito.
5. Ligar tooone de Olá VMs e [transferir pacotes de Service Fabric Olá autónomo para o Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) para uma nova pasta no Olá máquina e extrair Olá pacote.
6. Abra Olá *ClusterConfig.Unsecure.MultiMachine.json* ficheiro no bloco de notas e editar cada nó com Olá três endereços IP Olá. Alterar o nome do cluster Olá na parte superior do Olá e guarde o ficheiro de Olá.  Um exemplo parcial Olá do manifesto do cluster é mostrado abaixo.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Se tenciona este toobe um cluster seguro, decidir a medida de segurança de Olá teria como toouse e siga os passos de Olá em Olá associado à ligação: [certificados X509](service-fabric-windows-cluster-x509-security.md) ou [segurança do Windows](service-fabric-windows-cluster-windows-security.md). Se configurar o cluster de Olá através de segurança do Windows, terá de tooset segurança um toomanage de controlador de domínio do Active Directory. Tenha em atenção que utilizar um computador de controlador de domínio como um recurso de infraestrutura do serviço de nó não é suportado.
8. Abra um [janela ISE do PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Navegue toohello pasta onde extraiu o pacote de instalador do Olá autónomo transferido e guardado Olá ficheiro de configuração de cluster. Execute Olá seguir o cluster de Olá de toodeploy de comando do PowerShell:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

script de Olá remotamente irá configurar o cluster do Service Fabric Olá e deve comunica o progresso como faz o através da implementação.

9. Após sobre um minuto, pode verificar se o cluster de Olá está operacional ligando toohello Service Fabric Explorer através de um IP da máquina de Olá endereços, por exemplo, utilizando `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Passos seguintes
* [Create standalone Service Fabric clusters on Windows Server or Linux (Criar clusters autónomos do Service Fabric no Windows Server ou no Linux)](service-fabric-deploy-anywhere.md)
* [Adicionar ou remover cluster do Service Fabric nós tooa autónomo](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Definições de configuração do cluster do Windows autónomo](service-fabric-cluster-manifest.md)
* [Proteger um cluster autónomo no Windows com segurança do Windows](service-fabric-windows-cluster-windows-security.md)
* [Proteger um cluster autónomo no Windows utilizando X509 certificados](service-fabric-windows-cluster-x509-security.md)

