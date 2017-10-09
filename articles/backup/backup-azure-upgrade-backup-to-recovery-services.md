---
title: "aaaUpgrade um cofre de serviços de recuperação de tooa de Cofre de cópia de segurança (pré-visualização) | Microsoft Docs"
description: "As instruções e tooupgrade de informações de suporte a cópia de segurança do Azure cofre tooa cofre dos serviços de recuperação."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>Atualizar um cofre de serviços de recuperação de tooa de Cofre de cópia de segurança

Este artigo explica como tooupgrade um cofre de cópia de segurança dos serviços de recuperação tooa do cofre. processo de atualização de Olá não afeta quaisquer tarefas de cópia de segurança está em execução e não se tenha perdido nenhum dado cópia de segurança. Olá principal motivos pelos quais tooupgrade um tooa do Cofre de cópia de segurança do cofre dos serviços de recuperação:
- Todas as funcionalidades de um cofre de cópia de segurança são mantidas num cofre dos serviços de recuperação.
- Os cofres dos serviços de recuperação tem mais funcionalidades do que cofres de cópia de segurança, incluindo: melhor monitorização de segurança, integrada, restauros mais rápidos e restauros ao nível do item.
- Gerir itens de cópia de segurança a partir de um portal melhorado, simplificado.
- Novas funcionalidades só se aplicam os cofres dos serviços de tooRecovery.

## <a name="impact-toooperations-during-upgrade"></a>Impacto toooperations durante a atualização

Ao atualizar um cofre de serviços de recuperação de tooa de Cofre de cópia de segurança, há nenhum impacto sobre operações de plane tooyour dados. Todas as tarefas de cópia de segurança continuar como normal e quaisquer tarefas de restauro ativa continuar sem interrupção. Durante a atualização de Olá, operações de gestão cobrado um curto período de indisponibilidade e não é possível proteger novos itens ou criar adhoc tarefas de cópias de segurança. Não executam as tarefas de restauro para VMs de IaaS durante a atualização de Olá. atualização do Cofre de Olá demora em toocomplete uma hora. Depois de terminar, um cofre dos serviços de recuperação substitui o Cofre de cópia de segurança de Olá.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>As alterações tooyour automatização e a ferramenta após a atualização

Durante a preparação da sua infraestrutura de atualização de cofre Olá, tem de atualizar a automatização existente ou as ferramentas tooensure que continua toowork após a atualização de Olá.
Consulte as referências de cmdlets do PowerShell Olá para Olá [modelo de implementação do Service Manager](backup-client-automation-classic.md) e Olá [modelo de implementação do Resource Manager](backup-client-automation.md).


## <a name="before-you-upgrade"></a>Antes da atualização

Verifique o seguinte Olá problemas antes de atualizar os cofres de cópia de segurança tooRecovery cofres de serviço.

- **Versão do agente mínimo**: tooupgrade o cofre, o agente de serviços de recuperação do Azure (MARS) da Microsoft do disponibilizar se Olá é, pelo menos, versão 2.0.9070.0. Se o agente MARS Olá é anterior ao 2.0.9070.0, atualize o agente de Olá antes de iniciar o processo de atualização de Olá.
- **Modelo de faturação baseada na instância**: cofres de serviço de recuperação suportam apenas o modelo de faturação baseada na instância de Olá. Se tiver um cofre de cópia de segurança que está a utilizar Olá mais antigo armazenamento com base no modelo de faturação, converter o modelo de faturação Olá durante a atualização.
- **Não existem operações de configuração de cópia de segurança em curso**: durante a atualização, plane de gestão do acesso toohello é restrito. Conclua todas as ações de plane de gestão e, em seguida, iniciar a atualização de Olá.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>Utilizando os cofres de tooupgrade de scripts do PowerShell

Pode utilizar tooupgrade de scripts do PowerShell a cópia de segurança cofres dos cofres dos serviços de tooRecovery. Verifique se tem Olá necessário PowerShell componentes tootrigger Olá cofre a atualização. Scripts do PowerShell para cofres de cópia de segurança não funcionam para cofres dos serviços de recuperação. Prepare o ambiente de cofres de Olá tooupgrade:

1. Instalar ou atualizar [Windows Management Framework (WMF) tooversion 5](https://www.microsoft.com/download/details.aspx?id=50395) ou superior.
2. [Instalar o Azure PowerShell MSI](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi).
3. Transferir Olá [script do PowerShell](https://aka.ms/vaultupgradescript2) tooupgrade os cofres.

### <a name="run-hello-powershell-script"></a>Executar script do PowerShell Olá

Utilize Olá script seguinte tooupgrade os cofres. Olá seguinte script de exemplo tem uma explicação dos parâmetros de Olá.

RecoveryServicesVaultUpgrade 1.0.2.ps1 **- SubscriptionID** `<subscriptionID>` **- VaultName** `<vaultname>` **-localização** `<location>` **- ResourceType** `BackupVault` **- TargetResourceGroupName**`<rgname>`

**SubscriptionID** -Olá número de ID de subscrição do Cofre de Olá que está a ser atualizado.<br/>
**VaultName** - hello nome do Cofre de cópia de segurança de Olá que está a ser atualizado.<br/>
**Localização** -localização do Cofre de Olá a ser atualizado.<br/>
**ResourceType** -utilizar BackupVault.<br/>
**TargetResourceGroupName** - uma vez que estiver a atualizar Olá cofre tooa com base no Gestor de recursos de implementação, especifique um grupo de recursos. Pode utilizar um grupo de recursos existente ou criar um, fornecendo um nome novo. Se misspell nome Olá de um grupo de recursos, pode criar um novo grupo de recursos. toolearn mais informações sobre grupos de recursos, leia este [descrição geral sobre grupos de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups).

>[!NOTE]
> Os nomes de grupo de recursos ter restrições. Ser se toofollow Olá documentação de orientação; Falha toodo, por isso, pode causar toofail de atualizações do cofre.
>
>

Olá seguinte fragmento de código é um exemplo de que o comando do PowerShell deve ter o seguinte aspeto:

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

Também pode executar o script de Olá sem quaisquer parâmetros e é-lhe perguntado tooprovide entradas para todos os parâmetros necessários.

Olá script do PowerShell pede-lhe tooenter as suas credenciais. Introduza as suas credenciais duas vezes: uma vez para a conta do Service Manager Olá e uma segunda vez para Olá conta de Gestor de recursos.

### <a name="pre-requisites-checking"></a>A verificação de pré-requisitos
Depois de introduzir as suas credenciais do Azure, Azure verifica se o seu ambiente cumpre Olá os seguintes pré-requisitos:

- **Versão do agente mínimo** -atualizar a cópia de segurança cofres tooRecovery serviços cofres requer Olá MARS agente toobe, pelo menos, versão 2.0.9070. Se tiver itens registados tooa Cofre de cópia de segurança com um agente anteriores ao 2.0.9070, Olá verificação de pré-requisitos falha. Se falhar a verificação de pré-requisitos Olá, atualize o agente de Olá e tente novamente o Cofre de Olá tooupgrade. Pode transferir Olá a versão mais recente do agente de Olá de [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe).
- **Tarefas de configuração em curso**: se alguém está a configurar a tarefa para um cofre de cópia de segurança definido toobe atualizado ou registar um item, Olá falha de verificação de pré-requisitos. Concluir configuração de Olá, ou terminou o registo do item de Olá e, em seguida, inicie o processo de atualização do Olá cofre.
- **Modelo de faturação baseada no armazenamento**: serviços de recuperação cofres suporte Olá instância baseada em modelo de faturação. Se executar a atualização do Cofre de Olá num cofre de cópia de segurança que utiliza Olá modelo de faturação baseada no armazenamento, são tooupgrade pedido o seu modelo de faturação, juntamente com Olá cofre. Caso contrário, pode atualizar o modelo de faturação em primeiro lugar, em seguida, execute Olá cofre atualização.
- Identifica um grupo de recursos para o Cofre dos serviços de recuperação Olá. Olá, tootake partido das funcionalidades de implementação do Resource Manager, tem de colocar um cofre dos serviços de recuperação num grupo de recursos. Se não souber qual toouse de grupo de recursos, forneça o processo de atualização de um nome e Olá cria Olá grupo de recursos por si. processo de atualização de Olá também associa o Cofre de Olá com Olá novo grupo de recursos.

Depois do processo de atualização de Olá concluir a verificação de pré-requisitos Olá, processo Olá pede-lhe toostart Olá cofre atualização. Depois de confirmar, o processo de atualização de Olá demora, normalmente, à volta toocomplete 15 a 20 minutos, consoante o tamanho de Olá do seu cofre. Se tiver um cofre de grandes dimensões, a atualização pode demorar até too90 minutos.

## <a name="managing-your-recovery-services-vaults"></a>Gerir os cofres dos serviços de recuperação

Olá ecrãs a seguir mostra um novo cofre de serviços de recuperação, atualizado a partir do Cofre de cópia de segurança, no Olá portal do Azure. ecrã primeiro Olá mostra o dashboard do cofre Olá que apresenta entidades-chave para o Cofre de Olá.

![exemplo do Cofre de serviços de recuperação atualizado a partir de um cofre de cópia de segurança](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

ecrã segundo Olá mostra as ligações de ajuda de Olá toohelp disponível a começar a utilizar os serviços de recuperação de Olá do cofre.

![ajudar a ligações no painel de início rápido Olá](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>Passos pós-atualização
O Cofre de serviços de recuperação suporta a especificação informações de fuso horário na política de cópia de segurança. Depois de cofre é atualizado com êxito, aceda tooBackup políticas a partir do menu de definições do cofre e atualizar informações de fuso horário de Olá para cada uma das políticas de Olá configuradas no Cofre de Olá. Este ecrã mostra já Olá cópia de segurança agendar hora especificada como por fuso horário local utilizado quando criou a política. 

## <a name="enhanced-security"></a>Segurança melhorada

Quando é atualizado um cofre de cópia de segurança do cofre dos serviços de recuperação tooa, definições de segurança de Olá para esse cofre são ativadas automaticamente. Quando as definições de segurança de Olá são em determinadas operações, tais como as cópias de segurança a eliminar ou alterar uma frase de acesso necessitar de um [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) PIN. Para obter mais informações sobre segurança Olá avançada, consulte o artigo de Olá [tooprotect híbrida as cópias de segurança de funcionalidades de segurança](backup-azure-security-feature.md). 

Quando a segurança de Olá avançada está ativada, os dados são mantidos segurança too14 dias depois das informações de ponto de recuperação Olá foi eliminadas do Cofre de Olá. Os clientes são cobrados para armazenamento destes dados de segurança. Retenção de dados de segurança se aplica a pontos de toorecovery direcionados para o agente de cópia de segurança do Azure Olá, o servidor de cópia de segurança do Azure e o System Center Data Protection Manager. 

## <a name="gather-data-on-your-vault"></a>Recolher dados do seu Cofre

Depois de atualizar o Cofre de serviços de recuperação tooa, configure os relatórios para cópia de segurança do Azure (para VMs de IaaS e os serviços de recuperação do Azure (MARS) da Microsoft) e utilizar relatórios do Power BI tooaccess Olá. Para obter informações adicionais sobre a recolha de dados, consulte o artigo Olá, [relatórios de configurar a cópia de segurança do Azure](backup-azure-configure-reports.md).

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

**Plano de atualização de Olá afeta a minha cópias de segurança em curso?**</br>
Não. As cópias de segurança em curso continuam sem interrupções durante e após a atualização.

**Se não planear a sobre a atualização em breve, o que acontece toomy cofres?**</br>
Uma vez que todas as novas funcionalidades aplicam apenas tooRecovery os cofres dos serviços, recomendamos vivamente tooupgrade os cofres. Portal clássico Olá irá preterir, eventualmente, a Microsoft. A partir de 1 de Setembro de 2017, Microsoft começará a atualizar automaticamente os cofres dos serviços de tooRecovery cofres de cópia de segurança. Até 1 de Novembro de 2017, Microsoft irá concluir o processo de atualização de Olá. O Cofre pode ser atualizado automaticamente qualquer altura durante Setembro ou Outubro. A Microsoft recomenda a que atualizar o seu Cofre logo que possível.

**O que faz esta atualização média para os meus ferramentas existentes?**</br>
Atualize o modelo de implementação do Gestor de recursos de toohello ferramentas. Os serviços de recuperação cofres foram criadas para utilizar no modelo de implementação do Resource Manager Olá. Planeamento para o modelo de implementação do Resource Manager Olá e a contabilização de diferença de Olá nos seus cofres são importante. 

**Durante a atualização de Olá, é muito período de indisponibilidade?**</br>
Depende do número de Olá de recursos que estão a ser atualizado. Para implementações mais pequenas (alguns dezenas de instâncias protegidas), atualização todo Olá deve demorar menos de 20 minutos. Para implementações maiores, deve demorar um máximo de uma hora.

**Pode posso reverter após a atualização?**</br>
Não. A reversão não é suportada depois de recursos de Olá foram atualizados com êxito.

**Posso validar os meus recursos ou subscrição toosee se não estiverem com capacidade de atualização?**</br>
Sim. Olá primeiro passo para atualização valida que recursos Olá são capazes de atualização. No caso de falha de validação de Olá de pré-requisitos, receber mensagens por motivos de Olá todos os não é possível concluir a atualização de Olá.

**Que permissões devem tenho tootrigger cofre atualização?**</br>
Olá tooperform cofre atualização, tem de ser adicionado como coadministrador da subscrição de Olá no Olá portal clássico do Azure. Isto é necessário, mesmo que já estão listados como proprietário na Olá portal do Azure. Tente tooadd coadministrador da subscrição de Olá no toofind de portal clássico do Azure saída, se forem coadministrador da subscrição Olá. Se não for capaz de tooadd coadministrador, contacte um administrador de serviço ou coadministrador da subscrição Olá, que pode adicionar como coadministrador.

**Pode atualizar o meu Cofre de cópia de segurança com base CSP?**</br>
Não. Atualmente, não é possível atualizar os cofres de cópia de segurança com base CSP. Iremos adicionar suporte para atualização cofres de cópia de segurança com base CSP em versões seguintes Olá.

**Pode ver o meu cofre clássico post atualização?**</br>
Não. Não é possível ver ou gerir o seu Cofre clássico post atualização. Só será capaz de toouse Olá novo portal do Azure para todas as ações de gestão no Cofre de Olá.

**Falha ao atualizar o meu, mas a máquina de Olá que contido agente Olá necessidade de atualizar, não já existe. O que posso fazer nesse caso?**</br>
Se precisar de arquivo de Olá toouse, Olá cópias de segurança desta máquina para a retenção de longa duração, em seguida, não será capaz de tooupgrade Cofre de Olá. Em versões futuras iremos adicionar suporte para atualizar essa um cofre.
Se não precisar de cópias de segurança do toostore Olá desta máquina deixam de ser, em seguida, anular o registo nesta máquina a partir do Cofre de Olá e tente novamente a actualização de Olá.

**Por que motivo não vejo informações de tarefas Olá para os meus recursos no local após a atualização**</br>
Monitorização local cópias de segurança (o agente MARS, o DPM e o servidor de cópia de segurança do Azure) é uma nova funcionalidade que obtém quando atualizar o seu Cofre de serviços de tooRecovery de Cofre de cópia de segurança. informações de monitorização de Olá ocupa too12 horas toosync com o serviço de Olá.

**Como posso comunicar um problema?**</br>
Se atualizar qualquer parte do Cofre de Olá falhar, Olá nota OperationId listado no registo de erros Olá. Microsoft Support proativamente funcionará problema de Olá tooresolve. Pode entrar tooSupport ou e-mail-nos rsvaultupgrade@service.microsoft.com com o ID de subscrição, nome do cofre e OperationId. Vamos tentar problema de Olá tooresolve mais rapidamente possível. Não repita a operação de Olá, a menos que instruiu explicitamente toodo Sim pela Microsoft.


## <a name="next-steps"></a>Passos seguintes
Utilize Olá seguinte artigo para:</br>
[Cópia de segurança de uma VM do IaaS](backup-azure-arm-vms-prepare.md)</br>
[Cópia de segurança de um servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md)</br>
[Cópia de segurança um Windows Server](backup-configure-vault.md).
