---
title: aaaUse com o AD FS 2.0 do servidor MFA do Azure | Microsoft Docs
description: "Esta é a página de autenticação do Olá multi-factor do Azure que descreve como tooget utilizar a MFA do Azure e o AD FS 2.0."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>Configurar o servidor do Azure multi-factor Authentication toowork com o AD FS 2.0
Este artigo é para as organizações que são federadas com o Azure Active Directory e pretendem toosecure recursos que estão no local ou na nuvem de Olá. Proteger os seus recursos utilizando hello do servidor multi-factor Authentication Azure e configurando-toowork com o AD FS para que a verificação de dois passos seja acionada para pontos finais de valor elevado.

Esta documentação abrange a utilização hello do servidor multi-factor Authentication Azure com o AD FS 2.0. Para mais informações sobre o AD FS, consulte [Securing cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS (Proteger recursos na cloud e no local através do Servidor Multi-Factor Authentication do Azure com o AD FS no Windows Server 2012 R2)](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>Proteger o AD FS 2.0 com um proxy
toosecure do AD FS 2.0 com um proxy, instale hello do servidor multi-factor Authentication Azure no servidor de proxy do Olá AD FS.

### <a name="configure-iis-authentication"></a>Configurar a autenticação do IIS
1. No servidor do Azure multi-factor Authentication Olá, clique em Olá **autenticação IIS** ícone no menu esquerdo Olá.
2. Clique em Olá **baseada em formulários** separador.
3. Clique em **Adicionar**.

   <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. variáveis de nome de utilizador, palavra-passe e domínio toodetect automaticamente, introduza o URL de início de sessão de Olá (por exemplo, https://sso.contoso.com/adfs/ls) na caixa de diálogo autoconfigurar Web site Olá e clique em **OK**.
5. Verifique Olá **correspondência de utilizador exigir autenticação multi-factor do Azure** caixa se todos os utilizadores tiverem sido ou importados para Olá servidor e a verificação de passo tootwo do requerente. Se um número significativo de utilizadores ainda não foram importado para Olá servidor e/ou estiverem excluído da verificação de dois passos, deixe Olá caixa desmarcada.
6. Se as variáveis de página Olá não não possível detetar automaticamente, clique em Olá **especificar manualmente...** botão na caixa de diálogo autoconfigurar Web site Olá.
7. Na caixa de diálogo Adicionar Web site de Olá, introduza a página de início de sessão do Olá URL toohello AD FS no campo URL de envio de Olá (por exemplo, https://sso.contoso.com/adfs/ls) e introduza um nome de aplicação (opcional). nome da aplicação Olá aparece nos relatórios do Azure multi-factor Authentication e poderá ser apresentado nas mensagens de autenticação SMS ou da aplicação móvel.
8. Definir o formato de pedido de Olá demasiado**POST ou GET**.
9. Introduza a variável de nome de utilizador Olá (ctl00$ ContentPlaceHolder1$ UsernameTextBox) e a variável de palavra-passe (ctl00$ ContentPlaceHolder1$ PasswordTextBox). Se a página de início de sessão baseado em formulários apresentar uma caixa de texto do domínio, introduza a variável de domínio de Olá bem. os nomes de Olá toofind das caixas de entrada Olá na página de início de sessão de Olá, aceda toohello página de início de sessão num browser, faça duplo clique na página Olá e selecione **Ver origem**.
10. Verifique Olá **correspondência de utilizador exigir autenticação multi-factor do Azure** caixa se todos os utilizadores tiverem sido ou importados para Olá servidor e a verificação de passo tootwo do requerente. Se um número significativo de utilizadores ainda não foram importado para Olá servidor e/ou estiverem excluído da verificação de dois passos, deixe Olá caixa desmarcada.
    <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Clique em **Avançado...** tooreview definições avançada. As definições que pode configurar incluem:

    - Selecione um ficheiro de página de rejeição personalizado
    - Site de toohello cache autenticações efetuadas com êxito a utilização de cookies
    - Selecione a forma como tooauthenticate Olá credenciais principais

12. Uma vez que o servidor de proxy do Olá AD FS não é provável que toobe associados a um domínio toohello, pode utilizar o controlador de domínio do LDAP tooconnect tooyour para a importação de utilizador e a pré-autenticação. Na caixa de diálogo site avançado baseado em formulários de Olá, clique em Olá **autenticação primária** separador e selecione **enlace LDAP** para Olá tipo de autenticação de pré-autenticação.
13. Quando terminar, clique em **OK** tooreturn toohello caixa de diálogo Adicionar Web site.
14. Clique em **OK** caixa de diálogo de Olá tooclose.
15. Uma vez Olá URL e as variáveis de página foram detetadas ou introduzidas, dados do site Olá apresenta no Olá painel baseado em formulário.
16. Clique em Olá **módulo nativo** separador e selecione Olá servidor, site Olá que proxy do Olá AD FS está em execução sob (como "Default Web Site"), ou hello do AD FS proxy aplicação (por exemplo, "ls" em "adfs") tooenable Olá Plug-in ao hello do IIS nível pretendido.
17. Clique em Olá **autenticação ativar o IIS** caixa, Olá parte superior do ecrã de Olá.

autenticação do IIS Olá está agora ativada.

### <a name="configure-directory-integration"></a>Configurar a integração de diretórios
Ativar a autenticação do IIS, mas tooperform Olá pré-autenticação tooyour do Active Directory (AD) através de LDAP, tem de configurar Olá controlador de domínio de toohello de ligação LDAP.

1. Clique em Olá **integração de diretórios** ícone.
2. No separador de definições de Olá, selecione Olá **utilize a configuração de LDAP específica** botão de opção.

   <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Clique em **Editar**.
4. Na caixa de diálogo Editar configuração de LDAP de Olá, preencha os campos de Olá com o controlador de domínio do Olá informações necessárias tooconnect toohello AD. As descrições dos campos de Olá estão incluídas no ficheiro de ajuda do servidor do Azure multi-factor Authentication Olá.
5. Testar a ligação de LDAP Olá clicando Olá **teste** botão.

   <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Se o teste de ligação LDAP Olá foi concluída com êxito, clique em **OK**.

### <a name="configure-company-settings"></a>Configurar definições da empresa
1. Em seguida, clique em Olá **definições da empresa** ícone e selecione Olá **resolução de nome de utilizador** separador.
2. Selecione Olá **o atributo de identificador exclusivo de LDAP de utilização para correspondentes** botão de opção.
3. Se os utilizadores introduzirem o respetivo nome de utilizador no formato "domínio \ nomedeutilizador", Olá servidor tem de domínio de Olá toobe toostrip consegue desativar Olá nome de utilizador ao criar consulta LDAP Olá. Isso pode ser feito através de uma definição de registo.
4. Abra o editor de registo Olá e aceda tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive redes/PhoneFactor num servidor de 64 bits. Se no servidor de 32 bits, coloque Olá "Wow6432Node" fora do caminho de Olá. Criar um DWORD chave de registo denominada "UsernameCxz_stripPrefixDomain" e defina Olá valor too1. Multi-factor Authentication do Azure está agora a proteger o proxy de Olá do AD FS.

Certifique-se de que os utilizadores tiverem sido importados do Active Directory para hello do servidor. Consulte Olá [secção IPs fidedignos](#trusted-ips) se gostaria de toowhitelist endereços IP internos para que a verificação não é necessária quando iniciar sessão no site de toohello partir dessas localizações.

<center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>AD FS 2.0 Direct sem proxy
Pode proteger o AD FS quando não for utilizado o proxy do Olá AD FS. Instalar hello do servidor multi-factor Authentication Azure no servidor de Olá do AD FS e configurar Olá servidor por Olá os seguintes passos:

1. No servidor do Azure multi-factor Authentication Olá, clique em Olá **autenticação IIS** ícone no menu esquerdo Olá.
2. Clique em Olá **HTTP** separador.
3. Clique em **Adicionar**.
4. Na caixa de diálogo Adicionar URL Base Olá, introduza o URL de Olá para Olá Web site do AD FS onde será efetuada a autenticação HTTP (por exemplo, https://sso.domain.com/adfs/ls/auth/integrated) no campo URL de Base de Olá. Em seguida, introduza um Nome da aplicação (opcional). nome da aplicação Olá aparece nos relatórios do Azure multi-factor Authentication e poderá ser apresentado nas mensagens de autenticação SMS ou da aplicação móvel.
5. Se pretender, ajuste o tempo limite de inatividade Olá e máximo horas de sessão.
6. Verifique Olá **correspondência de utilizador exigir autenticação multi-factor do Azure** caixa se todos os utilizadores tiverem sido ou importados para Olá servidor e a verificação de passo tootwo do requerente. Se um número significativo de utilizadores ainda não foram importado para Olá servidor e/ou estiverem excluído da verificação de dois passos, deixe Olá caixa desmarcada.
7. Selecione a caixa de cache de cookie de Olá se assim o desejar.

   <center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Clique em **OK**.
9. Clique em Olá **módulo nativo** separador e selecione Olá servidor, site Olá (como "Default Web Site") ou Olá de tooenable de aplicação (por exemplo, "ls" em "adfs") Olá do AD FS IIS Plug-in em Olá pretendido nível.
10. Clique em Olá **autenticação ativar o IIS** caixa, Olá parte superior do ecrã de Olá.

O Multi-Factor Authentication do Azure está agora a proteger o AD FS.

Certifique-se de que os utilizadores tiverem sido importados do Active Directory para hello do servidor. Consulte Olá secção IPs fidedignos se gostaria de IP interno toowhitelist endereços, de modo a que a verificação não é necessária quando iniciar sessão no site de toohello partir dessas localizações.

## <a name="trusted-ips"></a>IPs Fidedignos
Os IPs fidedignos permitem aos utilizadores toobypass Azure multi-factor Authentication para pedidos de Web site provenientes de endereços IP ou sub-redes específicas. Por exemplo, poderá pretender que os utilizadores de tooexempt da verificação de dois passos quando iniciam sessão no escritório de Olá. Para tal, tem de especificar a sub-rede do escritório Olá como uma entrada de IPs fidedignos.

### <a name="tooconfigure-trusted-ips"></a>tooconfigure IPs fidedignos
1. Na secção autenticação do IIS Olá, clique em Olá **IPs fidedignos** separador.
2. Clique em Olá **adicionar...** Adicionar...
3. Quando for apresentada a caixa de diálogo Adicionar IPs fidedignos Olá, selecione uma das Olá **IP único**, **intervalo IP**, ou **sub-rede** botões de opção.
4. Introduza o endereço IP Olá, intervalo de endereços IP ou sub-rede que deve estar na lista de permissões. Se introduzir uma sub-rede, selecione Olá Olá adequada de máscara de rede e clique em **OK** botão. Olá fidedigno que foi agora adicionado IP.

<center>![Configuração](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
