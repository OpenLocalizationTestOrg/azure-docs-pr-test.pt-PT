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
# <a name="container-security"></a>Segurança de contentor

O Service Fabric fornece um mecanismo para serviços no interior de um contentor tooaccess um certificado que está instalado em Olá nós num cluster do Windows ou Linux (versão 5.7 ou superior). Além disso, a Service Fabric também suporta a gMSA (grupo contas de serviço geridas) para contentores do Windows. 

## <a name="certificate-management-for-containers"></a>Gestão de certificados para contentores

Pode proteger os serviços de contentor, especificando um certificado. certificado de Olá deve ser instalado em nós de Olá do cluster de Olá. Olá informações do certificado são fornecidas no manifesto da aplicação Olá em Olá `ContainerHostPolicies` etiquetas como Olá fragmento mostra os seguintes:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Ao iniciar a aplicação de Olá, o tempo de execução Olá lê certificados Olá e gera um ficheiro PFX e a palavra-passe para cada certificado. Este ficheiro PFX e a palavra-passe estão acessíveis no interior do contentor de Olá utilizando Olá seguintes variáveis de ambiente: 

* **Certificate_ [CodePackageName] _ [CertName] _PFX**
* **Certificate_ [CodePackageName] _ [CertName] _Password**

serviço de contentor Olá ou processo é responsável por importar o ficheiro PFX de Olá para o contentor de Olá. certificado de Olá tooimport, pode utilizar `setupentrypoint.sh` scripts ou executar código personalizado no processo do contentor Olá. Código de exemplo em c# para importar o ficheiro PFX de Olá segue:

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
Este certificado PFX pode ser utilizado para autenticar Olá aplicação ou serviço ou um commmunication segura com outros serviços.


## <a name="set-up-gmsa-for-windows-containers"></a>Configurar a gMSA para contentores do Windows

tooset segurança gMSA (grupo de contas de serviço gerida), um ficheiro de especificação de credenciais (`credspec`) é colocada em todos os nós no cluster de Olá. ficheiro de Olá pode ser copiado em todos os nós a utilizar uma extensão VM.  Olá `credspec` ficheiro tem de conter as informações da conta gMSA Olá. Para mais informações sobre Olá `credspec` de ficheiros, consulte [contas de serviço](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). especificação de credenciais Olá e Olá `Hostname` etiquetas são especificado no manifesto da aplicação Olá. Olá `Hostname` etiquetas tem de corresponder ao nome de conta de gMSA Olá hello é executado de contentor sob.  Olá `Hostname` tag permite Olá contentor tooauthenticate próprio tooother serviços no domínio Olá utilizando a autenticação Kerberos.  Um exemplo sobre como especificar Olá `Hostname` e Olá `credspec` no Olá manifesto da aplicação é apresentado na Olá seguinte fragmento:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Passos seguintes

* [Implementar um tooService de contentor do Windows Fabric no Windows Server 2016](service-fabric-get-started-containers.md)
* [Implementar um tooService de contentor do Docker recursos de infraestrutura no Linux](service-fabric-get-started-containers-linux.md)
