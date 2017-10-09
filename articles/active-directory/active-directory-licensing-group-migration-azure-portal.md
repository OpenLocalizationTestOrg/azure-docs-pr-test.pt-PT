---
title: toomigrate aaaHow tooa os utilizadores licenciados individuais de grupo no Azure Active Directory | Microsoft Docs
description: "Como tooswitch de utilizador individuais licenças toogroup baseado licenciamento com o Azure Active Directory"
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Como tooadd licenciado grupo tooa de utilizadores para licenciamento no Azure Active Directory

Poderá ter existente toousers de licenças implementadas em organizações de Olá através de "atribuição direta"; ou seja, utilizando scripts do PowerShell ou outras licenças de utilizador individuais de tooassign de ferramentas. Se quiser toostart com licenças de toomanage licenciamento baseadas em grupos na sua organização, terá de uma migração plano tooseamlessly substitua as soluções existentes de baseadas em grupos de licenciamento.

Olá mais importante coisa tookeep em consideração é que deve evitar uma situação em que a migração baseada em toogroup licenciamento resultará na utilizadores perder temporariamente cujas licenças são atualmente atribuídas. Qualquer processo que pode resultar na remoção das licenças deve ser evitadas risco de Olá tooremove de perder acesso tooservices e os respetivos dados de utilizadores.

## <a name="recommended-migration-process"></a>Processo de migração recomendada

1. Tem de automatização existente (por exemplo, o PowerShell), gestão de atribuição de licenças e remoção de utilizadores. Deixe a funcionar conforme está.

2. Criar um novo grupo de licenciamento (ou decidir qual existente grupos toouse) e certifique-se de que todas as necessárias para os utilizadores são adicionados como membros.

3. Atribuir licenças de Olá necessário toothose grupos; o seu objetivo deverá ser tooreflect Olá mesmo Estado de licenciamento a automatização existente (por exemplo, o PowerShell) estiver a aplicar toothose utilizadores.

4. Certifique-se de que as licenças tem sido aplicados tooall os utilizadores esses grupos. Isto pode ser feito ao verificar o estado de processamento de Olá em cada grupo e verificando os registos de auditoria.

  - Pode utilizadores individuais lugar para cima verificação observando os detalhes de licença. Verá que tenham Olá mesmo licenças atribuídas "diretamente" e "herdada" dos grupos.

  - Pode executar um script do PowerShell demasiado[verificar como licenças são atribuídas toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - Quando hello mesmo licença do produto é atribuída toohello utilizador diretamente e através de um grupo, apenas uma licença é consumida pelo utilizador Olá. Por conseguinte, não há licenças adicionais são migração tooperform necessário.

5. Certifique-se de que não as atribuições de licenças falharam ao verificar a cada grupo de utilizadores num Estado de erro. Para obter mais informações, consulte [Identifying e resolver problemas de licenciamento para um grupo](active-directory-licensing-group-problem-resolution-azure-portal.md).

6. Considere remover atribuições direta original Olá; poderá ser útil toodo gradualmente, na "waves" toomonitor Olá primeiro resultado num subconjunto de utilizadores.

  Pode deixar Olá originais atribuições diretas nos utilizadores, mas quando os utilizadores de Olá deixam os respetivos grupos licenciados ainda manterão licença original Olá, que é possivelmente não pretende que pretende.

## <a name="an-example"></a>Um exemplo

Temos uma organização com 1000 utilizadores. Todos os utilizadores necessitam de Enterprise Mobility + licenças de segurança (EMS). 200 utilizadores são no Olá departamento financeiro e necessitam de licenças do Office 365 Enterprise E3. Temos um script do PowerShell no local adição e remoção de licenças de utilizadores, visto que vêm e aceda a executar. Queremos que o script de Olá tooreplace baseado no grupo de licenciamento para que licenças são geridas automaticamente pelo Azure AD.

Eis o processo de migração de Olá foi aspeto, como:

1. Utilizar Olá atribuir portal do Azure Olá EMS licença toohello **todos os utilizadores** grupo no Azure AD. Atribuir Olá E3 licença toohello **departamento financeiro** grupo que contém todos os utilizadores de Olá necessário.

2. Para cada grupo, confirme que a atribuição de licenças foi concluída para todos os utilizadores. Painel toohello aceda para cada grupo, selecione **licenças**e verifique o estado de processamento de Olá, Olá parte superior do Olá **licenças** painel.

  - Procure para "alterações mais recentes de licença tem sido aplicados tooall utilizadores" tooconfirm processamento foi concluída.

  - Procure uma notificação na parte superior sobre todos os utilizadores para quem licenças podem ter não foi atribuídas com êxito. Executamos fora de licenças para alguns utilizadores? Alguns utilizadores dispõem de SKUs impedi-los de herança licenças do grupo de licenças em conflito?

3. Lugar para cima verifique tooverify alguns utilizadores que têm Olá direta e licenças de grupo aplicadas. Painel toohello aceda para um utilizador, selecione **licenças**e examine o estado de Olá de licenças.

  - Este é o estado do utilizador Olá esperado durante a migração:

      ![Estado do utilizador esperado](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  Isto confirma que o utilizador Olá tiver licenças diretas e herdadas. Vemos que ambos **EMS** e **E3** são atribuídos.

  - Selecione cada licença tooshow detalhes serviços Olá ativada. Isto pode ser utilizado toocheck se Olá direta e ativação de licenças de grupo Olá exatamente o mesmo planos de serviço para utilizador Olá.

      ![Verifique os planos de serviço](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. Depois de confirmar que são equivalentes diretas e o grupo de licenças, pode começar a remover diretas licenças de utilizadores. Pode testar isto, removendo-os para utilizadores individuais no portal de Olá e, em seguida, executar toohave de scripts de automatização-los removidos em massa. Eis um exemplo de Olá mesmo utilizador com licenças direta Olá removido através do portal Olá. Tenha em atenção que o estado da licença Olá permanece inalterado, mas já não vemos atribuições diretas.

  ![licenças diretas removidas](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre outros cenários para gestão de licenças através de grupos, ler

* [Atribuição de licenças tooa grupo no Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [O que é o licenciamento no Azure Active Directory com base no grupo?](active-directory-licensing-whatis-azure-portal.md)
* [Identificar e resolver problemas de licenciamento para um grupo no Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Azure Active Directory baseadas em grupos licenciamento cenários adicionais](active-directory-licensing-group-advanced.md)
