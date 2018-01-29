---
title: "FAQ e problemas conhecidos com geridos serviço de identidade (MSI) para o Azure Active Directory"
description: "Problemas conhecidos com a identidade de serviço gerida do Azure Active Directory."
services: active-directory
documentationcenter: 
author: BryanLa
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: identity
ms.date: 12/15/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 7a71010567a76569da969db3d53f71535f96f2d0
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/22/2017
---
# <a name="faq-and-known-issues-with-managed-service-identity-msi-for-azure-active-directory"></a>FAQ e problemas conhecidos com geridos serviço de identidade (MSI) para o Azure Active Directory

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

### <a name="does-msi-work-with-azure-cloud-services"></a>MSI funciona com Cloud Services do Azure?

Não, não existem nenhum planos para suportar MSI na Cloud Services do Azure.

### <a name="does-msi-work-with-the-active-directory-authentication-library-adal-or-the-microsoft-authentication-library-msal"></a>MSI funciona com o Active Directory Authentication Library (ADAL) ou a biblioteca de autenticação da Microsoft (MSAL)?

Não, MSI ainda não estiver integrado com o ADAL ou MSAL. Para obter mais informações sobre como adquirir um token MSI utilizando o ponto final de REST do MSI, consulte [como utilizar um Azure VM geridos serviço de identidade (MSI) para a aquisição do token](msi-how-to-use-vm-msi-token.md).

### <a name="what-are-the-supported-linux-distributions"></a>Quais são as distribuições suportadas de Linux?

As distribuições de Linux seguintes suportam MSI: 

- CoreOS Stable
- CentOS 7.1
- VM de RedHat 7.2
- Ubuntu 15.04

Outras distribuições de Linux não são atualmente suportadas e extensão poderá falhar no distribuições não suportadas.

A extensão funciona em CentOS 6.9. No entanto, devido a falta de suporte do sistema no 6.9, a extensão será não automaticamente reiniciar se falhou ou parado. É reiniciado quando a VM for reiniciado. Para reiniciar manualmente a extensão, consulte [como, reiniciar a extensão MSI?](#how-do-you-restart-the-msi-extension)

### <a name="how-do-you-restart-the-msi-extension"></a>Como reiniciar a extensão MSI
No Windows e determinadas versões do Linux, se a extensão é interrompido, o cmdlet seguinte pode ser utilizado para reiniciá-lo manualmente:

```powershell
Set-AzureRmVMExtension -Name <extension name>  -Type <extension Type>  -Location <location> -Publisher Microsoft.ManagedIdentity -VMName <vm name> -ResourceGroupName <resource group name> -ForceRerun <Any string different from any last value used>
```

Em que: 
- Nome da extensão e tipo para o Windows é: ManagedIdentityExtensionForWindows
- Nome da extensão e tipo para Linux é: ManagedIdentityExtensionForLinux

## <a name="known-issues"></a>Problemas conhecidos

### <a name="automation-script-fails-when-attempting-schema-export-for-msi-extension"></a>"Scripts de automatização" Falha ao tentar exportar o esquema de extensão MSI

Quando estiver ativada uma identidade de serviço gerida numa VM, o erro seguinte é apresentado ao tentar utilizar a funcionalidade de "Scripts de automatização" para a VM ou o respetivo grupo de recursos:

![Erro de exportação de scripts de automatização de MSI](~/articles/active-directory/media/msi-known-issues/automation-script-export-error.png)

A extensão de VM de identidade de serviço geridas não suporta atualmente a capacidade para exportar a esquema para um modelo de grupo de recursos. Como resultado, o modelo gerado não mostra os parâmetros de configuração para ativar a identidade de serviço geridas no recurso. Estas secções podem ser adicionadas manualmente, ao seguir os exemplos [configurar uma identidade de serviço geridas da VM utilizando um modelo](msi-qs-configure-template-windows-vm.md).

Quando a funcionalidade de exportação de esquema fica disponível para a extensão de VM de MSI, estas serão listadas no [exportar os grupos de recursos que contêm as extensões de VM](~/articles/virtual-machines/windows/extensions-export-templates.md#supported-virtual-machine-extensions).

### <a name="configuration-blade-does-not-appear-in-the-azure-portal"></a>Painel de configuração não é apresentada no portal do Azure

Se o painel Configuração de VM não aparecer na sua VM, em seguida, MSI não foi ativado no portal na sua região ainda.  Verifique novamente mais tarde.  Também pode ativar MSI para a sua VM utilizando [PowerShell](msi-qs-configure-powershell-windows-vm.md) ou [CLI do Azure](msi-qs-configure-cli-windows-vm.md).

### <a name="cannot-assign-access-to-virtual-machines-in-the-access-control-iam-blade"></a>Não é possível atribuir o acesso às máquinas virtuais no painel de controlo de acesso (IAM)

Se **Máquina Virtual** não aparece no portal do Azure como uma opção para **atribuir acesso** no **controlo de acesso (IAM)** > **adicionar permissões**, em seguida, a identidade de serviço geridas não foi ativada no portal na sua região ainda. Verifique novamente mais tarde.  Pode ainda selecionar a identidade de serviço geridas para a atribuição de função ao pesquisar o Principal de serviço para o MSI.  Introduza o nome da VM no **selecione** campo e o Principal de serviço é apresentada no resultado da pesquisa.

### <a name="vm-fails-to-start-after-being-moved-from-resource-group-or-subscription"></a>VM falha a iniciação após a ser movidos do grupo de recursos ou subscrição

Se mover uma VM no estado de execução, este continua a ser executado durante a mudança. No entanto, após a mudança, se a VM estiver parada e reiniciada, ocorrerá uma falha ao iniciar. Este problema ocorre porque a VM não está a atualizar a referência à identidade do MSI e continua a apontar para, no grupo de recursos antigo.

**Solução** 
 
Acione uma atualização na VM para poder obter valores corretos para o MSI. Pode efetuar uma alteração de propriedade VM para atualizar a referência à identidade do MSI. Por exemplo, pode definir um novo valor de etiqueta na VM com o seguinte comando:

```azurecli-interactive
 az  vm update -n <VM Name> -g <Resource Group> --set tags.fixVM=1
```
 
Este comando define uma nova etiqueta "fixVM" com um valor de 1 na VM. 
 
Ao definir esta propriedade, atualiza a VM com o URI do recurso MSI correto e, em seguida, deve ser capaz de iniciar a VM. 
 
Depois da VM é iniciada, a etiqueta pode ser removida utilizando os seguintes comandos:

```azurecli-interactive
az vm update -n <VM Name> -g <Resource Group> --remove tags.fixVM
```

## <a name="known-issues-with-user-assigned-msi-private-preview-feature"></a>Os problemas conhecidos com o utilizador atribuído MSI *(funcionalidade de pré-visualização privada)*

- A única forma de remover todos os utilizadores atribuídos MSIs ao ativar o sistema atribuída MSI. 
- O aprovisionamento da extensão VM a uma VM pode falhar devido a falhas de pesquisa DNS. Reiniciar a VM e tente novamente. 
- CLI do Azure: `Az resource show` e `Az resource list` irá falhar numa VM com um utilizador atribuído MSI. Como solução, utilize`az vm/vmss show`
- Tutorial de armazenamento do Azure só está disponível no Central nos EUAP neste momento. 
- Quando um MSI atribuído do utilizador é concedido acesso a um recurso, o painel IAM para o recurso de mostra "Não é possível aceder a dados." Como solução, utilize o CLI para ver/editar atribuições de funções para esse recurso.
- Criar um utilizador atribuído MSI com um caráter de sublinhado no nome, não é suportada.
- Quando adicionar um segundo utilizador atribuído a identidade, o clientID poderão não estar disponível para tokens de pedidos para o mesmo. Como uma mitigação, reinicie a extensão de VM de MSI com os seguintes comandos de dois bash:
 - `sudo bash -c "/var/lib/waagent/Microsoft.ManagedIdentity.ManagedIdentityExtensionForLinux-1.0.0.8/msi-extension-handler disable"`
 - `sudo bash -c "/var/lib/waagent/Microsoft.ManagedIdentity.ManagedIdentityExtensionForLinux-1.0.0.8/msi-extension-handler enable"`
- VMAgent no Windows não suporta atualmente utilizador atribuído MSI. 
- Atribuir uma função para um MSI para aceder a um recurso atualmente não necessita de permissões especiais. 
- Quando uma VM tem um utilizador atribuído MSI, mas nenhum sistema atribuída MSI, o portal de IU irá mostrar MSI como ativada. Para ativar o sistema atribuído MSI, utilize um modelo Azure Resource Manager, um CLI do Azure ou um SDK.
