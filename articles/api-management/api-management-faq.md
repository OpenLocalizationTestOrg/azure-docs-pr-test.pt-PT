---
title: "aaaAzure FAQ de gestão de API | Microsoft Docs"
description: "Saiba Olá responde a questões toocommon, padrões e melhores práticas na API Management do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Perguntas mais frequentes sobre gestão de API do Azure
Obter Olá respostas toocommon perguntas, padrões e melhores práticas para a API Management do Azure.

## <a name="contact-us"></a>Contacte-nos
* [Como pode posso fazer a equipa de gestão de API do Microsoft Azure Olá uma pergunta?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Perguntas mais frequentes
* [O que o significa de uma funcionalidade está em pré-visualização?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Como proteger a ligação de Olá entre o gateway de gestão de API de Olá e os meus serviços de back-end?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [Como copiar o meu serviço instância tooa nova instância da API Management?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [Posso gerir os meus instância da API Management programaticamente?](#can-i-manage-my-api-management-instance-programmatically)
* [Como adicionar um grupo de administradores do utilizador toohello?](#how-do-i-add-a-user-to-the-administrators-group)
* [Por que motivo é política Olá que pretendo tooadd disponível no editor de políticas de Olá?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [Como utilizar o controlo de versões de API na API Management?](#how-do-i-use-api-versioning-in-api-management)
* [Como configurar vários ambientes numa única API?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [Pode utilizar SOAP com a API Management?](#can-i-use-soap-with-api-management)
* [É constante de endereço IP de gateway de gestão de API de Olá? Posso utilizá-lo em regras de firewall?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [Pode configurar um servidor de autorização do OAuth 2.0 com a segurança do AD FS?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [Que método de encaminhamento utilizar a API Management em localizações geográficas de toomultiple implementações?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Pode utilizar um toocreate de modelo do Azure Resource Manager uma instância de serviço de API Management?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [Pode utilizar um certificado SSL autoassinado para um back-end?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Por que motivo recebo uma falha de autenticação ao tentar tooclone um repositório de GIT?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [Gestão de API funciona com o Azure ExpressRoute?](#does-api-management-work-with-azure-expressroute)
* [Por que motivo é necessário uma sub-rede dedicada no Gestor de recursos de estilo VNETs quando a API Management está implementada para-las?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [O que é o tamanho de sub-rede mínima de Olá necessário ao implementar a API Management para uma VNET?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [Pode mover um serviço de API Management a partir de uma subscrição tooanother?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Existem restrições ou problemas conhecidos com importar meu API?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>Como pode posso fazer a equipa de gestão de API do Microsoft Azure Olá uma pergunta?
Pode contactar-nos através de uma destas opções:

* Publique as suas perguntas nos nossos [fórum MSDN de gestão de API](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Enviar um e-mail demasiado<mailto:apimgmt@microsoft.com>.
* Envie-num pedido de funcionalidade em Olá [fórum de comentários do Azure](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>O que o significa de uma funcionalidade está em pré-visualização?
Quando é uma funcionalidade de pré-visualização, significa está a procura ativamente comentários sobre a forma como a funcionalidade de Olá está a funcionar para si. Uma funcionalidade em pré-visualização é funcionalmente concluída, mas é possível que iremos irá efetuar uma última alteração no comentários toocustomer de resposta. Recomendamos que não dependem uma funcionalidade que está em pré-visualização no seu ambiente de produção. Se tiver quaisquer comentários sobre as funcionalidades de pré-visualização, indique através de uma das opções de contacto Olá no [como pode posso fazer equipa de gestão de API do Microsoft Azure Olá uma pergunta?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Como proteger a ligação de Olá entre o gateway de gestão de API de Olá e os meus serviços de back-end?
Tem várias opções de ligação de Olá de toosecure entre o gateway de gestão de API de Olá e os serviços de back-end. Pode:

* Utilize a autenticação básica de HTTP. Para obter mais informações, consulte [as definições da API configurar](api-management-howto-create-apis.md#configure-api-settings).
* Utilizar a autenticação mútua de SSL, conforme descrito em [como toosecure back-end de serviços utilizando a autenticação de certificado de cliente na API Management do Azure](api-management-howto-mutual-certificates.md).
* Utilize Adicionar à lista branca IP do seu serviço de back-end. Se tiver uma instância de gestão de API de camada Standard ou Premium, o endereço IP de Olá do gateway de Olá permanece constante. Pode definir a lista branca tooallow este endereço IP. Pode obter o endereço IP Olá da sua instância da API Management no Olá Dashboard no Olá portal do Azure.
* Ligar o seu tooan de instância de API Management rede Virtual do Azure.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>Como copiar o meu serviço instância tooa nova instância da API Management?
Tem várias opções se pretender toocopy uma API Management instância tooa nova instância. Pode:

* Utilizar Olá cópia de segurança e restaurar a função na API Management. Para obter mais informações, consulte [como recuperação de desastres tooimplement utilizando o serviço de cópia de segurança e restaurar na API Management do Azure](api-management-howto-disaster-recovery-backup-restore.md).
* Criar a suas próprias cópia de segurança e restaurar a funcionalidade utilizando Olá [API de REST de gestão de API](https://msdn.microsoft.com/library/azure/dn776326.aspx). Utilizar Olá toosave de REST API e restaurar entidades Olá de instância de serviço Olá que pretende.
* Transferir a configuração do serviço Olá utilizando o Git e, em seguida, carregá-la tooa nova instância. Para obter mais informações, consulte [como toosave e configurar a configuração do serviço de API Management utilizando o Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>Posso gerir os meus instância da API Management programaticamente?
Sim, pode gerir API Management através de programação utilizando:

* Olá [API de REST de gestão de API](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Olá [SDK de biblioteca do gestão de serviço do Microsoft Azure ApiManagement](http://aka.ms/apimsdk).
* Olá [implementação de serviços](https://msdn.microsoft.com/library/mt619282.aspx) e [gestão de serviço](https://msdn.microsoft.com/library/mt613507.aspx) cmdlets do PowerShell.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>Como adicionar um grupo de administradores do utilizador toohello?
Eis como pode adicionar um grupo de administradores de toohello de utilizador:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Visite o grupo de recursos de toohello que tenha a instância da API Management Olá pretende tooupdate.
3. Na API Management, atribuir Olá **contribuinte de gestão de Api** utilizador toohello de função.

Agora Olá recém-adicionada contribuinte pode utilizar o Azure PowerShell [cmdlets](https://msdn.microsoft.com/library/mt613507.aspx). Eis como toosign na como administrador:

1. Olá utilize `Login-AzureRmAccount` toosign cmdlet no.
2. Definir Olá contexto toohello subscrição que tenha o serviço de Olá utilizando `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Obter um URL de início de sessão único utilizando `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Utilize o portal de administração do Olá URL tooaccess Olá.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Por que motivo é política Olá que pretendo tooadd disponível no editor de políticas de Olá?
Se a política de Olá que pretende que aparece tooadd desativada ou sombreados no editor de políticas de Olá, lembre-se de que está no âmbito correto Olá política Olá. Cada declaração de política foi concebida para toouse âmbitos específicos e secções de política. secções de política de Olá tooreview e âmbitos de uma política, consulte a utilização da política de Olá secção [políticas de gestão de API](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>Como utilizar o controlo de versões de API na API Management?
Tem algumas opções toouse API controlo de versões na API Management:

* Na API Management, pode configurar as diferentes versões toorepresent APIs. Por exemplo, poderá ter duas APIs diferentes, MyAPIv1 e MyAPIv2. Um programador pode escolher a versão de Olá que Olá programador pretende toouse.
* Também pode configurar a sua API com um URL de serviço não inclui um segmento de versão, por exemplo, https://my.api. Em seguida, configure um segmento de versão de cada operação [Rewrite URL](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) modelo. Por exemplo, pode ter uma operação com um [modelo URL](api-management-howto-add-operations.md#url-template) chamado /resource e um [Rewrite URL](api-management-howto-add-operations.md#rewrite-url-template) modelo chamado/v1/recursos. Pode alterar o valor de segmento de versão Olá em separado para cada operação.
* Se quiser tookeep um segmento de versão "predefinido" no URL do serviço Olá da API, no selecionada operations, definir uma política que utiliza Olá [definir o serviço de back-end](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) caminho da política toochange Olá pedido de back-end.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Como configurar vários ambientes numa única API?
tooset segurança vários ambientes, por exemplo, um ambiente de teste e ambiente de produção, uma única API, tem duas opções. Pode:

* Olá, anfitrião APIs diferentes no mesmo inquilino.
* Anfitrião Olá as mesmas APIs em diferentes inquilinos.

### <a name="can-i-use-soap-with-api-management"></a>Pode utilizar SOAP com a API Management?
[Pass-through SOAP](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) suporte está agora disponível. Os administradores podem importar Olá WSDL do seu serviço de SOAP e API Management do Azure irá criar um front-end SOAP. Documentação do portal de programador, a consola de teste, políticas e análise está disponível para os serviços SOAP.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>É constante de endereço IP de gateway de gestão de API de Olá? Posso utilizá-lo em regras de firewall?
Em camadas Standard e Premium Olá, Olá endereço IP público (VIP) do inquilino de gestão de API de Olá é estático para a duração de Olá do inquilino Olá, com algumas exceções. alterações do endereço IP de Olá nestas circunstâncias:

* serviço de Olá é eliminado e, em seguida, voltar a criar.
* subscrição do serviço de Olá [suspenso](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) ou [avisado](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (por exemplo, para nonpayment) e, em seguida, reinstated.
* Adicionar ou remover a rede Virtual do Azure (pode utilizar a rede Virtual apenas ao hello programador e o escalão Premium).

Para implementações de multirregião, Olá as alterações do endereço regional se região Olá vacated e, em seguida, reinstated (pode utilizar a implementação de multirregião apenas no escalão Premium de Olá).

Inquilinos de escalão Premium que estão configurados para implementação de multirregião são atribuídos um endereço IP público por região.

Pode obter o endereço (ou endereços IP, numa implementação de multirregião) na página de inquilino Olá na Olá portal do Azure.

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>Pode configurar um servidor de autorização do OAuth 2.0 com a segurança do AD FS?
toolearn como tooconfigure um servidor de autorização do OAuth 2.0 com a segurança de serviços de Federação do Active Directory (AD FS), ver [utilizando ADFS na API Management](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>Que método de encaminhamento utilizar a API Management em localizações geográficas de toomultiple implementações?
Utiliza a API Management Olá [método de encaminhamento de tráfego de desempenho](../traffic-manager/traffic-manager-routing-methods.md#priority) em localizações geográficas de toomultiple de implementações. Tráfego de entrada é encaminhado toohello gateway da API mais próximo. Se uma região ficar offline, o tráfego de entrada é automaticamente encaminhadas toohello gateway mais próximo seguinte. Saiba mais sobre os métodos de encaminhamento no [métodos de encaminhamento do Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>Pode utilizar um toocreate de modelo do Azure Resource Manager uma instância de serviço de API Management?
Sim. Consulte Olá [serviço de gestão de API do Azure](http://aka.ms/apimtemplate) modelos de início rápido.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>Pode utilizar um certificado SSL autoassinado para um back-end?
Sim. Eis como toouse um autoassinado SSL Secure Sockets Layer () do certificado para um back-end:

1. Criar um [back-end](https://msdn.microsoft.com/library/azure/dn935030.aspx) entidade utilizando a API Management.
2. Conjunto Olá **skipCertificateChainValidation** propriedade demasiado**verdadeiro**.
3. Se já não pretender tooallow os certificados autoassinados, eliminar a entidade de back-end Olá ou defina Olá **skipCertificateChainValidation** propriedade demasiado**falso**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>Por que motivo recebo uma falha de autenticação ao tentar tooclone um repositório de Git?
Se utilizar o Gestor de credenciais do Git, ou se estiver a tentar tooclone um repositório de Git, utilizando o Visual Studio, poderá executar para um problema conhecido com a caixa de diálogo de credenciais de Windows hello. caixa de diálogo Olá limita carateres de too127 de comprimento de palavra-passe e trunca a palavra-passe geradas pelo Microsoft hello. Estamos a trabalhar encurtar a palavra-passe de Olá. Por agora, utilize Git Bash tooclone o repositório de Git.

### <a name="does-api-management-work-with-azure-expressroute"></a>Gestão de API funciona com o Azure ExpressRoute?
Sim. Gestão de API funciona com o Azure ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Por que motivo é necessário uma sub-rede dedicada no Gestor de recursos de estilo VNETs quando a API Management está implementada para-las?
requisito de sub-rede dedicado Olá para a API de gestão provém de facto Olá, que está incorporada no modelo de implementação clássica (PAAS V1 layer). Enquanto pode implementar para uma VNET do Resource Manager (V2 layer), existem consequências toothat. Olá modelo de implementação clássico no Azure não é fortemente conjugado com o modelo do Resource Manager Olá e, se criar um recurso na camada V2, a camada de V1 Olá desconheça-lo e problemas podem acontecer, tais como a API Management tentar toouse um IP que já foi atribuído tooa NIC (criada no V2).
toolearn mais informações sobre a diferença dos modelos clássica e Resource Manager no Azure Consulte demasiado[diferença nos modelos de implementação](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>O que é o tamanho de sub-rede mínima de Olá necessário ao implementar a API Management para uma VNET?
tamanho de sub-rede mínimo Olá necessário toodeploy a API Management está [/29](../virtual-network/virtual-networks-faq.md#configuration), que é o tamanho da sub-rede mínimo Olá que suporte do Azure.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>Pode mover um serviço de API Management a partir de uma subscrição tooanother?
Sim. como, consulte toolearn [mover recursos tooa novo grupo de recursos ou subscrição](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Existem restrições ou problemas conhecidos com importar meu API?
[Problemas e restrições conhecidos](api-management-api-import-restrictions.md) para abrir API(Swagger), WSDL e WADL formatos.
