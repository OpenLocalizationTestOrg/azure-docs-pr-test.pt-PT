---
title: "aaaBest práticas para as empresas mover tooAzure | Microsoft Docs"
description: "Descreve um andaime que as empresas podem utilizar tooensure um ambiente seguro e fácil de gerir."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Andaime enterprise do Azure - governação prescritiva subscrição
As empresas adotem cada nuvem pública do Olá para a agilidade e a flexibilidade. Estes são a utilização força da codificação toogenerate de receitas da nuvem Olá ou otimizar os recursos para empresas Olá. O Microsoft Azure oferece um em diversos serviços de que as empresas podem assemblar como blocos modulares tooaddress um grande número de aplicações e cargas de trabalho. 

Mas, saber onde toobegin muitas vezes é difícil. Depois de decidir toouse do Azure, algumas perguntas surgem normalmente:

* "Como cumprir nosso requisitos legais para soberania de dados em determinados países?"
* "Como posso que garante que alguém não inadvertidamente, alterar um sistema crítico?"
* "Como posso saber que cada recurso é de suporte para que posso pode conta-lo e fatura criar uma com precisão?"

prospect Olá de uma subscrição vazia com rails sem proteção é uma tarefa intimidante. Este espaço em branco pode hamper tooAzure a movimentação.

Este artigo fornece um ponto de partida para o técnico de profissionais tooaddress Olá necessário para implementar a governação e equilíbrio com Olá necessita para agilidade. -Apresenta o conceito de Olá do andaime enterprise que o orienta às organizações implementar e gerir as suas subscrições do Azure. 

## <a name="need-for-governance"></a>Necessidade de governação
Quando move tooAzure, devem ser abordadas tópico Olá de governação antecipado tooensure Olá bem-sucedida utilização da nuvem Olá dentro de empresa Olá. Infelizmente, tempo de Olá e bureaucracy de criação de um sistema de governação abrangente significa alguns grupos de empresas diretamente aceda toovendors sem envolver TI empresariais. Esta abordagem pode deixar Olá enterprise abra toovulnerabilities se recursos Olá não são corretamente geridos. Olá características da Olá público em nuvem - agilidade, flexibilidade e baseada no consumo preços - são importantes toobusiness grupos que têm de tooquickly satisfazem pedidos de Olá de clientes (internos e externos). No entanto, TI empresariais tem tooensure que dados e sistemas de forma eficaz estão protegidos.

No vida real, andaime é a base de Olá toocreate utilizados da estrutura de Olá. andaime Olá guias de descrição geral de Olá e fornece pontos de âncora para toobe de sistemas mais permanente montada. Um andaime empresarial é Olá mesmo: um conjunto de controlos flexíveis e capacidades do Azure que fornecem estrutura toohello ambiente e âncoras para serviços em nuvem pública Olá. Fornece construtores Olá (IT e grupos de empresas) um toocreate foundation e anexe novos serviços.

andaime Olá baseia-se nas práticas que iremos ter reunidas a partir de várias ações de envolvimento com clientes de vários tamanhos. Intervalo esses clientes, de pequenas organizações desenvolver soluções nas empresas de tooFortune 500 Olá cloud e fornecedores independentes de software que estão a migrar e desenvolver soluções na nuvem de Olá. Olá andaime empresarial é toosupport flexível toobe "específico" tradicionais IT as cargas de trabalho e cargas de trabalho seja ágil; tal como os programadores criar aplicações de software-como-um-serviço (SaaS) com base nas capacidades do Azure.

andaime de enterprise Olá é toobe pretendido Olá foundation de cada nova subscrição no Azure. Permite que os administradores tooensure cargas de trabalho às Olá mínimo requisitos de governação de uma organização sem a impedir que os grupos de empresas e os programadores rapidamente a cumprir os seus próprios objetivos.

> [!IMPORTANT]
> Governação é fundamental toohello êxito do Azure. Destinos este artigo Olá implementação técnica do andaime enterprise, mas apenas tocar no processo mais amplo Olá e relações entre componentes Olá. Governação da política flui da parte superior do Olá para baixo e é determinada pelo que Olá negócio pretende tooachieve. Naturalmente, criação de Olá de um modelo de governação para o Azure inclui representantes do departamento de TI, mas o mais importante ainda, deve possuir representação segura de líderes do grupo de negócio e gestão de segurança e riscos. No final de Olá, um andaime enterprise é para mitigar o negócio risco toofacilitate missão e os objetivos da organização.
> 
> 

Olá imagem a seguir descreve os componentes de Olá do andaime Olá. foundation Olá depende de um plano sólido para departamentos, contas e subscrições. pillars Olá consistem de políticas de Gestor de recursos e normas de nomenclatura fortes. restante Olá andaime Olá provém de núcleos capacidades do Azure e as funcionalidades que ativar um ambiente seguro e fácil de gerir.

![componentes do andaime](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure desenvolveu-se rapidamente desde a introdução 2008. Este crescimento necessário equipas de engenharia do Microsoft toorethink sua abordagem para gerir e implementar serviços. modelo do Azure Resource Manager Olá foi introduzido em 2014 e substitui o modelo de implementação clássica Olá. O Resource Manager permite às organizações toomore facilmente implementar, organizar e controlar os recursos do Azure. Gestor de recursos inclui parallelization ao criar recursos para a implementação mais rápida de soluções complexas, interdependentes. Também inclui Olá capacidade tootag recursos com os metadados e o controlo de acesso granular. A Microsoft recomenda que todos os recursos através do modelo do Resource Manager Olá de criar. andaime de enterprise Olá explicitamente foi concebida para o modelo do Resource Manager Olá.
> 
> 

## <a name="define-your-hierarchy"></a>Definir a sua hierarquia
foundation Olá do andaime Olá é Olá inscrição Enterprise de Azure (e Olá Enterprise Portal). inscrição enterprise de Olá define a forma de Olá e utilizar serviços do Azure dentro de uma empresa e é a estrutura de governação Olá core. Dentro do enterprise agreement do Olá, os clientes conseguem toofurther subdividir ambiente Olá departamentos, contas e, por fim, subscrições. Uma subscrição do Azure é a unidade básica de olá onde estão incluídos todos os recursos. Também define os limites de vários no Azure, tais como o número de núcleos, recursos, etc.

![hierarquia](./media/resource-manager-subscription-governance/agreement.png)

Cada empresa é diferente e hierarquia Olá na imagem anterior Olá permite uma flexibilidade significativa na como o Azure está organizado dentro da empresa de Olá. Antes de implementar orientações Olá contidas neste documento, deve a hierarquia de modelo e compreender o impacto de Olá sobre faturação, acesso a recursos e complexidade.

Olá três padrões comuns para inscrições através do Azure são:

* Olá **funcional** padrão
  
    ![funcional](./media/resource-manager-subscription-governance/functional.png)
* Olá **unidade de negócio** padrão 
  
    ![empresa](./media/resource-manager-subscription-governance/business.png)
* Olá **geográfica** padrão
  
    ![geográfica](./media/resource-manager-subscription-governance/geographic.png)

Aplicar andaime Olá em Olá tooextend nível Olá governação requisitos da subscrição do enterprise Olá numa subscrição Olá.

## <a name="naming-standards"></a>Normas de nomenclatura
pilar primeiro de Olá do andaime Olá é nomenclatura normas. As normas de nomenclatura devidamente concebidas permitem-lhe tooidentify recursos no portal de Olá, uma fatura e scripts. Provavelmente, já ter normas de nomenclatura para a infraestrutura no local. Ao adicionar ambiente tooyour do Azure, deve expandir os tooyour normas de nomenclatura recursos do Azure. Padrão de nomenclatura facilitar a gestão mais eficiente de ambiente de Olá em todos os níveis.

> [!TIP]
> Para as convenções de nomenclatura:
> * Reveja e que adotar sempre que possível Olá [orientações de padrões e práticas](../guidance/guidance-naming-conventions.md). Esta orientação ajuda-o a decidir sobre uma norma de nomenclatura significativa.
> * Utilize camelCasing para nomes de recursos (como myResourceGroup e vnetNetworkName). Nota: Existem determinados recursos, tais como contas de armazenamento, em que a opção apenas Olá é toouse minúsculas (e não existem outros carateres especiais).
> * Considere a utilização do Azure Resource Manager políticas (descritas na secção seguinte Olá) tooenforce normas de nomenclatura.
> 
> Olá anteriores sugestões ajudá-lo a implementar uma convenção de nomenclatura consistente.

## <a name="policies-and-auditing"></a>As políticas e de auditoria
pilar segundo do Olá do andaime Olá envolve criar [políticas do Azure Resource Manager](resource-manager-policy.md) e [auditoria do registo de atividade Olá](resource-group-audit.md). Políticas de Gestor de recursos poderá risco de toomanage Olá capacidade no Azure. Pode definir políticas que garantem soberania de dados ao restringir, impor ou auditoria determinadas ações. 

* A política é uma predefinição **permitir** sistema. Controlar as ações ao definir e atribuir políticas tooresources negar ou ações em recursos de auditoria.
* As políticas são descritas por definições de política na linguagem de definição de política (if-a em seguida, em seguida condições).
* Criar políticas com JSON (Javascript Object Notation) ficheiros formatados. Depois de definir uma política, atribui-tooa determinado âmbito: subscrição, o grupo de recursos ou o recurso.

Políticas tem várias ações que permitem cenários de tooyour uma abordagem de detalhado. ações de Olá são:

* **Negar**: pedido de recurso de Olá blocos
* **Auditoria**: permite que o pedido de Olá, mas adiciona um registo de atividade de toohello de linha (que pode ser utilizados tooprovide alertas ou tootrigger runbooks)
* **Acrescentar**: adiciona informações toohello recurso especificado. Por exemplo, se não existir uma etiqueta de "CostCenter" num recurso, adicione essa tag com um valor predefinido.

### <a name="common-uses-of-resource-manager-policies"></a>Utilizações comuns das políticas do Gestor de recursos
Políticas de Gestor de recursos do Azure são uma ferramenta poderosa no Olá toolkit do Azure. Dão-lhe tooavoid custos inesperados, tooidentify um custo do Centro de recursos através de marcação e tooensure esse conformidade era requisitos são cumpridos. Quando as políticas são combinadas com funcionalidades de auditoria incorporadas Olá, pode fashion soluções flexíveis e complexas. Políticas de permitir que as empresas tooprovide controlos para cargas de trabalho "TI tradicionais" e "Agile" cargas de trabalho; tal como desenvolver aplicações de cliente. Olá padrões mais comuns, que vemos para políticas são:

* **Soberania de conformidade/dados de Georreplicação** -Azure fornece regiões Olá mundo. As empresas, muitas vezes, pretendem toocontrol onde os recursos são criados (se soberania dos dados de tooensure ou apenas tooensure recursos são criados toohello fechar os consumidores de fim de recursos de Olá).
* **A gestão de custos** -subscrição do Azure um pode conter recursos de vários tipos e escala. As empresas têm, muitas vezes, assim o desejar tooensure esse padrão subscrições evitar a utilização de recursos desnecessariamente grandes, o que podem custo centenas de utilizados no compromisso um mês ou mais.
* **Predefinição governação através de etiquetas necessárias** -necessidade de etiquetas é uma das funcionalidades de Olá mais comuns e altamente pretendido. Através de políticas do Azure Resource Manager empresas são tooensure capaz de que um recurso é adequadamente etiquetado. Olá etiquetas mais comuns são: tipo de departamento, o proprietário do recurso e o ambiente (por exemplo - produção, teste, desenvolvimento)

**Exemplos**

"Tradicional IT" subscrição para aplicações de linha de negócio

* Impor departamento e proprietário etiquetas em todos os recursos
* Restringir toohello de criação de recursos norte americano região
* Restringir Olá capacidade toocreate G série VMs e Clusters do HDInsight

Ambiente "Seja ágil" para uma unidade de negócio a criação de aplicações em nuvem

* requisitos de soberania dos dados de toomeet, permitir a criação de Olá de recursos apenas numa região específica.
* Impor a etiqueta de ambiente em todos os recursos. Se um recurso é criado sem uma etiqueta, acrescentar Olá **ambiente: desconhecido** tag toohello recursos.
* Auditoria quando os recursos são criados fora da América do Norte, mas não impedir.
* Auditoria ao custo de alta recursos é criados.

> [!TIP]
> Hello mais comuns a utilização de políticas de Gestor de recursos entre organizações está toocontrol *onde* recursos podem ser criados e *que* tipos de recursos podem ser criados. Além disso tooproviding controlos *onde* e *que*, muitas empresas utilize políticas tooensure recursos tem Olá os metadados adequados toobill novamente para consumo. É recomendável aplicar políticas ao nível de subscrição de Olá para:
> 
> * Soberania de conformidade/dados de Georreplicação
> * Gestão de custos
> * Etiquetas necessárias (Determined por necessidade empresarial, tais como BillTo, o proprietário da aplicação)
> 
> Pode aplicar políticas adicionais em níveis inferiores de âmbito.
> 
> 

### <a name="audit---what-happened"></a>Auditoria - o que aconteceu?
tooview como ambiente está a funcionar, terá de atividade do utilizador tooaudit. A maioria dos tipos de recursos no Azure criar registos de diagnóstico que pode analisar através de uma ferramenta de registo ou no Azure Operations Management Suite. É possível recolher os registos de atividade entre várias subscrições tooprovide, um departamental ou de vista de empresa. Os registos de auditoria são uma ferramenta de diagnóstico importante e eventos de tootrigger um mecanismo fundamental no Olá ambiente do Azure.

Os registos de atividade de implementações do Resource Manager permitem-lhe toodetermine Olá **operações** que demorou local e de quem efetuou-los. Registos de atividade podem ser recolhidos e agregadas ferramentas como a análise de registos.

## <a name="resource-tags"></a>Sinalizadores de recursos
Como os utilizadores na sua organização adicionar subscrição toohello de recursos, torna-se os recursos de cada vez mais importante tooassociate com departamento apropriado Olá, o cliente e o ambiente. Pode anexar tooresources de metadados através de [etiquetas](resource-group-using-tags.md). Utilize etiquetas tooprovide informações sobre recursos de Olá ou proprietário Olá. As etiquetas permitem-lhe toonot apenas agregado e do grupo de recursos de várias formas, mas utilizam esses dados para efeitos de Olá de estorno. Pode Etiquetar recursos com segurança too15 chave: pares de valores. 

Os sinalizadores de recursos são flexíveis e devem ser anexado toomost recursos. Exemplos de etiquetas de recursos comuns são:

* BillTo
* Departamento (ou unidade de negócio)
* Ambiente (programação de produção, fase)
* Camada (camada Web, a camada da aplicação)
* Proprietário da aplicação
* ProjectName

![etiquetas](./media/resource-manager-subscription-governance/resource-group-tagging.png)

Para obter mais exemplos das etiquetas, consulte [recomendado convenções de nomenclatura para recursos do Azure](../guidance/guidance-naming-conventions.md).

> [!TIP]
> Considere efetuar uma política que exige deste etiquetagem para:
> 
> * Grupos de recursos
> * Armazenamento
> * Virtual Machines
> * Servidores de ambientes de serviço/web de aplicação
> 
> Esta estratégia etiquetagem identifica nas suas subscrições que metadados é necessário para o negócio Olá, financeiros, segurança, gestão de riscos e gestão geral do ambiente de Olá. 

## <a name="resource-group"></a>Grupo de recursos
Gestor de recursos permite-lhe tooput recursos em grupos de afinidade de faturação ou natural de gestão, de significativos. Conforme mencionado anteriormente, o Azure tem dois modelos de implementação. Na Olá o modelo de clássico anterior, unidade básica de Olá de gestão foi subscrição Olá. Foi difícil toobreak baixo recursos numa subscrição, que levou a criação de toohello de grandes quantidades de subscrições. Com o modelo do Resource Manager Olá, vimos introdução Olá de grupos de recursos. Grupos de recursos são contentores de recursos que têm um ciclo de vida comuns ou partilham um atributo, tais como "todos os servidores SQL" ou "A aplicação".

Grupos de recursos não podem ser incluídos em si e recursos só podem pertencer tooone grupo de recursos. Pode aplicar determinadas ações em todos os recursos num grupo de recursos. Por exemplo, a eliminação de um grupo de recursos remove todos os recursos do grupo de recursos de Olá. Normalmente, colocar uma aplicação completa ou sistema relacionado no Olá mesmo grupo de recursos. Por exemplo, uma aplicação de três camadas denominada Contoso Web aplicação iria conter o servidor de web de Olá, o servidor de aplicações e o SQL server no Olá mesmo grupo de recursos.

> [!TIP]
> Como organizar os seus grupos de recursos podem diferir das cargas de trabalho "TI tradicionais" demasiado cargas de trabalho "TI seja ágil":
> 
> * "Tradicional IT" cargas de trabalho maior frequência estão agrupadas por itens num Olá mesmo ciclo de vida, como uma aplicação. Permite a gestão de aplicações individuais agrupamento por aplicação.
> * "Seja ágil IT" cargas de trabalho tendem toofocus em aplicações externas orientado para o cliente em nuvem. grupos de recursos de Olá devem refletir camadas Olá da implementação (por exemplo, a camada Web, a camada de aplicação) e gestão.
> 
> Compreender a sua carga de trabalho ajuda-o a desenvolver uma estratégia de grupo de recursos.

## <a name="role-based-access-control"></a>Controlo de acesso baseado em funções
É, provavelmente, pedimos sozinho "que devem ter acesso tooresources?" e "como controlar este acesso?" Permitir ou desautorizar acesso toohello portal do Azure e controlar o acesso tooresources no portal de Olá é fundamental. 

Quando o Azure foi lançado inicialmente, o acesso controlos tooa subscrição foram básico: administrador ou Coadministrador. Aceder à subscrição de tooa Olá clássico modelo implícito acesso tooall Olá recursos no portal de Olá. Esta falta de um controlo detalhado guiado toohello proliferação de subscrições tooprovide um nível de controlo de acesso razoável para uma inscrição do Azure.

Este proliferação de subscrições já não é necessária. Com o controlo de acesso baseado em funções, pode atribuir utilizadores toostandard funções (como "leitor" comuns e os tipos de funções "escritor"). Também pode definir funções personalizadas.

> [!TIP]
> controlo de acesso baseado em funções de tooimplement:
> * Ligar a sua identidade empresarial store (normalmente Active Directory) tooAzure do Active Directory através de Olá ferramenta AD Connect.
> * Controla Olá administrador/Coadministrador da subscrição utilizando uma identidade gerida. **Não** atribuir administrador/coadministrador tooa novo proprietário da subscrição. Em alternativa, utilize tooprovide de funções RBAC **proprietário** grupo tooa de direitos ou individuais.
> * Adicione grupo de tooa de utilizadores do Azure (por exemplo, X os proprietários da aplicação) no Active Directory. Utilize Olá grupo sincronizado tooprovide grupo Membros Olá direitos adequados toomanage Olá grupo de recursos que contém a aplicação Olá.
> * Siga o princípio de Olá de conceder Olá **menor privilégio** toodo necessário Olá esperado trabalho. Por exemplo:
>   * Grupo de implementação: Um grupo que é apenas capaz de toodeploy recursos.
>   * : Máquina virtual um grupo de gestão Que é capaz de toorestart VMs (para operações de)
> 
> Estas sugestões ajudam a gerir o acesso de utilizador na sua subscrição.

## <a name="azure-resource-locks"></a>Bloqueios de recursos do Azure
Como a sua organização adiciona a subscrição de toohello de serviços de núcleos, torna-se cada vez mais importante tooensure que esses serviços estão disponíveis tooavoid interrupção de negócio. [Bloqueios de recurso](resource-group-lock-resources.md) permitem-lhe toorestrict operações nos recursos de elevado valor onde modificar ou eliminá-los teria um impacto significativo na sua aplicações ou a infraestrutura de nuvem. Pode aplicar bloqueios tooa subscrição, o grupo de recursos ou o recurso. Normalmente, aplicar bloqueios toofoundational recursos, tais como redes virtuais, gateways e as contas de armazenamento. 

Bloqueios de recursos atualmente suportam dois valores: CanNotDelete e só de leitura. CanNotDelete significa que os utilizadores (com os direitos adequados Olá) podem ainda ler ou modificar um recurso, mas não é possível eliminá-lo. Só de leitura significa que os utilizadores autorizados não é possível eliminar ou modificar um recurso.

toocreate ou eliminar bloqueios de gestão, tem de ter acesso demasiado`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações.
Das funções incorporadas Olá, apenas o proprietário e o administrador de acesso de utilizador são concedidas essas ações.

> [!TIP]
> Opções de rede principal devem ser protegidas com bloqueios. A eliminação acidental de um gateway, de VPN de site para site seria tooan desastroso subscrição do Azure. Azure não permite que toodelete uma rede virtual que está a ser utilizado, mas aplicar restrições mais é útil precaução. 
> 
> * Rede virtual: CanNotDelete
> * Grupo de segurança de rede: CanNotDelete
> * Políticas: CanNotDelete
> 
> As políticas também são toohello fundamental manutenção dos controlos adequados. Recomendamos que aplique uma **CanNotDelete** bloquear toopolices que estão em utilização.

## <a name="core-networking-resources"></a>Recursos de rede principal
Acesso tooresources pode ser interno (numa rede de corporation Olá) ou externos (através de Olá internet). É fácil para os utilizadores na sua organização tooinadvertently colocar recursos lugar para cima de errado do Olá e potencialmente abrir toomalicious acesso. Tal como acontece com dispositivos no local, as empresas tem de adicionar tooensure controlos adequados que os utilizadores do Azure decisões Olá à direita. Para governação de subscrição, podemos identificar recursos principais do que permitem controlar básica de acesso. recursos principais do Olá é composto por:

* **Redes virtuais** são objetos de contentor para sub-redes. Apesar de não estritamente necessários, muitas vezes, é utilizada ao ligar a recursos da empresa toointernal aplicações.
* **Grupos de segurança de rede** são semelhantes tooa firewall e fornecer para como um recurso pode "conversar"com as regras de rede de Olá. Se fornecer um controlo granular sobre como / Olá mesmo se uma sub-rede (ou a máquina virtual) pode ligar-se toohello Internet ou outras sub-redes na rede virtual.

![componentes essenciais de rede](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> Funcionamento em rede:
> * Crie redes virtuais dedicadas tooexternal orientada para as cargas de trabalho e interno com acesso à cargas de trabalho. Esta abordagem reduz a possibilidade de Olá de inadvertidamente colocar as máquinas virtuais que foram concebidas para cargas de trabalho internas num espaço com acesso externo.
> * Configure o acesso de toolimit de grupos de segurança de rede. No mínimo, bloquear acesso toohello internet a partir de redes virtuais internas e a rede empresarial do bloco acesso toohello de redes virtuais externas.
> 
> Estas sugestões ajudam a implementar recursos de funcionamento em rede seguros.

### <a name="automation"></a>Automatização
Gerir recursos individualmente é uma operação morosa e potencialmente suscetível para determinadas operações de erro. O Azure oferece várias capacidades de automatização, incluindo a automatização do Azure, as Logic Apps e as funções do Azure. [A automatização do Azure](../automation/automation-intro.md) permite que os administradores toocreate e definir as tarefas comuns de toohandle runbooks na gestão de recursos. Criar runbooks utilizando um editor de código do PowerShell ou um editor gráfico. Pode produzir fluxos de trabalho de fase multi complexos. A automatização do Azure é frequentemente utilizado toohandle tarefas comuns como encerrar recursos não utilizados, ou ao criar recursos no acionador de específica de tooa de resposta sem necessitar de intervenção do homem.

> [!TIP]
> Para automatização:
> * Criar uma conta de automatização do Azure e rever Olá runbooks disponíveis (linha de comando e gráfica) disponíveis no Olá [Galeria de Runbooks](../automation/automation-runbook-gallery.md).
> * Importar e personalizar runbooks chaves para utilização própria.
> 
> Um cenário comum é Olá capacidade tooStart/encerrar as máquinas virtuais com base numa agenda. Existem runbooks de exemplo que estão disponíveis no Olá galeria que processar este cenário e lhe ensinar como tooexpand-lo.
> 
> 

## <a name="azure-security-center"></a>Centro de Segurança do Azure
Talvez um Olá maior bloqueadores toocloud a adoção foi preocupações Olá através da segurança. Gestores de riscos de TI e departamentos de segurança necessário tooensure que recursos no Azure são seguros. 

Olá [Centro de segurança do Azure](../security-center/security-center-intro.md) fornece uma vista de estado de segurança de Olá dos recursos nas subscrições Olá central e fornece recomendações que ajudam a impedir recursos comprometidos. Pode ativar a políticas mais granulares (por exemplo, aplicar políticas toospecific grupos de recursos que permitem Olá enterprise tootailor os riscos de toohello postura que são endereçamento). Por fim, o Centro de segurança do Azure é uma plataforma aberta que permite que parceiros da Microsoft e o software de toocreate de fornecedores independentes de software plugs no Centro de segurança do Azure tooenhance as respetivas capacidades. 

> [!TIP]
> Centro de segurança do Azure está ativado por predefinição em cada subscrição. No entanto, tem de ativar a recolha de dados de máquinas virtuais tooallow Centro de segurança do Azure tooinstall o agente e começar a recolher dados.
> 
> ![Recolha de dados](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>Passos seguintes
* Agora que aprendeu sobre governação de subscrição, está tempo toosee estas recomendações na prática. Consulte [exemplos para implementar a governação de subscrição do Azure](resource-manager-subscription-examples.md).

