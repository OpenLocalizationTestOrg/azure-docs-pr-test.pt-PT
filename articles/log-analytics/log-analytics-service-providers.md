---
title: "Funcionalidades de análise para fornecedores de serviços de aaaLog | Microsoft Docs"
description: "Análise de registos pode ajudar geridos fornecedores de serviços (MSPs), as grandes empresas, os fabricantes Sofware independentes (ISVs) e fornecedores de serviços de alojamento gerirem e monitorizar os servidores de infraestrutura de nuvem ou no local do cliente."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>Funcionalidades de análise do registo para fornecedores de serviços
Análise de registos pode ajudar os fornecedores de serviços geridos (MSPs), as grandes empresas, os fabricantes independentes de software (ISV) e fornecedores de serviços de alojamento gerir e monitorizar os servidores de infraestrutura de nuvem ou no local do cliente. 

As grandes empresas partilham diversas semelhanças com fornecedores de serviços, especialmente quando existe uma equipa de TI centralizada que é responsável pela gestão IT para muitas unidades empresariais diferentes. De simplicidade, este documento utiliza o termo Olá *fornecedor de serviços* mas hello mesma funcionalidade também está disponível para as empresas e outros clientes.

## <a name="cloud-solution-provider"></a>Fornecedor de Soluções Cloud
Parceiros e fornecedores de serviço que fazem parte do Olá [fornecedor de solução em nuvem (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) programa, análise de registos é uma das Olá serviços do Azure disponíveis uma subscrição do CSP. 

Para análise de registos, Olá seguintes funcionalidades está ativada em *provedor de soluções de nuvem* subscrições.

Como um *provedor de soluções de nuvem* , pode:

* Crie áreas de trabalho de análise de registos na subscrição de um inquilino (cliente).
* Áreas de trabalho de acesso criadas pelos inquilinos. 
* Adicionar e remover utilizador acesso toohello área de trabalho utilizando a gestão de utilizador do Azure. Quando na área de trabalho de um inquilino na Olá OMS a página de gestão de utilizadores Olá portal em definições não está disponível
  * Análise de registos não suporta o acesso baseado em funções ainda - dar um utilizador `reader` permissão no Olá portal do Azure permite-lhes toomake alterações de configuração no portal do OMS Olá

toolog na subscrição do inquilino tooa, terá de identificador de inquilino de Olá toospecify. Identificador de inquilino Olá é, frequentemente, essa última parte do Olá correio electrónico endereço utilizado toosign no.

* No portal do OMS Olá, adicionar `?tenant=contoso.com` no Olá URL para o portal de Olá. Por exemplo, `mms.microsoft.com/?tenant=contoso.com`
* No PowerShell, utilize Olá `-Tenant contoso.com` parâmetro ao utilizar `Add-AzureRmAccount` cmdlet
* Identificador de inquilino Olá é adicionado automaticamente ao utilizar Olá `OMS portal` associar de Olá tooopen portal do Azure e inicie sessão no portal do OMS toohello para área de trabalho Olá selecionado

Como um *cliente* de um fornecedor de solução em nuvem, pode:

* Criar registo de áreas de trabalho de análise numa subscrição CSP
* Áreas de trabalho de acesso criadas pelo Olá CSP
  * Olá utilize `OMS portal` associar de Olá tooopen portal do Azure e inicie sessão no portal do OMS toohello para área de trabalho Olá selecionado
* Ver e utilizar a página de gestão de utilizadores do Olá em definições no portal do OMS Olá

> [!NOTE]
> Olá incluídos cópia de segurança e soluções de recuperação de Site para análise de registos não são capazes de tooconnect tooa dos serviços de recuperação cofre e não podem ser configuradas numa subscrição do CSP. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Gerir vários clientes através da análise do registo
Recomenda-se que crie uma área de trabalho de análise de registos de cada cliente, que gere. Fornece uma área de trabalho de análise de registos:

* Uma localização geográfica para toobe dados armazenado. 
* Granularidade para faturação 
* Isolamento de dados 
* Configuração exclusiva

Ao criar uma área de trabalho por cliente, são tookeep capaz de dados de cada cliente separados e também controlar a utilização de Olá de cada cliente.

Obter mais detalhes sobre quando e por que motivo toocreate várias áreas de trabalho descrita no [gerir acesso toolog análise](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Criação e configuração de áreas de trabalho do cliente podem ser automatizadas utilizando [PowerShell](log-analytics-powershell-workspace-configuration.md), [modelos do Resource Manager](log-analytics-template-workspace-configuration.md), ou utilizando Olá [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

utilização de Olá de modelos do Resource Manager para a configuração de área de trabalho permite-lhe toohave uma configuração principal que pode ser utilizado toocreate e configurar áreas de trabalho. Pode ter a certeza de que, como áreas de trabalho são criadas para os clientes são automaticamente configurados tooyour requisitos. Quando atualizar os seus requisitos, o modelo de Olá é atualizado e, em seguida, reaplicada áreas de trabalho existente Olá. Este processo garante que o mesmo existentes áreas de trabalho cumpram as normas de novo.    

Quando gerir várias áreas de trabalho de análise de registos, recomendamos a integração de cada área de trabalho com o seu sistema de emissão de permissões existente / consola de operações utilizando Olá [alertas](log-analytics-alerts.md) funcionalidade. Através da integração com os sistemas existentes, pessoal de suporte pode continuar toofollow os respetivos processos familiares. Análise de registos regularmente verifica cada área de trabalho com Olá alerta os critérios que especificar e gera um alerta quando for necessária ação.

Para personalizado vistas de dados, utilize Olá [dashboard](../azure-portal/azure-portal-dashboards.md) capacidade no Olá portal do Azure.  

Para o nível de executive relatórios resumir os dados em áreas de trabalho pode utilizar Olá integração entre análise de registos e [PowerBI](log-analytics-powerbi.md). Se precisar de toointegrate com outro sistema de relatórios, pode utilizar Olá API de pesquisa (através do PowerShell ou [REST](log-analytics-log-search-api.md)) toorun consultas e exportar resultados da pesquisa.

## <a name="next-steps"></a>Passos Seguintes
* Automatizar a criação e a configuração de áreas de trabalho utilizando [modelos do Resource Manager](log-analytics-template-workspace-configuration.md)
* Automatizar a criação de áreas de trabalho utilizando [PowerShell](log-analytics-powershell-workspace-configuration.md) 
* Utilize [alertas](log-analytics-alerts.md) toointegrate com sistemas existentes
* Gerar relatórios de resumo utilizando [PowerBI](log-analytics-powerbi.md)

