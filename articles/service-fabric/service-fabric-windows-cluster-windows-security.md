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
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Proteger um cluster autónomo no Windows utilizando a segurança do Windows
cluster do Service Fabric de tooa de acesso não autorizado de tooprevent, tem de proteger o cluster de Olá. Segurança é especialmente importante quando executa o cluster de Olá cargas de trabalho de produção. Este artigo descreve como tooconfigure segurança de nó de nó e nó de cliente utilizando a segurança do Windows hello *Clusterconfig* ficheiro.  processo de Olá corresponde toohello configurar o passo de segurança do [criar um cluster autónomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md). Para obter mais informações sobre como o Service Fabric utiliza a segurança do Windows, consulte [cenários de segurança do Cluster](service-fabric-cluster-security.md).

> [!NOTE]
> Deve considerar a seleção de Olá de nó de nó segurança cuidadosamente porque não existe nenhuma atualização de cluster a partir de um tooanother de opção de segurança. seleção de segurança do toochange Olá, terá de cluster completo de Olá toorebuild.
>
>

## <a name="configure-windows-security-using-gmsa"></a>Configurar a segurança do Windows utilizam a gMSA  
exemplo de Olá *ClusterConfig.gMSA.Windows.MultiMachine.JSON* transferir ficheiro de configuração com Olá [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. Zip](http://go.microsoft.com/fwlink/?LinkId=730690) pacote do cluster autónomo contém um modelo para a configuração através de segurança do Windows [conta de serviço gerida da grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

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
  
| **Definição de configuração** | **Descrição** |  
| --- | --- |  
| WindowsIdentities |Contém identidades Olá de cluster e o cliente. |  
| ClustergMSAIdentity |Configura a segurança de nó de nó. Um grupo de conta de serviço gerida. |  
| ClusterSPN |Domínio completamente qualificado SPN de conta gMSA|  
| ClientIdentities |Configura a segurança de nó de cliente. Uma matriz de contas de utilizador do cliente. |  
| Identidade |identidade do cliente Olá, um utilizador de domínio. |  
| IsAdmin |VERDADEIRO Especifica que esse utilizador de domínio de Olá tem acesso de cliente de administrador, FALSO para acesso de cliente do utilizador. |  
  
[Segurança do nó toonode](service-fabric-cluster-security.md#node-to-node-security) é configurada através da definição **ClustergMSAIdentity** quando os recursos de infraestrutura de serviço tem toorun em gMSA. Na ordem toobuild as relações de confiança entre os nós, estes têm de ser efetuadas em consideração entre si. Isto pode ser conseguido de duas formas diferentes: Especifique Olá grupo conta de serviço gerida que inclui todos os nós no cluster de Olá ou especifique Olá domínio máquina grupo que inclua todos os nós no cluster de Olá. Recomendamos vivamente a utilização Olá [conta de serviço gerida da grupo (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) abordagem, especialmente para clusters maiores (mais de 10 nós) ou para os clusters que são toogrow provavelmente ou diminuir.  
Esta abordagem não necessita de Olá criação de um grupo de domínio para o qual os administradores de cluster foi concedidos tooadd de direitos de acesso e remover membros. Estas contas também são úteis para a gestão de palavra-passe automática. Para obter mais informações, consulte [introdução às contas de serviço geridas de grupo](http://technet.microsoft.com/library/jj128431.aspx).  
 
[Segurança do cliente toonode](service-fabric-cluster-security.md#client-to-node-security) é configurada utilizando **ClientIdentities**. Em ordem tooestablish confiança entre um cluster de cliente e Olá, tem de configurar as identidades de cliente que pode confiar Olá tooknow de cluster. Isto pode ser feito de duas formas diferentes: Especifique Olá grupo os utilizadores de domínio que podem ligar ou especificar Olá utilizadores de nó de domínio que possam ligar. Service Fabric suportam dois tipos de controlo de acesso diferentes para clientes que estejam ligados tooa cluster do Service Fabric: administrador e utilizador. Controlo de acesso permite Olá para Olá cluster administrador toolimit acesso toocertain os tipos de operações de cluster para diferentes grupos de utilizadores, tornando o cluster de Olá mais segura.  Os administradores têm capacidades de toomanagement acesso total (incluindo as capacidades de leitura/escrita). Por predefinição, os utilizadores, tem apenas capacidades de toomanagement de acesso de leitura (por exemplo, capacidades de consulta) e Olá capacidade tooresolve serviços e aplicações. Para obter mais informações sobre controlos de acesso, consulte [baseado em funções controlo de acesso para clientes de Service Fabric](service-fabric-cluster-security-roles.md).  
 
Olá seguintes exemplo **segurança** secção configura a segurança do Windows utilizam a gMSA e especifica que Olá máquinas na *ServiceFabric.clusterA.contoso.com* gMSA fazem parte do cluster de Olá e que *CONTOSO\usera* tem acesso de cliente de administrador:  
  
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
  
## <a name="configure-windows-security-using-a-machine-group"></a>Configurar a segurança do Windows utilizando um grupo de máquinas  
exemplo de Olá *ClusterConfig.Windows.MultiMachine.JSON* transferir ficheiro de configuração com Olá [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. Zip](http://go.microsoft.com/fwlink/?LinkId=730690) pacote do cluster autónomo contém um modelo para a configuração de segurança do Windows.  Segurança do Windows está configurada no Olá **propriedades** secção: 

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

| **Definição de configuração** | **Descrição** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** estiver definido demasiado*Windows* se ClusterIdentity Especifica um nome de grupo de computador do Active Directory. |  
| ServerCredentialType |Definir demasiado*Windows* tooenable segurança do Windows para clientes.<br /><br />Isto indica que os clientes de Olá Olá do cluster de e cluster Olá próprio estão em execução dentro de um domínio do Active Directory. |  
| WindowsIdentities |Contém identidades Olá de cluster e o cliente. |  
| ClusterIdentity |Utilize um nome de grupo do computador, a domain\machinegroup, a segurança do nó para o nó de tooconfigure. |  
| ClientIdentities |Configura a segurança de nó de cliente. Uma matriz de contas de utilizador do cliente. |  
| Identidade |Adicione utilizador de domínio Olá, domínio ome de utilizador para a identidade do cliente Olá. |  
| IsAdmin |Conjunto tootrue toospecify que Olá utilizador de domínio tem acesso de cliente de administrador ou FALSO para acesso de cliente do utilizador. |  

[Segurança do nó toonode](service-fabric-cluster-security.md#node-to-node-security) estiver configurado utilizando a definição **ClusterIdentity** se quiser toouse um grupo de computador dentro de um domínio do Active Directory. Para obter mais informações, consulte [criar um grupo de computador no Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).

[Segurança de cliente para o nó](service-fabric-cluster-security.md#client-to-node-security) é configurada utilizando **ClientIdentities**. tooestablish confiança entre o cluster de cliente e Olá, tem de configurar Olá cluster tooknow Olá cliente identidades Olá cluster podem confiar. Pode estabelecer confiança de duas formas diferentes:

- Especifique Olá grupo os utilizadores de domínio que possam ligar.
- Especifique Olá nó os utilizadores de domínio que possam ligar.

Service Fabric suportam dois tipos de controlo de acesso diferentes para clientes que estejam ligados tooa cluster do Service Fabric: administrador e utilizador. Controlo de acesso permite Olá administrador toolimit acesso toocertain tipos de cluster de operações de cluster para diferentes grupos de utilizadores, que faz com que o cluster de Olá mais segura.  Os administradores têm capacidades de toomanagement acesso total (incluindo as capacidades de leitura/escrita). Por predefinição, os utilizadores, tem apenas capacidades de toomanagement de acesso de leitura (por exemplo, capacidades de consulta) e Olá capacidade tooresolve serviços e aplicações.  

Olá seguintes exemplo **segurança** secção configura a segurança do Windows, especifica que Olá máquinas na *ServiceFabric/clusterA.contoso.com* fazem parte do cluster de Olá e especifica que  *CONTOSO\usera* tem acesso de cliente de administrador:

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
> Service Fabric não devem ser implementado num controlador de domínio. Certifique-se de que Clusterconfig não incluir o endereço IP de Olá de controlador de domínio Olá quando utilizar um grupo de computador ou grupo a conta de serviço gerida (gMSA).
>
>

## <a name="next-steps"></a>Passos seguintes
Depois de configurar a segurança do Windows numa Olá *Clusterconfig* ficheiro, retomar o processo de criação do cluster Olá no [criar um cluster autónomo em execução no Windows](service-fabric-cluster-creation-for-windows-server.md).

Para obter mais informações sobre consulte de segurança, segurança de nó de cliente e o controlo de acesso baseado em funções, como nó ao nó [cenários de segurança do Cluster](service-fabric-cluster-security.md).

Consulte [Connect tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para obter exemplos de ligar utilizando o PowerShell ou FabricClient.
