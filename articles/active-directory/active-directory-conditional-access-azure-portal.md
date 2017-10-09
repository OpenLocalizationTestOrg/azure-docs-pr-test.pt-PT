---
title: aaaAzure acesso condicional de Active Directory | Microsoft Docs
description: "Utilize o controlo de acesso condicional no Azure Active Directory toocheck para condições específicas durante a autenticação para acesso tooapplications."
services: active-directory
keywords: "acesso condicional tooapps, acesso condicional com o Azure AD, proteger o acesso a recursos de toocompany, políticas de acesso condicional"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Acesso condicional no Azure Active Directory

No mundo mobile-primeiro, primeiro de nuvem, o Azure Active Directory permite toodevices de início de sessão único, aplicações e serviços a partir de qualquer lugar. Com a proliferação de Olá de dispositivos (incluindo o BYOD), trabalham em redes empresariais e aplicações de SaaS de terceiros 3rd, profissionais de TI são confrontadas com dois objetivos adversária:

- Capacitar Olá os utilizadores finais toobe produtivo onde quer que e sempre
- Proteger recursos da empresa Olá em qualquer altura

tooimprove produtividade, Azure Active Directory fornece os seus utilizadores com uma vasta gama de opções tooaccess os recursos da empresa. Gestão de acesso de aplicações, do Azure Active Directory permite-lhe que apenas tooensure *Olá pessoas corretas* possam aceder às suas aplicações. E se pretende toohave mais controlo sobre como pessoas corretas Olá estão a aceder os recursos em determinadas condições? E se tiver mesmo condições sob as quais pretende tooblock acesso toocertain aplicações mesmo para Olá *com o botão direito pessoas*? Por exemplo, poderá ser OK para si se as pessoas corretas Olá estão a aceder a determinadas aplicações de uma rede fidedigna; No entanto, não poderá-los tooaccess estas aplicações de uma rede que não fidedigna. Pode resolver estas questões, utilizando o acesso condicional.

Acesso condicional é uma funcionalidade do Azure Active Directory permite-lhe controlos tooenforce Olá acesso tooapps no seu ambiente com base nas condições específicas. Com controlos, ou pode juntar acesso de toohello requisitos adicionais ou pode bloqueá-lo. implementação de Olá do acesso condicional é com base em políticas. Uma abordagem baseada em políticas simplifica a sua experiência de configuração porque segue forma Olá que tem em consideração os requisitos de acesso.  

Normalmente, definir os requisitos de acesso instruções que se baseiam em Olá seguir o padrão de utilização:

![Controlo](./media/active-directory-conditional-access-azure-portal/10.png)

Quando substituir Olá dois as ocorrências "*isto*" com as informações do mundo real, tiver um exemplo de uma declaração de política que provavelmente procura familiar tooyou:

*Quando contratantes estão a tentar tooaccess nossas aplicações em nuvem das redes que não são fidedignas, bloquear o acesso.*

declaração de política de Olá acima destaca energia Olá do acesso condicional. Enquanto pode ativar contratantes toobasically aceder às suas aplicações de nuvem (**quem**), com o acesso condicional, também pode definir condições sob as qual Olá acesso é possível (**como**).

No contexto de Olá do acesso condicional do Azure Active Directory,

- "**Quando isto acontece**" denomina **declaração de condição**
- "**, Em seguida, fazer isto**" denomina **controlos**

![Controlo](./media/active-directory-conditional-access-azure-portal/11.png)

combinação de Olá de uma instrução de condição com os controlos representa uma política de acesso condicional.

![Controlo](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>Controlos

Uma política de acesso condicional, controlos de definem o que é que deve acontecer quando uma instrução de condição foram satisfeita.  
Com controlos, pode bloquear o acesso ou permitir o acesso com requisitos adicionais.
Quando configurar uma política que permite o acesso, terá de tooselect, pelo menos, um requisito.   

### <a name="grant-controls"></a>Controlos de conceder
implementação atual do Olá do Azure Active Directory permite-lhe Olá tooconfigure os requisitos de controlo da concessão:

![Controlo](./media/active-directory-conditional-access-azure-portal/05.png)

- **Autenticação multifator** -pode exigir a autenticação forte através da autenticação multifator. Como fornecedor, pode utilizar o multi-factor do Azure ou um fornecedor de autenticação multifator no local, juntamente com os serviços de Federação do Active Directory (AD FS). Utilizar multi-factor authentication ajuda a proteger os recursos de que está a ser acedida por um utilizador não autorizado que poderá ter obteve acesso toohello credenciais de um utilizador válido.

- **Dispositivo com conformidade** -pode definir políticas de acesso condicional ao nível do dispositivo Olá. Pode configurar uma política tooonly ativar os computadores em conformidade ou de dispositivos móveis que estejam inscritos num tooaccess de gestão de dispositivos móveis a recursos da sua organização. Por exemplo, pode utilizar a conformidade de dispositivo do Intune toocheck e, em seguida, comunicar-tooAzure AD para a imposição quando o utilizador Olá tenta tooaccess uma aplicação. Para obter orientações detalhadas sobre como toouse Intune tooprotect aplicações e dados, consulte [proteger aplicações e dados com o Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune). Também pode utilizar proteção de dados de tooenforce do Intune para dispositivos perdidos ou roubados. Para obter mais informações, consulte [ajudar a proteger os seus dados com a eliminação completa ou seletiva através do Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

- **Dispositivo associado a um domínio** – pode exigir Olá dispositivos que utilizou tooconnect tooAzure do Active Directory toobe associados a um domínio tooyour no local do Active Directory (AD). Esta política aplica-se tooWindows computadores de secretária, portáteis e enterprise tablets. 

Se tiver vários controlos selecionados, também pode configurar se todos eles são necessários quando a política for processada.

![Controlo](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>Controlos de sessão
Controlos de sessão ativar experiência restritiva numa aplicação de nuvem. controlos de sessão de Olá são impostos pelo aplicações na nuvem e dependem das informações adicionais fornecidas pela aplicação do Azure AD toohello sobre sessão Olá.

![Controlo](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>Utilize as restrições da aplicação imposta
Pode utilizar este controlo toorequire do Azure AD toopass Olá dispositivo informações toohello aplicação na nuvem. Isto ajuda a aplicação de nuvem Olá saber se o utilizador de Olá for proveniente de um dispositivo compatível com ou um dispositivo associado a um domínio. Este controlo está atualmente só é suportada com o SharePoint como Olá aplicação de nuvem. SharePoint utiliza os utilizadores a tooprovide de informações de dispositivos de Olá uma experiência completa ou limitada, dependendo do Estado do dispositivo Olá.
toolearn mais informações sobre como toorequire limitada acesso com o SharePoint, vá [aqui](https://aka.ms/spolimitedaccessdocs).

## <a name="condition-statement"></a>Declaração de condição

secção anterior Olá tem introduzida toosupported opções tooblock ou restringir acesso tooyour recursos num formulário de controlos. Na política de acesso condicional, é possível definir critérios de Olá que têm toobe cumprido para sua toobe controlos aplicado no formulário de uma instrução de condição.  

Pode incluir Olá seguir atribuições para a sua declaração de condição:

![Controlo](./media/active-directory-conditional-access-azure-portal/07.png)


- **Quem** -em muitos casos, pretende que os controlos toobe aplicada tooa conjunto específico de utilizadores. Uma instrução de condição, pode definir este conjunto selecionando utilizadores Olá e grupos que a política se aplica. Se necessário, também explicitamente pode excluir um conjunto de utilizadores da sua política, exempting-los.  
Ao selecionar utilizadores e grupos, definir âmbito de Olá de utilizadores que a política se aplica a.    

    ![Controlo](./media/active-directory-conditional-access-azure-portal/08.png)



- **O que** -normalmente, existem determinadas aplicações que estejam a executar no seu ambiente que necessitam de uma perspetiva de proteção, a mais atenção que outros. Este procedimento afeta, por exemplo, as aplicações que tenham acesso toosensitive dados.
Ao selecionar as aplicações na nuvem, pode define âmbito de Olá aplicações em nuvem, que a política se aplica. Se necessário, pode excluir explicitamente também um conjunto de aplicações da sua política.

    ![Controlo](./media/active-directory-conditional-access-azure-portal/09.png)


- **Como** - desde que o acesso tooyour aplicações é efetuada em condições pode controlar, há pode ser necessário para impor controlos adicionais sobre como as suas aplicações em nuvem são acedidas pelos seus utilizadores. No entanto, coisas podem parecer diferentes se acesso a aplicações na nuvem tooyour for executado, por exemplo, de redes que não são fidedignas ou dispositivos que não são compatíveis. Uma instrução de condição, pode definir determinadas condições de acesso que têm requisitos adicionais de forma acesso tooyour aplicações é efetuada.

    ![Condições](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>Condições

Na implementação atual de Olá do Azure Active Directory, pode definir condições para Olá seguintes áreas:

- Risco de início de sessão
- Plataformas de dispositivos
- Localizações
- Aplicações de cliente

![Condições](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>Risco de início de sessão

Um risco de início de sessão é um objeto que é utilizado pelo probabilidade do Azure Active Directory tootrack Olá que uma tentativa de início de sessão não foi efetuada pelo proprietário de legítimos Olá de uma conta de utilizador. Este objeto, a probabilidade de Olá (alta, média ou baixa) é armazenada em formato de um atributo chamado [ao nível do risco de início de sessão](active-directory-reporting-risk-events.md#risk-level). Este objeto é gerado durante um início de sessão de um utilizador se o início de sessão riscos foram detetados pelo Azure Active Directory. Para obter mais detalhes, veja [Inícios de sessão de risco](active-directory-identityprotection.md#risky-sign-ins).  
Pode utilizar o nível de risco de início de sessão de Olá calculado como condição numa política de acesso condicional. 

![Condições](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>Plataformas de dispositivos

plataforma de dispositivos de Olá é caracterizada por sistema operativo Olá que está a executar no seu dispositivo:

- Android
- iOS
- Windows Phone
- Windows
- macOS (pré-visualização). 

![Condições](./media/active-directory-conditional-access-azure-portal/02.png)

Pode definir plataformas de dispositivos de Olá que estão incluídas, bem como as plataformas de dispositivos que são excluídas de uma política.  
plataformas de dispositivos de toouse na política de Olá, primeiro altere Olá configurar mudanças de modo email demasiado**Sim**e, em seguida, selecionar todas ou dispositivo individual plataformas Olá política se aplica. Se selecionar plataformas de dispositivos individuais, política de Olá tem apenas um impacto nas plataformas seguintes. Neste caso, as plataformas de tooother suportado de inícios de sessão não são afetadas pela política de Olá.


### <a name="locations"></a>Localizações

Olá localização é identificada por endereço IP hello do cliente de Olá utilizou tooconnect tooAzure do Active Directory. Esta condição requer toobe familiarizado com **denominado localizações** e **MFA IPs fidedignos**.  

**Com o nome localizações** é uma funcionalidade do Azure Active Directory que permite-lhe intervalos de endereços IP toolabel fidedigno nas suas organizações. No seu ambiente, pode utilizar localizações chamadas no contexto de Olá deteção Olá de [eventos de risco](active-directory-reporting-risk-events.md) , bem como o acesso condicional. Para obter mais detalhes sobre a configuração com o nome localizações no Azure Active Directory, consulte [localizações no Azure Active Directory com o nome](active-directory-named-locations.md).

número de Olá das localizações, que pode configurar é limitado pela tamanho Olá de objeto relacionados Olá no Azure AD. Pode configurar:
 
 - Uma localização com o nome com configurar os intervalos IP too500
 - Um máximo de 60 localizações com nome (pré-visualização) com um intervalo IP atribuído tooeach deles 


**IPs fidedignos do MFA** é uma funcionalidade de autenticação multifator que lhe permite intervalos de endereços IP toodefine fidedigno que representa a intranet local da sua organização. Quando configura um condições de localização, IPs fidedignos permite-lhe toodistinguish entre ligações efetuadas a partir da rede da sua organização e todas as outras localizações. Para obter mais detalhes, consulte [IPs fidedignos](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).  



Pode optar por incluir todas as localizações ou todos os IPs fidedignos e pode excluir IPs fidedignos todos.

![Condições](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>Aplicação de cliente

aplicação de cliente Olá pode ser numa aplicação Olá nível genérico (web browser, aplicação móvel, cliente de ambiente de trabalho) que utilizou tooconnect tooAzure do Active Directory ou pode selecionar especificamente Exchange Active Sync.  
Autenticação legada refere-se tooclients utilizando a autenticação básica, tais como clientes mais antigos do Office que não utilizam autenticação moderna. Acesso condicional não é atualmente suportado com a autenticação de legado.

![Condições](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>Cenários comuns

### <a name="requiring-multi-factor-authentication-for-apps"></a>Exigir a autenticação multifator para aplicações

As aplicações que requerem um nível superior de proteção Olá outras pessoas de ter vários ambientes.
Isto é, por exemplo, caso Olá para aplicações que tenham acesso toosensitive dados.
Se quiser tooadd outra camada de proteção toothese aplicações, pode configurar uma política de acesso condicional que requer autenticação multifator, quando os utilizadores estão a aceder a estas aplicações.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Exigir a autenticação multifator para acesso a partir de redes que não são fidedignas

Este cenário é semelhante cenário anterior de toohello porque adiciona um requisito de autenticação multifator.
No entanto, a principal diferença de Olá é condição Olá para este requisito.  
Enquanto estava foco Olá cenário anterior Olá nas aplicações com dados de acesso de toosensitve, Olá foco deste cenário é fidedignas localizações.  
Por outras palavras, pode ter um requisito de autenticação multifator se aceder a uma aplicação por um utilizador de uma rede que não fidedigna.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Apenas os dispositivos fidedignos podem aceder a serviços do Office 365

Se estiver a utilizar o Intune no seu ambiente, pode iniciar imediatamente a utilizar a interface de política de acesso condicional Olá no Olá consola do Azure.

Muitos clientes do Intune estão a utilizar tooensure de acesso condicional que apenas os dispositivos fidedignos podem aceder a serviços do Office 365. Isto significa que os dispositivos móveis estão inscritos no Intune e cumpram os requisitos da política de conformidade e de que os PCs Windows estão tooan associados a um domínio de no local. Uma melhoria de chave é que não dispõe de tooset hello mesma política para cada um dos serviços de Olá do Office 365.  Quando cria uma nova política, configure Olá nuvem aplicações tooinclude cada de Olá O365 aplicações que pretende tooprotect com acesso condicional.

## <a name="next-steps"></a>Passos seguintes

Se quiser tooknow como tooconfigure uma política de acesso condicional, consulte [introdução ao acesso condicional no Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Se estiver pronto tooconfigure políticas de acesso condicional para o seu ambiente, consulte Olá [melhores práticas para acesso condicional no Azure Active Directory](active-directory-conditional-access-best-practices.md). 
