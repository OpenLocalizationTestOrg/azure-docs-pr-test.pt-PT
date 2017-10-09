---
title: "aaaEnable Proxy de aplicações do Azure AD no portal clássico Olá | Microsoft Docs"
description: "Ativar o Proxy de aplicações no Olá portal clássico do Azure e instalar os conectores de Olá para proxy inverso Olá."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Ativar o Proxy da aplicação no portal clássico Olá e transferir conectores
Este artigo explica os passos de Olá tooenable Proxy de aplicações do Microsoft Azure AD para o diretório em nuvem no Azure AD.

Se não estiver familiarizado com o Proxy de aplicações podem ajudar a fazer, saiba mais sobre [como tooprovide proteger o acesso remoto aplicações tooon local](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Pré-requisitos do Proxy da Aplicação
Antes de poder ativar e utilizar os serviços do Proxy de aplicações, terá de toohave:

* Uma [subscrição Basic ou Premium do Microsoft Azure AD](active-directory-editions.md) e um diretório do Azure AD para o qual terá de ser um administrador global.
* Um servidor a executar o Windows Server 2012 R2 ou 2016, em que pode instalar Olá conector do Proxy da aplicação. Olá servidor envia pedidos toohello serviços da Proxy da aplicação na nuvem de Olá, e necessita de um HTTP ou HTTPS ligação toohello aplicações que estão a publicar.
  * Para tooyour de início de sessão único publicado aplicações, esta máquina deve ser associado a um domínio no domínio Olá mesmo AD como aplicações de Olá que está a publicar. Para informações, consulte [-início de sessão único com o Proxy da aplicação](active-directory-application-proxy-sso-using-kcd.md)
* Se a sua organização utiliza o proxy de leitura de internet, servidores tooconnect toohello [funcionam com existente no local servidores proxy](application-proxy-working-with-proxy-servers.md) para obter detalhes sobre como tooconfigure-los.

## <a name="open-your-ports"></a>Abrir as portas

tooprepare o ambiente para Proxy de aplicações do Azure AD, terá primeiro de comunicação de tooenable tooAzure centros de dados. Se existir uma firewall no caminho de Olá, certifique-se de que está aberta, pelo que Olá que conector possa fazer HTTPS (TCP) solicita toohello Proxy de aplicações.

1. Seguinte Olá abrir portas demasiado**saída** tráfego:

   | Número de porta | Como é utilizado |
   | --- | --- |
   | 80 | Transferência de revogação de certificados as CRLs () ao validar o certificado SSL Olá |
   | 443 | Todas as comunicações de saída com Olá serviço Proxy de aplicações |

   Se a firewall impuser tráfego de acordo com os utilizadores de toooriginating, abra estas portas para o tráfego dos serviços do Windows em execução como um serviço de rede.

   > [!IMPORTANT]
   > tabela de Olá reflete os requisitos de portas de Olá para versões de conector 1.5.132.0 e mais recentes. Se ainda tiver uma versão mais antiga do conector, terá também de Olá tooenable seguintes portas: 5671, 8080, 9090, 9091, 9350, 9352 e 10100 – 10120.
   >
   >Para obter informações sobre como atualizar a versão mais recente do toohello de conectores, consulte [conetores da Proxy da aplicação Azure compreender AD](application-proxy-understand-connectors.md#automatic-updates).

2. Se a sua firewall ou proxy permite adicionar à lista branca DNS, pode toomsappproxy.net de ligações de lista branca e servicebus.windows.net. Se não, terá de tooallow acesso toohello [intervalos de IP de DataCenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653), que são atualizadas por semana.

3. Olá utilize [do Azure AD aplicação Proxy portas teste ferramenta do conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que o conector pode contactar o serviço de Proxy da aplicação Olá. No mínimo, certifique-se de que a região EUA Central de Olá e Olá região mais próxima tooyou têm todas as marcas de verificação verdes. Para além disso, as marcas de verificação verde mais significa maior resiliência.

## <a name="enable-application-proxy-in-azure-ad"></a>Ativar o Proxy da aplicação no Azure AD
1. Inicie sessão como administrador no Olá [portal clássico do Azure](https://manage.windowsazure.com/).
2. Aceda tooActive diretório e selecione o diretório de Olá em que pretende tooenable Proxy de aplicações.

    ![Active Directory – ícone](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Selecione **configurar** da página do diretório de Olá e desloque para baixo demasiado**Proxy de aplicações**.
4. Ativar/desativar **ativar serviços da Proxy da aplicação para este diretório** demasiado**ativado**.

    ![Ativar o Proxy da Aplicação](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. Selecione **Transferir agora**. Olá **do Azure AD aplicação transferir Conetor da Proxy** abre. Leia e aceite os termos de licenciamento de Olá e clique em **transferir** toosave Olá ficheiro do Windows Installer (.exe) para o conector de Olá.

## <a name="install-and-register-hello-connector"></a>Instalar e registar Olá conector
1. Executar **AADApplicationProxyConnectorInstaller.exe** no servidor de Olá que preparou de acordo com a pré-requisitos de toohello.
2. Siga as instruções de Olá Olá assistente tooinstall.
3. Durante a instalação, é pedido tooregister Olá conector com Olá Proxy da aplicação do inquilino do Azure AD.

   * Indique as suas credenciais de administrador global do Azure AD. O inquilino do administrador global pode ser diferente das suas credenciais do Microsoft Azure.
   * Certifique-se Olá, admin quem Olá, regista Olá conector está no mesmo diretório onde ativou Olá serviço Proxy de aplicações. Por exemplo, se Olá domínio de inquilino for contoso.com, Olá, admin deve ser admin@contoso.com ou qualquer outro alias nesse domínio.
   * Se **configuração de segurança avançada do IE** estiver definido demasiado**no** no servidor de Olá, ecrã de registo de Olá poderá ser bloqueado. acesso tooallow, siga as instruções de Olá na mensagem de erro de saudação. Certifique-se de que a Segurança Avançada do Internet Explorer está desativada.
   * Se o registo do conetor falhar, veja [Resolver Problemas da Proxy da Aplicação](active-directory-application-proxy-troubleshoot.md).  
4. Quando concluir a instalação de Olá, são adicionados dois novos serviços tooyour servidor:

   * O **Conector do Proxy da Aplicação do Microsoft AAD** ativa a conectividade

     * **Atualizador de conector do Proxy de aplicações do Microsoft AAD** é um serviço de atualização automática. Periodicamente verifica a existência de novas versões do conector de Olá e atualiza o conector de Olá conforme necessário.

     ![Serviços do Conector do Proxy da Aplicação – captura de ecrã](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Clique em **concluir** na janela de instalação de Olá.

Para obter informações sobre conectores, consulte [Understand Azure AD Application Proxy connectors (Compreender os conectores do Proxy da Aplicação do Azure AD)](application-proxy-understand-connectors.md).

Para fins de elevada disponibilidade, deve implementar pelo menos dois conetores. toodeploy mais conetores, repita os passos 2 e 3. Cada conetor tem de ser registado separadamente.

Se quiser toouninstall Olá conector, desinstale o serviço de conectores Olá e o serviço do Atualizador de Olá. Reinicie o serviço do Olá toofully remover o computador.

## <a name="next-steps"></a>Passos seguintes
Agora, está pronto demasiado[publicar aplicações com o Proxy de aplicações](active-directory-application-proxy-publish.md).

Se tiver aplicações que estão em redes separadas ou em diferentes localizações, pode utilizar o conector grupos tooorganize Olá diferentes conetores em unidades lógicas. Saiba mais sobre [Trabalhar com conetores da Proxy da Aplicação](active-directory-application-proxy-connectors.md).
