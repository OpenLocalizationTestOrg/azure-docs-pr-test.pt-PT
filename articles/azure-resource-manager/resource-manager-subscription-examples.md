---
title: "aaaScenarios e exemplos de governação de subscrição | Microsoft Docs"
description: "Fornece exemplos de como tooimplement governação de subscrição do Azure para cenários comuns."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Exemplos para implementar andaime enterprise do Azure
Este tópico fornece exemplos de como uma empresa pode implementar recomendações de Olá para um [andaime Azure enterprise](resource-manager-subscription-governance.md). Utiliza uma empresa fictícias com o nome Contoso tooillustrate melhores práticas para cenários comuns.

## <a name="background"></a>Em segundo plano
Contoso é uma empresa em todo o mundo, que fornece soluções de cadeia de fornecimento de clientes em tudo "Software como um modelo de serviço" modelo tooa em pacote implementado no local.  Desenvolvem software entre globo Olá com centros de desenvolvimento importantes no Índia, Olá dos Estados Unidos e Canadá.

Olá ISV parte da empresa de Olá está dividido em várias unidades de negócio independentes que gerem os produtos num negócio significativo. Cada unidade de negócio tem as suas próprias programadores, gestores de produto e arquitetos de TI.

unidade de negócio de serviços de tecnologia de Enterprise (ETS) Olá fornece a capacidade IT centralizada e gere vários centros de dados em unidades de negócio alojam as aplicações. Juntamente com a gestão de centros de dados de Olá, Olá organização ETS fornece e gere a colaboração centralizada (por exemplo, e-mail e os Web sites) e serviços de rede/telefonia. Também gerir orientado para o cliente cargas de trabalho para unidades de negócio mais pequenas que não tenham pessoal operacional.

Olá pessoas fictícias os seguintes é utilizado neste tópico:

* Dave é administrador do ETS Azure Olá.
* Alice é Director de desenvolvimento da Contoso na unidade de negócio da cadeia de fornecimento de Olá.

Contoso tem de aplicação toobuild um linha de negócios e uma aplicação de orientado para o cliente. Se decidiu toorun Olá aplicações no Azure. Dave lê Olá [governação de subscrição prescritiva](resource-manager-subscription-governance.md) tópico, e está agora pronto tooimplement recomendações Olá.

## <a name="scenario-1-line-of-business-application"></a>Cenário 1: aplicações de linha de negócio
Contoso está a criar uma origem código gestão sistema (BitBucket) toobe utilizado pelos programadores em Olá mundo.  aplicação Olá utiliza a infraestrutura como serviço (IaaS) para alojar e consiste em servidores web e um servidor de base de dados. Os programadores aceder aos servidores nos respetivos ambientes de desenvolvimento, mas não precisa de aceder a servidores de toohello no Azure. Contoso ETS pretende proprietário da aplicação Olá tooallow e aplicação de Olá toomanage de equipa. aplicação Olá só está disponível na rede empresarial da Contoso. Dave tem tooset de subscrição de Olá para esta aplicação. subscrição Olá irá também alojar outra relacionados com o Programador de software no Olá futura.  

### <a name="naming-standards--resource-groups"></a>Normas de nomenclatura & grupos de recursos
Dave cria uma subscrição de ferramentas de programador toosupport que são comuns a todas as unidades de negócio Olá. Ele precisa toocreate nomes significativo para a subscrição de Olá e grupos de recursos (para aplicação Olá e redes de Olá). Ele cria Olá seguintes grupos de recursos e de subscrição:

| Item | Nome | Descrição |
| --- | --- | --- |
| Subscrição |Contoso ETS DeveloperTools produção |Suporta as ferramentas de programador comuns |
| Grupo de Recursos |rgBitBucket |Contém servidor de web de aplicação Olá e servidor de base de dados |
| Grupo de Recursos |rgCoreNetworks |Contém a ligação de gateway site para site e redes virtuais Olá |

### <a name="role-based-access-control"></a>Controlo de acesso baseado em funções
Depois de criar a subscrição, Dave pretende tooensure Olá equipas adequadas e os proprietários da aplicação podem aceder aos respetivos recursos. Dave reconhece que cada equipa tem requisitos diferentes. Ele utiliza grupos de Olá que foram sincronizados de tooAzure do Active Directory (AD) da Contoso no local do Active Directory e fornece o nível adequado de Olá de equipas de toohello de acesso.

Dave atribui Olá funções da subscrição Olá os seguintes:

| Função | Atribuído demasiado| Descrição |
| --- | --- | --- |
| [Proprietário](../active-directory/role-based-access-built-in-roles.md#owner) |Gerido ID a partir da Contoso AD |Este ID é controlado com apenas acesso de tempo (JIT) através da ferramenta de gestão de identidades da Contoso e assegura que o acesso de proprietário da subscrição totalmente é auditado. |
| [Gestor de segurança](../active-directory/role-based-access-built-in-roles.md#security-manager) |Segurança e riscos departamento de gestão |Esta função permite toolook de utilizadores em Olá Centro de segurança do Azure e o estado de Olá dos recursos de Olá. |
| [Contribuidor de Rede](../active-directory/role-based-access-built-in-roles.md#network-contributor) |Equipa de rede |Esta função permite rede equipa toomanage Olá Site tooSite da Contoso VPN e Olá redes virtuais. |
| *Função personalizada* |Proprietário da aplicação |Dave cria uma função que concede recursos toomodify de capacidade de Olá dentro do grupo de recursos de Olá. Para obter mais informações, consulte [funções personalizadas no Azure RBAC](../active-directory/role-based-access-control-custom-roles.md) |

### <a name="policies"></a>Políticas
Dave tem Olá os requisitos para gerir recursos na subscrição Olá:

* Porque as ferramentas de desenvolvimento de Olá suportarem programadores em Olá mundo, ele não quer tooblock utilizadores de criação de recursos em qualquer região. No entanto, ele tem tooknow onde os recursos são criados.
* Ele é preocupado com os custos. Por conseguinte, John tooprevent os proprietários da aplicação de criação de máquinas de virtuais desnecessariamente dispendiosas.  
* Como esta aplicação serve os programadores em várias unidades de negócio, John tootag cada recurso com o proprietário de unidade e aplicações da empresa Olá. Utilizando estas etiquetas, ETS pode cobrar equipas adequado Olá.

Ele cria seguinte Olá [políticas do Gestor de recursos](resource-manager-policy.md):

| Campo | Efeito | Descrição |
| --- | --- | --- |
| localização |Auditoria |Auditar Olá criação dos recursos de Olá em qualquer região |
| tipo |Negar |Negar a criação de máquinas virtuais de série de G |
| etiquetas |Negar |Exigir a tag de proprietário da aplicação |
| etiquetas |Negar |Exigir a tag de centro de custos |
| etiquetas |Acrescentar |Acrescentar o nome da etiqueta **BusinessUnit** e valor da etiqueta **ETS** tooall recursos |

### <a name="resource-tags"></a>Sinalizadores de recursos
Dave compreende que ele precisa toohave informações específicas no Centro de custos Olá fatura tooidentify Olá para implementação do Olá BitBucket. Além disso, Dave pretende tooknow que Olá todos os recursos que ETS é proprietário.

Adiciona seguinte Olá [etiquetas](resource-group-using-tags.md) toohello grupos de recursos e recursos.

| Nome da etiqueta | Valor da etiqueta |
| --- | --- |
| ApplicationOwner |nome de Olá do Olá quem gere esta aplicação. |
| CostCenter |Centro de custos de Olá Olá do grupo de que é pagar Olá consumo do Azure. |
| BusinessUnit |**ETS** (unidade de negócio Olá associada à subscrição Olá) |

### <a name="core-network"></a>Rede principal
Olá ETS Contoso propostas de informações de equipa de gestão de riscos de segurança e revê de Dave planear toomove Olá aplicação tooAzure. Pretendem tooensure Olá aplicação não está exposta toohello internet.  Dave também tem aplicações de programadores que Olá futura serão tooAzure movido. Essas aplicações necessitarem de interfaces de públicas.  toomeet estes requisitos, ele fornece redes virtuais internas e externas tanto um acesso de toorestrict de grupo de segurança de rede.

Ele cria Olá os seguintes recursos:

| Tipo de recurso | Nome | Descrição |
| --- | --- | --- |
| Rede Virtual |vnInternal |Utilizado com Olá aplicação BitBucket e está ligado através da rede empresarial do ExpressRoute tooContoso.  Uma sub-rede (sbBitBucket) fornece aplicação Olá com um espaço de endereço IP específico. |
| Rede Virtual |vnExternal |Disponível para as aplicações futuras que necessitam de pontos finais de destinado ao público. |
| Grupo de segurança de rede |nsgBitBucket |Garante que Olá superfície de ataque desta carga de trabalho é minimizado ao permitir ligações apenas na porta 443 para a sub-rede de olá onde a aplicação Olá encontre (sbBitBucket). |

### <a name="resource-locks"></a>Bloqueios de recursos
Dave reconhece que conectividade Olá partir da rede empresarial toohello interno rede virtual da Contoso deve ser protegida de qualquer wayward script ou a eliminação acidental.

Ele cria seguinte Olá [bloqueio de recurso](resource-group-lock-resources.md):

| Tipo de bloqueio | Recurso | Descrição |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |Impede que os utilizadores a eliminar Olá uma rede virtual ou sub-redes, mas não impede a adição de Olá de novas sub-redes. |

### <a name="azure-automation"></a>Automatização do Azure
Dave tem nada tooautomate para esta aplicação. Embora criado uma conta de automatização do Azure, ele inicialmente usaremos-lo.

### <a name="azure-security-center"></a>Centro de Segurança do Azure
Gestão de serviço de TI da Contoso tem tooquickly identificar e processar ameaças. Também pretendem toounderstand que problemas poderão existir.  

toofulfill estes requisitos, Dave permite Olá [Centro de segurança do Azure](../security-center/security-center-intro.md)e fornece a função de segurança Gestor de toohello de acesso.

## <a name="scenario-2-customer-facing-app"></a>Cenário 2: cliente com acesso à aplicação
liderança de negócio Olá na unidade de negócio da cadeia de fornecimento de Olá identificou vários oportunidades tooincrease um envolvimento com clientes da Contoso através da utilização de um cartão loyalty. Equipa de Alice tem de criar esta aplicação e decide que Azure aumenta os respetivos toomeet capacidade Olá necessidade empresarial. Alice funciona com Dave de subscrições de dois tooconfigure ETS para desenvolver e funcionamento desta aplicação.

### <a name="azure-subscriptions"></a>Subscrições do Azure
Dave inicia sessão no toohello Enterprise Portal do Azure e verá que departamento de cadeia de fornecimento de Olá já existe.  No entanto, dado que este projeto é Olá primeiro desenvolvimento projeto de equipa de cadeia de fornecimento de Olá no Azure, Dave reconhece Olá necessário para uma nova conta para a equipa de desenvolvimento de Alice.  Ele cria a conta "R & D" Olá para a equipa e atribui acesso tooAlice. Alice nos registos através de Olá portal do Azure e cria duas subscrições: servidores de desenvolvimento de Olá um toohold e servidores de produção de Olá um toohold.  Ela segue normas de nomenclatura de Olá anteriormente estabelecida quando criar Olá seguintes subscrições:

| Utilização de subscrição | Nome |
| --- | --- |
| Desenvolvimento |SupplyChain ResearchDevelopment LoyaltyCard desenvolvimento |
| Produção |SupplyChain operações LoyaltyCard produção |

### <a name="policies"></a>Políticas
Dave e Alice discutem aplicação Olá e identificam que esta aplicação serve apenas os clientes na região Norte American Olá.  Alice e a equipa planear o ambiente de serviço de aplicações e aplicações do SQL do Azure toocreate Olá toouse do Azure. Pode precisam de máquinas virtuais toocreate durante o desenvolvimento.  Alice pretende tooensure que os programadores têm recursos Olá necessitam tooexplore e examine problemas sem solicitação no ETS.

Para Olá **subscrição desenvolvimento**, criarem Olá seguinte política:

| Campo | Efeito | Descrição |
| --- | --- | --- |
| localização |Auditoria |Auditar criação de Olá dos recursos de Olá em qualquer região. |

Limita o tipo de Olá de um utilizador pode criar no desenvolvimento de sku e não necessitam de etiquetas para grupos de recursos ou recursos.

Para Olá **subscrição de produção**, criarem Olá políticas os seguintes:

| Campo | Efeito | Descrição |
| --- | --- | --- |
| localização |Negar |Negar a criação de Olá de quaisquer recursos fora Olá E.U.A. centros de dados. |
| etiquetas |Negar |Exigir a tag de proprietário da aplicação |
| etiquetas |Negar |Exigir a tag de departamento. |
| etiquetas |Acrescentar |Acrescente o grupo de recursos de tooeach a etiqueta que indica o ambiente de produção. |

Não limitam tipo Olá do sku, que pode criar um utilizador na produção.

### <a name="resource-tags"></a>Sinalizadores de recursos
Dave compreende que ele precisa toohave informações específicas tooidentify Olá negócio correto grupos de faturação e de propriedade. Define as etiquetas de recursos para grupos de recursos e recursos.

| Nome da etiqueta | Valor da etiqueta |
| --- | --- |
| ApplicationOwner |nome de Olá do Olá quem gere esta aplicação. |
| Departamento |Centro de custos de Olá Olá do grupo de que é pagar Olá consumo do Azure. |
| EnvironmentType |**Produção** (embora Olá subscrição inclui **produção** no nome de Olá, incluindo esta etiqueta permite a identificação fácil quando observar a recursos no portal de Olá ou na fatura Olá.) |

### <a name="core-networks"></a>Redes de núcleo
Olá ETS Contoso propostas de informações de equipa de gestão de riscos de segurança e revê de Dave planear toomove Olá aplicação tooAzure. Pretendem tooensure Olá aplicação Loyalty Card corretamente é isolada e protegida numa rede DMZ.  toofulfill este requisito, Dave e Alice criar uma rede virtual externa e um Olá de tooisolate de grupo de segurança de rede aplicação Loyalty Card a partir da rede empresarial do Olá Contoso.  

Para Olá **subscrição desenvolvimento**, criarem:

| Tipo de recurso | Nome | Descrição |
| --- | --- | --- |
| Rede Virtual |vnInternal |Serve de ambiente de desenvolvimento de Contoso Loyalty cartão Olá e está ligado através da rede empresarial do ExpressRoute tooContoso. |

Para Olá **subscrição de produção**, criarem:

| Tipo de recurso | Nome | Descrição |
| --- | --- | --- |
| Rede Virtual |vnExternal |Aloja a aplicação de cartão de Loyalty Olá e não está ligado diretamente tooContoso's ExpressRoute. Código é feito através do seu sistema de código fonte diretamente o toohello PaaS serviços. |
| Grupo de segurança de rede |nsgBitBucket |Garante que Olá superfície de ataque desta carga de trabalho é minimizado permitindo apenas a comunicação no vinculados no TCP 443.  Contoso é também investigar a utilizar uma Firewall de aplicação Web para a proteção adicional. |

### <a name="resource-locks"></a>Bloqueios de recursos
Dave e Alice confer e decidir tooadd bloqueios de recursos de alguns dos recursos principais do Olá no Olá ambiente tooprevent a eliminação acidental durante um push errant código.

Criarem Olá bloqueio os seguintes:

| Tipo de bloqueio | Recurso | Descrição |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |pessoas tooprevent contrária eliminem Olá sub-redes ou de rede virtual. bloqueio Olá não impede a adição de Olá de novas sub-redes. |

### <a name="azure-automation"></a>Automatização do Azure
Alice e a equipa de desenvolvimento tem ambiente de Olá toomanage runbooks extensas para esta aplicação. Olá runbooks permitem Olá adições/eliminações de nós da aplicação Olá e outras tarefas de DevOps.

toouse estes runbooks, elas permitem [automatização](../automation/automation-intro.md).

### <a name="azure-security-center"></a>Centro de Segurança do Azure
Gestão de serviço de TI da Contoso tem tooquickly identificar e processar ameaças. Também pretendem toounderstand que problemas poderão existir.  

toofulfill estes requisitos, Dave permite que o Centro de segurança do Azure. Ele assegura que o Centro de segurança do Azure Olá está a monitorizar os recursos de Olá, fornece acesso toohello equipas de DevOps e segurança.

## <a name="next-steps"></a>Passos seguintes
* toolearn sobre a criação de modelos do Resource Manager, consulte [melhores práticas para a criação de modelos Azure Resource Manager](resource-manager-template-best-practices.md).

