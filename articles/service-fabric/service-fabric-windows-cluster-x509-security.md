---
title: cluster aaaSecure um Azure Service Fabric no Windows utilizando certificados | Microsoft Docs
description: "Este artigo descreve como toosecure comunicação Olá autónomo ou privada, bem como cluster impedindo os clientes e cluster Olá."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="4b6df-103">Proteger um cluster autónomo no Windows utilizando certificados x. 509</span><span class="sxs-lookup"><span data-stu-id="4b6df-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="4b6df-104">Este artigo descreve como comunicação de Olá toosecure entre Olá vários nós do cluster do Windows autónomo, bem como sobre como clientes de tooauthenticate toothis cluster, de que se ligam utilizando certificados x. 509.</span><span class="sxs-lookup"><span data-stu-id="4b6df-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="4b6df-105">Isto garante que apenas utilizadores autorizados podem aceder a cluster Olá, Olá aplicações implementadas e efetuar tarefas de gestão.</span><span class="sxs-lookup"><span data-stu-id="4b6df-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="4b6df-106">Segurança do certificado deve ser ativada no cluster de Olá quando Olá cluster for criado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="4b6df-107">Para obter mais informações sobre a segurança do cluster como nó de nó segurança, segurança de nó de cliente e o controlo de acesso baseado em funções, consulte [cenários de segurança do Cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="4b6df-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="4b6df-108">Os certificados vai precisar?</span><span class="sxs-lookup"><span data-stu-id="4b6df-108">Which certificates will you need?</span></span>
<span data-ttu-id="4b6df-109">toostart com [transferir o pacote do cluster Olá autónomo](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone de nós de Olá no seu cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="4b6df-110">No Olá transferido o pacote, encontrará um **ClusterConfig.X509.MultiMachine.json** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="4b6df-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="4b6df-111">Abra o ficheiro de Olá e reveja a secção de Olá para **segurança** em Olá **propriedades** secção:</span><span class="sxs-lookup"><span data-stu-id="4b6df-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

<span data-ttu-id="4b6df-112">Esta secção descreve os certificados de Olá que precisa para proteger o seu cluster do Windows autónomo.</span><span class="sxs-lookup"><span data-stu-id="4b6df-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="4b6df-113">Se especificar um certificado de cluster, defina o valor de Olá da **ClusterCredentialType** too_**X509**_. Se estiver a especificar o certificado de servidor para ligações externos, defina Olá **ServerCredentialType** demasiado_**X509**_. Embora não seja obrigatório, recomenda-se toohave ambos estes certificados para um cluster corretamente protegido. Se definir estes valores demasiado*X509* , em seguida, também tem de especificar Olá certificados correspondentes ou de Service Fabric irá gerar uma exceção. Em alguns cenários, só poderá ser útil toospecify Olá _ClientCertificateThumbprints_ ou _ReverseProxyCertificate_. Os cenários, não precisa de definir _ClusterCredentialType_ ou _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="4b6df-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="4b6df-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) é Olá identidade principal de um certificado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="4b6df-115">Leitura [como tooretrieve thumbprint de um certificado](https://msdn.microsoft.com/library/ms734695.aspx) toofind saída thumbprint Olá de certificados de Olá que criar.</span><span class="sxs-lookup"><span data-stu-id="4b6df-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="4b6df-116">Olá tabela seguinte apresenta uma lista de certificados de Olá que terá na sua configuração de cluster:</span><span class="sxs-lookup"><span data-stu-id="4b6df-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="4b6df-117">**Definição de CertificateInformation**</span><span class="sxs-lookup"><span data-stu-id="4b6df-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="4b6df-118">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="4b6df-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="4b6df-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="4b6df-119">ClusterCertificate</span></span> |<span data-ttu-id="4b6df-120">Recomendado para ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4b6df-120">Recommended for test environment.</span></span> <span data-ttu-id="4b6df-121">Este certificado é necessário toosecure Olá comunicação entre nós Olá num cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="4b6df-122">Pode utilizar dois certificados diferentes, um servidor principal e secundária para a atualização.</span><span class="sxs-lookup"><span data-stu-id="4b6df-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="4b6df-123">Definir Olá impressão digital do certificado principal Olá no Olá **Thumbprint** secção e que Olá secundário no Olá **ThumbprintSecondary** variáveis.</span><span class="sxs-lookup"><span data-stu-id="4b6df-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="4b6df-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="4b6df-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="4b6df-125">Recomenda-se de que o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4b6df-125">Recommended for production environment.</span></span> <span data-ttu-id="4b6df-126">Este certificado é necessário toosecure Olá comunicação entre nós Olá num cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="4b6df-127">Pode utilizar um ou dois certificados comuns os nomes de clusters.</span><span class="sxs-lookup"><span data-stu-id="4b6df-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="4b6df-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="4b6df-128">ServerCertificate</span></span> |<span data-ttu-id="4b6df-129">Recomendado para ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4b6df-129">Recommended for test environment.</span></span> <span data-ttu-id="4b6df-130">Este certificado é apresentado toohello cliente quando este tenta tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="4b6df-131">Para sua comodidade, pode escolher toouse Olá mesmo certificado para *ClusterCertificate* e *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="4b6df-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="4b6df-132">Pode utilizar dois certificados de servidor diferente, um servidor principal e secundária para a atualização.</span><span class="sxs-lookup"><span data-stu-id="4b6df-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="4b6df-133">Definir Olá impressão digital do certificado principal Olá no Olá **Thumbprint** secção e que Olá secundário no Olá **ThumbprintSecondary** variáveis.</span><span class="sxs-lookup"><span data-stu-id="4b6df-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="4b6df-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="4b6df-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="4b6df-135">Recomenda-se de que o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4b6df-135">Recommended for production environment.</span></span> <span data-ttu-id="4b6df-136">Este certificado é apresentado toohello cliente quando este tenta tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="4b6df-137">Para sua comodidade, pode escolher toouse Olá mesmo certificado para *ClusterCertificateCommonNames* e *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="4b6df-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="4b6df-138">Pode utilizar nomes do certificado de servidor comuns de um ou dois.</span><span class="sxs-lookup"><span data-stu-id="4b6df-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="4b6df-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="4b6df-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="4b6df-140">Este é um conjunto de certificados que pretende que o tooinstall nos clientes Olá autenticado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="4b6df-141">Pode ter um número de certificados de cliente diferente instalado nos computadores de Olá que pretende que o cluster de toohello tooallow acesso.</span><span class="sxs-lookup"><span data-stu-id="4b6df-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="4b6df-142">Definir o thumbprint de Olá de cada certificado em Olá **CertificateThumbprint** variável.</span><span class="sxs-lookup"><span data-stu-id="4b6df-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="4b6df-143">Se definir Olá **IsAdmin** demasiado*verdadeiro*, em seguida, o cliente de Olá com este certificado instalado no mesmo pode fazer administrador atividades de gestão no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="4b6df-144">Se hello **IsAdmin** é *falso*, cliente Olá com este certificado só pode efetuar ações de Olá permitidas para direitos de acesso de utilizador, normalmente só de leitura.</span><span class="sxs-lookup"><span data-stu-id="4b6df-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="4b6df-145">Para obter mais informações sobre as funções leia [(RBAC) do controlo de acesso baseado em funções](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="4b6df-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="4b6df-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="4b6df-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="4b6df-147">Conjunto Olá nome comum do certificado de cliente primeiro Olá para Olá **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="4b6df-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="4b6df-148">Olá **CertificateIssuerThumbprint** destina thumbprint Olá emissor Olá deste certificado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="4b6df-149">Leitura [trabalhar com certificados](https://msdn.microsoft.com/library/ms731899.aspx) tooknow mais informações sobre nomes comuns e o emissor de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="4b6df-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="4b6df-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="4b6df-151">Recomendado para ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4b6df-151">Recommended for test environment.</span></span> <span data-ttu-id="4b6df-152">Este é um certificado opcional que pode ser especificado se quiser toosecure sua [Proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="4b6df-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="4b6df-153">Certifique-se reverseProxyEndpointPort está definido no nodeTypes se estiver a utilizar este certificado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="4b6df-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="4b6df-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="4b6df-155">Recomenda-se de que o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4b6df-155">Recommended for production environment.</span></span> <span data-ttu-id="4b6df-156">Este é um certificado opcional que pode ser especificado se quiser toosecure sua [Proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="4b6df-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="4b6df-157">Certifique-se reverseProxyEndpointPort está definido no nodeTypes se estiver a utilizar este certificado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="4b6df-158">Eis exemplo de configuração de cluster onde certificados de Cluster, o servidor e cliente Olá foram fornecidos.</span><span class="sxs-lookup"><span data-stu-id="4b6df-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="4b6df-159">Tenha em atenção que para o cluster / servidor / reverseProxy certificados, o thumbprint e o nome comum não são permitidas toobe configurada em conjunto para Olá mesmo tipo de certificado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a><span data-ttu-id="4b6df-160">Rollover de certificado</span><span class="sxs-lookup"><span data-stu-id="4b6df-160">Certificate roll over</span></span>
<span data-ttu-id="4b6df-161">Ao utilizar o nome comum do certificado em vez de thumbprint, agregação de certificado através de não necessita de atualização de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="4b6df-162">Se o emissor implicar a agregação de certificado através de rollover, mantenha certificados de emissor antigo Olá no arquivo de certificados de Olá, pelo menos, duas horas após a instalação do certificado de emissor novo Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="4b6df-163">Adquirir certificados x. 509 de Olá</span><span class="sxs-lookup"><span data-stu-id="4b6df-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="4b6df-164">comunicação de toosecure num cluster de Olá, primeiro terá tooobtain x. 509 certificados para os nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="4b6df-165">Além disso, toolimit ligação toothis tooauthorized máquinas/utilizadores de cluster, irá precisar tooobtain e instalar certificados para computadores de cliente do Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="4b6df-166">Para clusters que executam cargas de trabalho de produção, deve utilizar um [autoridade de certificação (CA)](https://en.wikipedia.org/wiki/Certificate_authority) assinado cluster de Olá de toosecure de certificado x. 509.</span><span class="sxs-lookup"><span data-stu-id="4b6df-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="4b6df-167">Para obter mais informações sobre como obter estes certificados, visite demasiado[como: obter um certificado](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b6df-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="4b6df-168">Para os clusters que utilizar para fins de teste, pode escolher toouse um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="4b6df-169">Opcional: Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="4b6df-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="4b6df-170">Uma forma toocreate um certificado autoassinado que pode ser protegido corretamente é toouse Olá *CertSetup.ps1* scripts na pasta do SDK de Service Fabric Olá no diretório de Olá *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="4b6df-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="4b6df-171">Editar este nome do ficheiro toochange Olá predefinido do certificado de Olá (procure valor Olá *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="4b6df-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="4b6df-172">Execute este script como `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="4b6df-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="4b6df-173">Agora exporte o ficheiro PFX de tooa de certificado do Olá com uma palavra-passe protegida.</span><span class="sxs-lookup"><span data-stu-id="4b6df-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="4b6df-174">Obter primeiro Olá impressão digital do certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="4b6df-175">De Olá *iniciar* menu, execute Olá *gerir certificados de computador*.</span><span class="sxs-lookup"><span data-stu-id="4b6df-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="4b6df-176">Navegue toohello **Local\Pessoal.** pasta e localizar Olá de certificado acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="4b6df-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="4b6df-177">Faça duplo clique em Olá certificado tooopen-lo, selecione de Olá *detalhes* separador e desloque-se para baixo toohello *Thumbprint* campo.</span><span class="sxs-lookup"><span data-stu-id="4b6df-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="4b6df-178">Copie o valor do thumbprint Olá para o comando do PowerShell Olá abaixo, depois de remover os espaços de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="4b6df-179">Olá alteração `String` valor tooa tooprotect de palavra-passe segura adequado e Olá execução seguinte do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4b6df-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="4b6df-180">detalhes de Olá toosee de um certificado instalado no Olá máquina pode executar Olá seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4b6df-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="4b6df-181">Em alternativa, se tiver uma subscrição do Azure, siga secção Olá [adicionar certificados tooKey cofre](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="4b6df-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="4b6df-182">Instalar certificados Olá</span><span class="sxs-lookup"><span data-stu-id="4b6df-182">Install hello certificates</span></span>
<span data-ttu-id="4b6df-183">Assim que tiver o certificado (s), pode instalá-los em nós de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="4b6df-184">Os nós têm toohave hello mais recente do Windows PowerShell 3 instalado nos mesmos.</span><span class="sxs-lookup"><span data-stu-id="4b6df-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="4b6df-185">Terá de toorepeat estes passos em cada nó de Cluster e servidor de certificados e quaisquer certificados secundários.</span><span class="sxs-lookup"><span data-stu-id="4b6df-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="4b6df-186">Copie o nó de toohello Olá. pfx ficheiros.</span><span class="sxs-lookup"><span data-stu-id="4b6df-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="4b6df-187">Abra uma janela do PowerShell como administrador e introduza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="4b6df-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="4b6df-188">Substitua Olá *$pswd* com palavra-passe de Olá que utilizou toocreate este certificado.</span><span class="sxs-lookup"><span data-stu-id="4b6df-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="4b6df-189">Substitua Olá *$PfxFilePath* com o caminho completo do Olá do nó de toothis copiados Olá. pfx.</span><span class="sxs-lookup"><span data-stu-id="4b6df-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="4b6df-190">Agora defina o controlo de acesso Olá este certificado para que o processo de Service Fabric Olá, o que é executado em Olá conta de serviço de rede, pode utilizá-lo executando o seguinte script de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="4b6df-191">Fornece Olá impressão digital do certificado de Olá e "Serviço de rede" para a conta de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="4b6df-192">Pode verificar que Olá ACLs no certificado Olá estão corretos ao abrir o certificado de Olá no *iniciar* > *gerir certificados de computador* e observar *todas as tarefas*  >  *Gerir chaves privadas*.</span><span class="sxs-lookup"><span data-stu-id="4b6df-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="4b6df-193">Repita os passos de Olá acima para cada certificado de servidor.</span><span class="sxs-lookup"><span data-stu-id="4b6df-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="4b6df-194">Também pode utilizar estes passos tooinstall Olá certificados de cliente em máquinas de Olá que pretende que o cluster de toohello tooallow acesso.</span><span class="sxs-lookup"><span data-stu-id="4b6df-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="4b6df-195">Criar cluster segura Olá</span><span class="sxs-lookup"><span data-stu-id="4b6df-195">Create hello secure cluster</span></span>
<span data-ttu-id="4b6df-196">Depois de configurar Olá **segurança** secção Olá **ClusterConfig.X509.MultiMachine.json** ficheiro, pode avançar demasiado[criar o cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure secção Olá nós e criar Olá autónomo cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="4b6df-197">Lembre-se toouse Olá **ClusterConfig.X509.MultiMachine.json** ficheiro ao criar o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b6df-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="4b6df-198">Por exemplo, o comando aspeto que poderá ter Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b6df-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="4b6df-199">Assim que tiver Olá segura autónomo Windows cluster ser executada com êxito e que a configuração Olá clientes autenticado tooconnect tooit, siga a secção de Olá [Connect tooa segura cluster através do PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="4b6df-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="4b6df-200">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4b6df-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="4b6df-201">Em seguida, pode executar outro toowork de comandos do PowerShell com este cluster.</span><span class="sxs-lookup"><span data-stu-id="4b6df-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="4b6df-202">Por exemplo, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow uma lista de nós neste cluster segura.</span><span class="sxs-lookup"><span data-stu-id="4b6df-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="4b6df-203">cluster de Olá tooremove, ligar toohello de nó no cluster de olá onde transferiu o pacote de Service Fabric Olá, abra uma linha de comandos e navegue até toohello pasta do pacote.</span><span class="sxs-lookup"><span data-stu-id="4b6df-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="4b6df-204">Agora, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4b6df-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="4b6df-205">Configuração de certificado incorreto poderão impedir a cluster Olá futuras cópias de segurança durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="4b6df-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="4b6df-206">tooself-diagnosticar problemas de segurança, consulte no grupo de Visualizador de eventos *registos de serviços e aplicações* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="4b6df-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

