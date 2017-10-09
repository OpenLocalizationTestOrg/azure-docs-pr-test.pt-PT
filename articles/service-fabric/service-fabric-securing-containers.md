---
title: "aaaAzure segurança de contentor do Service Fabric | Microsoft Docs"
description: "Saiba agora toosecure serviços de contentor."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a><span data-ttu-id="74b9b-103">Segurança de contentor</span><span class="sxs-lookup"><span data-stu-id="74b9b-103">Container security</span></span>

<span data-ttu-id="74b9b-104">O Service Fabric fornece um mecanismo para serviços no interior de um contentor tooaccess um certificado que está instalado em Olá nós num cluster do Windows ou Linux (versão 5.7 ou superior).</span><span class="sxs-lookup"><span data-stu-id="74b9b-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="74b9b-105">Além disso, a Service Fabric também suporta a gMSA (grupo contas de serviço geridas) para contentores do Windows.</span><span class="sxs-lookup"><span data-stu-id="74b9b-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="74b9b-106">Gestão de certificados para contentores</span><span class="sxs-lookup"><span data-stu-id="74b9b-106">Certificate management for containers</span></span>

<span data-ttu-id="74b9b-107">Pode proteger os serviços de contentor, especificando um certificado.</span><span class="sxs-lookup"><span data-stu-id="74b9b-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="74b9b-108">certificado de Olá deve ser instalado em nós de Olá do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="74b9b-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="74b9b-109">Olá informações do certificado são fornecidas no manifesto da aplicação Olá em Olá `ContainerHostPolicies` etiquetas como Olá fragmento mostra os seguintes:</span><span class="sxs-lookup"><span data-stu-id="74b9b-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="74b9b-110">Ao iniciar a aplicação de Olá, o tempo de execução Olá lê certificados Olá e gera um ficheiro PFX e a palavra-passe para cada certificado.</span><span class="sxs-lookup"><span data-stu-id="74b9b-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="74b9b-111">Este ficheiro PFX e a palavra-passe estão acessíveis no interior do contentor de Olá utilizando Olá seguintes variáveis de ambiente:</span><span class="sxs-lookup"><span data-stu-id="74b9b-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="74b9b-112">**Certificate_ [CodePackageName] _ [CertName] _PFX**</span><span class="sxs-lookup"><span data-stu-id="74b9b-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="74b9b-113">**Certificate_ [CodePackageName] _ [CertName] _Password**</span><span class="sxs-lookup"><span data-stu-id="74b9b-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="74b9b-114">serviço de contentor Olá ou processo é responsável por importar o ficheiro PFX de Olá para o contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="74b9b-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="74b9b-115">certificado de Olá tooimport, pode utilizar `setupentrypoint.sh` scripts ou executar código personalizado no processo do contentor Olá.</span><span class="sxs-lookup"><span data-stu-id="74b9b-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="74b9b-116">Código de exemplo em c# para importar o ficheiro PFX de Olá segue:</span><span class="sxs-lookup"><span data-stu-id="74b9b-116">Sample code in C# for importing hello PFX file follows:</span></span>

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
<span data-ttu-id="74b9b-117">Este certificado PFX pode ser utilizado para autenticar Olá aplicação ou serviço ou um commmunication segura com outros serviços.</span><span class="sxs-lookup"><span data-stu-id="74b9b-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="74b9b-118">Configurar a gMSA para contentores do Windows</span><span class="sxs-lookup"><span data-stu-id="74b9b-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="74b9b-119">tooset segurança gMSA (grupo de contas de serviço gerida), um ficheiro de especificação de credenciais (`credspec`) é colocada em todos os nós no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="74b9b-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="74b9b-120">ficheiro de Olá pode ser copiado em todos os nós a utilizar uma extensão VM.</span><span class="sxs-lookup"><span data-stu-id="74b9b-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="74b9b-121">Olá `credspec` ficheiro tem de conter as informações da conta gMSA Olá.</span><span class="sxs-lookup"><span data-stu-id="74b9b-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="74b9b-122">Para mais informações sobre Olá `credspec` de ficheiros, consulte [contas de serviço](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="74b9b-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="74b9b-123">especificação de credenciais Olá e Olá `Hostname` etiquetas são especificado no manifesto da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="74b9b-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="74b9b-124">Olá `Hostname` etiquetas tem de corresponder ao nome de conta de gMSA Olá hello é executado de contentor sob.</span><span class="sxs-lookup"><span data-stu-id="74b9b-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="74b9b-125">Olá `Hostname` tag permite Olá contentor tooauthenticate próprio tooother serviços no domínio Olá utilizando a autenticação Kerberos.</span><span class="sxs-lookup"><span data-stu-id="74b9b-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="74b9b-126">Um exemplo sobre como especificar Olá `Hostname` e Olá `credspec` no Olá manifesto da aplicação é apresentado na Olá seguinte fragmento:</span><span class="sxs-lookup"><span data-stu-id="74b9b-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="74b9b-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="74b9b-127">Next steps</span></span>

* [<span data-ttu-id="74b9b-128">Implementar um tooService de contentor do Windows Fabric no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="74b9b-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="74b9b-129">Implementar um tooService de contentor do Docker recursos de infraestrutura no Linux</span><span class="sxs-lookup"><span data-stu-id="74b9b-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
