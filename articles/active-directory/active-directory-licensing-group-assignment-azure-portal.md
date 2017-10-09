---
title: "grupo de tooa aaaAssign licenças no Azure Active Directory | Microsoft Docs"
description: "Como tooassign licenças toousers através de licenciamento de grupo do Azure Active Directory"
services: active-directory
keywords: Licenciamento do Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Atribuir licenças toousers através da associação a grupos no Azure Active Directory

Este artigo explica como atribuir tooa grupo do produto licenças de utilizadores no Azure Active Directory (Azure AD) e, em seguida, verificar se está a licenciados corretamente.

Neste exemplo, o inquilino Olá contém um grupo de segurança denominado **departamento de RH**. Este grupo inclui todos os membros do departamento de recursos humanos Olá (cerca de 1000 utilizadores). Pretende que o departamento de todo tooassign do Office 365 Enterprise E3 licenças toohello. Olá serviço Yammer Enterprise que está incluído no produto Olá tem de ser temporariamente desativada até que o departamento de Olá é toostart pronto a ser utilizado. Também deve toodeploy Enterprise Mobility + toohello de licenças de segurança mesmo grupo de utilizadores.

> [!NOTE]
> Alguns serviços da Microsoft não estão disponíveis em todas as localizações. Antes de uma licença pode ser atribuída tooa utilizador, o administrador de Olá tem propriedade de localização de utilização de Olá toospecify utilizador Olá.

> Para atribuição de licença de grupo, os utilizadores sem uma localização de utilização especificada herdem localização Olá do diretório de Olá. Se tiver utilizadores em vários locais, recomendamos que sempre definir localização de utilização como parte do seu fluxo de criação de utilizador no Azure AD (por exemplo, através do AAD Connect configuração) - irá garantir resultados Olá de atribuição de licença sempre estão correto e os utilizadores não recebem serviços em locais que não são permitidos.

## <a name="step-1-assign-hello-required-licenses"></a>Passo 1: Atribuir licenças de Olá necessário

1. Inicie sessão no toohello [ **portal do Azure** ](https://portal.azure.com) com uma conta de administrador. toomanage licenças, conta de Olá tem de ser um administrador de conta de utilizador ou função de administrador global.

2. Selecione **mais serviços** no Olá painel de navegação esquerdo e, em seguida, selecione **do Azure Active Directory**. Pode adicionar esta tooFavorites painel ou afixá-lo toohello dashboard do portal.

3. No Olá **do Azure Active Directory** painel, selecione **licenças**. Esta ação abre um painel onde pode ver e gerir todos os produtos sujeito a licença no inquilino Olá.

4. Em **todos os produtos**, selecione o Office 365 Enterprise E3 e Enterprise Mobility + Security selecionando os nomes de produtos de Olá. atribuição de Olá toostart, selecione **atribuir** , Olá parte superior do painel de Olá.

   ![Todos os produtos, atribuir licenças](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. No Olá **atribuir licenças** painel, clique em **utilizadores e grupos** tooopen Olá **utilizadores e grupos** painel. Procure o nome do grupo de Olá *departamento de RH*, selecione o grupo de Olá e, em seguida, ser tooconfirm se clicando **selecione** em Olá parte inferior do painel de Olá.

   ![Selecione um grupo](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. No Olá **atribuir licenças** painel, clique em **opções de atribuição (opcionais)**, que apresenta todos os planos de serviço incluídos no Olá dois produtos são selecionados anteriormente. Localizar **Yammer Enterprise** e ativá-la **desativar** toodisable do serviço de licença do produto Olá. Confirmar clicando **OK** na parte inferior de Olá de **opções de atribuição**.

   ![Opções de atribuição](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. atribuição de Olá toocomplete, no Olá **atribuir licenças** painel, clique em **atribuir** em Olá parte inferior do painel de Olá.

8. É apresentada uma notificação no canto superior direito Olá que mostra o estado de Olá e resultado Olá processo. Se não foi possível concluir o grupo de toohello de atribuição de Olá (por exemplo, devido a já existentes licenças no grupo de Olá), clique em detalhes de tooview Olá notificação de falha de Olá.

Especificamos agora um modelo de licença para o grupo do departamento de RH Olá. Um processo em segundo plano no Azure AD foi iniciado tooprocess todos os membros desse grupo existentes. Esta operação inicial pode demorar algum tempo, dependendo do tamanho atual do Olá do grupo de Olá. No próximo passo Olá, vamos descrever como tooverify esse processo Olá terminou e determinar se atenção adicional é necessário tooresolve problemas.

> [!NOTE]
> Pode iniciar Olá mesma atribuição de uma localização alternativa: **utilizadores e grupos** no Azure AD. Aceda demasiado**do Azure Active Directory** > **utilizadores e grupos** > **todos os grupos**. Em seguida, localize o grupo de Olá, selecione-a e aceda toohello **licenças** Olá separador **atribuir** botão por cima do painel de Olá abre o painel de atribuição de licença de Olá.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>Passo 2: Verificar se a atribuição de Olá inicial foi concluída

1. Aceda demasiado**do Azure Active Directory** > **utilizadores e grupos** > **todos os grupos**. Em seguida, localize Olá **departamento de RH** grupo de licenças atribuídas a.

2. No Olá **departamento de RH** painel do grupo, selecione **licenças**. Isto permite-lhe confirmar rapidamente se licenças tem sido totalmente atribuídas toousers e se existem quaisquer erros que precisa de toolook em. está disponível Olá seguintes informações:

   - Lista de licenças de produtos que estão atualmente atribuídas toohello grupo. Selecione uma entrada tooshow Olá serviços específicos que foram ativadas e toomake é alterado.

   - Estado da Olá mais recentes licença as alterações efetuadas grupo toohello (se estão a ser processadas alterações Olá ou se o processamento foi concluída para todos os membros de utilizador).

   - Informações sobre os utilizadores que estão num Estado de erro porque não foi possível atribuir licenças toothem.

   ![Opções de atribuição](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Ver informações mais detalhadas sobre a licença de processamento em **do Azure Active Directory** > **utilizadores e grupos** > *nome do grupo*  >  **Registos de auditoria**. Tenha em atenção Olá seguintes atividades:

   - Atividade: **iniciar aplicar toousers de licença de grupo com base**. Isto é registado quando o sistema de Olá escolherá Olá alteração de atribuição de licenças no grupo de Olá e inicia aplicá-la tooall membros de utilizador. Contém informações sobre a alteração de Olá que foi efetuada.

   - Atividade: **concluir aplicar toousers de licença de grupo com base**. Isto é registado quando o sistema de Olá concluir o processamento de todos os utilizadores no grupo de Olá. Contém um resumo de quantos utilizadores foram processados com êxito e o número de utilizadores que não foi possível atribuir licenças do grupo.

   [Leia esta secção](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn mais informações sobre como os registos de auditoria podem ser utilizado tooanalyze alterações por baseado no grupo de licenciamento.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Passo 3: Verificar problemas de licença e resolvê-los

1. Aceda demasiado**do Azure Active Directory** > **utilizadores e grupos** > **todos os grupos**e determinar Olá **departamento de RH**grupo de licenças atribuídas a.
2. No Olá **departamento de RH** painel do grupo, selecione **licenças**. notificação de Olá por cima do painel de Olá mostra que existem 10 utilizadores que não foi possível atribuir licenças. Clicar nela abre-se de uma lista de todos os utilizadores num Estado de erro de licenciamento para este grupo.
3. Olá **falha atribuições** coluna indica-nos que ambas as licenças de produto não foi possível atribuir utilizadores toohello. Olá **principais motivo da falha** coluna contém causa Olá falha Olá. Neste caso, tem **planos de serviços em conflito**.

   ![Atribuições de falha](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Selecione um Olá de tooopen utilizador **licenças** painel. Este painel mostra todas as licenças que estão atualmente atribuídas toohello utilizador. Neste exemplo, o utilizador de Olá tem licenças de Olá Office 365 Enterprise E1 que foi herdada de Olá **utilizadores de local público** grupo. Em conflito com a licença de Olá E3 Olá sistema tentou tooapply de Olá **departamento de RH** grupo. Como resultado, nenhum dos licenças Olá desse grupo foi atribuído toohello utilizador.

   ![Licenças de vista de um utilizador](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve este conflito, remover utilizador Olá Olá **utilizadores de local público** grupo. Depois do Azure AD processa alteração Olá, Olá **departamento de RH** corretamente são atribuídas as licenças.

   ![Licença atribuída corretamente](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre a funcionalidade de Olá definidas para a gestão de licenças através de grupos, consulte Olá seguintes artigos:

* [O que é o licenciamento no Azure Active Directory com base no grupo?](active-directory-licensing-whatis-azure-portal.md)
* [Identificar e resolver problemas de licenciamento para um grupo no Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Como toomigrate indivíduo licenciado a utilizadores baseados em toogroup licenciamento no Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory baseadas em grupos licenciamento cenários adicionais](active-directory-licensing-group-advanced.md)
