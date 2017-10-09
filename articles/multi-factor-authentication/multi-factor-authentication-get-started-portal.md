---
title: portal de aaaUser para o servidor MFA do Azure | Microsoft Docs
description: "Este é Olá multi-factor authentication página que descreve como tooget iniciado com o Azure MFA e o portal de utilizador Olá."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Portal de utilizador para hello do servidor multi-factor Authentication Azure

portal de utilizador de Olá é um web site do IIS que permite que os utilizadores tooenroll no Azure multi-factor Authentication (MFA) e manter as contas. Um utilizador pode alterar o número de telefone, alterar o PIN ou escolha toobypass verificação em dois passos durante o seu próximo início de sessão.

Os utilizadores iniciar sessão no portal de utilizador toohello com o respetivo nome de utilizador normal e a palavra-passe, em seguida, concluir uma chamada de verificação de dois passos ou responder toocomplete de perguntas de segurança a autenticação. Se for permitida a inscrição do utilizador, os utilizadores configurar o número de telefone e Olá PIN pela primeira vez que iniciarem sessão no portal de utilizador toohello.

Portal de utilizador administradores pode ser configurada e concedido os novos utilizadores tooadd de permissão e atualizar utilizadores existentes.

Dependendo do seu ambiente, poderá ser útil portal de utilizador de Olá toodeploy no Olá mesmo servidor como servidor do Azure multi-factor Authentication ou noutro servidor de acesso à internet.

![Portal de utilizador do MFA](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> portal de utilizador Olá só está disponível com o servidor multi-factor Authentication. Se utilizar o multi-factor Authentication na nuvem de Olá, consulte o toohello utilizadores [configurar a conta para a verificação de dois passos](./end-user/multi-factor-authentication-end-user-first-time.md) ou [gerir as definições de verificação em dois passos](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-hello-web-service-sdk"></a>Instalar o SDK do serviço de web Olá

O cenário, se hello Web Service SDK do Azure multi-factor Authentication é **não** já instalado Olá servidor multi-factor Authentication (MFA) do Azure, Olá concluir os passos que se seguem.

1. Abra a consola do servidor multi-factor Authentication Olá.
2. Aceda toohello **Web Service SDK** e selecione **instalar o Web Service SDK**.
3. Instalação completa Olá com predefinições do Olá não ser que necessite toochange-las por algum motivo.
4. Vincule a um site de toohello certificado SSL no IIS.

Se tiver dúvidas sobre como configurar um certificado SSL num servidor IIS, consulte o artigo de Olá [como tooSet segurança SSL no IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Olá SDK do serviço Web tem de estar protegido por um certificado SSL. Pode utilizar um certificado autoassinado para este fim. Importar o certificado de Olá para arquivo de "Raiz autoridades de certificação" de Olá Olá Local da conta do computador no servidor de web do Portal de utilizador Olá, para que confia esse certificado quando inicia a ligação de SSL Olá.

![SDK do Serviço Web de configuração do Servidor MFA](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>Implementar o portal de utilizador de Olá no Olá mesmo servidor que hello do servidor multi-factor Authentication Azure

Olá pré-requisitos seguintes são necessários tooinstall portal de utilizador de Olá no Olá **mesmo servidor** como hello do servidor multi-factor Authentication Azure:

* IIS, incluindo compatibilidade base meta para ASP.NET e IIS 6 (para IIS 7 ou posterior)
* Uma conta com direitos de administrador para o computador de Olá e domínio, se aplicável. conta de Olá tem de grupos de segurança permissões toocreate do Active Directory.
* Portal de utilizador de Olá segura com um certificado SSL.
* Proteja Olá Web Service SDK do Azure multi-factor Authentication com um certificado SSL.

toodeploy Olá siga portal, utilizador estes passos:

1. Abra a consola do servidor do Azure multi-factor Authentication Olá, clique em Olá **Portal de utilizador** menu à esquerda de ícone na Olá, em seguida, clique em **instalar o Portal de utilizador**.
2. Instalação completa Olá com predefinições do Olá não ser que necessite toochange-las por algum motivo.
3. Vincular um site de toohello certificado SSL no IIS

   > [!NOTE]
   > Este certificado SSL é, normalmente, um certificado SSL assinado publicamente.

4. Abra um browser a partir de qualquer computador e navegar URL toohello em que o portal de utilizador Olá foi instalado (exemplo: https://mfa.contoso.com/MultiFactorAuth). Certifique-se de que não são apresentados erros ou avisos de certificado.

![Instalação do Portal de Utilizador do Servidor MFA](./media/multi-factor-authentication-get-started-portal/install.png)

Se tiver dúvidas sobre como configurar um certificado SSL num servidor IIS, consulte o artigo de Olá [como tooSet segurança SSL no IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>Implementar o portal de utilizador de Olá num servidor separado

Servidor Olá, onde servidor do Azure multi-factor Authentication está em execução não esteja através da Internet, deve instalar o portal de utilizador Olá num **servidor separado, para a internet**.

Se a organização utiliza Olá aplicação Microsoft Authenticator como um dos métodos de verificação Olá e pretende portal de utilizador de Olá toodeploy no seu próprio servidor, conclua Olá os seguintes requisitos:

* Utilizar v 6.0 ou superior do hello do servidor do Azure multi-factor Authentication.
* Instalar o portal de utilizador de Olá num servidor web para a internet com o Microsoft internet Information Services (IIS) 6. x ou superior.
* Ao utilizar o IIS 6. x, certifique-se de que ASP.NET v 2.0.50727 está instalado, registado e definido demasiado**permitidos**.
* Ao utilizar o IIS 7.x ou superior, IIS, incluindo compatibilidade base meta para Autenticação Básica, ASP.NET e IIS 6.
* Portal de utilizador de Olá segura com um certificado SSL.
* Proteja Olá Web Service SDK do Azure multi-factor Authentication com um certificado SSL.
* Certifique-se de que o portal de utilizador que Olá pode ligar toohello Web Service SDK do Azure multi-factor Authentication através de SSL.
* Certifique-se de que portal de utilizador Olá pode autenticar toohello Web Service SDK do Azure multi-factor Authentication com credenciais de Olá de uma conta de serviço no grupo de segurança "Admins de PhoneFactor" Olá. Esta conta de serviço e o grupo devem existir no Active Directory se hello do servidor multi-factor Authentication Azure está em execução num servidor associado a um domínio. Esta conta de serviço e o grupo localmente existem no hello do servidor multi-factor Authentication Azure se não for tooa associado ao domínio.

Instalar portal de utilizador de Olá num servidor diferente hello do servidor multi-factor Authentication Azure requer Olá os seguintes passos:

1. **No servidor MFA de Olá**, procure o caminho de instalação toohello (exemplo: c:\Programas\Microsoft files\servidor multi-Factor Authentication Server) e copiar o ficheiro de Olá **MultiFactorAuthenticationUserPortalSetup64** tooa localização servidor de acesso à internet toohello acessível onde irá instalar.
2. **No servidor de web de acesso à internet Olá**, execute o ficheiro de instalação de Olá MultiFactorAuthenticationUserPortalSetup64 como administrador, alterar Olá Site, se assim o desejar e alterar o nome abreviado do Olá Virtual diretório tooa se desejar.
3. Vincule a um site de toohello certificado SSL no IIS.

   > [!NOTE]
   > Este certificado SSL é, normalmente, um certificado SSL assinado publicamente.

4. Procurar demasiado**C:\inetpub\wwwroot\MultiFactorAuth**
5. Editar o ficheiro Web. config de Olá no bloco de notas

    * Localizar a chave de Olá **"USE_WEB_SERVICE_SDK"** e alterar **valor = "false"** demasiado**valor = "true"**
    * Localizar a chave de Olá **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** e alterar **valor = ""** demasiado**valor = "Domínio \ utilizador"** onde domínio ome de utilizador é uma conta de serviço que faz parte Grupo de "PhoneFactor Admins".
    * Localizar a chave de Olá **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** e alterar **valor = ""** demasiado**valor = "Password"** onde a palavra-passe é Olá palavra-passe para Olá serviço Conta introduzida na linha anterior Olá.
    * Localize o valor de Olá **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** e alterar toohello de URL esta marcador de posição URL de SDK do serviço Web que está instalada no passo 2.
    * Guarde o ficheiro Web. config de Olá e feche o bloco de notas.

6. Abra um browser a partir de qualquer computador e navegar URL toohello em que o portal de utilizador Olá foi instalado (exemplo: https://mfa.contoso.com/MultiFactorAuth). Certifique-se de que não são apresentados erros ou avisos de certificado.

Se tiver dúvidas sobre como configurar um certificado SSL num servidor IIS, consulte o artigo de Olá [como tooSet segurança SSL no IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Configurar definições de portal de utilizador no hello do servidor multi-factor Authentication Azure

Agora está instalado o portal de utilizador que Olá, terá de tooconfigure hello do servidor multi-factor Authentication Azure toowork com o portal de Olá.

1. Na consola do servidor do Azure multi-factor Authentication Olá, clique em Olá **Portal de utilizador** ícone. No separador de definições de Olá, introduza o portal de utilizador do Olá URL toohello no Olá **URL do Portal de utilizador** caixa de texto. Se tiver sido ativada a funcionalidade de e-mail, este URL está incluído nos e-mails de Olá que são enviados toousers quando forem importados para hello do servidor do Azure multi-factor Authentication.
2. Escolher Olá definições que pretende que o toouse no Olá Portal de utilizador. Por exemplo, se os utilizadores têm permissão toochoose os respetivos métodos de autenticação, certifique-se de que **permitir que os utilizadores tooselect método** estiver selecionada, juntamente com os métodos de Olá que podem escolher.
3. Definir que devem ser administradores em Olá **administradores** separador. Pode criar permissões administrativas granulares utilizando Olá caixas de verificação e as dropdowns nas caixas de adicionar/editar Olá.

Configuração opcional:
- **Perguntas de segurança** -definir aprovados perguntas de segurança para o seu idioma de ambiente e Olá aparecem no.
- **Sessões Passadas** - configure a integração do portal de utilizador com um site baseado em formulários através do MFA.
- **IPs fidedignos** -permitir que os utilizadores tooskip MFA quando a autenticação de uma lista de confiança IPs ou intervalos.

![Configuração do Portal de Utilizador do Servidor MFA](./media/multi-factor-authentication-get-started-portal/config.png)

O servidor multi-factor Authentication do Azure fornece várias opções Olá no portal de utilizador. Olá tabela seguinte fornece uma lista destas opções e obter uma explicação sobre o que são utilizadas.

| Definições do Portal de Utilizador | Descrição |
|:--- |:--- |
| URL do Portal de Utilizador | Introduza o URL de Olá de onde Olá portal está alojado. |
| Autenticação primária | Especifique o tipo de Olá de autenticação toouse quando iniciar sessão no portal de toohello. Autenticação do Windows, Radius ou LDAP. |
| Permitir que os utilizadores toolog no | Permitir que os utilizadores tooenter um nome de utilizador e palavra-passe Olá-na página sessão Olá no portal de utilizador. Se esta opção não estiver selecionada, as caixas de Olá estão desativadas. |
| Permitir a inscrição de utilizador | Permitir tooenroll um utilizador no multi-factor Authentication ao redirecioná-lo tooa ecrã de configuração que lhe solicita informações adicionais, tais como o número de telefone. O pedido do telefone alternativo permite que os utilizadores toospecify um número de telefone secundário. Pedido de terceiros OATH token permite que os utilizadores toospecify um token OATH de terceiros. |
| Permitir que os utilizadores tooinitiate omissão de uso individual | Permitir que os utilizadores tooinitiate uma omissão de uso individual. Se um utilizador configura esta opção, irá demorar Olá efeito próxima vez Olá utilizador inicia sessão. Pedido de Desativação segundos fornece Olá utilizador uma caixa para que podem alterar a predefinição de Olá de 300 segundos. Caso contrário, a omissão de uso individual Olá só é adequada para 300 segundos. |
| Permitir que os utilizadores tooselect método | Permitir que os utilizadores toospecify método de contacto principal. Este método pode ser chamada telefónica, mensagem de texto, aplicação móvel ou token OATH. |
| Permitir que os utilizadores tooselect idioma | Permitir que os utilizadores idioma de Olá toochange que é utilizado para chamada telefónica de Olá, mensagem de texto, aplicação móvel ou OATH token. |
| Permitir que a aplicação móvel de tooactivate de utilizadores | Permitir que utilizadores toogenerate um código toocomplete Olá aplicação móvel ativação processo de ativação que é utilizado com o servidor de Olá.  Também pode definir o número de Olá de dispositivos, estes podem ativar aplicação Olá, entre 1 e 10. |
| Utilizar perguntas de segurança para contingência | Permitir perguntas de segurança no caso de falha da verificação em dois passos. Pode especificar o número de Olá de perguntas de segurança que têm de ser respondidas com êxito. |
| Permitir que o token OATH de terceiros de tooassociate de utilizadores | Permitir que os utilizadores toospecify um token OATH de terceiros. |
| Utilizar token OATH para contingência | Permitir a utilização de Olá de um token OATH no caso de verificação de dois passos não for bem sucedida. Também pode especificar o tempo limite da sessão Olá em minutos. |
| Ativar registo | Ative o registo no portal de utilizador Olá. Olá ficheiros de registo estão localizados em: c:\Programas\Microsoft files\servidor multi-Factor authentication\registos.. |

Estas definições ficam utilizador toohello visível no portal de Olá quando estão ativadas e iniciar a sessão no portal de utilizador toohello.

![Definições do portal de utilizador](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Inscrição de utilizador self-service

Se pretender toosign a utilizadores em e inscrever, tem de selecionar Olá **permitir que os utilizadores toolog no** e **permitir inscrição de utilizador** opções no separador de definições de Olá. Lembre-se de que as definições de Olá que selecionar afetam Olá início de sessão experiência de utilizador.

Por exemplo, quando um utilizador inicia sessão no portal de utilizador toohello para Olá pela primeira vez, é direcionado toohello página de configuração de utilizador do Azure multi-factor Authentication. Dependendo de como tiver configurado o multi-factor Authentication do Azure, o utilizador Olá poderá ser capaz de tooselect o método de autenticação.

Se estes selecionem método de verificação de chamada de voz Olá ou tem sido previamente configurada toouse este método, página Olá pede-lhe Olá utilizador tooenter o número de telefone principal e a extensão, se aplicável. Também pode ser permitido tooenter um número de telefone alternativo.

![Registar números de telefone primários e de cópia de segurança](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Se o utilizador de Olá toouse necessário um PIN quando fizer a autenticação, página Olá solicita toocreate um PIN. Após introduzir as respetivas number(s) de telefone e o PIN (se aplicável), o utilizador Olá clica Olá **telefonar-Me agora tooAuthenticate** botão. Número de telefone principal de chamada telefónica verificação toohello um utilizador efetua a multi-factor Authentication do Azure. utilizador Olá tem de responder a chamada telefónica de Olá e introduzir o PIN (se aplicável) e prima # toomove no toohello próximo passo do processo de autoinscrição Olá.

Se o utilizador Olá seleciona o método de verificação de mensagem de texto Olá ou tiver sido previamente configurada toouse este método, a página Olá solicita Olá do utilizador para o respetivo número de telemóvel. Se o utilizador de Olá toouse necessário um PIN quando fizer a autenticação, página Olá também solicita tooenter um PIN.  Após introduzir o número de telefone e PIN (se aplicável), o utilizador Olá clica Olá **texto-Me agora tooAuthenticate** botão. Multi-factor Authentication do Azure efetua telemóvel do utilizador um SMS verificação toohello. Olá utilizador recebe uma mensagem de texto de saudação com um one-time-código de acesso (OTP), em seguida, mensagem de toohello responde com esse OTP e o PIN (se aplicável).

![SMS do portal de utilizador](./media/multi-factor-authentication-get-started-portal/text.png)

Se o utilizador Olá seleciona o método de verificação de aplicação móvel Olá, a página Olá pede-lhe Olá utilizador tooinstall Olá Microsoft Authenticator aplicação nos respetivos dispositivos e gerar um código de ativação. Depois de instalar a aplicação Olá, o utilizador Olá clica no botão gerar código de ativação de Olá.

> [!NOTE]
> aplicação do Microsoft Authenticator de toouse Olá, o utilizador Olá tem de ativar as notificações push para o respetivo dispositivo.

página Olá, em seguida, apresenta um código de ativação e um URL, juntamente com uma imagem de código de barras. Se o utilizador de Olá toouse necessário um PIN quando fizer a autenticação, página Olá adicionalmente solicita tooenter um PIN. utilizador Olá entra Olá código de ativação e o URL na aplicação do Microsoft Authenticator Olá ou utiliza a imagem de código de barras de Olá scanner tooscan Olá código de barras e clica no botão Ativar de Olá.

Após a conclusão da ativação Olá, utilizador de Olá clica Olá **autenticar-Me agora** botão. Multi-factor Authentication do Azure efetua a aplicação móvel de um utilizador de toohello de verificação. utilizador Olá tem de introduzir o PIN (se aplicável) e clique no botão Olá autenticar no respetivo toomove de aplicação móvel no toohello próximo passo do processo de autoinscrição Olá.

Se tem configurado os administradores de Olá hello do servidor multi-factor Authentication Azure toocollect segurança perguntas e respostas, utilizador de Olá é então direcionado toohello página de perguntas de segurança. utilizador Olá tem de selecionar quatro perguntas de segurança e fornecer respostas a perguntas tootheir selecionado.

![Perguntas de segurança do portal de utilizador](./media/multi-factor-authentication-get-started-portal/secq.png)

Olá autoinscrição do utilizador está agora concluída e o utilizador de Olá é iniciada no portal de utilizador toohello. Utilizadores podem iniciar sessão no portal de utilizador toohello em qualquer altura nas toochange futuras Olá os respetivos números de telefone, PINs, métodos de autenticação e perguntas de segurança se é permitido alterar os respetivos métodos pelos administradores deles.

## <a name="next-steps"></a>Passos seguintes

- [Implementar Olá Azure multi-factor Authentication Server Mobile serviço Web da aplicação](multi-factor-authentication-get-started-server-webservice.md)
