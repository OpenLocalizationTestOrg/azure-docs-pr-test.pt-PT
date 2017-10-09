---
title: "auditoria de Active Directory aaaAzure referência da API | Microsoft Docs"
description: "Como tooget começar a utilizar Olá API de auditoria do Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Auditoria de Active Directory referência da API do Azure
Este tópico faz parte de uma coleção de tópicos sobre Olá do Azure Active Directory API do relatório.  
Relatórios do Azure AD fornecem uma API que permite-lhe dados de auditoria tooaccess utilizando código ou ferramentas relacionadas.
âmbito de Olá deste tópico é tooprovide, com informações de referência sobre Olá **API de auditoria**.

Consulte:

* [Registos de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações concetuais

* [Introdução ao hello API do Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API do relatório.


Para:

- Perguntas mais frequentes, leia a nossa [FAQ](active-directory-reporting-faq.md) 

- Problemas,. [um pedido de suporte de ficheiros](active-directory-troubleshooting-support-howto.md) 


## <a name="who-can-access-hello-data"></a>Quem pode aceder a dados Olá?
* Utilizadores Olá a função de administrador de segurança ou de leitor de segurança
* Administradores Globais
* Qualquer aplicação que tenha autorização tooaccess Olá API (autorização da aplicação pode ser o programa de configuração apenas com base nas permissões de Administrador Global)

## <a name="prerequisites"></a>Pré-requisitos
No tooaccess ordem isto comunicar através de Olá API de relatórios, tem de ter:

* Um [gratuito do Azure Active Directory ou a edição melhor](active-directory-editions.md)
* Olá concluída [pré-requisitos tooaccess Olá do Azure AD relatórios API](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Aceder à API de Olá
Se pode aceder a esta API através de Olá [gráfico Explorer](https://graphexplorer2.cloudapp.net) ou através de programação utilizando, por exemplo, do PowerShell. Ordem de PowerShell toocorrectly interpretar sintaxe de filtro de OData Olá utilizada nas chamadas REST de gráfico do AAD, tem de utilizar Olá backtick (aka: grave acentos) caráter demasiado "" Olá $ como carácter de escape. caráter de backtick Olá serve como [caráter de escape do PowerShell](https://technet.microsoft.com/library/hh847755.aspx), permitindo PowerShell toodo uma literal interpretação do caráter de $ Olá e evitar confusa-lo como um nome de variável do PowerShell (ie: $filter).

Olá foco deste tópico é Olá Explorador do gráfico. Para obter um exemplo do PowerShell, consulte este [script do PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>Ponto final de API
Pode aceder a esta API utilizando Olá URI os seguintes:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Não há nenhum limite do número de Olá de registos devolvidos pela API de auditoria de Olá do Azure AD (utilizando a paginação de OData).
Para limites de retenção de dados de relatórios, veja [relatórios de políticas de retenção](active-directory-reporting-retention.md).

Esta chamada devolve dados Olá em lotes. Cada lote tem um máximo de 1000 registos.  
tooget Olá seguinte o lote de registos, utilize Olá seguinte ligação. Obter informações de skiptoken Olá do primeiro conjunto de Olá de registos devolvidos. token de ignorar Olá será no fim de Olá do conjunto de resultados de Olá.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Filtros suportados
Pode reduzir o número de Olá de registos que são devolvidos por uma API chamada em forma de um filtro.  
API de início de sessão para dados relacionados, Olá seguintes filtros são suportados:

* **$top =\<devolvido um número de registos toobe\>**  -toolimit Olá diversas registos devolvidos. Esta é uma operação dispendiosa. Não deve utilizar este filtro, se quiser tooreturn milhares de objetos.     
* **$filter =\<sua declaração de filtro\>**  -toospecify, numa base de Olá dos campos de filtro suportado, tipo de Olá de registos que mais lhe interessam

## <a name="supported-filter-fields-and-operators"></a>Operadores e campos de filtro suportado
tipo de Olá toospecify de registos que mais lhe interessam, pode criar uma instrução de filtro que pode conter um ou uma combinação de Olá seguintes campos de filtro:

* [activityDate](#activitydate) -define uma data ou um intervalo de datas
* [categoria](#category) -define a categoria de Olá pretende toofilter nos.
* [activityStatus](#activitystatus) -define o estado de Olá de uma atividade
* [activityType](#activitytype) -define o tipo de Olá de uma atividade
* [atividade](#activity) -define a atividade de Olá como cadeia  
* [nome doactor/](#actorname) -define ator Olá no formato de nome do actor Olá
* [ator/objectid](#actorobjectid) -define ator Olá no formato de ID do ator Olá   
* [ator/upn](#actorupn) -define ator Olá no formato de nome de princípio do ator Olá utilizador (UPN) 
* [nome do destino](#targetname) -define o destino de Olá no formato de nome do actor Olá
* [destino/objectid](#targetobjectid) -define o destino de Olá no formato de ID do destino de Olá  
* [destino/upn](#targetupn) -define ator Olá no formato de nome de princípio do ator Olá utilizador (UPN)   

- - -
### <a name="activitydate"></a>activityDate
**Suportado operadores**: eq, ge, le, gt, lt

**Exemplo**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Notas**:

DateTime deve estar no formato UTC

- - -
### <a name="category"></a>categoria

**Valores suportados**:

| Categoria                         | Valor     |
| :--                              | ---       |
| Diretório do Núcleo                   | Diretório |
| Gestão de Palavra-passe Personalizada | SSPR      |
| Gestão de Grupos Personalizada    | SSGM      |
| Aprovisionamento de Contas             | Sync      |
| Rollover de Palavra-passe Automatizada      | Rollover de Palavra-passe Automatizada |
| Identity Protection              | IdentityProtection |
| Utilizadores Convidados                    | Utilizadores Convidados |
| Serviço MIM                      | Serviço MIM |



**Suportado operadores**: eq

**Exemplo**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>ActivityStatus

**Valores suportados**:

| Estado da atividade | Valor |
| :--             | ---   |
| Êxito         | 0     |
| Falha         | - 1   |

**Suportado operadores**: eq

**Exemplo**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**Suportado operadores**: eq

**Exemplo**:

    $filter=activityType eq 'User'    

**Notas**:

maiúsculas e minúsculas

- - -
### <a name="activity"></a>Atividade
**Suportado operadores**: eq, contém, startsWith

**Exemplo**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Notas**:

maiúsculas e minúsculas

- - -
### <a name="actorname"></a>nome do actor /
**Suportado operadores**: eq, contém, startsWith

**Exemplo**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Notas**:

Sensível

- - -
### <a name="actorobjectid"></a>ator/objectId
**Suportado operadores**: eq

**Exemplo**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>nome do destino
**Suportado operadores**: eq, contém, startsWith

**Exemplo**:

    $filter=targets/any(t: t/name eq 'some name')    

**Notas**:

Sensível

- - -
### <a name="targetupn"></a>destino/upn
**Suportado operadores**: eq, startsWith

**Exemplo**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Notas**:

* Sensível
* Precisa de espaço de nomes completa tooadd Olá ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity

- - -
### <a name="targetobjectid"></a>destino/objectId
**Suportado operadores**: eq

**Exemplo**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>ator/upn
**Suportado operadores**: eq, startsWith

**Exemplo**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Notas**:

* Sensível 
* Precisa de espaço de nomes completa tooadd Olá ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity

- - -
## <a name="next-steps"></a>Passos Seguintes
* Pretende toosee exemplos para atividades de sistema filtrado? Veja Olá [amostras de API de auditoria do Azure Active Directory](active-directory-reporting-api-audit-samples.md).
* Pretende tooknow mais informações sobre a API de relatórios Olá do Azure AD? Consulte [introdução Olá API do Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).

