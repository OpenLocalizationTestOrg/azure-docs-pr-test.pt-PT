---
title: "Azure Active Directory dos serviços de domínio: Administrar um domínio gerido | Microsoft Docs"
description: "Administrar o Azure Active Directory Domain Services de domínios geridos"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Administrar um domínio gerido pelos Serviços de Domínio do Azure Active Directory
Este artigo mostra como tooadminister um serviços de domínio do Azure Active Directory (AD) geridos por domínio.

## <a name="before-you-begin"></a>Antes de começar
tarefas de Olá tooperform apresentadas neste artigo, tem de:

1. Um **subscrição do Azure**.
2. Um **diretório do Azure AD** -está sincronizada com um diretório no local ou um diretório apenas na nuvem.
3. **Serviços de domínio do Azure AD** tem de estar ativada para o diretório de Olá do Azure AD. Se ainda não o feito, siga todas as tarefas de Olá descritas em Olá [guia de introdução](active-directory-ds-getting-started.md).
4. A **máquinas de virtuais associados a um domínio** do qual administrar Olá domínio gerido dos serviços de domínio do Azure AD. Se não tiver uma máquina de virtual, siga todas as tarefas de Olá descritas no artigo Olá intitulado [aderir a um domínio gerido do Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Precisa de credenciais de Olá de um **conta pertencentes toohello 'AAD DC administradores' grupo de utilizadores do** no seu diretório, tooadminister seu domínio gerido.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Tarefas administrativas que pode efetuar um domínio gerido
Membros Olá ' AAD DC' do grupo de administradores são concedidos privilégios no domínio gerido Olá ativá-los tooperform tarefas, tais como:

* Associe máquinas toohello gerido domínio.
* Configure Olá GPO incorporadas para contentores de 'AADDC computadores' e 'AADDC utilizadores' Olá no domínio gerido Olá.
* Administrar o DNS no domínio Olá de gerido.
* Criar e administrar personalizado unidades organizacionais (UOs) no domínio Olá de gerido.
* Obter acesso administrativo toocomputers associados a um domínio gerido toohello.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>Privilégios administrativos não dispõe de um domínio gerido
domínio Olá é gerido pela Microsoft, incluindo atividades tais como a aplicação de patches, monitorização e, efetua cópias de segurança. Por conseguinte, o domínio de Olá está bloqueado para baixo e não dispõe de privilégios tooperform determinadas tarefas administrativas no domínio Olá. Alguns exemplos de tarefas que não é possível efetuar são abaixo.

* Não são concedidos privilégios de administrador do domínio ou de administrador de empresa para o domínio Olá de gerido.
* Não é possível expandir o esquema Olá de domínio geridos Olá.
* Não é possível ligar toodomain controladores para Olá domínio gerido utilizando o ambiente de trabalho remoto.
* Não é possível adicionar domínio toohello de controladores domínio gerido.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Tarefa 1 - aprovisionar um tooremotely de máquina virtual associado a um domínio do Windows Server administrar domínio Olá de gerido
Domínios geridos de serviços de domínio do AD do Azure podem ser geridos através do Active Directory administrativas ferramentas familiares como Olá Active Directory Centro de administração (ADAC) ou do AD do PowerShell. Os administradores inquilinos não dispõe de controladores de toodomain privilégios tooconnect Olá domínio gerido através do ambiente de trabalho remoto. Por conseguinte, os membros Olá grupo 'AAD DC administradores' pode administrar remotamente utilizando ferramentas administrativas do AD de um computador de servidor/cliente do Windows que é toohello associados a um domínio de gerido de domínios geridos. Ferramentas de administração do AD podem ser instaladas como parte da funcionalidade opcional do Olá ferramentas de administração remota de servidor (FARS) em máquinas de cliente e servidor Windows associados a um domínio toohello gerido.

Step-by-Olá primeiro passo é tooset de uma máquina virtual do Windows Server que está associado a um toohello gerido domínio. Para obter instruções, consulte o artigo toohello intitulado [aderir a um servidor Windows máquina virtual tooan serviços de domínio do Azure AD gerido domínio](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Administrar remotamente domínio Olá de gerido a partir de um computador cliente (por exemplo, o Windows 10)
Utilize este artigo um Olá de tooadminister de máquina virtual do Windows Server AAD DS instruções Olá geridos domínio. No entanto, pode também escolher toouse um toodo de máquina virtual de cliente (por exemplo, o Windows 10) do Windows, por isso.

Pode [instalar ferramentas de administração remota de servidor (FARS)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) na máquina virtual do cliente Windows ao seguir as instruções de Olá no TechNet.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Tarefa 2 - ferramentas de administração do Active Directory de instalação na máquina virtual de Olá
Efetue Olá seguintes ferramentas de administração do Active Directory passos tooinstall Olá na máquina de virtual Olá associado a um domínio. Consulte o Technet para obter mais informações [informações sobre como instalar e utilizar as ferramentas de administração remota do servidor](https://technet.microsoft.com/library/hh831501.aspx).

1. Navegue demasiado**máquinas virtuais** nó Olá portal clássico do Azure. Selecione a máquina virtual de Olá que criou na tarefa 1 e clique em **Connect** na barra de comando Olá em Olá parte inferior da janela de Olá.

    ![Ligar a máquina virtual de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portal clássico Olá pede-lhe tooopen ou guardar um ficheiro com uma extensão '. rdp', que é utilizado tooconnect toohello máquina. Clique em ficheiro de Olá tooopen quando foi concluída a transferência.
3. Na linha de comandos de início de sessão Olá, utilize Olá as credenciais de utilizadores que pertençam a grupo do toohello 'AAD DC administradores'. Por exemplo, utilizamos 'bob@domainservicespreview.onmicrosoft.com' no nosso caso.
4. A partir do ecrã de início de Olá, abra **Gestor de servidor**. Clique em **para adicionar funções e funcionalidades** no painel central do Olá da janela do Gestor de servidor Olá.

    ![Inicie o Gestor de servidor numa máquina virtual](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. No Olá **antes de começar** página do Olá **Assistente Adicionar funções e funcionalidades**, clique em **seguinte**.

    ![Antes de começar a página](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. No Olá **tipo de instalação** página, deixe Olá **instalação baseada em funções ou baseada em funcionalidade** opção selecionada e clique em **seguinte**.

    ![Página tipo de instalação](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. No Olá **seleção de servidor** página, selecione a máquina virtual atual do Olá Olá agrupamento de servidores e clique em **seguinte**.

    ![Página de seleção de servidor](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. No Olá **funções de servidor** página, clique em **seguinte**. Vamos ignorar esta página, uma vez que vamos não estiver a instalar quaisquer funções no servidor de Olá.
9. No Olá **funcionalidades** página, clique em tooexpand Olá **ferramentas de administração remota do servidor** nó e, em seguida, clique em tooexpand Olá **ferramentas de administração de funções** nós. Selecione **AD DS e AD LDS ferramentas** funcionalidade a partir da lista de Olá das ferramentas de administração de função.

    ![Página de funcionalidades](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. No Olá **confirmação** página, clique em **instalar** tooinstall Olá AD ferramentas e AD LDS funcionalidade na máquina virtual de Olá. Quando a instalação da funcionalidade for concluída com êxito, clique em **fechar** tooexit Olá **para adicionar funções e funcionalidades** assistente.

    ![Página de confirmação](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Tarefa 3 - Ligar tooand explorar domínio Olá de gerido
Agora que ferramentas administrativas Olá AD estão instaladas no Olá associados a um domínio máquina virtual, pode utilizar estas ferramentas tooexplore e administrar domínio Olá de gerido.

> [!NOTE]
> Precisa de um membro de toobe Olá ' AAD DC' do grupo de administradores, tooadminister Olá geridos domínio.
>
>

1. A partir do ecrã de início de Olá, clique em **ferramentas administrativas**. Deverá ver ferramentas administrativas Olá AD instaladas na máquina virtual de Olá.

    ![Ferramentas administrativas instaladas no servidor](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Clique em **Centro de administração do Active Directory**.

    ![Centro de administração do Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. domínio de Olá tooexplore, clique no nome de domínio Olá no painel esquerdo do Olá (por exemplo, ' contoso100.com'). Tenha em atenção dois contentores chamados 'AADDC computadores' e 'AADDC utilizadores' respetivamente.

    ![ADAC - domínio de vista](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Clique em contentor Olá denominado **AADDC utilizadores** toosee todos os utilizadores e grupos que pertençam toohello geridos domínio. Deverá ver as contas de utilizador e grupos do seu Azure AD inquilino Mostrar cópias de segurança neste contentor. Observe que, neste exemplo, uma conta de utilizador para o utilizador de Olá chamado 'Bernardo' e um grupo chamado 'AAD DC administradores' estão disponíveis neste contentor.

    ![ADAC - utilizadores de domínio](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Clique em contentor Olá denominado **AADDC computadores** computadores de Olá toosee associados a um domínio gerido toothis. Deverá ver uma entrada para a máquina de virtual actual Olá, que é toohello associado ao domínio. Contas de computador para todos os computadores que estejam associados toohello domínio gerido são armazenados neste contentor "AADDC computadores" de serviços de domínio do Azure AD.

    ![ADAC - computadores associados ao domínio](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de domínio do Azure AD - guia de introdução](active-directory-ds-getting-started.md)
* [Aderir a um servidor Windows máquina virtual tooan serviços de domínio do Azure AD gerido domínio](active-directory-ds-admin-guide-join-windows-vm.md)
* [Implementar ferramentas de administração do servidor remoto](https://technet.microsoft.com/library/hh831501.aspx)
