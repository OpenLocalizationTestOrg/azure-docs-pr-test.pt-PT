---
title: 'Gerar e exportar certificados para ponto a Site: PowerShell: Azure | Microsoft Docs'
description: "Este artigo contém passos toocreate um certificado de raiz autoassinado, exportar a chave pública Olá e gerar os certificados de cliente através do PowerShell no Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Gerar e exportar certificados para ligações ponto a Site através do PowerShell no Windows 10

Ligações de ponto a Site utilizam certificados tooauthenticate. Este artigo mostra-lhe como toocreate autoassinado a raiz do certificado e gerar os certificados de cliente através do PowerShell no Windows 10. Se está a procurar passos de configuração de ponto a Site, tais como como certificados de raiz tooupload, selecione um dos artigos Olá ' Configurar ponto a Site' de Olá seguinte listam:

> [!div class="op_single_selector"]
> * [Criar certificados autoassinados - PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Criar certificados autoassinados - MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Configurar o ponto a Site - Resource Manager - portal do Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Configurar o ponto a Site - Gestor de recursos - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Configurar o ponto a Site - Classic - portal do Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


Tem de efetuar os passos de Olá neste artigo num computador com o Windows 10. cmdlets do PowerShell Olá que utilize certificados toogenerate fazem parte do sistema de operativo Olá Windows 10 e não funcionam nas outras versões do Windows. computador Olá Windows 10 é apenas necessário toogenerate Olá certificados. Assim que são gerados certificados Olá, pode carregá-los ou instalá-los em qualquer sistema operativo de cliente suportada. 

Se não tiver o computador do acesso tooa Windows 10, pode utilizar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificados. Olá certificados que geram o utilizando um dos métodos podem ser instalados em qualquer [suportado](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) sistema operativo do cliente.

## <a name="rootcert"></a>Criar um certificado de raiz autoassinado

Utilize Olá SelfSignedCertificate novo cmdlet toocreate um certificado de raiz autoassinado. Para informações de parâmetros adicionais, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. A partir de um computador com o Windows 10, abra uma consola do Windows PowerShell com privilégios elevados.
2. Utilize Olá certificado de raiz autoassinado de Olá de toocreate de exemplo a seguir. Olá exemplo seguinte cria um certificado de raiz autoassinado com o nome 'P2SRootCert', que é instalado automaticamente em 'Certificados atual User\Personal\Certificates'. Pode ver o certificado de Olá abrindo *certmgr.msc*, ou *gerir certificados de utilizador*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Exportar a chave pública de Olá (. cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Olá exported.cer ficheiro tem de ser tooAzure carregado. Para obter instruções, consulte [configurar uma ligação ponto a Site](vpn-gateway-howto-point-to-site-rm-ps.md#upload). tooadd um certificado de raiz fidedigna adicionais, [nesta secção](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) artigo Olá.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Exportar o certificado de raiz autoassinado Olá e toostore de chave pública-(opcional)

Poderá ser útil tooexport Olá um certificado de raiz autoassinado e armazena de forma segura. Se necessário, mais tarde pode instalá-lo noutro computador e gerar mais certificados de cliente ou exportar outro ficheiro. cer. Olá tooexport raiz um certificado autoassinado como uma. pfx, certificado de raiz de Olá selecione e utilize Olá mesmos passos conforme descrito em [exportar um certificado de cliente](#clientexport).

## <a name="clientcert"></a>Gerar um certificado de cliente

Cada computador cliente que liga tooa a VNet com ponto a Site tem de ter um certificado de cliente instalado. Gerar um certificado de cliente a partir do certificado de raiz autoassinado Olá e, em seguida, exportar e instalar o certificado de cliente Olá. Se o certificado de cliente Olá não estiver instalado, a autenticação falha. 

Olá seguintes passos guiá-lo a gerar um certificado de cliente de um certificado de raiz autoassinado. Pode gerar vários certificados de cliente a partir de Olá mesmo certificado de raiz. Ao gerar os certificados de cliente utilizando Olá passos abaixo, o certificado de cliente Olá é automaticamente instalado no computador de Olá que utilizou o certificado de Olá toogenerate. Se quiser tooinstall um certificado de cliente no outro computador cliente, pode exportar o certificado de Olá.

Exemplos de Olá utilizam Olá SelfSignedCertificate novo cmdlet toogenerate um certificado de cliente que expira dentro de um ano. Para informações de parâmetros adicionais, como a definição de um valor diferente de expiração do certificado de cliente Olá, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Exemplo 1

Este exemplo utiliza Olá declarado '$cert' variável da secção anterior Olá. Se fechar a consola do PowerShell Olá depois de criar Olá certificado de raiz autoassinado ou estiver a criar adicionais de cliente certificados numa nova sessão de consola do PowerShell, utilize os passos de Olá em [exemplo 2](#ex2).

Modificar e execute toogenerate de exemplo de Olá um certificado de cliente. Se executar Olá seguinte o exemplo sem modificá-lo, o resultado de Olá é um certificado de cliente com o nome 'P2SChildCert'.  Se pretender que os certificados de subordinados de Olá tooname algo pessoa, modifique o valor CN Olá. Não altere Olá TextExtension quando executar este exemplo. certificado de cliente de Olá gerar é instalado automaticamente nos 'Certificados - User\Personal\Certificates atual' no seu computador.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Exemplo 2

Se estiver a criar adicionais de cliente certificados ou são não utilizar Olá mesmo sessão do PowerShell que utilizou toocreate seu certificado de raiz autoassinado, Olá utilize os seguintes passos:

1. Identifica o certificado de raiz autoassinado Olá que está instalado no computador de Olá. Este cmdlet devolve uma lista de certificados que estão instalados no seu computador.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Localize o nome de requerente Olá de Olá devolvida a lista, em seguida, impressão digital de Olá de cópia é localizado seguinte tooit tooa texto ficheiro. No seguinte exemplo de Olá, existem dois certificados. Olá CN é Olá nome do certificado de raiz autoassinado Olá partir das quais pretende toogenerate um certificado de subordinados. Neste caso, 'P2SRootCert'.

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Declare uma variável para o certificado de raiz de Olá utilizando thumbprint Olá do passo anterior Olá. Substitua o THUMBPRINT com Olá impressão digital do certificado de raiz de Olá partir do qual pretende toogenerate um certificado de subordinados.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Por exemplo, a utilizar o thumbprint Olá para P2SRootCert no passo anterior Olá, variável Olá este aspeto:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Modificar e execute toogenerate de exemplo de Olá um certificado de cliente. Se executar Olá seguinte o exemplo sem modificá-lo, o resultado de Olá é um certificado de cliente com o nome 'P2SChildCert'. Se pretender que os certificados de subordinados de Olá tooname algo pessoa, modifique o valor CN Olá. Não altere Olá TextExtension quando executar este exemplo. certificado de cliente de Olá gerar é instalado automaticamente nos 'Certificados - User\Personal\Certificates atual' no seu computador.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Exportar um certificado de cliente   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Instalar um certificado de cliente exportado

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Passos seguintes

Continue com a sua configuração de ponto a Site. 

* Para **Resource Manager** passos de modelo de implementação, consulte [configurar um tooa de ligação de ponto a Site VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Para **clássico** passos de modelo de implementação, consulte [configurar um tooa de ligação VPN ponto a Site VNet (clássica)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
