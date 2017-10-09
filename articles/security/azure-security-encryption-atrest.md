---
title: "aaaMicrosoft encriptação em Rest da Azure dados | Microsoft Docs"
description: "Este artigo fornece uma descrição geral da encriptação de dados do Microsoft Azure em rest, Olá gerais capacidades e considerações gerais."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Dados do Azure encriptação em Rest
Existem várias ferramentas nos dados do Microsoft Azure toosafeguard de acordo com as necessidades de segurança e conformidade de tooyour da empresa. Este documento centra-se em como dados estão protegidos em rest em todo o Microsoft Azure, aborda Olá vários componentes a parte na implementação de proteção de dados de Olá e revê os profissionais de TI e contras de abordagens de proteção de gestão de chaves diferentes Olá. 

Encriptação de Inativos é um requisito de segurança comuns. Uma vantagem do Microsoft Azure é que as organizações podem alcançar a encriptação de Inativos sem ter de custo de Olá de implementação e gestão e Olá risco de uma solução de gestão de chaves personalizadas. As organizações têm a opção de Olá de permitir que o Azure completamente gerir a encriptação de inativos. Além disso, as organizações têm várias opções tooclosely, gerir a encriptação ou chaves de encriptação.

## <a name="what-is-encryption-at-rest"></a>O que é a encriptação de Inativos?
Encriptação de Inativos refere-se toohello criptográficos codificação (encriptação) de dados quando é mantida. Olá estruturas de Rest no Azure a encriptação utilizar encriptação simétrica tooencrypt e desencriptar grandes quantidades de dados de acordo com rapidamente tooa de modelo concetual simples:

- Uma chave de encriptação simétrica é utilizada tooencrypt dados que é persistente 
- Olá a mesma chave de encriptação é utilizado toodecrypt que os dados é readied para utilização na memória
- Poderão ser particionados dados e podem ser utilizadas chaves diferentes para cada partição
- As chaves têm de ser armazenadas numa localização segura com políticas de controlo de acesso limitar acesso toocertain identidades e a utilização de chave de registo. Chaves de encriptação de dados, muitas vezes, são encriptadas com acesso de limite de toofurther encriptação assimétrico (abordado Olá *chave hierarquia*, mais à frente neste artigo)

Olá acima descreve os elementos de alto nível comuns Olá de encriptação de inativos. Na prática, cenários de gestão e o controlo de chaves, bem como oferece garantias ao rendimento dimensionamento e disponibilidade, requerem construções adicionais. Microsoft Azure a encriptação Rest conceitos e componentes são descritas abaixo.

## <a name="hello-purpose-of-encryption-at-rest"></a>objetivo de Olá de encriptação de Inativos
A encriptação de Inativos é tooprovide pretendido de proteção de dados para dados em rest (conforme descrito acima.) Os ataques contra dados em rest incluem hardware toohello tentativas tooobtain acesso físico no qual Olá os dados são armazenados e, em seguida, o compromisso Olá continha dados. Num ataque de unidade de disco rígido de um servidor pode ter sido mishandled durante a manutenção, permitindo que um atacante a unidade de disco rígido tooremove Olá. Posterior atacante de Olá seria colocar o disco rígido Olá num computador com os seus dados de Olá do controlo tooattempt tooaccess. 

Encriptação de Inativos é o atacante de Olá tooprevent concebida de aceder aos dados Olá não encriptada, assegurando que Olá dados são encriptados quando no disco. Se um atacante foram tooobtain um disco rígido com, tais encriptados dados e não existem chaves de encriptação de toohello de acesso, o atacante Olá não iria comprometer a dados Olá sem dificuldade em excelente. Neste cenário, um atacante teria tooattempt os ataques contra os dados encriptados são muito mais complexos e consumir recursos que aceder não encriptada dados num disco rígido. Por este motivo, a encriptação de Inativos é vivamente recomendável e é um requisito de alta prioridade para muitas organizações. 

Em alguns casos, a encriptação de Inativos também é necessário pelo necessidade de uma organização de esforços de governação e conformidade de dados. As normas da indústria e governamentais, como HIPAA, PCI e FedRAMP e requisitos de regulamentação internacionais, esquematizar salvaguardas específicas através de processos e políticas sobre requisitos de encriptação e proteção de dados. Para muitos essas normas de encriptação de Inativos é uma medida de obrigatória necessária para a proteção e gestão de dados em conformidade. 

Além disso toocompliance e requisitos de regulamentação, encriptação de Inativos deve ser interpretada como uma capacidade de plataforma de defesa em profundidade. Apesar da Microsoft fornece uma plataforma em conformidade para os serviços, aplicações, e dados, das instalações abrangente e segurança física, dados de controlo de acesso e auditoria, é importante tooprovide adicionais "sobrepostos" medidas de segurança no caso de um dos Olá outra segurança mede a falhar. Encriptação de Inativos fornece essa um mecanismo de defesa adicional.

A Microsoft está consolidada tooproviding a encriptação opções de rest através de serviços em nuvem e tooprovide clientes adequado capacidade de gestão de chaves de encriptação e toologs de acesso que mostra quando são utilizadas chaves de encriptação. Além disso, a Microsoft está a trabalhar para objetivo Olá efetuar todos os dados de cliente encriptados em descanso ao, por predefinição.

## <a name="azure-encryption-at-rest-components"></a>Componentes de Rest a encriptação do Azure

Tal como descrito anteriormente, o objetivo de Olá de encriptação de Inativos é que os dados que são mantidos no disco são encriptados com uma chave de encriptação do segredo. tooachieve esse objetivo de proteger a criação de chave, armazenamento, o controlo de acesso e gestão de encriptação de Olá chaves tem de ser fornecidas. Embora detalhes podem variar, serviços do Azure encriptação em implementações de Rest podem ser descritos em termos de Olá abaixo conceitos que, em seguida, são ilustrados na Olá diagrama a seguir.

![Componentes](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>Azure Key Vault

Olá a localização de armazenamento de chaves de encriptação de Olá e chaves de toothose de controlo de acesso é a encriptação central tooan modelo rest. chaves de Olá necessário toobe altamente protegido mas gerível pelos utilizadores especificados e serviços toospecific disponíveis. Para serviços do Azure, o Cofre de chaves do Azure é Olá recomendado a solução de armazenamento de chaves e fornece uma experiência de gestão comuns em serviços. As chaves são armazenadas e geridas no cofres de chaves, e pode ser especificado o Cofre de chaves do acesso tooa toousers ou serviços. O Cofre de chaves do Azure suporta a criação de cliente de chaves ou a importação das chaves de cliente para utilização em situações de chave de encriptação gerida pelo cliente.

### <a name="azure-active-directory"></a>Azure Active Directory

Chaves de Olá permissões toouse armazenados no Cofre de chaves do Azure, toomanage ou tooaccess-los para a encriptação em Rest encriptação e desencriptação, pode ser especificado tooAzure contas do Active Directory. 

### <a name="key-hierarchy"></a>Hierarquia de chave

Normalmente, mais do que uma chave de encriptação é utilizada numa encriptação na implementação de rest. Encriptação assimétrica é útil para estabelecer confiança Olá e for necessário para a gestão e acesso a chaves de autenticação. Encriptação simétrica é mais eficiente para encriptação em massa e de desencriptação, permitindo uma encriptação mais forte e melhor desempenho. Além disso, limitação de utilização de Olá de um diminuições de chave de encriptação único risco Olá Olá chave será comprometido e Olá custo de reencriptação quando uma chave têm de ser substituída. vantagens de Olá tooleverage de encriptação simétrica e assimétrica e a utilização de Olá de limite e exposição de uma única chave, a encriptação do Azure modelos de rest utilizar uma hierarquia de chave composta por Olá os seguintes tipos de chaves:

- **Chave de encriptação de dados (DEK)** – uma chave simétrica de AES256 utilizado tooencrypt uma partição ou o bloco de dados.  Um único recurso pode ter partições muitas e muitas chaves de encriptação de dados. Encriptação de cada bloco de dados com uma chave diferente torna ataques de análise de criptografia mais difícil. É necessário acesso tooDEKs Olá aplicação ou fornecedor de instância de recurso que está a encriptar e desencriptar um bloco específico. Quando um DEK é substituída por uma nova chave apenas hello dados no bloco associado tem de ser encriptados novamente com a nova chave de Olá.
- **Chave de encriptação de chaves (KEK)** – uma chave de encriptação assimétrico utilizado tooencrypt Olá chaves de encriptação de dados. Utilização de uma chave de encriptação de chave permite Olá chaves de encriptação de dados próprios toobe encriptados e controlado. entidade Olá que tenha acesso toohello KEK poderá ser diferente da entidade de Olá que requer Olá DEK. Isto permite uma entidade toobroker acesso toohello DEK objetivo Olá garantir acesso limitado de cada partição de toospecific DEK. Uma vez que Olá KEK toodecrypt necessário Olá DEKs, Olá KEK é, efetivamente, um ponto único através do qual DEKs podem ser eliminados eficazmente pela eliminação de Olá KEK.

Chaves de encriptação de dados de Olá, encriptada com Olá chaves de encriptação de chave são armazenadas em separado e apenas uma entidade com a chave de encriptação pode obter as chaves de encriptação de dados de toohello de acesso encriptado com essa chave. São suportados modelos diferentes, de armazenamento de chaves. Cada modelo em mais detalhe posteriormente na secção seguinte, Olá, vamos abordar.

## <a name="data-encryption-models"></a>Modelos de encriptação de dados

Noções sobre Olá vários modelos de encriptação e os respetivos os profissionais de TI e contras é essencial para compreender como Olá vários fornecedores de recursos do Azure de implementar a encriptação inativa. Estas definições são partilhadas entre todos os fornecedores de recursos no idioma comum tooensure do Azure e taxonomia. 

Existem três cenários de encriptação do lado do servidor:

- Encriptação do lado do servidor utilizando as chaves de serviço geridas
    - Fornecedores de recursos do Azure efetuar operações de encriptação e desencriptação de Olá
    - Microsoft gere as chaves de Olá
    - Funcionalidade completa de nuvem

- Encriptação do lado do servidor utilizando as chaves gerida pelo cliente no Cofre de chaves do Azure
    - Fornecedores de recursos do Azure efetuar operações de encriptação e desencriptação de Olá
    - Cliente controla chaves através do Cofre de chaves do Azure
    - Funcionalidade completa de nuvem

- Utilizar chaves gerida pelo cliente em hardware de cliente controlado de encriptação do lado do servidor
    - Fornecedores de recursos do Azure efetuar operações de encriptação e desencriptação de Olá
    - As chaves de controlos do cliente no cliente controlada hardware
    - Funcionalidade completa de nuvem

Para a encriptação do lado do cliente, considere o seguinte Olá:

- Serviços do Azure não podem ver dados desencriptados
- Os clientes gerir e armazenam as chaves no local (ou noutras secure arquivos). As chaves não estão disponíveis tooAzure serviços
- Funcionalidade reduzida de nuvem

encriptação de Olá suportado modelos no Azure dividida em dois grupos principais: "Encriptação de cliente" e "encriptação do lado do servidor" mencionado anteriormente. Tenha em atenção que, independente da encriptação de Olá no modelo de rest dos serviços do Azure, utilizados sempre recomendada a Olá utilização um transporte seguro, tais como TLS ou HTTPS. Por conseguinte, a encriptação no transporte deve ser resolvida pelo protocolo de transporte de Olá e não deve ser um fator principais determinar que a encriptação toouse de modelo de rest.

### <a name="client-encryption-model"></a>Modelo de encriptação do cliente

Modelo de encriptação do cliente refere-se tooencryption fora Olá fornecedor de recursos ou do Azure, é efetuada pelo serviço de Olá ou a aplicação de chamada. encriptação de Olá pode ser efetuada pela aplicação de serviço Olá no Azure, ou por uma aplicação em execução no Centro de dados de cliente Olá. Em ambos os casos, ao tirar partido deste modelo de encriptação, Olá fornecedor de recursos do Azure recebe um blob encriptado dos dados sem dados de Olá Olá capacidade toodecrypt de qualquer forma ou ter chaves de encriptação de toohello de acesso. Neste modelo, gestão de chaves Olá é feito ao hello chamar a aplicação do serviço e é completamente opaco toohello serviço do Azure.

![Cliente](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>Modelo de encriptação do lado do servidor

Modelos de encriptação do lado do servidor Consulte tooencryption que é executada pela Olá serviço do Azure. Nesse modelo, Olá fornecedor de recursos efetua Olá encriptar e desencriptar operações. Por exemplo, o Storage do Azure pode receber dados em operações de texto simples e executará Olá encriptação e desencriptação internamente. Olá fornecedor de recursos poderá utilizar chaves de encriptação que são geridas pela Microsoft ou pelo cliente de Olá consoante Olá fornecido a configuração. 

![Servidor](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>Modelos de gestão de chaves de encriptação do lado do servidor

Cada um da encriptação do lado do servidor Olá modelos rest implica distinctive características da gestão de chaves. Isto inclui o onde e como as chaves de encriptação são criadas e armazenadas como bem como modelos de acesso de Olá e Olá procedimentos de rotação da chave. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>Encriptação do lado do servidor com o serviço de chaves geridas

Para muitos clientes, o requisito essencial Olá é tooensure Olá dados é encriptado sempre que estejam inativos. Utilizando o serviço gerido chaves de encriptação do lado do servidor permite que este modelo, permitindo que os clientes toomark Olá recurso específico (conta de armazenamento, base de dados SQL, etc.) para a encriptação e deixando todos os aspetos de gestão de chaves, tais como a emissão de chave, rotação e cópia de segurança tooMicrosoft. A maioria dos serviços do Azure que suportam encriptação de Inativos normalmente suportar este modelo de descarga gestão Olá tooAzure de chaves de encriptação de Olá. fornecedor de recursos do Azure de Olá cria chaves Olá, coloca-os no armazenamento seguro e obtém-las quando necessário. Isto significa que o serviço de Olá tem as chaves de toohello acesso total e serviço Olá tem controlo total sobre a gestão de ciclo de vida Olá credenciais.

![Gerido](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

Encriptação do lado do servidor a utilizar chaves de serviço gerida, por conseguinte, rapidamente endereços Olá necessidade toohave a encriptação inativa com o cliente toohello gerais baixa. Se estiver disponível um cliente é normalmente abre Olá portal do Azure para a subscrição de destino Olá e fornecedor de recursos e verifica uma caixa com a indicação de que gostaria de Olá toobe de dados encriptado. Em alguns encriptação do lado do servidor de gestores de recursos com o serviço de chaves geridas está ativada por predefinição. 

Encriptação do lado do servidor com as chaves Microsoft gerida implica serviço Olá tem acesso total toostore e gere chaves Olá. Embora alguns clientes podem pretender chaves de Olá toomanage porque estes sentir que podem garantir uma maior segurança, hello custo e os riscos associados uma solução de armazenamento de chaves devem ser considerados ao avaliar este modelo. Em muitos casos, uma organização pode determinar que riscos de uma solução no local ou restrições de recurso podem maior risco de Olá de gestão de nuvem de encriptação Olá chaves rest.  No entanto, este modelo não pode ser suficiente para as organizações que tenham a criação de Olá requisitos toocontrol ou ciclo de vida das chaves de encriptação de Olá ou pessoal diferente toohave gerir chaves de encriptação de um serviço que são gerir (ou seja, o serviço de Olá segregação da gestão de chaves de Olá modelo global de gestão para o serviço de Olá).

##### <a name="key-access"></a>Acesso a chaves

Olá, quando é utilizada a encriptação do lado do servidor com o serviço gerido chaves, criação de chave, armazenamento e o serviço de acesso são geridos pelo serviço de Olá. Normalmente, os fornecedores de recursos do Azure básico Olá armazenará Olá chaves de encriptação de dados num arquivo que está a fechar toohello dados e rapidamente disponível e acessível ao hello chaves de encriptação de chave são armazenados num arquivo seguro interno.

**Vantagens**

- Configuração simples
- Microsoft gere a rotação da chave, a cópia de segurança e a redundância
- Cliente não ter Olá custos associados a implementação ou Olá risco de um esquema de gestão de chaves personalizadas.

**Desvantagens**

- Nenhum controlo de cliente através de chaves de encriptação Olá (especificação da chave, do ciclo de vida, revogação, etc.)
- Gestão de chaves de toosegregate sem capacidade de modelo global de gestão para o serviço de Olá

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Encriptação do lado do servidor utilizando o cliente chaves geridas no Cofre de chaves do Azure 

Para cenários em que é o requisito de Olá tooencrypt Olá dadosem rest e clientes de chaves de encriptação do controlo Olá podem utilizar a encriptação do lado do servidor a utilizar chaves gerido do cliente no Cofre de chaves. Alguns serviços poderão armazenar apenas Olá de raiz chave de encriptação no Cofre de chaves do Azure e Olá de arquivo encriptado chave de encriptação de dados nos dados de toohello próximo localização interno. Em que os clientes de cenário podem trazer os seus próprios tooKey (BYOK – traga a sua própria chave), do Cofre de chaves ou gerar novos e utilizá-los tooencrypt recursos de Olá assim o desejar. Enquanto o fornecedor de recursos de Olá executa operações de encriptação e desencriptação de Olá utiliza chave Olá configurado como chave de raiz de Olá para todas as operações de encriptação. 

##### <a name="key-access"></a>Acesso a chaves

Olá modelo de encriptação do lado do servidor com as chaves de cliente gerido no Cofre de chaves do Azure envolve Olá serviço ao aceder aos Olá chaves tooencrypt e desencriptar conforme necessário. A encriptação chaves rest que são efetuados serviço tooa acessível através de uma política de controlo de acesso essa chave de Olá tooreceive de acesso de identidade de serviço de concessão de permissões. Um serviço do Azure em execução em nome de uma subscrição associada pode ser configurado com uma identidade para esse serviço dentro dessa subscrição. serviço de Olá pode efetuar a autenticação do Azure Active Directory e receber um token de autenticação identificar-se automaticamente como esse serviço agir em nome de subscrição de Olá. Esse token poderá, então, ser apresentado tooKey cofre tooobtain uma chave foi indicado acesso.

Para operações utilizando chaves de encriptação, uma identidade de serviço pode ser concedida acesso tooany de Olá seguintes operações: desencriptar, encriptar, unwrapKey, wrapKey, certifique-se, iniciar sessão, obter, listar, atualizar, criar, importar, eliminar, cópia de segurança e restaurar.

tooobtain uma chave para utilização no encriptar ou desencriptar dados na identidade de serviço de Olá rest que Olá Resource Manager a instância de serviço será executado como têm de ter UnwrapKey (chave de Olá tooget para desencriptação) e WrapKey (tooinsert uma chave para o Cofre de chaves ao criar uma nova chave).


>[!NOTE] 
>Para mais detalhes sobre o Cofre de chaves autorização Consulte Olá proteger a sua página Cofre de chaves no Olá [documentação do Cofre de chaves do Azure](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault). 

**Vantagens**

- Controlo total sobre chaves de Olá utilizado – geridas no Cofre de chaves do cliente Olá sob o controlo do cliente Olá chaves de encriptação.
- Capacidade tooencrypt mestre de tooone vários serviços
- Pode segregar a gestão de chaves do modelo global de gestão para o serviço de Olá
- Pode definir o serviço e a localização da chave em regiões

**Desvantagens**

- O cliente tem responsabilidade completa de gestão de chaves de acesso
- O cliente tem responsabilidade completa de gestão do ciclo de vida das chave
- Overhead de configuração do & configuration adicional

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>Encriptação do lado do servidor com o serviço de chaves geridas no hardware de cliente controlado

Para cenários em que o requisito de Olá é tooencrypt Olá dadosem rest e gerir chaves de Olá num repositório proprietária fora do controlo da Microsoft, alguns serviços do Azure permitem o modelo de gestão de chaves de anfitrião sua própria chave (HYOK) Olá. Neste modelo, serviço Olá tem de obter chave Olá de um site externo e, por conseguinte, as garantias de disponibilidade e desempenho são afetadas e configuração for mais complexa. Além disso, uma vez que o serviço de Olá tem acesso toohello DEK durante a encriptação de Olá e operações de desencriptação Olá geral garantias de segurança deste modelo são semelhantes toowhen Olá, as chaves são geridos de cliente no Cofre de chaves do Azure.  Como resultado, este modelo não é adequado para a maioria das organizações, a menos que têm requisitos de gestão de chaves específico, sendo necessárias-lo. Devido a limitações de toothese, a maioria dos serviços do Azure não suportam a encriptação do lado do servidor utilizando as chaves de servidor gerido no hardware de cliente controlado.

##### <a name="key-access"></a>Acesso a chaves

Quando é utilizada com chaves de serviço gerida no hardware de cliente controlado de encriptação do lado do servidor são mantidas chaves Olá num sistema configurado pelo cliente de Olá. Serviços do Azure que suportem este modelo fornecem um meio de estabelecimento de um cliente de tooa ligação segura fornecido armazenamento de chaves.

**Vantagens**

- Controlo total sobre a chave de raiz de Olá utilizado – encriptação de chaves são geridas por um arquivo de cliente fornecido
- Capacidade tooencrypt mestre de tooone vários serviços
- Pode segregar a gestão de chaves do modelo global de gestão para o serviço de Olá
- Pode definir o serviço e a localização da chave em regiões

**Desvantagens**

- Responsabilidade completa para o armazenamento de chaves, segurança, desempenho e disponibilidade
- Responsabilidade completa de gestão de chaves de acesso
- Responsabilidade completa de gestão do ciclo de vida das chave
- Programa de configuração significativo, configuração e os custos de manutenção em curso
- Dependência de aumento de disponibilidade de rede entre o Centro de dados do Olá cliente e os datacenters do Azure.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Encriptação de Inativos na cloud services da Microsoft

Serviços Cloud da Microsoft são utilizados em todos os modelos de nuvem três: IaaS, PaaS, SaaS. Abaixo, pode encontrar exemplos de como se ajustar a cada modelo:

- Serviços de software, referidos tooas Software como um servidor ou o SaaS, que têm aplicações fornecidas pela nuvem Olá como o Office 365.
- Serviços da plataforma que clientes tirar partido de nuvem Olá nas respetivas aplicações, utilizando a nuvem de Olá para coisas, como a funcionalidade de barramento de armazenamento, de serviço e de análise.
- Serviços de infraestrutura ou de infraestrutura como serviço (IaaS) na qual cliente implementar sistemas operativos e aplicações que estão alojadas no Olá nuvem e, possivelmente, tirar partido de outros serviços em nuvem.

### <a name="encryption-at-rest-for-saas-customers"></a>Encriptação de Inativos para clientes de SaaS

Software como um clientes do serviço (SaaS) têm normalmente encriptação de inativos disponíveis em cada serviço ou ativada. Serviços do Office 365 tem várias opções para a encriptação de tooverify ou ativar clientes inativos. Para obter informações sobre serviços do Office 365, consulte tecnologias de encriptação de dados para o Office 365.

### <a name="encryption-at-rest-for-paas-customers"></a>Encriptação de Inativos para clientes de PaaS

Plataforma como dados de um cliente de serviço (PaaS) normalmente reside num ambiente de execução da aplicação e quaisquer fornecedores de recursos do Azure utilizados toostore dados de cliente. a encriptação Olá toosee rest opções disponíveis tooyou examinar a tabela de Olá abaixo para plataformas de armazenamento e da aplicação Olá que utilizar. Se suportado, ligações tooinstructions sobre como ativar a encriptação de Inativos são fornecidos para cada fornecedor de recursos. 

### <a name="encryption-at-rest-for-iaas-customers"></a>Encriptação de Inativos para clientes do IaaS

Infraestrutura como um clientes do serviço (IaaS) pode ter uma variedade de serviços e aplicações em utilização. Serviços de IaaS podem ativar a encriptação de Inativos no respetivo Azure alojada máquinas virtuais e VHDs utilizando a Azure Disk Encryption. 

#### <a name="encrypted-storage"></a>Armazenamento encriptado

Como PaaS, soluções de IaaS podem tirar partido outros serviços do Azure que armazenam dados encriptados em pausa. Nestes casos, pode ativar Olá encriptação no suporte de Rest conforme fornecida pelos cada serviço do Azure foram consumido. Olá tabela abaixo enumera armazenamento principais Olá, serviços e plataformas de aplicação e modelo de Olá de encriptação de Inativos suportado. Se suportado, são fornecidas hiperligações tooinstructions sobre como ativar a encriptação de inativos. 

#### <a name="encrypted-compute"></a>Encriptados de computação

A encriptação completa uma solução de Rest requer que Olá dados nunca são continuados no formato não encriptado. Enquanto utilização, num hello do servidor a carregar dados na memória, dados podem ser localmente persistente de várias formas, incluindo o ficheiro de paginação do Windows hello, as informações de falhas e Olá qualquer registo de aplicação pode executar. tooensure estes dados são encriptados em descanso ao aplicações de IaaS podem utilizar Azure Disk Encryption uma máquina virtual de IaaS do Azure (Windows ou Linux) e o disco virtual. 

#### <a name="custom-encryption-at-rest"></a>Encriptação personalizado Inativos

Recomenda-se que sempre que possível, aplicações de IaaS tirar partido do Azure Disk Encryption e encriptação em Opções de Rest fornecidas por todos os serviços do Azure foram consumidos. Em alguns casos, tais como requisitos de encriptação de dados ou não do Azure com base em armazenamento, um programador de uma aplicação de IaaS poderá ter a encriptação tooimplement rest próprios. Os programadores de IaaS soluções podem melhor integram expectativas de gestão e o cliente do Azure através do aproveitamento determinados componentes do Azure. Especificamente, os programadores devem utilizar Olá Cofre de chaves do Azure service tooprovide proteger o armazenamento de chaves, bem como fornecer os seus clientes com opções de gestão de chaves consistente com que mais Azure de serviços da plataforma. Além disso, as soluções personalizadas devem utilizar chaves de encriptação do Azure identidades de serviço geridas tooenable serviço contas tooaccess. Para obter informações de Programador no Cofre de chaves do Azure e identidades de serviço geridas por ver os seus respetivos SDKs.

## <a name="azure-resource-providers-encryption-model-support"></a>Suporte de modelo de encriptação de fornecedores de recursos do Azure

Serviços do Microsoft Azure cada suporta um ou mais dos modelos de rest a encriptação Olá. Para alguns serviços, no entanto, um ou mais dos modelos de encriptação de Olá poderão não ser aplicáveis. Além disso, os serviços podem de versão suporte para estes cenários em diferentes agendamentos. Esta secção descreve a encriptação Olá rest suporte momento Olá desta redação para cada um dos serviços de armazenamento de dados do Azure principais Olá.

### <a name="azure-disk-encryption"></a>Encriptação de disco do Azure

Qualquer cliente utilizando a infraestrutura do Azure como um serviço (IaaS) funcionalidades podem alcançar a encriptação de Inativos as respetivas VMs de IaaS e discos através do Azure Disk Encryption. Para obter mais informações sobre o disco do Azure encriptação Consulte Olá [documentação do Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

#### <a name="azure-storage"></a>Storage do Azure

Blob do Azure e ficheiro suporta encriptação de Inativos para cenários de encriptado do lado do servidor, bem como os dados de cliente encriptado (encriptação do lado do cliente).

- Lado do servidor: os clientes utilizam o armazenamento de Blobs do Azure podem ativar a encriptação de Inativos em cada conta de recursos de armazenamento do Azure. Uma vez ativada encriptação do lado do servidor é feita transparente toohello aplicação. Consulte [encriptação do serviço de armazenamento do Azure para dados Inativos](https://docs.microsoft.com/azure/storage/storage-service-encryption) para obter mais informações.
- Do lado do cliente: a encriptação do lado do cliente de Blobs do Azure é suportada. Quando utilizar a encriptação do lado do cliente clientes encriptar Olá dados e carregar dados de Olá como um blob encriptado. Gestão de chaves é feita pelo cliente de Olá. Consulte [encriptação do lado do cliente e o Cofre de chaves do Azure para armazenamento do Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) para obter mais informações.


#### <a name="sql-azure"></a>SQL Azure

Atualmente, o SQL Azure suporta encriptação de Inativos para cenários de encriptação do lado do cliente e do lado de serviço gerida pela Microsoft.

Servidor de suporte para encriptação atualmente é fornecida através da funcionalidade SQL de Olá denominada a encriptação transparente de dados. Depois de um cliente do SQL Azure permite chave TDE são automaticamente criados e geridos para os mesmos. Pode ser ativada a encriptação de Inativos níveis Olá da base de dados e servidor. A partir de Junho de 2017, [encriptação de dados transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx) será ativada por predefinição nas bases de dados recentemente criados.

Encriptação do lado do cliente de dados SQL Azure é suportada através de Olá [sempre encriptados](https://msdn.microsoft.com/library/mt163865.aspx) funcionalidade. Sempre encriptado utiliza uma chave que criada e armazenada pelo cliente de Olá. Os clientes podem armazenar a chave mestra de Olá num arquivo de certificados do Windows, o Cofre de chaves do Azure ou um módulo de Hardware de segurança local. Utilizar SQL Server Management Studio, os utilizadores do SQL Server escolher que chave gostaria toouse tooencrypt que coluna.

|                                  |                |                     | **Modelo de encriptação**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **Cliente** |
|                                  | **Gestão de chaves** | **O serviço gerido chave** | **Cliente gerido no Cofre de chaves** | **Cliente gerido no local** |        |
| **Armazenamento e bases de dados**            |                |                     |                              |                              |        |
| Disco (IaaS)                      |                | -                   | Sim                          | Sim*                         | -      |
| SQL Server (IaaS)                |                | Sim                 | Sim                          | Sim                          | Sim    |
| Azure SQL (PaaS)                 |                | Sim                 | Pré-visualização                      | -                            | Sim    |
| Armazenamento do Azure (Blobs de blocos/páginas) |                | Sim                 | Pré-visualização                      | -                            | Sim    |
| Armazenamento do Azure (ficheiros)            |                | Sim                 | -                            | -                            | -      |
| Armazenamento do Azure (tabelas, filas)   |                | -                   | -                            | -                            | Sim    |
| Cosmos BD (documento DB)          |                | Sim                 | -                            | -                            | -      |
| StorSimple                       |                | Sim                 | -                            | -                            | Sim    |
| Cópia de segurança                           |                | -                   | -                            | -                            | Sim    |
| **Intelligence e análise**       |                |                     |                              |                              |        |
| Azure Data Factory               |                | Sim                 | -                            | -                            | -      |
| Azure Machine Learning           |                | -                   | Pré-visualização                      | -                            | -      |
| Azure Stream Analytics           |                | Sim                 | -                            | -                            | -      |
| HDInsights (armazenamento de Blobs do Azure)  |                | Sim                 | -                            | -                            | -      |
| HDInsights (armazenamento do Data Lake)   |                | Sim                 | -                            | -                            | -      |
| Azure Data Lake Store            |                | Sim                 | Sim                          | -                            | -      |
| Catálogo de Dados do Azure               |                | Sim                 | -                            | -                            | -      |
| Power BI                         |                | Sim                 | -                            | -                            | -      |
| **Serviços IoT**                     |                |                     |                              |                              |        |
| IoT Hub                          |                | -                   | -                            | -                            | Sim    |
| Service Bus                      |                | -              | -                            | -                            | Sim    |
| Event Hubs                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>Conclusão

Proteção de dados de cliente armazenados dentro de serviços do Azure é de importância essencial da tooMicrosoft. Todos os Azure alojada serviços são consolidar tooproviding encriptação em Opções de Rest. Serviços de intelligence e serviços fundamentais sobre como o Storage do Azure, SQL Azure e análise de chave já fornecem a encriptação em Opções de Rest. Alguns destes serviços suportam chaves cliente controlada e de encriptação do lado do cliente, bem como chaves geridas e encriptação de serviço. Serviços do Microsoft Azure são amplamente Otimização da encriptação na disponibilidade de Rest e novas opções estejam planeadas para pré-visualização e disponibilidade geral em meses futuros Olá.

