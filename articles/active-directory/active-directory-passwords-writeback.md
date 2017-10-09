---
title: "Azure AD SSPR com repetição de escrita de palavras-passe | Microsoft Docs"
description: "Utilização do Azure AD e o Azure AD directory tooon local do Connect toowriteback palavras-passe"
services: active-directory
keywords: "Gestão de palavras-passe do Active Directory, gestão de palavras-passe, do Azure AD Self-repor a palavra-passe do serviço"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>Descrição geral de repetição de escrita de palavras-passe

Repetição de escrita de palavras-passe permite que palavras-passe do tooconfigure do Azure AD toowrite efetuar uma cópia tooyou no local do Active Directory. -Remove Olá necessidade tooset configurar e gerir uma solução de reposição de palavra-passe self-service complicada no local e fornece uma maneira conveniente baseado na nuvem para a sua tooreset utilizadores as respetivas palavras-passe no local onde quer que estejam. Repetição de escrita de palavras-passe é um componente do [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) que pode ser ativada e utilizado por subscritores atuais do Premium [edições do Azure Active Directory](active-directory-editions.md).

Repetição de escrita de palavras-passe fornece Olá seguintes funcionalidades

* **Zero atraso comentários** -repetição de escrita de palavras-passe é uma operação síncrona. Os utilizadores são notificados imediatamente se a palavra-passe não cumpria política ou foi toobe não é possível repor ou alterado por qualquer motivo.
* **Suporta a reposição de palavras-passe para utilizadores através do AD FS ou outras tecnologias de Federação** -com repetição de escrita de palavras-passe, desde que hello contas de utilizador federado são sincronizadas no seu inquilino do Azure AD, são toomanage capaz dos AD no local palavras-passe da nuvem Olá.
* **Suporta a reposição de palavras-passe para utilizadores que utilizam [sincronização de hash de palavra-passe](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  - quando o serviço de reposição de palavra-passe Olá Deteta que uma conta de utilizador sincronizadas esteja ativada para sincronização de hash de palavra-passe, repomos ambas esta conta no local e na nuvem palavra-passe em simultâneo.
* **Suporta a alteração de palavras-passe Olá aceder ao painel e o Office 365** - quando federado ou palavra-passe sincronizar utilizadores provenientes toochange as palavras-passe expiradas ou não expirou, iremos escrever esses ambiente de back-tooyour local AD as palavras-passe.
* **Olá, suporta ao escrever novamente as palavras-passe quando um administrador repor-los a partir do portal do Azure** - sempre que um administrador repõe a palavra-passe de um utilizador no Olá [portal do Azure](https://portal.azure.com), se estiver federado que o utilizador ou palavra-passe sincronizado, iremos definir Olá palavra-passe Olá, admin seleciona no seu AD local, bem. Isto não é atualmente suportado no Olá Portal de administração do Office.
* **Impõe no local políticas de palavra-passe do AD** - quando um utilizador repõe a palavra-passe, mas certifique-se de que cumpre no local política AD antes de consolidar esta toothat diretório. Isto inclui histórico, complexidade, idade, filtros de palavra-passe e outras restrições de palavra-passe que definiu no seu AD local.
* **Não requer quaisquer regras de firewall de entrada** -repetição de escrita de palavras-passe utiliza um reencaminhamento do Service Bus do Azure como um canal de comunicação subjacente, que significa que não tem tooopen nenhuma porta de entrada na sua firewall para toowork esta funcionalidade.
* **Não é suportada para contas de utilizador existem no âmbito de grupos protegidos no Active Directory no local** – para obter mais informações sobre grupos protegidos, consulte [protegidos contas e grupos no Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>Como funciona a repetição de escrita de palavras-passe

Quando um hash de palavra-passe ou federado sincronizadas utilizador vem tooreset ou alterar a palavra-passe na nuvem de Olá, ocorre a seguinte Olá:

1. Verificamos toosee tem o tipo de utilizador de Olá de palavra-passe.
    * Se detetarmos palavra-passe de Olá é gerida no local
        * Iremos verificar se hello repetição de escrita serviço está ativo e em execução, caso seja, permite ao utilizador Olá continuar
        * Se o serviço de repetição de escrita de Olá não está ativo, vamos informar o Olá utilizador que a palavra-passe não pode ser reposta agora
2. Em seguida, o utilizador de Olá transmite portas de autenticação adequado Olá e atinge Olá reposição de palavra-passe ecrã.
3. utilizador Olá seleciona uma nova palavra-passe e confirma-lo.
4. Após clicar em submeter, iremos encriptar palavra-passe de texto simples de Olá com uma chave simétrica que foi criada durante o processo de configuração de repetição de escrita de Olá.
5. Após a encriptação palavra-passe de Olá, iremos incluí-la num payload que é enviado através de um reencaminhamento de barramento do HTTPS canal tooyour service de inquilino específico (que também configuramos para si durante o processo de configuração de repetição de escrita de Olá). Este reencaminhamento está protegido por uma palavra-passe gerada aleatoriamente que sabe apenas a instalação no local.
6. Depois de mensagem de saudação atinge o barramento de serviço, hello ponto final de reposição de palavra-passe automaticamente reativado e vê que tem um pedido de reposição pendentes.
7. serviço de Olá, em seguida, procura utilizador Olá em questão utilizando o atributo de âncora Olá na nuvem. Para este toosucceed de pesquisa:

    * objeto de utilizador Olá tem de existir na Olá espaço de conector AD
    * objeto de utilizador Olá tem de ser ligado toohello correspondente de objeto de MV
    * objeto de utilizador Olá tem de ser ligado toohello objecto correspondente do conector AAD.
    * Olá ligação a partir do AD conector objeto tooMV tem de ter regras de sincronização de Olá `Microsoft.InfromADUserAccountEnabled.xxx` na ligação de Olá. <br> <br>
    Quando chamada Olá vêm nuvem de Olá, utiliza de motor de sincronização de Olá Olá cloudAnchor atributo toolook segurança de objeto de espaço de conector AAD Olá, segue-se o objeto de MV Olá ligação toohello back- e, em seguida, segue-se o objeto de back-toohello AD Olá ligação. Porque podem existir vários objetos do AD (multifloresta) para Olá mesmo utilizador, o motor de sincronização de Olá depende Olá `Microsoft.InfromADUserAccountEnabled.xxx` Olá toopick de ligação, corrija uma.

    > [!Note]
    > Como resultado esta lógica, o Azure AD Connect tem de ser capaz de toocommunicate com Olá emulador PDC para toowork de repetição de escrita de palavras-passe. Se precisar de tooenable neste manualmente, pode ligar o Azure AD Connect toohello emulador PDC clicando no Olá **propriedades** do conector de sincronização do Active Directory Olá, em seguida, selecionar **configurar as partições de diretório**. A partir daí, procure Olá **definições de ligação do controlador de domínio** secção e marque a caixa de Olá intitulada **utilizam apenas os controladores de domínio preferencial**. Mesmo se Olá preferencial que DC não é um emulador PDC, o Azure AD Connect tentará tooconnect toohello PDC para repetição de escrita de palavras-passe.

8. Assim que a conta de utilizador Olá for encontrada, tentarmos tooreset Olá palavra-passe diretamente floresta do AD adequada Olá.
9. Se a operação de definição de palavra-passe de Olá for bem sucedida, vamos informar o Olá utilizador que a palavra-passe foi alterada.
    > [!NOTE]
    > No caso de Olá quando a palavra-passe do utilizador Olá é sincronizado tooAzure AD utilizando a sincronização de palavra-passe, há a possibilidade de que a política de palavra-passe no local Olá é mais fraco de política de palavras-passe de nuvem Olá. Neste caso, iremos ainda impor qualquer política de no local Olá é e, em vez disso, Permitir palavra-passe hash sincronização toosynchronize Olá valor hash dessa palavra-passe. Isto garante que a política no local é imposta na nuvem de Olá, no matter se utilizar tooprovide ou federações de sincronização de palavra-passe único início de sessão.

10. Se a palavra-passe de Olá definida falha da operação, iremos devolver o utilizador do Olá erro toohello e dar-lhes tente novamente.
    * operação de Olá poderá falhar devido à seguinte Olá
        * o serviço de Olá foi pendente
        * palavra-passe de Olá que selecionou não cumpria as políticas da organização
        * Não foi possível localizar utilizador Olá no Olá local AD

    Temos um específico da mensagem para muitos nestes casos e informar o utilizador de Olá que eles podem fazer problema de Olá tooresolve.

## <a name="configuring-password-writeback"></a>Configurar a repetição de escrita de palavras-passe

Recomendamos que utilize a funcionalidade de atualização automática de Olá do [do Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) se quiser toouse repetição de escrita de palavras-passe.

O DirSync e o Azure AD Sync já não são um meio suportado de ativação do artigo de Olá de repetição de escrita de palavras-passe [atualizar do DirSync e Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) tem mais de informações toohelp com a transição.

Olá passos abaixo partem do princípio de que já tenha configurado o Azure AD Connect no seu ambiente utilizando Olá [Express](./connect/active-directory-aadconnect-get-started-express.md) ou [personalizada](./connect/active-directory-aadconnect-get-started-custom.md) definições.

1. repetição de escrita de palavras-passe do tooconfigure e ativar inicie sessão no servidor do tooyour do Azure AD Connect e inicie Olá **do Azure AD Connect** Assistente de configuração.
2. No ecrã de boas-vindas Olá clique **configurar**.
3. No Olá adicionais tarefas ecrã clique **personalizar as opções de sincronização** e, em seguida, escolha **seguinte**.
4. No ecrã de tooAzure AD Connect de Olá introduza uma credencial de Administrador Global e escolha **seguinte**.
5. Olá ligar os diretórios e o domínio em UO filtragem ecrãs pode escolher **seguinte**.
6. No ecrã de funcionalidades opcionais de Olá caixa de verificação Olá junto demasiado**repetição de escrita de palavras-passe** e clique em **seguinte**.
   ![Ativar a repetição de escrita de palavras-passe no Azure AD Connect][Writeback]
7. No ecrã de tooconfigure pronto Olá clique **configurar** e aguarde Olá toocomplete de processo.
8. Quando vir configuração concluída, pode clicar em **saída**

## <a name="licensing-requirements-for-password-writeback"></a>Requisitos de licenciamento para a repetição de escrita de palavras-passe

Para informações sobre o licenciamento, consulte o tópico de Olá [licenças necessárias para a repetição de escrita de palavras-passe](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) ou Olá seguintes sites

* [Site de preços do Active Directory do Azure](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Proteger a empresa produtiva](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Modos de autenticação suportados para a repetição de escrita de palavras-passe no local

Repetição de escrita de palavras-passe funciona para Olá tipos de palavra-passe de utilizador seguintes:

* **Os utilizadores apenas na nuvem**: repetição de escrita de palavras-passe não se aplica esta situação, porque não há nenhuma palavra-passe de no local
* **Os utilizadores sincronizados de palavra-passe**: repetição de escrita de palavras-passe suportada
* **Os utilizadores federados**: repetição de escrita de palavras-passe suportada
* **Os utilizadores de autenticação pass-through**: repetição de escrita de palavras-passe suportada

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Operações de utilizador e administrador suportadas para a repetição de escrita de palavras-passe

As palavras-passe são gravadas no Olá todas as seguintes situações:

* **Operações suportadas do utilizador final**
  * Operação de palavra-passe de alterar quaisquer voluntário pelo utilizador final de self-service
  * Nenhuma operação de palavra-passe de alteração de imposição self-service de utilizador final (por exemplo, a expiração de palavra-passe)
  * Qualquer utilizador final personalizada de palavra-passe repor provenientes de Olá [Portal de reposição de palavra-passe](https://passwordreset.microsoftonline.com)
* **Operações suportadas de administrador**
  * Operação de palavra-passe de alterar quaisquer voluntário administrador de self-service
  * Nenhuma operação de palavra-passe de alteração de imposição de self-service de administrador (por exemplo, a expiração de palavra-passe)
  * Qualquer administrador personalizada de palavra-passe repor provenientes de Olá [Portal de reposição de palavra-passe](https://passwordreset.microsoftonline.com)
  * Qualquer palavra-passe de utilizador final iniciadas pelo administrador de reposição de Olá [portal clássico do Azure](https://manage.windowsazure.com)
  * Qualquer palavra-passe de utilizador final iniciadas pelo administrador de reposição de Olá [portal do Azure](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Operações de utilizador e administrador não suportadas para a repetição de escrita de palavras-passe

Palavras-passe são **não** escritos novamente em qualquer um dos Olá seguintes situações:

* **Operações do utilizador final não suportadas**
  * Qualquer utilizador final repor os seus próprios palavra-passe utilizando o PowerShell v1, v2 ou Olá AD Graph API do Azure
* **Operações de administrador não suportadas**
  * Qualquer palavra-passe de utilizador final iniciadas pelo administrador de reposição de Olá [portal de gestão do Office](https://portal.office.com)
  * Qualquer palavra-passe do utilizador final iniciadas pelo administrador repor PowerShell v1, v2, ou Olá AD Graph API do Azure

Enquanto que estamos a trabalhar tooremove estas limitações, não temos uma linha de tempo específica que partilhamos ainda.

## <a name="password-writeback-security-model"></a>Modelo de segurança de repetição de escrita de palavras-passe

Repetição de escrita de palavras-passe é um serviço altamente seguro.  tooensure que as suas informações estão protegidas, ativamos a um modelo de segurança de 4 camadas que é descrito abaixo.

* **Reencaminhamento de barramento de serviço de inquilino específico**
  * Quando configurar o serviço de Olá, iremos definir um reencaminhamento de barramento de serviço de inquilino específico que está protegido por uma gerado aleatoriamente palavra-passe segura que Microsoft nunca tenha acesso à.
* **Chave de encriptação da palavra-passe bloqueado para baixo e criptograficamente forte,**
  * Depois de criado o reencaminhamento de barramento de serviço Olá, criamos uma chave simétrica forte, utilizamos a palavra-passe do tooencrypt Olá conforme for necessário durante a transmissão Olá. Esta chave se encontra apenas no arquivo de secreta da sua empresa numa nuvem Olá, que é fortemente bloqueado e auditado, tal como qualquer palavra-passe no diretório de Olá.
* **TLS padrão da indústria**
  1. Quando uma palavra-passe reponham ou alterem operação ocorre na nuvem de Olá, iremos assumir a palavra-passe de texto simples de Olá e encriptá-lo com a chave pública.
  2. Vamos, em seguida, coloque que numa mensagem de HTTPS, que é enviada através de um canal encriptado utilizando o reencaminhamento de bus de serviço de tooyour certificados SSL da Microsoft.
  3. Depois de mensagem de saudação chega para o Service Bus, o agente no local sair cópias de segurança e efetua a autenticação através do barramento de tooService Olá palavra-passe segura gerada anteriormente.
  4. Agente local escolherá a mensagem de saudação encriptados, desencripta-la utilizando a chave privada Olá que são gerados.
  5. Agente no local, em seguida, tenta palavra-passe de Olá de tooset através de Olá AD DS SetPassword API.
     * Este passo é o que nos permite tooenforce do AD no local política de palavras-passe (complexidade, idade, histórico, filtros, etc.) na nuvem de Olá.
* **Políticas de expiração da mensagem** 
  * Se a mensagem de saudação encontra-se no Service Bus porque o serviço no local não está disponível, será de tempo e ser removida após a segurança de tooincrease do minutos várias ainda mais.

### <a name="password-writeback-encryption-details"></a>Detalhes de encriptação de repetição de escrita de palavras-passe

passos de encriptação de Olá um pedido de reposição de palavra-passe atravessa depois de um utilizador submete, antes que chega no seu ambiente no local, a fiabilidade de serviço máximo tooensure e a segurança são descritos abaixo.

* **Passo 1 - encriptação da palavra-passe com chave RSA de 2048 bits** - depois de um utilizador submete um toobe de palavra-passe gravado tooon local, primeiro, Olá submetido palavra-passe em si é encriptado com uma chave RSA de 2048 bits.
* **Passo 2 - encriptação a nível do pacote com o AES GCM** -, em seguida, o pacote completo de Olá (palavra-passe + metadados necessários) é encriptado com AES-GCM. Isto impede que qualquer pessoa com canal de ServiceBus subjacente do acesso direto toohello visualização/adulteração com conteúdo Olá.
* **Passo 3 - todas as comunicações ocorre através de TLS / SSL** -todas as comunicações de Olá com ServiceBus ocorre um canal SSL/TLS. Protege os conteúdos de Olá de partes 3rd não autorizadas.
* **Rollover de chave automático a cada seis meses** - automaticamente cada 6 meses, ou sempre que a repetição de escrita de palavras-passe está desativada / reativada no Azure AD Connect, iremos rollover todas estas chaves tooensure máxima do serviço e de segurança segurança.

### <a name="password-writeback-bandwidth-usage"></a>Utilização de largura de banda de repetição de escrita de palavras-passe

Repetição de escrita de palavras-passe é um serviço de pouca largura de banda que envia pedidos de fazer uma cópia de agente no local de toohello apenas em Olá seguintes circunstâncias:

1. Duas mensagens enviadas quando ativar ou desativar a funcionalidade de Olá através do Azure AD Connect.
2. Uma mensagem é enviada uma vez a cada cinco minutos como um heartbeat do serviço para, desde que o serviço de Olá está em execução.
3. Duas mensagens são enviadas a cada hora, uma nova palavra-passe é submetida
    * Primeira mensagem, como uma operação do pedido tooperform Olá
    * Segunda mensagem, que contém o resultado de Olá da operação de Olá e é enviada no Olá seguintes circunstâncias:
        * Sempre que uma nova palavra-passe é submetida durante uma reposição de palavra-passe self-service do utilizador.
        * Sempre que uma nova palavra-passe é submetida durante uma operação de alteração de palavra-passe do utilizador.
        * Sempre que uma nova palavra-passe é submetida durante uma palavra-passe de utilizador iniciadas pelo administrador de reposição (a partir de Olá administrador do Azure portais apenas).

#### <a name="message-size-and-bandwidth-considerations"></a>Considerações de largura de banda e o tamanho da mensagem

o tamanho de cada mensagem de saudação descrita acima Olá normalmente em 1 kb, mesmo sob cargas pesadas Alpine, serviço de repetição de escrita de palavras-passe Olá propriamente dito está a consumir alguns kilobits por segundo de largura de banda. Uma vez que cada mensagem é enviada em tempo real, apenas quando uma operação de atualização de palavra-passe e, uma vez que o tamanho da mensagem Olá, por isso, pequeno, utilização de largura de banda de Olá da capacidade de repetição de escrita de Olá eficazmente é demasiado pequena toohave qualquer impacto real significativo.

## <a name="next-steps"></a>Passos seguintes

Olá seguintes ligações fornece informações adicionais sobre a utilizar o Azure AD de reposição de palavra-passe

* [**Guia de Introdução** ](active-directory-passwords-getting-started.md) - Começar a trabalhar com a gestão de palavras-passe self-service do Azure AD 
* [**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing (Licenciamento - Configurar o Licenciamento do Azure AD)
* [**Dados** ](active-directory-passwords-data.md) - compreender Olá dados que é necessários e como são utilizadas para a gestão de palavra-passe
* [**Implementação** ](active-directory-passwords-best-practices.md) -planear e implementar os utilizadores de tooyour SSPR utilizando a orientação de Olá encontrada aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aspeto e funcionalidade de Olá SSPR experiência da sua empresa.
* [**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies (Política - Compreender e definir políticas de palavras-passe do Azure AD)
* [**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality (Relatórios - Descubra se, quando e a partir de onde é que os utilizadores acedem à funcionalidade SSPR)
* [**Descrição detalhada da Technical** ](active-directory-passwords-how-it-works.md) -voltar atrás Olá curtain toounderstand como funciona
* [**Frequently Asked Questions**](active-directory-passwords-faq.md) - How? Porquê? What? Where? Who? When? -Atender tooquestions sempre pretendia tooask
* [**Resolver problemas** ](active-directory-passwords-troubleshoot.md) -Saiba como tooresolve comuns problemas que vemos com SSPR

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Ativar a repetição de escrita de palavras-passe no Azure AD Connect"
