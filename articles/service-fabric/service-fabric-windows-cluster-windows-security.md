---
title: "aaaSecure um cluster em execução no Windows através de segurança do Windows | Microsoft Docs"
description: "Saiba como de segurança de nó de nó e nó de cliente de tooconfigure num autónomo cluster em execução no Windows através de segurança do Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="aa082-103">Proteger um cluster autónomo no Windows utilizando a segurança do Windows</span><span class="sxs-lookup"><span data-stu-id="aa082-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="aa082-104">cluster do Service Fabric de tooa de acesso não autorizado de tooprevent, tem de proteger o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="aa082-104">tooprevent unauthorized access tooa Service Fabric cluster, you must secure hello cluster.</span></span> <span data-ttu-id="aa082-105">Segurança é especialmente importante quando executa o cluster de Olá cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="aa082-105">Security is especially important when hello cluster runs production workloads.</span></span> <span data-ttu-id="aa082-106">Este artigo descreve como tooconfigure segurança de nó de nó e nó de cliente utilizando a segurança do Windows hello *Clusterconfig* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="aa082-106">This article describes how tooconfigure node-to-node and client-to-node security by using Windows security in hello *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="aa082-107">processo de Olá corresponde toohello configurar o passo de segurança do [criar um cluster autónomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="aa082-107">hello process corresponds toohello configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="aa082-108">Para obter mais informações sobre como o Service Fabric utiliza a segurança do Windows, consulte [cenários de segurança do Cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="aa082-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aa082-109">Deve considerar a seleção de Olá de nó de nó segurança cuidadosamente porque não existe nenhuma atualização de cluster a partir de um tooanother de opção de segurança.</span><span class="sxs-lookup"><span data-stu-id="aa082-109">You should consider hello selection of node-to-node security carefully because there is no cluster upgrade from one security choice tooanother.</span></span> <span data-ttu-id="aa082-110">seleção de segurança do toochange Olá, terá de cluster completo de Olá toorebuild.</span><span class="sxs-lookup"><span data-stu-id="aa082-110">toochange hello security selection, you have toorebuild hello full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="aa082-111">Configurar a segurança do Windows utilizam a gMSA</span><span class="sxs-lookup"><span data-stu-id="aa082-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="aa082-112">exemplo de Olá *ClusterConfig.gMSA.Windows.MultiMachine.JSON* transferir ficheiro de configuração com Olá [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. Zip](http://go.microsoft.com/fwlink/?LinkId=730690) pacote do cluster autónomo contém um modelo para a configuração através de segurança do Windows [conta de serviço gerida da grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="aa082-112">hello sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="aa082-113">**Definição de configuração**</span><span class="sxs-lookup"><span data-stu-id="aa082-113">**Configuration Setting**</span></span> | <span data-ttu-id="aa082-114">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="aa082-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="aa082-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="aa082-115">WindowsIdentities</span></span> |<span data-ttu-id="aa082-116">Contém identidades Olá de cluster e o cliente.</span><span class="sxs-lookup"><span data-stu-id="aa082-116">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="aa082-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="aa082-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="aa082-118">Configura a segurança de nó de nó.</span><span class="sxs-lookup"><span data-stu-id="aa082-118">Configures node-to-node security.</span></span> <span data-ttu-id="aa082-119">Um grupo de conta de serviço gerida.</span><span class="sxs-lookup"><span data-stu-id="aa082-119">A group managed service account.</span></span> |  
| <span data-ttu-id="aa082-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="aa082-120">ClusterSPN</span></span> |<span data-ttu-id="aa082-121">Domínio completamente qualificado SPN de conta gMSA</span><span class="sxs-lookup"><span data-stu-id="aa082-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="aa082-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="aa082-122">ClientIdentities</span></span> |<span data-ttu-id="aa082-123">Configura a segurança de nó de cliente.</span><span class="sxs-lookup"><span data-stu-id="aa082-123">Configures client-to-node security.</span></span> <span data-ttu-id="aa082-124">Uma matriz de contas de utilizador do cliente.</span><span class="sxs-lookup"><span data-stu-id="aa082-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="aa082-125">Identidade</span><span class="sxs-lookup"><span data-stu-id="aa082-125">Identity</span></span> |<span data-ttu-id="aa082-126">identidade do cliente Olá, um utilizador de domínio.</span><span class="sxs-lookup"><span data-stu-id="aa082-126">hello client identity, a domain user.</span></span> |  
| <span data-ttu-id="aa082-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="aa082-127">IsAdmin</span></span> |<span data-ttu-id="aa082-128">VERDADEIRO Especifica que esse utilizador de domínio de Olá tem acesso de cliente de administrador, FALSO para acesso de cliente do utilizador.</span><span class="sxs-lookup"><span data-stu-id="aa082-128">True specifies that hello domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="aa082-129">[Segurança do nó toonode](service-fabric-cluster-security.md#node-to-node-security) é configurada através da definição **ClustergMSAIdentity** quando os recursos de infraestrutura de serviço tem toorun em gMSA.</span><span class="sxs-lookup"><span data-stu-id="aa082-129">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs toorun under gMSA.</span></span> <span data-ttu-id="aa082-130">Na ordem toobuild as relações de confiança entre os nós, estes têm de ser efetuadas em consideração entre si.</span><span class="sxs-lookup"><span data-stu-id="aa082-130">In order toobuild trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="aa082-131">Isto pode ser conseguido de duas formas diferentes: Especifique Olá grupo conta de serviço gerida que inclui todos os nós no cluster de Olá ou especifique Olá domínio máquina grupo que inclua todos os nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="aa082-131">This can be accomplished in two different ways: Specify hello Group Managed Service Account that includes all nodes in hello cluster or Specify hello domain machine group that includes all nodes in hello cluster.</span></span> <span data-ttu-id="aa082-132">Recomendamos vivamente a utilização Olá [conta de serviço gerida da grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) abordagem, especialmente para clusters maiores (mais de 10 nós) ou para os clusters que são toogrow provavelmente ou diminuir.</span><span class="sxs-lookup"><span data-stu-id="aa082-132">We strongly recommend using hello [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely toogrow or shrink.</span></span>  
<span data-ttu-id="aa082-133">Esta abordagem não necessita de Olá criação de um grupo de domínio para o qual os administradores de cluster foi concedidos tooadd de direitos de acesso e remover membros.</span><span class="sxs-lookup"><span data-stu-id="aa082-133">This approach does not require hello creation of a domain group for which cluster administrators have been granted access rights tooadd and remove members.</span></span> <span data-ttu-id="aa082-134">Estas contas também são úteis para a gestão de palavra-passe automática.</span><span class="sxs-lookup"><span data-stu-id="aa082-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="aa082-135">Para obter mais informações, consulte [introdução às contas de serviço geridas de grupo](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa082-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="aa082-136">[Segurança do cliente toonode](service-fabric-cluster-security.md#client-to-node-security) é configurada utilizando **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="aa082-136">[Client toonode security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="aa082-137">Em ordem tooestablish confiança entre um cluster de cliente e Olá, tem de configurar as identidades de cliente que pode confiar Olá tooknow de cluster.</span><span class="sxs-lookup"><span data-stu-id="aa082-137">In order tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow which client identities that it can trust.</span></span> <span data-ttu-id="aa082-138">Isto pode ser feito de duas formas diferentes: Especifique Olá grupo os utilizadores de domínio que podem ligar ou especificar Olá utilizadores de nó de domínio que possam ligar.</span><span class="sxs-lookup"><span data-stu-id="aa082-138">This can be done in two different ways: Specify hello domain group users that can connect or specify hello domain node users that can connect.</span></span> <span data-ttu-id="aa082-139">Service Fabric suportam dois tipos de controlo de acesso diferentes para clientes que estejam ligados tooa cluster do Service Fabric: administrador e utilizador.</span><span class="sxs-lookup"><span data-stu-id="aa082-139">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="aa082-140">Controlo de acesso permite Olá para Olá cluster administrador toolimit acesso toocertain os tipos de operações de cluster para diferentes grupos de utilizadores, tornando o cluster de Olá mais segura.</span><span class="sxs-lookup"><span data-stu-id="aa082-140">Access control provides hello ability for hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, making hello cluster more secure.</span></span>  <span data-ttu-id="aa082-141">Os administradores têm capacidades de toomanagement acesso total (incluindo as capacidades de leitura/escrita).</span><span class="sxs-lookup"><span data-stu-id="aa082-141">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="aa082-142">Por predefinição, os utilizadores, tem apenas capacidades de toomanagement de acesso de leitura (por exemplo, capacidades de consulta) e Olá capacidade tooresolve serviços e aplicações.</span><span class="sxs-lookup"><span data-stu-id="aa082-142">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span> <span data-ttu-id="aa082-143">Para obter mais informações sobre controlos de acesso, consulte [baseado em funções controlo de acesso para clientes de Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="aa082-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="aa082-144">Olá seguintes exemplo **segurança** secção configura a segurança do Windows utilizam a gMSA e especifica que Olá máquinas na *ServiceFabric.clusterA.contoso.com* gMSA fazem parte do cluster de Olá e que *CONTOSO\usera* tem acesso de cliente de administrador:</span><span class="sxs-lookup"><span data-stu-id="aa082-144">hello following example **security** section configures Windows security using gMSA and specifies that hello machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of hello cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="aa082-145">Configurar a segurança do Windows utilizando um grupo de máquinas</span><span class="sxs-lookup"><span data-stu-id="aa082-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="aa082-146">exemplo de Olá *ClusterConfig.Windows.MultiMachine.JSON* transferir ficheiro de configuração com Olá [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. Zip](http://go.microsoft.com/fwlink/?LinkId=730690) pacote do cluster autónomo contém um modelo para a configuração de segurança do Windows.</span><span class="sxs-lookup"><span data-stu-id="aa082-146">hello sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="aa082-147">Segurança do Windows está configurada no Olá **propriedades** secção:</span><span class="sxs-lookup"><span data-stu-id="aa082-147">Windows security is configured in hello **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="aa082-148">**Definição de configuração**</span><span class="sxs-lookup"><span data-stu-id="aa082-148">**Configuration setting**</span></span> | <span data-ttu-id="aa082-149">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="aa082-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="aa082-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="aa082-150">ClusterCredentialType</span></span> |<span data-ttu-id="aa082-151">**ClusterCredentialType** estiver definido demasiado*Windows* se ClusterIdentity Especifica um nome de grupo de computador do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa082-151">**ClusterCredentialType** is set too*Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="aa082-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="aa082-152">ServerCredentialType</span></span> |<span data-ttu-id="aa082-153">Definir demasiado*Windows* tooenable segurança do Windows para clientes.</span><span class="sxs-lookup"><span data-stu-id="aa082-153">Set too*Windows* tooenable Windows security for clients.</span></span><br /><br /><span data-ttu-id="aa082-154">Isto indica que os clientes de Olá Olá do cluster de e cluster Olá próprio estão em execução dentro de um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa082-154">This indicates that hello clients of hello cluster and hello cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="aa082-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="aa082-155">WindowsIdentities</span></span> |<span data-ttu-id="aa082-156">Contém identidades Olá de cluster e o cliente.</span><span class="sxs-lookup"><span data-stu-id="aa082-156">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="aa082-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="aa082-157">ClusterIdentity</span></span> |<span data-ttu-id="aa082-158">Utilize um nome de grupo do computador, a domain\machinegroup, a segurança do nó para o nó de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="aa082-158">Use a machine group name, domain\machinegroup, tooconfigure node-to-node security.</span></span> |  
| <span data-ttu-id="aa082-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="aa082-159">ClientIdentities</span></span> |<span data-ttu-id="aa082-160">Configura a segurança de nó de cliente.</span><span class="sxs-lookup"><span data-stu-id="aa082-160">Configures client-to-node security.</span></span> <span data-ttu-id="aa082-161">Uma matriz de contas de utilizador do cliente.</span><span class="sxs-lookup"><span data-stu-id="aa082-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="aa082-162">Identidade</span><span class="sxs-lookup"><span data-stu-id="aa082-162">Identity</span></span> |<span data-ttu-id="aa082-163">Adicione utilizador de domínio Olá, domínio ome de utilizador para a identidade do cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="aa082-163">Add hello domain user, domain\username, for hello client identity.</span></span> |  
| <span data-ttu-id="aa082-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="aa082-164">IsAdmin</span></span> |<span data-ttu-id="aa082-165">Conjunto tootrue toospecify que Olá utilizador de domínio tem acesso de cliente de administrador ou FALSO para acesso de cliente do utilizador.</span><span class="sxs-lookup"><span data-stu-id="aa082-165">Set tootrue toospecify that hello domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="aa082-166">[Segurança do nó toonode](service-fabric-cluster-security.md#node-to-node-security) estiver configurado utilizando a definição **ClusterIdentity** se quiser toouse um grupo de computador dentro de um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa082-166">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want toouse a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="aa082-167">Para obter mais informações, consulte [criar um grupo de computador no Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="aa082-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="aa082-168">[Segurança de cliente para o nó](service-fabric-cluster-security.md#client-to-node-security) é configurada utilizando **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="aa082-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="aa082-169">tooestablish confiança entre o cluster de cliente e Olá, tem de configurar Olá cluster tooknow Olá cliente identidades Olá cluster podem confiar.</span><span class="sxs-lookup"><span data-stu-id="aa082-169">tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow hello client identities that hello cluster can trust.</span></span> <span data-ttu-id="aa082-170">Pode estabelecer confiança de duas formas diferentes:</span><span class="sxs-lookup"><span data-stu-id="aa082-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="aa082-171">Especifique Olá grupo os utilizadores de domínio que possam ligar.</span><span class="sxs-lookup"><span data-stu-id="aa082-171">Specify hello domain group users that can connect.</span></span>
- <span data-ttu-id="aa082-172">Especifique Olá nó os utilizadores de domínio que possam ligar.</span><span class="sxs-lookup"><span data-stu-id="aa082-172">Specify hello domain node users that can connect.</span></span>

<span data-ttu-id="aa082-173">Service Fabric suportam dois tipos de controlo de acesso diferentes para clientes que estejam ligados tooa cluster do Service Fabric: administrador e utilizador.</span><span class="sxs-lookup"><span data-stu-id="aa082-173">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="aa082-174">Controlo de acesso permite Olá administrador toolimit acesso toocertain tipos de cluster de operações de cluster para diferentes grupos de utilizadores, que faz com que o cluster de Olá mais segura.</span><span class="sxs-lookup"><span data-stu-id="aa082-174">Access control enables hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, which makes hello cluster more secure.</span></span>  <span data-ttu-id="aa082-175">Os administradores têm capacidades de toomanagement acesso total (incluindo as capacidades de leitura/escrita).</span><span class="sxs-lookup"><span data-stu-id="aa082-175">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="aa082-176">Por predefinição, os utilizadores, tem apenas capacidades de toomanagement de acesso de leitura (por exemplo, capacidades de consulta) e Olá capacidade tooresolve serviços e aplicações.</span><span class="sxs-lookup"><span data-stu-id="aa082-176">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>  

<span data-ttu-id="aa082-177">Olá seguintes exemplo **segurança** secção configura a segurança do Windows, especifica que Olá máquinas na *ServiceFabric/clusterA.contoso.com* fazem parte do cluster de Olá e especifica que  *CONTOSO\usera* tem acesso de cliente de administrador:</span><span class="sxs-lookup"><span data-stu-id="aa082-177">hello following example **security** section configures Windows security, specifies that hello machines in *ServiceFabric/clusterA.contoso.com* are part of hello cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="aa082-178">Service Fabric não devem ser implementado num controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="aa082-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="aa082-179">Certifique-se de que Clusterconfig não incluir o endereço IP de Olá de controlador de domínio Olá quando utilizar um grupo de computador ou grupo a conta de serviço gerida (gMSA).</span><span class="sxs-lookup"><span data-stu-id="aa082-179">Make sure that ClusterConfig.json does not include hello IP address of hello domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="aa082-180">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="aa082-180">Next steps</span></span>
<span data-ttu-id="aa082-181">Depois de configurar a segurança do Windows numa Olá *Clusterconfig* ficheiro, retomar o processo de criação do cluster Olá no [criar um cluster autónomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="aa082-181">After configuring Windows security in hello *ClusterConfig.JSON* file, resume hello cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="aa082-182">Para obter mais informações sobre consulte de segurança, segurança de nó de cliente e o controlo de acesso baseado em funções, como nó ao nó [cenários de segurança do Cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="aa082-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="aa082-183">Consulte [Connect tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para obter exemplos de ligar utilizando o PowerShell ou FabricClient.</span><span class="sxs-lookup"><span data-stu-id="aa082-183">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
