---
title: 'Azure Active Directory Domain Services: Ativar o Azure Active Directory Domain Services | Microsoft Docs'
description: "Ativar o Azure Active Directory Domain Services utilizando Olá portal clássico do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Ativar o Azure Active Directory Domain Services utilizando Olá portal clássico do Azure

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Tarefa 3: ativar o Azure Active Directory Domain Services
Nesta tarefa, ativar do Azure Active Directory Domain Services (Azure AD DS) para o seu diretório efetuando Olá os seguintes passos:

1. Aceda toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No painel esquerdo Olá, selecione Olá **do Active Directory** botão.
3. Selecione o inquilino do Azure Active Directory (Azure AD) Olá (diretório) para o qual pretende tooenable do Azure AD DS.

    ![Selecionar o Azure AD Directory](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. No Olá **diretório de pré-visualização** página, clique em Olá **configurar** separador.

    ![Separador Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Em **dos serviços de domínio**, alterar Olá **ativar os serviços de domínio para este diretório** opção demasiado**Sim**.  
    Opções adicionais de configuração do Azure Active Directory Domain Services apresentados na página de Olá.

    ![Ativar os Serviços de Domínio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > Quando ativar o Azure Active Directory Domain Services para o seu inquilino, o Azure AD gera e armazena Olá Kerberos e NTLM hashes de credencial necessários para autenticar utilizadores.
   >
   >
6. Especifique Olá **nome de domínio DNS dos serviços de domínio**.

   * nome de domínio predefinido Olá do diretório de Olá (com um **. onmicrosoft.com** sufixo) está selecionado por predefinição.

   * Olá lista contém todos os domínios que tenham sido configurados para o diretório do Azure AD, incluindo ambos verificados e não verificado os domínios que configura num Olá **domínios** separador.

   * Também pode introduzir um nome de domínio personalizado. Neste exemplo, é o nome de domínio personalizado de Olá *contoso100.com*.

     > [!WARNING]
     > prefixo de Olá do seu nome de domínio especificado (por exemplo, *contoso100* no Olá *contoso100.com* nome de domínio) tem de conter 15 ou menos carateres. Não pode criar um domínio do Azure Active Directory Domain Services com um prefixo que contenha mais do que 15 carateres.
     >
     >
7. Certifique-se de que nome de domínio DNS Olá que escolheu para Olá gerido domínio ainda não existir na rede virtual Olá. Especificamente, verifique se o toosee:

   * Já tiver um domínio com Olá mesmo nome de domínio DNS na rede virtual Olá.

   * Olá que selecionou a rede virtual tem uma ligação VPN à sua rede no local e, se tiver um domínio com Olá mesmo nome de domínio DNS na sua rede no local.

   * Tem um serviço em nuvem existente com esse nome na rede virtual Olá.
8. Selecione uma rede virtual no qual pretende que o Azure Active Directory Domain Services toobe disponível. Selecione a rede virtual Olá e sub-rede dedicada que criou no Olá **toothis de rede virtual de serviços de domínio do Connect** na lista pendente. Considere também a seguinte Olá:

   * Certifique-se a rede virtual Olá que especificou pertence tooan região do Azure que é suportado pelo Azure Active Directory Domain Services. tooascertain Olá regiões do Azure onde os serviços de domínio do Active Directory do Azure está disponível, consulte [serviços do Azure por região](https://azure.microsoft.com/regions/#services/).

   * Redes virtuais que pertencem a região tooa onde o Azure Active Directory Domain Services não é suportado não aparecer na Olá na lista pendente.

   * Utilize uma sub-rede numa rede virtual Olá dedicada para o Azure Active Directory Domain Services. Efetue *não* selecione Olá sub-rede do gateway. Veja [considerações de redes](active-directory-ds-networking.md).

   * Da mesma forma, redes virtuais que foram criadas utilizando o Gestor de recursos do Azure não aparecem na Olá na lista pendente. O Azure Active Directory Domain Services não suporta redes virtuais baseadas no ARM atualmente.
9. Clique em tooenable do Azure Active Directory Domain Services, no painel de tarefas de Olá na Olá parte inferior da página Olá, **guardar**.
    * Enquanto o Azure Active Directory Domain Services está a ser ativado para o seu diretório, a página Olá apresenta um Estado de *pendente*.

        ![Ativar a janela dos Serviços de Domínio](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > O Azure Active Directory Domain Services fornece elevada disponibilidade para o seu domínio gerido. Depois de ativar o Azure Active Directory Domain Services, endereços IP Olá no qual o domínio serviços estão disponíveis na rede virtual Olá são apresentado um de cada vez. endereço IP segundo Olá é apresentado em breve após Olá em primeiro lugar, como logo que o serviço de Olá permite elevada disponibilidade para o seu domínio. Quando a elevada disponibilidade está configurada e Active Directory para o seu domínio, deverá ver dois endereços IP na Olá **dos serviços de domínio** secção Olá **configurar** separador.
        >
        >
    * Depois de cerca de 20 too30 minutos, Olá primeiro endereço IP no qual o domínio serviços estão disponíveis na sua rede virtual no Olá **endereço IP** campo no Olá **configurar** página.

        ![Janela dos Serviços de Domínio apresenta primeiro IP aprovisionado](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * Quando a elevada disponibilidade está operacional para o seu domínio, dois endereços IP são apresentados na página Olá. O domínio gerido está disponível na rede virtual selecionada nestes dois endereços IP.

10. Tenha em atenção dois endereços IP Olá, de modo a que possa atualizar as definições de DNS Olá na sua rede virtual. Se o fizer, permite que as máquinas virtuais no domínio toohello de tooconnect de rede virtual do Olá para operações como associação a um domínio.

    ![Janela dos Serviços de Domínio apresenta ambos os IPs aprovisionados](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> Dependendo do tamanho de Olá do inquilino do Azure AD (por exemplo, número de Olá de utilizadores ou grupos), o domínio gerido de tooyour de sincronização demora algum tempo. Este processo de sincronização ocorre em segundo plano de Olá. Para inquilinos grandes, com dezenas de milhares de objetos, poderá demorar um dia ou dois para todos os utilizadores, as associações de grupo e toobe credenciais sincronizados.
>
>

## <a name="next-step"></a>Passo seguinte
[Tarefa 4: atualizar as definições de DNS de Olá de Olá rede virtual do Azure](active-directory-ds-getting-started-update-dns.md)
