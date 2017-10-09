---
title: "aaaAzure operações de fornecedor do Gestor de recursos | Microsoft Docs"
description: "Detalhes Olá operações disponíveis no fornecedores de recursos do Microsoft Azure Resource Manager Olá"
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Operações de fornecedor de recursos do Gestor de recursos do Azure

Este documento apresenta uma lista de operações de Olá disponíveis para cada fornecedor de recursos do Microsoft Azure Resource Manager. Estes podem ser utilizados em funções personalizados tooprovide granulares controlo de acesso baseado em funções (RBAC) permissões tooresources no Azure. Tenha em atenção de que não se trata de uma lista completa e operações podem ser adicionadas ou removidas como cada fornecedor está atualizado. Cadeias de operação seguem o formato de Olá de `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Para obter uma lista abrangente e atual utilize `Get-AzureRmProviderOperation` (no PowerShell) ou `azure provider operations show` (na CLI do Azure) operações toolist de fornecedores de recursos do Azure.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| Operação | Descrição |
|---|---|
|ação de configuração /|Configuração de inquilinos de atualizações.|
|/ services/ação|Uma instância de serviço no inquilino Olá de atualizações.|
|configuração/escrita|Cria uma configuração de inquilino.|
|/Configuration/Read|Lê Olá configuração de inquilinos.|
|/ services/escrita|Cria uma instância de serviço no inquilino Olá.|
|/Services/Read|Lê instâncias de serviço Olá no inquilino Olá.|
|/Services/DELETE|Elimina uma instância de serviço no inquilino Olá.|
|/Services/servicemembers/Action|Cria uma instância de membro de serviço no serviço de Olá.|
|/Services/servicemembers/Read|Lê a instância de membro de serviço Olá no serviço de Olá.|
|/Services/servicemembers/DELETE|Elimina uma instância de membro de serviço no serviço de Olá.|
|/Services/servicemembers/Alerts/Read|Lê alertas Olá para um membro de serviço.|
|/Services/Alerts/Read|Lê alertas Olá para um serviço.|
|/Services/Alerts/Read|Lê alertas Olá para um serviço.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| Operação | Descrição |
|---|---|
|generateRecommendations/ação|Gera recomendações|
|suppressions/ação|Cria/atualizações suppressions|
|registar/ação|Regista a subscrição de Olá para Olá Microsoft Advisor|
|/generateRecommendations/Read|Obtém gerar Estado recomendações|
|/recommendations/Read|Recomendações de leituras|
|/suppressions/Read|Obtém suppressions|
|/suppressions/DELETE|Elimina a supressão|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| Operação | Descrição |
|---|---|
|/Servers/Read|Obtém as informações de Olá de Olá especificado Analysis Server.|
|/ servidores/escrita|Cria ou atualiza Olá especificado Analysis Server.|
|/Servers/DELETE|Elimina Olá Analysis Server.|
|/Servers/suspend/Action|Suspende Olá Analysis Server.|
|/Servers/resume/Action|Retoma Olá Analysis Server.|
|servidores/checkNameAvailability<br>/Action|Verificações de que nome de servidor Analysis Services é válido e não em utilização.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| Operação | Descrição |
|---|---|
|checkNameAvailability/ação|Verifica se o nome de serviço está disponível|
|registar/ação|Registar a subscrição para o fornecedor de recursos de Microsoft.ApiManagement|
|ação de anular o registo /|Subscrição de anular o registo do fornecedor de recursos de Microsoft.ApiManagement|
|/ service/escrita|Criar uma nova instância do serviço de gestão de API|
|/Service/Read|Ler os metadados para uma instância de serviço de gestão de API|
|/Service/DELETE|Eliminar a instância de serviço de gestão de API|
|/Service/updatehostname/Action|O programa de configuração, atualizar ou remover nomes de domínio personalizado para um serviço de gestão de API|
|/Service/uploadcertificate/Action|Carregar o certificado SSL para um serviço de gestão de API|
|/Service/backup/Action|Cópia de segurança serviço de gestão de API toohello contentor especificado um utilizador forneceu a conta de armazenamento|
|/Service/Restore/Action|Restaurar o serviço de gestão de API a partir do contentor especificado de Olá um utilizador fornecida a conta de armazenamento|
|/Service/managedeployments/Action|Alterar o SKU/unidades, adicionar/remover implementações regional do serviço de gestão de API|
|/Service/getssotoken/Action|Obtém o token SSO que pode ser utilizado toologin no portal de legado de serviço de gestão de API como administrador|
|/Service/applynetworkconfigurationupdates/Action|Atualizações Olá Microsoft.ApiManagement recursos em execução na rede Virtual toopick atualizar as definições de rede.|
|/Service/operationresults/Read|Obtém o estado atual da operação de execução longa|
|/Service/networkStatus/Read|Obtém o estado de acesso de rede Olá de recursos.|
|/Service/loggers/Read|Obter a lista de registadores ou obter os detalhes de registo|
|/Service/loggers/Write|Adicionar novo registador ou atualizar detalhes do registo existente|
|/Service/loggers/DELETE|Remover o registo existente|
|/Service/Users/Read|Obter uma lista de utilizadores registados ou obter os detalhes da conta de utilizador|
|/Service/Users/Write|Registar um novo utilizador ou detalhes da conta de atualização de um utilizador existente|
|/Service/Users/DELETE|Remover a conta de utilizador|
|/Service/Users/generateSsoUrl/Action|Gere o URL do SSO. URL de Olá pode ser utilizados tooaccess portal de administração|
|/Service/Users/subscriptions/Read|Obter a lista de subscrições do utilizador|
|/Service/Users/Keys/Read|Obter a lista de chaves de utilizador|
|/Service/Users/Groups/Read|Obter a lista de grupos de utilizadores|
|/Service/tenant/operationResults/Read|Obter a lista de resultados da operação ou obter Resultado de uma operação específica|
|/Service/tenant/Policy/Read|Obter a configuração de política para o inquilino Olá|
|/Service/tenant/Policy/Write|Definir a configuração de política para o inquilino Olá|
|/Service/tenant/Policy/DELETE|Remover configuração da política para o inquilino Olá|
|/Service/tenant/Configuration/Save/Action|Cria a consolidação com ramo especificado do toohello de instantâneo de configuração no repositório de Olá|
|/Service/tenant/Configuration/Deploy/Action|Executa uma tarefa de implementação tooapply alterações da configuração do Olá git especificado ramo toohello na base de dados.|
|/Service/tenant/Configuration/Validate/Action|Valida as alterações do ramo de git especificado Olá|
|/Service/tenant/Configuration/operationResults/Read|Obter a lista de resultados da operação ou obter Resultado de uma operação específica|
|/Service/tenant/Configuration/syncState/Read|Obter o estado da última sincronização do git|
|/Service/tenant/Access/Read|Obter os detalhes de informações de acesso de inquilino|
|/Service/tenant/Access/Write|Atualizar detalhes de informações de acesso de inquilino|
|/Service/tenant/Access/regeneratePrimaryKey/Action|Regenerar a chave de acesso primária|
|/Service/tenant/Access/regenerateSecondaryKey/Action|Regenerar a chave de acesso secundária|
|/Service/identityProviders/Read|Obter a lista de fornecedores de identidade ou Obtenha detalhes do fornecedor de identidade|
|/Service/identityProviders/Write|Criar um novo fornecedor de identidade ou atualizar os detalhes de um fornecedor de identidade existentes|
|/Service/identityProviders/DELETE|Remover o fornecedor de identidade existentes|
|/Service/subscriptions/Read|Obter uma lista de subscrições do produto ou obter os detalhes da subscrição do produto|
|/Service/subscriptions/Write|Subscrever um produto existente de tooan existente do utilizador ou atualizar os detalhes da subscrição existente. Esta operação pode ser utilizado toorenew subscrição|
|/Service/subscriptions/DELETE|Elimine a subscrição. Esta operação pode ser utilizado toodelete subscrição|
|/Service/subscriptions/regeneratePrimaryKey/Action|Regenerar a chave primária da subscrição|
|/Service/subscriptions/regenerateSecondaryKey/Action|Regenerar a chave secundária da subscrição|
|/Service/backends/Read|Obter a lista de back-ends ou obter os detalhes de back-end|
|/Service/backends/Write|Adicionar um novo back-end ou atualizar detalhes do back-end existente|
|/Service/backends/DELETE|Remova o back-end existente|
|/Service/APIs/Read|Obter a lista de todos os registado APIs ou Get detalhes da API|
|/Service/APIs/Write|Criar nova API ou atualizar os detalhes de API existentes|
|/Service/APIs/DELETE|Remover API existente|
|/Service/APIs/Policy/Read|Obter os detalhes de configuração de políticas de API|
|/Service/APIs/Policy/Write|Definir os detalhes de configuração de política de API|
|/Service/APIs/Policy/DELETE|Remover configuração da política da API|
|/Service/APIs/Operations/Read|Obter a lista de operações de API existentes ou obter os detalhes da operação de API|
|/Service/APIs/Operations/Write|Criar nova operação da API ou atualizar a operação de API existente|
|/Service/APIs/Operations/DELETE|A operação de API existente de remoção|
|/Service/APIs/Operations/Policy/Read|Obter os detalhes de configuração de política para a operação|
|/Service/APIs/Operations/Policy/Write|Definir os detalhes da configuração de política para a operação|
|/Service/APIs/Operations/Policy/DELETE|Remover configuração da política de operação|
|/Service/Products/Read|Obter a lista de produtos ou obter os detalhes do produto|
|/Service/Products/Write|Criar novo produto ou atualizar detalhes do produto existente|
|/Service/Products/DELETE|Remova o produto existente|
|/Service/Products/subscriptions/Read|Obter a lista de subscrições do produto|
|/Service/Products/APIs/Read|Obter a lista de APIs adicionado tooexisting produto|
|/Service/Products/APIs/Write|Adicionar produto de tooexisting API existente|
|/Service/Products/APIs/DELETE|Remover API existente de produto existente|
|/Service/Products/Policy/Read|Obter a configuração da política de produto existente|
|/Service/Products/Policy/Write|Definir a configuração de política para o produto existente|
|/Service/Products/Policy/DELETE|Remover configuração da política de produto existente|
|/Service/Products/Groups/Read|Obter lista de grupos de programador associados ao produto|
|/Service/Products/Groups/Write|Associar grupo existente do Programador de produto existente|
|/Service/Products/Groups/DELETE|Eliminar a associação de grupo de programador existente com o produto existente|
|/Service/openidConnectProviders/Read|Obter a lista de fornecedores de OpenID Connect ou Obtenha detalhes de OpenID Connect fornecedor|
|/Service/openidConnectProviders/Write|Criar um novo OpenID Connect fornecedor ou atualizar os detalhes de um fornecedor de ligação de OpenID existente|
|/Service/openidConnectProviders/DELETE|Remover existente OpenID Connect fornecedor|
|/Service/Certificates/Read|Obter a lista de certificados ou obter os detalhes do certificado|
|/Service/Certificates/Write|Adicionar novo certificado|
|/Service/Certificates/DELETE|Remover o certificado existente|
|/Service/Properties/Read|Obtém a lista de todas as propriedades ou obtém os detalhes de propriedade especificado|
|/Service/Properties/Write|Cria uma nova propriedade ou atualiza o valor para a propriedade especificada|
|/Service/Properties/DELETE|Remove existente propriedade|
|/Service/Groups/Read|Obter a lista de grupos ou obtém detalhes de um grupo|
|/Service/Groups/Write|Criar novo grupo ou atualizar detalhes do grupo existente|
|/Service/Groups/DELETE|Remover grupo existente|
|/Service/Groups/Users/Read|Obter a lista de utilizadores do grupo|
|/Service/Groups/Users/Write|Adicionar grupo de tooexisting de utilizador existente|
|/Service/Groups/Users/DELETE|Remover utilizador existente do grupo existente|
|/Service/authorizationServers/Read|Obter a lista de servidores de autorização ou obter os detalhes do servidor de autorização|
|/Service/authorizationServers/Write|Criar um novo servidor de autorização ou detalhes da atualização de um servidor de autorização existente|
|/Service/authorizationServers/DELETE|Remover o servidor de autorização existente|
|/Service/Reports/bySubscription/Read|Obter o relatório agregado por subscrição.|
|/Service/Reports/byRequest/Read|Obter pedidos de dados de relatórios|
|/Service/Reports/byOperation/Read|Obter relatório agregado por operações|
|/Service/Reports/byGeo/Read|Obter relatório agregado por região geográfica|
|/Service/Reports/byUser/Read|Obter o relatório agregado pelos programadores.|
|/Service/Reports/byTime/Read|Obter relatório agregado pelo períodos de tempo|
|/Service/Reports/byApi/Read|Obter relatório agregado pelo APIs|
|/Service/Reports/byProduct/Read|Obter o relatório agregado pelo produtos.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| Operação | Descrição |
|---|---|
|appidentities/leitura|Devolve Olá recursos (web site) registado com Olá Gateway.|
|appidentities/escrita|Cria uma nova identidade de aplicação.|
|appidentities/eliminar|Elimina uma identidade de aplicação existente.|
|/deploymenttemplates/listMetadata/Action|Lista os metadados de IU associados Olá pacote de aplicação API.|
|/deploymenttemplates/Generate/Action|Devolve um modelo de implementação de tooprovision instâncias da aplicação API.|
|gateways/leitura|Instância de Gateway Olá devolve.|
|gateways/escrita|Cria um novo Gateway ou atualiza um existente.|
|gateways/eliminar|Elimina uma instância de Gateway existente.|
|/gateways/listLoginUris/Action|Povoa o arquivo de tokens e devolve o início de sessão OAuth URIs.|
|/gateways/listKeys/Action|Devolve os segredos do Gateway.|
|/gateways/tokens/Write|Cria um novo Token de Zumo com o nome fornecido Olá.|
|/gateways/Registrations/Read|Devolve Olá recursos (web site) registado com Olá Gateway.|
|/gateways/Registrations/Write|Regista um recurso (web site) com Olá Gateway.|
|/gateways/Registrations/DELETE|Anula o registo de um recurso (web site) do Olá Gateway.|
|apiapps/leitura|Devolve Olá instância da aplicação API.|
|apiapps/escrita|Cria uma nova aplicação API ou atualiza um existente.|
|apiapps/eliminar|Elimina uma instância existente da aplicação API.|
|/apiapps/listStatus/Action|Devolve o estado da aplicação API.|
|/apiapps/listKeys/Action|Devolve a aplicação API segredos.|
|/apiapps/apidefinitions/Read|Devolve a definição da API da aplicação API.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| Operação | Descrição |
|---|---|
|elevateAccess/ação|Concede Olá chamador acesso de administrador de acesso de utilizador no âmbito de inquilino Olá|
|/classicAdministrators/Read|Lê os administradores de Olá para a subscrição de Olá.|
|/ classicAdministrators/escrita|Adicionar ou modificar administrador tooa subscrição.|
|/classicAdministrators/DELETE|Remove o administrador de Olá da subscrição Olá.|
|/Locks/Read|Obtém bloqueios no Olá especificado âmbito.|
|/ bloqueios/escrita|Adiciona bloqueios ao hello especificado âmbito.|
|/Locks/DELETE|Bloqueios de eliminação no Olá especificado âmbito.|
|/policyAssignments/Read|Obtenha informação sobre uma atribuição de política.|
|/ policyAssignments/escrita|Criar uma política de atribuição no Olá especificado âmbito.|
|/policyAssignments/DELETE|Eliminar uma atribuição de política no Olá especificado âmbito.|
|/Permissions/Read|Apresenta uma lista de todos os Olá permissões Olá chamador tem num determinado âmbito.|
|/roleDefinitions/Read|Obtém informação sobre uma definição de função.|
|/ roleDefinitions/escrita|Criar ou atualizar uma definição de função personalizada com permissões especificadas e âmbitos atribuíveis.|
|/roleDefinitions/DELETE|Eliminar Olá especificada a definição de função personalizada.|
|/providerOperations/Read|Obter operações para todos os fornecedores de recursos que possam ser utilizadas em definições de funções.|
|/policyDefinitions/Read|Obtenha informação sobre uma definição de política.|
|/ policyDefinitions/escrita|Crie uma definição de política personalizada.|
|/policyDefinitions/DELETE|Elimine uma definição de política.|
|/roleAssignments/Read|Obter informações sobre uma atribuição de função.|
|/ roleAssignments/escrita|Criar uma função de atribuição no Olá especificado âmbito.|
|/roleAssignments/DELETE|Eliminar uma atribuição de função no Olá especificado âmbito.|

## <a name="microsoftautomation"></a>Microsoft

| Operação | Descrição |
|---|---|
|/automationAccounts/Read|Obtém uma conta de automatização do Azure|
|/ automationAccounts/escrita|Cria ou atualiza uma conta de automatização do Azure|
|/automationAccounts/DELETE|Elimina uma conta de automatização do Azure|
|/automationAccounts/Configurations/readContent/Action|Obtém o conteúdo do DSC de automatização do Azure|
|/automationAccounts/hybridRunbookWorkerGroups/Read|Lê recursos de trabalho de Runbook híbrida|
|/automationAccounts/hybridRunbookWorkerGroups/DELETE|Elimina recursos de trabalho de Runbook híbrida|
|/automationAccounts/jobSchedules/Read|Obtém uma tarefa da automatização do Azure|
|/automationAccounts/jobSchedules/Write|Cria uma tarefa da automatização do Azure|
|/automationAccounts/jobSchedules/DELETE|Elimina uma tarefa da automatização do Azure|
|/automationAccounts/connectionTypes/Read|Obtém um recurso de tipo de ligação de automatização do Azure|
|/automationAccounts/connectionTypes/Write|Cria um recurso de tipo de ligação de automatização do Azure|
|/automationAccounts/connectionTypes/DELETE|Elimina um recurso de tipo de ligação de automatização do Azure|
|/automationAccounts/Modules/Read|Obtém um módulo de automatização do Azure|
|/automationAccounts/Modules/Write|Cria ou atualiza um módulo de automatização do Azure|
|/automationAccounts/Modules/DELETE|Elimina um módulo de automatização do Azure|
|/automationAccounts/credentials/Read|Obtém um recurso de credencial de automatização do Azure|
|/automationAccounts/credentials/Write|Cria ou atualiza um recurso de credencial de automatização do Azure|
|/automationAccounts/credentials/DELETE|Elimina um recurso de credencial de automatização do Azure|
|/automationAccounts/Certificates/Read|Obtém um recurso de certificado da automatização do Azure|
|/automationAccounts/Certificates/Write|Cria ou atualiza um recurso de certificado da automatização do Azure|
|/automationAccounts/Certificates/DELETE|Elimina um recurso de certificado da automatização do Azure|
|/automationAccounts/Schedules/Read|Obtém um recurso de agenda da automatização do Azure|
|/automationAccounts/Schedules/Write|Cria ou atualiza um recurso de agenda da automatização do Azure|
|/automationAccounts/Schedules/DELETE|Elimina um recurso de agenda da automatização do Azure|
|/automationAccounts/Jobs/Read|Obtém uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/Write|Cria uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/Stop/Action|Para uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/suspend/Action|Suspende uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/resume/Action|Retoma uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/runbookContent/Action|Obtém o conteúdo de Olá de runbook de automatização do Azure Olá momento Olá da execução da tarefa Olá|
|/automationAccounts/Jobs/output/Action|Obtém o resultado de Olá de uma tarefa|
|/automationAccounts/Jobs/Read|Obtém uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/Write|Cria uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/Stop/Action|Para uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/suspend/Action|Suspende uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/resume/Action|Retoma uma tarefa de automatização do Azure|
|/automationAccounts/Jobs/Streams/Read|Obtém um fluxo de trabalho da automatização do Azure|
|/automationAccounts/Connections/Read|Obtém um recurso de ligação da automatização do Azure|
|/automationAccounts/Connections/Write|Cria ou atualiza um recurso de ligação da automatização do Azure|
|/automationAccounts/Connections/DELETE|Elimina um recurso de ligação da automatização do Azure|
|/automationAccounts/Variables/Read|Lê um recurso de variável da automatização do Azure|
|/automationAccounts/Variables/Write|Cria ou atualiza um recurso de variável da automatização do Azure|
|/automationAccounts/Variables/DELETE|Elimina um recurso de variável da automatização do Azure|
|/automationAccounts/runbooks/readContent/Action|Obtém o conteúdo de Olá de um runbook de automatização do Azure|
|/automationAccounts/runbooks/Read|Obtém um runbook de automatização do Azure|
|/automationAccounts/runbooks/Write|Cria ou atualiza um runbook de automatização do Azure|
|/automationAccounts/runbooks/DELETE|Elimina um runbook de automatização do Azure|
|/automationAccounts/runbooks/draft/readContent/Action|Obtém Olá conteúdo de um rascunho de runbook da automatização do Azure|
|/automationAccounts/runbooks/draft/writeContent/Action|Cria o conteúdo de Olá de um rascunho de runbook de automatização do Azure|
|/automationAccounts/runbooks/draft/Read|Obtém um rascunho de runbook da automatização do Azure|
|/automationAccounts/runbooks/draft/publish/Action|Publica um rascunho de runbook da automatização do Azure|
|/automationAccounts/runbooks/draft/undoEdit/Action|Anular edições tooan rascunho de runbook da automatização do Azure|
|/automationAccounts/runbooks/draft/testJob/Read|Obtém uma tarefa de teste de rascunho de runbook de automatização do Azure|
|/automationAccounts/runbooks/draft/testJob/Write|Cria uma tarefa de teste de rascunho de runbook de automatização do Azure|
|/automationAccounts/runbooks/draft/testJob/Stop/Action|Parar uma tarefa de teste de rascunho de runbook de automatização do Azure|
|/automationAccounts/runbooks/draft/testJob/suspend/Action|Suspende uma tarefa de teste de rascunho de runbook de automatização do Azure|
|/automationAccounts/runbooks/draft/testJob/resume/Action|Retoma uma tarefa de teste de rascunho de runbook de automatização do Azure|
|/automationAccounts/webhooks/Read|Lê um webhook de automatização do Azure|
|/automationAccounts/webhooks/Write|Cria ou atualiza um webhook de automatização do Azure|
|/automationAccounts/webhooks/DELETE|Elimina um webhook de automatização do Azure |
|/automationAccounts/webhooks/generateUri/Action|Gera um URI para um webhook de automatização do Azure|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Este fornecedor não é um fornecedor ARM completo e não fornece quaisquer operações ARM.

## <a name="microsoftbatch"></a>Microsoft.Batch

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição de Olá para Olá fornecedor de recursos do Batch e permite Olá criação de contas do Batch|
|/ batchAccounts/escrita|Cria uma nova conta do Batch ou atualiza uma conta de Batch existente|
|/batchAccounts/Read|Apresenta uma lista de contas do Batch ou obtém Olá propriedades de uma conta do Batch|
|/batchAccounts/DELETE|Elimina uma conta do Batch|
|/batchAccounts/listkeys/Action|Apresenta uma lista de aceder às chaves para uma conta do Batch|
|/batchAccounts/regeneratekeys/Action|Gera de novo a aceder às chaves para uma conta do Batch|
|/batchAccounts/syncAutoStorageKeys/Action|Sincroniza as chaves de acesso da conta de armazenamento automática Olá configurado para uma conta do Batch|
|/batchAccounts/Applications/Read|Apresenta uma lista de aplicações ou obtém Olá propriedades de uma aplicação|
|/batchAccounts/Applications/Write|Cria uma nova aplicação ou atualiza uma aplicação existente|
|/batchAccounts/Applications/DELETE|Elimina uma aplicação|
|/batchAccounts/Applications/versions/Read|Obtém Olá propriedades de um pacote de aplicação|
|/batchAccounts/Applications/versions/Write|Cria um novo pacote de aplicação ou atualiza um pacote de aplicação existente|
|/batchAccounts/Applications/versions/Activate/Action|Ativa um pacote de aplicação|
|/batchAccounts/Applications/versions/DELETE|Elimina um pacote de aplicação|
|/Locations/quotas/Read|Obtém as quotas de Batch de Olá especificado subscrição na região do Azure especificada de Olá|

## <a name="microsoftbilling"></a>Microsoft.Billing

| Operação | Descrição |
|---|---|
|/INVOICES/Read|Apresenta uma lista de faturas disponíveis|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| Operação | Descrição |
|---|---|
|mapApis/leitura|Operações de leitura|
|mapApis/escrita|Operação de escrita|
|mapApis/eliminar|A operação de eliminação|
|/mapApis/regenerateKey/Action|Gera de novo Olá chave|
|/mapApis/listSecrets/Action|Lista Olá segredos|
|/mapApis/listSingleSignOnToken/Action|Leitura único início de sessão na autorização Token para Olá recursos|
|/ Operações/leitura|Descrição da operação de Olá.|

## <a name="microsoftcache"></a>Microsoft.Cache

| Operação | Descrição |
|---|---|
|checknameavailability/ação|Verifica se um nome fica disponível para utilização com uma nova Cache de Redis|
|registar/ação|Regista o fornecedor de recursos do Olá 'Microsoft.Cache' com uma subscrição|
|ação de anular o registo /|Anula o registo de fornecedor de recursos 'Microsoft.Cache' Olá com uma subscrição|
|/ redis/escrita|Modificar as definições e configuração no portal de gestão de Olá Olá da Cache de Redis|
|/redis/Read|Ver definições e a configuração Olá da Cache de Redis no portal de gestão de Olá|
|/redis/DELETE|Eliminar Olá toda a Cache de Redis|
|/redis/listKeys/Action|Vista Olá valor das chaves de acesso da Cache de Redis no portal de gestão de Olá|
|/redis/regenerateKey/Action|Valor das chaves de acesso da Cache de Redis no portal de gestão de Olá Olá alteração|
|/redis/Import/Action|Importar dados de um formato especificado de vários blobs para Redis|
|/redis/Export/Action|Exportar os blobs de armazenamento do Redis dados tooprefixed no formato especificado|
|/redis/forceReboot/Action|Force reiniciar uma instância da cache, potencialmente com perda de dados.|
|/redis/Stop/Action|Pare uma instância da cache.|
|/redis/Start/Action|Inicie uma instância da cache.|
|/redis/metricDefinitions/Read|Obtém as métricas disponíveis de Olá para uma Cache de Redis|
|/redis/firewallRules/Read|Obter Olá regras de firewall IP de uma Cache de Redis|
|/redis/firewallRules/Write|Editar regras de firewall Olá IP de uma Cache de Redis|
|/redis/firewallRules/DELETE|Eliminar as regras de firewall IP de uma Cache de Redis|
|/redis/listUpgradeNotifications/Read|Lista Olá notificações de atualização mais recente para o inquilino da cache de Olá.|
|/redis/linkedservers/Read|Obter os servidores ligados associado uma cache de redis.|
|/redis/linkedservers/Write|Adicionar o servidor ligado tooa a Cache de Redis|
|/redis/linkedservers/DELETE|Eliminar o servidor ligado a partir de uma Cache de Redis|
|/redis/patchSchedules/Read|Obtém Olá aplicação de patches agendamento de uma Cache de Redis|
|/redis/patchSchedules/Write|Modificar Olá aplicação de patches de agendamento de uma Cache de Redis|
|/redis/patchSchedules/DELETE|Eliminar Olá patch agendamento de uma Cache de Redis|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| Operação | Descrição |
|---|---|
|provisionGlobalAppServicePrincipalInUserTenant/ação|Principal de serviço de aprovisionamento para o principal da aplicação de serviço|
|validateCertificateRegistrationInformation/ação|Validar o objeto de compra do certificado sem submetê-la|
|registar/ação|Registar o fornecedor de recursos do Microsoft Certificates Olá para a subscrição de Olá|
|certificateOrders/escrita|Adicionar um novo certificateOrder ou atualizar um já existente|
|certificateOrders/eliminar|Eliminar um AppServiceCertificate existente|
|certificateOrders/leitura|Obter a lista de Olá de CertificateOrders|
|/certificateOrders/reissue/Action|Volte a emitir um certificateorder existente|
|/certificateOrders/renew/Action|Renovar um certificateorder existente|
|/certificateOrders/retrieveCertificateActions/Action|Obter a lista de Olá das ações de certificado|
|/certificateOrders/retrieveEmailHistory/Action|Obter o histórico de correio eletrónico de certificado|
|/certificateOrders/resendEmail/Action|Certificado de reenviar correio eletrónico|
|/certificateOrders/verifyDomainOwnership/Action|Verificar a propriedade de domínio|
|/certificateOrders/resendRequestEmails/Action|Reenvie mensagens de correio eletrónico de pedido tooanother endereço de correio eletrónico|
|/certificateOrders/resendRequestEmails/Action|Obter selar de site para um certificado de serviço de aplicações emitido|
|/certificateOrders/Certificates/Write|Adicionar um certificado novo ou atualizar um já existente|
|/certificateOrders/Certificates/DELETE|Eliminar um certificado existente|
|/certificateOrders/Certificates/Read|Obter a lista de Olá de certificados|

## <a name="microsoftclassiccompute"></a>Microsoft. classiccompute

| Operação | Descrição |
|---|---|
|registar/ação|Registar tooClassic computação|
|checkDomainNameAvailability/ação|Verifica a disponibilidade de Olá de um determinado nome de domínio.|
|moveSubscriptionResources/ação|Mova todos os recursos clássicos tooa uma subscrição diferente.|
|validateSubscriptionMoveAvailability/ação|Valide a disponibilidade da subscrição Olá para a operação de movimentação clássico.|
|/operatingSystemFamilies/Read|Apresenta uma lista de famílias de sistema operativo de convidado Olá disponíveis no Microsoft Azure e também apresenta uma lista de versões do sistema operativo Olá disponíveis para cada f
|/Capabilities/Read|Mostra as capacidades de Olá|
|/operatingSystems/Read|Apresenta uma lista de versões de Olá do sistema de operativo convidado Olá que estão atualmente disponíveis no Microsoft Azure.|
|/resourceTypes/SKUs/Read|Obtém a lista de SKUs Olá para tipos de recurso suportados.|
|/domainNames/Read|Devolva os nomes de domínio Olá dos recursos.|
|/ domainNames/escrita|Adiciona ou modifica os nomes de domínio Olá dos recursos.|
|/domainNames/DELETE|Remova nomes de domínio Olá dos recursos.|
|/domainNames/swap/Action|Trocas Olá ranhura de produção toohello ranhura de teste.|
|/domainNames/serviceCertificates/Read|Devolve Olá certificados de serviço utilizados.|
|/domainNames/serviceCertificates/Write|Adiciona ou modifica os certificados de serviço Olá utilizados.|
|/domainNames/serviceCertificates/DELETE|Elimine certificados de serviço Olá utilizados.|
|/domainNames/serviceCertificates/operationStatuses/Read|Lê o estado da operação Olá para certificados de serviço de nomes de domínio Olá.|
|/domainNames/Capabilities/Read|Mostra as capacidades de nome de domínio Olá|
|/domainNames/Extensions/Read|Devolve Olá extensões de nome de domínio.|
|/domainNames/Extensions/Write|Adicione as extensões de nome de domínio Olá.|
|/domainNames/Extensions/DELETE|Remova extensões de nome de domínio Olá.|
|/domainNames/Extensions/operationStatuses/Read|Lê o estado da operação Olá de extensões de nomes de domínio Olá.|
|/domainNames/Active/Write|Define o nome de domínio do Active Directory Olá.|
|/domainNames/slots/Read|Mostra as ranhuras de implementação de Olá.|
|/domainNames/slots/Write|Cria ou atualiza a implementação de Olá.|
|/domainNames/slots/DELETE|Elimina uma ranhura de implementação especificado.|
|/domainNames/slots/Start/Action|Inicia uma ranhura de implementação.|
|/domainNames/slots/Stop/Action|Suspende a ranhura de implementação de Olá.|
|/domainNames/slots/operationStatuses/Read|Lê o estado da operação Olá de ranhuras de nomes de domínio Olá.|
|/domainNames/slots/roles/Read|Obter função Olá para a ranhura de implementação de Olá.|
|/domainNames/slots/roles/extensionReferences/Read|Devolve Olá referência de extensão para a função de bloco de implementação de Olá.|
|/domainNames/slots/roles/extensionReferences/Write|Adiciona ou modifica a referência de extensão de Olá para função de bloco de implementação de Olá.|
|/domainNames/slots/roles/extensionReferences/DELETE|Remova a referência de extensão de Olá para função de bloco de implementação de Olá.|
|/domainNames/slots/roles/extensionReferences/operationStatuses/Read|Lê o estado da operação Olá de referências de extensão de funções de ranhuras nomes domínio Olá.|
|/domainNames/slots/roles/roleInstances/Read|Obter a instância de função Olá.|
|/domainNames/slots/roles/roleInstances/Restart/Action|Reinicia as instâncias de função.|
|/domainNames/slots/roles/roleInstances/reimage/Action|Instância de função de Olá reimages.|
|/domainNames/slots/roles/roleInstances/operationStatuses/Read|Lê o estado da operação Olá de instâncias de função de funções de ranhuras nomes domínio Olá.|
|/domainNames/slots/State/Start/Write|As alterações Olá toostopped de estado de ranhura de implementação.|
|/domainNames/slots/State/Stop/Write|As alterações Olá toostarted de estado de ranhura de implementação.|
|/domainNames/slots/upgradeDomain/Write|Percorrer domínio de atualização Olá.|
|/domainNames/internalLoadBalancers/Read|Obtém os balanceadores de carga internos de Olá.|
|/domainNames/internalLoadBalancers/Write|Cria um novo Balanceador de carga interno.|
|/domainNames/internalLoadBalancers/DELETE|Remova um novo Balanceador de carga interno.|
|/domainNames/internalLoadBalancers/operationStatuses/Read|Lê o estado da operação Olá de balanceadores de carga internos de nomes de domínio de Olá.|
|/domainNames/loadBalancedEndpointSets/Read|Mostra os conjuntos de ponto final do Olá com balanceamento de carga|
|/domainNames/loadBalancedEndpointSets/operationStatuses/Read|Lê o estado da operação Olá de conjuntos de ponto final com balanceamento de carga de nomes de domínio de Olá.|
|/domainNames/availabilitySets/Read|Mostra Olá conjunto de disponibilidade para o recurso de Olá.|
|/quotas/Read|Obter quota Olá para subscrição Olá.|
|/virtualMachines/Read|Obtém a lista de máquinas virtuais.|
|/ virtualMachines/escrita|Adiciona ou modifica máquinas virtuais.|
|/virtualMachines/DELETE|Remove as máquinas virtuais.|
|/virtualMachines/Start/Action|Inicie máquina virtual de Olá.|
|/virtualMachines/redeploy/Action|Redeploys Olá máquina.|
|/virtualMachines/Restart/Action|Reinicia a máquinas virtuais.|
|/virtualMachines/Stop/Action|Pára Olá máquina virtual.|
|/virtualMachines/Shutdown/Action|Encerrar a máquina virtual Olá.|
|/virtualMachines/attachDisk/Action|Anexa uma máquina virtual de tooa de disco de dados.|
|/virtualMachines/detachDisk/Action|Desanexa um disco de dados da máquina virtual.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/Action|Transfere o ficheiro RDP Olá máquina virtual.|
|/virtualMachines/nomes de networkInterfaces /<br>associatedNetworkSecurityGroups/leitura|Obtém o grupo de segurança de rede de Olá associado à interface de rede Olá.|
|/virtualMachines/nomes de networkInterfaces /<br>associatedNetworkSecurityGroups/escrita|Adiciona um grupo de segurança de rede associado à interface de rede Olá.|
|/virtualMachines/nomes de networkInterfaces /<br>associatedNetworkSecurityGroups/eliminar|Elimina o grupo de segurança de rede de Olá associado à interface de rede Olá.|
|/virtualMachines/nomes de networkInterfaces /<br>operationStatuses/associatedNetworkSecurityGroups/leitura|Lê o estado da operação Olá para máquinas de virtuais Olá associados a grupos de segurança de rede.|
|/virtualMachines/Providers/Microsoft.Insights/metricDefinitions/Read|Obtém as definições de métrica de Olá.|
|/virtualMachines/Providers/Microsoft.Insights/diagnosticSettings/Read|Obter as definições de diagnóstico de Olá.|
|/virtualMachines/Providers/Microsoft.Insights/diagnosticSettings/Write|Adiciona ou modifica as definições de diagnóstico.|
|/virtualMachines/Metrics/Read|Obtém as métricas de Olá.|
|/virtualMachines/operationStatuses/Read|Lê o estado da operação Olá para máquinas de virtuais Olá.|
|/virtualMachines/Extensions/Read|Obtém a extensão da máquina virtual Olá.|
|/virtualMachines/Extensions/Write|Coloca a extensão da máquina virtual Olá.|
|/virtualMachines/Extensions/operationStatuses/Read|Lê o estado da operação Olá de extensões de máquinas virtuais de Olá.|
|/virtualMachines/asyncOperations/Read|Obtém as operações assíncronas possíveis de Olá|
|/virtualMachines/Disks/Read|Obtém a lista de discos de dados|
|/virtualMachines/associatedNetworkSecurityGroups/Read|Obtém o grupo de segurança de rede de Olá associado à máquina virtual de Olá.|
|/virtualMachines/associatedNetworkSecurityGroups/Write|Adiciona um grupo de segurança de rede associado à máquina virtual de Olá.|
|/virtualMachines/associatedNetworkSecurityGroups/DELETE|Elimina o grupo de segurança de rede de Olá associado à máquina virtual de Olá.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/Read|Lê o estado da operação Olá para máquinas de virtuais Olá associados a grupos de segurança de rede.|

## <a name="microsoftclassicnetwork"></a>Classicnetwork

| Operação | Descrição |
|---|---|
|registar/ação|Registar tooClassic rede|
|/gatewaySupportedDevices/Read|Obtém a lista de Olá de dispositivos suportados.|
|/reservedIps/Read|Obtém Olá Ips reservados|
|/ reservedIps/escrita|Adicionar um novo Ip reservado|
|/reservedIps/DELETE|Elimine um Ip reservado.|
|/reservedIps/Link/Action|Associar um Ip reservado|
|/reservedIps/JOIN/Action|Associar um Ip reservado|
|/reservedIps/operationStatuses/Read|Lê o estado da operação Olá para ips Olá reservado.|
|/virtualNetworks/Read|Obter a rede virtual Olá.|
|/ virtualNetworks/escrita|Adicione uma nova rede virtual.|
|/virtualNetworks/DELETE|Elimina a rede virtual Olá.|
|/virtualNetworks/peer/Action|Peers uma rede virtual com a outra rede virtual.|
|/virtualNetworks/JOIN/Action|Junta a rede virtual Olá.|
|/virtualNetworks/checkIPAddressAvailability/Action|Verifica a disponibilidade de Olá de um determinado endereço IP numa rede virtual.|
|/virtualNetworks/Capabilities/Read|Mostra as capacidades de Olá|
|/virtualNetworks/sub-redes /<br>associatedNetworkSecurityGroups/leitura|Obtém o grupo de segurança de rede de Olá associado à sub-rede Olá.|
|/virtualNetworks/sub-redes /<br>associatedNetworkSecurityGroups/escrita|Adiciona um grupo de segurança de rede associado à sub-rede Olá.|
|/virtualNetworks/sub-redes /<br>associatedNetworkSecurityGroups/eliminar|Elimina o grupo de segurança de rede de Olá associado à sub-rede Olá.|
|/virtualNetworks/sub-redes /<br>operationStatuses/associatedNetworkSecurityGroups/leitura|Lê o estado da operação Olá para o grupo de segurança de rede sub-rede associado Olá rede virtual.|
|/virtualNetworks/operationStatuses/Read|Lê o estado da operação Olá para redes virtuais Olá.|
|/virtualNetworks/gateways/Read|Obtém os gateways de rede virtual Olá.|
|/virtualNetworks/gateways/Write|Adiciona um gateway de rede virtual.|
|/virtualNetworks/gateways/DELETE|Elimina o gateway de rede virtual Olá.|
|/virtualNetworks/gateways/startDiagnostics/Action|Inicia o diagnóstico do gateway de rede virtual Olá.|
|/virtualNetworks/gateways/stopDiagnostics/Action|Pára Olá diagnóstico do gateway de rede virtual Olá.|
|/virtualNetworks/gateways/downloadDiagnostics/Action|Transfere o diagnóstico do gateway Olá.|
|/virtualNetworks/gateways/listCircuitServiceKey/Action|Obtém a chave de serviço de circuito Olá.|
|/virtualNetworks/gateways/downloadDeviceConfigurationScript/Action|Transfere o script de configuração de dispositivo Olá.|
|/virtualNetworks/gateways/listPackage/Action|Apresenta uma lista de pacote de gateway de rede virtual Olá.|
|/virtualNetworks/gateways/operationStatuses/Read|Lê o estado da operação Olá para gateways de redes virtuais Olá.|
|/virtualNetworks/gateways/Packages/Read|Obtém o pacote de gateway de rede virtual Olá.|
|/virtualNetworks/gateways/Connections/Read|Obtém a lista de Olá de ligações.|
|/virtualNetworks/gateways/Connections/Connect/Action|Liga-se uma ligação de gateway toosite do site.|
|/virtualNetworks/gateways/Connections/Disconnect/Action|Desliga uma ligação de gateway toosite do site.|
|/virtualNetworks/gateways/Connections/Test/Action|Testa uma ligação de gateway toosite do site.|
|/virtualNetworks/gateways/clientRevokedCertificates/Read|Olá leitura revogar certificados de cliente.|
|/virtualNetworks/gateways/clientRevokedCertificates/Write|Revoga um certificado de cliente.|
|/virtualNetworks/gateways/clientRevokedCertificates/DELETE|Unrevokes um certificado de cliente.|
|/virtualNetworks/gateways/clientRootCertificates/Read|Localize Olá certificados de raiz de cliente.|
|/virtualNetworks/gateways/clientRootCertificates/Write|Carrega um novo certificado de raiz de cliente.|
|/virtualNetworks/gateways/clientRootCertificates/DELETE|Elimina o certificado de cliente de gateway de rede virtual Olá.|
|/virtualNetworks/gateways/clientRootCertificates/download/Action|Transfere o certificado pelo thumbprint.|
|/virtualNetworks/gateways/clientRootCertificates/listPackage/Action|Apresenta uma lista de pacote de certificado de gateway de rede virtual Olá.|
|/networkSecurityGroups/Read|Obtém o grupo de segurança de rede Olá.|
|/ networkSecurityGroups/escrita|Adiciona um novo grupo de segurança de rede.|
|/networkSecurityGroups/DELETE|Elimina o grupo de segurança de rede Olá.|
|/networkSecurityGroups/operationStatuses/Read|Lê o estado da operação Olá para o grupo de segurança de rede Olá.|
|/networkSecurityGroups/securityRules/Read|Obtém a regra de segurança de Olá.|
|/networkSecurityGroups/securityRules/Write|Adiciona ou atualiza uma regra de segurança.|
|/networkSecurityGroups/securityRules/DELETE|Elimina a regra de segurança de Olá.|
|/networkSecurityGroups/securityRules/operationStatuses/Read|Lê o estado da operação Olá de regras de segurança de grupo de segurança de rede de Olá.|
|/quotas/Read|Obter quota Olá para subscrição Olá.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| Operação | Descrição |
|---|---|
|registar/ação|Registar tooClassic armazenamento|
|checkStorageAccountAvailability/ação|Verifica a disponibilidade de Olá de uma conta de armazenamento.|
|/Capabilities/Read|Mostra as capacidades de Olá|
|/publicImages/Read|Obtém a imagem do Olá pública máquina virtual.|
|/Images/Read|Imagem de Olá devolve.|
|/storageAccounts/Read|Devolva a conta de armazenamento Olá com Olá fornecido conta.|
|/ storageAccounts/escrita|Adiciona uma nova conta de armazenamento.|
|/storageAccounts/DELETE|Elimine conta do storage Olá.|
|/storageAccounts/listKeys/Action|Apresenta uma lista de chaves de acesso de Olá Olá contas do storage.|
|/storageAccounts/regenerateKey/Action|Olá chaves de acesso existentes para a conta de armazenamento Olá gera de novo.|
|/storageAccounts/operationStatuses/Read|Lê o estado da operação Olá para o recurso de Olá.|
|/storageAccounts/Images/Read|Devolve Olá imagem da conta de armazenamento.|
|/storageAccounts/Images/DELETE|Elimina uma imagem de conta de armazenamento.|
|/storageAccounts/Disks/Read|Devolve Olá disco de conta de armazenamento.|
|/storageAccounts/Disks/Write|Adiciona um disco de conta de armazenamento.|
|/storageAccounts/Disks/DELETE|Elimina um disco de conta de armazenamento.|
|/storageAccounts/Disks/operationStatuses/Read|Lê o estado da operação Olá para o recurso de Olá.|
|/storageAccounts/osImages/Read|Devolve Olá imagem de sistema operativo da conta de armazenamento.|
|/storageAccounts/osImages/DELETE|Elimina uma imagem de sistema operativo da conta de armazenamento.|
|/storageAccounts/Services/Read|Obter serviços disponíveis Olá.|
|/storageAccounts/Services/metricDefinitions/Read|Obtém as definições de métrica de Olá.|
|/storageAccounts/Services/Metrics/Read|Obtém as métricas de Olá.|
|/storageAccounts/Services/diagnosticSettings/Read|Obter as definições de diagnóstico de Olá.|
|/storageAccounts/Services/diagnosticSettings/Write|Adiciona ou modifica as definições de diagnóstico.|
|/Disks/Read|Devolve Olá disco de conta de armazenamento.|
|/osImages/Read|Imagem do sistema operativo de Olá devolve.|
|/quotas/Read|Obter quota Olá para subscrição Olá.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| Operação | Descrição |
|---|---|
|/Accounts/Read|Lê as contas de API.|
|contas/escrita|Grava as contas de API.|
|/Accounts/DELETE|Elimina as contas de API|
|/Accounts/listKeys/Action|Lista de chaves|
|/Accounts/regenerateKey/Action|Regeneração da chave|
|/Accounts/SKUs/Read|Lê SKUs disponíveis para um recurso existente.|
|/Accounts/usages/Read|Obter a utilização da quota Olá para um recurso existente.|
|/ Operações/leitura|Descrição da operação de Olá.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| Operação | Descrição |
|---|---|
|/ RateCard/leitura|Devolve oferece dados, os metadados do recurso/medir e as taxas de Olá dada subscrição.|
|/ UsageAggregates/leitura|Obtém o-consumo Microsoft Azure por uma subscrição. resultado de Olá contém agrega dados de utilização, subscrição e dos recursos relacionados com informações, um intervalo de tempo específico.|

## <a name="microsoftcompute"></a>Microsoft.Compute

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição no fornecedor de recursos Microsoft. Compute|
|/restorePointCollections/Read|Obter propriedades de Olá de uma coleção de ponto de restauro|
|/ restorePointCollections/escrita|Cria uma nova coleção de ponto de restauro ou atualiza um já existente|
|/restorePointCollections/DELETE|Coleção de ponto de restauro de Olá eliminações e pontos de restauro nele contidos|
|/restorePointCollections/restorePoints/Read|Obter propriedades de Olá de um ponto de restauro|
|/restorePointCollections/restorePoints/Write|Cria um novo ponto de restauro|
|/restorePointCollections/restorePoints/DELETE|Elimina o ponto de restauro Olá|
|/restorePointCollections/restorePoints/retrieveSasUris/Action|Obter propriedades de Olá de um ponto de restauro, juntamente com o URI de SAS do blob|
|/virtualMachineScaleSets/Read|Obter propriedades de Olá de um conjunto de dimensionamento de máquina virtual|
|/ virtualMachineScaleSets/escrita|Cria um novo conjunto de dimensionamento de máquina virtual ou atualiza um já existente|
|/virtualMachineScaleSets/DELETE|Elimina o conjunto de dimensionamento de máquina virtual de Olá|
|/virtualMachineScaleSets/Start/Action|Inicia Olá instâncias do conjunto de dimensionamento de máquina virtual de Olá|
|/virtualMachineScaleSets/powerOff/Action|Desliga Olá as instâncias do conjunto de dimensionamento de máquina virtual de Olá|
|/virtualMachineScaleSets/Restart/Action|Reinicia Olá as instâncias do conjunto de dimensionamento de máquina virtual de Olá|
|/virtualMachineScaleSets/deallocate/Action|Desliga e versões Olá recursos de computação de instâncias de Olá do conjunto de dimensionamento de máquina virtual de Olá |
|/virtualMachineScaleSets/manualUpgrade/Action|Atualiza manualmente o modelo de toolatest de instâncias do conjunto de dimensionamento de máquina virtual de Olá|
|/virtualMachineScaleSets/Scale/Action|Dimensionar de / definir aumentar horizontalmente a contagem de instâncias de um dimensionamento da máquina virtual existente|
|/virtualMachineScaleSets/instanceView/Read|Obtém a vista de instância de Olá de conjunto de dimensionamento de máquina virtual de Olá|
|/virtualMachineScaleSets/SKUs/Read|Apresenta uma lista de Olá SKUs válidos de um conjunto de dimensionamento de máquina virtual existente|
|/virtualMachineScaleSets/virtualMachines/Read|Obtém Olá propriedades de uma Máquina Virtual num conjunto de dimensionamento VM|
|/virtualMachineScaleSets/virtualMachines/DELETE|Elimine uma Máquina Virtual específica num conjunto de dimensionamento VM.|
|/virtualMachineScaleSets/virtualMachines/Start/Action|Inicia uma instância de Máquina Virtual num conjunto de dimensionamento VM.|
|/virtualMachineScaleSets/virtualMachines/powerOff/Action|Instância de Powers desligar uma máquina no conjunto de dimensionamento da VM.|
|/virtualMachineScaleSets/virtualMachines/Restart/Action|Reinicia uma instância de Máquina Virtual num conjunto de dimensionamento VM.|
|/virtualMachineScaleSets/virtualMachines/deallocate/Action|Desliga e recursos de computação de Olá versões para uma Máquina Virtual num conjunto de dimensionamento VM.|
|/virtualMachineScaleSets/virtualMachines/instanceView/Read|Obtém a vista de instância de Olá de uma Máquina Virtual num conjunto de dimensionamento VM.|
|/Images/Read|Obter propriedades de Olá de Olá imagem|
|imagens/escrita|Cria uma nova imagem ou atualiza um já existente|
|/Images/DELETE|Elimina Olá imagem|
|/Operations/Read|Lista as operações disponíveis no fornecedor de recursos Microsoft. Compute|
|/Disks/Read|Obter propriedades de Olá de um disco|
|discos/escrita|Cria um novo disco ou atualiza um já existente|
|/Disks/DELETE|Elimina Olá disco|
|/Disks/beginGetAccess/Action|Obter Olá URI de SAS do disco de Olá para acesso do blob|
|/Disks/endGetAccess/Action|Revogar Olá URI de SAS do disco de Olá|
|/snapshots/Read|Obter propriedades de Olá de um instantâneo|
|instantâneos/escrita|Criar um novo instantâneo ou atualizar um já existente|
|/snapshots/DELETE|Eliminar um instantâneo|
|/availabilitySets/Read|Obter propriedades de Olá de um conjunto de disponibilidade|
|/ availabilitySets/escrita|Cria um novo conjunto de disponibilidade ou atualiza um já existente|
|/availabilitySets/DELETE|Elimina o conjunto de disponibilidade de Olá|
|/availabilitySets/vmSizes/Read|Listar tamanhos disponíveis para criar ou atualizar uma máquina virtual no conjunto de disponibilidade de Olá|
|/virtualMachines/Read|Obter propriedades de Olá de uma máquina virtual|
|/ virtualMachines/escrita|Cria uma nova máquina virtual ou atualiza uma máquina virtual existente|
|/virtualMachines/DELETE|Elimina a máquina virtual de Olá|
|/virtualMachines/Start/Action|Inicia Olá máquina|
|/virtualMachines/powerOff/Action|Desliga Olá máquina. Tenha em atenção que a máquina virtual Olá continuará toobe cobrado.|
|/virtualMachines/redeploy/Action|Redeploys máquina virtual|
|/virtualMachines/Restart/Action|Reinicia a máquina virtual de Olá|
|/virtualMachines/deallocate/Action|Desliga Olá máquina virtual e liberta Olá recursos de computação|
|/virtualMachines/generalize/Action|Define tooGeneralized de estado de máquina virtual de Olá e prepara a máquina virtual de Olá para captura|
|/virtualMachines/Capture/Action|Captura de máquina virtual de Olá copiando os discos rígidos virtuais e gera um modelo que pode ser utilizados toocreate máquinas de virtuais semelhantes|
|/virtualMachines/convertToManagedDisks/Action|Converte discos de baseadas em BLOBs Olá dos discos de toomanaged Olá máquina virtual|
|/virtualMachines/vmSizes/Read|Apresenta uma lista de tamanhos disponíveis Olá máquina pode ser atualizada para|
|/virtualMachines/instanceView/Read|Olá, obtém o estado de runtime detalhado da máquina virtual de Olá e os respetivos recursos|
|/virtualMachines/Extensions/Read|Obter propriedades de Olá de uma extensão da máquina virtual|
|/virtualMachines/Extensions/Write|Cria uma nova extensão de máquina virtual ou atualiza um já existente|
|/virtualMachines/Extensions/DELETE|Elimina a extensão da máquina virtual Olá|
|/Locations/vmSizes/Read|Apresenta uma lista de tamanhos de máquina virtual disponíveis numa localização|
|/Locations/usages/Read|Obtém os limites de serviço e as quantidades de utilização atuais para os recursos de computação da subscrição Olá numa localização|
|/Locations/Operations/Read|Obtém o estado de Olá de uma operação assíncrona|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos de registo de contentor Olá e permite a criação de Olá de registos do contentor.|
|/checknameavailability/Read|Verifica que o nome do registo é válido e não está em utilização.|
|/registries/Read|Devolve Olá lista de registos do contentor ou obtém Olá propriedades de registo de contentor especificado Olá.|
|os registos/escrita|Cria um registo de contentor com Olá parâmetros especificados ou atualizar propriedades de Olá ou etiquetas para registo de contentor especificado Olá.|
|/registries/DELETE|Elimina um registo de contentor existente.|
|/registries/listCredentials/Action|Apresenta uma lista de credenciais de início de sessão de Olá para Olá contentor especificado de registo.|
|/registries/regenerateCredential/Action|As credenciais de início de sessão de Olá para registo de contentor especificado Olá gera de novo.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| Operação | Descrição |
|---|---|
|/containerServices/subscriptions/Read|Get Olá serviços de contentor especificados com base na subscrição|
|/containerServices/resourceGroups/Read|Get Olá serviços de contentor especificados com base no grupo de recursos|
|/containerServices/resourceGroups/ContainerServiceName/Read|Obtém Olá especificado o serviço de contentor|
|/containerServices/resourceGroups/ContainerServiceName/Write|Serviço de contentor de especificado de PUT ou Olá de atualizações|
|/containerServices/resourceGroups/ContainerServiceName/DELETE|Elimina Olá especificado o serviço de contentor|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| Operação | Descrição |
|---|---|
|updateCommunicationPreference/ação|Preferência de comunicação de atualização|
|listCommunicationPreference/ação|Preferência de comunicação de lista|
|/Applications/Read|Operações de leitura|
|aplicações/escrita|Operação de escrita|
|aplicações/escrita|Operação de escrita|
|/Applications/DELETE|A operação de eliminação|
|/Applications/listSecrets/Action|Lista os segredos|
|/Applications/listSingleSignOnToken/Action|Início de sessão único Tokens de leitura|
|/Operations/Read|operações de leitura|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| Operação | Descrição |
|---|---|
|/hubs/Read|Ler qualquer Hub de informações de cliente do Azure|
|hubs/escrita|Criar ou atualizar qualquer Hub de informações de cliente do Azure|
|/hubs/DELETE|Eliminar o Hub de Insights qualquer cliente do Azure|
|/hubs/Providers/Microsoft.Insights/metricDefinitions/Read|Obtém as métricas do Olá disponíveis para o recurso|
|/hubs/Providers/Microsoft.Insights/diagnosticSettings/Read|Obtém a definição de diagnóstico de Olá para o recurso de Olá|
|/hubs/Providers/Microsoft.Insights/diagnosticSettings/Write|Cria ou atualiza a definição de diagnóstico de Olá para o recurso de Olá|
|/hubs/Providers/Microsoft.Insights/logDefinitions/Read|Obtém os registos disponíveis Olá para o recurso|
|/hubs/authorizationPolicies/Read|Leia a que política de assinatura de acesso de partilhadas quaisquer informações de cliente do Azure|
|/hubs/authorizationPolicies/Write|Criar ou atualizar qualquer política de assinatura de acesso partilhado de informações de cliente do Azure|
|/hubs/authorizationPolicies/DELETE|Eliminar qualquer política de assinatura de acesso partilhado de informações de cliente do Azure|
|/hubs/authorizationPolicies/regeneratePrimaryKey/Action|Regenerar a chave primária da política de assinaturas de acesso de partilhado das informações do cliente do Azure|
|/hubs/authorizationPolicies/regenerateSecondaryKey/Action|Regenerar a chave secundária da política de assinaturas de acesso de partilhado das informações do cliente do Azure|
|/hubs/Profiles/Read|Ler nenhum perfil de informações de cliente do Azure|
|/hubs/Profiles/Write|Escrever qualquer perfil de informações de cliente do Azure|
|/hubs/KPI/Read|Ler qualquer indicador de chave de desempenho de informações de cliente do Azure|
|/hubs/KPI/Write|Criar ou atualizar qualquer indicador de chave de desempenho de informações de cliente do Azure|
|/hubs/KPI/DELETE|Eliminar qualquer indicador de chave de desempenho de informações de cliente do Azure|
|/hubs/views/Read|Ler a qualquer vista de aplicação de informações de cliente do Azure|
|/hubs/views/Write|Criar ou atualizar qualquer vista de aplicação de informações de cliente do Azure|
|/hubs/views/DELETE|Eliminar qualquer vista de aplicação de informações de cliente do Azure|
|/hubs/interactions/Read|Ler qualquer interação de informações de cliente do Azure|
|/hubs/interactions/Write|Criar ou atualizar qualquer interação de informações de cliente do Azure|
|/hubs/roleAssignments/Read|Ler qualquer atribuição do cliente do Azure Insights Rbac|
|/hubs/roleAssignments/Write|Criar ou atualizar qualquer atribuição do cliente do Azure Insights Rbac|
|/hubs/roleAssignments/DELETE|Eliminar qualquer atribuição do cliente do Azure Insights Rbac|
|/hubs/Connectors/Read|Leia os conectores de informações de cliente do Azure|
|/hubs/Connectors/Write|Criar ou atualizar qualquer conector das informações de cliente do Azure|
|/hubs/Connectors/DELETE|Eliminar qualquer conector das informações de cliente do Azure|
|/hubs/Connectors/mappings/Read|Ler qualquer mapeamento de conector de informações de cliente do Azure|
|/hubs/Connectors/mappings/Write|Criar ou atualizar qualquer mapeamento de conector de informações de cliente do Azure|
|/hubs/Connectors/mappings/DELETE|Eliminar qualquer mapeamento de conector de informações de cliente do Azure|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| Operação | Descrição |
|---|---|
|checkNameAvailability/ação|Verifica a disponibilidade do nome de catálogo para o inquilino.|
|/catalogs/Read|Obter propriedades para o catálogo ou catálogos sob a subscrição ou grupo de recursos.|
|/ catálogos/escrita|Cria o catálogo ou atualizações de etiquetas de Olá e propriedades para o catálogo de Olá.|
|/catalogs/DELETE|Elimina o catálogo de Olá.|

## <a name="microsoftdatafactory"></a>Microsoft. DataFactory

| Operação | Descrição |
|---|---|
|/datafactories/Read|Lê a fábrica de dados.|
|/ datafactories/escrita|Criar ou atualizar a fábrica de dados|
|/datafactories/DELETE|Elimina a fábrica de dados.|
|/datafactories/datapipelines/Read|Lê o Pipeline.|
|/datafactories/datapipelines/DELETE|Elimina o Pipeline.|
|/datafactories/datapipelines/pause/Action|Pipeline de pausa.|
|/datafactories/datapipelines/resume/Action|Pipeline de retoma.|
|/datafactories/datapipelines/Update/Action|Pipeline de atualizações.|
|/datafactories/datapipelines/Write|Criar ou atualizar o Pipeline|
|/datafactories/linkedServices/Read|Lê o serviço ligado.|
|/datafactories/linkedServices/DELETE|Elimina o serviço ligado.|
|/datafactories/linkedServices/Write|Criar ou o serviço ligado de atualização|
|/datafactories/Tables/Read|Lê a tabela.|
|/datafactories/Tables/DELETE|Elimina a tabela.|
|/datafactories/Tables/Write|Criar ou atualizar tabela|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| Operação | Descrição |
|---|---|
|/Accounts/Read|Obter informações sobre Olá DataLakeAnalytics conta.|
|contas/escrita|Criar ou atualizar a conta de DataLakeAnalytics Olá.|
|/Accounts/DELETE|Elimine conta de DataLakeAnalytics Olá.|
|/Accounts/firewallRules/Read|Obter informações sobre uma regra de firewall.|
|/Accounts/firewallRules/Write|Criar ou atualizar uma regra de firewall.|
|/Accounts/firewallRules/DELETE|Elimine uma regra de firewall.|
|/Accounts/storageAccounts/Read|Obter a conta de armazenamento ligada para Olá DataLakeAnalytics conta.|
|/Accounts/storageAccounts/Write|Ligar um toohello de conta de armazenamento DataLakeAnalytics conta.|
|/Accounts/storageAccounts/DELETE|Desassociar uma conta de armazenamento da Olá DataLakeAnalytics conta.|
|/Accounts/storageAccounts/containers/Read|Obter contentores em Olá conta de armazenamento|
|/Accounts/storageAccounts/containers/listSasTokens/Action|Lista os Tokens SAS Olá contentor de armazenamento|
|/Accounts/dataLakeStoreAccounts/Read|Obter conta DataLakeStore ligada para Olá DataLakeAnalytics conta.|
|/Accounts/dataLakeStoreAccounts/Write|Ligar um toohello de conta DataLakeStore DataLakeAnalytics conta.|
|/Accounts/dataLakeStoreAccounts/DELETE|Desassociar uma conta de DataLakeStore da Olá DataLakeAnalytics conta.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| Operação | Descrição |
|---|---|
|/Accounts/Read|Obter informações sobre uma conta de DataLakeStore existed.|
|contas/escrita|Criar uma nova conta de DataLakeStore ou atualizar uma conta de DataLakeStore existed.|
|/Accounts/DELETE|Elimine uma conta de DataLakeStore existed.|
|/Accounts/firewallRules/Read|Obter informações sobre uma regra de firewall.|
|/Accounts/firewallRules/Write|Criar ou atualizar uma regra de firewall.|
|/Accounts/firewallRules/DELETE|Elimine uma regra de firewall.|
|/Accounts/trustedIdProviders/Read|Obter informações sobre um fornecedor de identidade fidedigna.|
|/Accounts/trustedIdProviders/Write|Criar ou atualizar um fornecedor de identidade fidedigna.|
|/Accounts/trustedIdProviders/DELETE|Elimine um fornecedor de identidade fidedigna.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| Operação | Descrição |
|---|---|
|registar/ação|Registar a subscrição de Olá Olá IotHub recursos fornecedor e permite Olá criação dos recursos de IotHub|
|checkNameAvailability/ação|Verifique o nome do IotHub se está disponível|
|utilizações/leitura|Obter detalhes de utilização de subscrição para este fornecedor.|
|operações/leitura|Obter todas as operações de ResourceProvider|
|iotHubs/leitura|Obtém Olá IotHub atualizará|
|iotHubs/escrita|Criar ou atualizar o recurso de IotHub|
|iotHubs/eliminar|Eliminar recurso IotHub|
|/iotHubs/listkeys/Action|Obter todas as chaves de IotHub|
|/iotHubs/exportDevices/Action|Dispositivos de exportação|
|/iotHubs/importDevices/Action|Importar dispositivos|
|/ IotHubs/metricDefinitions/leitura|Obtém as métricas disponíveis de Olá para Olá serviço IotHub|
|/iotHubs/iotHubKeys/listkeys/Action|Obter a chave de IotHub para Olá o nome fornecido|
|/iotHubs/iotHubStats/Read|Obter estatísticas IotHub|
|/iotHubs/quotaMetrics/Read|Obter métricas de Quota|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|Criar grupo de consumidores de EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|Obter os grupos de consumidores de EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/DELETE|Eliminar grupo de consumidores de EventHub|
|/iotHubs/Routing/routes/$ testall/ação|Testar uma mensagem de todas as rotas existentes|
|/iotHubs/Routing/routes/$ testnew/ação|Uma mensagem de um teste fornecido rota de teste|
|/ IotHubs/diagnosticSettings/leitura|Obtém a definição de diagnóstico de Olá para o recurso de Olá|
|/ IotHubs/diagnosticSettings/escrita|Cria ou atualiza a definição de diagnóstico de Olá para o recurso de Olá|
|/iotHubs/SKUs/Read|Obter Skus válidos de IotHub|
|/iotHubs/Jobs/Read|Obter tarefas detalhes submetidos numa fornecido IotHub|
|/iotHubs/routingEndpointsHealth/Read|Obtém o estado de funcionamento de Olá de todos os pontos finais de encaminhamento para um IotHub|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| Operação | Descrição |
|---|---|
|/ Subscrição/register/ação|Regista a subscrição de Olá|
|/Labs/DELETE|Elimine laboratórios.|
|/Labs/Read|Laboratórios de leitura.|
|laboratórios/escrita|Adiciona ou modifica laboratórios.|
|/Labs/ListVhds/Action|Imagens de disco de lista disponível para criação de imagens personalizadas.|
|/Labs/GenerateUploadUri/Action|Gere um URI para carregar as imagens de disco personalizado tooa laboratório.|
|/Labs/CreateEnvironment/Action|Crie máquinas virtuais no laboratório.|
|/Labs/ClaimAnyVm/Action|Uma máquina virtual claimable aleatória num laboratório Olá de afirmações.|
|/Labs/ExportResourceUsage/Action|Exportações Olá utilização de recursos de laboratório para uma conta de armazenamento|
|/Labs/Users/DELETE|Elimine perfis de utilizador.|
|/Labs/Users/Read|Perfis de utilizador de leitura.|
|/Labs/Users/Write|Adiciona ou modifica os perfis de utilizador.|
|/Labs/Users/Secrets/DELETE|Elimine segredos.|
|/Labs/Users/Secrets/Read|Ler os segredos.|
|/Labs/Users/Secrets/Write|Adiciona ou modifica os segredos.|
|/Labs/Users/Environments/DELETE|Elimine ambientes.|
|/Labs/Users/Environments/Read|Ambientes de leitura.|
|/Labs/Users/Environments/Write|Adiciona ou modifica os ambientes.|
|/Labs/Users/Disks/DELETE|Elimine os discos.|
|/Labs/Users/Disks/Read|Leitura de discos.|
|/Labs/Users/Disks/Write|Adiciona ou modifica os discos.|
|/Labs/Users/Disks/Attach/Action|Ligar e criar concessão Olá da máquina virtual do Olá disco toohello.|
|/Labs/Users/Disks/detach/Action|Desligue e concessão de Olá de quebra de disco Olá ligado toohello máquina.|
|/Labs/customImages/DELETE|Elimine imagens personalizadas.|
|/Labs/customImages/Read|Ler imagens personalizadas.|
|/Labs/customImages/Write|Adiciona ou modifica imagens personalizadas.|
|/Labs/serviceRunners/DELETE|Elimine runners de serviço.|
|/Labs/serviceRunners/Read|Ler runners de serviço.|
|/Labs/serviceRunners/Write|Adiciona ou modifica runners de serviço.|
|/Labs/artifactSources/DELETE|Elimine as origens de artefactos.|
|/Labs/artifactSources/Read|Ler as origens de artefactos.|
|/Labs/artifactSources/Write|Adiciona ou modifica as origens de artefactos.|
|/Labs/artifactSources/artifacts/Read|Ler os artefactos.|
|/Labs/artifactSources/artifacts/GenerateArmTemplate/Action|Gera um modelo ARM para Olá fornecido artefactos, carrega a conta de armazenamento do Olá necessário ficheiros tooa e valida o artefacto Olá gerado.|
|/Labs/artifactSources/armTemplates/Read|Ler modelos do Gestor de recursos do azure.|
|/Labs/Costs/Read|Ler os custos.|
|/Labs/Costs/Write|Adiciona ou modifica os custos.|
|/Labs/virtualNetworks/DELETE|Elimine redes virtuais.|
|/Labs/virtualNetworks/Read|Ler as redes virtuais.|
|/Labs/virtualNetworks/Write|Adiciona ou modifica as redes virtuais.|
|/Labs/formulas/DELETE|Elimine as fórmulas.|
|/Labs/formulas/Read|Ler as fórmulas.|
|/Labs/formulas/Write|Adiciona ou modifica as fórmulas.|
|/Labs/Schedules/DELETE|Elimine agendas.|
|/Labs/Schedules/Read|As agendas de leitura.|
|/Labs/Schedules/Write|Adiciona ou modifica as agendas.|
|/Labs/Schedules/execute/Action|Execute uma agenda.|
|/Labs/Schedules/ListApplicable/Action|Apresenta uma lista de todos os agendamentos aplicáveis|
|/Labs/galleryImages/Read|Ler imagens gallery.|
|/Labs/policySets/EvaluatePolicies/Action|Avalia a política de laboratório.|
|/Labs/policySets/Policies/DELETE|Elimine políticas.|
|/Labs/policySets/Policies/Read|Políticas de leitura.|
|/Labs/policySets/Policies/Write|Adicionar ou modificar as políticas.|
|/Labs/virtualMachines/DELETE|Elimine as máquinas virtuais.|
|/Labs/virtualMachines/Read|Máquinas virtuais de leitura.|
|/Labs/virtualMachines/Write|Adiciona ou modifica máquinas virtuais.|
|/Labs/virtualMachines/Start/Action|Inicie uma máquina virtual.|
|/Labs/virtualMachines/Stop/Action|Parar uma máquina virtual|
|/Labs/virtualMachines/ApplyArtifacts/Action|Aplicam-se a máquina de toovirtual de artefactos.|
|/Labs/virtualMachines/AddDataDisk/Action|Anexe uma máquina de toovirtual de disco de dados nova ou existente.|
|/Labs/virtualMachines/DetachDataDisk/Action|Exposição do disco especificado de Olá da máquina virtual de Olá.|
|/Labs/virtualMachines/Claim/Action|Assumir a propriedade de uma máquina virtual existente|
|/Labs/virtualMachines/ListApplicableSchedules/Action|Apresenta uma lista de todos os agendamentos aplicáveis|
|/Labs/virtualMachines/Schedules/DELETE|Elimine agendas.|
|/Labs/virtualMachines/Schedules/Read|As agendas de leitura.|
|/Labs/virtualMachines/Schedules/Write|Adiciona ou modifica as agendas.|
|/Labs/virtualMachines/Schedules/execute/Action|Execute uma agenda.|
|/Labs/notificationChannels/DELETE|Elimine notificationchannels.|
|/Labs/notificationChannels/Read|Ler notificationchannels.|
|/Labs/notificationChannels/Write|Adiciona ou modifica notificationchannels.|
|/Labs/notificationChannels/Notify/Action|Envie o canal de notificação de tooprovided.|
|/Schedules/DELETE|Elimine agendas.|
|/Schedules/Read|As agendas de leitura.|
|as agendas/escrita|Adiciona ou modifica as agendas.|
|/Schedules/execute/Action|Execute uma agenda.|
|/Schedules/Retarget/Action|ID de recurso de destino de uma agenda de atualizações|
|/Locations/Operations/Read|Operações de leitura.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| Operação | Descrição |
|---|---|
|/databaseAccountNames/Read|Verifica a disponibilidade do nome.|
|/databaseAccounts/Read|Lê uma conta de base de dados.|
|/ databaseAccounts/escrita|Atualize contas de base de dados.|
|/databaseAccounts/listKeys/Action|Lista de chaves de uma conta de base de dados|
|/databaseAccounts/regenerateKey/Action|Rodar chaves de uma conta de base de dados|
|/databaseAccounts/listConnectionStrings/Action|Obter as cadeias de ligação de Olá para uma conta de base de dados|
|/databaseAccounts/changeResourceGroup/Action|Alterar o grupo de recursos de uma conta de base de dados|
|/databaseAccounts/failoverPriorityChange/Action|Alterar as prioridades de ativação pós-falha de regiões de uma conta de base de dados. Esta operação de ativação pós-falha manual tooperform utilizado é|
|/databaseAccounts/DELETE|Elimina as contas de base de dados de Olá.|
|/databaseAccounts/metricDefinitions/Read|Lê a conta de base de dados de Olá definições de métricas.|
|/databaseAccounts/Metrics/Read|Lê as métricas de conta de base de dados de Olá.|
|/databaseAccounts/usages/Read|Lê utilizações de conta de base de dados de Olá.|
|/databaseAccounts/Databases/Collections/metricDefinitions/Read|Lê a coleção de Olá as definições de métrica.|
|/databaseAccounts/Databases/Collections/Metrics/Read|Lê as métricas de coleção de Olá.|
|/databaseAccounts/Databases/Collections/usages/Read|Lê utilizações de coleção de Olá.|
|/databaseAccounts/Databases/metricDefinitions/Read|Lê as definições de métrica de base de dados do Olá|
|/databaseAccounts/Databases/Metrics/Read|Lê as métricas de base de dados de Olá.|
|/databaseAccounts/Databases/usages/Read|Lê utilizações de base de dados de Olá.|
|/databaseAccounts/readonlykeys/Read|Lê a conta de base de dados de Olá chaves de só de leitura.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| Operação | Descrição |
|---|---|
|generateSsoRequest/ação|Gere um pedido de assinatura no Centro de controlo de domínio.|
|validateDomainRegistrationInformation/ação|Validar o objeto de compra de domínio sem submetê-la|
|checkDomainAvailability/ação|Verifique se um domínio está disponível para a compra|
|listDomainRecommendations/ação|Obter recomendações de domínio de lista de Olá com base em palavras-chave|
|registar/ação|Registar o fornecedor de recursos do Microsoft Domains Olá para a subscrição de Olá|
|domínios/leitura|Obter a lista de Olá de domínios|
|domínios/escrita|Adicionar um novo domínio ou atualizar um já existente|
|domínios/eliminar|Elimine um domínio existente.|
|/Domains/operationresults/Read|Obter uma operação de domínio|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| Operação | Descrição |
|---|---|
|/lcsprojects/Read|Apresentar os projetos de serviços de ciclo de vida do Microsoft Dynamics que pertencem tooa utilizador|
|/ lcsprojects/escrita|Criar e atualizar os projetos de serviços de ciclo de vida do Microsoft Dynamics que pertencem toohello utilizador. Propriedades só de nome e uma descrição de Olá podem ser atualizadas. subscrição de Olá e a localização associadas projeto Olá não podem ser atualizadas após a criação|
|/lcsprojects/DELETE|Eliminar projetos de serviços de ciclo de vida do Microsoft Dynamics que pertencem toohello utilizador|
|/lcsprojects/clouddeployments/Read|Apresentar as implementações de avaliação do Microsoft Dynamics AX 2012 R3 num projeto dos serviços de ciclo de vida do Microsoft Dynamics que pertencem tooa utilizador|
|/lcsprojects/clouddeployments/Write|Crie implementação de avaliação do Microsoft Dynamics AX 2012 R3 num projeto dos serviços de ciclo de vida do Microsoft Dynamics que pertencem tooa utilizador. Implementações podem ser geridas a partir do portal de gestão do Azure|
|/lcsprojects/Connectors/Read|Os conectores que pertencem o projeto de serviços de ciclo de vida do Microsoft Dynamics tooa de leitura|
|/lcsprojects/Connectors/Write|Criar e atualizar os conectores que pertencem o projeto de serviços de ciclo de vida do Microsoft Dynamics tooa|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| Operação | Descrição |
|---|---|
|checkNameAvailability/ação|Verificações de disponibilidade de espaço de nomes em dada subscrição.|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos de EventHub Olá e permite Olá criação dos recursos de EventHub|
|espaços de nomes/escrita|Crie um recurso de espaço de nomes e Atualize as respetivas propriedades. As etiquetas e estado do espaço de nomes de Olá são propriedades de Olá que podem ser atualizadas.|
|/Namespaces/Read|Obter a lista de Olá da descrição de recursos do espaço de nomes|
|espaços de nomes/eliminar|Eliminar recurso do espaço de nomes|
|/Namespaces/metricDefinitions/Read|Obter a lista de descrições de recursos de métricas de espaço de nomes|
|/Namespaces/authorizationRules/Read|Obter a lista de Olá da descrição de regras de autorização de espaços de nomes.|
|/Namespaces/authorizationRules/Write|Criar regras de autorização ao nível de espaço de nomes e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/authorizationRules/DELETE|Elimine regra de autorização de espaço de nomes. Não é possível eliminar Olá regra de autorização de espaço de nomes predefinido. |
|/Namespaces/authorizationRules/listkeys/Action|Obter a cadeia de ligação de Olá toohello espaço de nomes|
|/Namespaces/authorizationRules/regenerateKeys/Action|Regenerar Olá principal ou secundário chave toohello recursos|
|/Namespaces/eventhubs/Write|Criar ou propriedades de EventHub de atualização.|
|/Namespaces/eventhubs/Read|Obter a lista de descrições de recursos de EventHub|
|/Namespaces/eventhubs/DELETE|Operação toodelete EventHub recursos|
|/Namespaces/eventHubs/consumergroups/Write|Criar ou atualizar ConsumerGroup propriedades.|
|/Namespaces/eventHubs/consumergroups/Read|Obter a lista de descrições de recurso ConsumerGroup|
|/Namespaces/eventHubs/consumergroups/DELETE|Operação toodelete ConsumerGroup recursos|
|/Namespaces/eventhubs/authorizationRules/Read| Obter a lista de Olá EventHub das regras de autorização|
|/Namespaces/eventhubs/authorizationRules/Write|Criar regras de autorização de EventHub e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/eventhubs/authorizationRules/DELETE|Operação toodelete regras de autorização de EventHub|
|/Namespaces/eventhubs/authorizationRules/listkeys/Action|Obter Olá tooEventHub de cadeia de ligação|
|/Namespaces/eventhubs/authorizationRules/regenerateKeys/Action|Regenerar Olá principal ou secundário chave toohello recursos|
|/Namespaces/diagnosticSettings/Read|Obter a lista de descrições de recursos de definições de diagnóstico de espaço de nomes|
|/Namespaces/diagnosticSettings/Write|Obter a lista de descrições de recursos de definições de diagnóstico de espaço de nomes|
|/Namespaces/logDefinitions/Read|Obter a lista de registos de espaço de nomes descrições de recursos|

## <a name="microsoftfeatures"></a>Microsoft.Features

| Operação | Descrição |
|---|---|
|/providers/Features/Read|Obtém a funcionalidade de Olá de uma subscrição de um fornecedor de recursos específico.|
|/providers/Features/register/Action|Regista a funcionalidade de Olá para uma subscrição de um fornecedor de recursos específico.|
|/Features/Read|Obtém as funcionalidades de Olá de uma subscrição.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| Operação | Descrição |
|---|---|
|clusters/escrita|Criar ou atualizar o Cluster do HDInsight|
|/clusters/Read|Obter detalhes sobre o Cluster do HDInsight|
|/clusters/DELETE|Eliminar um Cluster do HDInsight|
|/clusters/changerdpsetting/Action|Alteração da definição de RDP de Cluster do HDInsight|
|/clusters/Configurations/Action|Atualizar a configuração de Cluster do HDInsight|
|/clusters/Configurations/Read|Obter configurações de Cluster do HDInsight|
|/clusters/roles/resize/Action|Redimensionar um Cluster do HDInsight|
|/Locations/Capabilities/Read|Obter as funções da subscrição|
|/Locations/checkNameAvailability/Read|Verifique a disponibilidade de nome|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos de importação/exportação Olá e permite a criação de Olá de tarefas de importação/exportação.|
|/ tarefas/escrita|Cria uma tarefa com Olá parâmetros especificados ou atualizar propriedades de Olá ou etiquetas para a tarefa especificada Olá.|
|/Jobs/Read|Obtém as propriedades de Olá para trabalho especificado Olá ou devolve Olá lista de tarefas.|
|/Jobs/listBitLockerKeys/Action|Obtém as chaves do BitLocker Olá para trabalho especificado Olá.|
|/Jobs/DELETE|Elimina uma tarefa existente.|
|/Locations/Read|Obtém as propriedades de Olá para Olá localização ou devolve Olá lista especificada de localizações.|

## <a name="microsoftinsights"></a>Insights

| Operação | Descrição |
|---|---|
|/ Register/ação|Registar o fornecedor de insights Olá microsoft|
|/ AlertRules/escrita|Configuração de regra de alerta de tooan de escrita|
|/ AlertRules/eliminar|Eliminar uma configuração de regra de alerta|
|/ AlertRules/leitura|Ler uma configuração de regra de alerta|
|/ AlertRules/ativado/ação|Regra de alerta ativada|
|/ AlertRules/resolvido/ação|Regra de alerta resolvida|
|/ AlertRules/limitadas/ação|Regra de alerta é limitada|
|/ AlertRules/incidentes/leitura|Ler uma configuração de incidente de regra de alerta|
|/ MetricDefinitions/leitura|Definições de métrica de leitura|
|/eventtypes/Values/Read|Leia o artigo gestão valores do tipo de evento|
|/eventtypes/digestevents/Read|Resumo de tipo de evento de gestão de leitura|
|/ Métricas/leitura|Métricas de leitura|
|/ LogProfiles/escrita|Escrita de configuração do perfil de registo de tooa|
|/ LogProfiles/eliminar|Eliminar a configuração de perfis de registo|
|/ LogProfiles/leitura|Perfis de registo de leitura|
|/ AutoscaleSettings/escrita|Escrita de configuração de definição de dimensionamento automático tooan|
|/ AutoscaleSettings/eliminar|Eliminar uma configuração de definição de dimensionamento automático|
|/ AutoscaleSettings/leitura|Ler uma configuração de definição de dimensionamento automático|
|/ AutoscaleSettings/Scaleup/ação|Trabalho operação de dimensionamento de dimensionamento automático|
|/ AutoscaleSettings/Scaledown/ação|Escala de dimensionamento automático para baixo de operação|
|/AutoscaleSettings/Providers/Microsoft.Insights/MetricDefinitions/Read|Definições de métrica de leitura|
|/ ActivityLogAlerts/ativado/ação|Olá accionada alerta de registo de atividade|
|/ DiagnosticSettings/escrita|Configuração de definições de toodiagnostic de escrita|
|/ DiagnosticSettings/eliminar|Eliminar a configuração de definições de diagnóstico|
|/ DiagnosticSettings/leitura|Ler uma configuração de definições de diagnóstico|
|/ LogDefinitions/leitura|Definições de registo de leitura|
|/ ExtendedDiagnosticSettings/escrita|Configuração de definições de diagnóstico de tooextended de escrita|
|/ ExtendedDiagnosticSettings/eliminar|Eliminar a configuração de definições de diagnóstico expandida|
|/ ExtendedDiagnosticSettings/leitura|Ler uma configuração de definições de diagnóstico expandida|

## <a name="microsoftkeyvault"></a>Keyvault

| Operação | Descrição |
|---|---|
|registar/ação|Regista uma subscrição|
|/checkNameAvailability/Read|Verifica se um nome de cofre de chaves é válido e se não está em utilização|
|/vaults/Read|Ver Olá propriedades de um cofre de chaves|
|/ cofres/escrita|Criar um Olá nova chave de cofre ou atualizar propriedades de um cofre de chaves|
|/vaults/DELETE|Eliminar um cofre de chaves|
|/vaults/Deploy/Action|Permite aceder toosecrets no Cofre de chaves durante a implementação de recursos do Azure|
|/vaults/Secrets/Read|Ver Olá propriedades de um segredo, mas não o valor|
|/vaults/Secrets/Write|Crie um novo valor de Olá de segredo ou atualização de um segredo existente|
|/vaults/accessPolicies/Write|Atualizar uma política de acesso existente ao intercalar ou substituir, ou adicione um novo cofre de tooa de política de acesso.|
|/deletedVaults/Read|Ver propriedades de Olá de forma recuperável eliminado cofres de chaves|
|/Locations/operationResults/Read|Resultado da verificação Olá de uma operação de execução longa|
|/Locations/deletedVaults/Read|Ver Olá propriedades de um cofre de chaves eliminado recuperável|
|/Locations/deletedVaults/PURGE/Action|Remover um cofre de chaves eliminado recuperável|

## <a name="microsoftlogic"></a>Microsoft.Logic

| Operação | Descrição |
|---|---|
|/workflows/Read|Lê o fluxo de trabalho Olá.|
|fluxos de trabalho/escrita|Cria ou atualiza o fluxo de trabalho Olá.|
|/workflows/DELETE|Elimina o fluxo de trabalho Olá.|
|/workflows/Run/Action|Inicia a execução do fluxo de trabalho Olá.|
|/workflows/disable/Action|Desativa o fluxo de trabalho Olá.|
|/workflows/Enable/Action|Permite que o fluxo de trabalho Olá.|
|/workflows/Validate/Action|Valida o fluxo de trabalho Olá.|
|/workflows/move/Action|Move o fluxo de trabalho do respetivo existente id de subscrição, grupo de recursos e/ou o id de subscrição diferente do nome tooa, grupo de recursos e/ou nome.|
|/workflows/listSwagger/Action|Obtém o fluxo de trabalho Olá swagger definições.|
|/workflows/regenerateAccessKey/Action|Segredos de chave de acesso de Olá gera de novo.|
|/workflows/listCallbackUrl/Action|Obtém o URL de chamada de retorno de Olá de fluxo de trabalho.|
|/workflows/versions/Read|Lê a versão de fluxo de trabalho de Olá.|
|/workflows/versions/triggers/listCallbackUrl/Action|Obtém o URL de chamada de retorno de Olá para o acionador.|
|fluxos de trabalho/executa/leitura|Lê o fluxo de trabalho de Olá executar.|
|/workflows/runs/Cancel/Action|Cancela a execução de Olá de um fluxo de trabalho.|
|/workflows/runs/Actions/Read|Lê o fluxo de trabalho de Olá executar uma ação.|
|/workflows/runs/Operations/Read|Lê o fluxo de trabalho de Olá executar o estado da operação.|
|/workflows/triggers/Read|Lê o acionador de Olá.|
|/workflows/triggers/Run/Action|Executa o acionador de Olá.|
|/workflows/triggers/listCallbackUrl/Action|Obtém o URL de chamada de retorno de Olá para o acionador.|
|/workflows/triggers/histories/Read|Lê histories de Acionador de Olá.|
|/workflows/triggers/histories/resubmit/Action|Resubmits acionador do fluxo de trabalho de Olá.|
|/workflows/accessKeys/Read|Lê a chave de acesso de Olá.|
|/workflows/accessKeys/Write|Cria ou atualiza a chave de acesso de Olá.|
|/workflows/accessKeys/DELETE|Elimina a chave de acesso de Olá.|
|/workflows/accessKeys/List/Action|Apresenta uma lista de segredos de chave de acesso de Olá.|
|/workflows/accessKeys/Regenerate/Action|Segredos de chave de acesso de Olá gera de novo.|
|/Locations/workflows/Validate/Action|Valida o fluxo de trabalho Olá.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos do serviço web de aprendizagem de Olá e permite Olá criação de serviços web.|
|webServices/ação|Criar as propriedades do serviço Web regional para as regiões suportadas|
|/commitmentPlans/Read|Ler qualquer compromisso plano de aprendizagem|
|/ commitmentPlans/escrita|Criar ou atualizar qualquer plano de compromisso do Machine Learning|
|/commitmentPlans/DELETE|Eliminar qualquer compromisso plano de aprendizagem|
|/commitmentPlans/JOIN/Action|Aderir a qualquer máquina compromisso plano de aprendizagem|
|/commitmentPlans/commitmentAssociations/Read|Qualquer do Machine Learning compromisso plano de associação de leitura|
|/commitmentPlans/commitmentAssociations/move/Action|Mover quaisquer do Machine Learning compromisso plano de associação|
|/ Áreas de trabalho/leitura|Ler qualquer área de trabalho de aprendizagem|
|/ Áreas de trabalho/escrita|Criar ou atualizar qualquer área de trabalho de aprendizagem|
|/ Áreas de trabalho/eliminar|Eliminar qualquer área de trabalho de aprendizagem|
|/ Áreas de trabalho/listworkspacekeys/ação|Lista de chaves para uma área de trabalho do Machine Learning|
|/ Áreas de trabalho/resyncstoragekeys/ação|Ressincronizar chaves de conta de armazenamento configurada para uma área de trabalho do Machine Learning|
|/webServices/Read|Ler a qualquer serviço Web do Machine Learning|
|/ webServices/escrita|Criar ou atualizar qualquer serviço Web do Machine Learning|
|/webServices/DELETE|Eliminar qualquer serviço Web do Machine Learning|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| Operação | Descrição |
|---|---|
|/agreements/offers/plans/Read|Devolver um contrato de um item do marketplace indicado|
|/agreements/offers/plans/Sign/Action|Assinar um contrato de um item do marketplace indicado|
|/agreements/offers/plans/Cancel/Action|Cancelar um contrato de um item do marketplace indicado|

## <a name="microsoftmedia"></a>Microsoft.Media

| Operação | Descrição |
|---|---|
|/mediaservices/Read||
|/ mediaservices/escrita||
|/mediaservices/DELETE||
|/mediaservices/regenerateKey/Action||
|/mediaservices/listKeys/Action||
|/mediaservices/syncStorageKeys/Action||

## <a name="microsoftnetwork"></a>Microsoft.Network

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição de Olá|
|ação de anular o registo /|Anula o registo da subscrição Olá|
|checkTrafficManagerNameAvailability/ação|Verifica a disponibilidade de Olá de um nome de DNS de caminho relativo do Gestor de tráfego.|
|/dnszones/Read|Obtenha a zona DNS Olá, no formato JSON. Propriedades da zona Olá incluem as etiquetas, etag, numberOfRecordSets e maxNumberOfRecordSets. Tenha em atenção que este comando não obter conjuntos de registos de Olá contidos na zona de Olá.|
|/ dnszones/escrita|Crie ou Atualize uma zona DNS dentro de um grupo de recursos.  Olá utilizados tooupdate etiquetas num recurso de zona DNS. Tenha em atenção que este comando não pode ser utilizados toocreate ou atualizar conjuntos de registos na zona de Olá.|
|/dnszones/DELETE|Elimine a zona DNS de Olá, no formato JSON. Propriedades da zona Olá incluem as etiquetas, etag, numberOfRecordSets e maxNumberOfRecordSets.|
|/dnszones/MX/Read|Obter conjunto de registos de Olá do tipo "MX", no formato JSON. conjunto de registos de Olá contém uma lista de registos, bem como Olá TTL, as etiquetas e etag.|
|/dnszones/MX/Write|Crie ou Atualize um conjunto de registos do tipo "MX" dentro de uma zona DNS. registos de Olá especificados irão substituir os registos de atuais de Olá no conjunto de registos de Olá.|
|/dnszones/MX/DELETE|Remova o conjunto de registos de Olá de um determinado nome e tipo "MX" de uma zona DNS.|
|/dnszones/NS/Read|Obtém o conjunto de registos de DNS do tipo NS|
|/dnszones/NS/Write|Cria ou atualiza o conjunto de registos de DNS do tipo NS|
|/dnszones/NS/DELETE|Elimina o conjunto de registos de DNS de Olá do tipo NS|
|/dnszones/aaaa/Read|Obter conjunto de registos de Olá do tipo "AAAA", no formato JSON. conjunto de registos de Olá contém uma lista de registos, bem como Olá TTL, as etiquetas e etag.|
|/dnszones/aaaa/Write|Crie ou Atualize um conjunto de registos do tipo "AAAA" dentro de uma zona DNS. registos de Olá especificados irão substituir os registos de atuais de Olá no conjunto de registos de Olá.|
|/dnszones/aaaa/DELETE|Remova o conjunto de registos de Olá de um determinado nome e tipo "AAAA" de uma zona DNS.|
|/dnszones/CNAME/Read|Obter conjunto de registos de Olá do tipo "CNAME", no formato JSON. conjunto de registos de Olá contém Olá TTL, as etiquetas e etag.|
|/dnszones/CNAME/Write|Crie ou Atualize um conjunto de registos do tipo "CNAME" dentro de uma zona DNS. registos de Olá especificados irão substituir os registos de atuais de Olá no conjunto de registos de Olá.|
|/dnszones/CNAME/DELETE|Remova o conjunto de registos de Olá de um determinado nome e tipo "CNAME" de uma zona DNS.|
|/dnszones/SOA/Read|Obtém o conjunto de registos DNS do tipo SOA|
|/dnszones/SOA/Write|Cria ou atualiza o conjunto de registos DNS do tipo SOA|
|/dnszones/SRV/Read|Obter conjunto de registos de Olá do tipo "SRV", no formato JSON. conjunto de registos de Olá contém uma lista de registos, bem como Olá TTL, as etiquetas e etag.|
|/dnszones/SRV/Write|Criar ou atualizar conjunto de registos do tipo SRV|
|/dnszones/SRV/DELETE|Remova o conjunto de registos de Olá de um determinado nome e tipo "SRV" de uma zona DNS.|
|/dnszones/PTR/Read|Obter conjunto de registos de Olá do tipo "PTR", no formato JSON. conjunto de registos de Olá contém uma lista de registos, bem como Olá TTL, as etiquetas e etag.|
|/dnszones/PTR/Write|Crie ou Atualize um conjunto de registos do tipo "PTR" dentro de uma zona DNS. registos de Olá especificados irão substituir os registos de atuais de Olá no conjunto de registos de Olá.|
|/dnszones/PTR/DELETE|Remova o conjunto de registos de Olá de um determinado nome e tipo "PTR" de uma zona DNS.|
|/dnszones/A/Read|Obter conjunto de registos de Olá do tipo "A", no formato JSON. conjunto de registos de Olá contém uma lista de registos, bem como Olá TTL, as etiquetas e etag.|
|/dnszones/A/Write|Crie ou Atualize um conjunto de registos do tipo 'A' dentro de uma zona DNS. registos de Olá especificados irão substituir os registos de atuais de Olá no conjunto de registos de Olá.|
|/dnszones/A/DELETE|Remova o conjunto de registos de Olá de um determinado nome e o tipo A partir de uma zona DNS.|
|/dnszones/txt/Read|Obter conjunto de registos de Olá do tipo "TXT", no formato JSON. conjunto de registos de Olá contém uma lista de registos, bem como Olá TTL, as etiquetas e etag.|
|/dnszones/txt/Write|Crie ou Atualize um conjunto de registos do tipo "TXT" dentro de uma zona DNS. registos de Olá especificados irão substituir os registos de atuais de Olá no conjunto de registos de Olá.|
|/dnszones/txt/DELETE|Remova o conjunto de registos de Olá de um determinado nome e tipo "TXT" de uma zona DNS.|
|/dnszones/recordsets/Read|Obtém os conjuntos de registos de DNS em tipos|
|/networkInterfaces/Read|Obtém uma definição de interface de rede. |
|nomes de networkInterfaces/escrita|Cria uma interface de rede ou atualiza uma interface de rede existente. |
|/networkInterfaces/JOIN/Action|Associa uma interface de rede de tooa de Máquina Virtual|
|/networkInterfaces/DELETE|Elimina uma interface de rede|
|/networkInterfaces/effectiveRouteTable/Action|Obter tabela de rotas configurado na Interface de rede de Olá Vm|
|/networkInterfaces/effectiveNetworkSecurityGroups/Action|Obter grupos de segurança de rede configurada na rede Interface de Olá Vm|
|/networkInterfaces/loadBalancers/Read|Obtém todos os balanceadores de carga Olá Olá interface de rede faz parte|
|/networkInterfaces/ipconfigurations/Read|Obtém uma definição de configuração de ip de interface de rede. |
|/publicIPAddresses/Read|Obtém uma definição de endereço ip público.|
|/ publicIPAddresses/escrita|Cria um endereço Ip público ou atualiza um endereço Ip público existente. |
|/publicIPAddresses/DELETE|Elimina um endereço Ip público.|
|/publicIPAddresses/JOIN/Action|Associa um endereço ip público|
|/routeFilters/Read|Obtém uma definição de filtro de rota|
|/routeFilters/JOIN/Action|Associa um filtro de rota|
|/routeFilters/DELETE|Elimina uma definição de filtro de rota|
|/ routeFilters/escrita|Cria um filtro de rota ou atualiza um filtro já existente|
|/routeFilters/Rules/Read|Obtém a definição de uma regra de filtro de rota|
|/routeFilters/Rules/Write|Cria uma regra de filtro de rota ou atualiza uma regra de filtro de rota existente|
|/routeFilters/Rules/DELETE|Elimina a definição de uma regra de filtro de rota|
|/networkWatchers/Read|Obter a definição de observador de rede Olá|
|/ networkWatchers/escrita|Cria um observador de rede ou atualiza um observador de rede existente|
|/networkWatchers/DELETE|Elimina um observador de rede|
|/networkWatchers/configureFlowLog/Action|Configura o registo de fluxo para um recurso de destino.|
|/networkWatchers/ipFlowVerify/Action|Devolve se pacotes hello é permitido ou negado tooor de um destino específico.|
|/networkWatchers/nextHop/Action|Para um destino especificado e o endereço IP de destino, devolver o tipo de salto seguinte Olá e hope seguinte endereço IP.|
|/networkWatchers/queryFlowLogStatus/Action|Obtém o estado de Olá do fluxo de registo num recurso.|
|/networkWatchers/queryTroubleshootResult/Action|Obtém Olá resultado de Olá anteriormente executados ou atualmente em execução operação de resolução de problemas de resolução de problemas.|
|/networkWatchers/securityGroupView/Action|Ver Olá configuradas e aplicadas numa VM de regras de grupo de segurança de rede eficiente.|
|/networkWatchers/Topology/Action|Obtém uma vista de nível de rede de recursos e as respetivas relações num grupo de recursos.|
|/networkWatchers/Troubleshoot/Action|Inicia a resolução de problemas num recurso de rede no Azure.|
|/networkWatchers/packetCaptures/queryStatus/Action|Obtém informações sobre as propriedades e estado de um recurso de captura de pacotes.|
|/networkWatchers/packetCaptures/Stop/Action|Pare Olá com a sessão de captura de pacotes.|
|/networkWatchers/packetCaptures/Read|Obter a definição de captura de pacotes de Olá|
|/networkWatchers/packetCaptures/Write|Cria uma captura de pacotes|
|/networkWatchers/packetCaptures/DELETE|Elimina uma captura de pacotes|
|/loadBalancers/Read|Obtém uma definição de Balanceador de carga|
|/ loadBalancers/escrita|Cria um balanceador de carga ou atualiza um balanceador de carga existente|
|/loadBalancers/DELETE|Elimina um balanceador de carga|
|/loadBalancers/networkInterfaces/Read|Obtém as referências de interfaces de rede Olá tooall um balanceador de carga|
|/loadBalancers/loadBalancingRules/Read|Obtém uma definição de regra balanceamento de carga Balanceador de carga|
|/loadBalancers/backendAddressPools/Read|Obtém uma definição de conjunto de endereços de back-end de Balanceador de carga|
|/loadBalancers/backendAddressPools/JOIN/Action|Associa um conjunto de endereços de back-end de Balanceador de carga|
|/loadBalancers/inboundNatPools/Read|Obtém um balanceador de carga definição do conjunto nat de entrada|
|/loadBalancers/inboundNatPools/JOIN/Action|Associa um balanceador de carga conjunto nat de entrada|
|/loadBalancers/inboundNatRules/Read|Obtém um balanceador de carga definição da regra nat de entrada|
|/loadBalancers/inboundNatRules/Write|Cria uma regra de nat de entrada do Balanceador de carga ou atualiza uma regra nat de entrada do Balanceador de carga existente|
|/loadBalancers/inboundNatRules/DELETE|Elimina uma regra de nat de entrada do Balanceador de carga|
|/loadBalancers/inboundNatRules/JOIN/Action|Associa uma regra de nat de entrada do Balanceador de carga|
|/loadBalancers/outboundNatRules/Read|Obtém uma definição de regra de nat de saída de Balanceador de carga|
|/loadBalancers/probes/Read|Obtém uma sonda do Balanceador de carga|
|/loadBalancers/virtualMachines/Read|Obtém as referências tooall Olá máquinas virtuais num Balanceador de carga|
|/loadBalancers/frontendIPConfigurations/Read|Obtém uma definição de configuração de IP de front-end de Balanceador de carga|
|/trafficManagerGeographicHierarchies/Read|Obtém o Olá Gestor de tráfego Geographic hierarquia que contém regiões que podem ser utilizadas com Olá método de encaminhamento de tráfego geográfica|
|/bgpServiceCommunities/Read|Obter Comunidades de Bgp de serviço|
|/applicationGatewayAvailableWafRuleSets/Read|Obtém o Gateway de aplicação define a regra de Waf disponíveis|
|/virtualNetworks/Read|Obter a definição de rede virtual Olá|
|/ virtualNetworks/escrita|Cria uma rede virtual ou atualiza uma rede virtual existente|
|/virtualNetworks/DELETE|Elimina uma rede virtual|
|/virtualNetworks/peer/Action|Peers uma rede virtual com a outra rede virtual|
|/virtualNetworks/virtualNetworkPeerings/Read|Obtém uma definição de peering de rede virtual|
|/virtualNetworks/virtualNetworkPeerings/Write|Cria um peering de rede virtual ou atualiza um peering de rede virtual existente|
|/virtualNetworks/virtualNetworkPeerings/DELETE|Elimina um peering de rede virtual|
|/virtualNetworks/Subnets/Read|Obtém uma definição de sub-rede de rede virtual|
|/virtualNetworks/Subnets/Write|Cria uma sub-rede de rede virtual ou atualiza uma sub-rede de rede virtual existente|
|/virtualNetworks/Subnets/DELETE|Elimina uma sub-rede de rede virtual|
|/virtualNetworks/Subnets/JOIN/Action|Associa uma rede virtual|
|/virtualNetworks/Subnets/joinViaServiceTunnel/Action|Associa os recursos, tais como a conta de armazenamento ou SQL Server da base de dados tooa serviço túnel ativada sub-rede.|
|/virtualNetworks/Subnets/virtualMachines/Read|Obtém as referências Olá tooall máquinas virtuais numa sub-rede de rede virtual|
|/virtualNetworks/checkIpAddressAvailability/Read|Verifique se o endereço Ip está disponível na rede virtual especificado de Olá|
|/virtualNetworks/virtualMachines/Read|Obtém as referências Olá tooall máquinas virtuais numa rede virtual|
|/expressRouteServiceProviders/Read|Obtém os fornecedores de serviços de Expressroute|
|/dnsoperationresults/Read|Obtém os resultados de uma operação de DNS|
|/localnetworkgateways/Read|Obtém LocalNetworkGateway|
|/ localnetworkgateways/escrita|Cria ou atualiza um LocalNetworkGateway existente|
|/localnetworkgateways/DELETE|Elimina LocalNetworkGateway|
|/trafficManagerProfiles/Read|Obter a configuração de perfil do Gestor de tráfego de Olá. Isto inclui as definições DNS, as definições de encaminhamento de tráfego, as definições de monitorização do ponto final e lista Olá de pontos finais encaminhados por este perfil do Traffic Manager.|
|/ trafficManagerProfiles/escrita|Criar um perfil de Gestor de tráfego ou modificar a configuração de Olá de um perfil do Traffic Manager existente. Isto inclui ativar ou desativar um perfil e modificar as definições de DNS, as definições de encaminhamento de tráfego ou as definições de monitorização do ponto final. Os pontos finais encaminhados pelo perfil do Traffic Manager Olá podem ser adicionados, removidos, ativados ou desativados.|
|/trafficManagerProfiles/DELETE|Elimine perfil do Gestor de tráfego de Olá. Todas as definições associadas Olá perfil do Gestor de tráfego serão perdidas e perfil Olá já não pode ser utilizado tooroute tráfego.|
|/dnsoperationstatuses/Read|Obtém o estado de uma operação de DNS |
|/Operations/Read|Obter operações disponíveis|
|/expressRouteCircuits/Read|Obter um ExpressRouteCircuit|
|/ expressRouteCircuits/escrita|Cria ou atualiza um ExpressRouteCircuit existente|
|/expressRouteCircuits/DELETE|Elimina um ExpressRouteCircuit|
|/expressRouteCircuits/Stats/Read|Obtém um ExpressRouteCircuit Stat|
|/expressRouteCircuits/peerings/Read|Obtém um ExpressRouteCircuit Peering|
|/expressRouteCircuits/peerings/Write|Cria ou atualiza um ExpressRouteCircuit Peering existente|
|/expressRouteCircuits/peerings/DELETE|Elimina um ExpressRouteCircuit Peering|
|/expressRouteCircuits/peerings/arpTables/Action|Obtém um ArpTable ExpressRouteCircuit de Peering|
|/expressRouteCircuits/peerings/routeTables/Action|Obtém um RouteTable ExpressRouteCircuit de Peering|
|/expressRouteCircuits/peerings /<br>routeTablesSummary/ação|Obtém um resumo de RouteTable Peering ExpressRouteCircuit|
|/expressRouteCircuits/peerings/Stats/Read|Obtém um ExpressRouteCircuit Peering Stat|
|/expressRouteCircuits/Authorizations/Read|Obtém uma ExpressRouteCircuit autorização|
|/expressRouteCircuits/Authorizations/Write|Cria ou atualiza uma autorização ExpressRouteCircuit existente|
|/expressRouteCircuits/Authorizations/DELETE|Elimina uma ExpressRouteCircuit autorização|
|/Connections/Read|Obtém o VirtualNetworkGatewayConnection|
|ligações/escrita|Cria ou atualiza um VirtualNetworkGatewayConnection existente|
|/Connections/DELETE|Elimina o VirtualNetworkGatewayConnection|
|/Connections/sharedKey/Read|Obtém o VirtualNetworkGatewayConnection SharedKey|
|/Connections/sharedKey/Write|Cria ou atualiza um VirtualNetworkGatewayConnection SharedKey existente|
|/networkSecurityGroups/Read|Obtém uma definição de grupo de segurança de rede|
|/ networkSecurityGroups/escrita|Cria um grupo de segurança de rede ou atualiza um grupo de segurança de rede existente|
|/networkSecurityGroups/DELETE|Elimina um grupo de segurança de rede|
|/networkSecurityGroups/JOIN/Action|Associa um grupo de segurança de rede|
|/networkSecurityGroups/defaultSecurityRules/Read|Obtém uma definição de regra de segurança predefinida|
|/networkSecurityGroups/securityRules/Read|Obtém a definição de uma regra de segurança|
|/networkSecurityGroups/securityRules/Write|Cria uma regra de segurança ou atualiza uma regra de segurança existente|
|/networkSecurityGroups/securityRules/DELETE|Elimina uma regra de segurança|
|/applicationGateways/Read|Obtém um gateway de aplicação|
|/ applicationGateways/escrita|Cria um gateway de aplicação ou atualiza um gateway de aplicação|
|/applicationGateways/DELETE|Elimina um gateway de aplicação|
|/applicationGateways/backendhealth/Action|Obtém um funcionamento de back-end do gateway de aplicação|
|/applicationGateways/Start/Action|Inicia um gateway de aplicação|
|/applicationGateways/Stop/Action|Parar um gateway de aplicação|
|/applicationGateways/backendAddressPools/JOIN/Action|Associa um conjunto de endereços de back-end de gateway de aplicação|
|/routeTables/Read|Obtém uma definição de tabela de rota|
|/ routeTables/escrita|Cria uma tabela de rotas ou atualiza uma tabela já existente|
|/routeTables/DELETE|Elimina uma definição de tabela de rota|
|/routeTables/JOIN/Action|Junta a tabela de rotas|
|/routeTables/routes/Read|Obtém uma definição de rota|
|/routeTables/routes/Write|Cria uma rota ou atualiza uma já existente|
|/routeTables/routes/DELETE|Elimina uma definição de rota|
|/Locations/operationResults/Read|Obtém o resultado de um async POST ou operação de eliminação|
|/Locations/checkDnsNameAvailability/Read|Verifica se a etiqueta de dns está disponível em Olá especificado localização|
|/Locations/usages/Read|Obtém a métrica de utilização de recursos de Olá|
|/Locations/Operations/Read|Obtém o recurso da operação que representa o estado de uma operação assíncrona|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos de NotifciationHubs Olá e permite a criação de Olá de espaços de nomes e Notification hubs|
|/ CheckNamespaceAvailability/ação|Verifica se é ou não um nome de recurso indicado do espaço de nomes disponível dentro de Olá NotificationHub serviço.|
|/ Espaços de nomes/escrita|Crie um recurso de espaço de nomes e Atualize as respetivas propriedades. As etiquetas e estado do espaço de nomes de Olá são propriedades de Olá que podem ser atualizadas.|
|/ Espaços de nomes/leitura|Obter a lista de Olá da descrição de recursos do espaço de nomes|
|/ Espaços de nomes/eliminar|Eliminar recurso do espaço de nomes|
|/ Espaços de nomes/authorizationRules/ação|Obter a lista de Olá da descrição de regras de autorização de espaços de nomes.|
|/ Espaços de nomes/CheckNotificationHubAvailability/ação|Verifica se é ou não um determinado nome de NotificationHub disponível dentro de um espaço de nomes.|
|/ Espaços de nomes/authorizationRules/escrita|Criar regras de autorização ao nível de espaço de nomes e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/ Espaços de nomes/authorizationRules/leitura|Obter a lista de Olá da descrição de regras de autorização de espaços de nomes.|
|/ Espaços de nomes/authorizationRules/eliminar|Elimine regra de autorização de espaço de nomes. Não é possível eliminar Olá regra de autorização de espaço de nomes predefinido. |
|/ Espaços de nomes/authorizationRules/listkeys/ação|Obter a cadeia de ligação de Olá toohello espaço de nomes|
|/ Espaços de nomes/authorizationRules/regenerateKeys/ação|Espaço de nomes autorização regra regenerar principal/SecondaryKey, especifique Olá chave que necessita de toobe regenerada|
|/ Espaços de nomes/NotificationHubs/escrita|Criar um Hub de notificação e atualizar as respetivas propriedades. As respetivas propriedades incluem principalmente PNS credenciais. Regras de autorização e TTL|
|/ Espaços de nomes/NotificationHubs/leitura|Obter a lista de descrições de recursos de Hub de notificação|
|/ Espaços de nomes/NotificationHubs/eliminar|Eliminar recurso do Hub de notificação|
|/ Espaços de nomes/NotificationHubs/authorizationRules/ação|Obter a lista de Olá das regras de autorização de Hub de notificação|
|/ Espaços de nomes/NotificationHubs/pnsCredentials/ação|Obter todas as credenciais PNS do Hub de notificação. Isto inclui as credenciais do WNS, o MPNS, o APNS, o GCM e o Baidu|
|/ Espaços de nomes/NotificationHubs/debugSend/ação|Envie uma notificação push de teste.|
|/ Espaços de nomes/NotificationHubs/metricDefinitions/leitura|Obter a lista de descrições de recursos de métricas de espaço de nomes|
|/Namespaces/NotificationHubs /<br>authorizationRules/escrita|Criar regras de autorização de Hub de notificação e atualizar as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/NotificationHubs /<br>authorizationRules/leitura|Obter a lista de Olá das regras de autorização de Hub de notificação|
|/Namespaces/NotificationHubs /<br>authorizationRules/eliminar|Eliminar regras de autorização de Hub de notificação|
|/Namespaces/NotificationHubs /<br>listkeys/authorizationRules/ação|Obter a cadeia de ligação de Olá toohello Notification Hub|
|/Namespaces/NotificationHubs /<br>regenerateKeys/authorizationRules/ação|Notification Hub autorização regra regenerar principal/SecondaryKey, especifique Olá chave que necessita de toobe regenerada|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| Operação | Descrição |
|---|---|
|registar/ação|Registe um fornecedor de recursos de tooa de subscrição.|
|/linkTargets/Read|Apresenta uma lista de contas existentes que não estão associadas uma subscrição do Azure. toolink esta área de trabalho de tooa de subscrição do Azure, utilize um id de cliente devolvido por esta operação na propriedade de id de cliente Olá de Olá operação da área de trabalho de criar.|
|/ áreas de trabalho/escrita|Cria uma nova área de trabalho ou a área de trabalho existente ligações tooan fornecendo o id de cliente Olá da área de trabalho existente Olá.|
|/Workspaces/Read|Obtém uma área de trabalho existente|
|/Workspaces/DELETE|Elimina uma área de trabalho. Se a área de trabalho Olá foi ligada a área de trabalho existente do tooan no momento da criação, em seguida, Olá área de trabalho foi ligado toois não eliminar.|
|/Workspaces/generateregistrationcertificate/Action|Gera o certificado de registo para a área de trabalho Olá. Este certificado é utilizado tooconnect Microsoft System Center Operation Manager toohello área.|
|/Workspaces/sharedKeys/Action|Obtém as chaves de Olá partilhado para a área de trabalho Olá. Estas chaves são utilizadas tooconnect informações operacionais do Microsoft agentes toohello área de trabalho.|
|/Workspaces/Search/Action|Executa uma consulta de pesquisa|
|/Workspaces/DataSources/Read|Obter as origens de dados na área de trabalho.|
|/Workspaces/DataSources/Write|Criar/atualizar as origens de dados na área de trabalho.|
|/Workspaces/DataSources/DELETE|Elimine as origens de dados na área de trabalho.|
|/Workspaces/managementGroups/Read|Obtém os nomes de Olá e metadados para a área de trabalho do System Center Operations Manager management grupos toothis ligado.|
|/Workspaces/Schema/Read|Obtém o esquema de pesquisa de Olá para área de trabalho Olá.  Esquema de pesquisa inclui campos Olá exposto e os respetivos tipos.|
|/Workspaces/usages/Read|Obtém dados de utilização de uma área de trabalho, incluindo a quantidade de Olá de dados lidos pelo área de trabalho Olá.|
|/Workspaces/intelligencepacks/Read|Apresenta uma lista de todos os pacotes de intelligence que estão visíveis para um determinado worksapce e também indica se o pacote de Olá está ativado ou desativado para essa área de trabalho.|
|/Workspaces/intelligencepacks/Enable/Action|Permite que um pacote de análise para uma área de trabalho especificado.|
|/Workspaces/intelligencepacks/disable/Action|Desativa um pacote de análise para uma área de trabalho especificado.|
|/Workspaces/sharedKeys/Read|Obtém as chaves de Olá partilhado para a área de trabalho Olá. Estas chaves são utilizadas tooconnect informações operacionais do Microsoft agentes toohello área de trabalho.|
|/Workspaces/savedSearches/Read|Obtém uma consulta de pesquisa guardada|
|/Workspaces/savedSearches/Write|Cria uma consulta de pesquisa guardada|
|/Workspaces/savedSearches/DELETE|Elimina uma consulta de pesquisa guardada|
|/Workspaces/storageinsightconfigs/Write|Cria uma nova configuração de armazenamento. Estas configurações são utilizados toopull dados a partir de uma localização de uma conta de armazenamento existente.|
|/Workspaces/storageinsightconfigs/Read|Obtém uma configuração de armazenamento.|
|/Workspaces/storageinsightconfigs/DELETE|Elimina uma configuração de armazenamento. Isto irá parar informações operacionais do Microsoft da leitura de dados a partir da conta de armazenamento Olá.|
|/Workspaces/configurationScopes/Read|Obter o âmbito de configuração|
|/Workspaces/configurationScopes/Write|Definir âmbito de configuração|
|/Workspaces/configurationScopes/DELETE|Eliminar âmbito de configuração|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| Operação | Descrição |
|---|---|
|registar/ação|Registe um fornecedor de recursos de tooa de subscrição.|
|soluções/escrita|Criar nova solução do OMS|
|/Solutions/Read|Obter a sair com a solução do OMS|
|/Solutions/DELETE|Eliminar a solução existente do OMS|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| Operação | Descrição |
|---|---|
|/ Cofres/backupJobsExport/ação|Tarefas de exportação|
|/ Cofres/escrita|A operação Criar Cofre cria um recurso do tipo "cofre" do Azure|
|/ Cofres/leitura|Olá operação obter cofre obtém um objeto que representa Olá recursos do Azure do tipo 'cofre'|
|/ Cofres/eliminar|Olá eliminar cofre operação eliminações Olá especificado recursos do Azure do tipo 'cofre'|
|/ Cofres/refreshContainers/leitura|Atualiza a lista de contentor Olá|
|/ Cofres/backupJobsExport/operationResults/leitura|Olá devolve resultados exportar tarefa a operação.|
|/ Cofres/backupOperationResults/leitura|Devolve o Resultado da Operação da Cópia de Segurança do Cofre de Serviços de Recuperação.|
|/ Cofres/monitoringAlerts/leitura|Obtém os alertas de Olá para o Cofre de serviços de recuperação Olá.|
|/Vaults monitoringAlerts / {uniqueAlertId} / leitura|Obtém Olá os detalhes do alerta Olá.|
|/ Cofres/backupSecurityPIN/leitura|Devolve a segurança PIN Cofre de serviços de informação para recuperação.|
|/vaults/replicationEvents/Read|Ler quaisquer eventos|
|/ Cofres/backupProtectableItems/leitura|Devolve a lista de todos os Itens Susceptíveis de Proteção.|
|/vaults/replicationFabrics/Read|Ler todos os recursos de infraestrutura|
|/vaults/replicationFabrics/Write|Criar ou atualizar quaisquer recursos de infraestrutura|
|/vaults/replicationFabrics/remove/Action|Remover recursos de infraestrutura|
|/vaults/replicationFabrics/checkConsistency/Action|Verificações de consistência de Olá recursos de infraestrutura|
|/vaults/replicationFabrics/DELETE|Elimine quaisquer recursos de infraestrutura|
|/vaults/replicationFabrics/renewcertificate/Action||
|/vaults/replicationFabrics/deployProcessServerImage/Action|Implementar a imagem de servidor de processo|
|/vaults/replicationFabrics/reassociateGateway/Action|Reassociar Gateway|
|/ cofres replicationFabrics/replicationRecoveryServicesProviders /<br>Leitura|Ler quaisquer fornecedores de serviços de recuperação|
|/ cofres replicationFabrics/replicationRecoveryServicesProviders /<br>remover/ação|Remover o fornecedor de serviços de recuperação|
|/ cofres replicationFabrics/replicationRecoveryServicesProviders /<br>eliminar|Eliminar quaisquer fornecedores de serviços de recuperação|
|/ cofres replicationFabrics/replicationRecoveryServicesProviders /<br>refreshProvider/ação|Atualize o fornecedor|
|/vaults/replicationFabrics/replicationStorageClassifications/Read|Ler as classificações de armazenamento|
|/ cofres replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/leitura|Ler quaisquer mapeamentos de classificação de armazenamento|
|/ cofres replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/escrita|Criar ou atualizar quaisquer mapeamentos de classificação de armazenamento|
|/ cofres replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/eliminar|Eliminar quaisquer mapeamentos de classificação de armazenamento|
|/vaults/replicationFabrics/replicationvCenters/Read|Ler todas as tarefas|
|/vaults/replicationFabrics/replicationvCenters/Write|Criar ou atualizar todas as tarefas|
|/vaults/replicationFabrics/replicationvCenters/DELETE|Eliminar todas as tarefas|
|/vaults/replicationFabrics/replicationNetworks/Read|Ler a quaisquer redes|
|/ cofres replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/leitura|Leia os mapeamentos de rede|
|/ cofres replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/escrita|Criar ou atualizar quaisquer mapeamentos de rede|
|/ cofres replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/eliminar|Eliminar quaisquer mapeamentos de rede|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>Leitura|Leu os contentores de proteção|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>discoverProtectableItem/ação|Detetar o Item Protegível|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>escrita|Criar ou atualizar quaisquer contentores de proteção|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>remover/ação|Remover o contentor de proteção|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>switchprotection/ação|Contentor de proteção do comutador|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>replicationProtectableItems/leitura|Ler quaisquer itens passíveis de proteção|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/leitura|Ler quaisquer mapeamentos de contentor de proteção|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/escrita|Criar ou atualizar quaisquer mapeamentos de contentor de proteção|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>remover/replicationProtectionContainerMappings/ação|Remova o mapeamento de contentor de proteção|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/eliminar|Eliminar quaisquer mapeamentos de contentor de proteção|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/leitura|Ler os itens protegidos|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/escrita|Criar ou atualizar quaisquer itens protegidos|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/eliminar|Eliminar os itens protegidos|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>remover/replicationProtectedItems/ação|Remover o Item protegido|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>plannedFailover/replicationProtectedItems/ação|Ativação pós-falha planeada|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>unplannedFailover/replicationProtectedItems/ação|Ativação pós-falha|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>testFailover/replicationProtectedItems/ação|Ativação pós-falha de teste|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>testFailoverCleanup/replicationProtectedItems/ação|Limpeza da ativação pós-falha de teste|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>failoverCommit/replicationProtectedItems/ação|Consolidação de ativação pós-falha|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>Reproteção/replicationProtectedItems/ação|Proteja o Item protegido|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>updateMobilityService/replicationProtectedItems/ação|Serviço de mobilidade de atualização|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>repairReplication/replicationProtectedItems/ação|Reparar a replicação|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>applyRecoveryPoint/replicationProtectedItems/ação|Aplicar o ponto de recuperação|
|/ cofres replicationFabrics/replicationProtectionContainers /<br>recoveryPoints/replicationProtectedItems/leitura|Pontos de recuperação de replicação de leitura|
|/vaults/replicationPolicies/Read|Ler todas as políticas|
|/vaults/replicationPolicies/Write|Criar ou atualizar as políticas|
|/vaults/replicationPolicies/DELETE|Eliminar todas as políticas|
|/vaults/replicationRecoveryPlans/Read|Leia os planos de recuperação|
|/vaults/replicationRecoveryPlans/Write|Criar ou atualizar quaisquer planos de recuperação|
|/vaults/replicationRecoveryPlans/DELETE|Eliminar quaisquer planos de recuperação|
|/vaults/replicationRecoveryPlans/plannedFailover/Action|Plano de recuperação de ativação pós-falha planeada|
|/vaults/replicationRecoveryPlans/unplannedFailover/Action|Plano de recuperação de ativação pós-falha|
|/vaults/replicationRecoveryPlans/testFailover/Action|Plano de recuperação de ativação pós-falha de teste|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/Action|Plano de recuperação de limpeza da ativação pós-falha de teste|
|/vaults/replicationRecoveryPlans/failoverCommit/Action|Plano de recuperação de consolidação de ativação pós-falha|
|/vaults/replicationRecoveryPlans/reProtect/Action|Proteja o plano de recuperação|
|/ Cofres/extendedInformation/leitura|Olá operação expandido informações obtém informações expandidas de um objeto que representa Olá recursos do Azure do tipo? Cofre?|
|/ Cofres/extendedInformation/escrita|Olá operação expandido informações obtém informações expandidas de um objeto que representa Olá recursos do Azure do tipo? Cofre?|
|/ Cofres/extendedInformation/eliminar|Olá operação expandido informações obtém informações expandidas de um objeto que representa Olá recursos do Azure do tipo? Cofre?|
|/ Cofres/backupManagementMetaData/leitura|Devolve os Metadados da Gestão da Cópia de Segurança do Cofre de Serviços de Recuperação.|
|/ Cofres/backupProtectionContainers/leitura|Devolve todos os contentores pertencentes toohello subscrição|
|/ Cofres/backupFabrics/operationResults/leitura|Devolve o estado da operação de Olá|
|/ Cofres/backupFabrics/protectionContainers/leitura|Devolve todas as registado contentores|
|/ Cofres/backupFabrics/protectionContainers /<br>operationResults/leitura|Obtém o resultado da Operação efetuada no Contentor de Proteção.|
|/ Cofres/backupFabrics/protectionContainers /<br>protectedItems/leitura|Devolve detalhes do Olá Item protegido de objeto|
|/ Cofres/backupFabrics/protectionContainers /<br>protectedItems/escrita|Criar um Item protegido cópia de segurança|
|/ Cofres/backupFabrics/protectionContainers /<br>protectedItems/eliminar|Elimina protegidos Item|
|/ Cofres/backupFabrics/protectionContainers /<br>cópia de segurança/protectedItems/ação|Executa a Cópia de Segurança do Item Protegido.|
|/ Cofres/backupFabrics/protectionContainers /<br>operationResults/protectedItems/leitura|Obtém o Resultado da Operação Efetuada nos Itens Protegidos.|
|/ Cofres/backupFabrics/protectionContainers /<br>operationStatus/protectedItems/leitura|Devolve Olá o estado de funcionamento efetuado em itens protegidos.|
|/ Cofres/backupFabrics/protectionContainers /<br>recoveryPoints/protectedItems/leitura|Obter Pontos de Recuperação de Itens Protegidos.|
|/ Cofres/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>acção de restauro /|Restaurar Pontos de Recuperação de Itens Protegidos.|
|/ Cofres/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>provisionInstantItemRecovery/ação|Aprovisionar Item instantâneas recuperação para o Item protegido|
|/ Cofres/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>revokeInstantItemRecovery/ação|Revogar a recuperação do Item instantâneas para Item protegido|
|/ Cofres/utilizações/leitura|Devolve detalhes de utilização de um Cofre de Serviços de Recuperação.|
|/vaults/usages/Read|Ler as utilizações do Cofre|
|/ Cofres/certificados/escrita|Olá a operação de certificado de recursos de atualização atualiza o certificado da credencial Olá recurso/cofre.|
|/ Cofres/tokenInfo/leitura|Devolve informações sobre o token para o Cofre de serviços de recuperação.|
|/vaults/replicationAlertSettings/Read|Ler as definições de alertas|
|/vaults/replicationAlertSettings/Write|Criar ou atualizar as definições de alertas|
|/ Cofres/backupOperations/leitura|Devolve a operação de cópia de segurança cofre dos serviços de estado de recuperação.|
|/ Cofres/storageConfig/leitura|Devolve a configuração de armazenamento para a recuperação cofre dos serviços.|
|/ Cofres/storageConfig/escrita|Cofre dos serviços de configuração de armazenamento de atualizações para a recuperação.|
|/ Cofres/backupUsageSummaries/leitura|Devolve resumos de itens protegidos e os servidores protegidos dos serviços de recuperação.|
|/ Cofres/backupProtectedItems/leitura|Devolve Olá lista de todos os itens protegidos.|
|/ Cofres/backupconfig/vaultconfig/leitura|Cofre dos serviços de configuração de devolve para recuperação.|
|/ Cofres/backupconfig/vaultconfig/escrita|Cofre dos serviços de configuração de atualizações para a recuperação.|
|/ Cofres/registeredIdentities/escrita|Olá operação registar o contentor de serviços pode ser utilizado tooregister um contentor com o serviço de recuperação.|
|/ Cofres/registeredIdentities/leitura|Olá obter contentores operação pode ser utilizada obter contentores Olá registados para um recurso.|
|/ Cofres/registeredIdentities/eliminar|Olá operação anular o registo do contentor pode ser utilizado toounregister um contentor.|
|/ Cofres/registeredIdentities/operationResults/leitura|Olá obter os resultados da operação operação pode ser utilizados obter estado da operação de Olá e resultar no modo assíncrono para Olá submetido operação|
|/vaults/replicationJobs/Read|Ler todas as tarefas|
|/vaults/replicationJobs/Cancel/Action|Cancelar a tarefa|
|/vaults/replicationJobs/Restart/Action|Reinicie a tarefa|
|/vaults/replicationJobs/resume/Action|Retomar a tarefa|
|/ Cofres/backupPolicies/leitura|Devolve todas as políticas de proteção|
|/ Cofres/backupPolicies/escrita|Cria a política de proteção|
|/ Cofres/backupPolicies/eliminar|Eliminar uma política de proteção|
|/ Cofres/backupPolicies/operationResults/leitura|Obter Resultados da Operação de Política.|
|/ Cofres/backupPolicies/operationStatus/leitura|Obter o estado da operação de política.|
|/ Cofres/vaultTokens/leitura|Olá operação Token cofre pode ser utilizado tooget cofre Token para operações de back-end ao nível do cofre.|
|/ Cofres/monitoringConfigurations/notificationConfiguration/leitura|Obtém a configuração de notificação de Cofre de serviços de recuperação de Olá.|
|/ Cofres/backupJobs/leitura|Devolve todos os objetos da tarefa|
|/ Cofres/backupJobs / / ação de cancelamento|Cancelar Olá tarefa|
|/ Cofres/backupJobs/operationResults/leitura|Devolve Olá resultado da tarefa a operação.|
|/Locations/allocateStamp/Action|AllocateStamp é uma operação interna utilizada pelo serviço|
|/Locations/allocatedStamp/Read|GetAllocatedStamp é uma operação interna utilizada pelo serviço|

## <a name="microsoftrelay"></a>Microsoft.Relay

| Operação | Descrição |
|---|---|
|checkNamespaceAvailability/ação|Verificações de disponibilidade de espaço de nomes em dada subscrição.|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos de reencaminhamento Olá e permite Olá criação dos recursos de reencaminhamento|
|espaços de nomes/escrita|Crie um recurso de espaço de nomes e Atualize as respetivas propriedades. As etiquetas e estado do espaço de nomes de Olá são propriedades de Olá que podem ser atualizadas.|
|/Namespaces/Read|Obter a lista de Olá da descrição de recursos do espaço de nomes|
|espaços de nomes/eliminar|Eliminar recurso do espaço de nomes|
|/Namespaces/authorizationRules/Write|Criar regras de autorização ao nível de espaço de nomes e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/authorizationRules/DELETE|Elimine regra de autorização de espaço de nomes. Não é possível eliminar Olá regra de autorização de espaço de nomes predefinido. |
|/Namespaces/authorizationRules/listkeys/Action|Obter a cadeia de ligação de Olá toohello espaço de nomes|
|/Namespaces/HybridConnections/Write|Criar ou atualizar HybridConnection propriedades.|
|/Namespaces/HybridConnections/Read|Obter a lista de descrições de recurso HybridConnection|
|/Namespaces/HybridConnections/DELETE|Operação toodelete HybridConnection recursos|
|/Namespaces/HybridConnections/authorizationRules/Write|Criar regras de autorização de HybridConnection e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/HybridConnections/authorizationRules/DELETE|Operação toodelete HybridConnection regras de autorização|
|/Namespaces/HybridConnections/authorizationRules/listkeys/Action|Obter Olá tooHybridConnection de cadeia de ligação|
|/Namespaces/WcfRelays/Write|Criar ou atualizar WcfRelay propriedades.|
|/Namespaces/WcfRelays/Read|Obter a lista de descrições de recurso WcfRelay|
|/Namespaces/WcfRelays/DELETE|Operação toodelete WcfRelay recursos|
|/Namespaces/WcfRelays/authorizationRules/Write|Criar regras de autorização de WcfRelay e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/WcfRelays/authorizationRules/DELETE|Operação toodelete WcfRelay regras de autorização|
|/Namespaces/WcfRelays/authorizationRules/listkeys/Action|Obter Olá tooWcfRelay de cadeia de ligação|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| Operação | Descrição |
|---|---|
|/ AvailabilityStatuses/leitura|Obtém Olá Estados de disponibilidade para todos os recursos na Olá especificado âmbito|
|/ AvailabilityStatuses/atual/leitura|Estado de disponibilidade de Olá obtém para Olá recurso especificado|

## <a name="microsoftresources"></a>Microsoft.Resources

| Operação | Descrição |
|---|---|
|checkResourceName/ação|Verifique o nome do recurso Olá para validade.|
|/providers/Read|Obter a lista de Olá de fornecedores.|
|/subscriptions/Read|Obtém a lista de Olá de subscrições.|
|/subscriptions/operationresults/Read|Obter a subscrição de Olá os resultados da operação.|
|/subscriptions/Providers/Read|Obtém ou lista fornecedores de recursos.|
|/subscriptions/tagNames/Read|Obtém ou lista etiquetas de subscrição.|
|/subscriptions/tagNames/Write|Adiciona uma etiqueta de subscrição.|
|/subscriptions/tagNames/DELETE|Elimina uma etiqueta de subscrição.|
|/subscriptions/tagNames/tagValues/Read|Obtém ou lista valores de etiqueta de subscrição.|
|/subscriptions/tagNames/tagValues/Write|Adiciona um valor de etiqueta de subscrição.|
|/subscriptions/tagNames/tagValues/DELETE|Elimina um valor de etiqueta de subscrição.|
|/subscriptions/resources/Read|Obtém os recursos de uma subscrição.|
|/subscriptions/resourceGroups/Read|Obtém ou lista de grupos de recursos.|
|/subscriptions/resourceGroups/Write|Cria ou atualiza um grupo de recursos.|
|/subscriptions/resourceGroups/DELETE|Elimina um grupo de recursos e todos os respetivos recursos.|
|/subscriptions/resourceGroups/moveResources/Action|Move os recursos de tooanother do grupo de recursos.|
|/subscriptions/resourceGroups/validateMoveResources/Action|Valide a movimentação de recursos de tooanother do grupo de recursos.|
|/subscriptions/resourcegroups/Resources/Read|Obtém os recursos de Olá Olá grupo de recursos.|
|/subscriptions/resourcegroups/Deployments/Read|Obtém ou lista de implementações.|
|/subscriptions/resourcegroups/Deployments/Write|Cria ou atualiza uma implementação.|
|/subscriptions/resourcegroups/Deployments/operationstatuses/Read|Obtém ou lista de Estados de operação de implementação.|
|/subscriptions/resourcegroups/Deployments/Operations/Read|Obtém ou lista as operações de implementação.|
|/subscriptions/Locations/Read|Obtém a lista de Olá de localizações suportadas.|
|/Links/Read|Obtém ou lista ligações de recursos.|
|ligações/escrita|Cria ou atualiza uma ligação de recursos.|
|/Links/DELETE|Elimina uma ligação de recursos.|
|/Tenants/Read|Obtém a lista de Olá dos inquilinos.|
|/Resources/Read|Obter a lista de Olá de recursos com base em filtros.|
|/Deployments/Read|Obtém ou lista de implementações.|
|implementações/escrita|Cria ou atualiza uma implementação.|
|/Deployments/DELETE|Elimina uma implementação.|
|/Deployments/Cancel/Action|Cancela uma implementação.|
|/Deployments/Validate/Action|Valida uma implementação.|
|/Deployments/Operations/Read|Obtém ou lista as operações de implementação.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| Operação | Descrição |
|---|---|
|/jobcollections/Read|Obter a coleção de tarefas|
|as jobcollections/escrita|Cria ou atualiza a coleção de tarefas.|
|/jobcollections/DELETE|Elimina a coleção de tarefas.|
|/jobcollections/Enable/Action|Permite que a coleção de tarefas.|
|/jobcollections/disable/Action|Desativa a coleção de tarefas.|
|/jobcollections/Jobs/Read|Obtém a tarefa.|
|/jobcollections/Jobs/Write|Cria ou atualiza a tarefa.|
|/jobcollections/Jobs/DELETE|Elimina a tarefa.|
|/jobcollections/Jobs/Run/Action|Tarefa é executada.|
|/jobcollections/Jobs/generateLogicAppDefinition/Action|Gera a definição da aplicação lógica com base numa tarefa do agendador.|
|/jobcollections/Jobs/jobhistories/Read|Obtém o histórico de tarefa.|

## <a name="microsoftsearch"></a>Microsoft.Search

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos de pesquisa de Olá e permite a criação de Olá dos serviços de pesquisa.|
|checkNameAvailability/ação|Verifica a disponibilidade do nome do serviço Olá.|
|/ searchServices/escrita|Cria ou atualiza o serviço de pesquisa de Olá.|
|/searchServices/Read|Lê o serviço de pesquisa de Olá.|
|/searchServices/DELETE|Elimina o serviço de pesquisa de Olá.|
|/searchServices/Start/Action|Inicia o serviço de pesquisa de Olá.|
|/searchServices/Stop/Action|Para o serviço de pesquisa de Olá.|
|/searchServices/listAdminKeys/Action|Lê chaves de administração de Olá.|
|/searchServices/regenerateAdminKey/Action|Chave de administrador Olá gera de novo.|
|/searchServices/createQueryKey/Action|Cria a chave de consulta Olá.|
|/searchServices/queryKey/Read|Lê as chaves de consulta Olá.|
|/searchServices/queryKey/DELETE|Elimina a chave de consulta Olá.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| Operação | Descrição |
|---|---|
|/jitNetworkAccessPolicies/Read|Obtém as políticas de acesso de rede de just-in-time Olá|
|/ jitNetworkAccessPolicies/escrita|Cria uma nova política de acesso de rede de just-in-time ou atualiza um já existente|
|/jitNetworkAccessPolicies/initiate/Action|Inicia uma política de acesso de rede de just-in-time|
|/securitySolutionsReferenceData/Read|Obtém as soluções de segurança de Olá dados de referência|
|/securityStatuses/Read|Obtém segurança Olá Estados de funcionamento de recursos do Azure|
|/webApplicationFirewalls/Read|Obtém as firewalls de aplicação web de Olá|
|/ webApplicationFirewalls/escrita|Cria uma nova firewall de aplicação web ou atualiza um já existente|
|/webApplicationFirewalls/DELETE|Elimina uma firewall de aplicação web|
|/securitySolutions/Read|Obtém as soluções de segurança de Olá|
|/ securitySolutions/escrita|Cria uma nova solução de segurança ou atualiza um já existente|
|/securitySolutions/DELETE|Elimina uma solução de segurança|
|/Tasks/Read|Obtém todas as recomendações de segurança disponíveis|
|/Tasks/dismiss/Action|Ignorar uma recomendação de segurança|
|/Tasks/Activate/Action|Ativar uma recomendação de segurança|
|/Policies/Read|Obtém a política de segurança de Olá|
|/ políticas/escrita|Olá, atualizações de política de segurança|
|/applicationWhitelistings/Read|Obtém Olá whitelistings de aplicação|
|/ applicationWhitelistings/escrita|Cria uma nova aplicação a listas brancas ou atualiza um já existente|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| Operação | Descrição |
|---|---|
|subscrições/escrita|Cria ou atualiza uma subscrição|
|/ gateways/escrita|Cria ou atualiza um gateway|
|/gateways/DELETE|Elimina um gateway|
|/gateways/Read|Obtém um gateway|
|/gateways/regenerateprofile/Action|Gera de novo perfil de gateway Olá|
|/gateways/upgradetolatest/Action|Atualizações Olá versão mais recente do gateway toohello|
|nós/escrita|cria ou atualiza um nó|
|/nodes/DELETE|Elimina um nó|
|/nodes/Read|Obtém um nó|
|sessões/escrita|Cria ou atualiza uma sessão|
|/Sessions/Read|Obtém uma sessão|
|/Sessions/DELETE|Elimina um sesssion|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| Operação | Descrição |
|---|---|
|checkNameAvailability/ação|Verificações de disponibilidade de espaço de nomes em dada subscrição.|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos de ServiceBus Olá e permite Olá criação dos recursos de barramento de serviço|
|espaços de nomes/escrita|Crie um recurso de espaço de nomes e Atualize as respetivas propriedades. As etiquetas e estado do espaço de nomes de Olá são propriedades de Olá que podem ser atualizadas.|
|/Namespaces/Read|Obter a lista de Olá da descrição de recursos do espaço de nomes|
|espaços de nomes/eliminar|Eliminar recurso do espaço de nomes|
|/Namespaces/metricDefinitions/Read|Obter a lista de descrições de recursos de métricas de espaço de nomes|
|/Namespaces/authorizationRules/Write|Criar regras de autorização ao nível de espaço de nomes e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/authorizationRules/Read|Obter a lista de Olá da descrição de regras de autorização de espaços de nomes.|
|/Namespaces/authorizationRules/DELETE|Elimine regra de autorização de espaço de nomes. Não é possível eliminar Olá regra de autorização de espaço de nomes predefinido. |
|/Namespaces/authorizationRules/listkeys/Action|Obter a cadeia de ligação de Olá toohello espaço de nomes|
|/Namespaces/authorizationRules/regenerateKeys/Action|Regenerar Olá principal ou secundário chave toohello recursos|
|/Namespaces/diagnosticSettings/Read|Obter a lista de descrições de recursos de definições de diagnóstico de espaço de nomes|
|/Namespaces/diagnosticSettings/Write|Obter a lista de descrições de recursos de definições de diagnóstico de espaço de nomes|
|/Namespaces/Queues/Write|Criar ou as propriedades da fila de atualização.|
|/Namespaces/Queues/Read|Obter a lista de descrições de recursos da fila|
|/Namespaces/Queues/DELETE|Operação toodelete recursos da fila|
|/Namespaces/Queues/authorizationRules/Write|Criar regras de autorização de fila e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/Queues/authorizationRules/Read| Obter a lista de Olá fila das regras de autorização|
|/Namespaces/Queues/authorizationRules/DELETE|Operação toodelete regras de autorização de fila|
|/Namespaces/Queues/authorizationRules/listkeys/Action|Obter Olá tooQueue de cadeia de ligação|
|/Namespaces/Queues/authorizationRules/regenerateKeys/Action|Regenerar Olá principal ou secundário chave toohello recursos|
|/Namespaces/logDefinitions/Read|Obter a lista de registos de espaço de nomes descrições de recursos|
|/Namespaces/topics/Write|Criar ou propriedades de tópico de atualização.|
|/Namespaces/topics/Read|Obter a lista de descrições de recursos de tópico|
|/Namespaces/topics/DELETE|Operação toodelete recursos de tópico|
|/Namespaces/topics/authorizationRules/Write|Criar regras de autorização de tópico e Atualize as respetivas propriedades. Direitos de acesso de regras de autorização de Olá, Olá primário e as chaves secundárias podem ser atualizadas.|
|/Namespaces/topics/authorizationRules/Read| Obter a lista de Olá das regras de autorização de tópico|
|/Namespaces/topics/authorizationRules/DELETE|Operação toodelete regras de autorização de tópico|
|/Namespaces/topics/authorizationRules/listkeys/Action|Obter Olá tooTopic de cadeia de ligação|
|/Namespaces/topics/authorizationRules/regenerateKeys/Action|Regenerar Olá principal ou secundário chave toohello recursos|
|/Namespaces/topics/subscriptions/Write|Criar ou atualizar TopicSubscription propriedades.|
|/Namespaces/topics/subscriptions/Read|Obter a lista de descrições de recurso TopicSubscription|
|/Namespaces/topics/subscriptions/DELETE|Operação toodelete TopicSubscription recursos|
|/Namespaces/topics/subscriptions/Rules/Write|Criar ou propriedades da regra de atualização.|
|/Namespaces/topics/subscriptions/Rules/Read|Obter a lista de descrições de recurso de regra|
|/Namespaces/topics/subscriptions/Rules/DELETE|Operação toodelete recurso de regra|

## <a name="microsoftsql"></a>Microsoft.Sql

| Operação | Descrição |
|---|---|
|/Servers/Read|Devolver uma lista de servidores num grupo de recursos de uma subscrição|
|/ servidores/escrita|Criar um novo servidor ou modificar as propriedades do servidor existente num grupo de recursos de uma subscrição|
|/Servers/DELETE|Eliminar um servidor e incluídas todas as bases de dados e conjuntos elásticos|
|/Servers/Import/Action|Criar uma nova base de dados no servidor de Olá e implementar o esquema e dados a partir de um pacote de DacPac|
|/Servers/Upgrade/Action|Ativar novas funcionalidades disponíveis na versão mais recente do hello do servidor e especificar o mapa de conversão de edição de bases de dados|
|/Servers/VulnerabilityAssessmentScans/Action|Executar a análise de servidor avaliação da vulnerabilidade|
|/Servers/operationResults/Read|Operação é utilizada tootrack progresso da atualização do servidor de inferior toohigher de versão|
|/Servers/operationResults/DELETE|Abortar a atualização de versão do servidor em curso|
|/Servers/securityAlertPolicies/Read|Obter os detalhes de Olá servidor ameaça deteção política configurada num determinado servidor|
|/Servers/securityAlertPolicies/Write|Alterar a deteção de ameaças de servidor de Olá para um determinado servidor|
|/Servers/securityAlertPolicies/operationResults/Read|Obter resultados do servidor de Olá a operação de definição de política de deteção de ameaças|
|/Servers/Administrators/Read|Obter os detalhes de administrador do servidor|
|/Servers/Administrators/Write|Criar ou atualizar o administrador do servidor|
|/Servers/Administrators/DELETE|Elimine o administrador do servidor do servidor de Olá|
|/Servers/recoverableDatabases/Read|Esta operação é utilizada para recuperação após desastre de base de dados dinâmicos toorestore da base de dados toolast conhecido boa cópia de segurança ponto. Devolve informações sobre Olá última boa cópia de segurança mas, na verdade, o sistema não restaurar base de dados de Olá.|
|/Servers/serviceObjectives/Read|Obter a lista de serviço objetivos do nível (também conhecido como escalões de desempenho) disponíveis num determinado servidor|
|/Servers/firewallRules/Read|Obter os detalhes de regras de firewall do servidor|
|/Servers/firewallRules/Write|Criar ou atualizar regra de firewall do servidor que controla o intervalo de endereços IP permitido tooconnect toohello servidor|
|/Servers/firewallRules/DELETE|Eliminar regra de firewall do servidor de Olá|
|/Servers/administratorOperationResults/Read|Obter resultados de operação de administrador do servidor|
|/Servers/recommendedElasticPools/Read|Obter recomendação custo de tooreduce de conjuntos de bases de dados elásticas ou melhorar o desempenho com base na utilização de recursos de historica|
|/Servers/recommendedElasticPools/Metrics/Read|Obter métricas para os conjuntos de bases de dados elásticas recomendado para um determinado servidor|
|/Servers/recommendedElasticPools/Databases/Read|Obter bases de dados que devem ser adicionados para conjuntos de bases de dados elásticas para um determinado servidor recomendados.|
|/Servers/elasticPools/Read|Obter os detalhes do agrupamento de base de dados elástica num determinado servidor|
|/Servers/elasticPools/Write|Crie um novo ou alterar as propriedades do conjunto de bases de dados elásticas existente|
|/Servers/elasticPools/DELETE|Eliminar conjunto de bases de dados elásticas existente|
|/Servers/elasticPools/operationResults/Read|Obter detalhes sobre uma operação de agrupamento de base de dados elásticas indicado|
|/Servers/elasticPools/Providers/Microsoft.Insights/<br>metricDefinitions/leitura|Tipos de retorno de métricas que estão disponíveis para conjuntos de bases de dados elásticas|
|/Servers/elasticPools/Providers/Microsoft.Insights/<br>diagnosticSettings/leitura|Obtém a definição de diagnóstico de Olá para o recurso de Olá|
|/Servers/elasticPools/Providers/Microsoft.Insights/<br>diagnosticSettings/escrita|Cria ou atualiza a definição de diagnóstico de Olá para o recurso de Olá|
|/Servers/elasticPools/Metrics/Read|Devolver métricas de utilização de recursos de agrupamento de base de dados elástica|
|/Servers/elasticPools/elasticPoolDatabaseActivity/Read|Obter as atividades e os detalhes numa determinada base de dados que faz parte do agrupamento de base de dados elástica|
|/Servers/elasticPools/advisors/Read|Devolve a lista de consultores disponíveis para o conjunto elástico Olá|
|/Servers/elasticPools/advisors/Write|Atualização automática-executar o estado de um advisor no nível do conjunto elástico.|
|/Servers/elasticPools/advisors/recommendedActions/Read|Devolve a lista de ações recomendadas do advisor especificado para o conjunto elástico Olá|
|/Servers/elasticPools/advisors/recommendedActions/Write|Aplicar Olá ação num agrupamento elástico de Olá recomendada|
|/Servers/elasticPools/elasticPoolActivity/Read|Obter as atividades e detalhes sobre um conjunto de bases de dados elásticas indicado|
|/Servers/elasticPools/Databases/Read|Obter a lista e os detalhes das bases de dados que fazem parte do conjunto de bases de dados elásticas num determinado servidor|
|/Servers/auditingPolicies/Read|Obter os detalhes da tabela de servidor de predefinição Olá configurada num determinado servidor de política de auditoria|
|/Servers/auditingPolicies/Write|Alterar a tabela de servidor de predefinição Olá auditoria para um determinado servidor|
|/Servers/disasterRecoveryConfiguration/operationResults/Read|Obter resultados de operação de configuração de recuperação de desastre|
|/Servers/advisors/Read|Devolve a lista de consultores disponíveis para o servidor de Olá|
|/Servers/advisors/Write|As atualizações de autom-executar o estado de um advisor no nível do servidor.|
|/Servers/advisors/recommendedActions/Read|Devolve a lista de ações recomendadas do advisor especificado para o servidor de Olá|
|/Servers/advisors/recommendedActions/Write|Aplicar Olá ação no servidor de Olá recomendada|
|/Servers/usages/Read|Devolver a quota DTU do servidor e consuption DTU atual por todas as bases de dados no servidor de Olá|
|/Servers/elasticPoolEstimates/Read|Devolve a lista de estimativas de conjunto elástico já criada para este servidor|
|/Servers/elasticPoolEstimates/Write|Cria nova estimativa de conjunto elástico para obter a lista de bases de dados fornecido|
|/Servers/auditingSettings/Read|Obter os detalhes do blob de servidor Olá configurada num determinado servidor de política de auditoria|
|/Servers/auditingSettings/Write|Alterar Olá auditoria de blob de servidor para um determinado servidor|
|/Servers/auditingSettings/operationResults/Read|Obter Resultado de blob de servidor Olá operação de definição de política de auditoria|
|/Servers/backupLongTermRetentionVaults/Read|Esta operação é utilizado tooget um cofre de retenção de cópias de segurança de longo prazo. Devolve informações sobre o servidor do Olá cofre toothis registado.|
|/Servers/backupLongTermRetentionVaults/Write|Registe um cofre de retenção de cópias de segurança de longa duração|
|/Servers/restorableDroppedDatabases/Read|Obter uma lista de bases de dados que foram ignorados num determinado servidor que estão ainda na política de retenção. Esta operação devolve uma lista de bases de dados e metadados associados, como data de eliminação.|
|/Servers/Databases/Read|Devolver uma lista de servidores num grupo de recursos de uma subscrição|
|/Servers/Databases/Write|Criar um novo servidor ou modificar as propriedades do servidor existente num grupo de recursos de uma subscrição|
|/Servers/Databases/DELETE|Eliminar um servidor e incluídas todas as bases de dados e conjuntos elásticos|
|/Servers/Databases/Export/Action|Criar uma nova base de dados no servidor de Olá e implementar o esquema e dados a partir de um pacote de DacPac|
|/Servers/Databases/VulnerabilityAssessmentScans/Action|Execute uma análise de avaliação da vulnerabilidade da base de dados.|
|/Servers/Databases/pause/Action|Colocar em pausa de uma base de dados de edição de DataWarehouse|
|/Servers/Databases/resume/Action|Retomar uma base de dados de edição de DataWarehouse|
|/Servers/Databases/operationResults/Read|Operação é utilizada tootrack progresso da operação de base de dados longa, por exemplo, a escala.|
|/Servers/Databases/replicationLinks/Read|Retorno detalhes sobre ligações de replicação estabelecidas para uma determinada base de dados|
|/Servers/Databases/replicationLinks/DELETE|Terminar a relação de replicação de Olá forçadamente e com uma potencial perda de dados|
|/Servers/Databases/replicationLinks/unlink/Action|Terminar a relação de replicação de Olá forçadamente ou após a sincronização com o parceiro de Olá|
|/Servers/Databases/replicationLinks/failover/Action|Ativação pós-falha depois de sincronizar todas as alterações de Olá primário, tornar esta base de dados numa Olá primário e efetuar remoto site primário relação de replicação a Olá para uma secundária|
|/Servers/Databases/replicationLinks/forceFailoverAllowDataLoss/Action|Ativação pós-falha imediatamente com potencial perda de dados, tornar esta base de dados para remoto de Olá primário e execuções de relação de replicação a Olá primário para uma secundária|
|/Servers/Databases/replicationLinks/updateReplicationMode/Action|Atualizar o modo de replicação para a ligação toosynchronous ou de modo assíncrono|
|/Servers/Databases/replicationLinks/operationResults/Read|Obter o estado das operações de execução longa em ligações de replicação de base de dados|
|/Servers/Databases/dataMaskingPolicies/Read|Obter os detalhes da política configurada numa determinada base de dados de máscara de dados de Olá|
|/Servers/Databases/dataMaskingPolicies/Write|Alterar a política para uma determinada base de dados de máscara de dados|
|/Servers/Databases/dataMaskingPolicies/Rules/Read|Obter os detalhes da regra de política configurada numa base de dados indicado de máscara de dados de Olá|
|/Servers/Databases/dataMaskingPolicies/Rules/Write|Alterar a regra de política para uma determinada base de dados de máscara de dados|
|/Servers/Databases/securityAlertPolicies/Read|Obter os detalhes da política de deteção de ameaças de Olá configurado numa base de dados indicado|
|/Servers/Databases/securityAlertPolicies/Write|Alterar a política de deteção de ameaças Olá para uma determinada base de dados|
|/Servers/Databases/Providers/Microsoft.Insights/<br>metricDefinitions/leitura|Tipos de retorno de métricas que estão disponíveis para bases de dados|
|/Servers/Databases/Providers/Microsoft.Insights/<br>diagnosticSettings/leitura|Obtém a definição de diagnóstico de Olá para o recurso de Olá|
|/Servers/Databases/Providers/Microsoft.Insights/<br>diagnosticSettings/escrita|Cria ou atualiza a definição de diagnóstico de Olá para o recurso de Olá|
|/Servers/Databases/Providers/Microsoft.Insights/<br>logDefinitions/leitura|Obtém os registos disponíveis Olá para bases de dados|
|/Servers/Databases/topQueries/Read|Devolve agregar estatísticas de tempo de execução para a consulta selecionada no período de tempo selecionado|
|/Servers/Databases/topQueries/queryText/Read|Devolve o texto de Transact-SQL Olá para o ID de consulta selecionada|
|/Servers/Databases/topQueries/statistics/Read|Devolve agregar estatísticas de tempo de execução para a consulta selecionada no período de tempo selecionado|
|/Servers/Databases/connectionPolicies/Read|Obter os detalhes da política de ligação de Olá configurado numa base de dados indicado|
|/Servers/Databases/connectionPolicies/Write|Alterar a política de ligação para uma determinada base de dados|
|/Servers/Databases/Metrics/Read|Devolver métricas de utilização de recursos de base de dados|
|/Servers/Databases/auditRecords/Read|Obter registos de auditoria de blob de base de dados de Olá|
|/Servers/Databases/transparentDataEncryption/Read|Obter o estado e os detalhes da funcionalidade de segurança de encriptação transparente de dados para uma determinada base de dados|
|/Servers/Databases/transparentDataEncryption/Write|Ativar ou desativar a encriptação transparente de dados para uma determinada base de dados|
|/Servers/Databases/transparentDataEncryption/operationResults/Read|Obter o estado e os detalhes da funcionalidade de segurança de encriptação transparente de dados para uma determinada base de dados|
|/Servers/Databases/auditingPolicies/Read|Obter os detalhes da política de auditoria de tabela de Olá configurado numa base de dados indicado|
|/Servers/Databases/auditingPolicies/Write|Alterar a política de auditoria de tabela de Olá para uma determinada base de dados|
|/Servers/Databases/dataWarehouseQueries/Read|Devolve Olá informações de consulta da distribuição de armazém de dados para o ID de consulta selecionada|
|/ servidores bases de dados/dataWarehouseQueries /<br>dataWarehouseQuerySteps/leitura|Olá devolve distribuídas passo as informações da consulta da consulta de armazém de dados para o ID do passo selecionado|
|/Servers/Databases/serviceTierAdvisors/Read|Devolver a sugestão sobre dimensionar a base de dados ou reduzir verticalmente com base no desempenho de tooimprove de estatísticas de execução de consulta ou reduzir o custo|
|/Servers/Databases/advisors/Read|Devolve a lista de consultores disponíveis para a base de dados de Olá|
|/Servers/Databases/advisors/Write|Atualização automática-executar o estado de um advisor no nível de base de dados.|
|/Servers/Databases/advisors/recommendedActions/Read|Devolve a lista de ações recomendadas do advisor especificado da base de dados de Olá|
|/Servers/Databases/advisors/recommendedActions/Write|Aplicar Olá ação na base de dados de Olá recomendada|
|/Servers/Databases/usages/Read|Devolver o tamanho máximo da base de dados que pode ser contactado e o tamanho atual ocupado por dados|
|/Servers/Databases/queryStore/Read|Devolve os valores atuais das definições de arquivo de consultas da base de dados de Olá|
|/Servers/Databases/queryStore/Write|Atualizações de definição de arquivo de consultas da base de dados de Olá|
|/Servers/Databases/auditingSettings/Read|Obter os detalhes da política de auditoria de blob de Olá configurado numa base de dados indicado|
|/Servers/Databases/auditingSettings/Write|Alterar a política de auditoria de blob de Olá para uma determinada base de dados|
|/Servers/Databases/schemas/Tables/recommendedIndexes/Read|Obter a lista de recomendações do índice numa base de dados|
|/Servers/Databases/schemas/Tables/recommendedIndexes/Write|Aplicar a recomendação do índice|
|/Servers/Databases/schemas/Tables/columns/Read|Obter a lista de colunas de uma tabela|
|/Servers/Databases/missingindexes/Read|Devolver sugestões sobre toocreate de índices de base de dados, modificar ou eliminar no desempenho das consultas tooimprove ordem|
|/Servers/Databases/missingindexes/Write|Utilize a recomendação do índice de base de dados numa base de dados específico|
|/Servers/Databases/importExportOperationResults/Read|Devolve detalhes sobre a importação da base de dados ou a operação de exportação de DacPac localizado na conta de armazenamento|
|/Servers/importExportOperationResults/Read|Devolver a lista de Olá com detalhes para operações de importação de base de dados da conta de armazenamento num determinado servidor|

## <a name="microsoftstorage"></a>Microsoft.Storage

| Operação | Descrição |
|---|---|
|registar/ação|Regista a subscrição de Olá do fornecedor de recursos de armazenamento Olá e permite Olá criação de contas do storage.|
|/checknameavailability/Read|Verifica esse nome de conta é válido e não está em utilização.|
|/ storageAccounts/escrita|Cria uma conta de armazenamento com Olá especificado parâmetros ou atualização Olá propriedades ou etiquetas ou adiciona personalizada Olá no domínio especificado a conta de armazenamento.|
|/storageAccounts/DELETE|Elimina uma conta de armazenamento existente.|
|/storageAccounts/listkeys/Action|Chaves de acesso de Olá devolve para Olá especificar conta de armazenamento.|
|/storageAccounts/regeneratekey/Action|Chaves de acesso de Olá gera de novo para Olá especificar conta de armazenamento.|
|/storageAccounts/Read|Devolve Olá lista de contas de armazenamento ou obtém Olá propriedades Olá especificar conta de armazenamento.|
|/storageAccounts/listAccountSas/Action|Token de conta SAS de Olá devolve para Olá especificar conta de armazenamento.|
|/storageAccounts/listServiceSas/Action|Token SAS do serviço de armazenamento|
|/storageAccounts/Services/diagnosticSettings/Write|Criar/atualizar definições de diagnóstico de conta de armazenamento.|
|/SKUs/Read|Apresenta uma lista de Olá Skus suportados pela Microsoft.|
|/usages/Read|Devolve Olá limite e Olá contagem de utilização atual dos recursos no Olá especificado subscrição|
|/Operations/Read|Estado de Olá inquéritos de uma operação assíncrona.|
|/Locations/deleteVirtualNetworkOrSubnets/Action|Notifica Microsoft que está a ser eliminada uma rede virtual ou de sub-rede|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| Operação | Descrição |
|---|---|
|/managers/clearAlerts/Action|Limpe todos os alertas de Olá associados ao Gestor de dispositivos de Olá.|
|/managers/getActivationKey/Action|Obter a chave de ativação para o Gestor de dispositivos de Olá.|
|/managers/regenerateActivationKey/Action|Regenere a chave de ativação de Gestor de dispositivos de Olá.|
|/managers/regenarateRegistationCertificate/Action|Regenere o certificado de registo para os gestores de dispositivo Olá.|
|/managers/getEncryptionKey/Action|Obter a chave de encriptação para o Gestor de dispositivos de Olá.|
|/managers/Read|Apresenta uma lista ou obtém Olá gestores de dispositivos|
|/managers/DELETE|Elimina Olá gestores de dispositivos|
|gestores/escrita|Criar ou atualizar Olá gestores de dispositivos|
|/managers/configureDevice/Action|Configura um dispositivo|
|/managers/listActivationKey/Action|Obtém a chave de ativação de Olá de Olá Gestor de dispositivos do StorSimple.|
|/managers/listPublicEncryptionKey/Action|Listar chaves de encriptação pública de um Gestor de dispositivos do StorSimple.|
|/managers/listPrivateEncryptionKey/Action|Obtém a chave privada de encriptação para um Gestor de dispositivos do StorSimple.|
|/managers/provisionCloudAppliance/Action|Crie uma nova aplicação de nuvem.|
|/ Gestores/escrita|A operação Criar Cofre cria um recurso do tipo "cofre" do Azure|
|/ Gestores/leitura|Olá operação obter cofre obtém um objeto que representa Olá recursos do Azure do tipo 'cofre'|
|/ Gestores/eliminar|Olá eliminar cofre operação eliminações Olá especificado recursos do Azure do tipo 'cofre'|
|/managers/storageAccountCredentials/Write|Criar ou atualizar as credenciais de conta de armazenamento Olá|
|/managers/storageAccountCredentials/Read|Apresenta uma lista ou obtém Olá credenciais da conta de armazenamento|
|/managers/storageAccountCredentials/DELETE|Elimina Olá credenciais da conta de armazenamento|
|/managers/storageAccountCredentials/listAccessKey/Action|Lista de chaves de acesso das credenciais de conta de armazenamento|
|/managers/accessControlRecords/Read|Apresenta uma lista ou obtém os registos de controlo de acesso de Olá|
|/managers/accessControlRecords/Write|Criar ou atualizar os registos de controlo de acesso de Olá|
|/managers/accessControlRecords/DELETE|Elimina os registos de controlo de acesso de Olá|
|/managers/Metrics/Read|Apresenta uma lista ou obtém Olá métricas|
|/managers/bandwidthSettings/Read|Lista as definições de largura de banda Olá (8000 série apenas)|
|/managers/bandwidthSettings/Write|Cria um novo ou atualiza as definições de largura de banda (8000 série apenas)|
|/managers/bandwidthSettings/DELETE|Elimina as definições de largura de banda de um existente (8000 série apenas)|
|/ Gestores/extendedInformation/leitura|Olá operação expandido informações obtém informações expandidas de um objeto que representa Olá recursos do Azure do tipo? Cofre?|
|/ Gestores/extendedInformation/escrita|Olá operação expandido informações obtém informações expandidas de um objeto que representa Olá recursos do Azure do tipo? Cofre?|
|/ Gestores/extendedInformation/eliminar|Olá operação expandido informações obtém informações expandidas de um objeto que representa Olá recursos do Azure do tipo? Cofre?|
|/managers/Alerts/Read|Apresenta uma lista ou obtém Olá alertas|
|/managers/storageDomains/Read|Apresenta uma lista ou obtém Olá armazenamento domínios|
|/managers/storageDomains/Write|Criar ou atualizar Olá armazenamento domínios|
|/managers/storageDomains/DELETE|Elimina Olá armazenamento domínios|
|/managers/Devices/scanForUpdates/Action|Análise de atualizações de um dispositivo.|
|/managers/Devices/download/Action|Atualizações de transferências para um dispositivo.|
|/managers/Devices/Install/Action|Instale as atualizações num dispositivo.|
|/managers/Devices/Read|Apresenta uma lista ou obtém Olá dispositivos|
|/managers/Devices/Write|Criar ou atualizar Olá dispositivos|
|/managers/Devices/DELETE|Elimina Olá dispositivos|
|/managers/Devices/Deactivate/Action|Desativa um dispositivo.|
|/managers/Devices/publishSupportPackage/Action|Publica o pacote de suporte de um dispositivo para a resolução de problemas de Support da Microsoft.|
|/managers/Devices/failover/Action|Ativação pós-falha do dispositivo Olá.|
|/managers/Devices/sendTestAlertEmail/Action|Envie e-mail de teste de alerta tooconfigured destinatários de e-mail.|
|/managers/Devices/installUpdates/Action|Instala atualizações em dispositivos Olá|
|/managers/Devices/listFailoverSets/Action|Ativação pós-falha de Olá lista define para um dispositivo existente.|
|/managers/Devices/listFailoverTargets/Action|Destinos de ativação pós-falha de lista de dispositivos de Olá|
|/managers/Devices/publicEncryptionKey/Action|Chave de encriptação pública de lista do Gestor de dispositivos de Olá|
|/ gestores dispositivos/hardwareComponentGroups /<br>Leitura|Olá lista grupos de componentes de Hardware|
|/ gestores dispositivos/hardwareComponentGroups /<br>changeControllerPowerState/ação|Alterar o estado de energia do controlador de grupos de componentes de hardware|
|/managers/Devices/Metrics/Read|Apresenta uma lista ou obtém Olá métricas|
|/managers/Devices/chapSettings/Write|Criar ou atualizar definições de Chap Olá|
|/managers/Devices/chapSettings/Read|Apresenta uma lista ou obtém Olá Chap definições|
|/managers/Devices/chapSettings/DELETE|Elimina as definições Chap de Olá|
|/managers/Devices/backupScheduleGroups/Read|Apresenta uma lista ou obtém a grupos de agenda de cópia de segurança de Olá|
|/managers/Devices/backupScheduleGroups/Write|Criar ou atualizar os grupos de agenda de cópia de segurança de Olá|
|/managers/Devices/backupScheduleGroups/DELETE|Elimina a grupos de agenda de cópia de segurança de Olá|
|/managers/Devices/updateSummary/Read|Apresenta uma lista ou obtém Olá resumo de atualização|
|/ gestores dispositivos/migrationSourceConfigurations /<br>Importar/ação|Importar configurações de origem para migração|
|/ gestores dispositivos/migrationSourceConfigurations /<br>startMigrationEstimate/ação|Inicie uma tarefa tooestimate Olá durante Olá processo de migração.|
|/ gestores dispositivos/migrationSourceConfigurations /<br>startMigration/ação|Começar a utilizar configurações de origem de migração|
|/ gestores dispositivos/migrationSourceConfigurations /<br>confirmMigration/ação|Confirma que uma migração com êxito e a consolidação da mesma.|
|/ gestores dispositivos/migrationSourceConfigurations /<br>fetchMigrationEstimate/ação|Obter o estado de Olá Olá tarefa de migração estimativa.|
|/ gestores dispositivos/migrationSourceConfigurations /<br>fetchMigrationStatus/ação|Obter o estado de Olá para a migração de Olá.|
|/ gestores dispositivos/migrationSourceConfigurations /<br>fetchConfirmMigrationStatus/ação|Obtenção Olá confirmar o estado de migração.|
|/managers/Devices/alertSettings/Read|Apresenta uma lista ou obtém as definições de alerta de Olá|
|/managers/Devices/alertSettings/Write|Criar ou atualizar definições de alerta de Olá|
|/managers/Devices/networkSettings/Read|Apresenta uma lista ou obtém as definições de rede Olá|
|/managers/Devices/networkSettings/Write|Cria um novo ou atualiza as definições de rede|
|/managers/Devices/Jobs/Read|Apresenta uma lista ou obtém Olá tarefas|
|/managers/Devices/Jobs/Cancel/Action|Cancelar uma tarefa em execução|
|/managers/Devices/metricsDefinitions/Read|Apresenta uma lista ou obtém as definições de métrica de Olá|
|/managers/Devices/volumeContainers/Write|Cria um novo ou atualiza os contentores de Volume (8000 série apenas)|
|/managers/Devices/volumeContainers/Read|Lista os contentores de Volume Olá (8000 série apenas)|
|/managers/Devices/volumeContainers/DELETE|Elimina um contentores de Volume existente (8000 série apenas)|
|/managers/Devices/volumeContainers/listEncryptionKeys/Action|Lista de chaves de encriptação de contentores de Volume|
|/managers/Devices/volumeContainers/rolloverEncryptionKey/Action|Chaves de encriptação de rollover de contentores de Volume|
|/managers/Devices/volumeContainers/Metrics/Read|Lista Olá métricas|
|/managers/Devices/volumeContainers/volumes/Read|Lista Olá Volumes|
|/managers/Devices/volumeContainers/volumes/Write|Cria um novo ou Volumes de atualizações|
|/managers/Devices/volumeContainers/volumes/DELETE|Elimina um Volumes existentes|
|/managers/Devices/volumeContainers/volumes/Metrics/Read|Lista Olá métricas|
|/managers/Devices/volumeContainers/volumes/metricsDefinitions/Read|Olá lista as definições de métricas|
|/managers/Devices/volumeContainers/metricsDefinitions/Read|Olá lista as definições de métricas|
|/managers/Devices/iscsiservers/Read|Apresenta uma lista ou obtém o iSCSI Olá servidores|
|/managers/Devices/iscsiservers/Write|Criar ou atualizar Olá iSCSI servidores|
|/managers/Devices/iscsiservers/DELETE|Elimina Olá iSCSI servidores|
|/managers/Devices/iscsiservers/backup/Action|Efetuar cópia de segurança de um servidor de iSCSI.|
|/managers/Devices/iscsiservers/Metrics/Read|Apresenta uma lista ou obtém Olá métricas|
|/managers/Devices/iscsiservers/Disks/Read|Apresenta uma lista ou obtém Olá discos|
|/managers/Devices/iscsiservers/Disks/Write|Criar ou atualizar Olá discos|
|/managers/Devices/iscsiservers/Disks/DELETE|Elimina Olá discos|
|/managers/Devices/iscsiservers/Disks/Metrics/Read|Apresenta uma lista ou obtém Olá métricas|
|/managers/Devices/iscsiservers/Disks/metricsDefinitions/Read|Apresenta uma lista ou obtém as definições de métrica de Olá|
|/managers/Devices/iscsiservers/metricsDefinitions/Read|Apresenta uma lista ou obtém as definições de métrica de Olá|
|/managers/Devices/backups/Read|Apresenta uma lista ou obtém Olá definido de cópia de segurança|
|/managers/Devices/backups/DELETE|Olá, elimina o conjunto de cópia de segurança|
|/managers/Devices/backups/Restore/Action|Restaure todos os volumes de Olá a partir de um conjunto de cópia de segurança.|
|/managers/Devices/backups/elements/clone/Action|Clone de uma partilha ou volume com um elemento de cópia de segurança.|
|/managers/Devices/backupPolicies/Write|Cria um novo ou atualizações de políticas de cópia de segurança (8000 série apenas)|
|/managers/Devices/backupPolicies/Read|Olá lista das políticas de cópia de segurança (8000 série apenas)|
|/managers/Devices/backupPolicies/DELETE|Elimina um políticas de cópia de segurança existente (8000 série apenas)|
|/managers/Devices/backupPolicies/backup/Action|Tirar um toocreate de cópia de segurança manual uma pedido a cópia de segurança de todos os volumes de Olá protegidos pela política de Olá.|
|/managers/Devices/backupPolicies/Schedules/Write|Cria um novo ou agendas de atualizações|
|/managers/Devices/backupPolicies/Schedules/Read|Lista Olá agendas|
|/managers/Devices/backupPolicies/Schedules/DELETE|Elimina um agendas existentes|
|/managers/Devices/securitySettings/Update/Action|Atualize as definições de segurança de Olá.|
|/managers/Devices/securitySettings/Read|Olá lista as definições de segurança|
|/ gestores dispositivos/securitySettings /<br>syncRemoteManagementCertificate/ação|Sincronize o certificado de gestão remota de Olá para um dispositivo.|
|/managers/Devices/securitySettings/Write|Cria um novo ou atualiza as definições de segurança|
|/managers/Devices/fileservers/Read|Apresenta uma lista ou obtém Olá servidores de ficheiros|
|/managers/Devices/fileservers/Write|Criar ou atualizar os servidores de ficheiros de Olá|
|/managers/Devices/fileservers/DELETE|Elimina Olá servidores de ficheiros|
|/managers/Devices/fileservers/backup/Action|Efetuar cópia de segurança de um servidor de ficheiros.|
|/managers/Devices/fileservers/Metrics/Read|Apresenta uma lista ou obtém Olá métricas|
|/managers/Devices/fileservers/shares/Write|Criar ou atualizar as partilhas de Olá|
|/managers/Devices/fileservers/shares/Read|Apresenta uma lista ou obtém Olá partilhas|
|/managers/Devices/fileservers/shares/DELETE|Elimina Olá partilhas|
|/managers/Devices/fileservers/shares/Metrics/Read|Apresenta uma lista ou obtém Olá métricas|
|/managers/Devices/fileservers/shares/metricsDefinitions/Read|Apresenta uma lista ou obtém as definições de métrica de Olá|
|/managers/Devices/fileservers/metricsDefinitions/Read|Apresenta uma lista ou obtém as definições de métrica de Olá|
|/managers/Devices/timeSettings/Read|Apresenta uma lista ou obtém as definições de hora Olá|
|/managers/Devices/timeSettings/Write|Cria um novo ou atualiza as definições de hora|
|/ Gestores/certificados/escrita|Olá a operação de certificado de recursos de atualização atualiza o certificado da credencial Olá recurso/cofre.|
|/managers/cloudApplianceConfigurations/Read|Lista Olá configurações suportadas de nuvem do dispositivo|
|/managers/metricsDefinitions/Read|Apresenta uma lista ou obtém as definições de métrica de Olá|
|/managers/encryptionSettings/Read|Apresenta uma lista ou obtém as definições de encriptação de Olá|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| Operação | Descrição |
|---|---|
|/streamingjobs/Start/Action|Iniciar a tarefa do Stream Analytics|
|/streamingjobs/Stop/Action|Parar a tarefa do Stream Analytics|
|streamingjobs/leitura|Leitura tarefa do Stream Analytics|
|streamingjobs/escrita|Escrever a tarefa do Stream Analytics|
|streamingjobs/eliminar|Eliminar a tarefa do Stream Analytics|
|/streamingjobs/Providers/Microsoft.Insights/metricDefinitions/Read|Obtém as métricas disponíveis de Olá para streamingjobs|
|/streamingjobs/Providers/Microsoft.Insights/diagnosticSettings/Read|Definição de diagnóstico de leitura.|
|/streamingjobs/Providers/Microsoft.Insights/diagnosticSettings/Write|Escreva a definição de diagnóstico.|
|/streamingjobs/Providers/Microsoft.Insights/logDefinitions/Read|Obtém os registos disponíveis Olá para streamingjobs|
|/streamingjobs/Transformations/Read|Transformação de tarefa de análise de fluxo de leitura|
|/streamingjobs/Transformations/Write|Escrever transformação de tarefa do Stream Analytics|
|/streamingjobs/Transformations/DELETE|Eliminar a transformação de tarefa do Stream Analytics|
|/streamingjobs/inputs/Read|Entrada de tarefa de análise de fluxo de leitura|
|/streamingjobs/inputs/Write|Escrever a entrada de fluxo de trabalho de análise|
|/streamingjobs/inputs/DELETE|Eliminar a entrada de fluxo de trabalho de análise|
|/streamingjobs/outputs/Read|Resultado da tarefa leitura Stream Analytics|
|/streamingjobs/outputs/Write|Escrever a saída da tarefa do Stream Analytics|
|/streamingjobs/outputs/DELETE|Eliminar o resultado da tarefa do Stream Analytics|

## <a name="microsoftsupport"></a>Microsoft. support

| Operação | Descrição |
|---|---|
|registar/ação|Regista tooSupport fornecedor de recursos|
|/supportTickets/Read|Obtém os detalhes do pedido de suporte (incluindo o estado, gravidade, detalhes de contacto e comunicações) ou obtém a lista de Olá de pedidos de suporte nas subscrições.|
|/ supportTickets/escrita|Cria ou atualiza um pedido de suporte. Pode criar um pedido de suporte para técnica, Quotas ou gestão de subscrição de faturação problemas relacionados com. Pode atualizar a gravidade, detalhes de contacto e comunicações para pedidos de suporte existentes.|

## <a name="microsoftweb"></a>Microsoft. Web

| Operação | Descrição |
|---|---|
|ação de anular o registo /|Anular o registo do fornecedor de recursos Microsoft. Web para a subscrição de Olá.|
|Validar/ação|Valide.|
|registar/ação|Registe o fornecedor de recursos Microsoft. Web para a subscrição de Olá.|
|hostingEnvironments/leitura|Obter propriedades de Olá de um ambiente de serviço de aplicações|
|hostingEnvironments/escrita|Criar um novo ambiente de serviço de aplicações ou Atualize uma existente|
|hostingEnvironments/eliminar|Eliminar um ambiente de serviço de aplicações|
|/hostingEnvironments/reboot/Action|Reinicie todas as máquinas no ambiente de serviço de aplicações|
|/hostingenvironments/resume/Action|Retomar a ambientes de alojamento.|
|/hostingenvironments/suspend/Action|Suspenda a ambientes de alojamento.|
|/hostingenvironments/metricdefinitions/Read|Obter as definições de métrica de ambientes de alojamento.|
|/hostingEnvironments/workerPools/Read|Obter propriedades de Olá de um conjunto de trabalho num ambiente de serviço de aplicações|
|/hostingEnvironments/workerPools/Write|Criar um novo conjunto de trabalho num ambiente de serviço de aplicações ou atualizar um já existente|
|/hostingenvironments/workerpools/metricdefinitions/Read|Obter definições de métrica de Workerpools de ambientes de alojamento.|
|/hostingenvironments/workerpools/Metrics/Read|Obter métricas de Workerpools de ambientes de alojamento.|
|/hostingenvironments/workerpools/SKUs/Read|Obter o alojamento de ambientes Workerpools SKUs.|
|/hostingenvironments/workerpools/usages/Read|Obter o alojamento de ambientes Workerpools utilizações.|
|/hostingenvironments/sites/Read|Obter aplicações Web de ambientes de alojamento.|
|/hostingenvironments/serverfarms/Read|Obter planos de serviço de aplicações de ambientes de alojamento.|
|/hostingenvironments/usages/Read|Obter utilizações de ambientes de alojamento.|
|/hostingenvironments/capacities/Read|Obter as capacidades de ambientes de alojamento.|
|/hostingenvironments/Operations/Read|Obter operações de ambientes de alojamento.|
|/hostingEnvironments/multiRolePools/Read|Obter propriedades de Olá de um conjunto de front-end num ambiente de serviço de aplicações|
|/hostingEnvironments/multiRolePools/Write|Criar um novo conjunto de front-end num ambiente de serviço de aplicações ou atualizar um já existente|
|/hostingenvironments/multirolepools/metricdefinitions/Read|Obter as definições de métrica MultiRole conjuntos de ambientes de alojamento.|
|/hostingenvironments/multirolepools/Metrics/Read|Obter métricas de MultiRole conjuntos de ambientes de alojamento.|
|/hostingenvironments/multirolepools/SKUs/Read|Obter SKUs de MultiRole conjuntos de ambientes de alojamento.|
|/hostingenvironments/multirolepools/usages/Read|Obter utilizações MultiRole conjuntos de ambientes de alojamento.|
|/hostingenvironments/Diagnostics/Read|Obter o diagnóstico de ambientes de alojamento.|
|/publishingusers/Read|Obter a publicação os utilizadores.|
|/ publishingusers/escrita|Atualize a publicação de utilizadores.|
|/checknameavailability/Read|Verifique se o nome do recurso está disponível.|
|geoRegions/leitura|Obter a lista de Olá das regiões de Georreplicação.|
|sites/leitura|Obter propriedades de Olá de uma aplicação Web|
|sites/escrita|Criar uma nova aplicação Web ou atualizar um já existente|
|sites/eliminar|Eliminar uma aplicação Web existente|
|/sites/backup/Action|Criar uma nova cópia de segurança de aplicação de web|
|/sites/publishxml/Action|Obtenha o xml do perfil de publicação para uma aplicação Web|
|/sites/publish/Action|Publicar uma aplicação Web|
|/sites/Restart/Action|Reiniciar uma aplicação Web|
|/sites/Start/Action|Iniciar uma aplicação Web|
|/sites/Stop/Action|Parar uma aplicação Web|
|/sites/slotsswap/Action|Trocar ranhuras de implementação de aplicação Web|
|/sites/slotsdiffs/Action|Obter diferenças na configuração de aplicação web e de ranhuras|
|/sites/applySlotConfig/Action|Aplicar a configuração de ranhura de aplicação web da aplicação de web destino ranhura toohello atual|
|/sites/resetSlotConfig/Action|Repor a configuração de aplicação web|
|/sites/Functions/Action|Aplicações Web de funções.|
|/sites/listsyncfunctiontriggerstatus/Action|Lista sincronização função acionar Estado as Web Apps.|
|/sites/networktrace/Action|Aplicações de Web de rastreio de rede.|
|/sites/newpassword/Action|Aplicações newpassword Web.|
|/sites/Sync/Action|Aplicações Web de sincronização.|
|/sites/operationresults/Read|Obter os resultados da operação aplicações Web.|
|/sites/webjobs/Read|Obter WebJobs de aplicações Web.|
|sites/cópia de segurança/leitura|Obter a cópia de segurança do Web Apps.|
|/sites/backup/Write|Atualize a cópia de segurança do Web Apps.|
|/sites/metricdefinitions/Read|Obter definições de métrica de aplicações Web.|
|/sites/Metrics/Read|Obter métricas de aplicações Web.|
|/sites/continuouswebjobs/DELETE|Elimine tarefas de Web contínua de aplicações Web.|
|/sites/continuouswebjobs/Read|Obter as tarefas de Web contínua de aplicações Web.|
|/sites/continuouswebjobs/Start/Action|Inicie tarefas de Web contínua de aplicações Web.|
|/sites/continuouswebjobs/Stop/Action|Pare tarefas de Web contínua de aplicações Web.|
|/sites/domainownershipidentifiers/Read|Obter os identificadores de propriedade de domínio de aplicações Web.|
|/sites/domainownershipidentifiers/Write|Atualize identificadores de propriedade de domínio de aplicações Web.|
|/sites/premieraddons/DELETE|Elimine Addons de Premier de aplicações Web.|
|/sites/premieraddons/Read|Obter Addons de Premier de aplicações Web.|
|/sites/premieraddons/Write|Atualize Addons de Premier de aplicações Web.|
|/sites/triggeredwebjobs/DELETE|Elimine WebJobs accionadas de aplicações Web.|
|/sites/triggeredwebjobs/Read|Obter WebJobs accionadas de aplicações Web.|
|/sites/triggeredwebjobs/Run/Action|Execute Web Apps accionadas WebJobs.|
|/sites/hostnamebindings/DELETE|Elimine enlaces de nome de anfitrião de aplicações Web.|
|/sites/hostnamebindings/Read|Obter os enlaces de nome de anfitrião de aplicações Web.|
|/sites/hostnamebindings/Write|Atualize os enlaces de nome de anfitrião de aplicações Web.|
|/sites/virtualnetworkconnections/DELETE|Elimine ligações de rede Virtual de aplicações Web.|
|/sites/virtualnetworkconnections/Read|Obter ligações de rede Virtual de aplicações Web.|
|/sites/virtualnetworkconnections/Write|Atualize ligações de rede Virtual de aplicações Web.|
|/sites/virtualnetworkconnections/gateways/Read|Obter os Gateways de ligações de rede Virtual de aplicações Web.|
|/sites/virtualnetworkconnections/gateways/Write|Atualize os Gateways de ligações de rede Virtual de aplicações Web.|
|/sites/publishxml/Read|Obterem aplicações Web publicar XML.|
|/sites/hybridconnectionrelays/Read|Obter reencaminhamentos de ligação de híbrida de aplicações Web.|
|/sites/perfcounters/Read|Obter os contadores de desempenho de aplicações Web.|
|/sites/usages/Read|Obter as utilizações de aplicações Web.|
|/sites/slots/Write|Criar uma nova ranhura de aplicação Web ou atualizar um já existente|
|/sites/slots/DELETE|Eliminar uma ranhura de aplicação Web existente|
|/sites/slots/backup/Action|Crie nova cópia de segurança da ranhura de aplicação Web.|
|/sites/slots/publishxml/Action|Obtenha o xml do perfil de publicação para a ranhura de aplicação Web|
|/sites/slots/publish/Action|Publicar uma ranhura de aplicação Web|
|/sites/slots/Restart/Action|Reiniciar uma ranhura de aplicação Web|
|/sites/slots/Start/Action|Iniciar uma ranhura de aplicação Web|
|/sites/slots/Stop/Action|Parar uma ranhura de aplicação Web|
|/sites/slots/slotsswap/Action|Trocar ranhuras de implementação de aplicação Web|
|/sites/slots/slotsdiffs/Action|Obter diferenças na configuração de aplicação web e de ranhuras|
|/sites/slots/applySlotConfig/Action|Aplica a configuração de ranhura de aplicação web a partir da ranhura atual de toohello do bloco de destino.|
|/sites/slots/resetSlotConfig/Action|Repor a configuração de ranhura de aplicação web|
|/sites/slots/Read|Obter propriedades de Olá de uma ranhura de implementação de aplicação Web|
|/sites/slots/newpassword/Action|Ranhuras de aplicações newpassword Web.|
|/sites/slots/Sync/Action|Ranhuras de aplicações Web de sincronização.|
|/sites/slots/operationresults/Read|Obter resultados de operação de ranhuras de aplicações Web.|
|/sites/slots/webjobs/Read|Obter WebJobs de ranhuras de aplicações Web.|
|/sites/slots/backup/Write|Atualize a cópia de segurança de ranhuras de aplicações de Web.|
|/sites/slots/metricdefinitions/Read|Obter definições de métrica de ranhuras de aplicações de Web.|
|/sites/slots/Metrics/Read|Obter métricas de ranhuras de aplicações Web.|
|/sites/slots/continuouswebjobs/DELETE|Elimine tarefas de Web contínua de ranhuras de aplicações Web.|
|/sites/slots/continuouswebjobs/Read|Obter tarefas de Web contínua de ranhuras de aplicações Web.|
|/sites/slots/continuouswebjobs/Start/Action|Inicie tarefas de Web contínua de ranhuras de aplicações Web.|
|/sites/slots/continuouswebjobs/Stop/Action|Pare tarefas de Web contínua de ranhuras de aplicações Web.|
|/sites/slots/premieraddons/DELETE|Elimine Addons de Premier de ranhuras de aplicações Web.|
|/sites/slots/premieraddons/Read|Obter Addons de Premier de ranhuras de aplicações Web.|
|/sites/slots/premieraddons/Write|Atualize Addons de Premier de ranhuras de aplicações Web.|
|/sites/slots/triggeredwebjobs/DELETE|Elimine as Web Apps ranhuras accionadas WebJobs.|
|/sites/slots/triggeredwebjobs/Read|Obter Web Apps ranhuras accionadas WebJobs.|
|/sites/slots/triggeredwebjobs/Run/Action|Execute Web Apps ranhuras accionadas WebJobs.|
|/sites/slots/hostnamebindings/DELETE|Elimine enlaces de nome de anfitrião de ranhuras de aplicações Web.|
|/sites/slots/hostnamebindings/Read|Obter os enlaces de nome de anfitrião de ranhuras de aplicações Web.|
|/sites/slots/hostnamebindings/Write|Atualize os enlaces de nome de anfitrião de ranhuras de aplicações Web.|
|/sites/slots/phplogging/Read|Obter Phplogging de ranhuras de aplicações Web.|
|/sites/slots/virtualnetworkconnections/DELETE|Elimine ligações de rede Virtual de ranhuras de aplicações Web.|
|/sites/slots/virtualnetworkconnections/Read|Obter ligações de rede Virtual de ranhuras de aplicações Web.|
|/sites/slots/virtualnetworkconnections/Write|Atualize ligações de rede Virtual de ranhuras de aplicações Web.|
|/sites/slots/virtualnetworkconnections/gateways/Write|Atualize os Gateways de ligações de rede Virtual de ranhuras aplicações Web.|
|/sites/slots/usages/Read|Obter as utilizações de ranhuras de aplicações Web.|
|/sites/slots/hybridconnection/DELETE|Elimine a ligação de híbrida de ranhuras de aplicações Web.|
|/sites/slots/hybridconnection/Read|Obter aplicações da Web ranhuras ligação híbrida.|
|/sites/slots/hybridconnection/Write|Atualize ligação de híbrida de ranhuras de aplicações Web.|
|/sites/slots/config/Read|Obter as definições de configuração da ranhura de aplicação Web|
|/sites/slots/config/List/Action|Lista confidenciais definições de segurança da ranhura de aplicação Web, tais como publicar as credenciais, as definições de aplicação e as cadeias de ligação|
|/sites/slots/config/Write|Atualizar as definições de configuração da ranhura de aplicação Web|
|/sites/slots/config/DELETE|Elimine a configuração de ranhuras de aplicações Web.|
|/sites/slots/instances/Read|Obter instâncias de ranhuras de aplicações Web.|
|/sites/slots/instances/processes/Read|Obter os processos de instâncias de ranhuras de aplicações Web.|
|/sites/slots/instances/Deployments/Read|Obter implementações de instâncias de ranhuras de aplicações Web.|
|/sites/slots/sourcecontrols/Read|Obter as definições de configuração de controlo de origem da ranhura de aplicação Web|
|/sites/slots/sourcecontrols/Write|Atualizar definições de configuração de controlo de origem da ranhura de aplicação Web|
|/sites/slots/sourcecontrols/DELETE|Eliminar definições de configuração de controlo de origem da ranhura de aplicação Web|
|/sites/slots/Restore/Read|Obter o restauro de ranhuras de aplicações Web.|
|/sites/slots/analyzecustomhostname/Read|Introdução a Web Apps ranhuras analisam o nome do anfitrião personalizado.|
|/sites/slots/backups/Read|Obter propriedades de Olá da cópia de segurança dos ranhuras de aplicação um web|
|/sites/slots/backups/List/Action|Cópias de segurança da ranhuras de aplicações do Web de lista.|
|/sites/slots/backups/Restore/Action|Restaure cópias de segurança de ranhuras de aplicações de Web.|
|/sites/slots/Deployments/DELETE|Elimine as implementações de ranhuras de aplicações Web.|
|/sites/slots/Deployments/Read|Obter implementações de ranhuras de aplicações Web.|
|/sites/slots/Deployments/Write|Atualize as implementações de ranhuras de aplicações Web.|
|/sites/slots/Deployments/log/Read|Obter o registo de implementações de ranhuras de aplicações Web.|
|/sites/hybridconnection/DELETE|Elimine a ligação de híbrida de aplicações Web.|
|/sites/hybridconnection/Read|Obter da ligação híbrida de aplicações Web.|
|/sites/hybridconnection/Write|Atualize da ligação híbrida de aplicações Web.|
|/sites/recommendationhistory/Read|Obter o histórico de recomendação de aplicações Web.|
|/sites/recommendations/Read|Obter a lista de Olá recomendações para a aplicação web.|
|/sites/recommendations/disable/Action|Desative as recomendações de aplicações Web.|
|/sites/config/Read|Obter definições de configuração de aplicação Web|
|/sites/config/List/Action|Lista confidenciais definições de segurança da aplicação Web, tais como publicar as credenciais, as definições de aplicação e as cadeias de ligação|
|/sites/config/Write|Atualizar as definições de configuração da aplicação Web|
|/sites/config/DELETE|Elimine a configuração de aplicações Web.|
|/sites/instances/Read|Obter instâncias de aplicações Web.|
|/sites/instances/processes/DELETE|Elimine processos de instâncias de aplicações Web.|
|/sites/instances/processes/Read|Obter os processos de instâncias de aplicações Web.|
|/sites/instances/Deployments/Read|Obter implementações de instâncias de aplicações Web.|
|/sites/sourcecontrols/Read|Obter as definições de configuração de controlo de origem da aplicação Web|
|/sites/sourcecontrols/Write|Atualizar definições de configuração de controlo de origem da aplicação Web|
|/sites/sourcecontrols/DELETE|Eliminar definições de configuração de controlo de origem da aplicação Web|
|/sites/Restore/Read|Obter o restauro de aplicações Web.|
|/sites/analyzecustomhostname/Read|Analise o nome do anfitrião personalizado.|
|/sites/backups/Read|Obter propriedades de Olá da cópia de segurança de uma aplicação web|
|/sites/backups/List/Action|Lista Web Apps as cópias de segurança.|
|/sites/backups/Restore/Action|Restaure cópias de segurança do Web Apps.|
|/sites/snapshots/Read|Obter instantâneos de aplicações Web.|
|/sites/Functions/DELETE|Elimine funções de aplicações Web.|
|/sites/Functions/listsecrets/Action|Lista os segredos Web Apps funções.|
|/sites/Functions/Read|Obter as funções de aplicações Web.|
|/sites/Functions/Write|Atualize funções de aplicações Web.|
|/sites/Deployments/DELETE|Elimine as implementações de aplicações Web.|
|/sites/Deployments/Read|Obter implementações de aplicações Web.|
|/sites/Deployments/Write|Atualize as implementações de aplicações Web.|
|/sites/Deployments/log/Read|Obter o registo de implementações de aplicações Web.|
|/sites/Diagnostics/Read|Obter o diagnóstico de aplicações Web.|
|/sites/Diagnostics/workerprocessrecycle/Read|Obter a Reciclagem de processo de trabalho de diagnóstico de aplicações Web.|
|/sites/Diagnostics/workeravailability/Read|Obter Workeravailability de diagnóstico de aplicações Web.|
|/sites/Diagnostics/runtimeavailability/Read|Obter a disponibilidade de tempo de execução de diagnóstico de aplicações Web.|
|/sites/Diagnostics/cpuanalysis/Read|Obter Cpuanalysis de diagnóstico de aplicações Web.|
|/sites/Diagnostics/servicehealth/Read|Obter o estado de funcionamento de serviço Web diagnóstico de aplicações.|
|/sites/Diagnostics/frebanalysis/Read|Obter a análise FREB de diagnóstico de aplicações Web.|
|/availablestacks/Read|Obter pilhas disponíveis.|
|/isusernameavailable/Read|Verifique se o nome de utilizador está disponível.|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/leitura|Obter a lista de Olá de Apis.|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/escrita|Adicionar uma nova Api ou Atualize uma existente.|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/eliminar|Elimine uma Api existente.|
|/Microsoft.Web/apiManagementAccounts/<br>ligações/APIs/leitura|Obter a lista de Olá de ligações.|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/ligações/escrita|Guardar uma nova ligação ou atualizar um já existente.|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/ligações/eliminar|Elimine uma ligação existente.|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/ligações/connectionAcls/leitura|Ler ConnectionAcls|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/ligações/connectionAcls/escrita|Adicionar ou atualizar ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/ligações/connectionAcls/eliminar|Eliminar ConnectionAcl|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/connectionAcls/leitura|Ler ConnectionAcls para Api|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/apiAcls/leitura|Ler ConnectionAcls|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/apiAcls/escrita|Criar ou atualizar as Acls de Api|
|/Microsoft.Web/apiManagementAccounts/<br>APIs/apiAcls/eliminar|Eliminar a ACL de Api|
|serverfarms/leitura|Obter propriedades de Olá num plano do App Service|
|serverfarms/escrita|Criar um novo plano do App Service ou atualizar um já existente|
|serverfarms/eliminar|Eliminar uma existente plano do App Service|
|/serverfarms/restartSites/Action|Reiniciar todas as aplicações Web dentro de um plano do App Service|
|/serverfarms/operationresults/Read|Obter os resultados da operação planos do serviço de aplicações.|
|/serverfarms/Capabilities/Read|Obter capacidades de planos do App Service.|
|/serverfarms/metricdefinitions/Read|Obter as definições de métrica de planos do serviço de aplicações.|
|/serverfarms/Metrics/Read|Obter métricas de planos de serviço de aplicações.|
|/serverfarms/hybridconnectionplanlimits/Read|Obter os limites de plano de ligação do serviço de aplicações planos híbrida.|
|/serverfarms/virtualnetworkconnections/Read|Obter as ligações de rede Virtual de planos de serviço de aplicações.|
|/serverfarms/virtualnetworkconnections/routes/DELETE|Elimine rotas de ligações de rede Virtual de planos de serviço de aplicações.|
|/serverfarms/virtualnetworkconnections/routes/Read|Obter rotas de ligações de rede Virtual de planos de serviço de aplicações.|
|/serverfarms/virtualnetworkconnections/routes/Write|Atualize rotas de ligações de rede Virtual de planos de serviço de aplicações.|
|/serverfarms/virtualnetworkconnections/gateways/Write|Atualize os Gateways de ligações de rede Virtual de planos de serviço de aplicações.|
|/serverfarms/firstpartyapps/Settings/DELETE|Elimine o serviço de aplicações planos primeiro intervenientes as definições de aplicações.|
|/serverfarms/firstpartyapps/Settings/Read|Obter definições de aplicações intervenientes primeiro planos do serviço de aplicações.|
|/serverfarms/firstpartyapps/Settings/Write|Atualize definições de aplicações da primeira planos do serviço de aplicações.|
|/serverfarms/sites/Read|Obter aplicações de Web de planos do App Service.|
|/serverfarms/Workers/reboot/Action|Reinicie trabalhadores de planos de serviço de aplicações.|
|/serverfarms/hybridconnectionrelays/Read|Obter planos de serviço de aplicações híbridas reencaminhamentos de ligação.|
|/serverfarms/SKUs/Read|Obter SKUs de planos de serviço de aplicações.|
|/serverfarms/usages/Read|Obter utilizações de planos de serviço de aplicações.|
|/serverfarms/hybridconnectionnamespaces/relays/sites/Read|Obter planos do serviço de aplicações híbridas ligação espaços de nomes reencaminhamentos da aplicações Web.|
|/ishostnameavailable/Read|Verifique se o nome do anfitrião está disponível.|
|connectionGateways/leitura|Obter a lista de Olá dos Gateways de ligação.|
|connectionGateways/escrita|Cria ou atualiza um Gateway de ligação.|
|connectionGateways/eliminar|Elimina um Gateway de ligação.|
|/connectionGateways/JOIN/Action|Associa um Gateway de ligação.|
|/classicmobileservices/Read|Obter clássicos Mobile Services.|
|/SKUs/Read|Obter SKUs.|
|certificados/leitura|Obter a lista de Olá de certificados.|
|certificados/escrita|Adicionar um certificado novo ou atualizar um já existente.|
|certificados/eliminar|Elimine um certificado existente.|
|/Operations/Read|Obter operações.|
|recomendações/leitura|Obter a lista de Olá recomendações para subscrições.|
|/ishostingenvironmentnameavailable/Read|Get se o nome do ambiente de alojamento está disponível.|
|apiManagementAccounts/leitura|Obter a lista de Olá de ApiManagementAccounts.|
|apiManagementAccounts/escrita|Adicionar um novo ApiManagementAccount ou atualizar um já existente|
|apiManagementAccounts/eliminar|Eliminar um ApiManagementAccount existente|
|/apiManagementAccounts/connectionAcls/Read|Obter a lista de Olá das Acls de ligação.|
|/apiManagementAccounts/apiAcls/Read|Ler ConnectionAcls|
|ligações/leitura|Obter a lista de Olá de ligações.|
|ligações/escrita|Cria ou atualiza uma ligação.|
|ligações/eliminar|Elimina uma ligação.|
|/Connections/JOIN/Action|Associa uma ligação.|
|/Connections/confirmconsentcode/Action|Confirme o código de autorização de ligações.|
|/Connections/listconsentlinks/Action|Ligações de consentimento de lista de ligações.|
|/deploymentlocations/Read|Obter as localizações de implementação.|
|/sourcecontrols/Read|Obter controlos de origem.|
|/ sourcecontrols/escrita|Controlos de origem de atualização.|
|/managedhostingenvironments/Read|Obter geridos ambientes de alojamento.|
|/managedhostingenvironments/sites/Read|Obter geridos aplicações Web de ambientes de alojamento.|
|/managedhostingenvironments/serverfarms/Read|Obter geridos planos de serviço de aplicações de ambientes de alojamento.|
|/Locations/managedapis/Read|Obter as localizações de APIs geridas.|
|/Locations/apioperations/Read|Obter operações de API de localizações.|
|/Locations/connectiongatewayinstallations/Read|Obter instalações de Gateway de ligação de localizações.|
|listSitesAssignedToHostName/leitura|Obter os nomes dos sites atribuídos toohostname.|

## <a name="next-steps"></a>Passos seguintes

- Saiba como demasiado[criar uma função personalizada](role-based-access-control-custom-roles.md).

- Olá revisão [RBAC funções incorporadas](role-based-access-built-in-roles.md).

- Saiba como toomanage aceder às atribuições [por utilizador](role-based-access-control-manage-assignments.md) ou [por recurso](role-based-access-control-configure.md) 
