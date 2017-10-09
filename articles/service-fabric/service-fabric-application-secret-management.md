---
title: "aaaManaging segredos em aplicações de Service Fabric | Microsoft Docs"
description: "Este artigo descreve como segredo toosecure valores numa aplicação de Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="23853-103">Gerir os segredos em aplicações de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="23853-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="23853-104">Este guia explica Olá passos de gestão de segredos numa aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="23853-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="23853-105">Os segredos podem ser qualquer informações confidenciais, tais como cadeias de ligação de armazenamento, as palavras-passe ou outros valores que não devem ser processados em texto simples.</span><span class="sxs-lookup"><span data-stu-id="23853-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="23853-106">Este guia utiliza o Cofre de chaves do Azure toomanage chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="23853-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="23853-107">No entanto, *utilizando* segredos de uma aplicação é o cluster de tooa implementada na nuvem plataforma agnóstico tooallow aplicações toobe alojadas em qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="23853-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="23853-108">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="23853-108">Overview</span></span>
<span data-ttu-id="23853-109">Olá definições de configuração do serviço de toomanage de forma recomendada é efetuada através de [pacotes de configuração do serviço][config-package].</span><span class="sxs-lookup"><span data-stu-id="23853-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="23853-110">Pacotes de configuração são com versão e atualizável através de atualizações graduais geridas com a reversão da validação do Estado de funcionamento e o automático.</span><span class="sxs-lookup"><span data-stu-id="23853-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="23853-111">Esta é configuração tooglobal preferencial que reduz as possibilidades de Olá de uma interrupção do serviço global.</span><span class="sxs-lookup"><span data-stu-id="23853-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="23853-112">Os segredos encriptados são sem exceção.</span><span class="sxs-lookup"><span data-stu-id="23853-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="23853-113">Service Fabric tem funções incorporadas para encriptar e desencriptar valores num ficheiro de Settings.xml pacote configuração utilizando a encriptação do certificado.</span><span class="sxs-lookup"><span data-stu-id="23853-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="23853-114">Olá diagrama seguinte ilustra Olá fluxo básico para a gestão secreta numa aplicação de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="23853-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![Descrição geral da gestão secreta][overview]

<span data-ttu-id="23853-116">Existem quatro passos principais deste fluxo:</span><span class="sxs-lookup"><span data-stu-id="23853-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="23853-117">Obter um certificado de encriptação de dados.</span><span class="sxs-lookup"><span data-stu-id="23853-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="23853-118">Instale o certificado de Olá no seu cluster.</span><span class="sxs-lookup"><span data-stu-id="23853-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="23853-119">Encriptar o segredo valores quando implementar uma aplicação com o certificado de Olá e inseri-los no ficheiro de configuração de Settings.xml de um serviço.</span><span class="sxs-lookup"><span data-stu-id="23853-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="23853-120">Valores de leitura encriptado fora Settings.xml ao desencriptar com Olá mesmo certificado de encriptação.</span><span class="sxs-lookup"><span data-stu-id="23853-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="23853-121">[O Cofre de chaves do Azure] [ key-vault-get-started] é aqui utilizada como uma localização de armazenamento seguro para certificados e como uma forma tooget certificados instalados em clusters de Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="23853-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="23853-122">Se não estiver a implementar tooAzure, não terá de segredos de toomanage toouse Cofre de chaves em aplicações de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="23853-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="23853-123">Certificado de encriptação de dados</span><span class="sxs-lookup"><span data-stu-id="23853-123">Data encipherment certificate</span></span>
<span data-ttu-id="23853-124">Um certificado de encriptação de dados é utilizado estritamente para a encriptação e desencriptação da configuração de valores em Settings.xml de um serviço e não é utilizado para autenticação ou assinatura de texto de cifra.</span><span class="sxs-lookup"><span data-stu-id="23853-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="23853-125">certificado Olá tem de cumprir os requisitos de Olá:</span><span class="sxs-lookup"><span data-stu-id="23853-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="23853-126">certificado de Olá tem de conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="23853-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="23853-127">certificado de Olá tem de ser criado para a troca de chaves, tooa exportável ficheiro Personal Information Exchange (. pfx).</span><span class="sxs-lookup"><span data-stu-id="23853-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="23853-128">utilização de chave do certificado de Olá tem de incluir a encriptação de dados (10) e não deve incluir a autenticação de servidor ou a autenticação de cliente.</span><span class="sxs-lookup"><span data-stu-id="23853-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="23853-129">Por exemplo, quando criar um certificado autoassinado com o PowerShell, Olá `KeyUsage` sinalizador deve ser definido demasiado`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="23853-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="23853-130">Instalar o certificado de Olá do cluster</span><span class="sxs-lookup"><span data-stu-id="23853-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="23853-131">Este certificado tem de ser instalado em cada nó no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="23853-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="23853-132">Será utilizado no tempo de execução toodecrypt valores armazenados em Settings.xml de um serviço.</span><span class="sxs-lookup"><span data-stu-id="23853-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="23853-133">Consulte [como toocreate um cluster com o Azure Resource Manager] [ service-fabric-cluster-creation-via-arm] para obter instruções de configuração.</span><span class="sxs-lookup"><span data-stu-id="23853-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="23853-134">Encriptar os segredos de aplicação</span><span class="sxs-lookup"><span data-stu-id="23853-134">Encrypt application secrets</span></span>
<span data-ttu-id="23853-135">Olá SDK de Service Fabric tem funções incorporadas de encriptação e desencriptação de secretas.</span><span class="sxs-lookup"><span data-stu-id="23853-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="23853-136">Segredo valores podem ser encriptados durante a incorporada e, em seguida, desencriptados e ler programaticamente com código do serviço.</span><span class="sxs-lookup"><span data-stu-id="23853-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="23853-137">Olá seguinte comando do PowerShell é utilizado tooencrypt um segredo.</span><span class="sxs-lookup"><span data-stu-id="23853-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="23853-138">Este comando só encripta value Olá; faz **não** assinar texto de cifra Olá.</span><span class="sxs-lookup"><span data-stu-id="23853-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="23853-139">Tem de utilizar Olá mesmo certificado de encriptação está instalado no seu ficheiro de encriptação de tooproduce de cluster para os valores de segredos:</span><span class="sxs-lookup"><span data-stu-id="23853-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="23853-140">Olá resultante base-64 cadeia contém o ficheiro de encriptação secreta Olá, bem como informações sobre Olá certificado que foi utilizado tooencrypt-lo.</span><span class="sxs-lookup"><span data-stu-id="23853-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="23853-141">Olá cadeia com codificação base 64 pode ser inserida no parâmetro no ficheiro de configuração do seu serviço Settings.xml com Olá `IsEncrypted` atributo definido demasiado`true`:</span><span class="sxs-lookup"><span data-stu-id="23853-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="23853-142">Inserir segredos de aplicação no instâncias da aplicação</span><span class="sxs-lookup"><span data-stu-id="23853-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="23853-143">Idealmente, ambientes de toodifferent implementação devem ser como automatizadas quanto possível.</span><span class="sxs-lookup"><span data-stu-id="23853-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="23853-144">Isto pode ser efetuado ao efetuar a encriptação secreta num ambiente de compilação e fornecer segredos Olá encriptada como parâmetros ao criar instâncias da aplicação.</span><span class="sxs-lookup"><span data-stu-id="23853-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="23853-145">Utilizar parâmetros substituíveis em Settings.xml</span><span class="sxs-lookup"><span data-stu-id="23853-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="23853-146">ficheiro de configuração de Settings.xml Olá permite substituíveis parâmetros que podem ser fornecidos no momento de criação de aplicações.</span><span class="sxs-lookup"><span data-stu-id="23853-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="23853-147">Olá utilize `MustOverride` atributo em vez de fornecer um valor para um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="23853-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="23853-148">valores de toooverride em Settings.xml, declare um parâmetro de substituição para o serviço de Olá no ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="23853-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

<span data-ttu-id="23853-149">Agora pode ser especificado o valor de Olá como um *parâmetro de aplicação* quando criar uma instância da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="23853-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="23853-150">Criar uma instância de aplicação pode ser convertidos em script com o PowerShell, ou escrito em c#, para integração fácil num processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="23853-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="23853-151">Utilizar o PowerShell, o parâmetro de Olá é fornecido toohello `New-ServiceFabricApplication` comando como um [tabela hash](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="23853-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="23853-152">Parâmetros de aplicação com c#, estão especificados num `ApplicationDescription` como um `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="23853-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="23853-153">Desencriptar segredos do código do serviço</span><span class="sxs-lookup"><span data-stu-id="23853-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="23853-154">Serviços de no Service Fabric são executados ao abrigo do serviço de rede por predefinição no Windows e não tem acesso toocertificates instalado no nó de Olá sem alguma configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="23853-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="23853-155">Quando utilizar um certificado de encriptação de dados, terá de toomake se de que o serviço de rede ou de qualquer serviço de Olá de conta de utilizador está a ser executado não tem chave privada do certificado toohello acesso.</span><span class="sxs-lookup"><span data-stu-id="23853-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="23853-156">Service Fabric processará conceder acesso para o seu serviço automaticamente se configurar toodo por isso.</span><span class="sxs-lookup"><span data-stu-id="23853-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="23853-157">Esta configuração pode ser efetuada no ApplicationManifest.xml definir utilizadores e as políticas de segurança para os certificados.</span><span class="sxs-lookup"><span data-stu-id="23853-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="23853-158">No seguinte exemplo de Olá, Olá conta de serviço de rede é dado acesso de leitura tooa certificado definido pelo respetivo thumbprint:</span><span class="sxs-lookup"><span data-stu-id="23853-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> <span data-ttu-id="23853-159">Quando copiar um thumbprint de certificado do certificado de Olá arquivo snap-in no Windows, um caráter invisível é colocado no início de Olá da cadeia de thumbprint Olá.</span><span class="sxs-lookup"><span data-stu-id="23853-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="23853-160">Este caráter invisível pode originar um erro quando tenta toolocate um certificado por thumbprint, por isso ser toodelete se este caráter adicional.</span><span class="sxs-lookup"><span data-stu-id="23853-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="23853-161">Utilizar segredos de aplicação com código do serviço</span><span class="sxs-lookup"><span data-stu-id="23853-161">Use application secrets in service code</span></span>
<span data-ttu-id="23853-162">Olá API para aceder aos valores de configuração de Settings.xml num pacote de configuração permite a fácil de desencriptação de valores que tenham Olá `IsEncrypted` atributo definido demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="23853-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="23853-163">Uma vez que o texto de Olá encriptado contém informações sobre Olá certificado utilizado para encriptação, não precisa de certificado de Olá toomanually localizar.</span><span class="sxs-lookup"><span data-stu-id="23853-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="23853-164">Olá apenas tem de certificado toobe instalado no nó de Olá Olá serviço está em execução.</span><span class="sxs-lookup"><span data-stu-id="23853-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="23853-165">Chamar simplesmente Olá `DecryptValue()` método tooretrieve Olá secreta valor original:</span><span class="sxs-lookup"><span data-stu-id="23853-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="23853-166">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="23853-166">Next Steps</span></span>
<span data-ttu-id="23853-167">Saiba mais sobre [aplicações em execução com permissões de segurança diferentes](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="23853-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
