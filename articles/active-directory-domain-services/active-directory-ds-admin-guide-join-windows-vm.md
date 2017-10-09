---
title: "Azure Active Directory dos serviços de domínio: Aderir a um domínio gerido de tooa de VM do Windows Server | Microsoft Docs"
description: "Associar uma máquina virtual do Windows Server dos serviços de domínio tooAzure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Aderir a um domínio do Windows Server máquina virtual tooa gerido
> [!div class="op_single_selector"]
> * [Portal clássico do Azure – Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell – Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

Este artigo mostra como toojoin um tooan de Windows Server 2012 R2 em execução da máquina virtual dos serviços de domínio do Azure AD geridos domínio, utilizando Olá portal clássico do Azure.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>Passo 1: Criar a máquina de virtual do Windows Server Olá
Siga as instruções de Olá descritas em Olá [criar uma máquina virtual com o Windows hello portal clássico do Azure](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) tutorial. É importante tooensure que esta máquina virtual criada recentemente seja associado toohello mesma rede virtual em que ativou os serviços de domínio do Azure AD. Olá opção 'Criação rápida' não permitem toojoin Olá tooa virtual rede da máquina virtual. Por conseguinte, terá de Olá toouse 'Da galeria' opção toocreate Olá da máquina virtual.

Efetuar Olá os seguintes passos toocreate Windows toohello associados virtual rede da máquina virtual em que tiver ativado os serviços de domínio do Azure AD.

1. No Olá portal clássico do Azure, na barra de comando Olá em Olá parte inferior da janela de Olá, clique em **novo**.
2. Em **computação**, clique em **Máquina Virtual**, em seguida, clique em **da galeria**.
3. ecrã primeiro Olá permite-lhe **escolhe uma imagem** para a máquina virtual da lista de Olá de imagens disponíveis. Escolha a imagem adequada Olá.

    ![Selecione a imagem](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. ecrã segundo Olá permite-lhe escolher um nome de computador, tamanho e nome de utilizador administrativo e palavra-passe. Camada de Olá de utilização e o tamanho necessário toorun sua aplicação ou a carga de trabalho. nome de utilizador de Olá que escolher aqui é um utilizador de administrador local no computador de Olá. Introduza aqui a credenciais de uma conta de utilizador de domínio.

    ![Configurar a máquina virtual](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. ecrã de terceiro Olá permite-lhe configurar recursos de rede, armazenamento e disponibilidade. Certifique-se de selecionar Olá de rede virtual em que ativou os serviços de domínio do Azure AD da Olá **afinidade de região/grupo/Virtual Network** pendente. Especifique um **nome de DNS do serviço de nuvem** conforme adequado para a máquina virtual de Olá.

    ![Selecione a rede virtual para a máquina virtual](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Certifique-se de que associa o toohello de máquina virtual de Olá mesma rede virtual em que tiver ativado os serviços de domínio do Azure AD. Como resultado, máquina virtual de Olá podem 'consulte' domínio Olá e executar tarefas, tais como a associação a domínio Olá. Se escolher toocreate Olá máquina numa rede virtual diferente, ligar a rede virtual toohello rede virtual em que tiver ativado os serviços de domínio do Azure AD.
   >
   >
6. ecrã quarta Olá permite-lhe instalar Olá agente da VM e configurar algumas das extensões disponíveis Olá.

    ![Concluído](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Depois de criar a máquina virtual de Olá, o portal clássico Olá lista Olá nova máquina virtual em Olá **máquinas virtuais** nós. Máquina virtual de Olá e o serviço em nuvem são iniciados automaticamente e o estado está listado como **executar**.

    ![Máquina virtual se encontra em execução](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>Passo 2: Ligar a máquina virtual do Windows Server de toohello utilizando a conta de administrador local Olá
Agora, vamos ligar toohello recém-criado Windows máquina virtual do servidor toojoin-toohello domínio. Utilize as credenciais de administrador local Olá especificado ao criar a máquina virtual de Olá, tooconnect tooit.

Efetue Olá os seguintes passos tooconnect toohello máquina.

1. Navegue demasiado**máquinas virtuais** no portal clássico Olá nó. Selecione a máquina virtual de Olá que criou no passo 1 e clique em **Connect** na barra de comando Olá em Olá parte inferior da janela de Olá.

    ![Ligar a máquina virtual de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portal clássico Olá pede-lhe tooopen ou guardar um ficheiro com uma extensão '. rdp', que é utilizado tooconnect toohello máquina. Clique em ficheiro de Olá tooopen quando foi concluída a transferência.
3. Na linha de comandos de início de sessão Olá, introduza o **credenciais de administrador local**, que especificou durante a criação de máquina virtual de Olá. Por exemplo, tiver utilizámos 'localhost\mahesh' neste exemplo.

Neste momento, deve ter sessão iniciada no toohello recentemente criada a máquina virtual do Windows utilizando credenciais de administrador locais. passo seguinte Olá é o domínio de toohello toojoin Olá máquina virtual.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>Passo 3: Associar o domínio de toohello AAD DS de máquina virtual do Windows Server do Olá gerido
Efetue Olá os seguintes passos toojoin Olá do Windows Server máquina virtual toohello AAD DS domínio gerido.

1. Ligue toohello do Windows Server, conforme mostrado no passo 2. A partir do ecrã de início de Olá, abra **Gestor de servidor**.
2. Clique em **servidor Local** no painel esquerdo do Olá da janela do Gestor de servidor Olá.

    ![Inicie o Gestor de servidor numa máquina virtual](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Clique em **WORKGROUP** em Olá **propriedades** secção. No Olá **propriedades do sistema** página de propriedades, clique em **alteração** domínio de Olá toojoin.

    ![Página de propriedades do sistema](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Especifique o nome de domínio Olá do seu domínio gerido dos serviços de domínio do Azure AD no Olá **domínio** caixa de texto e clique em **OK**.

    ![Especifique Olá domínio toobe associado](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. É tooenter pedido o domínio de Olá toojoin credenciais. Certifique-se de que **especificar Olá as credenciais para um toohello pertencentes de utilizador administradores de DC do AAD** grupo. Apenas os membros deste grupo têm privilégios toojoin máquinas toohello gerido de domínio.

    ![Especifique as credenciais de associação a um domínio](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Pode especificar as credenciais dos Olá seguintes formas:

   * Formato UPN: Especifique o sufixo UPN de Olá Olá conta de utilizador, conforme configurado no Azure AD. Neste exemplo, Olá o sufixo UPN do utilizador Olá 'Bernardo' é 'bob@domainservicespreview.onmicrosoft.com'.
   * Formato de SAMAccountName: pode especificar o nome da conta Olá no formato de SAMAccountName Olá. Neste exemplo, o utilizador de Olá 'João' seria necessário tooenter 'CONTOSO100\bob'.

     > [!NOTE]
     > **Recomendamos que utilize as credenciais do Olá UPN formato toospecify.** Olá SAMAccountName pode ser gerada automaticamente se o prefixo UPN do utilizador é demasiado longo (por exemplo, 'joereallylongnameuser'). Se vários utilizadores tem Olá mesmo prefixo de UPN (por exemplo, "João') no seu inquilino do Azure AD, o respetivo formato SAMAccountName pode ser gerada automaticamente pelo serviço de Olá. Nestes casos, o formato UPN Olá pode ser utilizado fiável toolog no domínio toohello.
     >
     >
7. Depois de associação a um domínio for bem sucedida, verá Olá seguir a mensagem de boas-vindas toohello domínio. Reinicie a máquina virtual de Olá para toocomplete de operação de associação de domínio Olá.

    ![Toohello bem-vindo ao domínio](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Resolução de problemas de associação a um domínio
### <a name="connectivity-issues"></a>Problemas de conectividade
Se a máquina de virtual Olá domínio de Olá toofind não é possível, consulte toohello os seguintes passos de resolução de problemas:

* Certifique-se de que a máquina virtual Olá toohello ligada mesma rede virtual que tiver ativado os serviços de domínio no. Caso contrário, máquina virtual de Olá é tooconnect não é possível toohello domínio e, por conseguinte, é o domínio de Olá toojoin não é possível.
* Se a máquina de virtual Olá tooanother ligados de rede virtual, certifique-se de que esta rede virtual está ligado toohello rede virtual em que tiver ativado os serviços de domínio.
* Repita o domínio de Olá tooping através do nome de domínio Olá do Olá domínio gerido (por exemplo, ' ping contoso100.com'). Se estiver, por isso, não é possível toodo, tente endereços IP Olá tooping para o domínio de Olá apresentada na página olá onde ativou os serviços de domínio do Azure AD (por exemplo, ' ping 10.0.0.4'). Se tiver o endereço IP tooping capaz de Olá, mas não os domínio Olá, DNS pode estar incorretamente configurado. Poderá não tiver configurado os endereços IP Olá do domínio Olá como servidores DNS para a rede virtual Olá.
* Tente libertar Olá cache de resolução DNS na máquina virtual de Olá ('ipconfig /flushdns').

Se obtiver toohello caixa de diálogo que pede-lhe para o domínio de Olá toojoin de credenciais, não tem problemas de conectividade.

### <a name="credentials-related-issues"></a>Problemas relacionados com as credenciais
Consulte toohello se tiver problemas com as credenciais e não é possível toojoin Olá domínio os seguintes passos.

* Tente utilizar as credenciais do Olá UPN formato toospecify. Olá SAMAccountName para a sua conta pode ser gerada automaticamente se existirem vários utilizadores com Olá UPN mesmo prefixo no seu inquilino ou se o prefixo UPN é demasiado longos. Por conseguinte, o formato de SAMAccountName Olá para a sua conta pode ser diferente das que pode espera ou utiliza no seu domínio no local.
* Tente credenciais de Olá toouse de uma conta de utilizador que pertence toohello 'AAD DC administradores' grupo toojoin máquinas toohello domínio gerido.
* Certifique-se de que tem [ativada a sincronização de palavra-passe](active-directory-ds-getting-started-password-sync.md) em conformidade com os passos de Olá descritos no guia de introdução Olá.
* Certifique-se de que usa Olá UPN do utilizador Olá conforme configurado no Azure AD (por exemplo, 'bob@domainservicespreview.onmicrosoft.com') toosign no.
* Certifique-se de que tem aguardaram suficientemente longa para a sincronização de palavra-passe toocomplete conforme especificado no guia de introdução Olá.

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de domínio do Azure AD - guia de introdução](active-directory-ds-getting-started.md)
* [Administrar um domínio gerido dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
