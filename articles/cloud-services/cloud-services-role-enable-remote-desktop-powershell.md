---
title: "aaaEnable ligação ao ambiente de trabalho remoto para uma função nos serviços de nuvem do Azure com o PowerShell"
description: "Como tooconfigure do azure na nuvem através de ligações de ambiente de trabalho do PowerShell tooallow remotas de aplicação de serviço"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="5bab5-103">Ativar a ligação de ambiente de trabalho remoto para uma função nos serviços de nuvem do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5bab5-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5bab5-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab5-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="5bab5-105">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab5-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="5bab5-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5bab5-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="5bab5-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5bab5-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="5bab5-108">Ambiente de trabalho remoto permite-lhe o ambiente de trabalho do tooaccess Olá de uma função em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="5bab5-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="5bab5-109">Pode utilizar um tootroubleshoot de ligação de ambiente de trabalho remoto e diagnosticar problemas com a sua aplicação enquanto estiver em execução.</span><span class="sxs-lookup"><span data-stu-id="5bab5-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="5bab5-110">Este artigo descreve como ambiente de trabalho remoto do tooenable nas funções do serviço de nuvem com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5bab5-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="5bab5-111">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para pré-requisitos Olá necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="5bab5-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="5bab5-112">PowerShell utiliza Olá extensão de ambiente de trabalho remoto, pelo que pode ativar o ambiente de trabalho remoto após a implementação da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5bab5-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="5bab5-113">Configurar o ambiente de trabalho remoto a partir do PowerShell</span><span class="sxs-lookup"><span data-stu-id="5bab5-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="5bab5-114">Olá [conjunto AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet permite-lhe tooenable ambiente de trabalho remoto em funções ou especificados todas as funções da sua implementação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5bab5-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="5bab5-115">Olá cmdlet permite-lhe especificar Olá nome de utilizador e palavra-passe para o utilizador ambiente de trabalho remoto através de Olá Olá *credencial* parâmetro aceita um objeto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="5bab5-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="5bab5-116">Se estiver a utilizar interativamente PowerShell, pode facilmente definir dos objetos de PSCredential Olá ao chamar Olá [Get-credenciais](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5bab5-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="5bab5-117">Este comando apresenta uma caixa de diálogo, permitindo-lhe tooenter Olá nome de utilizador e palavra-passe do utilizador remoto Olá de forma segura.</span><span class="sxs-lookup"><span data-stu-id="5bab5-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="5bab5-118">Uma vez que o PowerShell ajuda-o em cenários de automatização, pode também definir Olá **PSCredential** objeto de forma a que não requer interação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="5bab5-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="5bab5-119">Em primeiro lugar, precisa de tooset uma palavra-passe segura.</span><span class="sxs-lookup"><span data-stu-id="5bab5-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="5bab5-120">Começar com a especificação de uma palavra-passe de texto simples, converta-cadeia segura tooa utilizando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bab5-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="5bab5-121">Em seguida precisa tooconvert esta cadeia segura para uma cadeia padrão encriptada utilizando [ConvertFrom SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bab5-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="5bab5-122">Agora pode guardar esta cadeia padrão encriptada tooa ficheiros com [conjunto conteúdo](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bab5-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="5bab5-123">Também pode criar um ficheiro de palavra-passe segura para que não tenham tootype na palavra-passe de Olá sempre.</span><span class="sxs-lookup"><span data-stu-id="5bab5-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="5bab5-124">Além disso, um ficheiro de palavra-passe segura é melhor do que um ficheiro de texto simples.</span><span class="sxs-lookup"><span data-stu-id="5bab5-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="5bab5-125">Utilize Olá PowerShell toocreate um ficheiro de palavra-passe segura os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5bab5-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="5bab5-126">Ao definir a palavra-passe de Olá, certifique-se de que cumpre Olá [requisitos de complexidade](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bab5-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="5bab5-127">objeto de credencial de Olá toocreate do ficheiro de palavra-passe segura Olá, tem de ler o conteúdo do ficheiro Olá e convertê-los back tooa secure cadeia utilizando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bab5-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="5bab5-128">Olá [conjunto AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet também aceita um *expiração* parâmetro, que especifica um **DateTime** pelo utilizador que Olá conta expirar.</span><span class="sxs-lookup"><span data-stu-id="5bab5-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="5bab5-129">Por exemplo, pode configurar Olá conta tooexpire de alguns dias do Olá data e hora atuais.</span><span class="sxs-lookup"><span data-stu-id="5bab5-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="5bab5-130">Neste exemplo do PowerShell mostra como tooset Olá a extensão de ambiente de trabalho remoto num serviço em nuvem:</span><span class="sxs-lookup"><span data-stu-id="5bab5-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="5bab5-131">É também pode especificar opcionalmente o bloco de implementação de Olá e funções de que pretende o ambiente de trabalho remoto tooenable nos.</span><span class="sxs-lookup"><span data-stu-id="5bab5-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="5bab5-132">Estes parâmetros são se não for especificados, Olá cmdlet permite que o ambiente de trabalho remoto em todas as funções no Olá **produção** ranhura de implementação.</span><span class="sxs-lookup"><span data-stu-id="5bab5-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="5bab5-133">Olá extensão de ambiente de trabalho remoto está associado uma implementação.</span><span class="sxs-lookup"><span data-stu-id="5bab5-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="5bab5-134">Se criar uma nova implementação do serviço de Olá, tem de ambiente de trabalho remoto tooenable dessa implementação.</span><span class="sxs-lookup"><span data-stu-id="5bab5-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="5bab5-135">Se quiser sempre toohave ambiente de trabalho remoto ativado, em seguida, deve considerar a integrar scripts do PowerShell Olá em seu fluxo de trabalho de implementação.</span><span class="sxs-lookup"><span data-stu-id="5bab5-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="5bab5-136">Ambiente de trabalho remoto para uma instância de função</span><span class="sxs-lookup"><span data-stu-id="5bab5-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="5bab5-137">Olá [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet é utilizado tooremote ambiente de trabalho para uma instância de função específica do seu serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="5bab5-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="5bab5-138">Pode utilizar Olá *LocalPath* Olá toodownload de parâmetro RDP ficheiro localmente.</span><span class="sxs-lookup"><span data-stu-id="5bab5-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="5bab5-139">Em alternativa, pode utilizar Olá *iniciar* tooaccess de caixa de diálogo de ligação de ambiente de trabalho remoto iniciação Olá parâmetro toodirectly Olá instância de função Serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5bab5-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="5bab5-140">Verifique se a extensão de ambiente de trabalho remoto está ativado num serviço</span><span class="sxs-lookup"><span data-stu-id="5bab5-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="5bab5-141">Olá [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet apresenta que ambiente de trabalho remoto está ativado ou desativado na implementação de serviço.</span><span class="sxs-lookup"><span data-stu-id="5bab5-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="5bab5-142">Olá cmdlet devolve Olá nome de utilizador para o utilizador de ambiente de trabalho remoto Olá e funções de Olá que Olá extensão de ambiente de trabalho remoto está ativada para.</span><span class="sxs-lookup"><span data-stu-id="5bab5-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="5bab5-143">Por predefinição, isto acontece no bloco de implementação de Olá e pode escolher Olá toouse em vez disso, a ranhura de teste.</span><span class="sxs-lookup"><span data-stu-id="5bab5-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="5bab5-144">Remover extensão de ambiente de trabalho remoto a partir de um serviço</span><span class="sxs-lookup"><span data-stu-id="5bab5-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="5bab5-145">Se já tiver ativado a extensão ambiente de trabalho remoto numa implementação Olá, e tem tooupdate Olá as definições de ambiente de trabalho remoto, remova primeiro a extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bab5-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="5bab5-146">E volte a ativá-lo com as novas definições Olá.</span><span class="sxs-lookup"><span data-stu-id="5bab5-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="5bab5-147">Por exemplo, se quiser tooset uma nova palavra-passe para a conta de utilizador remoto Olá ou Olá conta expirou.</span><span class="sxs-lookup"><span data-stu-id="5bab5-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="5bab5-148">Efetuar este procedimento é necessário em implementações existentes que tenham Olá de extensão ambiente de trabalho remoto ativado.</span><span class="sxs-lookup"><span data-stu-id="5bab5-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="5bab5-149">Para novas implementações, pode simplesmente aplicar extensão Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="5bab5-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="5bab5-150">tooremove Olá remoto ambiente de trabalho extensão da implementação de Olá, pode utilizar Olá [remover AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5bab5-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="5bab5-151">Pode também pode especificar opcionalmente o bloco de implementação de Olá e função a partir do qual pretende que a extensão de ambiente de trabalho remoto tooremove Olá.</span><span class="sxs-lookup"><span data-stu-id="5bab5-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="5bab5-152">configuração de extensão do toocompletely remover Olá, deve chamar Olá *remover* cmdlet com Olá **UninstallConfiguration** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="5bab5-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="5bab5-153">Olá **UninstallConfiguration** parâmetro desinstala qualquer configuração de extensão que é aplicado toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="5bab5-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="5bab5-154">Cada configuração da extensão está associada a configuração do serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="5bab5-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="5bab5-155">Chamar Olá *remover* cmdlet sem **UninstallConfiguration** disassociates Olá <mark>implementação</mark> da configuração de extensão de Olá, deste modo, removendo efetivamente extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="5bab5-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="5bab5-156">No entanto, a configuração da extensão Olá permanece associada ao serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="5bab5-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="5bab5-157">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5bab5-157">Additional resources</span></span>

<span data-ttu-id="5bab5-158">[Como tooConfigure serviços em nuvem](cloud-services-how-to-configure.md)
[Cloud services FAQ – ambiente de trabalho remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="5bab5-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
