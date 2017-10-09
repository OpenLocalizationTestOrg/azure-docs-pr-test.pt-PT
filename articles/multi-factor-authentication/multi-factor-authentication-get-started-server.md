---
title: aaaGetting iniciado Azure multi-factor Authentication Server | Microsoft Docs
description: "Esta é a página de autenticação do Olá multi-factor do Azure que descreve como tooget iniciado com o servidor MFA do Azure."
services: multi-factor-authentication
keywords: "servidor de autenticação, página de ativação da aplicação multi factor authentication do azure, transferência do servidor de autenticação"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Introdução ao hello do servidor multi-factor Authentication Azure

<center>![MFA no local](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Agora que Determinámos toouse-local no servidor multi-factor Authentication, vamos começar. Esta página abrange uma nova instalação do servidor de Olá e configurar com o Active Directory no local. Se já tiver o servidor MFA de Olá instalado e estiver à procura tooupgrade, consulte o artigo [atualizar toohello mais recente do Azure multi-factor Authentication Server](multi-factor-authentication-server-upgrade.md). Se estiver à procura de informações sobre como instalar apenas o serviço de web Olá, consulte [Olá de implementação do Azure multi-factor Authentication Server Mobile serviço Web da aplicação](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Planear a sua implementação

Antes de transferir hello do servidor do Azure multi-factor Authentication, pensa sobre quais são os requisitos de elevada disponibilidade e carga. Utilize este toodecide informações como e onde toodeploy.

Uma boa orientação para a quantidade de Olá de memória que precisa é o número de Olá de utilizadores esperar tooauthenticate regularmente.

| Utilizadores | RAM |
| ----- | --- |
| 1-10,000 | 4GB |
| 10,001-50,000 | 8 GB |
| 50,001-100,000 | 12 GB |
| 100,000-200,001 | 16 GB |
| 200,001+ | 32 GB |

Tem de tooset configurar vários servidores para elevada disponibilidade ou o balanceamento de carga? Existem várias formas tooset esta configuração de servidor MFA do Azure. Quando instalar o primeiro servidor MFA do Azure, torna-se mestre Olá. Todos os servidores adicionais ficam subordinados e sincronizar automaticamente os utilizadores e a configuração com o mestre de Olá. Em seguida, pode configurar um servidor primário e ter rest Olá agir como cópia de segurança, ou pode configurar com balanceamento de carga entre todos os servidores de Olá.

Quando o mestre de um servidor MFA do Azure fica offline, servidores subordinada Olá ainda podem pedidos de verificação de dois passos do processo. No entanto, não é possível adicionar novos utilizadores e os utilizadores existentes não é possível atualizar as definições até que o mestre de Olá está online ou subordinado obtém promovido.

### <a name="prepare-your-environment"></a>Preparar o ambiente

Certifique-se de servidor de Olá que estiver a utilizar para o Azure multi-factor Authentication cumpre os requisitos de Olá:

| Requisitos do Servidor Multi-Factor Authentication do Azure | Descrição |
|:--- |:--- |
| Hardware |<li>200 MB de espaço no disco rígido</li><li>processador com capacidade de 32 ou 64 bits</li><li>1 GB de RAM ou superior</li> |
| Software |<li>Windows Server 2008 ou superior, se o anfitrião de Olá for um SO servidor</li><li>Windows 7 ou superior, se o anfitrião de Olá for um SO de cliente</li><li>Microsoft .NET 4.0 Framework</li><li>IIS 7.0 ou superior, se instalar Olá utilizador portal ou do web service SDK</li> |

### <a name="azure-mfa-server-components"></a>Componentes de Servidor MFA do Azure

Existem três componentes Web que compõem o servidor MFA do Azure:

* O serviço SDK - ativa a comunicação com Olá outros componentes e está instalado no servidor de aplicações do Azure MFA Olá Web
* Portal de utilizador - um web site do IIS que permite que os utilizadores tooenroll no Azure multi-factor Authentication (MFA) e manter as contas.
* Serviço Web da aplicação móvel - ativa uma aplicação móvel como Olá Microsoft Authenticator aplicação a utilizar para verificação de dois passos.

Todos os três componentes podem ser instalados em Olá mesmo servidor, se o servidor Olá é para a internet. Se dividi componentes Olá, Olá Web Service SDK está instalado no servidor de aplicações do Azure MFA Olá e Olá Portal de utilizador e o serviço Web da aplicação móvel são instalados num servidor de acesso à internet.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Requisitos da firewall do Servidor Multi-Factor Authentication do Azure

Cada servidor MFA tem de ser capaz de toocommunicate na porta 443 toohello saída, os seguintes endereços:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Se as firewalls de saída estiverem restritas na porta 443, abra Olá seguintes intervalos de endereços IP:

| Subrede IP | Máscara de rede | Intervalo de IP |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Se não estiverem a utilizar funcionalidades de confirmação de evento Olá e os utilizadores não estiverem a utilizar as aplicações móveis tooverify dos dispositivos na rede empresarial Olá, basta Olá intervalos os seguintes:

| Subrede IP | Máscara de rede | Intervalo de IP |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Transferir hello do servidor multi-factor Authentication Azure

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) como administrador.
2. Olá esquerda, selecione **do Active Directory**
3. Clique em **Utilizadores e grupos**
4. Clique em **Todos os utilizadores**
5. Clique em **Multi-Factor Authentication**
6. Na secção **autenticação multifator**, selecione **definições de serviço**

   ![Página de definições de serviço](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Na página de definições de serviços de Olá, na Olá parte inferior do ecrã de Olá, clique em **aceda toohello portal**. Uma nova página é aberta.
7. Clique em **Transferências**.
8. Clique em Olá **transferir** e guardar o instalador Olá da ligação.

   ![Transferir o Servidor MFA](./media/multi-factor-authentication-get-started-server/download4.png)

9. Esta página manter abertas que iremos dar tooit depois de instalador de Olá em execução.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>Instalar e configurar hello do servidor multi-factor Authentication Azure

Agora que transferiu o servidor de Olá pode instalar e configurá-lo. Lembre-se de que esse servidor de Olá que está a instalar cumpre os requisitos listados em Olá secção sobre o planeamento.

1. Faça duplo clique Olá executável.
2. No ecrã selecionar pasta de instalação de Olá, certifique-se dessa pasta Olá está correta e clique em **seguinte**.
3. Após a conclusão da instalação de Olá, clique em **concluir**.  inicia o Assistente de configuração de Olá.
4. No Olá assistente bem-vindo ao ecrã de configuração, verifique **Olá, ignorar utilizando o Assistente de configuração de autenticação** e clique em **seguinte**.  Olá assistente for fechado e o servidor de Olá é iniciado.

   ![Nuvem](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Novamente na página de Olá que transferimos o servidor Olá, clique em Olá **gerar credenciais de ativação** botão. Copie estas informações para Olá servidor MFA do Azure nas caixas de Olá fornecida e clique em **ativar**.

## <a name="send-users-an-email"></a>Enviar uma mensagem de e-mail aos utilizadores

implementação de tooease, permitir que o servidor MFA toocommunicate com os seus utilizadores. Servidor MFA pode enviar um e-mail tooinform-los de que tenham sido inscritos para verificação de dois passos.

e-mail Olá que enviar deve ser determinado pelo como configurar os seus utilizadores para a verificação de dois passos. Por exemplo, se forem tooimport capaz de números de telefone do diretório da empresa Olá, o e-mail Olá deve incluir números de telefone Olá predefinido para que os utilizadores saibam que tooexpect. Se não importar números de telefone ou os utilizadores vão aplicação móvel do toouse Olá, enviar uma mensagem de e-mail que direciona-los toocomplete a inscrição de conta. Incluem um Portal de utilizador do Azure multi-factor Authentication de toohello hiperligação no e-mail de Olá.

conteúdo de Olá do e-mail Olá também varia consoante o método de Olá de verificação que foi definida para o utilizador Olá (chamada telefónica, SMS, aplicação móvel ou).  Por exemplo, se o utilizador de Olá toouse necessário um PIN quando fizer a autenticação, e-mail Olá indica que foi definido o PIN inicial para.  Os utilizadores é necessária toochange PIN durante a respetiva verificação primeiro.

### <a name="configure-email-and-email-templates"></a>Configurar o e-mail e modelos de e-mail

Clique em ícone de e-mail Olá no Olá tooset esquerdo definições Olá de envio destes e-mails. Esta página é onde pode introduzir informações de Olá SMTP do seu e-mail de servidor e envio de correio, verificando Olá **enviar e-mails toousers** caixa de verificação.

![Configuração do E-mail do Servidor MFA](./media/multi-factor-authentication-get-started-server/email1.png)

No separador conteúdo de correio eletrónico de Olá, pode ver os modelos de e-mail Olá que estão disponível toochoose do. Dependendo de como tiver configurado a verificação de dois passos tooperform utilizadores, escolha o modelo de Olá que melhor se adapta às.

![Modelos de E-mail do Servidor MFA](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Importar utilizadores do Active Directory

Agora que o servidor Olá está instalado quiser tooadd utilizadores. Pode escolher toocreate-los manualmente, importar utilizadores do Active Directory, ou configurar a sincronização automática com o Active Directory.

### <a name="manual-import-from-active-directory"></a>Importar manualmente do Active Directory

1. No servidor do MFA do Azure, de Olá Olá esquerda, selecione **utilizadores**.
2. Na parte inferior do Olá, selecione **importar do Active Directory**.
3. Agora pode optar por procurar para utilizadores individuais ou Olá pesquisa diretório AD UOs com utilizadores nas mesmas.  Neste caso, iremos especificar utilizadores Olá UO.
4. Realce todos os utilizadores Olá Olá direito e clique em **importação**.  Deverá receber um pop-up a indicar que a importação foi bem-sucedida.  Janela de importação de Olá fechar.

   ![Importação de utilizador do Servidor MFA](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Sincronização automatizada com o Active Directory

1. No servidor do MFA do Azure, de Olá Olá esquerda, selecione **integração de diretórios**.
2. Navegue toohello **sincronização** separador.
3. Na parte inferior do Olá, escolha **adicionar**
4. No Olá **Adicionar Item de sincronização** caixa que é apresentada a escolha Olá domínio, UO **ou** grupo de segurança, as definições, predefinições de método e predefinições de idioma para esta sincronização de tarefas e clique em **Adicionar**.
5. Caixa de Olá de verificação com etiqueta **ativar a sincronização com o Active Directory** e escolha um **intervalo de sincronização** entre um minuto e 24 horas.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Como hello do servidor multi-factor Authentication Azure gere dados de utilização

Quando utilizar Olá servidor multi-factor Authentication (MFA) no local, os dados de um utilizador são armazenados em servidores no local de Olá. Não existem dados de utilizador persistentes são armazenados na nuvem de Olá. Quando o utilizador de Olá efetua uma verificação de dois passos, Olá servidor MFA envia dados toohello verificação de Olá de tooperform de serviço em nuvem do MFA do Azure. Quando estes pedidos de autenticação são enviados toohello o serviço em nuvem, hello campos seguintes são enviados no pedido de Olá e registos para que fiquem disponíveis nos relatórios de autenticação/utilização do cliente Olá. Alguns dos campos de Olá são opcionais, pelo que podem ser ativados ou desativados no Olá servidor multi-factor Authentication. comunicações de Olá de Olá serviço em nuvem do servidor MFA toohello MFA utiliza SSL/TLS através da porta 443 de saída. Estes campos são:

* ID exclusivo - nome de utilizador ou ID interno do servidor MFA
* Nome próprio e apelido (opcional)
* Endereço de e-mail (opcional)
* Número de telefone - ao realizar uma chamada de voz ou autenticação por SMS
* Token do dispositivo - ao efetuar a autenticação da aplicação móvel
* Modo de autenticação
* Resultado da autenticação
* Nome do Servidor MFA
* IP do Servidor MFA
* Cliente IP - se disponível

Além disso toohello campos acima, o resultado da verificação de Olá (êxito/rejeição) e o motivo para quaisquer rejeições também é armazenado com dados de autenticação de Olá e disponível através de relatórios de autenticação/utilização Olá.

## <a name="back-up-and-restore-azure-mfa-server"></a>Criar cópias de segurança e restaurar o Servidor MFA do Azure

Certificar-se de que tem uma cópia de segurança boa é tootake um passo importante com qualquer sistema.

tooback se o servidor do MFA do Azure, certifique-se de que tem uma cópia de Olá **c:\Programas\Microsoft files\servidor multi-Factor Authentication Server\Data** pasta incluindo Olá **PhoneFactor.pfdata** ficheiro. 

No caso de um restauro é Olá concluída necessário os seguintes passos:

1. Reinstale o Servidor MFA do Azure num servidor novo.
2. Ativar Olá novo servidor MFA do Azure.
3. Parar Olá **MultiFactorAuth** serviço.
4. Substituir Olá **PhoneFactor.pfdata** com Olá efetuada a cópia de segurança.
5. Iniciar Olá **MultiFactorAuth** serviço.

novo servidor de Olá está agora a funcionar com Olá com cópia de segurança utilizador e a configuração de dados original.

## <a name="next-steps"></a>Passos seguintes

- Configurar Olá [Portal de utilizador](multi-factor-authentication-get-started-portal.md) de utilizador self-service.
- Configurar hello do servidor do MFA do Azure com [serviço de Federação do Active Directory](multi-factor-authentication-get-started-adfs.md), [autenticação RADIUS](multi-factor-authentication-get-started-server-radius.md), ou [autenticação LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Defina e configure o [Gateway de Ambiente de Trabalho Remoto e o Servidor Multi-Factor Authentication do Azure com o RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- [Implementar Olá Azure multi-factor Authentication Server Mobile serviço Web da aplicação](multi-factor-authentication-get-started-server-webservice.md).
- [Cenários avançados com Multi-Factor Authentication do Azure e VPNs de terceiros](multi-factor-authentication-advanced-vpn-configurations.md).
