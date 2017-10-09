---
title: "definições de FabricTransport aaaChange no Azure micro-serviços | Microsoft Docs"
description: "Saiba mais sobre como configurar definições de comunicação de atores do Service Fabric do Azure."
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: e312b475407eb95a435b93d80c0f2e9618b9ea1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="07fd2-103">Configurar as definições de FabricTransport dos Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="07fd2-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="07fd2-104">Seguem-se as definições de Olá que pode configurar:</span><span class="sxs-lookup"><span data-stu-id="07fd2-104">Here are hello settings that you can configure:</span></span>
- <span data-ttu-id="07fd2-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="07fd2-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="07fd2-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="07fd2-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="07fd2-107">Pode modificar a configuração predefinida Olá FabricTransport das seguintes formas.</span><span class="sxs-lookup"><span data-stu-id="07fd2-107">You can modify hello default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="07fd2-108">Atributo de assemblagem</span><span class="sxs-lookup"><span data-stu-id="07fd2-108">Assembly attribute</span></span>

<span data-ttu-id="07fd2-109">Olá [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) atributo necessita toobe aplicado Olá ator cliente e ator serviço assemblagens.</span><span class="sxs-lookup"><span data-stu-id="07fd2-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs toobe applied on hello actor client and actor service assemblies.</span></span>

<span data-ttu-id="07fd2-110">Olá seguinte exemplo mostra como toochange Olá valor predefinido de FabricTransport OperationTimeout definições:</span><span class="sxs-lookup"><span data-stu-id="07fd2-110">hello following example shows how toochange hello default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="07fd2-111">Segundo exemplo alterações predefinido valores de FabricTransport MaxMessageSize e OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="07fd2-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="07fd2-112">Pacote de configuração</span><span class="sxs-lookup"><span data-stu-id="07fd2-112">Config package</span></span>

<span data-ttu-id="07fd2-113">Pode utilizar um [o pacote de configuração](service-fabric-application-model.md) configuração predefinida do toomodify Olá.</span><span class="sxs-lookup"><span data-stu-id="07fd2-113">You can use a [config package](service-fabric-application-model.md) toomodify hello default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-hello-actor-service"></a><span data-ttu-id="07fd2-114">Configurar as definições de FabricTransport para o serviço de atores Olá</span><span class="sxs-lookup"><span data-stu-id="07fd2-114">Configure FabricTransport settings for hello actor service</span></span>

<span data-ttu-id="07fd2-115">Adicione uma secção de TransportSettings no ficheiro de settings.xml Olá.</span><span class="sxs-lookup"><span data-stu-id="07fd2-115">Add a TransportSettings section in hello settings.xml file.</span></span>

<span data-ttu-id="07fd2-116">Por predefinição, o código de ator procura SectionName como "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="07fd2-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="07fd2-117">Se o que não foi encontrada, verifica a existência de SectionName como "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="07fd2-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-hello-actor-client-assembly"></a><span data-ttu-id="07fd2-118">Configurar as definições de FabricTransport para a assemblagem de cliente de ator Olá</span><span class="sxs-lookup"><span data-stu-id="07fd2-118">Configure FabricTransport settings for hello actor client assembly</span></span>

<span data-ttu-id="07fd2-119">Se o cliente de Olá não está em execução como parte de um serviço, pode criar um "&lt;cliente Exe nome&gt;. settings.xml" ficheiros Olá mesma localização do ficheiro de .exe Olá cliente.</span><span class="sxs-lookup"><span data-stu-id="07fd2-119">If hello client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in hello same location as hello client .exe file.</span></span> <span data-ttu-id="07fd2-120">Em seguida, adicione uma secção de TransportSettings nesse ficheiro.</span><span class="sxs-lookup"><span data-stu-id="07fd2-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="07fd2-121">SectionName deve ser "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="07fd2-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="07fd2-122">Configurar definições de FabricTransport de Ator segura/cliente do serviço com o certificado secundário.</span><span class="sxs-lookup"><span data-stu-id="07fd2-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="07fd2-123">As informações do certificado secundário podem ser adicionadas ao adicionar o parâmetro CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="07fd2-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="07fd2-124">Segue-se exemplo Olá Olá TransportSettings do serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="07fd2-124">Below is hello example for hello Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="07fd2-125">Segue-se exemplo Olá Olá TransportSettings de cliente.</span><span class="sxs-lookup"><span data-stu-id="07fd2-125">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="07fd2-126">Configurar definições de FabricTransport para proteger Ator/cliente do serviço com o nome do requerente.</span><span class="sxs-lookup"><span data-stu-id="07fd2-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="07fd2-127">Utilizador necessidades tooprovide findType como FindBySubjectName, adicione os valores CertificateIssuerThumbprints e CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="07fd2-127">User needs tooprovide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="07fd2-128">Segue-se exemplo Olá Olá TransportSettings do serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="07fd2-128">Below is hello example for hello Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="07fd2-129">Segue-se exemplo Olá Olá TransportSettings de cliente.</span><span class="sxs-lookup"><span data-stu-id="07fd2-129">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
