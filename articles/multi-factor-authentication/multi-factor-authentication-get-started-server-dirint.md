---
title: "aaaDirectory integração entre o Azure multi-factor Authentication e o Active Directory"
description: "Esta é a página de autenticação do Olá multi-factor do Azure que descreve como toointegrate Olá Azure multi-factor Authentication Server com o Active Directory para que possa sincronizar os diretórios de Olá."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Integração de diretórios entre o Servidor MFA do Azure e o Active Directory
Utilize a secção Integração de diretórios Olá Olá toointegrate de servidor MFA do Azure com o Active Directory ou outro diretório LDAP. Pode configurar o esquema de diretório do atributos toomatch Olá e configurar a sincronização automática do utilizador.

## <a name="settings"></a>Definições
Por predefinição, hello do servidor multi-factor Authentication (MFA) do Azure está configurado tooimport ou sincronizar utilizadores do Active Directory.  separador de integração de diretórios de Olá permite-lhe toooverride Olá comportamento predefinido e toobind tooa outro diretório LDAP, um diretório ADAM ou controlador de domínio do Active Directory específico.  Também fornece Olá utilização da autenticação LDAP tooproxy LDAP ou enlace de LDAP como destino RADIUS, pré-autenticação para autenticação do IIS ou autenticação primária no Portal de utilizador.  Olá, a tabela seguinte descreve as definições individuais Olá.

![Definições](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| Funcionalidade | Descrição |
| --- | --- |
| Utilizar o Active Directory |Selecione Olá Use Active Directory opção toouse do Active Directory para importação e sincronização.  Esta é a predefinição de Olá. <br>Nota: Para o Active Directory integração toowork corretamente, associar o domínio de tooa Olá computador e inicie sessão com uma conta de domínio. |
| Incluir domínios fidedignos |Verifique **incluir domínios fidedignos** toohave Olá agente tentativa tooconnect toodomains considerado fidedigno pelo Olá domínio atual, outro domínio na floresta hello ou domínios envolvidos numa confiança de floresta.  Quando não importar nem sincronizar utilizadores de qualquer Olá fidedigno domínios, desmarque o desempenho de tooimprove Olá caixa de verificação.  Olá predefinição é marcada. |
| Utilizar configuração de LDAP específica |Selecione Olá utilizar LDAP opção toouse Olá definições de LDAP especificadas para importação e sincronização. Nota: Quando está selecionado utilizar LDAP, interface de utilizador Olá altera as referências de tooLDAP do Active Directory. |
| Botão Editar |botão para editar Olá permite toomodified de definições de configuração Olá atual LDAP. |
| Utilizar consultas de âmbito de atributos |Indica se devem ser utilizadas consultas de âmbito de atributos.  Consultas de âmbito de atributo permitem obter registos com base no Olá as entradas no atributo de outro registo qualificativos de procuras em diretórios eficientes.  Hello do servidor multi-factor Authentication Azure utiliza o atributo âmbito consultas tooefficiently Olá os utilizadores da consulta que sejam membros de um grupo de segurança.   <br>Nota: existem alguns casos em que as consultas de âmbito de atributos são suportadas, mas não devem ser utilizadas.  Por exemplo, o Active Directory pode ter problemas com as consultas de âmbito de atributos quando um grupo de segurança contém membros de mais de um domínio. Neste caso, anule a seleção Olá caixa de verificação. |

Olá, a tabela seguinte descreve as definições de configuração de LDAP Olá.

| Funcionalidade | Descrição |
| --- | --- |
| Servidor |Introduza Olá nome de anfitrião ou endereço IP do servidor de Olá com o diretório LDAP Olá.  Também pode ser especificado um servidor de cópia de segurança, separado por ponto e vírgula. <br>Nota: quando o Tipo de Enlace é SSL, é preciso um nome de anfitrião totalmente qualificado. |
| DN Base |Introduza Olá nome único do objeto de diretório base Olá partir do qual iniciar todas as consultas de diretório.  Por exemplo, dc=abc,dc=com. |
| Tipo de enlace - Consultas |Selecione o tipo de enlace adequado Olá para utilização quando se vincula o diretório LDAP toosearch Olá.  Este serve para importações, sincronização e resolução de nomes de utilizador. <br><br>  Anónimo - é feito um enlace anónimo.  DN do Enlace e Palavra-passe do Enlace não são utilizados.  Isto só funciona se o diretório LDAP Olá permite enlace anónimo e as permissões permitirem Olá consulta dos Olá registos e atributos adequados.  <br><br> Simples - enlace DN e enlace palavra-passe são transmitidos como texto simples toobind diretório LDAP toohello.  Trata-se para fins de teste, pode ser contactado tooverify hello do servidor e essa conta de enlace de Olá possui acesso adequado de Olá. Após a instalação do certificado adequado Olá, em vez disso, a utilizar o SSL.  <br><br> SSL - enlace DN e enlace palavra-passe são encriptados com SSL toobind toohello LDAP directory.  Instale localmente um certificado que Olá confianças de diretório LDAP.  <br><br> Windows - enlace nome de utilizador e enlace palavra-passe são utilizado toosecurely ligar controlador de domínio do Active Directory tooan ou diretório ADAM.  Se enlace nome de utilizador for deixado em branco, Olá com sessão iniciada da conta de utilizador é toobind utilizado. |
| Tipo de enlace - Autenticações |Selecione o tipo de enlace adequado Olá para utilizar quando efetuar a autenticação do enlace LDAP.  Consulte as descrições de tipo de enlace Olá em tipo de enlace - consultas.  Por exemplo, isto permite toobe enlace anónimo utilizada para consultas enquanto o enlace SSL é as autenticações de enlace LDAP toosecure utilizados. |
| DN do Enlace ou Nome de utilizador do enlace |Introduza o nome distinto Olá do registo de utilizador Olá para Olá conta toouse quando se vincula toohello diretório LDAP.<br><br>nome único do enlace Olá só é utilizado quando o tipo de enlace for simples ou SSL.  <br><br>Introduza o nome de utilizador de Olá do toouse de conta do Windows hello quando se vincula toohello diretório LDAP quando o tipo de enlace é Windows.  Se deixado em branco, Olá com sessão iniciada da conta de utilizador é toobind utilizado. |
| Palavra-passe do Enlace |Introduza a palavra-passe de enlace de Olá para Olá enlace DN ou o nome de utilizador que está a ser o diretório LDAP toohello toobind utilizados.  tooconfigure Olá palavra-passe Olá serviço AdSync do multi-factor Auth servidor, ativar a sincronização e certifique-se de que o serviço de Olá está em execução no computador local Olá.  palavra-passe de Olá é guardada no Olá Windows armazenados nomes de utilizador e palavras-passe em Olá de conta Olá que serviço AdSync do multi-factor Auth Server está em execução como.  palavra-passe de Olá também é guardada em Olá de conta Olá multi-factor Auth Server interface de utilizador está a executar como e, em Olá de conta Olá serviço do servidor multi-factor Auth está a ser executado.  <br><br>Uma vez que a palavra-passe de Olá apenas é armazenada nos nomes de utilizador do Windows armazenados e palavras-passe do servidor local Olá, repita este passo em cada servidor de autenticação Multifator que necessita de palavra-passe toohello de acesso. |
| Tamanho limite da consulta |Especifique Olá tamanho limite Olá máximo de utilizadores que devolva uma procura no diretório.  Este limite deve corresponder à configuração de Olá no diretório LDAP Olá.  Para consultas grandes onde não é suportada paginação, sincronização e a importação tenta tooretrieve utilizadores em lotes.  Se o limite de tamanho de Olá especificado aqui for maior do que o limite de Olá configurado no diretório LDAP Olá, alguns utilizadores poderão ser perdidos. |
| Botão Testar |Clique em **teste** servidor LDAP do tootest enlace toohello.  <br><br>Não precisa de tooselect Olá **utilizar LDAP** opção tootest enlace. Isto permite Olá enlace toobe testada antes de utilizar a configuração de LDAP Olá. |

## <a name="filters"></a>Filtros
Os filtros permitem-lhe registos de tooqualify tooset critérios ao realizar uma pesquisa de diretório.  Ao definir o filtro de Olá, pode definir o âmbito Olá objetos que pretende toosynchronize.  

![Filtros](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

Multi-factor Authentication do Azure tem Olá seguintes três opções de filtro:

* **Filtro de contentor** -especificar critérios de filtro de Olá utilizada tooqualify registos do contentor quando efetuar uma procura no diretório.  Para o Active Directory e ADAM, é normalmente utilizado (|(objectClass=organizationalUnit)(objectClass=container)).  Para outros diretórios LDAP, utilize os critérios de filtro que qualificam cada tipo de objeto de contentor, dependendo do esquema de diretório Olá.  <br>Nota: se for deixado em branco, é utilizado por predefinição, ((objectClass=organizationalUnit)(objectClass=container)).
* **Filtro de grupo de segurança** -especificar critérios de filtro de Olá utilizar registos de grupo de segurança tooqualify quando efetuar uma procura no diretório.  Para o Active Directory e ADAM, é normalmente utilizado, (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)).  Para outros diretórios LDAP, utilize os critérios de filtro que qualificam cada tipo de objeto do grupo de segurança, dependendo do esquema de diretório Olá.  <br>Nota: se for deixado em branco, é utilizado por predefinição (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)).
* **Filtro de utilizador** -especificar critérios de filtro de Olá utilizada tooqualify registos de utilizador quando efetuar uma procura no diretório.  Para o Active Directory e ADAM, é normalmente utilizado (&(objectClass=user)(objectCategory=person)).  Para outros diretórios LDAP, utilize (objectClass = inetOrgPerson) ou algo semelhante, dependendo do esquema de diretório Olá. <br>Nota: se for deixado em branco, é utilizado por predefinição (&(objectCategory=person)(objectClass=user)).

## <a name="attributes"></a>Atributos
Pode personalizar os atributos conforme necessário para um diretório específico.  Isto permite-lhe tooadd de atributos personalizados e otimizar Olá sincronização tooonly Olá os atributos que precisa. Utilize o nome de Olá de Olá attricute conforme definido no esquema de diretório de Olá para o valor de Olá de cada campo de atributo. Olá tabela seguinte fornece informações adicionais sobre cada funcionalidade.

Os atributos podem ser introduzidos manualmente e não são necessária toomatch um atributo na lista de atributos de Olá.

![Atributos](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| Funcionalidade | Descrição |
| --- | --- |
| Identificador exclusivo |Introduza o nome de atributo Olá do atributo de Olá que funciona como identificador exclusivo do Olá do contentor, grupo de segurança e registos de utilizador.  No Active Directory, normalmente é objectGUID. Outras implementações de LDAP podem utilizar entryUUID ou algo semelhante.  Olá predefinição é objectGUID. |
| Tipo de identificador exclusivo |Selecione o tipo de Olá de atributo de identificador exclusivo de Olá.  No Active Directory, o atributo de objectGUID Olá é do tipo GUID. Outras implementações de LDAP podem utilizar o tipo Matriz de Bytes ASCII ou Cadeia.  Olá predefinição é GUID. <br><br>É importante tooset este tipo corretamente uma vez que os itens de sincronização são referenciados pelo respetivo Identificador exclusivo. Olá, tipo de identificador exclusivo é objeto de Olá de localizar toodirectly utilizado no diretório de Olá.  Definição tooString deste tipo quando diretório Olá armazena, na verdade, o valor de Olá como uma matriz de bytes de carateres ASCII impede a sincronização funcione devidamente. |
| Nome único |Introduza o nome de atributo Olá do atributo de Olá que contém Olá nome único para cada registo.  No Active Directory, normalmente é distinguishedName. Outras implementações de LDAP podem utilizar entryDN ou algo semelhante.  Olá predefinição é distinguishedName. <br><br>Se não existir um atributo que contém apenas Olá nome único, o atributo adspath de Olá pode ser utilizado.  Olá "LDAP: / /\<servidor\>/" parte do caminho de Olá é removida automaticamente, desativar, deixando apenas Olá nome único do objeto de Olá. |
| Nome do contentor |Introduza o nome de atributo Olá do atributo de Olá que contém o nome de Olá num registo de contentor.  valor de Olá deste atributo é apresentado no Olá hierarquia do contentor quando importar do Active Directory ou adicionar itens de sincronização.  Olá predefinição é name. <br><br>Se contentores diferentes utilizarem atributos diferentes para os respetivos nomes, utilize ponto e vírgula tooseparate vários atributos de nome de contentor.  atributo de nome do Olá primeiro contentor encontrado num objeto de contentor é utilizado toodisplay respetivo nome. |
| Nome do grupo de segurança |Introduza o nome de atributo Olá do atributo de Olá que contém o nome de Olá no registo de grupo de segurança.  valor de Olá deste atributo é apresentado na lista de grupos de segurança de Olá quando importar do Active Directory ou adicionar itens de sincronização.  Olá predefinição é name. |
| Nome de utilizador |Introduza o nome de atributo Olá do atributo de Olá que contém o nome de utilizador Olá num registo de utilizador.  valor de Olá deste atributo é utilizado como nome de utilizador do Olá servidor multi-Factor Auth.  Um segundo atributo pode ser especificado como uma cópia de segurança toohello primeiro.  Step-by-Olá segundo atributo só é utilizado se o primeiro atributo de Olá não contém um valor para o utilizador Olá.  Olá predefinições são userPrincipalName e sAMAccountName. |
| Nome próprio |Introduza o nome de atributo Olá do atributo de Olá que contém o nome do próprio Olá num registo de utilizador.  Olá predefinição é givenName. |
| Apelido |Introduza o nome de atributo Olá do atributo de Olá que contém o apelido Olá num registo de utilizador.  Olá predefinição é sn. |
| Endereço de e-mail |Introduza o nome de atributo Olá do atributo de Olá que contém o endereço de correio eletrónico Olá num registo de utilizador.  Endereço de correio eletrónico é utilizada toosend de boas-vindas e a atualização de utilizador de toohello de mensagens de correio eletrónico.  Olá predefinição é mail. |
| Grupo de utilizadores |Introduza o nome de atributo Olá do atributo de Olá que contém o grupo de utilizadores de Olá num registo de utilizador.  Grupo de utilizadores pode ser utilizado toofilter utilizadores no agente Olá e nos relatórios no Olá Portal de gestão de servidor do multi-factor Auth. |
| Descrição |Introduza o nome de atributo Olá do atributo de Olá que contém Olá descrição num registo de utilizador.  A descrição só é utilizada para procurar.  Olá predefinição é description. |
| Idioma da chamada telefónica |Introduza o nome do atributo do atributo de Olá que contém o nome abreviado Olá de Olá idioma toouse para chamadas de voz do utilizador Olá Olá. |
| Idioma da mensagem de texto |Introduza o nome do atributo do atributo de Olá que contém o nome abreviado Olá de Olá idioma toouse para mensagens de texto SMS para o utilizador Olá Olá. |
| Idioma da aplicação móvel |Introduza o nome do atributo do atributo de Olá que contém o nome abreviado Olá de Olá idioma toouse para mensagens de texto de aplicação de telefone do utilizador Olá Olá. |
| Idioma do token OATH |Introduza o nome do atributo do atributo de Olá que contém o nome abreviado Olá de Olá idioma toouse para mensagens de texto do token OATH do utilizador Olá Olá. |
| Telefone da empresa |Introduza o nome de atributo Olá do atributo de Olá que contém o número de telefone da empresa Olá num registo de utilizador.  Olá predefinição é telephoneNumber. |
| Telefone de casa |Introduza o nome de atributo Olá do atributo de Olá que contém o número de telefone de casa Olá num registo de utilizador.  Olá predefinição é homePhone. |
| Pager |Introduza o nome de atributo Olá do atributo de Olá que contém o número de pager Olá num registo de utilizador.  Olá predefinição é pager. |
| Número de telemóvel |Introduza o nome de atributo Olá do atributo de Olá que contém o número de telemóvel Olá num registo de utilizador.  Olá predefinição é mobile. |
| Fax |Introduza o nome de atributo Olá do atributo de Olá que contém o número de fax Olá num registo de utilizador.  Olá predefinição é facsimileTelephoneNumber. |
| Número de IP |Introduza o nome de atributo Olá do atributo de Olá que contém o número de telefone IP Olá num registo de utilizador.  Olá predefinição é ipPhone. |
| Personalizado |Introduza o nome de atributo Olá do atributo de Olá que contém um número de telefone personalizado num registo de utilizador.  predefinição de Olá está em branco. |
| Extensão |Introduza o nome de atributo Olá do atributo de Olá que contém a extensão de número de telefone de Olá num registo de utilizador.  valor de Olá do campo de extensão de Olá é utilizado como Olá extensão toohello telefone principal apenas do número.  predefinição de Olá está em branco. <br><br>Se não for especificado o atributo de extensão de Olá, as extensões podem ser incluídas como parte do atributo de telefone de Olá. Neste caso, preceder extensão Olá com um 'x', para que este obtém analisar corretamente.  Por exemplo, 555-123-4567 x890 resultaria em 555-123-4567 como número de telefone Olá e 890 como extensão Olá. |
| Botão Restaurar Predefinições |Clique em **restaurar predefinições** tooreturn fazer uma cópia de todos os atributos de valor predefinido de tootheir.  Olá predefinições deverão funcionar corretamente com Olá normal do Active Directory ou ADAM um esquema. |

tooedit atributos, clique em **editar** no separador de atributos de Olá.  Isto permite beneficiar de uma janela de onde pode editar atributos Olá. Selecione Olá **...**  tooopen de atributo do seguinte tooany uma janela de onde pode escolher qual toodisplay de atributos.

![Editar Atributos](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>Sincronização
Sincronização mantém sincronizada com Olá utilizadores no Active Directory ou outro diretório acesso protocolo LDAP (Lightweight Directory) Olá base de dados de utilizador de MFA do Azure. o processo de Olá é semelhante tooimporting utilizadores manualmente do Active Directory, mas consulta periodicamente se existem para o utilizador do Active Directory e grupo de segurança tooprocess é alterado.  Também desativa ou remove os utilizadores que foram removidos de um contentor, de um grupo de segurança ou do Active Directory.

Olá, o serviço ADSync do multi-factor Auth é um serviço do Windows que executa Olá periódica de consulta do Active Directory.  Não é toobe confundido com o Azure AD Sync ou do Azure AD Connect.  Olá ADSync do multi-factor Auth, embora incorporado numa base de código semelhante, é específica toohello servidor do Azure multi-factor Authentication.  Este é instalado num estado parado e é iniciado pelo serviço servidor multi-Factor Auth quando configurado de Olá toorun.  Se tiver uma configuração de servidor multi-Factor Auth multisservidor, Olá ADSync do multi-factor Auth só pode ser executado num único servidor.

Olá, o serviço ADSync do multi-factor Auth utiliza Olá extensão de servidor DirSync LDAP fornecida pela consulta de tooefficiently da Microsoft para que as alterações.  Este controlo Dirsync tem de ter Olá "diretório obtém alterações" à direita e DS-Replication-Get-Changes expandida controlar o acesso à direita.  Por predefinição, estes direitos são atribuídos toohello as contas de administrador e LocalSystem em controladores de domínio.  Olá, o serviço AdSync do multi-factor Auth está configurado toorun como LocalSystem, por predefinição.  Por conseguinte, é mais simples serviço de Olá toorun num controlador de domínio.  Se configurar Olá serviço tooalways efetuar uma sincronização completa, pode ser executado como uma conta com permissões menores.  É menos eficiente, mas requer menos privilégios de conta.

Se o diretório LDAP Olá suporta e está configurado para o DirSync, em seguida, consulta de alterações ao grupo de segurança e utilizadores funcionará Olá mesmo como acontece com o Active Directory.  Se o diretório LDAP Olá não suporta Olá controlo DirSync, é efetuada uma sincronização completa durante cada ciclo.

![Sincronização](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

Olá tabela seguinte contém informações adicionais sobre cada uma das definições de tabulações Olá sincronização.

| Funcionalidade | Descrição |
| --- | --- |
| Ativar a sincronização com o Active Directory |Quando selecionado, Olá serviço servidor multi-Factor Auth consulta periodicamente se existem do Active Directory para que as alterações. <br><br>Nota: tem de ser adicionado, pelo menos, um Item de sincronização e uma tarefa sincronizar agora tem de ser executada antes de Olá multi-factor Auth servidor serviço começar a processar alterações. |
| Sincronizar a cada |Especifique Olá de intervalo de tempo de Olá multi-factor Auth servidor serviço irá esperar entre consultas e processamento de alterações. <br><br> Nota: intervalo de Olá especificado está na altura de Olá entre o início de Olá de cada ciclo.  Se as alterações de processamento de tempo de Olá excedem o intervalo de Olá, o serviço de Olá irá consultar novamente de imediato. |
| Remover utilizadores que já não constem no Active Directory |Quando selecionado, Olá serviço servidor multi-Factor Auth irá processar tombstones de utilizadores eliminados do Active Directory e remover Olá relacionados com o servidor multi-Factor Auth utilizador. |
| Efetuar sempre uma sincronização completa |Quando selecionado, Olá serviço servidor multi-Factor Auth irá efetuar sempre uma sincronização completa.  Quando desmarcado, Olá serviço servidor multi-Factor Auth irá efetuar uma sincronização incremental, consultando apenas os utilizadores que tenham sido alterados.  Olá predefinição é desmarcada. <br><br>Quando desmarcado, o servidor MFA do Azure efetua a sincronização incremental apenas quando o diretório de Olá suporta o controlo de DirSync Olá e diretório de toohello de enlace de contas de Olá tem consultas incrementais do permissões tooperform DirSync.  Se Olá conta não tem as permissões adequadas Olá ou se estiverem envolvidos vários domínios na sincronização Olá, o servidor MFA do Azure efetua uma sincronização completa. |
| Exigir aprovação do administrador quando o número de utilizadores desativados ou removidos exceder o limiar |Itens de sincronização podem ser configurado toodisable ou remover utilizadores que deixaram de ser um membro do grupo de segurança ou contentor do item de Olá.  Como salvaguarda, aprovação do administrador pode ser exigida quando Olá diversas toodisable de utilizadores ou remover exceder um limiar.  Quando selecionada, é exigida aprovação para o limiar especificado.  Olá predefinição é 5 e o intervalo de Olá é 1 too999. <br><br> A aprovação é facilitada enviando primeiro uma tooadministrators de notificação de correio eletrónico. notificação de correio eletrónico de Olá dá instruções para rever e aprovar Olá desativação e remoção de utilizadores.  Quando a interface de utilizador do servidor multi-Factor Auth Olá é iniciada, pedirá aprovação. |

Olá **sincronizar agora** botão permite-lhe toorun uma sincronização completa para a sincronização de Olá itens especificados.  Uma sincronização completa é precisa sempre que forem adicionados, modificados, removidos ou reordenados itens de sincronização.  Também é Olá necessário antes do serviço AdSync do multi-factor Auth está operacional, uma vez que define Olá a partir do qual o serviço de Olá irá efetuar consultas para alterações incrementais de ponto de partida.  Se forem feitas alterações toosynchronization itens, mas ainda não foi efetuada uma sincronização completa, será pedido tooSynchronize agora.

Olá **remover** botão permite Olá administrador toodelete um ou mais itens de sincronização da lista de itens de sincronização do Olá servidor multi-Factor Auth.

> [!WARNING]
> Assim que um registo de item de sincronização tiver sido removido, não pode ser recuperado. Terá de sincronização de Olá tooadd item registos novamente caso o tenha eliminado por engano.

item de sincronização de Olá ou itens de sincronização foram removidos do servidor multi-Factor Auth.  Olá serviço servidor multi-Factor Auth já não irá processar os itens de sincronização de Olá.

os botões Mover para cima e mover para baixo de Olá permitem administrador Olá ordem de Olá toochange dos itens de sincronização de Olá.  Olá ordem é importante uma vez que hello mesmo utilizador pode ser um membro de mais do que um item de sincronização (por exemplo, um contentor e um grupo de segurança).  definições de Olá utilizador toohello aplicadas durante a sincronização serão provenientes Olá primeiro item de sincronização no utilizador de Olá Olá lista toowhich está associado.  Por conseguinte, os itens de sincronização de Olá devem ser colocados por ordem de prioridade.

> [!TIP]
> Depois de remover itens de sincronização, deve fazer uma sincronização completa.  Depois de ordenar itens de sincronização, deve fazer uma sincronização completa.  Clique em **sincronizar agora** tooperform uma sincronização completa.

## <a name="multi-factor-auth-servers"></a>Servidores Multi-Factor Auth
Servidores de autenticação Multifator adicionais podem ser programados tooserve como um proxy RADIUS cópia de segurança, LDAP proxy ou para autenticação do IIS. configuração de sincronização de Olá é partilhada entre todos os agentes de Olá. No entanto, apenas um destes agentes poderá ter o serviço do servidor multi-Factor Auth Olá está em execução. Este separador permite-lhe tooselect Olá servidor do multi-factor Auth que deve ser ativado para sincronização.

![Servidores Multi-Factor-Auth](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)
