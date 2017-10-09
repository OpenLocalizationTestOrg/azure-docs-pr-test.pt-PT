---
title: "aaaCreate um nó principal do HPC Pack numa VM do Azure | Microsoft Docs"
description: "Saiba como toouse Olá implementação de Gestor de recursos do Azure portal e Olá modelo toocreate um nó principal do Microsoft HPC Pack 2012 R2 numa VM do Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Criar o nó principal do Olá de um cluster HPC Pack numa VM do Azure com uma imagem do Marketplace
Utilize um [imagem de máquina virtual do Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) de Olá Azure Marketplace e Olá toocreate portal do Azure Olá nó principal de um cluster HPC. Esta imagem de VM de pacote HPC é baseada no Windows Server 2012 R2 Datacenter com o HPC Pack 2012 R2 Update 3 pré-instaladas. Utilize este nó principal para uma prova de implementação de conceito de pacote HPC no Azure. Em seguida, pode adicionar computação nós toohello cluster toorun cargas de trabalho HPC.

> [!TIP]
> toodeploy um cluster HPC Pack 2012 R2 completado no Azure que inclui o nó principal Olá e nós de computação, recomendamos que utilize um método automatizado. As opções incluem Olá [script de implementação de HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e modelos do Resource Manager, tais como Olá [cluster HPC Pack para cargas de trabalho do Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). Modelos do Resource Manager também estão disponíveis para [clusters do Microsoft HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Considerações de planeamento
Conforme mostrado na figura a seguir de Olá, implementar nó principal de HPC Pack Olá num domínio do Active Directory numa rede virtual do Azure.

![Nó principal do HPC Pack][headnode]

* **Domínio do Active Directory**: Olá HPC Pack 2012 R2 nó principal tem de ser associado a um domínio do Active Directory tooan no Azure antes de iniciar os serviços HPC Olá no Olá VM. Conforme mostrado neste artigo, para uma prova de implementação de conceito, pode promover Olá VM que criar para o nó principal Olá como um controlador de domínio antes de iniciar os serviços HPC Olá. Outra opção consiste toodeploy um controlador de domínio separado e floresta no Azure toowhich associar Olá VM de nó principal.

* **Modelo de implementação**: para a maioria das implementações novas, a Microsoft recomenda que utilize o modelo de implementação do Resource Manager Olá. Este artigo pressupõe que utiliza este modelo de implementação.

* **Rede virtual do Azure**: ao utilizar Olá Resource Manager implementação modelo toodeploy Olá nó principal, que especificar ou criar uma rede virtual do Azure. Utilizar a rede virtual Olá se precisar de toojoin Olá nó principal tooan existente domínio do Active Directory. Também precisa de-nó de computação do posterior tooadd VMs toohello cluster.

## <a name="steps-toocreate-hello-head-node"></a>Nó principal do passos toocreate Olá
Seguem-se passos de alto nível toouse Olá toocreate do portal do Azure, uma VM do Azure para o nó principal do HPC Pack Olá utilizando o modelo de implementação do Resource Manager Olá. 

1. Se quiser toocreate uma nova floresta do Active Directory no Azure com VMs do controlador de domínio separado, uma das alternativas consiste toouse um [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Para uma prova simple de implementação de conceito, tem de ajustar tooomit este passo e configurar o nó principal do Olá VM si próprio como controlador de domínio. Esta opção é descrita mais à frente neste artigo.
2. No Olá [HPC Pack 2012 R2, Windows Server 2012 R2 página](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) no Azure Marketplace Olá, clique em **criar Máquina Virtual**. 
3. No portal de Olá, no Olá **HPC Pack 2012 R2 no Windows Server 2012 R2** página, selecione de Olá **Resource Manager** modelo de implementação e, em seguida, clique em **criar**.
   
    ![Imagem de HPC Pack][marketplace]
4. Utilizar Olá portal tooconfigure Olá definições e crie Olá VM. Se tiver tooAzure novo, siga o tutorial Olá [criar máquina virtual do Windows no portal do Azure de Olá](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para uma prova de implementação de conceito, normalmente, pode aceitar a predefinição de Olá ou definições recomendadas.
   
   > [!NOTE]
   > Se quiser toojoin Olá nó principal tooan existente de domínio do Active Directory no Azure, certifique-se de que especificar rede virtual do Olá desse domínio, ao criar Olá VM.
   > 
   > 
5. Depois de criar Olá VM e hello VM está em execução, [ligar toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pelo ambiente de trabalho remoto. 
6. Associação a floresta de domínio do Active Directory do Olá VM tooan escolhendo uma das seguintes opções de Olá:
   
   * Se tiver criado Olá VM numa rede virtual do Azure com uma floresta de domínio existente, associe a floresta de toohello Olá VM utilizando ferramentas padrão do Gestor de servidor ou o Windows PowerShell. Em seguida, reinicie.
   * Se tiver criado Olá VM numa rede virtual novo (sem uma floresta de domínio existente), em seguida, promova Olá VM como um controlador de domínio. Utilize tooinstall passos padrão e configurar a função de serviços de domínio do Active Directory Olá no nó principal Olá. Para obter passos detalhados, consulte [instalar uma nova floresta Windows Server 2012 Active Directory](https://technet.microsoft.com/library/jj574166.aspx).
7. Após Olá VM está em execução e está associado a um tooan floresta do Active Directory, inicie os serviços HPC Pack Olá da seguinte forma:
   
    a. Ligar o nó principal do toohello VM utilizando uma conta de domínio que seja membro do grupo de administradores local Olá. Por exemplo, utilize a conta de administrador de Olá que configurou quando criou o nó principal do Olá VM.
   
    b. Para uma configuração predefinida do nó principal, inicie o Windows PowerShell como administrador e escreva Olá seguinte:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Pode demorar alguns minutos para Olá HPC Pack serviços toostart.
   
    Nó principal adicionais para opções de configuração, escreva `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Passos seguintes
* Agora, pode trabalhar com o nó principal do Olá do cluster HPC Pack. Por exemplo, inicie o Gestor de clusters HPC e Olá concluída [lista de tarefas de implementação](https://technet.microsoft.com/library/jj884141.aspx).
* Se pretender tooincrease Olá cluster computação capacidade a pedido, adicione [Azure burst nós](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) num serviço em nuvem. 
* Tente executar uma carga de trabalho de teste no cluster de Olá. Por exemplo, consulte Olá HPC Pack [guia de introdução](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
