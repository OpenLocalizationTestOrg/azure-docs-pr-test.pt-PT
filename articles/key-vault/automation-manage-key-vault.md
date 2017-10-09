---
title: "aaaManage Cofre de chaves do Azure através da automatização do Azure | Microsoft Docs"
description: "Saiba mais sobre como Olá serviço de automatização do Azure pode ser utilizado toomanage Cofre de chaves do Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Gerir o Cofre de chaves do Azure através da automatização do Azure
Este guia irá apresentar toohello serviço de automatização do Azure e como pode ser utilizado toosimplify gestão das suas chaves e segredos no Cofre de chaves do Azure.

## <a name="what-is-azure-automation"></a>O que é a Automatização do Azure?
[A automatização do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar a gestão de nuvem através de automatização de processos e a configuração de estado pretendido. Através da automatização do Azure, as tarefas manuais, repetidas, execução longa e propensas ao erro podem ser automatizada tooincrease fiabilidade, eficiência e toovalue de tempo para a sua organização.

A automatização do Azure fornece um motor de execução do fluxo de trabalho altamente fiável, de elevada disponibilidade que dimensiona toomeet às suas necessidades. Na automatização do Azure, os processos podem ser arrancou manualmente, por sistemas de terceiros 3rd ou em intervalos agendados para que as tarefas acontecer exatamente quando necessário.

Reduzir a sobrecarga operacional e libertar IT e DevOps pessoal toofocus no trabalho que adiciona o valor de negócio, movendo a sua toobe de tarefas de gestão de nuvem são executadas automaticamente pela automatização do Azure.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Como pode que o automatização do Azure ajuda a gerir o Cofre de chaves do Azure?
O Cofre de chaves que podem ser gerido na automatização do Azure utilizando Olá [cmdlets do Cofre de chaves AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) e [cmdlets do Cofre de chaves do Azure clássico](https://msdn.microsoft.com/library/azure/dn868052.aspx). Olá módulo do Azure para gerir o Cofre de chaves clássico está disponível automaticamente na automatização do Azure e pode importar Olá [AzureRM KeyVault módulo](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) na automatização do Azure, para que possam executar muitas da gestão de Cofre de chaves tarefas no âmbito do serviço de Olá. Também pode ser emparelhado estes cmdlets na automatização do Azure com cmdlets de Olá para outros serviços do Azure, as tarefas complexas tooautomate através de serviços do Azure e 3rd sistemas de terceiros.

Com os cmdlets do Cofre de chaves do Azure Olá pode efetuar estas tarefas das restantes: 

* Criar e configurar um cofre de chaves
* Criar ou importar uma chave
* Criar ou atualizar um segredo
* Atualizar os atributos de uma chave
* Obter uma chave ou segredo
* Eliminar uma chave ou segredo

Seguem-se alguns exemplos de utilização do PowerShell toomanage Cofre de chaves:  

* [Cofre de chaves do Azure - passo a passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Definir e configurar um cofre de chaves do Azure](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá da automatização do Azure e como pode ser utilizado toomanage Cofre de chaves do Azure, siga estas toolearn ligações mais sobre a automatização do Azure.

* Consulte Olá da automatização do Azure [introdução Tutorial iniciado](../automation/automation-first-runbook-graphical.md).
* Consulte Olá [scripts do PowerShell do Cofre de chaves do Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

