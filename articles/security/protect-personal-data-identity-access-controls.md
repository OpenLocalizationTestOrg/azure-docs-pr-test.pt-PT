---
title: os dados pessoais aaaProtect com controlos de identidades e acessos do Azure | Microsoft Docs
description: Utilizar toohelp de controlos de identidades e acessos do Azure pode protege os seus dados pessoais
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory e o multi-factor Authentication: proteger os dados pessoais com controlos de identidades e acessos

Este artigo fornece informações e procedimentos que pode utilizar os dados pessoais tooprotect utilizar os serviços e funcionalidades de segurança do Azure Active Directory e o multi-factor authentication.

## <a name="scenario"></a>Cenário

Uma empresa de grande cruise headquartered no Olá dos Estados Unidos, está a expandir as respetivas itineraries de toooffer operações no Mediterranean Olá, Adriatic e Baltic seas, bem como Olá território Isles. toosupport os esforços obteve várias linhas cruise mais pequenas com base em (Itália), na Alemanha, Dinamarca e Olá U.K. 

empresa Olá utiliza os dados empresariais do Microsoft Azure toostore na nuvem de Olá. Isto inclui informações pessoais tais como nomes, endereços, números de telefone e informações de cartão de crédito da respetiva base de cliente global. Também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, os números de identificação de dedução dos impostos e médicas informações sobre os funcionários da empresa em todas as localizações. linha de cruise Olá mantém também uma grande base de dados de membros de programa reward e loyalty que inclui as relações de tootrack informações pessoais com clientes atuais e anteriores.

Empresariais aos funcionários acesso Olá rede de armazenamento da empresa Olá escritórios remotos e agentes levar localizados em torno Olá mundo ter toosome aceder a recursos empresariais.

## <a name="problem-statement"></a>Declaração do problema

empresa Olá deve proteger a privacidade de Olá dos dados pessoais dos clientes e dos empregados de atacantes pesquisa toouse comprometido identidades toogain acesso. Eles também tem de garantir que toopersonal de acesso a dados por utilizadores legítimos estão restringidos apenas a quem será necessário toodo as respetivas tarefas.

## <a name="company-goal"></a>Objetivo da empresa

Objetivo da empresa Olá é tooensure aceder a dados toopersonal é estritamente controlada. É essencial que as identidades dos utilizadores com aceder a dados toopersonal estar protegido por autenticação forte. Uma política do [menor privilégio] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) tem de ser imposta para que os utilizadores legítimos tem apenas Olá nível de acesso que precisam e não existem mais.

## <a name="solutions"></a>Soluções

Microsoft Azure fornece ferramentas de gestão de identidades e acesso de controlo de empresas de toohelp quem tem acesso tooresources que contêm dados pessoais.

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) gere as identidades e controla o acesso tooAzure, bem como outro no local e outros recursos na nuvem, dados e aplicações. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) ajuda os administradores do Azure toominimize Olá diversas pessoas que têm acesso toocertain informações tais como os dados pessoais. Permite-lhes toodiscover, restringir e monitorizar as identidades privilegiadas e o respetivos acesso tooresources tooassign temporário, just (JIT) direitos administrativos tooeligible utilizadores e. Também fornece informações sobre os utilizadores que possuem os privilégios administrativos AAD.

as atividades de Olá envolvidas na utilizando AAD PIM incluem:

- Ativar o Privileged Identity Management para o seu diretório

- Utilizando informações importantes de Privileged Identity Management admin dashboard toosee num instante

- Gestão de identidades Olá privilegiado (administradores) através da adição ou remoção de função de tooeach administradores permanentes ou elegíveis

- Configurar definições de ativação de função Olá

- Ativar funções

- Rever a actividade de função

#### <a name="how-do-i-enable-aad-pim"></a>Como ativar a PIM do AAD?

toostart PIM a utilizar para o seu diretório, Olá a seguir:

1. Inicie sessão no toohello portal do Azure como um administrador global do seu diretório.

2. Se a sua organização tiver mais do que um diretório, selecione o seu nome de utilizador no canto direito superior Olá de Olá portal do Azure. Selecione o diretório de olá onde utilizará o Azure AD Privileged Identity Management.

3. Selecione **mais serviços** e utilizar Olá **filtro** toosearch de caixa de texto para o Azure AD Privileged Identity Management.

4. Verifique **Pin toodashboard** e, em seguida, clique em **criar**. é aberto o Olá aplicação Privileged Identity Management.

Depois de configurada do Azure AD Privileged Identity Management, consulte painel de navegação de Olá sempre que abrir a aplicação Olá.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

Para obter mais informações e instruções sobre como começar a PIM do AAD, consulte [começar a utilizar o Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)

### <a name="azure-role-based-access-control"></a>Controlo de acesso baseado em funções do Azure

[Controlo de acesso baseado em funções do Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ajuda os administradores do Azure gerir aceder a recursos tooAzure Ativando Olá concessão de permissões de acesso com base na função de utilizador Olá atribuído. Pode segregar funções dentro de uma equipa e conceder apenas Olá quantidade de acesso toousers, grupos e aplicações que precisam de tooperform as respetivas tarefas.

Acesso baseado em funções pode ser concedido toousers utilizando Olá portal do Azure, as ferramentas da linha de comandos do Azure ou APIs de gestão do Azure.

Para mais informações sobre noções básicas do RBAC do Azure, consulte [introdução ao controlo de acesso baseado em funções na Olá Portal do Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>Como gerir o RBAC do Azure com o PowerShell

Pode utilizar o PowerShell cmdlets toomanage RBAC do Azure, incluindo Olá seguintes tarefas de gestão:

- Lista de funções

- Ver quem tem acesso

- Conceder acesso

- Remover o acesso

- Criar uma função personalizada

- Obter as ações de um fornecedor de recursos

- Modificar uma função personalizada

- Eliminar uma função personalizada

- Lista de funções personalizadas

Para obter instruções sobre como toomanage RBAC do Azure com o PowerShell, consulte o artigo [baseada em funções gerir acesso com o Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).

### <a name="azure-multi-factor-authentication"></a>Multi-Factor Authentication do Azure

[Multi-factor Authentication do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) é uma solução de verificação de dois passos que ajuda a salvaguardar acesso toodata e aplicações, cumprindo o pedido do utilizador para um processo de início de sessão simple. Oferece autenticação forte através de vários métodos de verificação, incluindo chamada telefónica, mensagem de texto ou verificação de aplicação móvel.

toodeploy MFA na Olá em nuvem do Azure, terá de toofirst ativá-la e, em seguida, ative a verificação em dois passos para os utilizadores.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>Como ativar a toouse do Azure MFA?

Se os utilizadores têm de licenças que incluem o Azure multi-factor Authentication, não há nada que precisa de toodo tooturn na MFA do Azure. Caso contrário, terá de toocreate um fornecedor de multi-Factor Auth no seu diretório. toodo isto, siga estes passos:

1. Selecione **do Active Directory** no Olá portal clássico do Azure (com sessão iniciado como administrador).

2. Selecione **fornecedores do multi-factor Authentication.**

3. Selecione **novo,** e, em **serviços aplicacionais,** selecione **fornecedor do multi-factor Auth.**

4. Selecione **criação rápida.**

5. Preencha o campo de nome de Olá e selecione um modelo de utilização (por autenticação ou por utilizador ativado).

6. Designa um diretório com que Olá fornecedor de MFA está associado.

7. Clique em Olá **criar** botão.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

Para obter mais instruções sobre como toomanage o fornecedor do multi-factor Auth, consulte [introdução de um fornecedor do multi-factor Auth do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>Como ativar verificação em dois passos para os utilizadores?

Pode impor a verificação de dois passos para todos os inícios de sessão ou pode criar a verificação de acesso condicional políticas toorequire apenas quando aplicam condições específicas.

Ativar a MFA do Azure, alterando os Estados de utilizador é a abordagem tradicional de Olá para exigir a verificação de dois passos. Todos os utilizadores de Olá que ativar terão Olá tooperform a verificação de requisito mesmo sempre iniciar sessão. Ativar um utilizador substitui quaisquer políticas de acesso condicional que podem afetar esse utilizador.

Ativar a MFA do Azure com uma política de acesso condicional é uma abordagem mais flexível para exigir a verificação de dois passos. Pode criar políticas de acesso condicional que se aplicam toogroups, bem como os utilizadores individuais. Grupos de alto risco podem ser especificados mais restrições de grupos de baixo risco, ou pode ser necessário apenas para aplicações na nuvem de alto risco e ignorada para baixo risco aqueles verificação em dois passos. No entanto, o acesso condicional é uma funcionalidade paga do Azure Active Directory.

tooenable MFA alterando o estado do utilizador, Olá seguintes:

1. Inicie sessão no toohello portal do Azure como administrador.
2. Aceda demasiado**do Azure Active Directory \> utilizadores e grupos \> todos os utilizadores**.
3. Selecione **multi-factor Authentication**.
4. Localizar Olá utilizador que pretende que tooenable para MFA do Azure. Poderá ser necessário toochange Olá vista na parte superior do Olá.
5. Verifique o nome de Olá caixa seguinte toohello do utilizador.
6. Olá direita, em passos rápidos, escolha **ativar**.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Confirme a sua selecção na janela de pop-up Olá que é aberta.  Os utilizadores para o qual o MFA tiver sido ativada serão pedidos tooregister Olá vez seguinte que iniciar sessão.

tooenable MFA do Azure com uma política de acesso condicional, Olá seguintes:

1. Inicie sessão no toohello portal do Azure como administrador.

2. Aceda demasiado**do Azure Active Directory \> acesso condicional**.

3. Selecione **nova política**.

4. Em **atribuições**, selecione **utilizadores e grupos**. Olá utilize **incluir** e **excluir** separadores toospecify quais os utilizadores e grupos será gerido pela política de Olá.

5. Em **atribuições**, selecione **aplicações em nuvem.** Escolha demasiado**incluem todas as aplicações em nuvem**.
6.  Em **controlos de acesso**, selecione **conceder**. Escolha **requer autenticação multifator**.
7.  Ativar **ativar política de** demasiado**no** e, em seguida, selecione **guardar**.

Para obter informações sobre como tooconfigure MFA do Azure definições tooset configurar alertas de fraude, criar uma omissão de uso individual, utilizar mensagens de voz personalizadas, configurar a colocação em cache, especificar IPs fidedignos, criar palavras-passe de aplicação, ativar a MFA para dispositivos que os utilizadores de confiança e selecione a memorizar métodos de verificação, consulte [configurar definições de autenticação de multi-factor do Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>Passos seguintes

- [Proteger o acesso privilegiado no Azure AD](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Perguntas mais frequentes sobre o Multi-Factor Authentication do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [Resolução de problemas de controlo de acesso baseado em funções](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Proteção de identidade do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
