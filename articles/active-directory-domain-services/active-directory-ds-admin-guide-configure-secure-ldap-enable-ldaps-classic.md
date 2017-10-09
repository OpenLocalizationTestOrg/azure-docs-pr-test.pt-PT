---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do Azure AD | Microsoft Docs"
description: "Configurar o LDAP seguro (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurar segura LDAP (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD

## <a name="before-you-begin"></a>Antes de começar
Certifique-se de que concluiu [tarefa 2 - exportação Olá segura LDAP certificado tooa. Ficheiro PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Optar por toouse Olá pré-visualização experiência do portal do Azure ou Olá toocomplete de portal clássico do Azure esta tarefa.
> [!div class="op_single_selector"]
> * **Portal do Azure (pré-visualização)**: [Enable secure LDAP utilizando Olá portal do Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Portal clássico do Azure**: [Enable secure LDAP utilizando o portal clássico do Azure Olá](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Tarefa 3 - ativar LDAP seguro para Olá domínio gerido utilizando o portal clássico do Azure Olá
tooenable LDAP seguro, execute os seguintes passos de configuração de Olá:

1. Navegue toohello  **[portal clássico do Azure](https://manage.windowsazure.com)**.
2. Selecione Olá **do Active Directory** nós no painel esquerdo Olá.
3. Selecione o diretório de Olá do Azure AD (também referida tooas "tenant"), para que tiver ativado os serviços de domínio do Azure AD.

    ![Selecionar o Azure AD Directory](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Clique em Olá **configurar** separador.

    ![Separador Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Desloque para baixo toohello secção intitulada **dos serviços de domínio**. Deverá ver uma opção intitulada **LDAP seguro (LDAPS)** conforme mostrado na seguinte captura de ecrã de Olá:

    ![Secção de configuração dos Serviços de Domínio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Clique em Olá **configurar certificado...**  botão toobring segurança Olá **configurar certificados para proteger o LDAP** caixa de diálogo.

    ![Configurar o certificado para o LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Clique em seguinte de ícone de pasta Olá **ficheiro com um certificado PFX** toospecify Olá PFX ficheiro que contém o certificado Olá desejar toouse para toohello de acesso LDAP seguro geridos domínio. Também introduza a palavra-passe de Olá que especificou ao exportar o ficheiro do Olá certificado toohello PFX. Em seguida, clique em Olá feito botão na parte inferior de Olá.

    ![Especifique o ficheiro de LDAP PFX seguro e a palavra-passe](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Olá **dos serviços de domínio** secção Olá **configurar** separador deve obter cinzento e está a ser Olá **pendentes...**  Estado alguns minutos. Durante este período, certificado LDAPS Olá é verificado em termos de exatidão e segura LDAP estiver configurado para o seu domínio gerido.

    ![Proteger o LDAP - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Demora cerca de 10 minutos de too15 tooenable proteger LDAP para o seu domínio gerido. Se Olá fornecido não corresponde ao certificado LDAP seguro Olá necessário critérios, LDAP seguro não está ativada para o seu diretório e verá uma falha. Por exemplo, nome de domínio Olá está incorreto, certificado Olá já expirou ou expira em breve.
   >
   >

9. Quando o LDAP seguro está ativado com êxito para o seu domínio gerido, Olá **pendentes...**  deve desaparecer mensagem. Deverá ver Olá impressão digital do certificado de Olá apresentado.

    ![LDAP seguro ativado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Tarefa 4 - ativar o acesso LDAP seguro através de Olá internet
**Tarefas opcionais** - se não planear tooaccess Olá domínio gerido utilizando LDAPS mais Olá internet, ignorar esta tarefa de configuração.

Antes de começar esta tarefa, certifique-se de que concluiu os passos de Olá descritos em [tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. Deverá ver uma opção demasiado**ATIVAR SECURE LDAP acesso através de Olá INTERNET** no Olá **dos serviços de domínio** secção Olá **configurar** página. Esta opção estiver definida demasiado**não** por predefinição, uma vez que toohello de acesso à internet geridos domínio através de LDAP seguro está desativado por predefinição.

    ![LDAP seguro ativado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. Ativar/desativar **ATIVAR SECURE LDAP acesso através de Olá INTERNET** demasiado**Sim**. Clique em Olá **guardar** botão no painel inferior de Olá.
    ![LDAP seguro ativado](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Olá **dos serviços de domínio** secção Olá **configurar** separador deve obter cinzento e está a ser Olá **pendentes...**  Estado alguns minutos. Após algum tempo, internet acesso tooyour domínio gerido através de LDAP seguro está ativado.

    ![Proteger o LDAP - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Demora cerca de 10 minutos tooenable acesso à internet através de LDAP seguro para o seu domínio gerido.
   >
   >
4. Quando tooyour de acesso LDAP seguro efectuada domínio Olá internet é ativada com êxito, Olá **pendentes...**  deve desaparecer mensagem. Deverá ver Olá IP externo de endereços que podem ser o diretório de tooaccess utilizados por LDAPS no campo Olá **IP endereço para LDAPS acesso externo**.

    ![LDAP seguro ativado](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Tarefa 5 - configurar o DNS tooaccess Olá domínio gerido de Olá internet
**Tarefas opcionais** - se não planear tooaccess Olá domínio gerido utilizando LDAPS mais Olá internet, ignorar esta tarefa de configuração.

Antes de começar esta tarefa, certifique-se de que concluiu os passos de Olá descritos em [Tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).

Assim que tiver ativado o acesso LDAP seguro através de Olá internet para o seu domínio gerido, terá de tooupdate DNS para que os computadores cliente possam localizar este domínio gerido. No final Olá Tarefa 4, um endereço IP externo é apresentado no Olá **configurar** separador **IP endereço para LDAPS acesso externo**.

Configure o seu fornecedor de DNS externo para que esse nome DNS Olá de Olá geridos endereço IP externo do domínio (por exemplo, ' ldaps.contoso100.com') toothis pontos. No nosso exemplo, é preciso Olá toocreate seguir a entrada DNS:

    ldaps.contoso100.com  -> 52.165.38.113

Já está - está agora toohello tooconnect pronto gerido Olá de domínio utilizando o LDAP seguro através de internet.

> [!WARNING]
> Lembre-se de que os computadores cliente têm de confiar emissor Olá de Olá LDAPS certificado toobe capaz de tooconnect com êxito toohello gerido a utilizar o LDAPS do domínio. Se estiver a utilizar uma autoridade de certificação empresarial ou uma autoridade de certificação publicamente fidedigna, não terá toodo nada, uma vez que os computadores cliente confiar estes emissores de certificados. Se estiver a utilizar um certificado autoassinado, terá de tooinstall Olá pública faz parte do certificado autoassinado Olá no arquivo de certificados fidedignos Olá no computador de cliente Olá.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Bloqueio pendente LDAPS aceder domínio gerido tooyour através de Olá internet
> [!NOTE]
> **Tarefas opcionais** - se não tiver ativado o LDAPS domínio gerido do acesso toohello mais Olá internet, ignorar esta tarefa de configuração.
>
>

Antes de começar esta tarefa, certifique-se de que concluiu os passos de Olá descritos em [Tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).

A exposição do seu domínio gerido para o acesso LDAPS através de Olá internet representa uma ameaça de segurança. Olá domínio gerido está acessível a partir do Olá internet na porta de Olá utilizada para o LDAP seguro (ou seja, porta 636). Por conseguinte, pode escolher toorestrict acesso toohello gerido domínio toospecific conhecido endereços IP. Para segurança melhorada, crie um grupo de segurança de rede (NSG) e associá-la a sub-rede de olá onde tiver ativado os serviços de domínio do Azure AD.

Olá tabela a seguir ilustra um exemplo NSG pode configurar, toolock para baixo de acesso LDAP seguro através de Olá internet. Olá NSG contém um conjunto de regras que permitem acesso de entrada de LDAPS através da porta TCP 636 apenas a partir de um conjunto especificado de endereços IP. Olá predefinido 'DenyAll' regra aplica-se tooall outro tráfego de entrada de Olá internet. Olá NSG regra tooallow LDAPS acesso através de Olá internet a partir de endereços IP especificados tem uma prioridade superior à Olá regra DenyAll NSG.

![Olá, acesso LDAPS do exemplo NSG toosecure pela internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Obter mais informações** - [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de domínio do Azure AD - guia de introdução](active-directory-ds-getting-started.md)
* [Administrar um domínio gerido dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Administrar a política de grupo num domínio gerido dos serviços de domínio do Azure AD](active-directory-ds-admin-guide-administer-group-policy.md)
* [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md)
* [Criar um grupo de segurança de rede](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
