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
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>Ativar a ligação de ambiente de trabalho remoto para uma função nos serviços de nuvem do Azure com o PowerShell
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portal Clássico do Azure](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Ambiente de trabalho remoto permite-lhe o ambiente de trabalho do tooaccess Olá de uma função em execução no Azure. Pode utilizar um tootroubleshoot de ligação de ambiente de trabalho remoto e diagnosticar problemas com a sua aplicação enquanto estiver em execução.

Este artigo descreve como ambiente de trabalho remoto do tooenable nas funções do serviço de nuvem com o PowerShell. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para pré-requisitos Olá necessários para este artigo. PowerShell utiliza Olá extensão de ambiente de trabalho remoto, pelo que pode ativar o ambiente de trabalho remoto após a implementação da aplicação Olá.

## <a name="configure-remote-desktop-from-powershell"></a>Configurar o ambiente de trabalho remoto a partir do PowerShell
Olá [conjunto AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet permite-lhe tooenable ambiente de trabalho remoto em funções ou especificados todas as funções da sua implementação do serviço de nuvem. Olá cmdlet permite-lhe especificar Olá nome de utilizador e palavra-passe para o utilizador ambiente de trabalho remoto através de Olá Olá *credencial* parâmetro aceita um objeto PSCredential.

Se estiver a utilizar interativamente PowerShell, pode facilmente definir dos objetos de PSCredential Olá ao chamar Olá [Get-credenciais](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

```
$remoteusercredentials = Get-Credential
```

Este comando apresenta uma caixa de diálogo, permitindo-lhe tooenter Olá nome de utilizador e palavra-passe do utilizador remoto Olá de forma segura.

Uma vez que o PowerShell ajuda-o em cenários de automatização, pode também definir Olá **PSCredential** objeto de forma a que não requer interação do utilizador. Em primeiro lugar, precisa de tooset uma palavra-passe segura. Começar com a especificação de uma palavra-passe de texto simples, converta-cadeia segura tooa utilizando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). Em seguida precisa tooconvert esta cadeia segura para uma cadeia padrão encriptada utilizando [ConvertFrom SecureString](https://technet.microsoft.com/library/hh849814.aspx). Agora pode guardar esta cadeia padrão encriptada tooa ficheiros com [conjunto conteúdo](https://technet.microsoft.com/library/ee176959.aspx).

Também pode criar um ficheiro de palavra-passe segura para que não tenham tootype na palavra-passe de Olá sempre. Além disso, um ficheiro de palavra-passe segura é melhor do que um ficheiro de texto simples. Utilize Olá PowerShell toocreate um ficheiro de palavra-passe segura os seguintes:

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Ao definir a palavra-passe de Olá, certifique-se de que cumpre Olá [requisitos de complexidade](https://technet.microsoft.com/library/cc786468.aspx).
>
>

objeto de credencial de Olá toocreate do ficheiro de palavra-passe segura Olá, tem de ler o conteúdo do ficheiro Olá e convertê-los back tooa secure cadeia utilizando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Olá [conjunto AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet também aceita um *expiração* parâmetro, que especifica um **DateTime** pelo utilizador que Olá conta expirar. Por exemplo, pode configurar Olá conta tooexpire de alguns dias do Olá data e hora atuais.

Neste exemplo do PowerShell mostra como tooset Olá a extensão de ambiente de trabalho remoto num serviço em nuvem:

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
É também pode especificar opcionalmente o bloco de implementação de Olá e funções de que pretende o ambiente de trabalho remoto tooenable nos. Estes parâmetros são se não for especificados, Olá cmdlet permite que o ambiente de trabalho remoto em todas as funções no Olá **produção** ranhura de implementação.

Olá extensão de ambiente de trabalho remoto está associado uma implementação. Se criar uma nova implementação do serviço de Olá, tem de ambiente de trabalho remoto tooenable dessa implementação. Se quiser sempre toohave ambiente de trabalho remoto ativado, em seguida, deve considerar a integrar scripts do PowerShell Olá em seu fluxo de trabalho de implementação.

## <a name="remote-desktop-into-a-role-instance"></a>Ambiente de trabalho remoto para uma instância de função
Olá [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet é utilizado tooremote ambiente de trabalho para uma instância de função específica do seu serviço em nuvem. Pode utilizar Olá *LocalPath* Olá toodownload de parâmetro RDP ficheiro localmente. Em alternativa, pode utilizar Olá *iniciar* tooaccess de caixa de diálogo de ligação de ambiente de trabalho remoto iniciação Olá parâmetro toodirectly Olá instância de função Serviço de nuvem.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Verifique se a extensão de ambiente de trabalho remoto está ativado num serviço
Olá [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet apresenta que ambiente de trabalho remoto está ativado ou desativado na implementação de serviço. Olá cmdlet devolve Olá nome de utilizador para o utilizador de ambiente de trabalho remoto Olá e funções de Olá que Olá extensão de ambiente de trabalho remoto está ativada para. Por predefinição, isto acontece no bloco de implementação de Olá e pode escolher Olá toouse em vez disso, a ranhura de teste.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Remover extensão de ambiente de trabalho remoto a partir de um serviço
Se já tiver ativado a extensão ambiente de trabalho remoto numa implementação Olá, e tem tooupdate Olá as definições de ambiente de trabalho remoto, remova primeiro a extensão de Olá. E volte a ativá-lo com as novas definições Olá. Por exemplo, se quiser tooset uma nova palavra-passe para a conta de utilizador remoto Olá ou Olá conta expirou. Efetuar este procedimento é necessário em implementações existentes que tenham Olá de extensão ambiente de trabalho remoto ativado. Para novas implementações, pode simplesmente aplicar extensão Olá diretamente.

tooremove Olá remoto ambiente de trabalho extensão da implementação de Olá, pode utilizar Olá [remover AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet. Pode também pode especificar opcionalmente o bloco de implementação de Olá e função a partir do qual pretende que a extensão de ambiente de trabalho remoto tooremove Olá.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> configuração de extensão do toocompletely remover Olá, deve chamar Olá *remover* cmdlet com Olá **UninstallConfiguration** parâmetro.
>
> Olá **UninstallConfiguration** parâmetro desinstala qualquer configuração de extensão que é aplicado toohello serviço. Cada configuração da extensão está associada a configuração do serviço Olá. Chamar Olá *remover* cmdlet sem **UninstallConfiguration** disassociates Olá <mark>implementação</mark> da configuração de extensão de Olá, deste modo, removendo efetivamente extensão de Olá. No entanto, a configuração da extensão Olá permanece associada ao serviço Olá.
>
>

## <a name="additional-resources"></a>Recursos adicionais

[Como tooConfigure serviços em nuvem](cloud-services-how-to-configure.md)
[Cloud services FAQ – ambiente de trabalho remoto](cloud-services-faq.md)
