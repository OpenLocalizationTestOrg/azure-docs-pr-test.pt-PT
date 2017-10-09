---
title: "aplicação de exemplo aaaAzure para utilização com DMZ | Microsoft Docs"
description: "Implementar esta aplicação web simples depois de criar uma rede de Perímetro tootest cenários de fluxo de tráfego"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a>Exemplo de aplicação para utilização com DMZ
[Devolver toohello segurança limites melhores práticas de página][HOME]

Estes scripts do PowerShell podem ser executadas localmente no Olá IIS01 e AppVM01 tooinstall servidores e configurar uma aplicação web simples que apresenta uma página html do servidor de IIS01 front-end Olá com conteúdo do servidor de AppVM01 Olá back-end.

Esta aplicação fornece um ambiente de teste simples para muitos dos exemplos de rede de Perímetro Olá e como as alterações no Olá pontos finais, NSGs, UDR e regras de Firewall podem afetar os fluxos de tráfego.

## <a name="firewall-rule-tooallow-icmp"></a>Tooallow de regra de firewall ICMP
Esta declaração de PowerShell simple pode ser executada em qualquer tráfego ICMP (Ping) tooallow VM do Windows. Esta atualização de firewall permite mais fácil de teste e resolução de problemas, permitindo Olá ping protocolo toopass através da firewall do windows hello (para a maioria das Linux distros que ICMP está ativada por predefinição).

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

Se utilizar Olá seguintes scripts, esta adição da regra de firewall é a primeira instrução de Olá.

## <a name="iis01---web-application-installation-script"></a>IIS01 - o script de instalação de aplicações Web
Este script irão:

1. Abrir IMCPv4 (Ping) na firewall do windows local server Olá para fins de teste mais fácil
2. Instalar o IIS e Olá .net Framework 4.5
3. Criar uma página web do ASP.NET e Web. config
4. Alterar Olá predefinido aplicação conjunto toomake acesso a ficheiros mais fácil
5. Conta de administrador do conjunto Olá utilizador anónimo tooyour e a palavra-passe

Este script do PowerShell deve ser executado localmente enquanto RDP tinha em IIS01.

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a>AppVM01 - o script de instalação do servidor de ficheiros
Este script configura Olá back-end para esta aplicação simple. Este script irão:

1. Abrir IMCPv4 (Ping) na firewall de Olá para fins de teste mais fácil
2. Criar um diretório para Olá web site
3. Criar um toobe do ficheiro de texto remotamente aceder através da página web de Olá
4. Definir as permissões no tooAnonymous de ficheiro e diretório Olá tooallow acesso
5. Desativar a mais fácil de navegar a partir deste servidor tooallow de segurança avançada do IE 

> [!IMPORTANT]
> **Melhor prática**: nunca desativar a segurança avançada do IE num servidor de produção e, normalmente, é uma web de Olá toosurf ideia incorreta de um servidor de produção. Além disso, a abertura de partilhas de ficheiros para acesso anónimo é incorreto, mas já está aqui de simplicidade.
> 
> 

Este script do PowerShell deve ser executado localmente enquanto RDP tinha em AppVM01. PowerShell é necessário toobe run a execução do administrador tooensure com êxito.

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a>DNS01 - o script de instalação do servidor DNS
Não há nenhum script incluído neste tooset de aplicação de exemplo segurança do servidor de DNS Olá. Se o teste de regras de firewall de Olá, NSG ou UDR tem tooinclude o tráfego do DNS, servidor de Olá DNS01 tem toobe configurar manualmente. ficheiro de xml de configuração de rede de Olá e modelo do Resource Manager para ambos os exemplos incluem DNS01 como servidor DNS primário do Olá e servidor DNS público Olá alojadas pelo nível 3 como servidor DNS de cópia de segurança Olá. servidor de nível 3 DNS Olá teria de ser Olá real DNS do servidor utilizado para o tráfego não local e com DNS01 não o programa de configuração, não há redes locais ocorreriam DNS.

## <a name="next-steps"></a>Passos seguintes
* Executar script de IIS01 Olá num servidor de IIS
* Executar script de servidor de ficheiros em AppVM01
* Procurar toohello IP público na IIS01 toovalidate da compilação

<!--Link References-->
[HOME]: ../best-practices-network-security.md
