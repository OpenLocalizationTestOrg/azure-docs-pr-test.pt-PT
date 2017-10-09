---
title: "aaaAzure do Active Directory prova de conceito manual de comunicação social edifício blocos | Microsoft Docs"
description: "Explorar e implementar rapidamente a cenários de identidade e gestão de acesso"
services: active-directory
keywords: do Azure Active Directory, manual, uma prova de conceito, PoC
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Azure Active Directory prova do manual de comunicação social conceito: blocos modulares

## <a name="catalog-of-roles"></a>Catálogo de funções

| Função | Descrição | Prova de responsabilidade de conceito (PoC) |
| --- | --- | --- |
| **Arquitetura de identidade / equipa de desenvolvimento** | Este agrupamento é normalmente Olá um que estruturar a solução de Olá, implementa prototypes, aprovações de unidades e, finalmente, entrega toooperations | Fornecem ambientes Olá e são Olá aqueles avaliação Olá diferentes cenários de perspetiva de capacidade de gestão de Olá |
| **Equipa de operações de identidade no local** | Gere Olá identidade diferentes origens no local: florestas do Active Directory, diretórios LDAP, sistemas de RH e fornecedores de identidade de Federação. | Fornece acesso tooon local recursos necessários para Olá cenários de PoC.<br/>Deve estar envolvidas ligeiramente possível|
| **Proprietários técnica da aplicação** | Proprietários técnicos de Olá diferente na nuvem, aplicações e serviços que integram com o Azure AD | Fornecem detalhes sobre aplicações SaaS (potencialmente instâncias de teste) |
| **Administrador Global do Azure AD** | Gere a configuração de Olá do Azure AD | Forneça credenciais com o serviço de sincronização de Olá tooconfigure. Normalmente, Olá mesma equipa como identidade arquitetura durante a PoC mas separe durante a fase de operações de Olá|
| **Equipa de base de dados** | Proprietários da infraestrutura de base de dados de Olá | Fornece acesso de ambiente do tooSQL (AD FS ou do Azure AD Connect) para os preparativos cenário específico.<br/>Deve estar envolvidas ligeiramente possível |
| **Equipa de rede** | Proprietários Olá da infraestrutura de rede | Fornecer acesso necessário ao nível de rede Olá para a sincronização de Olá servidores tooproperly acesso Olá as origens de dados e dos serviços cloud (regras de firewall, portas abertas, regras de IPSec etc.) |
| **Equipa de segurança** | Define a estratégia de segurança de Olá, analisa os relatórios de segurança de várias origens e segue em findings. | Fornecer segurança destino cenários de avaliação |

## <a name="common-prerequisites-for-all-building-blocks"></a>Pré-requisitos comuns para todos os blocos modulares

Seguem-se alguns pré-requisitos necessários para qualquer POC com o Azure AD Premium.

| Pré-requisito | Recursos |
| --- | --- |
| Inquilino do Azure do AD definido com uma subscrição do Azure válida | [Como inquilino tooget um Azure Active Directory](active-directory-howto-tenant.md)<br/>**Nota:** se já tiver um ambiente com licenças do Azure AD Premium, pode obter uma subscrição de extremidade zero navegando toohttps://aka.ms/accessaad <br/>Saiba mais em: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ e https://technet.microsoft.com/library/dn832618.aspx |
| Domínios definido e verificado | [Adicionar um tooAzure de nome de domínio personalizado do Active Directory](active-directory-domains-add-azure-portal.md)<br/>**Nota:** algumas cargas de trabalho, tais como o Power BI foi aprovisionou um inquilino do AD do azure em Olá abrange. toocheck se um determinado domínio inquilino tooa associados, navegue até toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration. Poderá ser necessário se obter uma resposta com êxito, em seguida, o domínio de Olá já se encontra atribuído tooa inquilino e assumir o controlo. Se assim for, contacte a Microsoft para obter orientações adicionais. Saiba mais sobre as opções de alimentar Olá em: [que é a inscrição Self-Service do Azure?](active-directory-self-service-signup.md) |
| Azure AD Premium ou EMS ativado de avaliação | [Azure Active Directory Premium livre durante um mês](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Atribuiu licenças do Azure AD Premium ou EMS tooPoC utilizadores | [Licença de si e aos utilizadores no Azure Active Directory](active-directory-licensing-get-started-azure-portal.md) |
| Credenciais de Administrador Global do AD do Azure | [Atribuir funções de administrador no Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md) |
| Opcional mas vivamente recomendado: ambiente de laboratório paralelas como contingência | [Pré-requisitos do Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Diretório sincronização - sincronização de Hash de palavra-passe (PHS) - nova instalação

Aproximada tempo tooComplete: uma hora para menos de 1000 utilizadores de PoC

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Servidor tooRun do Azure AD Connect | [Pré-requisitos do Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) |
| Segmente utilizadores POC, no Olá mesmo domínio e faça parte de um grupo de segurança e a UO | [Instalação personalizada do Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Funcionalidades do Azure AD Connect necessários para Olá POC são identificados | [Ligar o Active Directory com o Azure Active Directory - configurar a sincronização de funcionalidades](./connect/active-directory-aadconnect.md#configure-sync-features) |
| É necessário ter credenciais no local e ambientes de nuvem  | [Azure AD Connect: contas e permissões](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Transferir Olá a versão mais recente do Azure AD Connect | [Transferir o Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| Instalar o Azure AD Connect com o caminho de mais simples de Olá: Express <br/>1. Tempo de ciclo de sincronização de Olá UO toominimize toohello destino de filtro<br/>2. Escolha o conjunto de destino de utilizadores no grupo local de Olá.<br/>3. Implementar funcionalidades Olá necessárias Olá por outros temas POC | [Azure AD Connect: Instalação personalizada: domínio e a UO filtragem](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: Instalação personalizada: baseado em grupo filtragem](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: Integrar as identidades no local com o Azure Active Directory: configurar funcionalidades de sincronização](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Abra Olá do Azure AD Connect da IU e veja Olá com perfis concluída (importar, sincronização e exportação) | [Sincronização do Azure AD Connect: Scheduler](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Abra Olá [portal de gestão do Azure AD](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), aceda toohello painel de "Todos os utilizadores", adicione a coluna de "Origem da autoridade" e consulte que são apresentados os utilizadores de Olá, corretamente marcado como feitos "Windows Server AD" | [Portal de gestão do Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Considerações

1. Observe as considerações de segurança de Olá de sincronização de hash de palavra-passe [aqui](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Se a sincronização de hash de palavra-passe para os utilizadores de produção piloto definitively não é uma opção, em seguida, considere Olá alternativas os seguintes:
   * Crie utilizadores de teste no domínio de produção Olá. Certifique-se de que não sincronizar a qualquer outra conta
   * Mover tooan UAT ambiente
2.  Se quiser toopursue Federação, é valer a pena os custos de Olá toounderstand associado a uma solução federada com o fornecedor de identidade no local para além de Olá POC e medida que contra Olá beneficia está a procurar:
    * Faz parte de caminho críticos Olá, para que tenha toodesign para elevada disponibilidade
    * É um serviço no local, terá de planear toocapacity
    * É um serviço no local tem de toomonitor/manter/patch

Saiba mais: [identidade de compreender o Office 365 e o Azure Active Directory - identidade federada](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>Imagem corporativa

Aproximada tempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Ativos (imagens, logótipos, etc.); Para melhor visualização Certifique-se ativos de Olá ter Olá recomendado tamanhos. | [Adicionar página de início de sessão do tooyour Olá do Azure Active Directory imagem corporativa](active-directory-branding-custom-signon-azure-portal.md) |
| Opcional: Se o ambiente de Olá tem um servidor do ADFS, acesso tema do toohello servidor toocustomize web | [AD FS utilizador início de sessão personalização](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| Experiência de início de sessão do utilizador final do cliente computador tooperform |  |
| Opcional: Dispositivos móveis toovalidate experiência |  |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Aceda tooAzure AD Portal de gestão | [Portal de gestão do Azure AD - imagem corporativa da empresa](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Carregar recursos Olá para a página de início de sessão Olá (logótipo heroína logótipo pequeno, etiquetas, etc.). Opcionalmente, se tiver o AD FS, alinhar Olá mesmos ativos com as páginas de início de sessão do AD FS | [Adicionar publicidade tooyour início de sessão e painel de acesso da empresa: elementos personalizáveis](active-directory-add-company-branding.md) |
| Aguarde alguns minutos para ativado Olá alteração toofully |  |
| Inicie sessão com Olá POC utilizador credencial toohttps://myapps.microsoft.com |  |
| Confirmar Olá aspeto e funcionalidade no browser | [Adicionar publicidade tooyour início de sessão e painel de acesso da empresa](active-directory-add-company-branding.md) |
| Opcionalmente, confirme Olá aspeto e funcionalidade nos outros dispositivos |  |

### <a name="considerations"></a>Considerações

Se Olá antigo aspeto e funcionalidade permanece após a personalização de Olá esvaziar a cache do cliente de browser de Olá e repita a operação de Olá.

## <a name="group-based-licensing"></a>Baseado em grupo de licenciamento

Aproximada tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Todos os utilizadores POC fazem parte de um grupo de segurança (na nuvem ou no local) | [Crie um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Aceda toolicenses painel no Portal de gestão do Azure AD | [Portal de gestão do Azure AD: licenciamento](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Atribua o grupo de segurança do Olá licenças toohello com utilizadores POC. | [Atribuir licenças tooa grupo de utilizadores no Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Considerações

Em caso de problemas, visite demasiado[cenários, limitações e problemas conhecidos com a utilização de grupos toomanage licenciamento no Azure Active Directory](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>Configuração de SSO federado SaaS

Aproximada tempo tooComplete: 60 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Testar o ambiente de Olá disponível de aplicações SaaS. Neste guia, utilizamos ServiceNow como exemplo.<br/>Recomendamos vivamente que toouse um friction de toominimize de instância de teste no navegar qualidade de dados existente e mapeamentos. | Aceda toohttps://developer.servicenow.com/app.do#! / processo de Olá toostart de obter uma instância de teste de casa |
| Consola de gestão de ServiceNow de toohello de acesso de administrador | [Tutorial: Integração do Azure Active Directory com o ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Destino definido de utilizadores tooassign Olá aplicação. Recomenda-se um grupo de segurança que contenha os utilizadores de PoC Olá. <br/>Se criar grupo de Olá não for viável, em seguida, atribuir utilizadores Olá toodirectly toohello aplicação para Olá PoC | [Atribuir um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Partilha de atores do tutorial tooall Olá na Microsoft Documentation  | [Tutorial: Integração do Azure Active Directory com o ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Defina uma reunião de trabalho e siga os passos de tutorial Olá com cada ator. | [Tutorial: Integração do Azure Active Directory com o ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Atribua Olá aplicação toohello grupo identificado na Olá pré-requisitos. Se Olá POC tem o acesso condicional do âmbito de Olá, pode revê que mais tarde e adicionar MFA e semelhantes. <br/>Tenha em atenção de que isto irá iniciar no Olá processo de aprovisionamento (se configurada) |  [Atribuir um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Crie um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Utilizar tooadd de Portal de gestão do Azure AD ServiceNow aplicação a partir da Galeria| [Gestão do AD do Azure Portal: aplicações da empresa](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[Novidades na gestão de aplicações da empresa no Azure Active Directory](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| No painel "De sessão único-" da aplicação do ServiceNow ativar "baseados em SAML início de sessão" |  |
| Preencha os campos "Início de sessão no URL" e "Identificador" com o seu URL de ServiceNow<br/>Caixa de Olá verificação demasiado "tornar novo certificado ativa"<br/>e guardar definições |  |
| Abrir painel "Configurar ServiceNow" Olá parte inferior da Olá painel tooview personalizado instruções para si tooconfigure ServiceNow |  |
| Siga as instruções tooconfigure ServiceNow |  |
| No painel de "A aprovisionar" da aplicação do ServiceNow ativar o aprovisionamento "Automático" | [Gerir a conta de utilizador para aplicações da empresa no novo portal do Azure Olá de aprovisionamento](active-directory-enterprise-apps-manage-provisioning.md) |
| Aguarde alguns minutos enquanto ter concluído o aprovisionamento.  No Olá entretanto, pode verificar em Olá aprovisionamento relatórios |  |
| Inicie sessão no toohttps://myapps.microsoft.com/ como um utilizador de teste que tem acesso | [O que é Olá painel de acesso?](active-directory-saas-access-panel-introduction.md) |
| Clique no mosaico de Olá da aplicação Olá que acabou de criar. Confirmar o acesso |  |
| Opcionalmente, pode verificar Olá relatórios de utilização de aplicação. Tenha em atenção que é alguma latência de, pelo que necessita de toowait algum tráfego de Olá toosee hora nos relatórios de Olá. | [Relatórios de atividade de início de sessão no portal do Azure Active Directory Olá: utilização de aplicações geridas](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Políticas de retenção de relatórios do Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Considerações

1. Acima [Tutorial](active-directory-saas-servicenow-tutorial.md) refere-se a experiência de gestão tooold do Azure AD. Mas PoC baseia-se no [início rápido](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away) experiência.
2. Se a aplicação de destino Olá não está presente na Galeria de Olá, em seguida, pode utilizar "Traga a sua própria aplicação". Saiba mais: [são as novidades na gestão de aplicações da empresa no Azure Active Directory: adicionar aplicações personalizadas a partir de um local](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>Configuração de SSO de palavra-passe de SaaS

Aproximada tempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Ambiente de teste para aplicações SaaS. Um exemplo de SSO de palavra-passe é HipChat e o Twitter. Para qualquer outra aplicação, terá de Olá URL exato da página Olá com o formulário de início de sessão de html. | [Twitter no Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[HipChat no Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Contas para aplicações de Olá de teste. | [Inscrever-se no Twitter](https://twitter.com/signup?lang=en)<br/>[Inscrever-se gratuitamente: HipChat](https://www.hipchat.com/sign_up) |
| Destino definido de utilizadores tooassign Olá aplicação. Recomenda-se os utilizadores Olá segurança grupo contido. | [Atribuir um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Olá de toodeploy do computador de tooa de acesso de administrador local extensão do painel de acesso para o Internet Explorer, Chrome ou Firefox | [Extensão do painel de acesso de i/e](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensão de painel de acesso para Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensão de painel de acesso para o Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Instalar a extensão de browser Olá | [Extensão do painel de acesso de i/e](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensão de painel de acesso para Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensão de painel de acesso para o Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configurar a aplicação a partir da Galeria | [Novidades na gestão de aplicações da empresa no Azure Active Directory: Galeria de aplicações novas e melhoradas de Olá](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configurar a palavra-passe SSO | [Gerir o início de sessão para aplicações da empresa no novo portal do Azure Olá: início de sessão baseado em palavra-passe](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Atribua Olá aplicação toohello grupo identificado na Olá pré-requisitos | [Atribuir um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Inicie sessão no toohttps://myapps.microsoft.com/ como um utilizador de teste que tem acesso |  |
| Clique no mosaico de Olá da aplicação Olá que acabou de criar. | [O que é o painel de acesso de Olá?: SSO baseada em palavra-passe sem aprovisionamento de identidade](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Forneça a credencial de aplicação Olá | [O que é o painel de acesso de Olá?: SSO baseada em palavra-passe sem aprovisionamento de identidade](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Feche o browser Olá e início de sessão Olá repetida. Neste vez cerca utilizador Olá deverá ver a aplicação de toohello acesso totalmente integrado. |  |
| Opcionalmente, pode verificar Olá relatórios de utilização de aplicação. Tenha em atenção que é alguma latência de, pelo que necessita de toowait algum tráfego de Olá toosee hora nos relatórios de Olá. | [Relatórios de atividade de início de sessão no portal do Azure Active Directory Olá: utilização de aplicações geridas](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Políticas de retenção de relatórios do Azure Active Directory](active-directory-reporting-retention.md) |

### <a name="considerations"></a>Considerações

Se a aplicação de destino Olá não está presente na Galeria de Olá, em seguida, pode utilizar "Traga a sua própria aplicação". Saiba mais: [são as novidades na gestão de aplicações da empresa no Azure Active Directory: adicionar aplicações personalizadas a partir de um local](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Tenha em Olá atenção os seguintes requisitos:
   * Aplicação deve ter um URL de início de sessão conhecidos
   * página de início de sessão Olá deve conter um formulário HTML com um mais campos de texto que as extensões de browser Olá podem auto-preencher. No mínimo, Olá, esta deve conter o nome de utilizador e palavra-passe.

## <a name="saas-shared-accounts-configuration"></a>Configuração de contas de partilhada de SaaS

Aproximada tempo tooComplete: 30 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Olá, lista de aplicações de destino e Olá URLS de início de sessão exatos antecedência. Por exemplo, pode utilizar o Twitter. | [Twitter no Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Inscrever-se no Twitter](https://twitter.com/signup?lang=en) |
| Partilhado credenciais para esta aplicação SaaS. | [Partilha de contas de utilizar o Azure AD](active-directory-sharing-accounts.md)<br/>[Azure AD automatizada palavra-passe roll a ativação pós-falha para o Facebook, Twitter e LinkedIn agora em pré-visualização! -Blogue Enterprise Mobility and Security] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| As credenciais para, pelo menos, dois membros do agrupamento que irão aceder aos Olá a mesma conta. Têm de ser parte de um grupo de segurança. | [Atribuir um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Olá de toodeploy do computador de tooa de acesso de administrador local extensão do painel de acesso para o Internet Explorer, Chrome ou Firefox | [Extensão do painel de acesso de i/e](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensão de painel de acesso para Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensão de painel de acesso para o Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Instalar a extensão de browser Olá | [Extensão do painel de acesso de i/e](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Extensão de painel de acesso para Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Extensão de painel de acesso para o Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Configurar a aplicação a partir da Galeria | [Novidades na gestão de aplicações da empresa no Azure Active Directory: Galeria de aplicações novas e melhoradas de Olá](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Configurar a palavra-passe SSO | [Gerir o início de sessão para aplicações da empresa no novo portal do Azure Olá: início de sessão baseado em palavra-passe](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Atribua Olá aplicação toohello grupo identificado na Olá pré-requisitos ao atribuir-lhes credenciais | [Atribuir um utilizador ou grupo tooan enterprise uma aplicação no Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Inicie sessão como utilizadores de diferentes nessa aplicação acesso como Olá **mesmo partilhado conta.**  |  |
| Opcionalmente, pode verificar Olá relatórios de utilização de aplicação. Tenha em atenção que é alguma latência de, pelo que necessita de toowait algum tráfego de Olá toosee hora nos relatórios de Olá. | [Relatórios de atividade de início de sessão no portal do Azure Active Directory Olá: utilização de aplicações geridas](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Políticas de retenção de relatórios do Azure Active Directory](active-directory-reporting-retention.md) |


### <a name="considerations"></a>Considerações

Se a aplicação de destino Olá não está presente na Galeria de Olá, em seguida, pode utilizar "Traga a sua própria aplicação". Saiba mais: [são as novidades na gestão de aplicações da empresa no Azure Active Directory: adicionar aplicações personalizadas a partir de um local](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Tenha em Olá atenção os seguintes requisitos:
   * Aplicação deve ter um URL de início de sessão conhecidos
   * página de início de sessão Olá deve conter um formulário HTML com um mais campos de texto que as extensões de browser Olá podem auto-preencher. No mínimo, Olá, esta deve conter o nome de utilizador e palavra-passe.

## <a name="app-proxy-configuration"></a>Configuração de Proxy de aplicações

Aproximada tempo tooComplete: 20 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Do Microsoft Azure AD basic ou subscrição premium e um diretório do Azure AD para o qual é um administrador global | [Edições do Azure Active Directory](active-directory-editions.md) |
| Uma aplicação web alojadas no local que pretende tooconfigure para acesso remoto |  |
| Um servidor a executar o Windows Server 2012 R2 ou Windows 8.1 ou superior, em que pode instalar Olá conector do Proxy da aplicação | [Compreender os conectores de Proxy de aplicações do Azure AD](application-proxy-understand-connectors.md) |
| Se existir uma firewall no caminho de Olá, certifique-se de que está aberta, pelo que Olá que conector possa fazer HTTPS (TCP) solicita toohello Proxy de aplicações | [Ativar o Proxy de aplicação no portal do Azure de Olá: pré-requisitos do Proxy de aplicações](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Se a sua organização utiliza o proxy servidores tooconnect toohello internet, execute uma vista de olhos Olá blogue após a trabalhar com servidores de proxy no local existentes para obter detalhes sobre como tooconfigure-las | [Trabalhar com servidores de proxy no local existentes](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Instalar um conector no servidor de Olá | [Ativar o Proxy de aplicação no portal do Azure de Olá: Instale e registe Olá conector](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Publicar aplicações no local de Olá no Azure AD como uma aplicação de Proxy de aplicações | [Publicar aplicações através do Proxy de aplicações do Azure AD](application-proxy-publish-azure-portal.md) |
| Atribuir utilizadores de teste | [Publicar aplicações através do Proxy de aplicações do Azure AD: adicionar um utilizador de teste](application-proxy-publish-azure-portal.md#add-a-test-user) |
| Opcionalmente, configure uma experiência único início de sessão para os seus utilizadores | [Forneça o início de sessão único com o Proxy de aplicações do Azure AD](application-proxy-sso-azure-portal.md) |
| Aplicação de teste ao inscrever-se no portal de tooMyApps como utilizador atribuído | https://MyApps.microsoft.com |

### <a name="considerations"></a>Considerações

1. Embora sugerimos colocando conector Olá na sua rede empresarial, há casos quando o utilizador verá um melhor desempenho colocando-lo na nuvem de Olá. Saiba mais: [considerações sobre a topologia de rede ao utilizar o Proxy de aplicações do Azure Active Directory](application-proxy-network-topology-considerations.md)
2. Para obter mais detalhes de segurança e como esta opção fornece um acesso remoto seguro particularmente Consulte solução, mantendo apenas ligações de saída: [considerações de segurança para aceder remotamente a aplicações ao utilizar o Proxy de aplicações do Azure AD](application-proxy-security-considerations.md)

## <a name="generic-ldap-connector-configuration"></a>Configuração do conector LDAP genérico

Aproximada tempo tooComplete: 60 minutos

> [!IMPORTANT]
> Esta é uma configuração avançada que requerem familiarizado com o FIM/MIM. Se utilizada na produção, aconselhamos perguntas sobre esta configuração passar por [suporte Premier](https://support.microsoft.com/premier).

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| O Azure AD Connect instalado e configurado | Bloco modular: [sincronização de diretórios - sincronização de Hash de palavra-passe](#directory-synchronization--password-hash-sync-phs--new-installation) |
| Requisitos de reunião de instância ADLDS | [Referência técnica de conector LDAP genérica: Descrição geral do Olá genérico conector LDAP](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Lista de cargas de trabalho, o que os utilizadores estão a utilizar e atributos associados estas cargas de trabalho | [Sincronização do Azure AD Connect: atributos sincronizados tooAzure do Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Adicione o conector LDAP genérico | [Referência técnica de conector LDAP genérica: criar um novo conector](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Criar perfis de execução para o conector criado (importação completa, a importação delta, sincronização completa, as sincronizações de diferenças, exportação) | [Criar um perfil de execução de agente de gestão](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [A utilização de conectores com Olá do Azure AD Connect sincronização do Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Importação completa perfil de execução e certifique-se de que existem objetos no espaço de conector | [Procurar um objecto de espaço de conector](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[A utilização de conectores com Olá do Azure AD Connect sincronização do Service Manager: espaço de conector de pesquisa](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Criar regras de sincronização, de modo a que os objetos no Metaverso têm atributos necessários para cargas de trabalho | [Sincronização do Azure AD Connect: melhores práticas para alterar a configuração predefinida de Olá: alterações tooSynchronization regras](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Sincronização do Azure AD Connect: Noções sobre o aprovisionamento declarativo](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Sincronização do Azure AD Connect: Noções sobre expressões de aprovisionamento declarativo](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Iniciar o ciclo de sincronização completa | [Sincronização do Azure AD Connect: programador: iniciar o Programador de Olá](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| Em caso de problemas de fazer a resolução de problemas | [Resolver problemas de um objeto que não está a sincronizar tooAzure AD](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Verificar, se LDAP utilizador pode iniciar sessão e aceder à aplicação Olá | https://MyApps.microsoft.com |

### <a name="considerations"></a>Considerações

> [!IMPORTANT]
> Esta é uma configuração avançada que requerem familiarizado com o FIM/MIM. Se utilizada na produção, aconselhamos perguntas sobre esta configuração passar por [suporte Premier](https://support.microsoft.com/premier).

## <a name="groups---delegated-ownership"></a>Grupos - propriedade delegado

Aproximada tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Aplicação SaaS (SSO federado ou palavra-passe SSO) já configurada | Bloco modular: [SaaS configuração de SSO federado](#saas-federated-sso-configuration) |
| Grupo de nuvem que é atribuído acesso toohello aplicação #1 é identificado | Bloco modular: [SaaS configuração de SSO federado](#saas-federated-sso-configuration) <br/>[Crie um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| As credenciais para o proprietário do grupo de Olá estão disponíveis | [Gerir o acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md) |
| Identificou credenciais para Olá informações trabalho aceder Olá a aplicações | [O que é Olá painel de acesso?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Identificar o grupo de Olá que tiver sido concedido acesso toohello aplicação e configure o proprietário Olá determinado grupo| [Gerir definições de Olá para um grupo no Azure Active Directory](active-directory-groups-settings-azure-portal.md) |
| Inicie sessão como proprietário do grupo Olá, consulte a associação a grupos Olá no separador de grupos do painel de acesso | [Página de gestão de grupos do Active Directory do Azure](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Adicionar o técnico de informação de Olá pretende tootest |  |
| Inicie sessão como infotrabalhador Olá, confirme o mosaico Olá está disponível | [O que é Olá painel de acesso?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Considerações

Se a aplicação Olá tiver ativado o aprovisionamento, poderá ser necessário toowait alguns minutos para Olá aprovisionamento toocomplete antes de aceder à aplicação Olá como infotrabalhador Olá.

## <a name="saas-and-identity-lifecycle"></a>SaaS e o ciclo de vida de identidade

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Aplicação SaaS (SSO federado ou palavra-passe SSO) já configurada | Bloco modular: [SaaS configuração de SSO federado](#saas-federated-sso-configuration) |
| Grupo de nuvem que é atribuído acesso toohello aplicação #1 é identificado | Bloco modular: [SaaS configuração de SSO federado](#saas-federated-sso-configuration) <br/>[Crie um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Identificou credenciais para Olá informações trabalho aceder Olá a aplicações | [O que é Olá painel de acesso?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Remover utilizador Olá Olá grupo Olá aplicação está demasiado atribuído| [Gerir a associação de grupo para os utilizadores no seu inquilino do Azure Active Directory](active-directory-groups-members-azure-portal.md) |
| Aguarde alguns minutos para aprovisionamento automatizados. | [Automatizar o aprovisionamento de utilizadores de aplicações de SaaS no Azure AD: como funciona o trabalho de aprovisionamento automatizado?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| Numa sessão separada do browser, inicie sessão como o portal de aplicações do Olá informações trabalho toomy e confirme que mosaico está em falta | http://MyApps.microsoft.com |


### <a name="considerations"></a>Considerações

Utilize para tirar conclusões Olá PoC cenário tooleavers e/ou deixe de ausência cenários. Se o utilizador Olá obtém desativado no AD no local ou removida, há já não é uma forma toolog com toohello aplicação SaaS.

## <a name="self-service-access-tooapplication-management"></a>O acesso ao serviço tooApplication gestão gestão personalizada

Aproximada tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Identificar os utilizadores POC que irão solicitar acesso toohello aplicações, como parte do grupo de segurança de Olá | Bloco modular: [SaaS configuração de SSO federado](#saas-federated-sso-configuration) |
| Aplicação de destino implementada | Bloco modular: [SaaS configuração de SSO federado](#saas-federated-sso-configuration) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Aceda tooEnterprise painel de aplicações no Portal de gestão do Azure AD | [Portal de gestão do Azure AD: As aplicações da empresa](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| Configurar a aplicação de pré-requisitos com self-service | [Novidades na gestão de aplicações da empresa no Azure Active Directory: configurar o acesso de aplicação personalizada](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Inicie sessão como o portal de aplicações do Olá informações trabalho toomy | http://MyApps.microsoft.com |
| Tenha em atenção "+ Adicionar aplicação" botão op da página Olá. Utilizá-lo tooget acesso toohello aplicação |  |

### <a name="considerations"></a>Considerações

as aplicações de Olá escolhidas poderão ter de aprovisionamento os requisitos de, pelo que vai imediatamente toohello aplicação pode causar alguns erros. Se a aplicação Olá escolhida suporta o aprovisionamento com o azure ad e está configurado, pode utilizar esta opção como um oportunidade tooshow Olá todo fluxo trabalhar tooend de fim. Consulte o bloco modular de Olá para [SaaS configuração de SSO federado](#saas-federated-sso-configuration) para obter mais recomendações

## <a name="self-service-password-reset"></a>Reposição de palavra-passe Self-Service

Aproximada tempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Ative a gestão de palavra-passe self-service no seu inquilino. | [Azure Active Directory reposição palavra-passe para os administradores de TI](active-directory-passwords.md) |
| Permitir palavras-passe toomanage de repetição de escrita de palavras-passe no local. Note que isto requer específico do Azure AD Connect versões | [Pré-requisitos da Repetição de Escrita de Palavras-passe](active-directory-passwords-writeback.md) |
| Identifique os utilizadores de PoC de Olá que irão utilizar esta funcionalidade e certifique-se de que são membros de um grupo de segurança. utilizadores de Olá tem de ser a capacidade de Olá de demonstração de toofully não administradores | [Personalizar: Gestão de palavras-passe do Azure ao AD: restringir acesso toopassword reposição](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Navegue tooAzure AD Portal de gestão: repor a palavra-passe | [Portal de gestão do Azure AD: Reposição de palavra-passe](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Determine a política de reposição de palavra-passe de Olá. Para efeitos POC, pode utilizar chamada telefónica e Q & A. Recomenda-se tooenable registo toobe necessário no início de sessão tooaccess painel |  |
| Terminar sessão e inicie sessão como um técnico de informação |  |
| Fornecer dados de reposição de palavra-passe Self-Service Olá como configurado por passo 2 | http://aka.MS/ssprsetup |
| Browser de Olá fechar |  |
| Inicie o ao longo do processo de início de sessão de Olá como infotrabalhador Olá utilizada no passo 4 |  |
| Olá de reposição de palavra-passe | [Atualizar a sua própria palavra-passe: repor a minha palavra-passe](active-directory-passwords-update-your-own-password.md) |
| Tente iniciar sessão com a sua nova palavra-passe tooAzure AD, bem como os recursos tooon local |  |

### <a name="considerations"></a>Considerações

1. Se atualizar Olá do Azure AD Connect é toocause friction, em seguida, considere utilizá-lo contra contas na nuvem ou torná-lo uma demonstração em relação a um ambiente separada
2. Os administradores de Olá têm uma política diferente e utilizar Olá, admin palavra-passe do conta tooreset Olá poderá taint Olá PoC e fazer com que a confusão. Certifique-se de que utiliza um utilizador normal conta tootest Olá reposição de operações


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Azure multi-factor Authentication com as chamadas telefónicas

Aproximada tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Identificar os utilizadores POC que irão utilizar o MFA  |  |
| Telefone com boa receção de desafio MFA  | [O que é o Multi-Factor Authentication do Azure?](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Navegue demasiado painel "Utilizadores e grupos" no Portal de gestão do Azure AD | [Portal de gestão do Azure AD: Utilizadores e grupos](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| Escolha o painel de "Todos os utilizadores" |  |
| Na parte superior de Olá barra no botão "Multi-factor Authentication" de escolha | Direcionar o URL para o portal do Azure MFA: https://aka.ms/mfaportal |
| Nas definições do "Utilizador" Olá selecione Olá PoC utilizadores e ativá-los para a MFA | [Estados do Utilizador no Multi-Factor Authentication do Azure](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Inicie sessão como utilizador de PoC Olá e instruções sobre o processo de prova Olá  |  |

### <a name="considerations"></a>Considerações

1. passos seguintes Olá PoC neste bloco modular explicitamente a definição de MFA um utilizador em todos os inícios de sessão. Existem outras ferramentas, como o acesso condicional e a proteção de identidade que interagir com a MFA em mais direcionado cenários. Este será algo tooconsider quando mover de POC tooproduction.
2. passos de PoC Olá este bloco modular explicitamente estiver a utilizar as chamadas telefónicas como Olá método MFA para expedience. Como efetuar a transição de POC tooproduction, recomendamos a utilização de aplicações, tais como Olá [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) como o segundo fator sempre que possível.
Saiba mais: [rascunho publicação especial do NIST 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>Acesso condicional do MFA para aplicações SaaS

Aproximada tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Identifica PoC utilizadores tootarget Olá política. Estes utilizadores devem ter uma política de acesso condicional Olá de tooscope de grupo de segurança | [Configuração de SSO federado SaaS](#saas-federated-sso-configuration) |
| Aplicação SaaS já configurada |  |
| Utilizadores de PoC já estão atribuídos toohello aplicação |  |
| Utilizador POC credenciais toohello estão disponíveis |  |
| O utilizador POC está registado para MFA. Utilizar um telefone com boa receção | http://aka.MS/ssprsetup |
| Dispositivo na rede interna Olá. Endereço IP configurado no intervalo de endereço interno Olá | Localizar o endereço ip: https://www.bing.com/search?q=what%27s+my+ip |
| Dispositivo na rede externa Olá (pode ser um telefone com a rede móvel da operadora Olá) |  |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Aceda tooAzure AD Portal de gestão: painel de acesso condicional | [Portal de gestão do Azure AD: Acesso condicional](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Crie política de acesso condicional:<br/>-Os utilizadores de PoC destino em "Utilizadores e grupos"<br/>-Aplicação de PoC destino sob "Aplicações em nuvem"<br/>-Destino todas as localizações exceto aqueles fidedignas em "Condições" -> "Localizações" **Nota:** IPs fidedignos são configuradas no [MFA Portal](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)<br/>-Exigir autenticação multifator em "Conceder" | [Introdução ao acesso condicional no Azure Active Directory: passos de configuração de política](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Acesso aplicação a partir de dentro da rede empresarial | [Introdução ao acesso condicional no Azure Active Directory: teste Olá política](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Aplicação de acesso de rede pública | [Introdução ao acesso condicional no Azure Active Directory: teste Olá política](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Considerações

Se estiver a utilizar Federação, pode utilizar Olá do Olá no local o fornecedor de identidade (IdP) toocommunicate interior/exterior estado da rede empresarial com afirmações. Pode utilizar esta técnica sem ter de lista de Olá toomanage de endereços IP que possam ser tooassess complexa e gerir grandes organizações. A configuração, tem de conta para o cenário de "rede roaming" Olá (um utilizador registo a partir da rede interna Olá e ao comutadores com sessão iniciada localizações como num café) e certifique-se de que compreende as implicações de Olá. Saiba mais: [proteger recursos da nuvem com o Azure multi-factor Authentication e o AD FS: IPs fidedignos para utilizadores federados](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Privileged Identity Management (PIM)

Aproximada tempo tooComplete: 15 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Identificar Olá, admin global que farão parte do Olá POC PIM | [Começar a utilizar o Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| Identificar Olá, admin global que vai ser Olá administrador de segurança | [Começar a utilizar o Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Diferentes funções administrativas no Azure Active Directory PIM](active-directory-privileged-identity-management-roles.md) |
| Opcional: Confirme se os administradores globais Olá tem e-mail aceder tooexercise notificações de correio eletrónico no PIM | [O que é o Azure AD Privileged Identity Management?: configurar as definições de ativação de função Olá](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Início de sessão toohttps://portal.azure.com como um administrador global (GA) e o painel PIM Olá arranque de configuração. Olá Administrador Global que executa este passo é pré-propagadas como administrador de segurança de Olá.  Vamos chamar esta ator GA1 | [Utilizando o Assistente de segurança de Olá no Azure AD Privileged Identity Management](active-directory-privileged-identity-management-security-wizard.md) |
| Identificar Olá, admin global e movê-los a partir de tooeligible permanente. Deve ser um administrador separado da Olá utilizada no passo 1 para efeitos de clareza. Vamos chamar esta ator GA2 | [O Azure AD Privileged Identity Management: Como tooadd ou remover uma função de utilizador](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[O que é o Azure AD Privileged Identity Management?: configurar as definições de ativação de função Olá](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| Agora, inicie sessão como GA2 toohttps://portal.azure.com e tente alterar a "Definições de utilizador". Tenha em atenção algumas opções são desativadas. | |
| Num novo separador e no Olá mesma sessão como passo 3, navegue até toohttps://portal.azure.com agora e adicionar Olá PIM painel toohello dashboard. | [Como tooactivate ou desativar as funções no Azure AD Privileged Identity Management: adicionar a aplicação de Privileged Identity Management Olá](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| Função de Administrador Global do pedido de ativação toohello | [Como tooactivate ou desativar as funções no Azure AD Privileged Identity Management: ativar uma função](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| Tenha em atenção que se GA2 nunca inscreveu MFA, o registo para o MFA do Azure será necessário |  |
| Voltar atrás toohello separador original no passo 3 e clique no botão Atualizar Olá no browser Olá. Tenha em atenção que tem agora acesso toochange "Definições de utilizador" | |
| Opcionalmente, se os administradores globais tiverem o e-mail ativado, pode verificar GA1 e da GA2 pasta a receber e ver a notificação Olá da função de Olá a ser ativada |  |
| 8 Verifique o histórico de auditorias Olá e observar Olá relatório tooconfirm Olá ataques de elevação de GA2 é apresentado. | [O que é o Azure AD Privileged Identity Management?: função actividade de revisão](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Considerações

Esta capacidade é parte do Azure AD Premium P2 e/ou EMS E5

## <a name="discovering-risk-events"></a>Detetar eventos de risco

Aproximada tempo tooComplete: 20 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Dispositivo com browser Tor transferido e instalado | [Transferir Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Início de sessão do acesso tooPOC utilizador toodo Olá | [Azure Active Directory Identity Protection manual de comunicação social](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Browser abrir tor | [Transferir Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Inicie sessão no toohttps://myapps.microsoft.com com Olá conta de utilizador POC | [Azure Active Directory Identity Protection manual de comunicação social: simulando eventos de risco](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| Aguarde 5 a 7 minutos |  |
| Inicie sessão como um administrador global toohttps://portal.azure.com e abrir o painel do Olá Identity Protection | https://aka.MS/aadipgetstarted |
| Painel de eventos de risco Olá aberta. Deverá ver uma entrada em "Inícios de sessão de endereços IP anónimos"  | [Azure Active Directory Identity Protection manual de comunicação social: simulando eventos de risco](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Considerações

Esta capacidade é parte do Azure AD Premium P2 e/ou EMS E5

## <a name="deploying-sign-in-risk-policies"></a>Implementar políticas de início de sessão risco

Aproximada tempo tooComplete: 10 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Dispositivo com browser Tor transferido e instalado | [Transferir Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Acesso como um POC utilizador toodo Olá início de sessão de teste |  |
| O utilizador POC está registado com a MFA. Certifique-se de que toouse um telefone com boa receção | Bloco modular: [Azure multi-factor Authentication com as chamadas telefónicas](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Inicie sessão como um administrador global toohttps://portal.azure.com e abra o painel do Olá Identity Protection | https://aka.MS/aadipgetstarted |
| Ative uma política de início de sessão do risco da seguinte forma:<br/>-Atribuído a: utilizador POC<br/>-Condições: Início de sessão risco médio ou superior (início de sessão anónimo localização é considerado como um nível de risco média)<br/>-Controlos: Exigir a MFA | [Azure Active Directory Identity Protection manual de comunicação social: início de sessão risco](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Browser abrir tor | [Transferir Tor Browser](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Toohttps://myapps.microsoft.com com Olá PoC conta de utilizador de início de sessão |  |
| Olá aviso desafio MFA | [Início de sessão experiências com o Azure AD Identity Protection: recuperação de risco início de sessão](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Considerações

Esta capacidade é parte do Azure AD Premium P2 e/ou E5 do EMS. toolearn mais informações sobre eventos de risco visitam: [eventos de risco do Azure Active Directory](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Configurar a autenticação baseada em certificado

Aproximada tempo toocomplete: 20 minutos

### <a name="pre-requisites"></a>Pré-requisitos

| Pré-requisito | Recursos |
| --- | --- |
| Dispositivos com o certificado de utilizador aprovisionado (Windows, iOS ou Android) da PKI de empresa | [Implementar certificados de utilizador](https://msdn.microsoft.com/library/cc770857.aspx) |
| Domínio do Azure AD federadas com o AD FS | [Azure AD Connect e a federação](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Descrição geral de serviços de certificados do Active Directory](https://technet.microsoft.com/library/hh831740.aspx)|
| Para dispositivos iOS ter a aplicação Microsoft Authenticator instalada | [Introdução à aplicação do Microsoft Authenticator Olá](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Passos

| Passo | Recursos |
| --- | --- |
| Ativar "Autenticação de certificados" no ADFS | [Configurar políticas de autenticação: tooconfigure autenticação principal global no Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Opcional: Ative a autenticação de certificado no Azure AD para clientes do Exchange Active Sync | [Introdução à autenticação baseada em certificado no Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Navegue tooAccess painel e autenticar com o certificado de utilizador | https://MyApps.microsoft.com |

### <a name="considerations"></a>Considerações

toolearn mais informações sobre limitações desta implementação visitam: [ADFS: autenticação de certificado com o Azure AD & do Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> Posse do certificado de utilizador deve ser protegido. A pela gestão de dispositivos ou com o PIN em caso de smart cards.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
