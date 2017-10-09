---
title: "aaaUpdate Azure módulos na automatização do Azure | Microsoft Docs"
description: "Este artigo descreve como pode atualizar agora comuns módulos do PowerShell do Azure fornecidos por predefinição na automatização do Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>Como tooupdate módulos do Azure PowerShell na automatização do Azure

módulos do Azure PowerShell mais comuns do Olá são fornecidos por predefinição em cada conta de automatização.  atualizações da equipa do Azure de Olá Olá módulos do Azure regularmente, na conta de automatização de Olá fornecemos uma forma para si módulos de Olá tooupdate na conta de Olá quando existem novas versões do portal de Olá.  

Porque os módulos são atualizados regularmente por grupo de produtos Olá, as alterações podem ocorrer com cmdlets de Olá incluído, que poderá afetar negativamente os runbooks, dependendo do tipo de Olá de alteração, tais como mudar o nome de um parâmetro ou completamente a descontinuar a um cmdlet. tooavoid afetar os runbooks e Olá processos automatizar, recomenda-se vivamente que testar e validar antes de continuar.  Se não tiver uma conta de automatização dedicada pretendida para esta finalidade, considere criar um, para que possa testar muitos cenários diferentes e permutações durante o desenvolvimento de Olá dos seus runbooks, em alterações de tooiterative adição tais como a atualização Olá Módulos do PowerShell.  Depois de resultados de Olá são validados e ter aplicado as alterações necessárias, continuar com a coordenação de migração de Olá de todos os runbooks que necessário modificação e efetuar a atualização de Olá, conforme descrito abaixo na produção.     

## <a name="updating-azure-modules"></a>Atualizar os módulos do Azure

1. Módulos de Olá painel da sua conta da automatização é uma opção chamada **os módulos do Azure Update**.  É sempre ativada.<br><br> ![Atualizar a opção de módulos do Azure no painel de módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Clique em **os módulos do Azure Update** e será apresentada uma notificação de confirmação que pede-lhe se pretende toocontinue.<br><br> ![Atualizar notificação de módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Clique em **Sim** e processo de atualização do módulo Olá irá começar.  processo de atualização de Olá demora Olá de tooupdate 15 a 20 minutos seguintes módulos:

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Se os módulos de Olá já estiverem segurança toodate, em seguida, o processo de Olá será concluído dentro de alguns segundos.  Quando tiver concluído o processo de atualização de Olá será notificado.<br><br> ![Atualizar o estado de atualização de módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> A automatização do Azure irá utilizar módulos mais recentes Olá na sua conta de automatização quando uma nova tarefa agendada é executada.    

Se utilizar os cmdlets destes módulos do PowerShell do Azure na sua toomanage runbooks Azure recursos e irão tooperform este processo de atualização de todos os meses ou, por isso, tooassure tiver Olá módulos mais recentes.

## <a name="next-steps"></a>Passos seguintes

* toolearn mais informações sobre os módulos de integração e como toocreate módulos personalizados toofurther integrar automatização com outros sistemas, serviços ou soluções, consulte [módulos de integração](automation-integration-modules.md).

* Considere a utilização de integração de controlo de origem [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) ou [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally gerir e controlar as versões do seu portefólio automatização de runbook e a configuração.  
