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
# <a name="managing-secrets-in-service-fabric-applications"></a>Gerir os segredos em aplicações de Service Fabric
Este guia explica Olá passos de gestão de segredos numa aplicação de Service Fabric. Os segredos podem ser qualquer informações confidenciais, tais como cadeias de ligação de armazenamento, as palavras-passe ou outros valores que não devem ser processados em texto simples.

Este guia utiliza o Cofre de chaves do Azure toomanage chaves e segredos. No entanto, *utilizando* segredos de uma aplicação é o cluster de tooa implementada na nuvem plataforma agnóstico tooallow aplicações toobe alojadas em qualquer lugar. 

## <a name="overview"></a>Descrição geral
Olá definições de configuração do serviço de toomanage de forma recomendada é efetuada através de [pacotes de configuração do serviço][config-package]. Pacotes de configuração são com versão e atualizável através de atualizações graduais geridas com a reversão da validação do Estado de funcionamento e o automático. Esta é configuração tooglobal preferencial que reduz as possibilidades de Olá de uma interrupção do serviço global. Os segredos encriptados são sem exceção. Service Fabric tem funções incorporadas para encriptar e desencriptar valores num ficheiro de Settings.xml pacote configuração utilizando a encriptação do certificado.

Olá diagrama seguinte ilustra Olá fluxo básico para a gestão secreta numa aplicação de Service Fabric:

![Descrição geral da gestão secreta][overview]

Existem quatro passos principais deste fluxo:

1. Obter um certificado de encriptação de dados.
2. Instale o certificado de Olá no seu cluster.
3. Encriptar o segredo valores quando implementar uma aplicação com o certificado de Olá e inseri-los no ficheiro de configuração de Settings.xml de um serviço.
4. Valores de leitura encriptado fora Settings.xml ao desencriptar com Olá mesmo certificado de encriptação. 

[O Cofre de chaves do Azure] [ key-vault-get-started] é aqui utilizada como uma localização de armazenamento seguro para certificados e como uma forma tooget certificados instalados em clusters de Service Fabric no Azure. Se não estiver a implementar tooAzure, não terá de segredos de toomanage toouse Cofre de chaves em aplicações de Service Fabric.

## <a name="data-encipherment-certificate"></a>Certificado de encriptação de dados
Um certificado de encriptação de dados é utilizado estritamente para a encriptação e desencriptação da configuração de valores em Settings.xml de um serviço e não é utilizado para autenticação ou assinatura de texto de cifra. certificado Olá tem de cumprir os requisitos de Olá:

* certificado de Olá tem de conter uma chave privada.
* certificado de Olá tem de ser criado para a troca de chaves, tooa exportável ficheiro Personal Information Exchange (. pfx).
* utilização de chave do certificado de Olá tem de incluir a encriptação de dados (10) e não deve incluir a autenticação de servidor ou a autenticação de cliente. 
  
  Por exemplo, quando criar um certificado autoassinado com o PowerShell, Olá `KeyUsage` sinalizador deve ser definido demasiado`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Instalar o certificado de Olá do cluster
Este certificado tem de ser instalado em cada nó no cluster de Olá. Será utilizado no tempo de execução toodecrypt valores armazenados em Settings.xml de um serviço. Consulte [como toocreate um cluster com o Azure Resource Manager] [ service-fabric-cluster-creation-via-arm] para obter instruções de configuração. 

## <a name="encrypt-application-secrets"></a>Encriptar os segredos de aplicação
Olá SDK de Service Fabric tem funções incorporadas de encriptação e desencriptação de secretas. Segredo valores podem ser encriptados durante a incorporada e, em seguida, desencriptados e ler programaticamente com código do serviço. 

Olá seguinte comando do PowerShell é utilizado tooencrypt um segredo. Este comando só encripta value Olá; faz **não** assinar texto de cifra Olá. Tem de utilizar Olá mesmo certificado de encriptação está instalado no seu ficheiro de encriptação de tooproduce de cluster para os valores de segredos:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Olá resultante base-64 cadeia contém o ficheiro de encriptação secreta Olá, bem como informações sobre Olá certificado que foi utilizado tooencrypt-lo.  Olá cadeia com codificação base 64 pode ser inserida no parâmetro no ficheiro de configuração do seu serviço Settings.xml com Olá `IsEncrypted` atributo definido demasiado`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Inserir segredos de aplicação no instâncias da aplicação
Idealmente, ambientes de toodifferent implementação devem ser como automatizadas quanto possível. Isto pode ser efetuado ao efetuar a encriptação secreta num ambiente de compilação e fornecer segredos Olá encriptada como parâmetros ao criar instâncias da aplicação.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Utilizar parâmetros substituíveis em Settings.xml
ficheiro de configuração de Settings.xml Olá permite substituíveis parâmetros que podem ser fornecidos no momento de criação de aplicações. Olá utilize `MustOverride` atributo em vez de fornecer um valor para um parâmetro:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

valores de toooverride em Settings.xml, declare um parâmetro de substituição para o serviço de Olá no ApplicationManifest.xml:

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

Agora pode ser especificado o valor de Olá como um *parâmetro de aplicação* quando criar uma instância da aplicação Olá. Criar uma instância de aplicação pode ser convertidos em script com o PowerShell, ou escrito em c#, para integração fácil num processo de compilação.

Utilizar o PowerShell, o parâmetro de Olá é fornecido toohello `New-ServiceFabricApplication` comando como um [tabela hash](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

Parâmetros de aplicação com c#, estão especificados num `ApplicationDescription` como um `NameValueCollection`:

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

## <a name="decrypt-secrets-from-service-code"></a>Desencriptar segredos do código do serviço
Serviços de no Service Fabric são executados ao abrigo do serviço de rede por predefinição no Windows e não tem acesso toocertificates instalado no nó de Olá sem alguma configuração adicional.

Quando utilizar um certificado de encriptação de dados, terá de toomake se de que o serviço de rede ou de qualquer serviço de Olá de conta de utilizador está a ser executado não tem chave privada do certificado toohello acesso. Service Fabric processará conceder acesso para o seu serviço automaticamente se configurar toodo por isso. Esta configuração pode ser efetuada no ApplicationManifest.xml definir utilizadores e as políticas de segurança para os certificados. No seguinte exemplo de Olá, Olá conta de serviço de rede é dado acesso de leitura tooa certificado definido pelo respetivo thumbprint:

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
> Quando copiar um thumbprint de certificado do certificado de Olá arquivo snap-in no Windows, um caráter invisível é colocado no início de Olá da cadeia de thumbprint Olá. Este caráter invisível pode originar um erro quando tenta toolocate um certificado por thumbprint, por isso ser toodelete se este caráter adicional.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Utilizar segredos de aplicação com código do serviço
Olá API para aceder aos valores de configuração de Settings.xml num pacote de configuração permite a fácil de desencriptação de valores que tenham Olá `IsEncrypted` atributo definido demasiado`true`. Uma vez que o texto de Olá encriptado contém informações sobre Olá certificado utilizado para encriptação, não precisa de certificado de Olá toomanually localizar. Olá apenas tem de certificado toobe instalado no nó de Olá Olá serviço está em execução. Chamar simplesmente Olá `DecryptValue()` método tooretrieve Olá secreta valor original:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Passos Seguintes
Saiba mais sobre [aplicações em execução com permissões de segurança diferentes](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
