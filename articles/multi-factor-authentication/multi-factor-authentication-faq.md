---
title: aaaAzure multi-factor Authentication FAQ | Microsoft Docs
description: "Perguntas mais frequentes e respostas relacionados tooAzure multi-factor Authentication. Autenticação Multifator é um método de verificar a identidade de um utilizador que precisa de mais do que um nome de utilizador e palavra-passe. Fornece uma camada adicional de segurança toouser início de sessão e transações."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Perguntas mais frequentes sobre o multi-factor Authentication do Azure
Estas FAQ responde a questões recorrentes sobre o multi-factor Authentication do Azure e utilizar o serviço de multi-factor Authentication Olá. Este é dividido em perguntas sobre o serviço de Olá em geral, modelos, experiências de utilizador, de faturação e resolução de problemas.

## <a name="general"></a>Geral
**P: como é que o servidor do Azure multi-factor Authentication processar dados de utilizador?**

Com o servidor do multi-factor Authentication, os dados de utilizador são armazenados apenas em servidores no local de Olá. Não existem dados de utilizador persistentes são armazenados na nuvem de Olá. Quando o utilizador Olá efetua a verificação de dois passos, o servidor multi-factor Authentication envia dados toohello serviço de nuvem do Azure multi-factor Authentication para autenticação. A comunicação entre o servidor multi-factor Authentication e Olá serviço em nuvem de multi-factor Authentication utiliza Secure Sockets Layer (SSL) ou Transport Layer Security (TLS) através da porta 443 de saída.

Quando os pedidos de autenticação são enviados toohello o serviço em nuvem, os dados são recolhidos para a autenticação e a utilização de relatórios. Os campos de dados incluídos nos registos de verificação de dois passos são os seguintes:

* **ID exclusivo** (o nome ou no local multi-factor Authentication Server ID de utilizador)
* **Primeiro e último nome** (opcional)
* **Endereço de correio eletrónico** (opcional)
* **Número de telefone** (ao utilizar uma chamada de voz ou autenticação por SMS)
* **Token do dispositivo** (ao utilizar a autenticação da aplicação móvel)
* **Modo de autenticação**
* **Resultado da autenticação**
* **Nome do servidor multi-factor Authentication**
* **Servidor multi-factor Authentication IP**
* **Cliente IP** (se disponível)

campos opcionais Olá podem ser configurados no servidor multi-factor Authentication.

Olá, resultados de verificação (êxito ou recusa) e hello razão se foi negado, é armazenada com dados de autenticação de Olá. Estes dados ficarem disponíveis nos relatórios de utilização e de autenticação.

## <a name="billing"></a>Faturação
Perguntas sobre faturação a maioria das pode ser respondido por referência tooeither Olá [página de preços do multi-factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) ou Olá documentação sobre [como tooget Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md).

**P: é a minha organização cobrada para enviar mensagens de texto que são utilizadas para autenticação e as chamadas telefónicas de Olá?**

Não, não lhe serem cobrados para individuais chamadas telefónicas colocadas ou mensagens de texto enviada toousers através do Azure multi-factor Authentication. Se utilizar um fornecedor MFA por autenticação, é-lhe faturado para cada autenticação, mas não para o método Olá utilizado.

Os utilizadores poderão cobrados Olá chamadas de telefone ou as mensagens de texto recebem, de acordo com serviço de telefone pessoal tootheir.

**P: o modelo de faturação do Olá por utilizador cobram que me são ativados todos os utilizadores ou Olá apenas aqueles que efetuar a verificação de dois passos?**

Faturação é baseada no número de Olá dos utilizadores configurados toouse multi-factor Authentication, independentemente de se poderem efetuar verificação de dois passos desse mês.

**P: como funciona a faturação do multi-factor Authentication?**

Quando criar um fornecedor MFA por utilizador ou por autenticação, a subscrição do Azure da sua organização é faturada mensalmente com base na utilização. Este modelo de faturação é semelhante faturas toohow do Azure para a utilização de máquinas virtuais e os Web sites.

Ao adquirir uma subscrição do Azure multi-factor Authentication, organização pays apenas uma taxa de licença anuais Olá para cada utilizador. Licenças MFA e do Office 365, Azure AD Premium, ou Enterprise Mobility + os pacotes de segurança são faturados desta forma. 

Saiba mais sobre as suas opções em [como tooget Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md).

**P: existe uma versão gratuita do Azure multi-factor Authentication?**

Em alguns casos, Sim.

Autenticação Multifator para os administradores do Azure oferece um subconjunto das funcionalidades de MFA do Azure sem custos de acesso tooMicrosoft online services, incluindo os portais de administrador do Azure e o Office 365 Olá. Esta oferta aplica-se apenas os administradores de tooglobal nas instâncias do Azure Active Directory que não tem Olá versão completa do MFA do Azure através de uma licença do MFA, um pacote ou um fornecedor de autónomo com base no consumo. Se os seus administradores de utilizam a versão gratuita Olá e, em seguida, comprar uma versão completa do MFA do Azure, em seguida, todos os administradores globais são elevado toohello paga versão automaticamente.

Autenticação Multifator para utilizadores do Office 365 oferece um subconjunto das funcionalidades de MFA do Azure sem custos de acesso tooOffice 365 serviços, incluindo o Exchange Online e SharePoint Online. Esta oferta aplica-se toousers que tem uma licença do Office 365 atribuída, quando a instância correspondente da Olá do Azure Active Directory não tem Olá versão completa do MFA do Azure através de uma licença do MFA, um pacote ou um fornecedor de autónomo com base no consumo.

**P: pode mudar a minha organização entre por utilizador e por autenticação modelos de faturação consumo em qualquer altura?**

Se a sua organização comprar o MFA como um serviço autónomo com faturação baseada no consumo, escolha um modelo de faturação quando criar um fornecedor de MFA. Não é possível alterar o modelo de faturação Olá depois de criar um fornecedor de MFA. No entanto, pode eliminar o fornecedor de MFA Olá e, em seguida, criar uma com um modelo de faturação diferente.

Quando é criado um fornecedor de MFA, pode ser ligado tooan Azure Active Directory (também conhecido como "inquilino do Azure AD"). Se hello atual fornecedor de MFA inquilino tooan ligado do Azure AD, com segurança pode eliminar o fornecedor de MFA Olá e criar um que seja ligado toohello mesmo Azure AD inquilino. Em alternativa, se tiver adquirido suficiente MFA, Azure AD Premium, ou Enterprise Mobility + toocover de licenças de segurança (EMS) todos os utilizadores que estão ativados para a MFA, é possível eliminar o fornecedor de MFA Olá completamente.

Se for o fornecedor MFA *não* inquilino tooan ligado do Azure AD ou ligação Olá novo MFA fornecedor tooa diferente do Azure AD inquilino, opções de configuração e definições do utilizador não são transferidas. Além disso, existentes de servidores MFA do Azure tem toobe reativado com as credenciais de ativação geradas através de Olá novo fornecedor de MFA. Deve ser reactivado Olá MFA servidores toolink-los toohello novo fornecedor de MFA não tem impacto chamada telefónica e autenticação de mensagem de texto, mas a aplicação móvel notificações deixa de funcionar para todos os utilizadores até que o se reativar Olá de aplicação móvel.

Saiba mais sobre os fornecedores MFA no [introdução de um fornecedor do Azure multi-factor Auth](multi-factor-authentication-get-started-auth-provider.md).

**P: a minha organização alternar entre com base no consumo de faturação e subscrições (um modelo baseado em licenças) em qualquer altura?**

Em alguns casos, Sim.

Se tiver o seu diretório um *por utilizador* fornecedor do multi-factor Authentication do Azure, pode adicionar licenças MFA. Os utilizadores com licenças não são contabilizadas no baseada no consumo faturação por utilizador Olá. Os utilizadores sem licenças ainda podem ser ativados para a MFA através do fornecedor de MFA Olá. Se comprar e atribuir licenças para todos os utilizadores configurados toouse multi-factor Authentication, pode eliminar o fornecedor de multi-factor Authentication do Azure Olá. Pode criar sempre outro fornecedor MFA por utilizador se tiver mais utilizadores a licenças de Olá futura.

Se tiver o seu diretório um *por autenticação* fornecedor do multi-factor Authentication do Azure, é sempre faturado por cada autenticação, desde que o fornecedor de MFA Olá é ligado tooyour subscrição. Pode atribuir toousers de licenças MFA, mas irá ainda ser-lhe faturado para cada pedido de verificação de dois passos, se se trata de outra pessoa com uma licença do MFA atribuída ou não.

**P: a minha organização tiver toouse e sincronizar identidades toouse multi-factor Authentication do Azure?**

Se a organização utilizar um modelo de faturação baseada no consumo, o Azure Active Directory é opcional, mas não é necessária. Se o fornecedor MFA não estiver ligado tooan inquilino do Azure AD, só é possível implementar servidor do Azure multi-factor Authentication ou Olá SDK do multi-factor Authentication do Azure no local.

Azure Active Directory é necessário para o modelo de licença de Olá porque licenças são adicionadas inquilino do Azure AD toohello quando comprar e atribuir-lhes toousers no diretório de Olá.

## <a name="manage-and-support-user-accounts"></a>Gerir e suportam contas de utilizador

**P: o que devo dizer toodo os meus utilizadores se estes não recebem uma resposta no seu telefone ou não tem o telefone com os mesmos?**

Hopefully todos os seus utilizadores configurado mais do que um método de verificação. Informe-tootry voltar a iniciar sessão, mas selecionar um método de verificação diferente na página de início de sessão Olá.

Pode apontar o toohello utilizadores [guia de resolução de problemas do utilizador final](./end-user/multi-factor-authentication-end-user-troubleshoot.md).


**P: o que posso fazer se um dos meus utilizadores não é possível obter tootheir conta?**

Pode repor a conta de utilizador de Olá fazendo-los toogo durante o processo de registo de Olá novamente. Saiba mais sobre [gerir definições de utilizadores e dispositivos com o Azure multi-factor Authentication na nuvem de Olá](multi-factor-authentication-manage-users-and-devices.md).

**P: o que devo fazer se perder um dos meus utilizadores um telefone que está a utilizar palavras-passe de aplicação?**

tooprevent não autorizado acesso, eliminar as de palavras-passe do utilizador Olá todas as aplicações. Depois do utilizador Olá tem um dispositivo de substituição, que podem recriam palavras-passe de Olá. Saiba mais sobre [gerir definições de utilizadores e dispositivos com o Azure multi-factor Authentication na nuvem de Olá](multi-factor-authentication-manage-users-and-devices.md).

**P: E se um utilizador não é possível iniciar sessão em aplicações de toonon browser?**

Se a organização ainda utilizar clientes legados e [permitida a utilização de Olá de palavras-passe de aplicação](multi-factor-authentication-whats-next.md#app-passwords), em seguida, os utilizadores não é possível iniciar sessão em clientes legados de toothese com o respetivo nome de utilizador e palavra-passe. Em vez disso, precisam de demasiado[configurar palavras-passe de aplicação](./end-user/multi-factor-authentication-end-user-app-passwords.md). Os utilizadores tem de limpar (delete) as suas informações de início de sessão, reiniciar a aplicação Olá e, em seguida, inicie sessão com o nome de utilizador e *palavra-passe de aplicação* em vez da palavra-passe normal.

Se a sua organização não tiver clientes legados, deve não permitir que os utilizadores toocreate palavras-passe de aplicação.

> [!NOTE]
> Autenticação moderna para clientes do Office 2013
>
> As palavras-passe de aplicação só são necessárias para as aplicações que não suportem a autenticação moderna. Os clientes do Office 2013 suportam os protocolos de autenticação moderna, mas necessita toobe configurado. Clientes mais recentes do Office suportam automaticamente os protocolos de autenticação moderna. Para obter mais informações, consulte Olá [anúncio de pré-visualização pública de autenticação moderna do Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

**P: os meus utilizadores dizem que por vezes, não recebem mensagem de texto hello, ou responder a mensagens de texto de forma tootwo mas verificação Olá exceder o tempo limite.**

Não é garantido que entrega de mensagens de texto e a receção de respostas na SMS bidirecional porque existem uncontrollable fatores que podem afetar a fiabilidade de Olá do serviço de Olá. Estes fatores incluem país de destino Olá, operadora de telemóvel Olá e força de sinal Olá.

Se os utilizadores têm, muitas vezes, problemas com a receção de forma fiável as mensagens de texto, informe-toouse Olá móvel aplicação ou chamada telefónica método em vez disso. aplicação móvel Olá pode receber notificações tanto através de ligações Wi-Fi e de rede móvel. Além disso, aplicação móvel Olá pode gerar códigos de verificação, mesmo quando o dispositivo de Olá tem sem sinal de todo. aplicação do Microsoft Authenticator Olá está disponível para [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), e [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).

Se tiver de utilizar as mensagens de texto, recomendamos que utilize o SMS unidirecional em vez de SMS bidirecional sempre que possível. SMS unidirecional é mais fiável e impede que os utilizadores incorrer em custos SMS global da parte das mensagem de texto tooa foi enviada a partir de outro país.

**P: Posso alterar Olá período de tempo que os meus utilizadores têm o código de verificação de Olá tooenter partir de uma mensagem de texto, antes do sistema de Olá exceder o tempo limite?**

Em alguns casos, Sim. 

Para SMS unidirecional com o servidor MFA do Azure v-7.0 ou superior, pode configurar o tempo limite de Olá por definição uma chave de registo. Depois de Olá serviço de nuvem MFA envia a mensagem de texto Olá, código de verificação Olá (ou o código de acesso Monouso), é devolvido toohello servidor MFA. Olá servidor MFA armazena o código de Olá na memória para 300 segundos por predefinição. Se o utilizador Olá não introduza o código de Olá antes Olá passaram 300 segundos, a autenticação é negada. Utilize estes passos toochange Olá tempo limite predefinido definição:

1. Aceda tooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor.
2. Crie uma chave de registo DWORD denominada **pfsvc_pendingSmsTimeoutSeconds** e definir a hora de Olá em segundos que pretende que o Olá servidor MFA do Azure toostore Monouso códigos de acesso.

>[!TIP] 
>Se tiver vários servidores de MFA, apenas os Olá que processou o pedido de autenticação original Olá sabe o código de verificação de Olá que lhe foi enviado toohello utilizador. Quando o utilizador Olá introduzir o código de Olá, Olá toovalidate de pedido de autenticação, tem de ser enviados toohello mesmo servidor. Se a validação do código Olá é enviada tooa outro servidor, a autenticação de Olá é negada. 

Para SMS bidirecional com o servidor MFA do Azure, pode configurar a definição de tempo limite de Olá no Olá Portal de gestão MFA. Se os utilizadores não responder toohello SMS dentro do período de tempo limite definido de Olá, a autenticação é negada. 

Para obter SMS unidirecional com a Azure MFA na nuvem de Olá (incluindo Olá extensão de servidor de políticas de rede do adaptador ou Olá do AD FS), não é possível configurar a definição de tempo limite de Olá. Azure AD armazena o código de verificação Olá durante 180 segundos. 

**P: Posso utilizar tokens de hardware com o servidor do Azure multi-factor Authentication?**

Se estiver a utilizar o servidor do Azure multi-factor Authentication, pode importar tokens de baseados no tempo, uma única palavra-passe (TOTP) de autenticação aberta (OATH) de terceiros e, em seguida, utilizá-los para a verificação de dois passos.

Pode utilizar ActiveIdentity tokens que são tokens OATH TOTP se colocar a chave secreta Olá num ficheiro CSV e importar tooAzure servidor multi-factor Authentication. Pode utilizar OATH tokens com serviços de Federação do Active Directory (ADFS), autenticação baseada em formulários do servidor de informação Internet (IIS) e RADIUS Remote Authentication Dial-In User Service (), desde que o sistema de cliente Olá pode aceitar Olá intervenção do utilizador.

Pode importar tokens OATH TOTP de terceiros com Olá seguintes formatos:  

- Contentor de chave simétrico (PSKC) portátil  
- Se o ficheiro de Olá contém um número de série, uma chave secreta no formato de Base 32 e um intervalo de tempo CSV  

**P: Posso utilizar serviços de Terminal do servidor do Azure multi-factor Authentication toosecure?**

Sim, mas se estiver a utilizar o Windows Server 2012 R2 ou posterior só pode proteger os serviços de Terminal utilizando o Gateway de ambiente de trabalho remoto (Gateway de RD).

Alterações de segurança no Windows Server 2012 R2 alterar como o servidor do Azure multi-factor Authentication liga toohello pacote de segurança de autoridade de segurança Local (LSA) no Windows Server 2012 e versões anteriores. Para as versões dos serviços de Terminal no Windows Server 2012 ou anterior, pode [proteger uma aplicação com a autenticação do Windows](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure). Se estiver a utilizar o Windows Server 2012 R2, tem de Gateway de RD.

**P: Posso configurado o ID do autor da chamada no servidor MFA, mas os meus utilizadores continuar a receber chamadas de multi-factor Authentication de um emissor anónimo.**

Quando são colocadas chamadas de multi-factor Authentication através de rede de telefone pública Olá, por vezes, estes são encaminhados através de uma operadora que não suporta o ID do autor da chamada. Por este motivo, ID do autor da chamada não é garantido, apesar de Olá sistema de multi-factor Authentication sempre envia-a.

**P: por que razão são os meus utilizadores que está a ser pedido tooregister as suas informações de segurança?**
Existem vários motivos para que os utilizadores pode ser pedido tooregister as suas informações de segurança:

- utilizador Olá foi ativada para o MFA pelo seu administrador no Azure AD, mas não tem informações de segurança ainda registadas para a respetiva conta.
- utilizador Olá foi ativada para o self-service reposição palavra-passe no Azure AD. as informações de segurança de Olá irão ajudá-lo a repor a palavra-passe no Olá futura se se esquecer da-lo.
- Olá utilizador acedeu a uma aplicação que tenha um toorequire de política de acesso condicional MFA e ainda não registada para a MFA.
- utilizador Olá é registar um dispositivo com o Azure AD (incluindo a associação do Azure AD) e organização exige a MFA para registo de dispositivos, mas não utilizador Olá anteriormente registado para MFA.
- utilizador Olá está a gerar o Windows Hello para empresas no Windows 10 (o que necessita de MFA) e não registada para a MFA.
- organização Olá tem de criar e ativar a uma política de registo do MFA que foi aplicada toohello utilizador.
- utilizador Olá anteriormente registado para MFA, mas escolher um método de verificação que desativada uma vez que um administrador. utilizador Olá, por conseguinte, tem de aceder através do registo do MFA novamente tooselect um novo método de verificação de predefinição.


## <a name="errors"></a>Erros
**P: o que devem fazer os utilizadores se veem uma mensagem de erro "o pedido de autenticação não é para uma conta ativada" quando utilizar notificações de aplicação móvel?**

Informe-toofollow tooremove este procedimento conta a partir da aplicação móvel Olá, em seguida, adicioná-lo novamente:

1. Aceda demasiado[o perfil de portal do Azure](https://account.activedirectory.windowsazure.com/profile/) e inicie sessão com a sua conta organizacional.
2. Selecione **verificação adicional de segurança**.
3. Remova a conta existente Olá da aplicação móvel Olá.
4. Clique em **configurar**e, em seguida, siga a aplicação móvel do Olá instruções tooreconfigure Olá.

**P: o que devem fazer os utilizadores se veem uma mensagem de erro de 0x800434D4L quando iniciar sessão em aplicações não baseadas no browser de tooa?**

Erro de 0x800434D4L Olá ocorre quando tenta toosign na aplicação de browser não tooa, instalada num computador local, que não funciona com contas que necessitem de verificação em dois passos.

Uma solução para este erro é a contas de utilizador em separado toohave para relacionadas com administração e as operações de não administrador. Mais tarde, pode ligar caixas de correio entre a sua conta de administrador e a conta não administrativa, de modo a que pode iniciar sessão tooOutlook utilizando a sua conta não administrativa. Para obter mais detalhes sobre esta solução, saiba como demasiado[dar um Olá administrador capacidade tooopen vista Olá dos conteúdos e da caixa de correio de um utilizador](http://help.outlook.com/141/gg709759.aspx?sl=1).

## <a name="next-steps"></a>Passos seguintes
Se a sua pergunta não é atendida aqui, deixe-nos comentários de Olá em Olá parte inferior da página Olá. Em alternativa, aqui estão algumas opções adicionais para obter ajuda:

* Olá pesquisa [Base de dados de conhecimento de suporte do Microsoft](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) para problemas técnicos do toocommon soluções.
* Procurar e navegue até a técnicas perguntas e respostas da Comunidade Olá ou fazer a suas próprias pergunta nos Olá [fóruns do Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).
* Se tiver um cliente legado do PhoneFactor e tiver dúvidas ou precisar de ajuda para repor uma palavra-passe, utilize Olá [reposição de palavra-passe](mailto:phonefactorsupport@microsoft.com) ligação tooopen um incidente de suporte.
* Contactar um profissional de suporte através de [suporte de servidor do Azure multi-factor Authentication (PhoneFactor)](https://support.microsoft.com/oas/default.aspx?prid=14947). Quando contactar-nos, é útil se pode incluir a maior quantidade informações sobre o problema quanto possível. Pode fornecer as informações incluem a página olá onde vimos erro Olá, código de erro específico Olá, ID de sessão específicos de Olá e Olá ID de utilizador de Olá que vimos erro Olá.
