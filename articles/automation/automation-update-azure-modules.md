---
title: "Atualizar os módulos do Azure na automatização do Azure | Microsoft Docs"
description: "Este artigo descreve como pode atualizar agora comuns módulos do PowerShell do Azure fornecidos por predefinição na automatização do Azure."
services: automation
documentationcenter: 
author: georgewallace
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
ms.openlocfilehash: f5e7c66cfd26bd6927d48ffd8bc0f82e9a3e2d13
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a>Como atualizar os módulos do Azure PowerShell na automatização do Azure

Os módulos do Azure PowerShell mais comuns são fornecidos por predefinição em cada conta de automatização.  A equipa do Azure atualiza os módulos do Azure regularmente, na conta de automatização, fornecemos uma forma de atualizar os módulos na conta quando existem novas versões do portal.  

Porque os módulos são atualizados regularmente pelo grupo de produtos, as alterações podem ocorrer com os cmdlets incluídos, o que poderá afetar negativamente os runbooks dependendo do tipo de alteração, tal como mudar o nome de um parâmetro ou completamente a descontinuar a um cmdlet. Para evitar o impacto dos runbooks e os processos que automatizar, este é vivamente recomendado que testar e validar antes de continuar.  Se não tiver uma conta de automatização dedicada pretendida para esta finalidade, considere criar um, para que possa testar muitos cenários diferentes e permutações durante o desenvolvimento dos seus runbooks, além da iterativas alterações como a atualização do Módulos do PowerShell.  Depois dos resultados são validados e ter aplicado as alterações necessárias, continuar com a coordenação a migração de todos os runbooks que necessário modificação e efetuar a atualização, conforme descrito abaixo na produção.     

## <a name="updating-azure-modules"></a>Atualizar os módulos do Azure

1. Na página de módulos da sua conta de automatização, é uma opção chamada **os módulos do Azure Update**. É sempre ativada.<br><br> ![Atualizar a opção de módulos do Azure na página de módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Clique em **os módulos do Azure Update** e é-lhe apresentada uma notificação de confirmação que pede-lhe se pretende continuar.<br><br> ![Atualizar notificação de módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Clique em **Sim** e iniciar o processo de atualização do módulo. O processo de atualização demora cerca de 15 a 20 minutos para atualizar os seguintes módulos:

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Se os módulos já estão atualizados, em seguida, o processo é concluído dentro de alguns segundos. Quando o processo de atualização estiver concluída, será notificado.<br><br> ![Atualizar o estado de atualização de módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> A automatização do Azure utiliza os módulos mais recentes na sua conta de automatização quando uma nova tarefa agendada é executada.    

Se utilizar os cmdlets destes módulos do PowerShell do Azure nos runbooks para gerir recursos do Azure, em seguida, pretende executar este processo de atualização de cada mês ou, por isso, para garantir que têm os módulos mais recentes.

## <a name="next-steps"></a>Passos seguintes

* Para obter mais informações sobre como criar módulos personalizados para integrar mais automatização com outros sistemas, serviços ou soluções e a módulos de integração, consulte [módulos de integração](automation-integration-modules.md).

* Considere a utilização de integração de controlo de origem [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) ou [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) gerir centralmente e controlar as versões do seu portefólio automatização de runbook e a configuração.  