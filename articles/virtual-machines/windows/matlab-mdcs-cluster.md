---
title: "aaaMATLAB clusters em máquinas virtuais | Microsoft Docs"
description: "Utilizar toocreate de máquinas virtuais do Microsoft Azure MATLAB distribuídas Server informática clusters toorun intensivas de computação paralelas MATLAB cargas de trabalho"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Criar clusters de servidor de informática distribuída da MATLAB em VMs do Azure
Utilize Microsoft Azure virtual máquinas toocreate um ou mais MATLAB distribuídas informática clusters de servidores toorun intensivas de computação paralelas MATLAB cargas de trabalho. Instalar o software de servidor de informática distribuída da MATLAB no toouse VM, como uma imagem de base e utilizar um modelo de início rápido do Azure ou do script do PowerShell do Azure (disponível no [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy e gerir Olá cluster. Após a implementação, ligar toohello cluster toorun as cargas de trabalho.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>Sobre MATLAB e Server informática de MATLAB distribuído
Olá [MATLAB](http://www.mathworks.com/products/matlab/) plataforma está otimizada para resolver problemas de engenharia e científicos. MATLAB os utilizadores com simulações de larga escala e tarefas de processamento de dados podem utilizar paralelo MathWorks produtos toospeed segurança as respetivas cargas de trabalho de computação intensivas de computação, tirando partido dos clusters de computação e os serviços de grelha. [Paralela caixa de ferramentas de informática](http://www.mathworks.com/products/parallel-computing/) permite que os utilizadores MATLAB parallelize aplicações e tirar partido de processadores de vários núcleos, GPUs e clusters de computação. [Servidor de informática distribuída da MATLAB](http://www.mathworks.com/products/distriben/) permite MATLAB utilizadores tooutilize vários computadores num cluster de computação.

Através da utilização de máquinas virtuais do Azure, pode criar clusters MATLAB distribuídas Server informática que tenham todas Olá mesmo mecanismos toosubmit disponíveis paralelas trabalho como clusters no local, tais como tarefas interativas, tarefas do batch, tarefas independentes, e comunicar tarefas. Utilizar o Azure em conjunto com a plataforma de MATLAB Olá tem muitas vantagens em comparação com tooprovisioning e utilizar tradicional hardware no local: tamanhos de um intervalo de máquina virtual, a criação de clusters a pedido pelo que só paga pelos recursos de computação de Olá utilizar, e modelos de tootest de capacidade de Olá à escala.  

## <a name="prerequisites"></a>Pré-requisitos
* **Computador cliente** -terá um toocommunicate de computador cliente com Windows com o Azure e Olá cluster MATLAB distribuídas Server informática após a implementação.
* **O Azure PowerShell** -consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall-lo no seu computador cliente.
* **Subscrição do Azure** -se não tiver uma subscrição, pode criar um [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos. Para clusters maiores, considere uma subscrição pay as you go ou outras opções de compra.
* **Quota de núcleos** -poderá ser necessário toodeploy de quota de núcleos de Olá tooincrease um cluster de grandes dimensões ou mais de um cluster de servidor de informática distribuída da MATLAB. tooincrease uma quota [abrir um pedido de suporte ao cliente online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) , sem encargos.
* **Licenças MATLAB, caixa de ferramentas de computação paralelas e MATLAB distribuídas Server informática** -scripts Olá partem do princípio que Olá [MathWorks alojado do License Manager](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) é utilizada para todas as licenças.  
* **Software MATLAB distribuídas Server informática** -será instalado numa VM que será utilizada como imagem de VM base Olá para cluster Olá VMs.

## <a name="high-level-steps"></a>Passos de nível elevados
toouse virtual do Azure máquinas para os clusters de servidor de informática distribuída da MATLAB, hello são necessários passos de alto nível seguintes. Instruções detalhadas são na documentação de Olá que acompanha o modelo de início rápido Olá e scripts no [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Criar uma imagem VM base**  

   * Transfira e instale o software de servidor de informática distribuída da MATLAB para esta VM.

     > [!NOTE]
     > Este processo poderá demorar algumas horas, mas tem apenas toodo-lo, uma vez para cada versão do MATLAB utilizar.   
     >
     >
2. **Criar um ou mais clusters**  

   * Utilize o script do PowerShell Olá fornecido ou Olá início rápido modelo toocreate um cluster de imagem de VM base Olá.   
   * Gerir clusters de Olá utilizando o script do PowerShell Olá fornecido que lhe permite toolist, pausar, retomar e clusters de eliminação.

## <a name="cluster-configurations"></a>Configurações de cluster
Atualmente, script de criação do cluster Olá e modelo permitem-lhe toocreate uma única topologia MATLAB distribuídas Server informática. Se pretender, crie um ou mais clusters adicionais, com cada cluster ter um número diferente de trabalho VMs, utilizando tamanhos de VM diferentes e assim sucessivamente.

### <a name="matlab-client-and-cluster-in-azure"></a>Cliente MATLAB e cluster no Azure
nó de MATLAB Hello do cliente, o nó de Programador de tarefas MATLAB e MATLAB distribuídas informática servidor "trabalho" nós são todos configurados como VMs do Azure numa rede virtual, conforme mostrado na seguinte Olá figura.


* Olá toouse do cluster, se ligar ao nó de cliente do ambiente de trabalho remoto toohello. nó de Hello do cliente executa o cliente MATLAB Olá.
* nó de cliente Olá tem uma partilha de ficheiros que pode ser acedida por todos os funcionários.
* Gestor de licenças alojado MathWorks é utilizada para Olá verificações de licença de todo o software MATLAB.
* Por predefinição, é criado um trabalho de servidor de informática distribuída da MATLAB por núcleos no trabalho Olá VMs, mas pode especificar qualquer número.

## <a name="use-an-azure-based-cluster"></a>Utilizar um Cluster baseado no Azure
Tal como acontece com outros tipos de clusters de servidor de informática distribuída da MATLAB, terá de toouse Olá Gestor de clusters de perfil na Olá MATLAB cliente (no cliente de Olá VM) toocreate um perfil de cluster MATLAB Programador de tarefas.

![Gestor de clusters de perfil](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Passos seguintes
* Para obter instruções detalhadas toodeploy e gerir clusters de servidor de informática distribuída da MATLAB no Azure, consulte Olá [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) repositório que contém os modelos de Olá e scripts.
* Aceda toohello [MathWorks site](http://www.mathworks.com/) para documentação detalhada para MATLAB e MATLAB distribuídas Server informática.
