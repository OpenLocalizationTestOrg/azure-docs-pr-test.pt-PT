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
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="af6fb-103">Exemplo de aplicação para utilização com DMZ</span><span class="sxs-lookup"><span data-stu-id="af6fb-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="af6fb-104">[Devolver toohello segurança limites melhores práticas de página][HOME]</span><span class="sxs-lookup"><span data-stu-id="af6fb-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="af6fb-105">Estes scripts do PowerShell podem ser executadas localmente no Olá IIS01 e AppVM01 tooinstall servidores e configurar uma aplicação web simples que apresenta uma página html do servidor de IIS01 front-end Olá com conteúdo do servidor de AppVM01 Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="af6fb-105">These PowerShell scripts can be run locally on hello IIS01 and AppVM01 servers tooinstall and set up a simple web application that displays an html page from hello front-end IIS01 server with content from hello back-end AppVM01 server.</span></span>

<span data-ttu-id="af6fb-106">Esta aplicação fornece um ambiente de teste simples para muitos dos exemplos de rede de Perímetro Olá e como as alterações no Olá pontos finais, NSGs, UDR e regras de Firewall podem afetar os fluxos de tráfego.</span><span class="sxs-lookup"><span data-stu-id="af6fb-106">This application provides a simple testing environment for many of hello DMZ Examples and how changes on hello Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-tooallow-icmp"></a><span data-ttu-id="af6fb-107">Tooallow de regra de firewall ICMP</span><span class="sxs-lookup"><span data-stu-id="af6fb-107">Firewall rule tooallow ICMP</span></span>
<span data-ttu-id="af6fb-108">Esta declaração de PowerShell simple pode ser executada em qualquer tráfego ICMP (Ping) tooallow VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="af6fb-108">This simple PowerShell statement can be run on any Windows VM tooallow ICMP (Ping) traffic.</span></span> <span data-ttu-id="af6fb-109">Esta atualização de firewall permite mais fácil de teste e resolução de problemas, permitindo Olá ping protocolo toopass através da firewall do windows hello (para a maioria das Linux distros que ICMP está ativada por predefinição).</span><span class="sxs-lookup"><span data-stu-id="af6fb-109">This firewall update allows for easier testing and troubleshooting by allowing hello ping protocol toopass through hello windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="af6fb-110">Se utilizar Olá seguintes scripts, esta adição da regra de firewall é a primeira instrução de Olá.</span><span class="sxs-lookup"><span data-stu-id="af6fb-110">If you use hello following scripts, this firewall rule addition is hello first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="af6fb-111">IIS01 - o script de instalação de aplicações Web</span><span class="sxs-lookup"><span data-stu-id="af6fb-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="af6fb-112">Este script irão:</span><span class="sxs-lookup"><span data-stu-id="af6fb-112">This script will:</span></span>

1. <span data-ttu-id="af6fb-113">Abrir IMCPv4 (Ping) na firewall do windows local server Olá para fins de teste mais fácil</span><span class="sxs-lookup"><span data-stu-id="af6fb-113">Open IMCPv4 (Ping) on hello local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="af6fb-114">Instalar o IIS e Olá .net Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="af6fb-114">Install IIS and hello .Net Framework v4.5</span></span>
3. <span data-ttu-id="af6fb-115">Criar uma página web do ASP.NET e Web. config</span><span class="sxs-lookup"><span data-stu-id="af6fb-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="af6fb-116">Alterar Olá predefinido aplicação conjunto toomake acesso a ficheiros mais fácil</span><span class="sxs-lookup"><span data-stu-id="af6fb-116">Change hello Default application pool toomake file access easier</span></span>
5. <span data-ttu-id="af6fb-117">Conta de administrador do conjunto Olá utilizador anónimo tooyour e a palavra-passe</span><span class="sxs-lookup"><span data-stu-id="af6fb-117">Set hello Anonymous user tooyour admin account and password</span></span>

<span data-ttu-id="af6fb-118">Este script do PowerShell deve ser executado localmente enquanto RDP tinha em IIS01.</span><span class="sxs-lookup"><span data-stu-id="af6fb-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

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

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="af6fb-119">AppVM01 - o script de instalação do servidor de ficheiros</span><span class="sxs-lookup"><span data-stu-id="af6fb-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="af6fb-120">Este script configura Olá back-end para esta aplicação simple.</span><span class="sxs-lookup"><span data-stu-id="af6fb-120">This script sets up hello back-end for this simple application.</span></span> <span data-ttu-id="af6fb-121">Este script irão:</span><span class="sxs-lookup"><span data-stu-id="af6fb-121">This script will:</span></span>

1. <span data-ttu-id="af6fb-122">Abrir IMCPv4 (Ping) na firewall de Olá para fins de teste mais fácil</span><span class="sxs-lookup"><span data-stu-id="af6fb-122">Open IMCPv4 (Ping) on hello firewall for easier testing</span></span>
2. <span data-ttu-id="af6fb-123">Criar um diretório para Olá web site</span><span class="sxs-lookup"><span data-stu-id="af6fb-123">Create a directory for hello web site</span></span>
3. <span data-ttu-id="af6fb-124">Criar um toobe do ficheiro de texto remotamente aceder através da página web de Olá</span><span class="sxs-lookup"><span data-stu-id="af6fb-124">Create a text file toobe remotely access by hello web page</span></span>
4. <span data-ttu-id="af6fb-125">Definir as permissões no tooAnonymous de ficheiro e diretório Olá tooallow acesso</span><span class="sxs-lookup"><span data-stu-id="af6fb-125">Set permissions on hello directory and file tooAnonymous tooallow access</span></span>
5. <span data-ttu-id="af6fb-126">Desativar a mais fácil de navegar a partir deste servidor tooallow de segurança avançada do IE</span><span class="sxs-lookup"><span data-stu-id="af6fb-126">Turn off IE Enhanced Security tooallow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="af6fb-127">**Melhor prática**: nunca desativar a segurança avançada do IE num servidor de produção e, normalmente, é uma web de Olá toosurf ideia incorreta de um servidor de produção.</span><span class="sxs-lookup"><span data-stu-id="af6fb-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea toosurf hello web from a production server.</span></span> <span data-ttu-id="af6fb-128">Além disso, a abertura de partilhas de ficheiros para acesso anónimo é incorreto, mas já está aqui de simplicidade.</span><span class="sxs-lookup"><span data-stu-id="af6fb-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="af6fb-129">Este script do PowerShell deve ser executado localmente enquanto RDP tinha em AppVM01.</span><span class="sxs-lookup"><span data-stu-id="af6fb-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="af6fb-130">PowerShell é necessário toobe run a execução do administrador tooensure com êxito.</span><span class="sxs-lookup"><span data-stu-id="af6fb-130">PowerShell is required toobe run as Administrator tooensure successful execution.</span></span>

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

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="af6fb-131">DNS01 - o script de instalação do servidor DNS</span><span class="sxs-lookup"><span data-stu-id="af6fb-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="af6fb-132">Não há nenhum script incluído neste tooset de aplicação de exemplo segurança do servidor de DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="af6fb-132">There is no script included in this sample application tooset up hello DNS server.</span></span> <span data-ttu-id="af6fb-133">Se o teste de regras de firewall de Olá, NSG ou UDR tem tooinclude o tráfego do DNS, servidor de Olá DNS01 tem toobe configurar manualmente.</span><span class="sxs-lookup"><span data-stu-id="af6fb-133">If testing of hello firewall rules, NSG, or UDR needs tooinclude DNS traffic, hello DNS01 server needs toobe set up manually.</span></span> <span data-ttu-id="af6fb-134">ficheiro de xml de configuração de rede de Olá e modelo do Resource Manager para ambos os exemplos incluem DNS01 como servidor DNS primário do Olá e servidor DNS público Olá alojadas pelo nível 3 como servidor DNS de cópia de segurança Olá.</span><span class="sxs-lookup"><span data-stu-id="af6fb-134">hello Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as hello primary DNS server and hello public DNS server hosted by Level 3 as hello backup DNS server.</span></span> <span data-ttu-id="af6fb-135">servidor de nível 3 DNS Olá teria de ser Olá real DNS do servidor utilizado para o tráfego não local e com DNS01 não o programa de configuração, não há redes locais ocorreriam DNS.</span><span class="sxs-lookup"><span data-stu-id="af6fb-135">hello Level 3 DNS server would be hello actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af6fb-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="af6fb-136">Next steps</span></span>
* <span data-ttu-id="af6fb-137">Executar script de IIS01 Olá num servidor de IIS</span><span class="sxs-lookup"><span data-stu-id="af6fb-137">Run hello IIS01 script on an IIS server</span></span>
* <span data-ttu-id="af6fb-138">Executar script de servidor de ficheiros em AppVM01</span><span class="sxs-lookup"><span data-stu-id="af6fb-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="af6fb-139">Procurar toohello IP público na IIS01 toovalidate da compilação</span><span class="sxs-lookup"><span data-stu-id="af6fb-139">Browse toohello Public IP on IIS01 toovalidate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
