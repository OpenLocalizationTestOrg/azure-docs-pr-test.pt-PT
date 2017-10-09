---
title: "operações de Active Directory Connect Health aaaAzure"
description: "Este artigo descreve as operações adicionais que podem ser efetuadas depois de ter implementado o Azure AD Connect Health."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Operações do Azure Active Directory Connect Health
Este tópico descreve Olá várias operações pode efetuar ao utilizar o Azure Active Directory (Azure AD) Connect Health.

## <a name="enable-email-notifications"></a>Ativar notificações por e-mail
Pode configurar notificações de correio eletrónico de toosend de serviço do Azure AD Connect Health Olá quando alertas indicam que a sua infraestrutura de identidade não está em bom estada. Isto ocorre quando é gerado um alerta e, quando está resolvido.

![Definições de notificação de correio eletrónico do captura de ecrã do Azure AD Connect Health](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> Notificações por e-mail estão ativadas por predefinição.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>notificações de correio eletrónico tooenable do Azure AD Connect Health
1. Abra Olá **alertas** painel para o serviço de Olá para o qual pretende tooreceive notificação de correio eletrónico.
2. A partir da barra de ação de Olá, clique em **as definições de notificação**.
3. No comutador de notificação de correio eletrónico Olá, selecione **ON**.
4. Selecione a caixa de verificação de Olá se pretender que todos os administradores globais tooreceive as notificações de e-mail.
5. Se pretender que as notificações de e-mail tooreceive em outros endereços de correio eletrónico, especifique-os no Olá **destinatários de E-Mail adicionais** caixa. tooremove um endereço de correio eletrónico nesta lista, faça duplo clique entrada Olá e selecione **eliminar**.
6. as alterações de Olá toofinalize, clique em **guardar**. As alterações entram em vigor apenas depois de guardar.

## <a name="delete-a-server-or-service-instance"></a>Eliminar uma instância de servidor ou serviço

Em alguns casos, pode querer tooremove um servidor que está a ser monitorizado. Eis o que precisa de tooknow tooremove um servidor a partir do serviço do Olá do Azure AD Connect Health.

Quando estiver a eliminar um servidor, tenha em atenção seguinte Olá:

* Esta ação para recolher quaisquer novos dados a partir desse servidor. Este servidor é removido do serviço de monitorização de Olá. Após esta ação não é capaz de tooview novos alertas, monitorizar ou dados de análise de utilização para este servidor.
* Esta ação não desinstala Olá agente de estado de funcionamento do seu servidor. Se não o desinstalou Olá agente de estado de funcionamento antes de executar este passo, poderá ver erros relacionados toohello agente de estado de funcionamento no servidor de Olá.
* Esta ação não elimina dados de Olá já recolhidos a partir deste servidor. Os dados serem eliminados de acordo com Olá política de retenção de dados do Azure.
* Depois de efetuar esta ação, se pretender que a monitorização de toostart Olá mesmo servidor novamente, tem de desinstalar e reinstalar o agente de estado de funcionamento de Olá neste servidor.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete um servidor a partir do serviço do Olá do Azure AD Connect Health
Azure AD Connect Health para serviços de Federação do Active Directory (AD FS) e do Azure AD Connect (sincronização):

1. Abra Olá **servidor** painel do Olá **lista de servidores** painel selecionando toobe de nome de servidor Olá removido.
2. No Olá **servidor** painel, a partir da barra de ação de Olá, clique em **eliminar**.
3. O confirme, escrevendo o nome do servidor Olá na caixa de confirmação de Olá.
4. Clique em **Eliminar**.

Azure AD Connect Health para os serviços de domínio do Azure Active Directory:

1. Abra Olá **controladores de domínio** dashboard.
2. Selecione Olá toobe de controlador de domínio removido.
3. A partir da barra de ação de Olá, clique em **eliminar selecionado**.
4. Confirme o servidor de Olá Olá ação toodelete.
5. Clique em **Eliminar**.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Eliminar uma instância de serviço do serviço do Azure AD Connect Health
Em alguns casos, pode querer tooremove uma instância de serviço. Segue-se de que precisa de tooknow tooremove um serviço de instância do serviço do Olá do Azure AD Connect Health.

Quando estiver a eliminar uma instância de serviço, lembre-se de que seguinte Olá:

* Esta ação remove instância de serviço atual Olá Olá serviço de monitorização.
* Esta ação não desinstalar ou remover Olá agente de estado de funcionamento de qualquer um dos servidores de Olá que foram monitorizados como parte desta instância de serviço. Se não o desinstalou Olá agente de estado de funcionamento antes de executar este passo, poderá ver erros relacionados toohello estado de funcionamento do agente em servidores de Olá.
* Todos os dados desta instância de serviço são eliminados de acordo com Olá política de retenção de dados do Azure.
* Depois de efetuar esta ação, se quiser toostart Olá serviço de monitorização, desinstalar e reinstalar o agente de estado de funcionamento de Olá em todos os servidores de Olá. Depois de efetuar esta ação, se quiser toostart monitorização Olá mesmo servidor novamente, desinstalar, reinstalar e registar Olá agente de estado de funcionamento nesse servidor.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete uma instância de serviço do serviço do Olá do Azure AD Connect Health
1. Abra Olá **serviço** painel do Olá **lista serviço** painel selecionando o identificador do serviço Olá (nome do farm) que pretende que o tooremove.
2. No Olá **servidor** painel, a partir da barra de ação de Olá, clique em **eliminar**.
3. Confirmar, escrevendo o nome do serviço Olá na caixa de confirmação de Olá (por exemplo: sts.contoso.com).
4. Clique em **Eliminar**.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Gerir o acesso com controlo de acesso baseado em funções
[Controlo de acesso baseado em funções (RBAC)](../role-based-access-control-configure.md) para o Azure AD Connect Health fornece acesso toousers e grupos que não sejam administradores globais. RBAC atribui funções toohello pretendido utilizadores e grupos e fornece um mecanismo toolimit Olá os administradores globais no seu diretório.

### <a name="roles"></a>Funções
O Azure AD Connect Health suporta Olá funções incorporadas os seguintes:

| Função | Permissões |
| --- | --- |
| Proprietário |Os proprietários podem *gerir o acesso* (por exemplo, atribua um utilizador de tooa de função ou grupo), *ver todas as informações* (por exemplo, ver alertas) no portal de Olá, e *alterar definições* ( Por exemplo, notificações por correio eletrónico) no Azure AD Connect Health. <br>Por predefinição, os administradores globais do Azure AD são atribuídos esta função e não pode ser alterado. |
| Contribuinte |Os contribuintes podem *ver todas as informações* (por exemplo, ver alertas) no portal de Olá, e *alterar definições* (por exemplo, notificações por correio eletrónico) no Azure AD Connect Health. |
| Leitor |Os leitores podem *ver todas as informações* (por exemplo, ver alertas) do portal de Olá no Azure AD Connect Health. |

Todas as outras funções (por exemplo, os administradores de acesso de utilizador ou utilizadores do DevTest Labs) não tem tooaccess nenhum impacto no Azure AD Connect Health, mesmo que funções Olá estão disponíveis na experiência Olá do portal.

### <a name="access-scope"></a>Âmbito de acesso
O Azure AD Connect Health suporta acesso de gestão em dois níveis:

* **Todas as instâncias de serviço**: Este é Olá recomendado caminho na maioria dos casos. Controla o acesso para todas as instâncias de serviço (por exemplo, um farm do AD FS) em todos os tipos de função que estão a ser monitorizados pelo Azure AD Connect Health.
* **Instância de serviço**: em alguns casos, poderá ser necessário acesso toosegregate com base nos tipos de função ou por uma instância de serviço. Neste caso, pode gerir o acesso ao nível de instância de serviço Olá.  

Permissão é concedida se um utilizador final tem acesso no diretório Olá ou o serviço de nível de instância.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>Permitir que os utilizadores ou grupos de acesso tooAzure AD Connect Health
Olá passos seguintes mostram como tooallow aceder.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>Passo 1: Selecione o âmbito de acesso adequados Olá
tooallow um acesso de utilizador em Olá *todas as instâncias de serviço* nível no Azure AD Connect Health, painel principal do Olá aberta no Azure AD Connect Health.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>Passo 2: Adicionar utilizadores e grupos e atribuir funções
1. De Olá **configurar** secção, clique em **utilizadores**.<br>
   ![Painel, da principal de ligar RBAC de estado de funcionamento de captura de ecrã do Azure AD com utilizadores realçado](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. Selecione **Adicionar**.
3. No Olá **selecionar uma função** painel, selecione uma função (por exemplo, **proprietário**).<br>
   ![Janela de ligar os utilizadores RBAC de estado de funcionamento de captura de ecrã do Azure AD](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Escreva o nome de Olá ou o identificador de Olá direcionado utilizador ou grupo. Pode selecionar um ou mais utilizadores ou grupos Olá mesmo tempo. Clique em **Selecionar**.
   ![Janela de ligar os utilizadores RBAC de estado de funcionamento de captura de ecrã do Azure AD](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. Selecione **OK**.<br>
6. Depois de concluída a atribuição de função Olá, Olá utilizadores e grupos que aparecem na lista de Olá.<br>
   ![Janela de ligar utilizadores RBAC do Estado de funcionamento de captura de ecrã do Azure AD, com os novos utilizadores realçado](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Agora Olá listadas utilizadores e grupos que têm acesso, de acordo com tootheir atribuição de funções.

> [!NOTE]
> * Os administradores globais sempre dispor de operações do acesso total tooall Olá, mas não estão presentes na Olá anterior a lista de contas de administrador global.
> * funcionalidade de convidar utilizadores Olá não é suportada no Azure AD Connect Health.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>Passo 3: Partilhar a localização do painel de Olá com utilizadores ou grupos
1. Depois de atribuir permissões, um utilizador pode aceder do Azure AD Connect Health acedendo [aqui](http://aka.ms/aadconnecthealth).
2. No painel de Olá, utilizador de Olá pode afixar painel Olá ou diferentes partes do mesmo toohello dashboard. Basta clicar Olá **Pin toodashboard** ícone.<br>
   ![Captura de ecrã do Azure AD Connect RBAC de estado de funcionamento afixar painel, com o ícone de pino realçado](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Um utilizador com função de leitor de Olá atribuído não é a extensão do Azure AD Connect Health tooget capaz de Olá Azure Marketplace. utilizador Olá não é possível executar, por isso, Olá necessário toodo operação "Criar". utilizador Olá ainda pode obter toohello painel toohello vai anterior a ligação. Para utilização subsequente, o utilizador Olá pode afixar dashboard de toohello Olá painel.
>
>

### <a name="remove-users-or-groups"></a>Remover utilizadores ou grupos
Pode remover um utilizador ou um grupo adicionada tooAzure AD Connect RBAC de estado de funcionamento. Basta com o botão direito Olá utilizador ou grupo e selecione **remover**.<br>
![Janela de ligar os utilizadores RBAC de estado de funcionamento de captura de ecrã do Azure AD, com remover realçado](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Passos seguintes
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalação do Agente do Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Utilizar o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md)
* [Utilizar o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
* [Utilizar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md)
* [FAQ do Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Histórico de versões do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
