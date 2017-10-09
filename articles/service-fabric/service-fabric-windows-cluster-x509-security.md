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
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>Proteger um cluster autónomo no Windows utilizando certificados x. 509
Este artigo descreve como comunicação de Olá toosecure entre Olá vários nós do cluster do Windows autónomo, bem como sobre como clientes de tooauthenticate toothis cluster, de que se ligam utilizando certificados x. 509. Isto garante que apenas utilizadores autorizados podem aceder a cluster Olá, Olá aplicações implementadas e efetuar tarefas de gestão.  Segurança do certificado deve ser ativada no cluster de Olá quando Olá cluster for criado.  

Para obter mais informações sobre a segurança do cluster como nó de nó segurança, segurança de nó de cliente e o controlo de acesso baseado em funções, consulte [cenários de segurança do Cluster](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>Os certificados vai precisar?
toostart com [transferir o pacote do cluster Olá autónomo](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone de nós de Olá no seu cluster. No Olá transferido o pacote, encontrará um **ClusterConfig.X509.MultiMachine.json** ficheiro. Abra o ficheiro de Olá e reveja a secção de Olá para **segurança** em Olá **propriedades** secção:

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

Esta secção descreve os certificados de Olá que precisa para proteger o seu cluster do Windows autónomo. Se especificar um certificado de cluster, defina o valor de Olá da **ClusterCredentialType** too_**X509**_. Se estiver a especificar o certificado de servidor para ligações externos, defina Olá **ServerCredentialType** demasiado_**X509**_. Embora não seja obrigatório, recomenda-se toohave ambos estes certificados para um cluster corretamente protegido. Se definir estes valores demasiado*X509* , em seguida, também tem de especificar Olá certificados correspondentes ou de Service Fabric irá gerar uma exceção. Em alguns cenários, só poderá ser útil toospecify Olá _ClientCertificateThumbprints_ ou _ReverseProxyCertificate_. Os cenários, não precisa de definir _ClusterCredentialType_ ou _ServerCredentialType_ too_X509_.


> [!NOTE]
> A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) é Olá identidade principal de um certificado. Leitura [como tooretrieve thumbprint de um certificado](https://msdn.microsoft.com/library/ms734695.aspx) toofind saída thumbprint Olá de certificados de Olá que criar.
> 
> 

Olá tabela seguinte apresenta uma lista de certificados de Olá que terá na sua configuração de cluster:

| **Definição de CertificateInformation** | **Descrição** |
| --- | --- |
| ClusterCertificate |Recomendado para ambiente de teste. Este certificado é necessário toosecure Olá comunicação entre nós Olá num cluster. Pode utilizar dois certificados diferentes, um servidor principal e secundária para a atualização. Definir Olá impressão digital do certificado principal Olá no Olá **Thumbprint** secção e que Olá secundário no Olá **ThumbprintSecondary** variáveis. |
| ClusterCertificateCommonNames |Recomenda-se de que o ambiente de produção. Este certificado é necessário toosecure Olá comunicação entre nós Olá num cluster. Pode utilizar um ou dois certificados comuns os nomes de clusters. |
| ServerCertificate |Recomendado para ambiente de teste. Este certificado é apresentado toohello cliente quando este tenta tooconnect toothis cluster. Para sua comodidade, pode escolher toouse Olá mesmo certificado para *ClusterCertificate* e *ServerCertificate*. Pode utilizar dois certificados de servidor diferente, um servidor principal e secundária para a atualização. Definir Olá impressão digital do certificado principal Olá no Olá **Thumbprint** secção e que Olá secundário no Olá **ThumbprintSecondary** variáveis. |
| ServerCertificateCommonNames |Recomenda-se de que o ambiente de produção. Este certificado é apresentado toohello cliente quando este tenta tooconnect toothis cluster. Para sua comodidade, pode escolher toouse Olá mesmo certificado para *ClusterCertificateCommonNames* e *ServerCertificateCommonNames*. Pode utilizar nomes do certificado de servidor comuns de um ou dois. |
| ClientCertificateThumbprints |Este é um conjunto de certificados que pretende que o tooinstall nos clientes Olá autenticado. Pode ter um número de certificados de cliente diferente instalado nos computadores de Olá que pretende que o cluster de toohello tooallow acesso. Definir o thumbprint de Olá de cada certificado em Olá **CertificateThumbprint** variável. Se definir Olá **IsAdmin** demasiado*verdadeiro*, em seguida, o cliente de Olá com este certificado instalado no mesmo pode fazer administrador atividades de gestão no cluster de Olá. Se hello **IsAdmin** é *falso*, cliente Olá com este certificado só pode efetuar ações de Olá permitidas para direitos de acesso de utilizador, normalmente só de leitura. Para obter mais informações sobre as funções leia [(RBAC) do controlo de acesso baseado em funções](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Conjunto Olá nome comum do certificado de cliente primeiro Olá para Olá **CertificateCommonName**. Olá **CertificateIssuerThumbprint** destina thumbprint Olá emissor Olá deste certificado. Leitura [trabalhar com certificados](https://msdn.microsoft.com/library/ms731899.aspx) tooknow mais informações sobre nomes comuns e o emissor de Olá. |
| ReverseProxyCertificate |Recomendado para ambiente de teste. Este é um certificado opcional que pode ser especificado se quiser toosecure sua [Proxy inverso](service-fabric-reverseproxy.md). Certifique-se reverseProxyEndpointPort está definido no nodeTypes se estiver a utilizar este certificado. |
| ReverseProxyCertificateCommonNames |Recomenda-se de que o ambiente de produção. Este é um certificado opcional que pode ser especificado se quiser toosecure sua [Proxy inverso](service-fabric-reverseproxy.md). Certifique-se reverseProxyEndpointPort está definido no nodeTypes se estiver a utilizar este certificado. |

Eis exemplo de configuração de cluster onde certificados de Cluster, o servidor e cliente Olá foram fornecidos. Tenha em atenção que para o cluster / servidor / reverseProxy certificados, o thumbprint e o nome comum não são permitidas toobe configurada em conjunto para Olá mesmo tipo de certificado.

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

## <a name="certificate-roll-over"></a>Rollover de certificado
Ao utilizar o nome comum do certificado em vez de thumbprint, agregação de certificado através de não necessita de atualização de configuração do cluster.
Se o emissor implicar a agregação de certificado através de rollover, mantenha certificados de emissor antigo Olá no arquivo de certificados de Olá, pelo menos, duas horas após a instalação do certificado de emissor novo Olá.

## <a name="acquire-hello-x509-certificates"></a>Adquirir certificados x. 509 de Olá
comunicação de toosecure num cluster de Olá, primeiro terá tooobtain x. 509 certificados para os nós do cluster. Além disso, toolimit ligação toothis tooauthorized máquinas/utilizadores de cluster, irá precisar tooobtain e instalar certificados para computadores de cliente do Olá.

Para clusters que executam cargas de trabalho de produção, deve utilizar um [autoridade de certificação (CA)](https://en.wikipedia.org/wiki/Certificate_authority) assinado cluster de Olá de toosecure de certificado x. 509. Para obter mais informações sobre como obter estes certificados, visite demasiado[como: obter um certificado](http://msdn.microsoft.com/library/aa702761.aspx).

Para os clusters que utilizar para fins de teste, pode escolher toouse um certificado autoassinado.

## <a name="optional-create-a-self-signed-certificate"></a>Opcional: Criar um certificado autoassinado
Uma forma toocreate um certificado autoassinado que pode ser protegido corretamente é toouse Olá *CertSetup.ps1* scripts na pasta do SDK de Service Fabric Olá no diretório de Olá *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Editar este nome do ficheiro toochange Olá predefinido do certificado de Olá (procure valor Olá *CN = ServiceFabricDevClusterCert*). Execute este script como `.\CertSetup.ps1 -Install`.

Agora exporte o ficheiro PFX de tooa de certificado do Olá com uma palavra-passe protegida. Obter primeiro Olá impressão digital do certificado de Olá. De Olá *iniciar* menu, execute Olá *gerir certificados de computador*. Navegue toohello **Local\Pessoal.** pasta e localizar Olá de certificado acabou de criar. Faça duplo clique em Olá certificado tooopen-lo, selecione de Olá *detalhes* separador e desloque-se para baixo toohello *Thumbprint* campo. Copie o valor do thumbprint Olá para o comando do PowerShell Olá abaixo, depois de remover os espaços de Olá.  Olá alteração `String` valor tooa tooprotect de palavra-passe segura adequado e Olá execução seguinte do PowerShell:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

detalhes de Olá toosee de um certificado instalado no Olá máquina pode executar Olá seguinte comando do PowerShell:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

Em alternativa, se tiver uma subscrição do Azure, siga secção Olá [adicionar certificados tooKey cofre](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Instalar certificados Olá
Assim que tiver o certificado (s), pode instalá-los em nós de cluster Olá. Os nós têm toohave hello mais recente do Windows PowerShell 3 instalado nos mesmos. Terá de toorepeat estes passos em cada nó de Cluster e servidor de certificados e quaisquer certificados secundários.

1. Copie o nó de toohello Olá. pfx ficheiros.
2. Abra uma janela do PowerShell como administrador e introduza Olá os seguintes comandos. Substitua Olá *$pswd* com palavra-passe de Olá que utilizou toocreate este certificado. Substitua Olá *$PfxFilePath* com o caminho completo do Olá do nó de toothis copiados Olá. pfx.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Agora defina o controlo de acesso Olá este certificado para que o processo de Service Fabric Olá, o que é executado em Olá conta de serviço de rede, pode utilizá-lo executando o seguinte script de Olá. Fornece Olá impressão digital do certificado de Olá e "Serviço de rede" para a conta de serviço Olá. Pode verificar que Olá ACLs no certificado Olá estão corretos ao abrir o certificado de Olá no *iniciar* > *gerir certificados de computador* e observar *todas as tarefas*  >  *Gerir chaves privadas*.
   
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
4. Repita os passos de Olá acima para cada certificado de servidor. Também pode utilizar estes passos tooinstall Olá certificados de cliente em máquinas de Olá que pretende que o cluster de toohello tooallow acesso.

## <a name="create-hello-secure-cluster"></a>Criar cluster segura Olá
Depois de configurar Olá **segurança** secção Olá **ClusterConfig.X509.MultiMachine.json** ficheiro, pode avançar demasiado[criar o cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure secção Olá nós e criar Olá autónomo cluster. Lembre-se toouse Olá **ClusterConfig.X509.MultiMachine.json** ficheiro ao criar o cluster de Olá. Por exemplo, o comando aspeto que poderá ter Olá seguinte:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Assim que tiver Olá segura autónomo Windows cluster ser executada com êxito e que a configuração Olá clientes autenticado tooconnect tooit, siga a secção de Olá [Connect tooa segura cluster através do PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. Por exemplo:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

Em seguida, pode executar outro toowork de comandos do PowerShell com este cluster. Por exemplo, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow uma lista de nós neste cluster segura.


cluster de Olá tooremove, ligar toohello de nó no cluster de olá onde transferiu o pacote de Service Fabric Olá, abra uma linha de comandos e navegue até toohello pasta do pacote. Agora, execute Olá os seguintes comandos:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Configuração de certificado incorreto poderão impedir a cluster Olá futuras cópias de segurança durante a implementação. tooself-diagnosticar problemas de segurança, consulte no grupo de Visualizador de eventos *registos de serviços e aplicações* > *Microsoft Service Fabric*.
> 
> 

