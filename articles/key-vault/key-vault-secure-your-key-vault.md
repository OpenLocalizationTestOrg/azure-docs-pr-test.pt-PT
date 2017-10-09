---
title: aaaSecure a chave de cofre | Microsoft Docs
description: "Administre as permissões de acesso ao cofre de chaves para gerir cofres, chaves e segredos. Modelo de autenticação e autorização para o Cofre de chaves e como toosecure a chave do Cofre"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>Proteger o seu cofre de chaves
O Cofre de Chaves do Azure é um serviço em nuvem que protege chaves e segredos de encriptação (como certificados, cadeias de ligação e palavras-passe) das suas aplicações na nuvem. Uma vez que estes dados sensíveis e crítico de negócio, pretende cofres de chaves toosecure acesso tooyour, de modo a que apenas pessoal autorizado aplicações e os utilizadores podem aceder Cofre de chaves. Este artigo fornece uma descrição geral do modelo de Cofre de chaves de acesso, explica a autenticação e autorização e descreve como toosecure acesso tookey cofre para as suas aplicações em nuvem com um exemplo.

## <a name="overview"></a>Descrição geral
O Cofre de chaves do acesso tooa é controlado através de duas interfaces de rede separadas: plane de gestão e plane de dados. Em ambos os planos adequada autenticação e autorização é necessária antes de um emissor (um utilizador ou uma aplicação) pode obter o Cofre de tookey de acesso. Autenticação estabelece a identidade de Olá do autor da chamada Olá, enquanto autorização determina que chamador de Olá operações permitido tooperform.

Tanto o plano de gestão, como o de dados, utilizam o Azure Active Directory na autenticação. Relativamente à autorização, o plano de gestão utiliza o controlo de acesso baseado em funções (RBAC) e o plano de dados utiliza a política de acesso ao cofre de chaves.

Eis uma breve descrição geral dos tópicos de Olá abrangidos:

[A autenticação utilizando o Azure Active Directory](#authentication-using-azure-active-directory) -esta secção explica como um emissor efetua a autenticação com o Azure Active Directory tooaccess um cofre de chaves através de plane de gestão e plane de dados. 

[Plano de gestão e plano de dados](#management-plane-and-data-plane) - o plano de gestão e o plano de dados são dois planos de acesso utilizados para aceder aos seus cofres de chaves. Cada plano de acesso suporta operações específicas. Esta secção descreve pontos finais de acesso de Olá, as operações suportadas e utilizado por cada plane de método de controlo de acesso. 

[Controlo de acesso de plane gestão](#management-plane-access-control) - nesta secção, vamos abordar permitir o acesso operações de plane toomanagement utilizando o controlo de acesso baseado em funções.

[Controlo de acesso do dados plane](#data-plane-access-control) -esta secção descreve como dados de toocontrol de política de acesso de Cofre de chaves toouse plane acesso.

[Exemplo](#example) -este exemplo descreve a forma como o controlo para os Cofre de chaves tooallow três equipas diferentes (equipa de segurança, os programadores/operadores e auditores) de acesso de toosetup tooperform tarefas específicas toodevelop, gerir e monitorizar uma aplicação no Azure .

## <a name="authentication-using-azure-active-directory"></a>Autenticação com o Azure Active Directory
Quando criar um cofre de chaves numa subscrição do Azure, é automaticamente associado ao inquilino do Azure Active Directory da subscrição Olá. Todos os chamadores (utilizadores e aplicações) tem de ser registado no tooaccess inquilino neste Cofre de chaves. Uma aplicação ou um utilizador tem de autenticar com o Cofre de chaves do Azure Active Directory tooaccess. Isto aplica-se tooboth plane de gestão e plane dados acesso. Em ambos os casos, as aplicações podem aceder a um cofre de chaves de duas formas:

* **acesso de utilizador+aplicação** - normalmente, destina-se a aplicações que acedem a cofres de chaves em nome de um utilizador com sessão iniciada. O Azure PowerShell e o Portal do Azure são dois exemplos deste tipo de acesso. Existem duas formas toogrant acesso toousers: unidirecional está toogrant acesso toousers para que podem aceder Cofre de chaves a partir de qualquer aplicação e Olá outra forma toogrant um cofre de tookey de acesso de utilizador apenas se estiverem a utilizar uma aplicação específica (referidos tooas de identidade composta). 
* **acesso só de aplicação** – para aplicações que executar os serviços de daemon, tarefas em segundo plano identidade da aplicação Olá etc. é concedida acesso toohello Cofre de chaves.

Em ambos os tipos de aplicações, a aplicação Olá autentica com o Azure Active Directory utilizando qualquer um dos Olá [suportados métodos de autenticação](../active-directory/active-directory-authentication-scenarios.md) e adquirir um token. Método de autenticação utilizado depende do tipo de aplicação Olá. Em seguida, a aplicação de Olá utiliza este token e envia o Cofre de tookey de pedido de REST API. Em caso de Olá de acesso de plane de gestão pedidos são encaminhados através de ponto final do Azure Resource Manager. Quando aceder plane de dados, aplicações de Olá sua diretamente ponto final do Cofre de chaves de tooa. Ver mais detalhes sobre Olá [fluxo de autenticação todo](../active-directory/active-directory-protocols-oauth-code.md). 

nome do recurso Olá para o qual a aplicação de Olá solicita um token é diferente consoante se aplicação Olá está a aceder aos plane de gestão ou plane de dados. Por conseguinte, o nome do recurso de Olá é o plane ou dados plane ponto final de gestão descrita na tabela de Olá numa secção posterior, consoante Olá ambiente do Azure.

Ter um mecanismo único para autenticação tooboth plane de gestão e dados tem as suas próprias vantagens:

* As organizações podem controlar centralmente o acesso cofres de chaves de tooall na respetiva organização
* Se um utilizador deixa, estes instantaneamente perderem o acesso tooall cofres de chaves na organização de Olá
* As organizações podem personalizar a autenticação através de opções de Olá no Azure Active Directory (por exemplo, ativar autenticação multifator para segurança adicional)

## <a name="management-plane-and-data-plane"></a>Plano de gestão e plano de dados
O Cofre de Chaves do Azure é um serviço do Azure que está disponível através do modelo de implementação Azure Resource Manager. Quando cria um cofre de chaves, recebe um contentor virtual dentro do qual pode criar outros objetos, como chaves, segredos e certificados. Em seguida, aceder ao seu Cofre de chaves utilizando plane e dados plane tooperform específicas operações de gestão. Interface de gestão de plane é toomanage utilizada a chave de cofre próprio, como criar, eliminar, atualizar os atributos do Cofre de chaves e definir políticas de acesso para plane de dados. Interface de plane de dados é utilizada tooadd, eliminar, modificar e utilizar chaves de Olá, os segredos e certificados armazenados no seu Cofre de chaves.

Olá plane e dados plane interfaces de gestão são acedidas através de pontos finais diferentes (veja a tabela). segunda coluna de Olá na tabela de Olá descreve os nomes DNS de Olá para estes pontos finais em diferentes ambientes do Azure. coluna terceira Olá descreve as operações de Olá que pode executar a partir de cada plane de acesso. Cada um dos planos de acesso tem também o seu próprio mecanismo de controlo de acesso. No plano de gestão, o controlo de acesso é definido com o Controlo de Acesso Baseado em Funções (RBAC) do Azure Resource Manager, ao passo que, no plano de dados, o controlo de acesso é definido através da política de acesso do cofre de chaves.

| Plano de acesso | Pontos finais de acesso | Operações | Mecanismo de controlo de acesso |
| --- | --- | --- | --- |
| Plano de gestão |**Global:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure US Government:**<br> management.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> management.microsoftazure.de:443 |Criar/Ler/Atualizar/Eliminar cofre de chaves <br> Definir políticas de acesso ao cofre de chaves<br>Definir etiquetas para o cofre de chaves |Controlo de Acesso Baseado em Funções (RBAC) do Azure Resource Manager |
| Plano de dados |**Global:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure US Government:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |Em chaves: desencriptar, encriptar, unwrapKey, wrapKey, verificar, assinar, obter, listar, atualizar, criar, importar, eliminar, fazer cópia de segurança, restaurar<br><br> Em segredos: obter, listar, definir, eliminar |Política de acesso do cofre de chaves |

Olá gestão plane e dados plane controlos de acesso funcionam de forma independente. Por exemplo, se quiser toogrant um toouse chaves de acesso da aplicação no Cofre de chaves, só precisa de toogrant dados plane permissões de acesso utilizando as políticas de acesso do Cofre de chaves e sem acesso de plane de gestão é necessária para esta aplicação. E, por outro lado, se pretender que um utilizador toobe capaz de tooread etiquetas e propriedades do cofre, mas não tem qualquer acesso tookeys, segredos ou certificados, pode conceder este utilizador, é necessário acesso 'read' utilizar o RBAC e nenhum plane toodata de acesso.

## <a name="management-plane-access-control"></a>Controlo de acesso do plano de gestão
plane de gestão de Olá consiste em operações que afetam o Cofre de chaves Olá próprio. Por exemplo, pode criar ou eliminar um cofre de chaves. Pode ver uma lista dos cofres numa subscrição. Pode obter as propriedades do Cofre de chaves (por exemplo, o SKU, etiquetas) e definir políticas de acesso que controlam os utilizadores de Olá e aplicações que podem aceder às chaves e segredos no Cofre de chaves Olá o Cofre de chaves. O controlo de acesso do plano de gestão utiliza o RBAC. Consulte a lista completa de Olá de operações do Cofre de chaves que podem ser efetuadas por plane de gestão na tabela Olá anterior a secção. 

### <a name="role-based-access-control-rbac"></a>Controlo de Acesso Baseado em Funções (RBAC)
Cada subscrição do Azure tem um Azure Active Directory. Os utilizadores, grupos e aplicações a partir deste diretório podem ser concedidas acesso toomanage recursos Olá subscrição do Azure que utilizam o modelo de implementação Azure Resource Manager Olá. Este tipo de controlo de acesso é referenciado tooas controlo de acesso baseado em funções (RBAC). toomanage isto aceder, pode utilizar Olá [portal do Azure](https://portal.azure.com/), Olá [ferramentas da CLI do Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou Olá [REST APIsdoAzureResourceManager](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Com o modelo do Azure Resource Manager Olá, criar seu Cofre de chaves num recurso grupo e o controlo de acesso toohello gestão plane neste Cofre de chaves utilizando o Azure Active Directory. Por exemplo, pode conceder a utilizadores ou um grupo capacidade toomanage cofres de chaves num grupo de recursos específico.

Pode conceder acesso toousers, grupos e aplicações a um âmbito específico por atribuir funções de RBAC adequadas. Por exemplo, toogrant aceder tooa utilizador toomanage cofres de chaves, teria de atribuir um função predefinida 'Cofre de chaves Contribuinte' toothis utilizador a um âmbito específico. âmbito de Olá neste caso, seria uma subscrição, um grupo de recursos ou apenas um cofre de chaves específico. Uma função atribuída ao nível da subscrição aplica-se grupos de recursos de tooall e de recursos dentro dessa subscrição. Uma função atribuída ao nível do grupo de recursos aplica-se tooall recursos nesse grupo de recursos. Uma função atribuída para um recurso específico só se aplica toothat recursos. Existem várias funções predefinidas (consulte [RBAC: funções incorporadas](../active-directory/role-based-access-built-in-roles.md)), e se Olá predefinidas funções não atender às suas necessidades, também pode definir as suas próprias funções.

> [!IMPORTANT]
> Tenha em atenção que se um utilizador tiver plane de gestão do Cofre de chaves do Contribuidor permissões (RBAC) tooa, ela pode conceder herself plane de toodata de acesso, através da definição de política de acesso do Cofre de chaves, que controla plane toodata de acesso. Por conseguinte, é recomendado tootightly controlo que tenha contribuinte acesso tooyour cofres de chaves tooensure apenas pessoas autorizadas podem aceder e gerir os seus cofres de chaves, chaves, segredos e certificados.
> 
> 

## <a name="data-plane-access-control"></a>Controlo de acesso do plano de dados
plane de dados do Cofre de chaves Olá consiste em operações que afetam os objetos de Olá no Cofre de chaves, tais como certificados, chaves e segredos.  Incluem operações de chaves, como criar, importar, atualizar, listar, criar cópias de segurança e restaurar chaves, e operações criptográficas, como assinar, verificar, encriptar, desencriptar, encapsular, anular o encapsulamento e definir etiquetas e outros atributos de chaves. Do mesmo modo, relativamente a segredos, inclui obter, definir, listar e eliminar.

O acesso do plano de dados é concedido mediante a definição de políticas de acesso a cofres de chaves. Um utilizador, grupo ou uma aplicação tem de ter permissões de contribuinte (RBAC) para plane de gestão para um cofre de chaves toobe tooset capaz de políticas de acesso que Cofre de chaves. Um utilizador, grupo ou aplicação pode ser concedida acesso tooperform operações específicas para as chaves ou segredos no Cofre de chaves. Suporte do Cofre de chaves segurança too16 entradas de política de acesso para um cofre de chaves. Criar um grupo de segurança do Azure Active Directory e adicionar utilizadores toothat grupo toogrant dados plane acesso tooseveral utilizadores tooa Cofre de chaves.

### <a name="key-vault-access-policies"></a>Políticas de Acesso dos cofres de chaves
As políticas de acesso do Cofre de chaves de conceder permissões tookeys, os segredos e certificados em separado. Por exemplo, pode dar um chaves de tooonly de acesso de utilizador, mas sem permissões para segredos. No entanto, as chaves de tooaccess de permissões ou segredos ou certificados estão no nível de Cofre de Olá. Por outras palavras, a política de acesso do cofre de chaves não suporta permissões ao nível do objeto. Pode utilizar [portal do Azure](https://portal.azure.com/), Olá [ferramentas da CLI do Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou Olá [Cofre de chaves APIs REST de gestão](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset as políticas de acesso para um cofre de chaves.

> [!IMPORTANT]
> Tenha em atenção que se aplicam políticas de acesso do Cofre de chaves ao nível do Cofre de Olá. Por exemplo, quando um utilizador é concedido permissão toocreate e eliminar as chaves, ela pode efetuar as operações em todas as chaves nesse Cofre de chaves.
> 
> 

## <a name="example"></a>Exemplo
Imaginemos que está a desenvolver uma aplicação que utiliza um certificado para SSL, o Armazenamento do Azure para armazenar dados e uma chave RSA de 2048 bits para operações de assinatura. Imaginemos, agora, que a aplicação é executada numa VM (ou num Conjunto de Dimensionamento de VM). Pode utilizar um toostore do Cofre de chaves que todas Olá segredos de aplicação e utilizar Cofre de chaves toostore Olá arranque um certificado que é utilizado pelo Olá tooauthenticate de aplicação no Azure Active Directory.

Por isso, eis um resumo de todos os Olá chaves e segredos toobe armazenados no Cofre de chaves.

* **Certificado SSL** - utilizado para SSL
* **Chave de armazenamento** -utilizou tooget acesso tooStorage conta
* **Chave RSA de 2048 bits** - utilizada para operações de assinatura
* **Certificado de arranque de configuração** -utilizada tooauthenticate tooAzure do Active Directory, tooget acesso tookey cofre toofetch Olá chave do storage e utilize Olá RSA chave para assinatura.

Agora vamos cumprir as pessoas de Olá que estiver a gerir, implementar e auditoria esta aplicação. Vamos utilizar três funções neste exemplo.

* **Equipa de segurança** - estes são, normalmente, a equipa de TI do office' Olá de Olá CSO (responsável diretor pela segurança)' ou equivalente, é responsável por Olá salvaguarda adequada de segredos, tais como certificados de SSL, chaves RSA utilizadas para assinatura, cadeias de ligação bases de dados, chaves de conta de armazenamento.
* **Os programadores/operadores** -estes são os utilizadores de Olá que desenvolver esta aplicação e, em seguida, implementação-la no Azure. Normalmente, que não fazem parte da equipa de segurança de Olá e, por conseguinte, não devem ter acesso tooany dados confidenciais, tais como certificados SSL, chaves RSA, mas aplicação Olá que implementam deve ter acesso toothose.
* **Auditores** -trata-se normalmente um conjunto diferente de pessoas, isoladas entre os programadores de Olá e geral equipa de TI. Os respetivos responsabilidade utilização adequada tooreview e manutenção de certificados, chaves, etc. e garantir a conformidade com as normas de segurança de dados. 

Há uma função mais exteriores Olá âmbito desta aplicação, mas relevante toobe aqui mencionados, e que seria subscrição hello (ou grupo de recursos) administrador. Administrador de subscrição configura as permissões de acesso inicial para a equipa de segurança de Olá. Aqui partimos do princípio que administrador de subscrição de Olá concedeu acesso toohello segurança equipa tooa grupo de recursos no qual Olá todos os recursos necessários a esta reside de aplicação.

Agora vamos ver que ações executa cada função no contexto de Olá desta aplicação.

* **Equipa de segurança**
  * Criar cofres de chaves
  * Ativar o registo de cofres de chaves
  * Adicionar chaves/segredos
  * Criar cópias de segurança de chaves para recuperação após desastres
  * Definir acesso ao Cofre de chaves de política toogrant permissões toousers e aplicações tooperform operações específicas
  * Lançar periodicamente chaves/segredos
* **Programadores/operadores**
  * Obter as referências toobootstrap e certificados SSL (thumbprints), a chave de armazenamento (segredo URI) e chave (chave URI) da equipa de segurança de início de sessão
  * Desenvolver e implementar aplicações que acedam a chaves e segredos programaticamente
* **Auditores**
  * Reveja a utilização de chave/segredo utilização registos tooconfirm adequada e a conformidade com as normas de segurança de dados

Agora vamos ver que Cofre de tookey de permissões de acesso necessários para cada função (e aplicação Olá) tooperform as respetivas tarefas atribuídas. 

| Função de Utilizador | Permissões do plano de gestão | Permissões do plano de dados |
| --- | --- | --- |
| Equipa de Segurança |Contribuinte do cofre de chaves |Chaves: criar cópia de segurança, criar, eliminar, obter, importar, listar, restaurar <br> Segredos: todas |
| Programadores/operadores |cofre da chave de implementar permissão para VMs Olá que implementam podem obter segredos do Cofre de chaves Olá |Nenhuma |
| Auditores |Nenhuma |Chaves: listar<br>Segredos: listar |
| Aplicação |Nenhuma |Chaves: assinar<br>Segredos: obter |

> [!NOTE]
> Auditores tem de listar permissão para chaves e segredos, de modo que podem inspecionar os atributos de chaves e segredos que não são emitidos nos registos de Olá, tais como etiquetas, ativação e expiração datas.
> 
> 

Para além do Cofre de tookey de permissão, todas as funções de três também precisam de aceder a recursos tooother. Por exemplo, toobe capaz de toodeploy VMs (ou Web Apps etc.) Os programadores/operadores também precisa de tipos de recursos de toothose de acesso 'Contribuinte'. Auditores tem acesso de leitura toohello conta do storage onde os registos do Cofre de chaves Olá são armazenados.

Uma vez que o foco de Olá deste artigo está a proteger o Cofre de chaves do acesso tooyour, iremos apenas ilustrar partes relevantes Olá relativas toothis tópico e ignorar detalhes sobre a implementação de certificados, aceder programaticamente etc chaves e segredos. Esses detalhes já estão mencionados noutro artigo. Implementar certificados armazenados no Cofre de chaves tooVMs é abordada um [blogue](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/)e não existe [código de exemplo](https://www.microsoft.com/download/details.aspx?id=45343) disponíveis que ilustra como toouse arranque certificado tooauthenticate tooAzure AD tooget cofre do tookey de acesso.

Na maioria das permissões de acesso de Olá pode ser concedida através do portal do Azure, mas permissões granulares toogrant poderá ser necessário toouse Azure PowerShell (ou a CLI do Azure) tooachieve Olá o resultado pretendido. 

partem do princípio de Olá seguintes fragmentos do PowerShell:

* administrador do Azure Active Directory Olá criou os grupos de segurança que representam funções Olá três, nomeadamente equipa de segurança de Contoso, Devops de aplicação Contoso, auditores de aplicação de Contoso. administrador Olá tenha também adicionado utilizadores toohello grupos que pertencem.
* **ContosoAppRG** é o grupo de recursos de olá onde todos os recursos de Olá residem. **contosologstorage** é onde Olá registos são armazenados. 
* Cofre da chave **ContosoKeyVault** e conta de armazenamento utilizado para os registos do Cofre de chaves **contosologstorage** tem de ser Olá mesma localização do Azure

Primeiro administrador de subscrição de Olá atribui 'cofre contribuinte da chave' e a equipa de segurança ' Administrador de acesso de utilizador ' Funções toohello. Isto permite Olá segurança equipa toomanage aceder tooother a recursos e gerir cofres de chaves num grupo de recursos de Olá ContosoAppRG.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

Olá script a seguir ilustra como equipa de segurança de Olá pode criar um cofre de chaves, o registo de configuração e definir permissões de acesso para outras funções e a aplicação Olá. 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

função personalizada Olá definido, só pode ser atribuído toohello subscrição em que o grupo de recursos de ContosoAppRG Olá é criado. Se hello funções personalizadas mesmas serão utilizadas para outros projetos em outras subscrições, de âmbito pode ter mais subscrições adicionadas.

atribuição de função personalizada Olá para os programadores de Olá/operadores da permissão de "implementar/action" Olá é confinada toohello grupo de recursos. Desta forma apenas Olá VMs criada no grupo de recursos de Olá 'ContosoAppRG' irá obter segredos Olá (certificado SSL e certificados de arranque do sistema). As VMs que cria um membro da equipa de desenvolvimento/ops noutro grupo de recursos não serão capaz tooget estes segredos, mesmo que estes deverem segredo Olá URIs.

Este exemplo mostra um cenário simples. Cenários de vida real podem ser mais complexos e poderá ser necessário tooadjust permissões tooyour Cofre de chaves com base nas suas necessidades. Por exemplo, no nosso exemplo, partimos do pressuposto que essa equipa de segurança irá fornecer referências secretas (URIs e os thumbprints) e chave de Olá tooreference de necessidade de equipa que os programadores/operadores nas respetivas aplicações. Por conseguinte, não precisam de toogrant programadores/operadores qualquer acesso plane de dados. Note também que este exemplo se foca em proteger o seu cofre de chaves. Deve ser dada atenção semelhante toosecure [as suas VMs](https://azure.microsoft.com/services/virtual-machines/security/), [contas do storage](../storage/common/storage-security-guide.md) e outros recursos do Azure demasiado.

> [!NOTE]
> Nota: este exemplo mostra como o acesso do cofre de chaves estará bloqueado na produção. os programadores de Olá devem ter os seus próprios subscrição ou resourcegroup em que disponham de permissões totais toomanage os seus cofres, VMs e conta de armazenamento onde desenvolvem aplicação Olá.
> 
> 

## <a name="resources"></a>Recursos
* [Controlo de Acesso Baseado em Funções do Azure Active Directory](../active-directory/role-based-access-control-configure.md)
  
  Este artigo explica Olá controlo de acesso baseado em função do Active Directory do Azure e como funciona.
* [RBAC: Funções Incorporadas](../active-directory/role-based-access-built-in-roles.md)
  
  Olá, detalhes deste artigo todas as funções incorporadas disponíveis no RBAC.
* [Compreender a implementação do Resource Manager e a implementação clássica](../azure-resource-manager/resource-manager-deployment-model.md)
  
  Este artigo explica a implementação do Resource Manager Olá e modelos de implementação clássica e explica as vantagens de Olá da utilização de grupos de recursos e do Resource Manager Olá
* [Gerir o Controlo de Acesso Baseado em Funções com o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  Este artigo explica como o controlo com o Azure PowerShell de acesso de toomanage baseada em funções
* [Gestão do controlo de acesso baseado em funções com Olá REST API](../active-directory/role-based-access-control-manage-access-rest.md)
  
  Este artigo mostra como toouse Olá REST API toomanage RBAC.
* [Controlo de Acesso Baseado em Funções para o Microsoft Azure no Ignite](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  Este é um tooa ligação vídeo no Channel 9 de conferências de Ignite Olá MS versão 2015. Nesta sessão falar sobre aceder a gestão e capacidades de relatórios no Azure e explorar as melhores práticas em torno de proteger o acesso subscrições tooAzure utilizando o Azure Active Directory.
* [Autorizar o acesso tooweb aplicações utilizando OAuth 2.0 e o Azure Active Directory](../active-directory/active-directory-protocols-oauth-code.md)
  
  Este artigo descreve o fluxo completo de OAuth 2.0 para autenticar com o Azure Active Directory.
* [APIs REST de Gestão do cofre de chaves](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  Este documento é uma referência de Olá para Olá REST APIs toomanage a chave de cofre através de programação, incluindo a definição de política de acesso do Cofre de chaves.
* [APIs REST do cofre de chaves](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  Cofre do tookey de ligação documentação de referência da REST API.
* [Controlo de acesso a chaves](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  Documentação de referência de controlo de acesso de tooSecret uma ligação.
* [Controlo de acesso a segredos](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  Documentação de referência de controlo de acesso de tooKey uma ligação.
* [Definir](https://msdn.microsoft.com/library/mt603625.aspx) e [Remover](https://msdn.microsoft.com/library/mt619427.aspx) a política de acesso do cofre de chaves com o PowerShell
  
  Documentação de tooreference de ligações de política de acesso do PowerShell cmdlets toomanage Cofre de chaves.

## <a name="next-steps"></a>Passos Seguintes
Para obter um tutorial introdutório para administradores, veja [Introdução ao Cofre de Chaves do Azure](key-vault-get-started.md).

Para obter mais informações sobre o registo de utilização do cofre de chave, veja [Registo do Cofre de Chaves do Azure](key-vault-logging.md).

Para obter mais informações sobre a utilização de chaves e segredos com o cofre de chave do Azure, veja [About Keys and Secrets (Sobre Chaves e Segredos)](https://msdn.microsoft.com/library/azure/dn903623.aspx).

Se tiver dúvidas sobre o Cofre de chaves, visite Olá [Cofre de chaves do Azure fóruns](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

