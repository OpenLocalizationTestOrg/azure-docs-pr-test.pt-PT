---
title: "melhores práticas de segurança do aaaAzure Service Fabric | Microsoft Docs"
description: "Este artigo fornece um conjunto de melhores práticas de segurança do Azure Service Fabric."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Azure Service Fabric melhores práticas de segurança
Implementar uma aplicação no Azure é rápido, fácil e económica. Antes de implementar a aplicação na nuvem no toohave útil produção constitui uma melhor prática tooassist ao avaliar a aplicação relativamente a uma lista de melhores práticas recomendadas e essenciais.

Azure Service Fabric é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implementar e gerir micro-serviços escaláveis e fiáveis. Service Fabric também aborda os desafios significativos de Olá no desenvolvimento e gestão de aplicações em nuvem. Permite, assim, que os programadores e administradores evitem problemas complexos de infraestrutura e se concentrem na implementação de cargas de trabalho exigentes e fundamentais que sejam dimensionáveis, fiáveis e geríveis. 

Para cada melhor prática, vamos explicar:

-   Que Olá melhor prática é
-   Motivo pelo qual pretende tooenable que melhor prática
-   Se falhar tooenable Olá prática recomendada, que poderá ser resultado de Olá
-   Como pode saber tooenable Olá prática recomendada

Atualmente temos Olá seguindo os procedimentos de segurança do Azure Service Fabric:

-   Utilizar o modelo do Azure Manager (Arm) de recursos e cluster segura do Service Fabric do Azure PowerShell Module toocreate
-   Utilize certificados x. 509
-   Configurar políticas de segurança
-   Configuração de segurança do Reliable Actors
-   Configurar o SSL para recursos de infraestrutura de serviço do Azure
-   Isolamento de rede/segurança com recursos de infraestrutura do serviço do Azure
-   Configurar um cofre de chaves de segurança
-   Atribuir utilizadores tooroles


## <a name="best-practices-for-securing-your-cluster"></a>Melhores práticas para proteger o cluster

**Visão geral**

Utilize sempre um cluster seguro
-   Segurança de cluster – utilizar certificados
-   Utilizar o acesso de cliente (Admin e só de leitura) – AAD

Utilizar implementações automáticas
-   Utilizar scripts toogenerate, implementar e, rollover de segredos
-   Manter segredos Olá no KV, utilizar o AD para todos os outro acesso de cliente
-   Não existem humanos devem ter acesso toothem sem autenticação.

Além disso, considere o seguinte Olá:
-   Criar DMZ utilizar grupos de segurança de rede (NSGs)
-   Utilizar tooRDP de servidores de ir para as VMs do cluster ou toomanage o cluster

Clusters tem de ser utilizadores protegidos tooprevent não autorizado a ligação de tooyour cluster, sobretudo quando tem cargas de trabalho de produção em execução no mesmo. Embora seja possível toocreate um cluster não segura, se o fizer, permite que os utilizadores anónimos tooconnect tooit, se expõe toohello de pontos finais de gestão Internet pública.

As tecnologias utilizadas tooimplement esses cenários. Olá [cenários de segurança do cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) são:

-   Nó de nó segurança este protege comunicação entre computadores num cluster de Olá e Olá VMs. Isto garante que apenas os computadores que estejam autorizados toojoin cluster de Olá podem participar em aplicações e serviços em cluster Olá de alojamento.
Podem utilizar clusters em execução no Azure ou autónomo clusters em execução no Windows [certificado de segurança](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) ou [segurança do Windows](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security) para máquinas de Windows Server.
-   Nó de cliente segurança este além de proteger a comunicação entre um cliente de Service Fabric e os nós no cluster de Olá individuais.
-   O controlo de acesso baseado em funções (RBAC) - Especifique o Olá administrador e utilizador cliente funções momento Olá da criação do cluster, fornecendo identidades separadas (certificados, etc. do AAD) para cada.
-   Recomendações de segurança-clusters do Azure, é recomendado que utilize certificados e os clientes de tooauthenticate de segurança do AAD para o nó de nó de segurança.

tooconfigure Olá autónomo cluster do Windows, consulte [configurar definições para o cluster do windows autónomo](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest).

Utilize modelos Azure Resource Manager e o cluster segura do Service Fabric do Azure PowerShell Module toocreate.
Um guia passo a passo guia-o, através da configuração de um Azure Service Fabric segura de cluster no Azure utilizando o Gestor de recursos do Azure está disponível [aqui](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm).

Utilizar toocustomize de modelo do Azure Resource Manager Olá o cluster
-   Armazenamento gerido pelo programa de configuração para os VHDs de VM

Utilizar Olá do Azure Resource Manager modelo toodrive alterações tooyour grupo de recursos
-   Gestão de configuração fácil
-   Auditoria

Tratar a configuração do cluster como código
-   Ser detalhado na verificação de configurações de Olá escolha toodeploy
-   Evite utilizar comandos implícita tootweak os recursos diretamente

Muitos aspetos do Olá [ciclo de vida de aplicação de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) podem ser automatizadas. [Módulo do serviço de recursos de infraestrutura do Azure PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package) automatiza tarefas comuns para implementar, atualizar, remover e testar aplicações do Azure Service Fabric. Gerido e APIs de HTTP para gestão de aplicações também estão disponíveis.

## <a name="use-x509-certificates"></a>Utilize certificados x. 509
Clusters sempre devem ser protegidos com certificados x. 509 ou de segurança do Windows. Segurança está configurada apenas no momento de criação do cluster e não é possível tooenable segurança após Olá cluster é criado.

Se especificar um [certificado de cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), defina o valor de Olá de ClusterCredentialType tooX509. Se estiver a especificar o certificado de servidor para ligações externos, defina Olá ServerCredentialType tooX509.

-   Certificados utilizados em clusters que executam cargas de trabalho de produção devem ser criados utilizando um serviço de certificado de servidor Windows corretamente configurado ou obtidos a partir de um aprovados autoridade de certificação (CA).
-   Nunca utilize qualquer temporário ou certificados de teste em produção que são criados com ferramentas como o MakeCert.exe.
-   Pode utilizar um certificado autoassinado, mas deve apenas fazer para clusters de teste e não na produção.

Se o cluster de Olá é não segura. Qualquer pessoa pode ligar de forma anónima e efetuar operações de gestão, para que os clusters de produção sejam sempre protegidos ao utilizar certificados X.509 ou segurança do Windows.

toolearn mais como ver certificados tooenable no cluster do service fabric, [adicionar ou remover certificados para um cluster do service fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure).

## <a name="configure-security-policies"></a>Configurar políticas de segurança
Serviço de recursos de infraestrutura também ajuda a Olá segura recursos utilizados por aplicações momento Olá da implementação em contas de utilizador de Olá – por exemplo, ficheiros, diretórios e certificados. Isto faz com que aplicações em execução, mesmo num ambiente alojado partilhado, mais segura entre si.

-   Utilize um utilizador ou grupo de domínio do Active Directory: pode executar o serviço Olá sob credenciais de Olá para uma conta de utilizador ou grupo do Active Directory. Este é o Active Directory no local dentro do seu domínio e não está no Azure Active Directory (Azure AD). Através da utilização de um utilizador de domínio ou grupo, em seguida, pode aceder a outros recursos no domínio Olá (por exemplo, as partilhas de ficheiros) tem sido concedidos permissões.

-   Atribuir uma política de acesso de segurança para pontos finais HTTP e HTTPS: se aplicam-se de um serviço de tooa RunAs política e o manifesto de serviço Olá declara recursos de ponto final com o protocolo de Olá HTTP, tem de especificar um tooensure SecurityAccessPolicy que portas atribuídos toothese pontos finais estão corretamente acesso controlada listados para Olá conta RunAs de utilizador que executa o serviço de Olá em. Caso contrário, o http.sys não tem acesso toohello serviço e obter falhas com chamadas de cliente de Olá.
toolearn mais ativar políticas de segurança no service fabric, consulte [configurar políticas de segurança para a sua aplicação](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security).

## <a name="reliable-actors-security-configuration"></a>Configuração de segurança do Reliable Actors
Serviço de recursos de infraestrutura Reliable Actors é uma implementação padrão de conceção de ator Olá. Tal como acontece com quaisquer padrão de conceção de software, a decisão de Olá se toouse um padrão específico efetuado com base em se pretende ou não um software design problema encaixa padrão Olá.

Como orientações gerais, tenha em atenção Olá ator padrão toomodel seu cenário ou um problema se:
-   O espaço de problema envolve um grande número (milhares ou mais) de pequenas, independentes e isoladas unidades de estado e a lógica.
-   Pretende toowork com single-threaded objetos que não necessitam de significativa interação de componentes externos, incluindo a consultar o estado através de um conjunto de atores.
-   As instâncias de ator não irão bloquear os chamadores com atrasos imprevisíveis ao emitir operações de e/s.

No Service Fabric, atores são implementados na estrutura de Reliable Actors Olá: uma arquitetura de aplicações baseados no padrão de ator incorporada de [Service Fabric Reliable Services](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction). Cada serviço de Atores fiável que escreve é realmente uma particionadas, com monitorização de estado fiável serviço.
Cada ator está definida como uma instância de um tipo de ator, forma toohello idênticos objeto .NET é uma instância de um tipo .NET. Por exemplo, poderá existir um tipo de ator que implementa a funcionalidade de Olá de um cálculo e podem existir muitas atores desse tipo que estão distribuídos em vários nós de um cluster. Cada essa ator é identificado de forma exclusiva por um ID de actor.

[Configurações de segurança do replicador](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) são canal de comunicação de Olá toosecure utilizado que é utilizado durante a replicação. Isto significa que os serviços não é possível ver uns dos outros tráfego de replicação, garantir que os dados de Olá efetuada elevados também estão segurados. Por predefinição, uma secção de configuração de segurança vazio impede a segurança da replicação.
Configurações do replicador configurar replicador Olá que é responsável por verificar o estado de fornecedor de estado de Ator Olá altamente fiável.

## <a name="configure-ssl-for-azure-service-fabric"></a>Configurar o SSL para recursos de infraestrutura de serviço do Azure

Autenticação de servidor: [Authenticates](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) Olá cliente de gestão do cluster gestão pontos finais tooa, para que hello cliente de gestão sabe que está a falar com toohello real cluster. Este certificado também fornece um [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) para Olá API de gestão HTTPS e para o Service Fabric Explorer através de HTTPS.
Tem de obter um nome de domínio personalizado para o cluster. Quando solicitar um certificado a partir de uma AC, hello nome do requerente do certificado tem de corresponder ao nome de domínio personalizado de Olá que utilizar para o cluster.

tooconfigure SSL para uma aplicação, terá primeiro tooget um certificado SSL assinado por uma autoridade de certificação (CA), uma terceiros fidedigna, que emite certificados para esta finalidade. Se já tiver uma, terá de tooobtain um de uma empresa que sells certificados SSL.

certificado Olá tem de cumprir os requisitos para certificados SSL no Azure de Olá:
-   certificado de Olá tem de conter uma chave privada.
-   certificado de Olá tem de ser criado para a troca de chaves, tooa exportável ficheiro Personal Information Exchange (. pfx).
-   Olá nome do requerente do certificado deve corresponder ao serviço de nuvem do Olá domínio utilizado tooaccess Olá. Não é possível obter um certificado SSL a partir de uma autoridade de certificação (AC) para o domínio de cloudapp.net Olá. Tem de adquirir uma toouse de nome de domínio personalizado ao seu serviço de acesso. Quando solicitar um certificado a partir de uma AC, nome do requerente do certificado Olá tem de corresponder ao hello domínio personalizado nome utilizado tooaccess a aplicação. Por exemplo, se o nome de domínio personalizado for contoso.com seria pedir um certificado da AC para **. contoso.com** ou **www.contoso.com.**
-   certificado de Olá tem de utilizar um mínimo de encriptação de 2048 bits.

HTTP está inseguras e é requerente tooeavesdropping ataques porque hello dados a serem transferidos a partir do servidor de web Olá web browser toohello ou entre outros pontos finais, são transmitidas em texto não encriptado. Isto significa que os atacantes podem intercetar e ver dados confidenciais, tais como os detalhes do cartão de crédito e inícios de sessão de conta. Quando os dados são enviados ou publicados através de um browser através de HTTPS, o SSL garante que essas informações são encriptado e seguros a partir de interception.

toolearn mais, consulte o artigo, [configurar o SSL para a aplicação do azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate).

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Isolamento de rede/segurança com recursos de infraestrutura do serviço do Azure
Utilize [modelo Azure Resource Manager (ARM)](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) como um exemplo de como configurar um nodetype três cluster segura e toocontrol Olá tráfego de rede de entrada e saída utilizar grupos de segurança de rede.

modelo de Olá tem um grupo de segurança de rede para cada um dos Olá escala set(VMSS) toocontrol Olá tráfego da máquina virtual que entra e sai Olá VMSS. Por predefinição, as regras de Olá são configuradas tooallow que todas Olá tráfego necessário por Olá sistema serviços e Olá aplicação portas especificadas no modelo de Olá. Reveja as regras e efetuar alterações toofit às suas necessidades, incluindo adicionar quaisquer novos para as suas aplicações.

Para obter mais informações, consulte [Azure Service Fabric – cenários comuns de redes](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking).

## <a name="set-up-a-key-vault-for-security"></a>Configurar um cofre de chaves de segurança
Os certificados são utilizados no Service Fabric tooprovide autenticação e encriptação toosecure diferentes aspetos de um cluster e respetivas aplicações.

Service Fabric utiliza toosecure de certificados x. 509 um cluster e fornece funcionalidades de segurança da aplicação. Utilizar o Cofre de chaves demasiado[gerir certificados](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) para clusters de Service Fabric no Azure. Quando um cluster é implementado no Azure, o fornecedor de recursos do Azure de Olá que é responsável pela criação de clusters de Service Fabric obtém certificados a partir do Cofre de chaves e instala-los num cluster de Olá VMs.

Olá relação entre [Cofre de chaves do Azure](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), um cluster do service fabric e fornecedor de recursos do Azure de Olá que utiliza certificados armazenados no Cofre de chaves quando cria um cluster.

**Criar um grupo de recursos** Step-by-Olá primeiro passo é toocreate um grupo de recursos especificamente para o seu Cofre de chaves. Recomendamos que colocar o Cofre de chaves Olá no seu próprio grupo de recursos. Esta ação permite-lhe remover Olá computação e armazenamento grupos de recursos, incluindo o grupo de recursos de Olá que contém o cluster do Service Fabric, sem perder as chaves e segredos. grupo de recursos de Olá que contém o seu Cofre de chaves tem de constar Olá mesma região que o cluster de Olá que está a ser utilizado.

**Criar um cofre de chaves no novo grupo de recursos Olá** Cofre de chaves Olá tem de estar ativado para implementação tooallow Olá certificados da tooget de fornecedor de recursos de computação do mesmo e instalá-lo em instâncias de máquina virtual.
toolearn mais como ver tooset segurança Cofre de chaves do Azure, [introdução ao Cofre de chaves do Azure](https://docs.microsoft.com/azure/key-vault/key-vault-get-started).

## <a name="assign-users-roles"></a>Atribuir funções de utilizadores
Depois de criar Olá aplicações toorepresent o cluster, atribuir os seus utilizadores funções toohello suportadas pelo Service Fabric: só de leitura e administrador. Pode atribuir funções de Olá utilizando Olá portal clássico do Azure.

>[!Note]
> Para obter mais informações sobre as funções no Service Fabric, consulte [controlo de acesso baseado em funções para clientes de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

Azure Service Fabric suportam dois tipos de controlo de acesso diferentes para clientes que estejam ligado tooa [cluster do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): administrador e utilizador. Controlo de acesso permite Olá administrador toolimit acesso toocertain cluster operações de cluster para diferentes grupos de utilizadores, tornando o cluster de Olá mais segura.

## <a name="next-steps"></a>Passos seguintes
- Configurar o Service Fabric [ambiente de desenvolvimento](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started).
- Saiba mais sobre [as opções de suporte do Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).

