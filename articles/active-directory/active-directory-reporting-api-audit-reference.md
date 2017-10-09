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
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="6e17b-103">Auditoria de Active Directory referência da API do Azure</span><span class="sxs-lookup"><span data-stu-id="6e17b-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="6e17b-104">Este tópico faz parte de uma coleção de tópicos sobre Olá do Azure Active Directory API do relatório.</span><span class="sxs-lookup"><span data-stu-id="6e17b-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="6e17b-105">Relatórios do Azure AD fornecem uma API que permite-lhe dados de auditoria tooaccess utilizando código ou ferramentas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="6e17b-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="6e17b-106">âmbito de Olá deste tópico é tooprovide, com informações de referência sobre Olá **API de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="6e17b-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="6e17b-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="6e17b-107">See:</span></span>

* <span data-ttu-id="6e17b-108">[Registos de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações concetuais</span><span class="sxs-lookup"><span data-stu-id="6e17b-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="6e17b-109">[Introdução ao hello API do Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API do relatório.</span><span class="sxs-lookup"><span data-stu-id="6e17b-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="6e17b-110">Para:</span><span class="sxs-lookup"><span data-stu-id="6e17b-110">For:</span></span>

- <span data-ttu-id="6e17b-111">Perguntas mais frequentes, leia a nossa [FAQ](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="6e17b-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="6e17b-112">Problemas,. [um pedido de suporte de ficheiros](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="6e17b-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="6e17b-113">Quem pode aceder a dados Olá?</span><span class="sxs-lookup"><span data-stu-id="6e17b-113">Who can access hello data?</span></span>
* <span data-ttu-id="6e17b-114">Utilizadores Olá a função de administrador de segurança ou de leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="6e17b-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="6e17b-115">Administradores Globais</span><span class="sxs-lookup"><span data-stu-id="6e17b-115">Global Admins</span></span>
* <span data-ttu-id="6e17b-116">Qualquer aplicação que tenha autorização tooaccess Olá API (autorização da aplicação pode ser o programa de configuração apenas com base nas permissões de Administrador Global)</span><span class="sxs-lookup"><span data-stu-id="6e17b-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e17b-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6e17b-117">Prerequisites</span></span>
<span data-ttu-id="6e17b-118">No tooaccess ordem isto comunicar através de Olá API de relatórios, tem de ter:</span><span class="sxs-lookup"><span data-stu-id="6e17b-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="6e17b-119">Um [gratuito do Azure Active Directory ou a edição melhor](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="6e17b-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="6e17b-120">Olá concluída [pré-requisitos tooaccess Olá do Azure AD relatórios API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="6e17b-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="6e17b-121">Aceder à API de Olá</span><span class="sxs-lookup"><span data-stu-id="6e17b-121">Accessing hello API</span></span>
<span data-ttu-id="6e17b-122">Se pode aceder a esta API através de Olá [gráfico Explorer](https://graphexplorer2.cloudapp.net) ou através de programação utilizando, por exemplo, do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e17b-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="6e17b-123">Ordem de PowerShell toocorrectly interpretar sintaxe de filtro de OData Olá utilizada nas chamadas REST de gráfico do AAD, tem de utilizar Olá backtick (aka: grave acentos) caráter demasiado "" Olá $ como carácter de escape.</span><span class="sxs-lookup"><span data-stu-id="6e17b-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="6e17b-124">caráter de backtick Olá serve como [caráter de escape do PowerShell](https://technet.microsoft.com/library/hh847755.aspx), permitindo PowerShell toodo uma literal interpretação do caráter de $ Olá e evitar confusa-lo como um nome de variável do PowerShell (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="6e17b-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="6e17b-125">Olá foco deste tópico é Olá Explorador do gráfico.</span><span class="sxs-lookup"><span data-stu-id="6e17b-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="6e17b-126">Para obter um exemplo do PowerShell, consulte este [script do PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="6e17b-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="6e17b-127">Ponto final de API</span><span class="sxs-lookup"><span data-stu-id="6e17b-127">API Endpoint</span></span>
<span data-ttu-id="6e17b-128">Pode aceder a esta API utilizando Olá URI os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6e17b-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="6e17b-129">Não há nenhum limite do número de Olá de registos devolvidos pela API de auditoria de Olá do Azure AD (utilizando a paginação de OData).</span><span class="sxs-lookup"><span data-stu-id="6e17b-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="6e17b-130">Para limites de retenção de dados de relatórios, veja [relatórios de políticas de retenção](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="6e17b-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="6e17b-131">Esta chamada devolve dados Olá em lotes.</span><span class="sxs-lookup"><span data-stu-id="6e17b-131">This call returns hello data in batches.</span></span> <span data-ttu-id="6e17b-132">Cada lote tem um máximo de 1000 registos.</span><span class="sxs-lookup"><span data-stu-id="6e17b-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="6e17b-133">tooget Olá seguinte o lote de registos, utilize Olá seguinte ligação.</span><span class="sxs-lookup"><span data-stu-id="6e17b-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="6e17b-134">Obter informações de skiptoken Olá do primeiro conjunto de Olá de registos devolvidos.</span><span class="sxs-lookup"><span data-stu-id="6e17b-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="6e17b-135">token de ignorar Olá será no fim de Olá do conjunto de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e17b-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="6e17b-136">Filtros suportados</span><span class="sxs-lookup"><span data-stu-id="6e17b-136">Supported filters</span></span>
<span data-ttu-id="6e17b-137">Pode reduzir o número de Olá de registos que são devolvidos por uma API chamada em forma de um filtro.</span><span class="sxs-lookup"><span data-stu-id="6e17b-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="6e17b-138">API de início de sessão para dados relacionados, Olá seguintes filtros são suportados:</span><span class="sxs-lookup"><span data-stu-id="6e17b-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="6e17b-139">**$top =\<devolvido um número de registos toobe\>**  -toolimit Olá diversas registos devolvidos.</span><span class="sxs-lookup"><span data-stu-id="6e17b-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="6e17b-140">Esta é uma operação dispendiosa.</span><span class="sxs-lookup"><span data-stu-id="6e17b-140">This is an expensive operation.</span></span> <span data-ttu-id="6e17b-141">Não deve utilizar este filtro, se quiser tooreturn milhares de objetos.</span><span class="sxs-lookup"><span data-stu-id="6e17b-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="6e17b-142">**$filter =\<sua declaração de filtro\>**  -toospecify, numa base de Olá dos campos de filtro suportado, tipo de Olá de registos que mais lhe interessam</span><span class="sxs-lookup"><span data-stu-id="6e17b-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="6e17b-143">Operadores e campos de filtro suportado</span><span class="sxs-lookup"><span data-stu-id="6e17b-143">Supported filter fields and operators</span></span>
<span data-ttu-id="6e17b-144">tipo de Olá toospecify de registos que mais lhe interessam, pode criar uma instrução de filtro que pode conter um ou uma combinação de Olá seguintes campos de filtro:</span><span class="sxs-lookup"><span data-stu-id="6e17b-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="6e17b-145">[activityDate](#activitydate) -define uma data ou um intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="6e17b-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="6e17b-146">[categoria](#category) -define a categoria de Olá pretende toofilter nos.</span><span class="sxs-lookup"><span data-stu-id="6e17b-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="6e17b-147">[activityStatus](#activitystatus) -define o estado de Olá de uma atividade</span><span class="sxs-lookup"><span data-stu-id="6e17b-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="6e17b-148">[activityType](#activitytype) -define o tipo de Olá de uma atividade</span><span class="sxs-lookup"><span data-stu-id="6e17b-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="6e17b-149">[atividade](#activity) -define a atividade de Olá como cadeia</span><span class="sxs-lookup"><span data-stu-id="6e17b-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="6e17b-150">[nome doactor/](#actorname) -define ator Olá no formato de nome do actor Olá</span><span class="sxs-lookup"><span data-stu-id="6e17b-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="6e17b-151">[ator/objectid](#actorobjectid) -define ator Olá no formato de ID do ator Olá</span><span class="sxs-lookup"><span data-stu-id="6e17b-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="6e17b-152">[ator/upn](#actorupn) -define ator Olá no formato de nome de princípio do ator Olá utilizador (UPN)</span><span class="sxs-lookup"><span data-stu-id="6e17b-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="6e17b-153">[nome do destino](#targetname) -define o destino de Olá no formato de nome do actor Olá</span><span class="sxs-lookup"><span data-stu-id="6e17b-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="6e17b-154">[destino/objectid](#targetobjectid) -define o destino de Olá no formato de ID do destino de Olá</span><span class="sxs-lookup"><span data-stu-id="6e17b-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="6e17b-155">[destino/upn](#targetupn) -define ator Olá no formato de nome de princípio do ator Olá utilizador (UPN)</span><span class="sxs-lookup"><span data-stu-id="6e17b-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="6e17b-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="6e17b-156">activityDate</span></span>
<span data-ttu-id="6e17b-157">**Suportado operadores**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="6e17b-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="6e17b-158">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="6e17b-159">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-159">**Notes**:</span></span>

<span data-ttu-id="6e17b-160">DateTime deve estar no formato UTC</span><span class="sxs-lookup"><span data-stu-id="6e17b-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="6e17b-161">categoria</span><span class="sxs-lookup"><span data-stu-id="6e17b-161">category</span></span>

<span data-ttu-id="6e17b-162">**Valores suportados**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-162">**Supported values**:</span></span>

| <span data-ttu-id="6e17b-163">Categoria</span><span class="sxs-lookup"><span data-stu-id="6e17b-163">Category</span></span>                         | <span data-ttu-id="6e17b-164">Valor</span><span class="sxs-lookup"><span data-stu-id="6e17b-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="6e17b-165">Diretório do Núcleo</span><span class="sxs-lookup"><span data-stu-id="6e17b-165">Core Directory</span></span>                   | <span data-ttu-id="6e17b-166">Diretório</span><span class="sxs-lookup"><span data-stu-id="6e17b-166">Directory</span></span> |
| <span data-ttu-id="6e17b-167">Gestão de Palavra-passe Personalizada</span><span class="sxs-lookup"><span data-stu-id="6e17b-167">Self-service Password Management</span></span> | <span data-ttu-id="6e17b-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="6e17b-168">SSPR</span></span>      |
| <span data-ttu-id="6e17b-169">Gestão de Grupos Personalizada</span><span class="sxs-lookup"><span data-stu-id="6e17b-169">Self-service Group Management</span></span>    | <span data-ttu-id="6e17b-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="6e17b-170">SSGM</span></span>      |
| <span data-ttu-id="6e17b-171">Aprovisionamento de Contas</span><span class="sxs-lookup"><span data-stu-id="6e17b-171">Account Provisioning</span></span>             | <span data-ttu-id="6e17b-172">Sync</span><span class="sxs-lookup"><span data-stu-id="6e17b-172">Sync</span></span>      |
| <span data-ttu-id="6e17b-173">Rollover de Palavra-passe Automatizada</span><span class="sxs-lookup"><span data-stu-id="6e17b-173">Automated Password Rollover</span></span>      | <span data-ttu-id="6e17b-174">Rollover de Palavra-passe Automatizada</span><span class="sxs-lookup"><span data-stu-id="6e17b-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="6e17b-175">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="6e17b-175">Identity Protection</span></span>              | <span data-ttu-id="6e17b-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="6e17b-176">IdentityProtection</span></span> |
| <span data-ttu-id="6e17b-177">Utilizadores Convidados</span><span class="sxs-lookup"><span data-stu-id="6e17b-177">Invited Users</span></span>                    | <span data-ttu-id="6e17b-178">Utilizadores Convidados</span><span class="sxs-lookup"><span data-stu-id="6e17b-178">Invited Users</span></span> |
| <span data-ttu-id="6e17b-179">Serviço MIM</span><span class="sxs-lookup"><span data-stu-id="6e17b-179">MIM Service</span></span>                      | <span data-ttu-id="6e17b-180">Serviço MIM</span><span class="sxs-lookup"><span data-stu-id="6e17b-180">MIM Service</span></span> |



<span data-ttu-id="6e17b-181">**Suportado operadores**: eq</span><span class="sxs-lookup"><span data-stu-id="6e17b-181">**Supported operators**: eq</span></span>

<span data-ttu-id="6e17b-182">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="6e17b-183">ActivityStatus</span><span class="sxs-lookup"><span data-stu-id="6e17b-183">activityStatus</span></span>

<span data-ttu-id="6e17b-184">**Valores suportados**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-184">**Supported values**:</span></span>

| <span data-ttu-id="6e17b-185">Estado da atividade</span><span class="sxs-lookup"><span data-stu-id="6e17b-185">Activity Status</span></span> | <span data-ttu-id="6e17b-186">Valor</span><span class="sxs-lookup"><span data-stu-id="6e17b-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="6e17b-187">Êxito</span><span class="sxs-lookup"><span data-stu-id="6e17b-187">Success</span></span>         | <span data-ttu-id="6e17b-188">0</span><span class="sxs-lookup"><span data-stu-id="6e17b-188">0</span></span>     |
| <span data-ttu-id="6e17b-189">Falha</span><span class="sxs-lookup"><span data-stu-id="6e17b-189">Failure</span></span>         | <span data-ttu-id="6e17b-190">- 1</span><span class="sxs-lookup"><span data-stu-id="6e17b-190">- 1</span></span>   |

<span data-ttu-id="6e17b-191">**Suportado operadores**: eq</span><span class="sxs-lookup"><span data-stu-id="6e17b-191">**Supported operators**: eq</span></span>

<span data-ttu-id="6e17b-192">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="6e17b-193">activityType</span><span class="sxs-lookup"><span data-stu-id="6e17b-193">activityType</span></span>
<span data-ttu-id="6e17b-194">**Suportado operadores**: eq</span><span class="sxs-lookup"><span data-stu-id="6e17b-194">**Supported operators**: eq</span></span>

<span data-ttu-id="6e17b-195">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="6e17b-196">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-196">**Notes**:</span></span>

<span data-ttu-id="6e17b-197">maiúsculas e minúsculas</span><span class="sxs-lookup"><span data-stu-id="6e17b-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="6e17b-198">Atividade</span><span class="sxs-lookup"><span data-stu-id="6e17b-198">activity</span></span>
<span data-ttu-id="6e17b-199">**Suportado operadores**: eq, contém, startsWith</span><span class="sxs-lookup"><span data-stu-id="6e17b-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="6e17b-200">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="6e17b-201">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-201">**Notes**:</span></span>

<span data-ttu-id="6e17b-202">maiúsculas e minúsculas</span><span class="sxs-lookup"><span data-stu-id="6e17b-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="6e17b-203">nome do actor /</span><span class="sxs-lookup"><span data-stu-id="6e17b-203">actor/name</span></span>
<span data-ttu-id="6e17b-204">**Suportado operadores**: eq, contém, startsWith</span><span class="sxs-lookup"><span data-stu-id="6e17b-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="6e17b-205">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="6e17b-206">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-206">**Notes**:</span></span>

<span data-ttu-id="6e17b-207">Sensível</span><span class="sxs-lookup"><span data-stu-id="6e17b-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="6e17b-208">ator/objectId</span><span class="sxs-lookup"><span data-stu-id="6e17b-208">actor/objectId</span></span>
<span data-ttu-id="6e17b-209">**Suportado operadores**: eq</span><span class="sxs-lookup"><span data-stu-id="6e17b-209">**Supported operators**: eq</span></span>

<span data-ttu-id="6e17b-210">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="6e17b-211">nome do destino</span><span class="sxs-lookup"><span data-stu-id="6e17b-211">target/name</span></span>
<span data-ttu-id="6e17b-212">**Suportado operadores**: eq, contém, startsWith</span><span class="sxs-lookup"><span data-stu-id="6e17b-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="6e17b-213">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="6e17b-214">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-214">**Notes**:</span></span>

<span data-ttu-id="6e17b-215">Sensível</span><span class="sxs-lookup"><span data-stu-id="6e17b-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="6e17b-216">destino/upn</span><span class="sxs-lookup"><span data-stu-id="6e17b-216">target/upn</span></span>
<span data-ttu-id="6e17b-217">**Suportado operadores**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="6e17b-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="6e17b-218">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="6e17b-219">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-219">**Notes**:</span></span>

* <span data-ttu-id="6e17b-220">Sensível</span><span class="sxs-lookup"><span data-stu-id="6e17b-220">Case-insensitive</span></span>
* <span data-ttu-id="6e17b-221">Precisa de espaço de nomes completa tooadd Olá ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="6e17b-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="6e17b-222">destino/objectId</span><span class="sxs-lookup"><span data-stu-id="6e17b-222">target/objectId</span></span>
<span data-ttu-id="6e17b-223">**Suportado operadores**: eq</span><span class="sxs-lookup"><span data-stu-id="6e17b-223">**Supported operators**: eq</span></span>

<span data-ttu-id="6e17b-224">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="6e17b-225">ator/upn</span><span class="sxs-lookup"><span data-stu-id="6e17b-225">actor/upn</span></span>
<span data-ttu-id="6e17b-226">**Suportado operadores**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="6e17b-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="6e17b-227">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="6e17b-228">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="6e17b-228">**Notes**:</span></span>

* <span data-ttu-id="6e17b-229">Sensível</span><span class="sxs-lookup"><span data-stu-id="6e17b-229">Case-insensitive</span></span> 
* <span data-ttu-id="6e17b-230">Precisa de espaço de nomes completa tooadd Olá ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="6e17b-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="6e17b-231">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="6e17b-231">Next Steps</span></span>
* <span data-ttu-id="6e17b-232">Pretende toosee exemplos para atividades de sistema filtrado?</span><span class="sxs-lookup"><span data-stu-id="6e17b-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="6e17b-233">Veja Olá [amostras de API de auditoria do Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6e17b-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="6e17b-234">Pretende tooknow mais informações sobre a API de relatórios Olá do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="6e17b-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="6e17b-235">Consulte [introdução Olá API do Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e17b-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

