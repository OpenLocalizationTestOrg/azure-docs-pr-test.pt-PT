---
title: "Serviços de domínio do Azure Active Directory: Introdução | Microsoft Docs"
description: "Ativar o Azure Active Directory Domain Services utilizando Olá portal do Azure (pré-visualização)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Ativar o Azure Active Directory Domain Services utilizando Olá portal do Azure (pré-visualização)


## <a name="task-3-configure-administrative-group"></a>Tarefa 3: configurar o grupo administrativo
Nesta tarefa de configuração, crie um grupo administrativo no diretório do Azure AD. Este grupo administrativo especial denomina *AAD DC administradores*. Os membros deste grupo recebem permissões administrativas nas máquinas que estão associados a um domínio toohello de domínio gerido. Em computadores associados a um domínio, este grupo é adicionado toohello grupo de administradores. Além disso, os membros deste grupo podem utilizar o ambiente de trabalho remoto tooconnect remotamente toodomain computadores associados a um.

> [!NOTE]
> Não dispõe de permissões de administrador do domínio ou de administrador de empresa Olá domínio gerido que criou utilizando o Azure Active Directory Domain Services. Nos domínios geridos, estas permissões são reservadas pelo serviço de Olá em não ficam disponíveis toousers no inquilino Olá. No entanto, pode utilizar o Olá de grupo administrativo especial criada neste tooperform de tarefas de configuração privilegiado algumas operações. Estas operações incluem a associação a domínio toohello de computadores, que pertence o grupo de administração de toohello em computadores associados a um domínio e a configuração de política de grupo.
>

Assistente de Olá cria automaticamente o grupo administrativo Olá no diretório do Azure AD. Este grupo é chamado 'AAD DC administradores'. Se tiver um grupo existente com este nome no diretório do Azure AD, o Assistente de Olá seleciona deste grupo. Pode configurar a associação ao grupo utilizando Olá **grupo Administrador** página do assistente.

1. associação ao grupo de tooconfigure, clique em **AAD DC administradores**.

    ![Configurar a associação de grupo](./media/getting-started/domain-services-blade-admingroup.png)

2. Clique em Olá **adicionar membros** botão tooadd utilizadores do seu grupo de administrador do toohello de diretório do Azure AD.

3. Quando tiver terminado, clique em **OK** toomove no toohello **resumo** página do Assistente de Olá.

4. No Olá **resumo** página do Assistente de Olá, definições de configuração de Olá revisão do domínio Olá de gerido. Pode voltar atrás tooany passo do assistente toomake altera o Olá, se necessário. Quando tiver terminado, clique em **OK** toocreate Olá geridos novo domínio.

    ![Resumo](./media/getting-started/domain-services-blade-summary.png)

5. Verá uma notificação que mostra o progresso de Olá da sua implementação de serviços de domínio do Azure AD. Clique em notificação Olá toosee detalhadas progresso para a implementação de Olá.

    ![Notificação - implementação em curso](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Aprovisionar o seu domínio gerido
processo de Olá de aprovisionamento do seu domínio gerido pode demorar até tooan hora.

1. Enquanto a implementação está em curso, pode procurar 'Serviços de domínio' Olá **procurar recursos** caixa de pesquisa. Selecione **serviços de domínio do Azure AD** do resultado de pesquisa de Olá. Olá **serviços de domínio do Azure AD** painel lista Olá domínio gerido que está a ser aprovisionado.

    ![Localizar o domínio gerido que está a ser aprovisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Clique no nome de Olá de Olá gerido (por exemplo, ' contoso100.com') do domínio toosee mais detalhes sobre o domínio de Olá.

    ![Serviços de domínio - estado de aprovisionamento](./media/getting-started/domain-services-provisioning-state.png)

3. Olá **descrição geral** separador mostra esse domínio Olá está atualmente a ser aprovisionado. Não é possível configurar o domínio Olá de gerido até que esteja totalmente aprovisionado. Esta operação pode demorar tooan hora para a sua toobe domínio gerido totalmente aprovisionado.

    ![Serviços de domínio - separador de descrição geral durante Olá estado de aprovisionamento ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Quando o domínio gerido Olá esteja totalmente aprovisionado, Olá **descrição geral** separador mostra o estado de domínio de Olá como **executar**.

    ![Serviços de domínio - separador Descrição geral depois de totalmente aprovisionado](./media/getting-started/domain-services-provisioned.png)

5. No Olá **propriedades** separador, verá dois endereços IP no qual o domínio estão disponíveis para a rede virtual Olá controladores.

    ![Serviços de domínio - separador de propriedades depois totalmente aprovisionado](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Passo seguinte
[Tarefa 4: atualizar as definições de DNS de Olá de Olá rede virtual do Azure](active-directory-ds-getting-started-dns.md)
