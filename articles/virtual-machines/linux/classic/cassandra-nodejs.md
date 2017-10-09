---
title: aaaRun Cassandra com Linux no Azure | Microsoft Docs
description: "Como toorun um Cassandra cluster no Linux em máquinas virtuais do Azure a partir de uma aplicação Node.js"
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Executar o Cassandra com o Linux no Azure e Aceder a partir de Node.js
> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Ver modelos do Resource Manager para [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) e [Spark cluster e Cassandra em CentOS](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Descrição geral
Microsoft Azure é uma plataforma de nuvem aberto que executa ambos os Microsoft como bem como software não Microsoft que inclui os sistemas operativos, servidores de aplicações, mensagens middleware, bem como bases de dados NoSQL e SQL de ambos os modelos de comerciais e abrir a origem. Criação de resilientes serviços em nuvens públicas, incluindo o Azure requer um planeamento cuidadoso e arquitetura deliberate para ambos os servidores de aplicações como camadas de armazenamento bem. Arquitetura de armazenamento distribuído do Cassandra naturalmente ajuda na criação de sistemas elevados tolerante a falhas de cluster de falhas. Cassandra é uma base de dados NoSQL mantido pelo Apache Software Foundation a cassandra.apache.org; escala da nuvem Cassandra é escrito em Java e, por conseguinte, é executado no Windows, bem como em Linux plataformas.

Este artigo aborda Olá é tooshow Cassandra implementação Ubuntu como um cluster único e vários dados center tirar partido das máquinas virtuais do Microsoft Azure e redes virtuais. Olá implementação de cluster para cargas de trabalho de produção otimizada está fora do âmbito deste artigo porque requer configuração do nó de disco multi, design de topologia do anel adequado e os dados de modelação toosupport Olá necessário replicação, consistência dos dados, débito e requisitos de elevada disponibilidade.

Este guia de artigo tooshow uma abordagem fundamental que esteja envolvido na criação Olá Cassandra cluster em comparação com Docker, Chef ou Puppet, que pode efetuar Olá muito mais fácil de implementação da infraestrutura.  

## <a name="hello-deployment-models"></a>Olá modelos de implementação
Funcionamento em rede do Microsoft Azure permite a implementação Olá dos clusters privadas isolados, acesso Olá que pode ser segurança de rede detalhada bem tooattain restrito.  Uma vez que este artigo sobre implementação de Cassandra Olá um nível de fundamentais a mostrar, incidirá não no nível de consistência Olá e conceção do armazenamento ideal de Olá de débito. Eis Olá lista dos requisitos de rede para o nosso hipotético cluster:

* Sistemas externos que não é possível aceder Cassandra base de dados da dentro ou fora do Azure
* Cluster de Cassandra tem toobe atrás de um balanceador de carga para tráfego de thrift
* Implementar Cassandra nós em dois grupos em cada centro de dados para um disponibilidade do cluster avançada
* Bloquear cluster Olá, por isso, que só o farm de servidores de aplicação possui base de dados do access toohello diretamente
* Não existem públicas pontos finais de rede diferente de SSH
* Cada nó de Cassandra tem um endereço IP interno fixo

Cassandra pode ser implementado tooa única região do Azure ou regiões toomultiple com base na carga de trabalho Olá natureza Olá distribuído. Modelo de implementação de multirregião pode ser aproveitadas tooserve os utilizadores finais próximo tooa específico geografia através de Olá mesma infraestrutura de Cassandra. Resolvida replicação do nó incorporada do Cassandra de sincronização de Olá do mestre multi escreve provenientes de múltiplos centros de dados e apresenta uma vista de Olá dados tooapplications consistente. Também pode ajudar a implementação de multirregião mitigação de riscos Olá de falhas no serviço Azure Olá mais ampla. Topologia de replicação e consistência ajustáveis do Cassandra irão ajudar a satisfazer as necessidades de RPO diversificadas das aplicações.

### <a name="single-region-deployment"></a>Implementação única região
Iremos irá começar com uma implementação única região e recolher Olá learnings na criação de um modelo de multirregião. Redes virtuais do Azure será utilizado toocreate isolada sub-redes, para que possam ser satisfeitos requisitos de segurança de rede de Olá mencionados acima.  processo de Olá descrito na criação de implementação de única região Olá utiliza Ubuntu 14.04 LTS e Cassandra 2.08; No entanto, o processo de Olá pode facilmente ser adotado toohello outros variantes do Linux. Olá seguem-se algumas das características de systemic Olá da implementação do Olá única região.  

**Elevada disponibilidade:** Olá nós Cassandra mostrados na Olá figura 1 são implementadas conjuntos de disponibilidade de tootwo para que nós de Olá são distribuídas entre vários domínios de falhas de elevada disponibilidade. VMs anotadas com cada conjunto de disponibilidade está mapeada too2 domínios de falhas.  Microsoft Azure utiliza Olá conceito de toomanage de domínio de falha não planeada do tempo (por exemplo, falhas de hardware ou software) ao conceito de Olá de domínio de atualização (por exemplo, o convidado ou anfitrião SO aplicação de patches/atualizações, as atualizações de aplicações) é utilizado para gerir agendada tempo. Consulte [recuperação após desastre e elevada disponibilidade para aplicações do Azure](http://msdn.microsoft.com/library/dn251004.aspx) para a função de Olá de domínios de falhas e a atualização na attaining elevada disponibilidade.

![Implementação única região](./media/cassandra-nodejs/cassandra-linux1.png)

Figura 1: Implementação de única região

Tenha em atenção que no momento desta redação da Olá, Azure não permite o mapeamento de explícita Olá de um grupo de domínio de falhas específicas do VMs tooa; Por conseguinte, mesmo com o modelo de implementação de Olá mostrado na figura 1, é estatisticamente provável que todas as máquinas de virtuais Olá podem ser mapeadas tootwo domínios de falhas em vez de quatro.

**Tráfego de Thrift de balanceamento de carga:** bibliotecas de cliente de Thrift no interior do servidor de web de Olá ligam toohello cluster através de um balanceador de carga interno. Isto requer que o processo de Olá de adicionar a sub-rede de Olá carga interno balanceador toohello "dados" (consulte a figura 1) no contexto de Olá do cluster de Cassandra Olá de alojamento do serviço de nuvem Olá. Assim que o Balanceador de carga interno Olá estiver definida, a cada nó requer toobe de ponto final com balanceamento de carga de Olá adicionada com anotações Olá de um conjunto com balanceamento de carga anteriormente com o nome do Balanceador de carga definido. Consulte [Azure interno balanceamento de carga ](../../../load-balancer/load-balancer-internal-overview.md)para obter mais detalhes.

**Cluster Seeds:** é importante tooselect Olá maioria de nós de elevada disponibilidade para seeds como Olá novos nós irão comunicar com o seed nós toodiscover Olá topologia cluster Olá. Um nó de cada conjunto de disponibilidade está designado como o seed nós tooavoid único ponto da falha.

**Fator de replicação e o nível de consistência:** compilação na elevada disponibilidade e dados durabilidade do Cassandra é caracterizada por Olá fator de replicação (RF - número de cópias de cada linha armazenadas num cluster de Olá) e o nível de consistência (número de réplicas toobe leitura/escrita antes de o devolver Olá resultado toohello do chamador). Fator de replicação é especificada durante a Olá criação KEYSPACE (semelhante tooa base de dados relacional), enquanto que o nível de consistência Olá é especificado ao emitir consultas CRUD Olá. Consulte a documentação de Cassandra em [configurar para consistência](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para detalhes de consistência e fórmula Olá para o cálculo de quórum.

Cassandra suporta dois tipos de modelos de integridade de dados – consistência e a consistência Eventual; Olá fator de replicação e nível de consistência serão em conjunto determinam se os dados de Olá serão consistentes, assim que uma operação de escrita foi concluída ou que será eventualmente consistente. Por exemplo, o QUÓRUM (por exemplo, um) especificar QUÓRUM como Olá que nível de consistência será sempre garante a consistência de dados ao qualquer nível de consistência, abaixo o número de Olá de toobe réplicas escrito como tooattain necessário resulta em dados que está a ser eventualmente consistente.

cluster de nó de 8 Olá mostrado acima, com um fator de replicação de 3 e QUÓRUM (2 nós são lidas ou escritas para consistência) ao nível de consistência de leitura/escrita, pode sobreviver perda teórico Olá de em Olá a maioria das 1 nó por replicação grupo antes do início da aplicação de Olá Falha de Olá dar por isso. Esta parte do princípio de que todos os espaços de chave de Olá tem bem com balanceamento de pedidos de leitura/escrita.  Olá, são parâmetros Olá, que iremos utilizar para o cluster de Olá implementado:

Configuração de cluster de Cassandra única região:

| Parâmetro de cluster | Valor | Observações |
| --- | --- | --- |
| Número de nós (N) |8 |Número total de nós no cluster de Olá |
| Fator de replicação (RF) |3 |Número de réplicas de uma linha especificada |
| Nível de consistência (escrita) |QUORUM[(RF/2) +1) = resultado 2] Olá de Olá fórmula é arredondada para baixo |Escreve no Olá a maioria das 2 réplicas antes do envio do chamador toohello resposta Olá réplica 3rd é escrita de forma eventualmente consistente. |
| Nível de consistência (leitura) |QUÓRUM [(RF/2) + 1 = 2] resultado Olá de fórmula Olá é arredondado para baixo |Lê 2 réplicas antes de enviar o chamador de toohello de resposta. |
| Estratégia de replicação |Consulte NetworkTopologyStrategy [replicação de dados](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) na documentação de Cassandra para obter mais informações |Compreende a topologia de implementação de Olá e coloca réplicas em nós, para que todas as réplicas de Olá não acabar em Olá mesmo bastidor |
| Snitch |Consulte GossipingPropertyFileSnitch [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) na documentação de Cassandra para obter mais informações |NetworkTopologyStrategy utiliza um conceito de topologia do snitch toounderstand Olá. GossipingPropertyFileSnitch proporciona um melhor controlo em cada nó toodata Centro e em Bastidor de mapeamento. Olá cluster utiliza, em seguida, gossip toopropagate, estas informações. Isto é muito mais simples no dinâmica tooPropertyFileSnitch relativo para o IP definição |

**Considerações do Azure para o Cassandra Cluster:** capacidade de máquinas virtuais do Microsoft Azure utiliza o Blob storage do Azure para a persistência de disco; Armazenamento do Azure guarda 3 réplicas de cada disco para uma durabilidade elevada. Isto significa que cada linha da dados inseridos na tabela Cassandra já está armazenada na 3 réplicas e, por conseguinte, consistência de dados está já tratada, mesmo que esteja Olá fator de replicação (RF) 1. problema de principal de Olá com fator de replicação que está a ser 1 é que aplicação Olá será tempo de inatividade, mesmo se a um único nó Cassandra falha. No entanto, se um nó para baixo para problemas de Olá (por exemplo, hardware, falhas de software do sistema) reconhecidos pelo controlador de recursos do Azure, irá aprovisionar um novo nó no seu lugar utilizando Olá mesmo unidades de armazenamento. Aprovisionamento de um novo nó tooreplace Olá antigo um processo poderá demorar alguns minutos.  Da mesma forma para atividades de manutenção planeada, como as alterações de SO convidado, Cassandra atualiza e as alterações de aplicação o controlador de recursos do Azure efetua a implementar atualizações de nós de Olá num cluster de Olá.  Implementar atualizações também poderá demorar baixo alguns nós numa altura e, por conseguinte, o cluster Olá pode ter breve tempo de inatividade para partições alguns. No entanto, não poderá ser perdidos devido a redundância de armazenamento do Azure incorporada toohello dados Olá.  

Para sistemas implementado tooAzure não necessita de elevada disponibilidade (por exemplo, cerca de 99,9 que é equivalente too8.76 hrs/ano; consulte [elevada disponibilidade](http://en.wikipedia.org/wiki/High_availability) para obter detalhes) poderá ser capaz de toorun com RF = 1 e o nível de consistência = ONE.  Para aplicações com requisitos de elevada disponibilidade, RF = 3 e o nível de consistência = QUÓRUM serão tolerar Olá tempo de um de nós de Olá uma das réplicas Olá. RF = 1 em implementações tradicionais (por exemplo, no local) não pode ser utilizado devido toohello possíveis perdas de dados resultantes de problemas como falhas de disco.   

## <a name="multi-region-deployment"></a>Implementação de multirregião
Data center-com suporte para replicação e o modelo de consistência descrito acima ajuda-o com a implementação de multirregião Olá Box Olá sem Olá da Cassandra necessidade de quaisquer ferramentas externas. Isto é bastante diferente do Olá tradicionais bases de dados relacionais em que o programa de configuração de Olá para espelhamento da base de dados para escritas multi-mestre pode ser bastante complexo. Cenários de utilização de Olá incluindo Olá seguinte pode ajudar a Cassandra numa região multi configurar:

**Implementação baseada em proximidade:** aplicações multi-inquilino, com Limpar mapeamento de utilizadores de inquilino-para-região, pode ser benefited por baixas latências do cluster de multirregião Olá. Por exemplo, um gestão de aprendizagem sistemas operativos instituições educational podem implementar um cluster distribuído nos EUA leste e EUA oeste regiões tooserve Olá respetivos campuses para transacional, bem como a análise. dados de Olá podem ser localmente consistentes em Olá tempo leituras e escritas e podem ser eventualmente consistentes em ambas as regiões de Olá. Existem outros exemplos de como a distribuição de suporte de dados, comércio e nada e tudo o que funciona georreplicação concentrated utilizador base é um caso de utilização boa para este modelo de implementação.

**Elevada disponibilidade:** redundância é um fator chave attaining elevada disponibilidade de hardware e software; Consulte edifício fiável sistemas de nuvem no Microsoft Azure para obter mais detalhes. No Microsoft Azure, Olá forma fiável apenas de atingirem a total redundância verdadeira é implementar um cluster de multirregião. É possível implementar aplicações num modo ativo-ativo ou ativo-passivo e se uma das regiões Olá estiver desativado, o Gestor de tráfego do Azure pode redirecionar região ativa do tráfego toohello.  Com a implementação de única região Olá, se for de disponibilidade de Olá 99,9, uma implementação de dois região pode obter um disponibilidade dos 99.9999 calculado pela fórmula Olá: (1-(1-0.999) * (1-0.999)) * 100); Consulte Olá acima documento para obter mais detalhes.

**Recuperação após desastre:** cluster multirregião Cassandra, se concebido corretamente, pode conseguir falhas de center catastrófica de dados. Se uma região estiver em baixo, Olá aplicação implementada tooother regiões podem começar a servir os utilizadores finais de Olá. Como quaisquer outras empresas continuidade implementações, a aplicação de Olá tem tolerância a falhas para algumas perda de dados resultantes de dados de Olá no pipeline assíncrona Olá toobe. No entanto, Cassandra torna recuperação Olá muito swifter à hora de Olá executada por processos de recuperação de bases de dados tradicionais. Figura 2 mostra o modelo de implementação de multirregião típica Olá com oito nós em cada região. Ambas as regiões são imagens de espelho de si para Olá mesmo de symmetry; estruturas de mundo real dependem do tipo de carga de trabalho de Olá (por exemplo, analítico ou transacional), RPO, RTO, consistência dos dados e requisitos de disponibilidade.

![Implementação de região de múltipla](./media/cassandra-nodejs/cassandra-linux2.png)

Figura 2: Implementação de multirregião Cassandra

### <a name="network-integration"></a>Integração de rede
Conjuntos de máquinas virtuais, redes tooprivate implementado localizados em duas regiões comunica com entre si utilizando um túnel VPN. túnel VPN de Olá liga-se dois gateways de software aprovisionados durante o processo de implementação de rede Olá. Ambas as regiões têm a arquitetura de rede semelhante em termos de sub-redes "web" e "dados"; Redes do Azure permite a criação de Olá de sub-redes tantos conforme necessário e aplicar ACLs conforme necessário para a segurança de rede. Ao conceber a topologia de cluster Olá inter-data center comunicação latência e Olá económico impacto de Olá rede tráfego necessidade toobe considerado.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Consistência dos dados para a implementação de centro de dados de vários
Distribuída toobe necessidade de implementações em consideração impacto de topologia de cluster Olá no débito e elevada disponibilidade. Olá RF e o nível de consistência toobe necessidade selecionado forma que Olá quórum não depende disponibilidade Olá de todos os centros de dados de Olá.
Para um sistema que tem de consistência elevada, um LOCAL_QUORUM para o nível de consistência (para leituras e escritas) irá garantir que esse Olá local lê e escreve forem satisfeitas do Olá local nós enquanto os dados são replicadas de forma assíncrona toohello centros de dados remota.  Tabela 2 resume configuração Olá escrever os detalhes para o cluster de multirregião Olá descrito mais à frente no Olá cópias de segurança.

**Configuração de cluster Cassandra dois-região**

| Parâmetro de cluster | Valor | Observações |
| --- | --- | --- |
| Número de nós (N) |8 + 8 |Número total de nós no cluster de Olá |
| Fator de replicação (RF) |3 |Número de réplicas de uma linha especificada |
| Nível de consistência (escrita) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] resultado Olá de fórmula Olá é arredondado para baixo |2 nós serão escritos toohello primeiro centro de dados de forma síncrona; Olá outros 2 nós necessários para quórum serão escritos no modo assíncrono toohello 2nd Centro de dados. |
| Nível de consistência (leitura) |LOCAL_QUORUM ((RF/2) + 1) = 2 resultado Olá de fórmula Olá é arredondado para baixo |Pedidos de leitura são satisfeitos de apenas uma região; são lidos a 2 nós antes do envio de resposta Olá toohello back-cliente. |
| Estratégia de replicação |Consulte NetworkTopologyStrategy [replicação de dados](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) na documentação de Cassandra para obter mais informações |Compreende a topologia de implementação de Olá e coloca réplicas em nós, para que todas as réplicas de Olá não acabar em Olá mesmo bastidor |
| Snitch |Consulte GossipingPropertyFileSnitch [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) na documentação de Cassandra para obter mais informações |NetworkTopologyStrategy utiliza um conceito de topologia do snitch toounderstand Olá. GossipingPropertyFileSnitch proporciona um melhor controlo em cada nó toodata Centro e em Bastidor de mapeamento. Olá cluster utiliza, em seguida, gossip toopropagate, estas informações. Isto é muito mais simples no dinâmica tooPropertyFileSnitch relativo para o IP definição |

## <a name="hello-software-configuration"></a>Olá configuração de SOFTWARE
Olá seguintes versões de software é utilizado durante a implementação de Olá:

<table>
<tr><th>Software</th><th>Origem</th><th>Versão</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

Uma vez que transferir da JRE requer manual aceitação de licença do Oracle, implementação de Olá toosimplify, transferência que todas Olá ambiente de trabalho do software necessárias toohello para carregar mais tarde para a imagem de modelo do Ubuntu Olá que iremos criar como um cluster de toohello precursor implementação.

Transferir Olá acima software para um diretório de transferências bem conhecido (por exemplo, %TEMP%/downloads no Windows ou ~/Downloads na maioria das distribuições de Linux ou Mac) no computador local Olá.

### <a name="create-ubuntu-vm"></a>CRIAR A VM COM UBUNTU
Neste passo do processo de Olá iremos criar Ubuntu imagem com o software de pré-requisito Olá para que hello imagem pode ser reutilizada para o aprovisionamento de vários nós Cassandra.  

#### <a name="step-1-generate-ssh-key-pair"></a>PASSO 1: Gerar par de chaves de SSH
Azure tem uma chave pública que é PEM ou DER codificado em Olá tempo de aprovisionamento de X509. Gerar um par de chaves públicas/privadas, utilizando instruções Olá localizadas como tooUse SSH com o Linux no Azure. Se planear toouse putty.exe como um cliente SSH no Windows ou Linux, tem de tooconvert Olá PEM codificado em formato de tooPPK chaves privadas RSA utilizando puttygen.exe; Olá as instruções para isto podem ser encontradas na Olá acima página web.

#### <a name="step-2-create-ubuntu-template-vm"></a>PASSO 2: Criar o modelo de Ubuntu VM
VM, do modelo de Olá toocreate sessão Olá Azure clássico Olá de portal e utilize a seguinte sequência: clique em novo, COMPUTAÇÃO, máquina VIRTUAL, FROM GALERIA, UBUNTU, Ubuntu Server 14.04 LTS e, em seguida, clique em seta para a direita Olá. Para um tutorial que descreve como toocreate uma VM com Linux, consulte Criar uma Linux em execução de Máquina Virtual.

Introduza Olá seguindo as informações do ecrã de Olá "configuração da Máquina Virtual" #1:

<table>
<tr><th>NOME DO CAMPO              </td><td>       VALOR DO CAMPO               </td><td>         OBSERVAÇÕES                </td><tr>
<tr><td>DATA DE LANÇAMENTO DA VERSÃO    </td><td> Selecione uma data no Olá pendente</td><td></td><tr>
<tr><td>NOME DA MÁQUINA VIRTUAL    </td><td> modelo de CASS                   </td><td> Este é o nome de anfitrião de Olá do Olá VM </td><tr>
<tr><td>CAMADA                     </td><td> STANDARD                           </td><td> Deixe a predefinição de Olá              </td><tr>
<tr><td>TAMANHO                     </td><td> A1                              </td><td>Tem de selecionar Olá que VM com base no Olá e/s; para este fim, deixe a predefinição de Olá </td><tr>
<tr><td> NOVO NOME DE UTILIZADOR             </td><td> localadmin                       </td><td> "admin" é um nome de utilizador reservado no Ubuntu 12. xx e depois</td><tr>
<tr><td> AUTENTICAÇÃO         </td><td> Clique em caixa de verificação                 </td><td>Verifique se quiser toosecure com uma chave SSH </td><tr>
<tr><td> CERTIFICADO             </td><td> nome de ficheiro do certificado de chave pública Olá </td><td> Utilize a chave pública Olá gerado anteriormente</td><tr>
<tr><td> Nova palavra-passe    </td><td> palavra-passe segura </td><td> </td><tr>
<tr><td> Confirmar palavra-passe    </td><td> palavra-passe segura </td><td></td><tr>
</table>

Introduza Olá seguindo as informações do ecrã de Olá "configuração da Máquina Virtual" #2:

<table>
<tr><th>NOME DO CAMPO             </th><th> VALOR DO CAMPO                       </th><th> OBSERVAÇÕES                                 </th></tr>
<tr><td> SERVIÇO EM NUVEM    </td><td> Criar um novo serviço de nuvem    </td><td>Serviço em nuvem é um recursos de computação do contentor como máquinas virtuais</td></tr>
<tr><td> NOME DE DNS DO SERVIÇO DE NUVEM    </td><td>ubuntu template.cloudapp.net    </td><td>Dê um nome de Balanceador de carga com máquina</td></tr>
<tr><td> REGIÃO/GRUPO DE AFINIDADE/REDE VIRTUAL </td><td>    EUA Oeste    </td><td> Selecione uma região a partir da qual as suas aplicações web aceder ao cluster de Cassandra Olá</td></tr>
<tr><td>CONTA DE ARMAZENAMENTO </td><td>    Utilizar predefinição    </td><td>Utilizar a conta do storage predefinida Olá ou uma conta de armazenamento previamente criada numa região específica</td></tr>
<tr><td>CONJUNTO DE DISPONIBILIDADE </td><td>    Nenhuma </td><td>    Pode deixar em branco</td></tr>
<tr><td>PONTOS FINAIS    </td><td>Utilizar predefinição </td><td>    Utilize a configuração de SSH Olá predefinida </td></tr>
</table>

Clique em seta para a direita, deixe as predefinições de Olá no ecrã de Olá #3 e clique em Olá "verificar" botão toocomplete Olá VM processo de aprovisionamento. Após alguns minutos, Olá VM com o nome "ubuntu-modelo de Olá" deve estar no estado "em execução".

### <a name="install-hello-necessary-software"></a>INSTALAR Olá SOFTWARE necessário
#### <a name="step-1-upload-tarballs"></a>PASSO 1: Carregamento tarballs
Utilizar o scp ou pscp, Olá cópia anteriormente transferidos software demasiado ~ / diretório de transferências utilizando Olá segue o formato de comando:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp servidor-jre-8u5-linux-x64.tar.gzlocaladmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Repita Olá acima comando para JRE, bem como para bits de Cassandra Olá.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>PASSO 2: Preparar a estrutura de diretórios Olá e extrair os arquivos de Olá
Inicie sessão no Olá VM e criar a estrutura de diretórios Olá e extrair software como um Superutilizador utilizando scripts de bash Olá abaixo:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Se cole este script janela vim, certifique-se tooremove avanço de Olá retorno ('\r ") com Olá os seguintes comandos:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>Passo 3: Editar perfil/etc.
Acrescente seguinte Olá no fim de Olá:

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>Passo 4: Instalar JNA para sistemas de produção
Sequência de comandos seguinte Olá de utilização: seguinte Olá comando instalação jna-3.2.7.jar e jna-plataforma-3.2.7.jar too/usr/share.java diretório sudo apt-get instalará libjna java

Crie ligações simbólicas no diretório CASS_HOME/lib $ para que o script de arranque Cassandra pode encontrar estas v7:

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Passo 5: Configurar cassandra.yaml
Edite cassandra.yaml na configuração de tooreflect cada VM necessária para todas as máquinas de virtuais Olá [podemos irá otimizar este durante o aprovisionamento de Olá real]:

<table>
<tr><th>Nome do campo   </th><th> Valor  </th><th>    Observações </th></tr>
<tr><td>cluster_name </td><td>    "CustomerService"    </td><td> Utilize o nome Olá que reflete a implementação</td></tr>
<tr><td>listen_address    </td><td>[pode deixar em branco]    </td><td> Eliminar "localhost" </td></tr>
<tr><td>rpc_addres   </td><td>[pode deixar em branco]    </td><td> Eliminar "localhost" </td></tr>
<tr><td>Seeds    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>Lista de todos os endereços IP Olá que são designados como seeds.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> Isto é utilizado por Olá NetworkTopologyStrateg para o Centro de dados de Olá ao inferir e bastidor de Olá de Olá VM</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>Passo 6: Capturar a imagem de VM Olá
Iniciar sessão na máquina virtual de Olá utilizando Olá hostname (hk-ACs-template.cloudapp.net) e a chave do SSH de Olá privada que criou anteriormente. Veja como tooUse a SSH com o Linux no Azure para obter detalhes sobre como toolog utilizando Olá comando ssh ou putty.exe.

Execute Olá sequência da imagem de Olá toocapture de ações a seguir:

##### <a name="1-deprovision"></a>1. Desaprovisionamento
Utilize o comando de Olá "sudo waagent – deprovision + utilizador" tooremove informações específicas de instância de Máquina Virtual. Consulte para [como tooCapture uma Máquina Virtual Linux](capture-image.md) tooUse como um modelo em mais detalhe no processo de captura de imagem de Olá.

##### <a name="2-shutdown-hello-vm"></a>2: Olá encerramento VM
Certifique-se de que a máquina virtual Olá é realçada e clique em ligação de encerramento Olá da barra de comando Olá inferior.

##### <a name="3-capture-hello-image"></a>3: imagem de Olá de captura
Certifique-se de que a máquina virtual Olá é realçada e clique em ligação de captura Olá da barra de comando Olá inferior. No seguinte ecrã de Olá, atribua um nome de imagem (por exemplo, hk-cas-2-08-ub-14-04-2014071), adequado a descrição da imagem e clique em processo de captura de Olá marca toofinish Olá "verificar".

Esta ação irá demorar alguns segundos e imagem Olá deve estar disponível na secção das minhas imagens da Galeria de imagem de Olá. Olá de VM de origem será eliminado automaticamente após a imagem de Olá é capturada com êxito. 

## <a name="single-region-deployment-process"></a>Processo de implementação única região
**Passo 1: Criar rede Virtual de Olá** sessão Olá portal do Azure e criar uma rede virtual (clássica) com atributos de Olá mostrada na Olá a tabela seguinte. Consulte [criar uma rede virtual (clássica) com o portal do Azure de Olá](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) para obter passos detalhados do processo de Olá.      

<table>
<tr><th>Nome de atributo VM</th><th>Valor</th><th>Observações</th></tr>
<tr><td>Nome</td><td>vnet-cass--EUA oeste</td><td></td></tr>
<tr><td>Região</td><td>EUA Oeste</td><td></td></tr>
<tr><td>Servidores DNS</td><td>Nenhuma</td><td>Ignore esta indicação como podemos não estiver a utilizar um servidor DNS</td></tr>
<tr><td>Espaço de endereços</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>IP inicial</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Adicione Olá seguintes sub-redes:

<table>
<tr><th>Nome</th><th>IP inicial</th><th>CIDR</th><th>Observações</th></tr>
<tr><td>Web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Sub-rede para a web farm do Olá</td></tr>
<tr><td>dados</td><td>10.1.2.0</td><td>/24 (251)</td><td>Sub-rede para nós de base de dados de Olá</td></tr>
</table>

Dados e sub-redes Web podem ser protegidas através de grupos de segurança de rede cobertura de Olá que está fora do âmbito deste artigo.  

**Passo 2: Aprovisionar máquinas** utilizando a imagem de Olá criada anteriormente, iremos criar Olá seguintes máquinas virtuais na nuvem de Olá server "hk-c-svc-Oeste" e vinculá-los toohello respetivas sub-redes conforme mostrado abaixo:

<table>
<tr><th>Nome do computador    </th><th>Subrede    </th><th>Endereço IP    </th><th>Conjunto de disponibilidade</th><th>DC/Rack</th><th>Seed?</th></tr>
<tr><td>HK-c1--EUA oeste    </td><td>dados    </td><td>10.1.2.4    </td><td>HK-c-aset-1    </td><td>DC = WESTUS bastidor = rack1 </td><td>Sim</td></tr>
<tr><td>HK-c2--EUA oeste    </td><td>dados    </td><td>10.1.2.5    </td><td>HK-c-aset-1    </td><td>DC = WESTUS bastidor = rack1    </td><td>Não </td></tr>
<tr><td>HK-c3--EUA oeste    </td><td>dados    </td><td>10.1.2.6    </td><td>HK-c-aset-1    </td><td>DC = WESTUS bastidor = rack2    </td><td>Sim</td></tr>
<tr><td>HK-c4--EUA oeste    </td><td>dados    </td><td>10.1.2.7    </td><td>HK-c-aset-1    </td><td>DC = WESTUS bastidor = rack2    </td><td>Não </td></tr>
<tr><td>HK-c5--EUA oeste    </td><td>dados    </td><td>10.1.2.8    </td><td>HK-c-aset-2    </td><td>DC = WESTUS bastidor = rack3    </td><td>Sim</td></tr>
<tr><td>HK-c6--EUA oeste    </td><td>dados    </td><td>10.1.2.9    </td><td>HK-c-aset-2    </td><td>DC = WESTUS bastidor = rack3    </td><td>Não </td></tr>
<tr><td>HK-c7--EUA oeste    </td><td>dados    </td><td>10.1.2.10    </td><td>HK-c-aset-2    </td><td>DC = WESTUS bastidor = rack4    </td><td>Sim</td></tr>
<tr><td>HK-c8--EUA oeste    </td><td>dados    </td><td>10.1.2.11    </td><td>HK-c-aset-2    </td><td>DC = WESTUS bastidor = rack4    </td><td>Não </td></tr>
<tr><td>HK-w1--EUA oeste    </td><td>Web    </td><td>10.1.1.4    </td><td>HK-w-aset-1    </td><td>                       </td><td>N/D</td></tr>
<tr><td>HK-w2--EUA oeste    </td><td>Web    </td><td>10.1.1.5    </td><td>HK-w-aset-1    </td><td>                       </td><td>N/D</td></tr>
</table>

A criação de Olá acima lista de VMs requer Olá seguinte processo:

1. Criar um serviço em nuvem vazio numa região específica
2. Criar uma VM a partir da imagem capturada anteriormente Olá e anexe-toohello de rede virtual criada anteriormente; Repita esta para todas as VMs de Olá
3. Adicionar um serviço de nuvem de toohello de Balanceador de carga interno e anexe-sub-rede toohello "dados"
4. Para cada VM criada anteriormente, adicione um ponto de final com balanceamento de carga para tráfego de thrift através de um balanceador de carga interno com balanceamento de carga conjunto ligado toohello criado anteriormente

Olá acima processo pode ser executado através do portal clássico do Azure; utilizar uma máquina de Windows (utilize uma VM no Azure se não tiver máquina de Windows acesso tooa), utilize Olá seguir tooprovision de script do PowerShell todos os 8 VMs automaticamente.

**Lista 1: Script do PowerShell para o aprovisionamento de máquinas virtuais**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**Passo 3: Configurar Cassandra em cada VM**

Inicie sessão no Olá VM e efetuar Olá seguinte:

* Edite $CASS_HOME/conf/cassandra-rackdc.properties toospecify Olá Centro e bastidor propriedades de dados:
  
       dc =EASTUS, rack =rack1
* Edite nós de seed tooconfigure cassandra.yaml como abaixo:
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**Passo 4: Iniciar Olá VMs e testar cluster Olá**

Registo num de nós de Olá (por exemplo, hk-c1--EUA oeste) e estado do comando toosee Olá do cluster de Olá Olá executar os seguintes:

       nodetool –h 10.1.2.4 –p 7199 status

Deverá ver Olá apresentar semelhante toohello um abaixo para um cluster do nó de 8:

<table>
<tr><th>Estado</th><th>Endereço    </th><th>Carregar    </th><th>Tokens    </th><th>É proprietário </th><th>ID de anfitrião    </th><th>Bastidor</th></tr>
<tr><th>ANULAR    </td><td>10.1.2.4     </td><td>87.81 KB    </td><td>256    </td><td>38.0%    </td><td>GUID (removido)</td><td>rack1</td></tr>
<tr><th>ANULAR    </td><td>10.1.2.5     </td><td>41.08 KB    </td><td>256    </td><td>68.9%    </td><td>GUID (removido)</td><td>rack1</td></tr>
<tr><th>ANULAR    </td><td>10.1.2.6     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (removido)</td><td>rack2</td></tr>
<tr><th>ANULAR    </td><td>10.1.2.7     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (removido)</td><td>rack2</td></tr>
<tr><th>ANULAR    </td><td>10.1.2.8     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (removido)</td><td>rack3</td></tr>
<tr><th>ANULAR    </td><td>10.1.2.9     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (removido)</td><td>rack3</td></tr>
<tr><th>ANULAR    </td><td>10.1.2.10     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (removido)</td><td>rack4</td></tr>
<tr><th>ANULAR    </td><td>10.1.2.11     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (removido)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Olá de teste único Cluster de região
Utilize Olá cluster de Olá tootest de passos a seguir:

1. Utilizar Olá Powershell comando Get-AzureInternalLoadbalancer commandlet, obter o endereço IP de Olá Olá interno de Balanceador de carga (por exemplo  10.1.2.101). sintaxe de Olá do comando de Olá é mostrado abaixo: Get-AzureLoadbalancer – ServiceName "hk-c-svc--EUA Oeste" [apresenta detalhes de Olá de Balanceador de carga interno Olá, juntamente com o respetivo endereço IP]
2. Iniciar sessão no farm de web de Olá VM (por exemplo, hk-w1--EUA oeste) a utilizar o Putty ou ssh
3. Executar $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. Utilize Olá seguir CQL comandos tooverify se cluster Olá está a funcionar:
   
     Criar KEYSPACE customers_ks com replicação = {'class': 'SimpleStrategy', 'replication_factor': 3};   UTILIZAR customers_ks;   Criar tabela Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   Inserir em Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   Inserir em Customers(customer_id, firstname, lastname) os valores (2, 'Joana', 'Silva');
   
     SELECIONAR * de clientes;

Deverá ver uma apresentação como Olá um abaixo:

<table>
  <tr><th> customer_id </th><th> nome próprio </th><th> Apelido </th></tr>
  <tr><td> 1 </td><td> João </td><td> Silva </td></tr>
  <tr><td> 2 </td><td> Joana </td><td> Silva </td></tr>
</table>

Tenha em atenção que keyspace Olá criado no passo 4 utiliza SimpleStrategy com um replication_factor de 3. SimpleStrategy é recomendada para os dados únicos center implementações enquanto NetworkTopologyStrategy para dados multi center implementações. Um replication_factor de 3 proporcionará tolerância a falhas de nó.

## <a id="tworegion"></a>Processo de implementação de Multirregião
Irá tirar partido das foi concluída a implementação única região Olá e repita Olá mesmo processo para instalar a região segundo Olá. diferença de chave de Olá entre Olá único e implementação de vários região é a configuração de túnel VPN Olá para comunicação entre região; Iremos começar com a instalação de rede Olá, aprovisionar Olá VMs e configurar Cassandra.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>Passo 1: Criar rede Virtual de Olá Olá 2nd região
Inicie sessão no portal clássico do Azure de Olá e crie uma rede Virtual com Olá atributos Mostrar na tabela de Olá. Consulte [configurar uma rede Virtual Cloud-Only no portal clássico do Azure de Olá](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) para obter passos detalhados do processo de Olá.      

<table>
<tr><th>Nome do atributo    </th><th>Valor    </th><th>Observações</th></tr>
<tr><td>Nome    </td><td>vnet-cass-Leste-nos</td><td></td></tr>
<tr><td>Região    </td><td>EUA Leste</td><td></td></tr>
<tr><td>Servidores DNS        </td><td></td><td>Ignore esta indicação como podemos não estiver a utilizar um servidor DNS</td></tr>
<tr><td>Configurar uma VPN ponto a site</td><td></td><td>        Ignore esta indicação</td></tr>
<tr><td>Configurar uma rede de VPN</td><td></td><td>        Ignore esta indicação</td></tr>
<tr><td>Espaço de endereços    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>IP inicial    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Adicione Olá seguintes sub-redes:

<table>
<tr><th>Nome    </th><th>IP inicial    </th><th>CIDR    </th><th>Observações</th></tr>
<tr><td>Web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Sub-rede para a web farm do Olá</td></tr>
<tr><td>dados    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Sub-rede para nós de base de dados de Olá</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>Passo 2: Criar redes locais
Uma rede Local na rede virtual do Azure é um espaço de endereços de proxy que mapeie tooa site remoto, incluindo uma nuvem privada ou outra região do Azure. Este espaço de endereços de proxy é vinculado tooa gateway remoto para o encaminhamento de rede de toohello destinos de rede à direita. Consulte [configurar uma ligação de tooVNet VNet](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) para Olá obter instruções sobre como estabelecer a ligação VNET a VNET.

Crie duas redes locais por Olá os detalhes:

| Nome da rede | Endereço de Gateway VPN | Espaço de endereços | Observações |
| --- | --- | --- | --- |
| HK-lnet-Map-to-East-US |23.1.1.1 |10.2.0.0/16 |Ao criar Olá rede Local dar um marcador de posição endereço de gateway. endereço de real gateway Olá é preenchido quando for criado o gateway de Olá. Certifique-se de espaço de endereços de Olá corresponde exatamente ao hello respetiva VNET remota; Neste caso, hello VNET criada no Olá região EUA Leste. |
| HK-lnet-Map-to-West-US |23.2.2.2 |10.1.0.0/16 |Ao criar Olá rede Local dar um marcador de posição endereço de gateway. endereço de real gateway Olá é preenchido quando for criado o gateway de Olá. Certifique-se de espaço de endereços de Olá corresponde exatamente ao hello respetiva VNET remota; Neste caso, hello VNET criada no Olá região EUA oeste. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>Passo 3: Mapa "Local" rede toohello respetivas VNETs
De Olá portal clássico do Azure, selecione cada vnet, clique em "Configurar", consulte "Ligar toohello rede local" e selecione Olá redes locais por Olá os detalhes:

| Rede Virtual | Rede local |
| --- | --- |
| HK-vnet--EUA oeste |HK-lnet-Map-to-East-US |
| HK-vnet-Leste-nos |HK-lnet-Map-to-West-US |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>Passo 4: Criar Gateways no VNET1 e VNET2
A partir do dashboard de Olá de ambas as redes virtuais Olá, clique em criar GATEWAY que activarão o gateway de VPN de Olá processo de aprovisionamento. Após alguns minutos Olá dashboard de cada rede virtual deve apresentar o endereço de gateway real Olá.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Passo 5: Redes de "Local" de atualização com endereços de respetivos "Gateway" Olá
Edite os dois Olá redes locais tooreplace Olá marcador de posição gateway IP endereço com o endereço IP real Olá de Olá apenas aprovisionado gateways. Utilize Olá mapeamento os seguintes:

<table>
<tr><th>Rede local    </th><th>Gateway de Rede Virtual</th></tr>
<tr><td>HK-lnet-Map-to-East-US </td><td>Gateway de hk-vnet--EUA oeste</td></tr>
<tr><td>HK-lnet-Map-to-West-US </td><td>Gateway de hk-vnet-Leste-nos</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>Passo 6: Atualizar a chave partilhada Olá
Olá utilize a seguinte chave de IPSec do Powershell script tooupdate Olá de cada gateway VPN [Utilize Olá sake chave para ambas as gateways Olá]: hk-lnet-map-to-west-us de - LocalNetworkSiteName do conjunto AzureVNetGatewayKey - VNetName hk-vnet-Leste-nos - SharedKey D9E76BKK Conjunto AzureVNetGatewayKey - VNetName hk-vnet--EUA oeste - LocalNetworkSiteName hk-lnet-map-to-east-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>Passo 7: Estabelecer a ligação de Olá VNET a VNET
A partir de Olá portal clássico do Azure, utilize o menu de "DASHBOARD" Olá da ligação de gateway a gateway ambas Olá redes virtuais tooestablish. Utilize itens de menu "Ligar" Olá na barra de ferramentas do Olá inferior. Após alguns minutos dashboard Olá deve apresentar detalhes de ligação de Olá graficamente.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>Passo 8: Criar máquinas virtuais Olá na região #2
Criar imagem de Ubuntu Olá, conforme descrito na implementação de região #1 pelo seguinte Olá mesmos passos ou copie Olá imagem VHD ficheiro toohello conta de armazenamento Azure localizada numa região #2 e criar Olá imagem. Utilizar esta imagem e crie Olá seguinte lista de máquinas virtuais para um novo serviço em nuvem hk-c-svc-leste--na:

| Nome do computador | Subrede | Endereço IP | Conjunto de disponibilidade | DC/Rack | Seed? |
| --- | --- | --- | --- | --- | --- |
| HK-c1-Leste-nos |dados |10.2.2.4 |HK-c-aset-1 |DC = EASTUS bastidor = rack1 |Sim |
| HK-c2-Leste-nos |dados |10.2.2.5 |HK-c-aset-1 |DC = EASTUS bastidor = rack1 |Não |
| HK-c3-Leste-nos |dados |10.2.2.6 |HK-c-aset-1 |DC = EASTUS bastidor = rack2 |Sim |
| HK-c5-Leste-nos |dados |10.2.2.8 |HK-c-aset-2 |DC = EASTUS bastidor = rack3 |Sim |
| HK-c6-Leste-nos |dados |10.2.2.9 |HK-c-aset-2 |DC = EASTUS bastidor = rack3 |Não |
| HK-c7-Leste-nos |dados |10.2.2.10 |HK-c-aset-2 |DC = EASTUS bastidor = rack4 |Sim |
| HK-c8-Leste-nos |dados |10.2.2.11 |HK-c-aset-2 |DC = EASTUS bastidor = rack4 |Não |
| HK-w1-Leste-nos |Web |10.2.1.4 |HK-w-aset-1 |N/D |N/D |
| HK-w2-Leste-nos |Web |10.2.1.5 |HK-w-aset-1 |N/D |N/D |

Siga Olá mesmo instruções como região #1, mas utilizam o espaço de endereços 10.2.xxx.xxx.

### <a name="step-9-configure-cassandra-on-each-vm"></a>Passo 9: Configurar Cassandra em cada VM
Inicie sessão no Olá VM e efetuar Olá seguinte:

1. Editar $CASS_HOME/conf/cassandra-rackdc.properties toospecify Olá dados Centro e bastidor propriedades no formato de Olá: dc = EASTUS bastidor = rack1
2. Editar cassandra.yaml tooconfigure seed nós: Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10"

### <a name="step-10-start-cassandra"></a>Passo 10: Iniciar Cassandra
Inicie sessão em cada VM e inicie Cassandra em segundo plano de Olá executando Olá os seguintes comandos: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>Olá teste Multirregião Cluster
Por agora Cassandra foi implementado too16 nós com 8 nós em cada região do Azure. Estes nós estão no mesmo cluster em virtude de nome de cluster comum Olá e a configuração de nó de seed Olá de Olá. Utilize Olá cluster do processo tootest Olá os seguintes:

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>Passo 1: Obter o IP de Balanceador de carga interno Olá para ambas as regiões de Olá através do PowerShell
* Get-AzureInternalLoadbalancer - ServiceName "hk-c-svc--EUA Oeste"
* Get-AzureInternalLoadbalancer - ServiceName "hk-c-svc-Leste-us"  
  
    Tenha em atenção endereços IP Olá (por exemplo, oeste - 10.1.2.101 Leste - 10.2.2.101) apresentado.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>Passo 2: Executar seguinte Olá na região de oeste Olá depois de iniciar sessão em hk-w1--EUA oeste
1. Executar $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. Execute os seguintes comandos CQL de Olá:
   
     Criar KEYSPACE customers_ks com replicação = {'class': 'NetworkToplogyStrategy', 'WESTUS': 3, 'EASTUS': 3};   UTILIZAR customers_ks;   Criar tabela Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   Inserir em Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   Inserir em Customers(customer_id, firstname, lastname) os valores (2, 'Joana', 'Silva');   SELECIONAR * de clientes;

Deverá ver uma apresentação como Olá um abaixo:

| customer_id | nome próprio | Apelido |
| --- | --- | --- |
| 1 |João |Silva |
| 2 |Joana |Silva |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>Passo 3: Execute o seguinte Olá na região de Leste Olá depois de iniciar sessão em hk-w1-leste--na:
1. Executar $CASS_HOME/bin/cqlsh 10.2.2.101 9160
2. Execute os seguintes comandos CQL de Olá:
   
     UTILIZAR customers_ks;   Criar tabela Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   Inserir em Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   Inserir em Customers(customer_id, firstname, lastname) os valores (2, 'Joana', 'Silva');   SELECIONAR * de clientes;

Deverá ver Olá mesmo apresentar visto região de oeste Olá:

| customer_id | nome próprio | Apelido |
| --- | --- | --- |
| 1 |João |Silva |
| 2 |Joana |Silva |

Executar alguns inserções mais e ver que os obter toowest replicada-na parte do cluster de Olá.

## <a name="test-cassandra-cluster-from-nodejs"></a>Cluster de Cassandra de teste do Node.js
Utilizar uma das VMs do Linux Olá criado anteriormente na camada de "web" Olá, iremos irá executar um simples Node.js script tooread Olá anteriormente inserida de dados

**Passo 1: Instalar o Node.js e Cassandra cliente**

1. Instalar Node.js e npm
2. Instalar o pacote "cassandra-cliente de nó" utilizando npm
3. Execute o seguinte script na linha de comandos do shell Olá que apresenta a cadeia de json Olá de Olá obtida dados de Olá:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Conclusão
Microsoft Azure é uma plataforma flexível que permite a execução de Olá de ambos Microsoft, bem como o software open source para como é demonstrado neste exercício. Clusters de Cassandra elevadas podem ser implementados no Centro de dados único através de Olá propagando-se Olá nós de cluster em vários domínios de falhas. Cassandra clusters também podem ser implementados em várias regiões do Azure, geograficamente distantes para sistemas de prova de desastre. Azure e permite em conjunto Cassandra Olá construção de altamente dimensionável e altamente disponíveis e serviços de cloud possível recuperar de desastres necessitam através da internet de hoje aumentar.  

## <a name="references"></a>Referências
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

