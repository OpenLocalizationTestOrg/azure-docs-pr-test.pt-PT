---
title: "aaaAzure armazenamento desempenho e escalabilidade lista de verificação | Microsoft Docs"
description: "Uma lista de verificação das práticas comprovadas para utilização com o Storage do Azure no desenvolvimento performant aplicações."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c0cd77da4a1abda42c018255ed93215b71f4fad8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Lista de Verificação de Desempenho e Escalabilidade do Armazenamento do Microsoft Azure
## <a name="overview"></a>Descrição geral
Desde a versão de Olá dos serviços de armazenamento do Microsoft Azure Olá, Microsoft desenvolveu várias comprovadas práticas para utilizar estes serviços de forma performant e este artigo serve tooconsolidate Olá mais importantes-las numa lista lista de verificação estilo. intenção Olá deste artigo é que os programadores de aplicações toohelp Certifique-se de que estão a utilizar práticas comprovadas com o Storage do Azure e toohelp-los identificam outras práticas comprovadas deve considerar a adoção de. Este artigo não tenta toocover cada possíveis otimização de desempenho e escalabilidade — exclui os que são pequenos no respetivo impacto nas ou não é amplamente aplicável. a extensão toohello que Olá comportamento da aplicação possível prever durante a conceção, é útil tookeep no atenção numa fase inicial no tooavoid estruturas que serão depare com problemas de desempenho.  

Cada programador de aplicações utilizando o armazenamento do Azure deve demorar Olá tempo tooread neste artigo e verifique se a aplicação segue cada Olá comprovada práticas listadas abaixo.  

## <a name="checklist"></a>Lista de verificação
Este artigo organiza práticas Olá comprovada numa Olá seguintes grupos. Práticas comprovadas aplicadas-se a:  

* Todos os serviços de armazenamento do Azure (blobs, tabelas, filas e ficheiros)
* Blobs
* Tabelas
* Filas  

| Concluído | Área | Categoria | Pergunta |
| --- | --- | --- | --- |
| &nbsp; | Todos os Serviços |Objetivos de escalabilidade |[É a aplicação concebida tooavoid a aproximar-se os objetivos de escalabilidade Olá?](#subheading1) |
| &nbsp; | Todos os Serviços |Objetivos de escalabilidade |[É o tooenable Convenção concebida nomenclatura melhor balanceamento de carga?](#subheading47) |
| &nbsp; | Todos os Serviços |Redes |[Dispositivos de lado cliente dispõem de largura de banda alta suficientemente e desempenho Olá tooachieve de latência baixa necessários?](#subheading2) |
| &nbsp; | Todos os Serviços |Redes |[Dispositivos de lado cliente dispõem de uma ligação de qualidade suficientemente elevada?](#subheading3) |
| &nbsp; | Todos os Serviços |Redes |[Aplicação de cliente Olá está localizada "perto de" conta de armazenamento Olá?](#subheading4) |
| &nbsp; | Todos os Serviços |Distribuição de Conteúdos |[Está a utilizar uma CDN para distribuição de conteúdos?](#subheading5) |
| &nbsp; | Todos os Serviços |Acesso de cliente direto |[Está a utilizar SAS e o CORS toostorage de acesso direto tooallow em vez do proxy?](#subheading6) |
| &nbsp; | Todos os Serviços |Colocação em cache |[Raramente é a colocação em cache dados da aplicação que são utilizados repetidamente e as alterações?](#subheading7) |
| &nbsp; | Todos os Serviços |Colocação em cache |[É a aplicação de criação de batches atualizações (a colocação em cache-os do lado do cliente e, em seguida, carregar conjuntos de maior)?](#subheading8) |
| &nbsp; | Todos os Serviços |Configuração do .NET |[Tiver configurado a um número suficiente de ligações simultâneas de toouse do cliente?](#subheading9) |
| &nbsp; | Todos os Serviços |Configuração do .NET |[Tiver configurado .NET toouse um número suficiente de threads?](#subheading10) |
| &nbsp; | Todos os Serviços |Configuração do .NET |[Está a utilizar o .NET 4.5 ou posterior, que foi melhorado recolha de lixo?](#subheading11) |
| &nbsp; | Todos os Serviços |Paralelismo |[Pode certificar-se de que paralelismo é tem um vínculo adequadamente para que não a sobrecarga as capacidades de cliente ou destinos de escalabilidade Olá?](#subheading12) |
| &nbsp; | Todos os Serviços |Ferramentas |[É estiver a utilizar a versão mais recente do Olá do Microsoft fornecidas bibliotecas de cliente e ferramentas?](#subheading13) |
| &nbsp; | Todos os Serviços |Tentativas |[Estão a utilizar um término exponencial repetir a política de limitação de erros e tempos limite?](#subheading14) |
| &nbsp; | Todos os Serviços |Tentativas |[As tentativas de evitando aplicação destina-se a erros de não repetição?](#subheading15) |
| &nbsp; | Blobs |Objetivos de escalabilidade |[Tem um grande número de clientes aceder em simultâneo num único objeto?](#subheading46) |
| &nbsp; | Blobs |Objetivos de escalabilidade |[A aplicação é permanecendo no destino de escalabilidade de largura de banda ou operações Olá para um blob único?](#subheading16) |
| &nbsp; | Blobs |Copiar os Blobs |[Está a copiar os blobs de forma eficiente?](#subheading17) |
| &nbsp; | Blobs |Copiar os Blobs |[São utilizando o AzCopy para cópias em massa de blobs?](#subheading18) |
| &nbsp; | Blobs |Copiar os Blobs |[Está a utilizar o Azure para importar/exportar tootransfer muito grandes volumes de dados?](#subheading19) |
| &nbsp; | Blobs |Utilizar metadados |[São armazenar metadados utilizados frequentemente sobre blobs nos respetivos metadados?](#subheading20) |
| &nbsp; | Blobs |Carregar rápida |[Quando tenta um blob tooupload rapidamente, é-carregar blocos em paralelo?](#subheading21) |
| &nbsp; | Blobs |Carregar rápida |[Quando tenta tooupload blobs muitos rapidamente, é-carregar blobs em paralelo?](#subheading22) |
| &nbsp; | Blobs |Tipo de Blob correto |[Está a utilizar blobs de páginas ou blobs de blocos quando for adequado?](#subheading23) |
| &nbsp; | Tabelas |Objetivos de escalabilidade |[São, aproximado Olá os objetivos de escalabilidade para as entidades por segundo?](#subheading24) |
| &nbsp; | Tabelas |Configuração |[Está a utilizar JSON para os pedidos de tabela?](#subheading25) |
| &nbsp; | Tabelas |Configuração |[Ter tenha desativado Nagle desempenho de Olá tooimprove de pedidos pequenos?](#subheading26) |
| &nbsp; | Tabelas |As tabelas e partições |[Ter corretamente particionada os dados?](#subheading27) |
| &nbsp; | Tabelas |Partições frequente |[São evitando padrões só de acréscimo e só de preceder?](#subheading28) |
| &nbsp; | Tabelas |Partições frequente |[As inserções/atualizações são distribuídas por várias partições?](#subheading29) |
| &nbsp; | Tabelas |Âmbito de consulta |[Concebido tooallow o esquema para o ponto de consultas toobe utilizado na maioria dos casos e toobe de consultas de tabela utilizadas com moderação?](#subheading30) |
| &nbsp; | Tabelas |Densidade de consulta |[Efetue a análise de normalmente apenas consultas e devolvem linhas que irá utilizar a sua aplicação?](#subheading31) |
| &nbsp; | Tabelas |Dados devolvidos restritiva |[Está a utilizar filtragem tooavoid devolvidos as entidades que não são necessários?](#subheading32) |
| &nbsp; | Tabelas |Dados devolvidos restritiva |[Está a utilizar tooavoid projecção devolver propriedades que não são necessários?](#subheading33) |
| &nbsp; | Tabelas |Denormalization |[Ter desnormalizadas os dados que evitar consultas ineficazes ou vários pedidos de leitura quando tenta tooget dados?](#subheading34) |
| &nbsp; | Tabelas |Inserir/atualizar/eliminar |[Está a criação de batches de pedidos que precisam de toobe transacional ou podem ser feitos na Olá mesmo tempo de ida e volta de tooreduce?](#subheading35) |
| &nbsp; | Tabelas |Inserir/atualizar/eliminar |[É, evitando obter toodetermine de apenas uma entidade se toocall inserir ou atualizar?](#subheading36) |
| &nbsp; | Tabelas |Inserir/atualizar/eliminar |[Ter considerados armazenar série de dados que frequentemente serão obtidos em conjunto uma única entidade como propriedades em vez de várias entidades?](#subheading37) |
| &nbsp; | Tabelas |Inserir/atualizar/eliminar |[Para entidades que sempre serão obtidas em conjunto e podem ser escritas em lotes (por exemplo, dados de séries de tempo), ter é considerado utilizar blobs em vez de tabelas?](#subheading38) |
| &nbsp; | Filas |Objetivos de escalabilidade |[São, aproximado Olá os objetivos de escalabilidade para mensagens por segundo?](#subheading39) |
| &nbsp; | Filas |Configuração |[Ter tenha desativado Nagle desempenho de Olá tooimprove de pedidos pequenos?](#subheading40) |
| &nbsp; | Filas |Tamanho da Mensagem |[São as mensagens compact tooimprove Olá desempenho da fila de Olá?](#subheading41) |
| &nbsp; | Filas |Obter em massa |[A obter várias mensagens numa única operação "Get"?](#subheading42) |
| &nbsp; | Filas |Frequência de consulta |[A consulta com frequência suficiente Olá tooreduce percetível latência da sua aplicação?](#subheading43) |
| &nbsp; | Filas |Mensagem de actualização |[Está a utilizar UpdateMessage toostore progresso no processamento de mensagens, evitando terem mensagem completa de saudação tooreprocess se ocorrer um erro?](#subheading44) |
| &nbsp; | Filas |Arquitetura |[Está a utilizar filas toomake a aplicação toda escalável mais mantendo cargas de trabalho de longa execução fora do caminho críticos Olá e escala, em seguida, independentemente?](#subheading45) |

## <a name="allservices"></a>Todos os serviços
Esta secção lista comprovadas práticas que são aplicáveis toohello utilização de qualquer um dos serviços de armazenamento do Azure Olá (blobs, tabelas, filas ou ficheiros).  

### <a name="subheading1"></a>Objetivos de escalabilidade
Cada um dos serviços de armazenamento do Azure Olá tem destinos de escalabilidade da capacidade (GB), a taxa de transacção e a largura de banda. Se a sua aplicação atinja ou exceda qualquer um dos objetivos de escalabilidade Olá, poderá encontrar transação maiores latências ou limitação. Quando um serviço de armazenamento acelera a sua aplicação, o serviço de Olá começa tooreturn "503 servidor ocupado" ou "500 tempo limite da operação" códigos de erro para algumas transações de armazenamento. Esta secção descreve os dois toodealing de abordagem geral Olá com os objetivos de escalabilidade e objetivos de escalabilidade da largura de banda em particular. As secções que lidam com os serviços de armazenamento individuais abordam objetivos de escalabilidade no contexto de Olá desse serviço específico:  

* [Largura de banda de blob e pedidos por segundo](#subheading16)
* [Entidades da tabela por segundo](#subheading24)
* [Mensagens de fila por segundo](#subheading39)  

#### <a name="sub1bandwidth"></a>Destino de escalabilidade da largura de banda para todos os serviços
Momento Olá de escrita, destinos de largura de banda de Olá na conta de Olá E.U.A. para um armazenamento georredundante (GRS) são 10 gigabits por segundo (Gbps) de entrada (dados enviados toohello conta de armazenamento) e 20 Gbps de saída (dados enviados a partir da conta de armazenamento Olá). Para uma conta de armazenamento localmente redundante (LRS), os limites de Olá são superiores – 20 Gbps de entrada e de 30 Gbps de saída.  Limites de largura de banda internacional pode ser mais baixas e pode ser encontrados no nosso [página de destinos de escalabilidade](http://msdn.microsoft.com/library/azure/dn249410.aspx).  Para obter mais informações sobre as opções de redundância do armazenamento Olá, consulte as ligações de Olá em [recursos úteis](#sub1useful) abaixo.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>Que toodo quando atingir um destino de escalabilidade
Se a aplicação estiver a atingir os objetivos de escalabilidade Olá para uma única conta de armazenamento, considere a adoção de uma das seguintes abordagens de Olá:  

* Reconsider Olá a carga de trabalho faz com que a aplicação tooapproach ou exceder o destino de escalabilidade Olá. Pode estruturar-diferente toouse menos largura de banda ou capacidade ou menos transações?
* Se uma aplicação pode exceder um dos objetivos de escalabilidade Olá, deve criar várias contas de armazenamento e partição os dados da aplicação entre essas várias contas de armazenamento. Se utilizar este padrão, em seguida, ser toodesign se a aplicação para que possa adicionar mais contas de armazenamento no Olá futura para balanceamento de carga. No momento da escrita, cada subscrição do Azure pode ter segurança too100 contas de armazenamento.  As contas de armazenamento também tem sem qualquer custo que não seja a sua utilização em termos de dados armazenados, as transações efetuadas ou dados transferidos.
* Se a aplicação chega a destinos de largura de banda Olá, considere a compressão de dados no Olá cliente tooreduce Olá largura de banda necessária toosend Olá dados toohello serviço de armazenamento.  Tenha em atenção que isto pode poupar largura de banda e melhorar o desempenho de rede, pode também ter alguns impactos negativos.  Deve avaliar o impacto do desempenho Olá deste devido a requisitos de processamento adicional toohello para comprimir e descomprimir os dados no cliente Olá. Além disso, o armazenamento de dados comprimidos pode tornar mais difícil tootroubleshoot problemas, uma vez que poderia ser mais difícil tooview armazenado dados através de ferramentas padrão.
* Se a sua aplicação pedidos com êxito os objetivos de escalabilidade Olá, em seguida, certifique-se de que está a utilizar um término exponencial para tentativas (consulte [tentativas](#subheading14)).  Apenas não manter repetir rapidamente, tornando Olá limitação worse de melhor toomake se de nunca abordar objetivos de escalabilidade Olá (utilizando um dos Olá acima métodos), mas isto irá garantir a sua aplicação.  

#### <a name="useful-resources"></a>Recursos Úteis
Olá seguintes ligações fornece detalhes adicionais sobre os objetivos de escalabilidade:

* Consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md) para obter informações sobre os objetivos de escalabilidade.
* Consulte [replicação de armazenamento do Azure](storage-redundancy.md) e mensagem de blogue Olá [as opções de redundância do armazenamento do Azure e de armazenamento redundantes do acesso de leitura Georreplicação](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) para obter informações sobre as opções de redundância do armazenamento.
* Para obter informações atualizadas sobre os preços para os serviços do Azure, consulte [preços do Azure](https://azure.microsoft.com/pricing/overview/).  

### <a name="subheading47"></a>Convenção de nomenclatura de partição
Armazenamento do Azure utiliza um baseada no intervalo partições esquema tooscale e carga saldo Olá sistema. chave de partição Olá é dados toopartition utilizado para intervalos e estes intervalos são com balanceamento de carga em sistema Olá. Isto significa que as convenções de nomenclatura como lexical ordenar (por exemplo, msftpayroll msftperformance, msftemployees, etc.) ou utilizando os carimbos tempo (log20160101 log20160102, log20160102, etc.) serão cada partições toohello potencialmente a ser localizadas conjuntamente num Olá mesmo partição servidor, enquanto uma operação de balanceamento de carga divide-los em intervalos menores. Por exemplo, todos os blobs num contentor podem ser servidos por um único servidor até hello carga nestes blobs requer mais reequilíbrio dos intervalos de partição Olá. Da mesma forma, um grupo de contas ligeiramente carregados com os respetivos nomes dispostas numa ordem lexical poderão ser servido por um único servidor até Olá carregar um ou todas estas contas requerem-los toobe divisão em vários servidores de partições. Cada operação de balanceamento de carga pode ter impacto na latência de Olá de chamadas de armazenamento durante a operação de Olá. toohandle de capacidade do sistema de Olá que uma rajada repentino da partição do tráfego tooa é limitada pela escalabilidade Olá de um servidor de partições únicas até a operação de balanceamento de carga Olá kicks-in e efetua novamente o intervalo de chave de partição de Olá balanceamento.  

Pode seguir algumas melhores práticas tooreduce Olá uma frequência de operações.  

* Examine a Convenção de nomenclatura Olá que utilizar para as contas, contentores, blobs, tabelas e filas, rigorosamente. Considere lhe o prefixo nomes de conta com um hash de 3 dígitos a utilizar uma função de hash que melhor se adapta às suas necessidades.  
* Se a organizar os seus dados através de carimbos ou identificadores numéricos, terá tooensure não estiver a utilizar um padrões de tráfego de só de acréscimo (ou apenas de preceder). Estes padrões não são adequados para um intervalo de-com base em sistema de criação de partições e foi oportunidades potenciais tooall Olá tráfego irá tooa única partição e o sistema de Olá restritiva de forma eficaz balanceamento de carga. Por exemplo, se tiver diariamente operações que utilizam um objeto de blob com um carimbo como AAAAMMDD, em seguida, todos os Olá tráfego para que a operação diária é direcionado tooa único objeto que é fornecido por um servidor de partições únicas. Observar se limita Olá por BLOBs e por partição limites satisfazer as suas necessidades e considere danificando a esta operação em blobs vários se for necessário. Da mesma forma, se armazenar dados de séries de tempo nas suas tabelas, todo o tráfego Olá pode ser direcionado toohello última parte do espaço de nomes de chave Olá. Se tiver de utilizar carimbos ou os IDs de numéricos, prefixo de id de Olá com um hash de 3 dígitos ou no caso de Olá de carimbos prefixo Olá segundos parte do tempo de Olá como ssyyyymmdd. Se a lista e consultar operações são efetuadas regularmente, escolha uma função de hash irá limitar o número de consultas. Noutros casos, um prefixo aleatório pode ser suficiente.  
* Para informações adicionais sobre Olá a criação de partições de esquema utilizado no armazenamento do Azure, leia o documento SOSP Olá [aqui](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf).

### <a name="networking"></a>Redes
Enquanto Olá API chama independentemente, muitas vezes, restrições de rede física Olá da aplicação Olá tem um impacto significativo no desempenho. seguinte Olá descreve algumas das limitações que os utilizadores podem encontrar.  

#### <a name="client-network-capability"></a>Capacidade de rede do cliente
##### <a name="subheading2"></a>Débito
Largura de banda, problema Olá é frequentemente Olá das capacidades do cliente de Olá. Por exemplo, enquanto uma única conta de armazenamento pode processar igual ou mais de entrada a 10 Gbps (consulte [metas de escalabilidade da largura de banda](#sub1bandwidth)), velocidade de rede Olá numa instância de função de trabalho do Azure "Pequeno" só é capaz de aproximadamente 100 Mbps. Maior instâncias do Azure têm NICs com maior capacidade, pelo que deve considerar a utilização de uma instância maior ou mais VM se precisar de limites de rede superiores de um único computador. Se está a aceder ao serviço de armazenamento de uma aplicação no local no, em seguida, hello mesma regra aplica-se: compreender as capacidades de rede de Olá de dispositivo de cliente Olá e toohello de conectividade de rede Olá localização de armazenamento do Azure e a melhorar-os conforme necessário ou conceber a sua toowork aplicação dentro as respetivas capacidades.  

##### <a name="subheading3"></a>Qualidade de ligação
À semelhança de qualquer utilização de rede, lembre-se de que condições de rede, resultando em perda de pacotes e erros mais lento débito Efetivo.  Utilizar o WireShark ou NetMon pode ajudar a diagnosticar o problema.  

##### <a name="useful-resources"></a>Recursos Úteis
Para mais informações sobre os tamanhos de máquina virtual e largura de banda alocada, consulte [tamanhos de Windows VM](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [tamanhos de VM com Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

#### <a name="subheading4"></a>Localização
Em qualquer ambiente distribuído, colocar o cliente de Olá quase toohello servidor fornece num melhor desempenho possível Olá. Para aceder ao armazenamento do Azure com uma latência mais baixa Olá, localização de melhor Olá para o cliente se encontra dentro Olá mesma região do Azure. Por exemplo, se tiver um Web Site do Azure que utiliza o armazenamento do Azure, deve localize-los ambos numa única região (por exemplo, EUA Oeste ou Sudeste asiático). Isto reduz a latência de Olá e Olá custos — momento Olá de escrita, a utilização de largura de banda numa única região é gratuita.  

Se o cliente aplicações não alojadas no Azure (tais como aplicações de dispositivos móveis ou nos serviços de empresa no local), em seguida, novamente a colocação de conta de armazenamento Olá numa região quase toohello dispositivos que irão aceder aos mesmos, será geralmente reduzir a latência. Se os clientes são distribuídos amplamente (por exemplo, alguns na América do Norte e algumas na Europa), em seguida, deve considerar a utilização de várias contas de armazenamento: uma localizado na região Norte American e um numa região Europa. Isto ajudará a latência de tooreduce para os utilizadores em ambas as regiões. Esta abordagem é normalmente mais fácil tooimplement se hello lojas de aplicações de Olá dados utilizadores tooindividual específica e não necessita de replicar dados entre contas de armazenamento.  Abrangente para distribuição de conteúdos, recomenda-se uma CDN – Consulte Olá a secção seguinte para obter mais detalhes.  

### <a name="subheading5"></a>Distribuição de conteúdo
Por vezes, um Olá tooserve do necessidades de aplicação mesmo conteúdo toomany utilizadores (por exemplo, um produto demonstração vídeo utilizado na Olá home page de um Web site), localizado no Olá iguais ou em várias regiões. Neste cenário, deve utilizar uma rede de entrega de conteúdos (CDN), tais como o CDN do Azure e Olá CDN utilizaria o armazenamento do Azure como origem de Olá dos dados de Olá. Ao contrário de uma conta de armazenamento do Azure que existe numa única região e que não é possível distribuir os conteúdos com baixa latência tooother regiões, a CDN do Azure utiliza servidores em vários centros de dados em torno Olá mundo. Além disso, uma CDN, normalmente, pode suportar limites de saída muito superiores de uma única conta de armazenamento.  

Para obter mais informações sobre a CDN do Azure, consulte [CDN do Azure](https://azure.microsoft.com/services/cdn/).  

### <a name="subheading6"></a>Utilizando a SAS e o CORS
Quando precisar de código tooauthorize como JavaScript no browser da web de um utilizador ou um dados tooaccess da aplicação móvel no armazenamento do Azure, uma abordagem é toouse uma aplicação na função da web como um proxy: dispositivo do utilizador Olá efetua a autenticação com a função da web Olá, na qual ativar autentica com o serviço de armazenamento Olá. Desta forma, pode evitar expor as chaves de conta de armazenamento em dispositivos inseguras. No entanto, isto coloca uma sobrecarga de macrocomputação em função da web Olá porque todos os dados de Olá transferidos entre o dispositivo do utilizador Olá e hello serviço de armazenamento tem de passar através de função da web Olá. Pode evitar utilizar uma função da web como um proxy Olá para serviço de armazenamento através de acesso partilhado assinaturas (SAS), por vezes, em conjunto com cabeçalhos de partilha de recursos de várias origens (CORS). Através da SAS, pode permitir que os pedidos de toomake de dispositivo do utilizador diretamente o serviço de armazenamento tooa através de um token de acesso limitado. Por exemplo, se um utilizador pretende tooupload uma aplicação de tooyour fotografias, a função da web pode gerar e enviar dispositivo do utilizador toohello um token SAS, que concede blob específico do permissão toowrite tooa ou contentor para Olá seguintes 30 minutos (após o qual hello SAS token expira).

Normalmente, um browser não irá permitir JavaScript numa página alojada por um Web site de um domínio tooperform operações específicas, tais como um domínio de tooanother "Colocar". Por exemplo, se alojar uma função da web "contosomarketing.cloudapp.net" e pretender toouse cliente lado JavaScript tooupload tooyour conta do blob storage em "contosoproducts.blob.core.windows.net", hello do browser "mesma política de origem" será forbid Isto operação. CORS é uma funcionalidade de browser que permite Olá destino domínio (por esta conta de armazenamento Olá maiúsculas) toocommunicate toohello browser que confia pedidos com origem no domínio de origem Olá (em função da web este Olá maiúsculas).  

Ambas estas tecnologias podem ajudar a evitar carga desnecessária (e congestionamentos) na sua aplicação web.  

#### <a name="useful-resources"></a>Recursos Úteis
Para obter mais informações sobre SAS, consulte [assinaturas de acesso partilhado, parte 1: Olá compreender o modelo SAS](storage-dotnet-shared-access-signature-part-1.md).  

Para obter mais informações sobre a CORS, consulte [suporte de partilha de recursos de várias origens (CORS) para Olá dos serviços de armazenamento do Azure](http://msdn.microsoft.com/library/azure/dn535601.aspx).  

### <a name="caching"></a>Colocação em cache
#### <a name="subheading7"></a>Obter dados
Em geral, a obtenção de dados de um serviço, uma vez é melhor do que recuperá-la em duas vezes. Considere o exemplo de Olá de uma aplicação de web MVC em execução numa função da web que já tenha a obter um blob de 50MB da Olá tooserve de serviço de armazenamento como utilizador tooa conteúdo. aplicação Olá foi, em seguida, obter esse mesmo blob sempre que um utilizador solicita- ou -foi cache-la localmente toodisk reutilização Olá em cache versão e pedidos de utilizador subsequentes. Além disso, sempre que um utilizador solicita dados Olá, Olá, aplicação foi problema obter com um cabeçalho condicional para o tempo de modificação, o que seria evitar a introdução ao blob todo Olá se este não foi modificada. Pode aplicar este mesmo tooworking de padrão com as entidades da tabela.  

Em alguns casos, pode decidir que a aplicação pode assumir que blob Olá permanece válida para um curto período de tempo após a obtenção e durante este período Olá aplicação têm de toocheck se blob Olá foi modificada.

Configuração, pesquisa e outros dados que são sempre utilizados pela aplicação Olá são excelentes candidatos para a colocação em cache.  

Para obter um exemplo de como tooget Olá de toodiscover de propriedades de um blob data da última modificação através do .NET, consulte o artigo [conjunto e obter as propriedades e metadados](storage-properties-metadata.md). Para obter mais informações sobre as transferências condicionais, consulte [condicionalmente atualizar uma cópia Local de um Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx).  

#### <a name="subheading8"></a>Carregamento de dados em lotes
Em alguns cenários de aplicação, pode agregar dados localmente e, em seguida, carregá-lo periodicamente num batch em vez de carregamento de cada conjunto de dados imediatamente. Por exemplo, uma aplicação web poderá manter um ficheiro de registo de atividades: Olá aplicação foi a carregar detalhes de cada atividade como ocorre como uma entidade de tabela (o que necessita de muitas operações de armazenamento) ou se foi possível guardar a atividade detalhes tooa local ficheiro de registo e, em seguida, periodicamente, carregar todos os detalhes de atividade como um blob do ficheiro delimitado tooa. Se cada entrada de registo for de 1KB de tamanho, pode carregar milhares numa única transação "Colocar Blob" (pode carregar um blob de cópia de segurança too64MB tamanho numa única transação). Obviamente, se o computador local Olá falhas de carregamento anteriores toohello, potencialmente perderá alguns dados de registo: programador da aplicação Olá tem de design para a possibilidade de Olá de dispositivo cliente ou carregar falhas.  Se precisar de dados de atividade Olá toobe transferido para timespans (não apenas única atividade), os blobs são recomendados através de tabelas.

### <a name="net-configuration"></a>Configuração do .NET
Se utilizar hello .NET Framework, esta secção lista as várias definições de configuração rápida, que pode utilizar toomake melhorias de desempenho significativas.  Se utilizar outros idiomas, verifique toosee se conceitos semelhantes aplicam-se no idioma que escolheu.  

#### <a name="subheading9"></a>Aumentar o limite de ligação predefinido
No .NET, Olá seguinte código aumenta o limite de ligação predefinido do Olá (que é, normalmente, 2 num ambiente de cliente ou 10 num ambiente de servidor) too100. Normalmente, deve definir Olá valor tooapproximately Olá número de threads utilizados pela sua aplicação.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

Tem de definir o limite de ligação de Olá antes de abrir todas as ligações.  

Para outras linguagens de programação, consulte toodetermine de documentação nesse idioma como ligação de Olá tooset limitar.  

Para obter mais informações, consulte a mensagem de blogue de Olá [serviços Web: ligações simultâneas](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx).  

#### <a name="subheading10"></a>Aumentar ThreadPool Min Threads, se utilizar o código síncrono com Async tarefas
Este código irá aumentar os threads de mín. de conjunto de threads de Olá:  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

Para obter mais informações, consulte [ThreadPool.SetMinThreads método](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx).  

#### <a name="subheading11"></a>Tirar partido da recolha de lixo do .NET 4.5
Utilize o .NET 4.5 ou posterior para Olá cliente aplicação tootake partido melhoramentos de desempenho na recolha de lixo do servidor.

Para obter mais informações, consulte o artigo de Olá [uma descrição geral dos melhoramentos de desempenho no .NET 4.5](http://msdn.microsoft.com/magazine/hh882452.aspx).  

### <a name="subheading12"></a>Paralelismo unbounded
Enquanto o paralelismo pode ser para um desempenho ótimo, tenha cuidado sobre como utilizar o paralelismo unbounded (sem limite no número de Olá de threads e/ou pedidos paralelos) tooupload ou transferência de dados, utilizando vários trabalhadores tooaccess várias partições (contentores, filas, ou as partições de tabela) no Olá mesma conta de armazenamento ou tooaccess vários itens na Olá mesma partição. Se for unbounded paralelismo Olá, a aplicação pode exceder as capacidades do dispositivo cliente Olá ou Olá objetivos de escalabilidade da conta de armazenamento, resultando em períodos de latência superiores e limitação.  

### <a name="subheading13"></a>Bibliotecas de cliente de armazenamento e ferramentas
Utilize sempre a ferramentas e bibliotecas de cliente do Microsoft fornecido Olá mais recentes. No momento de Olá de escrita, existem bibliotecas de cliente disponíveis para .NET, Windows Phone, Windows e tempo de execução, Java, C++, bem como bibliotecas de pré-visualização para outros idiomas. Além disso, a Microsoft lançou comandos da CLI do Azure para trabalhar com o Storage do Azure e cmdlets do PowerShell. Microsoft ativamente desenvolvidas pela organização estas ferramentas com o desempenho em mente, mantém-na cópia de segurança toodate com versões de service Olá mais recentes e assegura que processam muitas das Olá comprovada internamente práticas de desempenho.  

### <a name="retries"></a>Tentativas
#### <a name="subheading14"></a>Limitação/ServerBusy
Em alguns casos, o serviço de armazenamento Olá pode limitar a aplicação ou podem simplesmente ser pedido de Olá tooserve não é possível devido a condição transitória toosome e devolver uma mensagem de "503 servidor ocupado" ou "tempo limite 500".  Isto pode acontecer se a aplicação está a aproximar-se qualquer um dos objetivos de escalabilidade hello, ou se o sistema Olá é reequilíbrio sua tooallow dados particionada para maior débito.  aplicação de cliente Olá, normalmente, deve repetir a operação de Olá que faz com que este tipo de erro: tentativa de Olá mesmo pedido mais tarde pode ter êxito. No entanto, se o serviço de armazenamento Olá é a limitação da aplicação porque está a exceder os objetivos de escalabilidade, ou mesmo que o serviço de Olá foi pedido de Olá tooserve não é possível, por algum motivo, tentativas agressiva se normalmente worse de problema Olá. Por este motivo, deve utilizar um exponencial novamente desativar (Olá cliente bibliotecas toothis comportamento predefinido). Por exemplo, a aplicação pode repetir após 2 segundos, em seguida, 4 segundos, em seguida, 10 segundos, em seguida, 30 segundos e, em seguida, dê a cópia de segurança completamente. Este comportamento resulta na sua aplicação significativamente reduzir a carga no serviço de Olá em vez de exacerbating quaisquer problemas.  

Tenha em atenção que erros de conectividade podem ser repetidos de imediato, pois não são resultado de Olá de limitação e são esperado toobe transitório.  

#### <a name="subheading15"></a>Erros de não repetição
bibliotecas de cliente Olá sabem que erros são capazes de repetição e que não são. No entanto, se estiver a escrever o seu próprio código com o armazenamento de Olá REST API, não existem alguns erros que não deve repetir: por exemplo, um 400 (pedido incorreto) resposta indica que aplicações de cliente Olá enviado um pedido que não foi possível processar porque-la não era um formato esperado. Reenviar este pedido resultará Olá resposta mesma sempre, pelo que não existe nenhum ponto no repeti-lo. Se estiver a escrever o seu próprio código com o armazenamento de Olá REST API, tenha em atenção que erro Olá códigos de média e Olá tooretry de forma adequada (ou não) para cada um deles.  

#### <a name="useful-resources"></a>Recursos Úteis
Para obter mais informações sobre códigos de erro de armazenamento, consulte [estado e códigos de erro](http://msdn.microsoft.com/library/azure/dd179382.aspx) no web site do Microsoft Azure Olá.  

## <a name="blobs"></a>Blobs
No toohello adição comprovada práticas para [todos os serviços](#allservices) descrito anteriormente, o seguinte Olá comprovada práticas aplicam-se o serviço de blob toohello especificamente.  

### <a name="blob-specific-scalability-targets"></a>Objetivos de escalabilidade de blob específico
#### <a name="subheading46"></a>Vários clientes aceder em simultâneo num único objeto
Se tiver um grande número de clientes aceder em simultâneo num único objeto terá tooconsider por objeto e o armazenamento objetivos de escalabilidade da conta. número exato de Olá de clientes que podem aceder a um único objeto irá variar dependendo de fatores, tais como o número de Olá de clientes que solicitam objeto Olá em simultâneo, tamanho de Olá do objeto de Olá, condições etc de rede.

Se o objeto de Olá pode ser distribuído através de uma CDN, como imagens ou vídeos servido a partir de um Web site, em seguida, deve utilizar uma CDN. Consulte [aqui](#subheading5).

Outros cenários tais como simulações científicos onde os dados de Olá são confidenciais tem duas opções. Olá é primeiro toostagger acesso da carga de trabalho esses que Olá objeto é acedido durante um período de vs tempo a ser acedido em simultâneo. Em alternativa, pode copiar temporariamente Olá objeto toomultiple contas do storage aumentando Olá ESP totais por objeto e em contas de armazenamento. Nos testes limitado encontrámos que cerca 25 VMs em simultâneo foi possível transferir um blob de 100GB em paralelo (cada VM foi parallelizing transferência Olá utilizando 32 threads). Se tiver 100 clientes que necessitam do objeto de Olá tooaccess, primeiro copiá-lo tooa segunda conta de armazenamento e, em seguida, ter Olá primeiro 50 VMs acesso Olá primeiro blob e Olá segundo 50 VMs acesso Olá segundo blob. Os resultados variam consoante o comportamento de aplicações, de modo deverá testar isto durante a conceção. 

#### <a name="subheading16"></a>Operações por BLOBs e largura de banda
Pode ler ou escrever tooa blob único na cópia de segurança máximo tooa 60 MB por segundo (isto é aproximadamente 480 Mbps que excede as capacidades de Olá de várias redes de lado do cliente (incluindo Olá NIC física no dispositivo de cliente Olá). Além disso, um blob único suporta a cópia de segurança too500 pedidos por segundo. Se tiver vários clientes que necessitam de tooread hello mesmo blob e poderá exceder estes limites, deve considerar a utilização de uma CDN para distribuir blob Olá.  

Para obter mais informações sobre o débito de destino para blobs, consulte [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md).  

### <a name="copying-and-moving-blobs"></a>Copiar e mover Blobs
#### <a name="subheading17"></a>Copiar Blob
armazenamento de Olá API de REST versão 2012-02-12 introduzida blobs de toocopy Olá capacidade útil em contas: uma aplicação cliente pode instruir Olá armazenamento serviço toocopy um blob de outra origem (possivelmente por uma conta de armazenamento diferente) e, em seguida, permitem Olá serviço efetuar cópia de Olá no modo assíncrono. Isto pode reduzir significativamente a largura de banda Olá necessária para a aplicação Olá quando estiver a migrar dados a partir de outras contas de armazenamento porque não tem toodownload e carregar dados de Olá.  

A primeira consideração, no entanto, é que, quando copiar entre contas de armazenamento, não há nenhuma garantia de tempo no quando a cópia de Olá irá concluir. Se a sua aplicação tiver toocomplete um blob rapidamente copiar sob o seu controlo, poderá ser melhor blob de Olá toocopy, transferindo-tooa VM e, em seguida, carregá-lo toohello destino.  Para a previsão completa nesta situação, certifique-se de que é efetuada cópia de Olá por uma VM em execução no Olá mesma região do Azure; caso contrário, as condições de rede poderá (e provavelmente serão) afetar o desempenho de cópia.  Além disso, pode monitorizar progresso Olá uma cópia assíncrona através de programação.  

Tenha em atenção que copia dentro Olá a mesma conta de armazenamento em si são geralmente concluída rapidamente.  

Para obter mais informações, consulte [copiar Blob](http://msdn.microsoft.com/library/azure/dd894037.aspx).  

#### <a name="subheading18"></a>Utilizar o AzCopy
equipa de armazenamento do Azure Olá lançou uma ferramenta da linha de comandos "AzCopy" que é o principal objetivo toohelp com transferir blobs muitas para, de e, em contas de armazenamento de massa.  Esta ferramenta está otimizada para este cenário e pode alcançar a velocidades máximas de transferência elevada.  A sua utilização está encouraged para carregamento em massa, transfira e cenários de cópia. mais acerca do mesmo toolearn e transferi-lo, consulte [transferir dados com o utilitário de linha de comandos do AzCopy Olá](storage-use-azcopy.md).  

#### <a name="subheading19"></a>Serviço de importação/exportação do Azure
Para grandes volumes de dados (mais de 1TB), Olá Storage do Azure oferece Olá serviço de importação/exportação, o que permite carregar e transferir a partir do blob storage pelo envio de unidades de disco rígido.  Pode colocar os dados num disco rígido e enviá-lo tooMicrosoft para carregamento ou enviar um disco rígido em branco tooMicrosoft toodownload de dados.  Para obter mais informações, consulte [utilizar Olá serviço de importação/exportação do Microsoft Azure tooTransfer dados tooBlob armazenamento](storage-import-export-service.md).  Isto pode ser muito mais eficiente do que o carregamento/transferir este volume de dados através de rede de Olá.  

### <a name="subheading20"></a>Utilizar metadados
serviço de blob Olá suporta pedidos head, que podem incluir metadados sobre blob Olá. Por exemplo, se a aplicação necessária dados EXIF Olá fora de uma fotografia, este obter fotografia Olá e extraia. toosave largura de banda e melhorar o desempenho, a aplicação foi possível armazenar dados EXIF de Olá nos metadados do blob Olá quando a aplicação Olá carregados de fotografia Olá: pode, em seguida, obter Olá EXIF dados nos metadados utilizando apenas um cabeçalho de pedido, poupando largura de banda significativa e tempo de processamento de Olá necessárias tooextract Olá dados EXIF cada blob Olá de tempo é de leitura. Isto é útil em cenários onde apenas tem metadados de Olá e não Olá conteúdo completo de um blob.  Tenha em atenção que apenas de 8 KB de metadados podem ser armazenado por blob (serviço de Olá não aceitará toostore um pedido superior), pelo que o se dados Olá não caber nesse tamanho, o utilizador não pode ser capaz de toouse esta abordagem.  

Para obter um exemplo de como tooget metadados de um blob através do .NET, consulte [conjunto e obter as propriedades e metadados](storage-properties-metadata.md).  

### <a name="uploading-fast"></a>Carregar rápida
os blobs tooupload rápidos, Olá primeira pergunta tooanswer é: tem a carregar um blob ou muitas?  Utilize Olá abaixo orientações toodetermine Olá método correto toouse dependendo do seu cenário.  

#### <a name="subheading21"></a>Carregar um blob grande rapidamente
tooupload rapidamente de um único grande BLOBs, a aplicação cliente deverá carregar os respetivos blocos ou páginas em paralelo (que está a ser mindful de destinos de escalabilidade Olá para os blobs individuais e conta de armazenamento de Olá como um todo).  Tenha em atenção que Olá oficiais Microsoft fornecidos pelo RTM armazenamento bibliotecas do cliente (.NET, Java) têm Olá capacidade toodo isto.  Para cada uma das bibliotecas de Olá, utilize Olá abaixo de nível de Olá tooset especificado/propriedade do objeto de concorrência:  

* .NET: Conjunto ParallelOperationThreadCount num toobe de objeto BlobRequestOptions utilizado.
* Java/Android: Utilizar BlobRequestOptions.setConcurrentRequestCount()
* NODE.js: Utilize parallelOperationThreadCount em qualquer uma das opções de pedido de Olá ou num serviço de blob Olá.
* C++: Olá blob_request_options::set_parallelism_factor método.

#### <a name="subheading22"></a>Carregar rapidamente muitas blobs
tooupload muitas blobs rapidamente, carregue blobs em paralelo. Este é mais rápida do que o carregamento blobs único numa altura com bloco parallel carregamentos porque esta propaga Olá carregamento em várias partições do serviço de armazenamento Olá. Um blob único só suporta um débito de 60 MB por segundo (Mbps aproximadamente 480). No momento de Olá de escrita, uma conta com base em E.U.A. LRS suporta até too20, entrada Gbps, que é muito mais do que o débito de Olá suportado por um blob individuais.  [AzCopy](#subheading18) efetua carregamentos em paralelo, por predefinição e é recomendado para este cenário.  

### <a name="subheading23"></a>Escolher Olá tipo correto de blob
Storage do Azure suporta dois tipos de BLOBs: *página* blobs e *bloco* blobs. Para um cenário de utilização de determinada, à sua escolha do tipo de blob afetará Olá desempenho e de escalabilidade da sua solução. Os blobs de blocos são adequados quando quiser grandes quantidades de tooupload de dados de forma eficiente: por exemplo, uma aplicação cliente pode ter fotografias tooupload ou armazenamento tooblob vídeo. Os blobs de páginas são adequados se a aplicação de Olá tiver tooperform gravações aleatórias em dados de Olá: por exemplo, os VHDs do Azure são armazenados como blobs de páginas.  

Para obter mais informações, consulte [compreender os Blobs de blocos, os Blobs de acréscimo e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).  

## <a name="tables"></a>Tabelas
No toohello adição comprovada práticas para [todos os serviços](#allservices) descrito anteriormente, o seguinte Olá comprovada práticas aplicam-se o serviço de tabela toohello especificamente.  

### <a name="subheading24"></a>Objetivos de escalabilidade da tabela específico
Limitações de largura de banda de toohello de adição de uma conta de armazenamento completa, tabelas tem Olá seguir o limite de escalabilidade específico.  Tenha em atenção que o sistema de Olá será o balanceamento de carga à medida que aumenta o tráfego, mas se o tráfego tiver bursts repentino, não pode ser capaz de tooget este volume de débito imediatamente.  Se o seu padrão de tem bursts, deve esperar toosee limitação e/ou tempos limite durante Olá rajada como serviço de armazenamento Olá automaticamente equilibra a carga fora da tabela.  Ramping lentamente, geralmente, a cópia de segurança tem melhores resultados, que fornece balanceamento de tooload de tempo de sistema Olá adequadamente.  

#### <a name="entities-per-second-account"></a>Entidades por segundo (conta)
o limite de escalabilidade Olá para aceder a tabelas está a funcionar de too20, 000 entidades (de 1KB cada) por segundo para uma conta.  Em geral, cada entidade que é inserida, atualizar, eliminado ou analisados contagens para este destino.  Por isso, uma inserção de lote que contém 100 entidades contabilizaria como 100 entidades.  Uma consulta que verifica a existência de entidades de 1000 devolve 5 contabilizaria como entidades de 1000.  

#### <a name="entities-per-second-partition"></a>Entidades por segundo (partição)
Dentro de uma única partição Olá destino escalabilidade para aceder a tabelas é 2.000 entidades (de 1KB cada) por segundo, utilizando Olá contando mesmo, tal como descrito na secção anterior Olá.  

### <a name="configuration"></a>Configuração
Esta secção apresenta várias definições de configuração rápida, que pode utilizar toomake melhorias de desempenho significativas no serviço de tabela Olá:  

#### <a name="subheading25"></a>Utilizar JSON
A partir da versão de serviço de armazenamento 2013-08-15, serviço de tabela Olá suporta utilizando JSON em vez do formato de baseado em XML AtomPub Olá para transferência de dados de tabela. Isto pode reduzir o tamanho do payload, quanto 75% e pode significativamente melhorar o desempenho de Olá da sua aplicação.

Para obter mais informações, consulte Olá publique [tabelas do Microsoft Azure: introdução ao JSON](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) e [formato de Payload para operações de serviço tabela](http://msdn.microsoft.com/library/azure/dn535600.aspx).

#### <a name="subheading26"></a>Nagle desativado
Algoritmo da Nagle amplamente é implementado em redes TCP/IP como um meio tooimprove um desempenho de rede. No entanto, não é ideal em todas as circunstâncias (por exemplo, ambientes de elevada disponibilidade interativas). Para o armazenamento do Azure, o algoritmo do Nagle tem um impacto negativo no desempenho de Olá dos serviços de tabela e fila de toohello de pedidos e deve desativá-lo se for possível.  

Para obter mais informações, consulte o nosso artigo de blogue [algoritmo do Nagle não é amigável para pedidos de pequenas](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), que explica por que motivo o algoritmo do Nagle mal interage com pedidos de tabela e fila e mostra como toodisable-lo no seu cliente aplicação.  

### <a name="schema"></a>Esquema
Como representar e os dados de consulta é Olá maior único fator que afeta o desempenho de Olá do serviço de tabela Olá. Enquanto todas as aplicações for diferente, esta secção descreve algumas práticas comprovadas gerais que se relacionam com a:  

* Estruturar tabela
* Consultas eficiente
* Atualizações de dados eficiente  

#### <a name="subheading27"></a>As tabelas e partições
As tabelas são divididas em partições. Cada entidade armazenada numa partição partilhas Olá a mesma chave de partição e tem um tooidentify de chave de linha exclusivo-lo dentro dessa partição. As partições fornecem vantagens, mas também introduzem limites de escalabilidade.  

* Benefícios: Pode atualizar as entidades de Olá mesma partição numa transação batch atomic, único que contém a cópia de segurança operações de armazenamento separada too100 (limite de tamanho total de 4MB). Partindo do princípio de Olá o mesmo número de entidades toobe obtido, pode também consultar dados dentro de uma única partição forma mais eficiente do que os dados que abrange partições (embora continue a ler para obter mais recomendações sobre consultar os dados de tabela).
* O limite de escalabilidade: tooentities de acesso armazenada numa única partição não pode ser com balanceamento de carga porque partições suportam transações de atomic batch. Por este motivo, o destino de escalabilidade Olá para uma partição de tabela individuais é inferior do serviço de tabela Olá como um todo.  

Devido a estas características de tabelas e partições, deve que adotar Olá seguintes princípios de design:  

* Dados que a aplicação cliente frequentemente atualizado ou consultados em Olá mesma unidade lógica de trabalho deve estar localizada no Olá mesma partição.  Isto poderá ser-se ao facto da aplicação é agregar escritas ou quiser tootake partido das operações de atomic batch.  Além disso, os dados de uma única partição podem ser de forma mais eficiente consultados numa única consulta de dados em partições.
* Dados que a aplicação de cliente não inserção/atualização ou consultar no Olá mesma unidade lógica de trabalho (uma consulta simples ou atualização do batch) deve estar localizada no separam partições.  Uma nota importante é que não é não existe nenhum limite toohello diversas chaves de partição numa tabela individual, para que ter milhões de chaves de partição não é um problema e não irá afetar o desempenho.  Por exemplo, se a aplicação é um Web site popular com início de sessão do utilizador, utilizar Olá Id de utilizador como chave de partição Olá poderia ser uma boa opção.  

#### <a name="hot-partitions"></a>Partições frequente
Uma partição de acesso frequente é aquele que está a receber uma percentagem desproporcionada da conta de tooan Olá tráfego e não pode ser com balanceamento de carga porque se trata de uma única partição.  Em geral, frequente são criadas partições uma de duas formas:  

##### <a name="subheading28"></a>Apenas a acrescentar e preceder padrões apenas
Olá "Acrescentar apenas" padrão é um onde todos os (ou quase todos os) de Olá tráfego tooa fornecido PK aumentam e diminui toohello de acordo com a hora atual.  Um exemplo é se a aplicação utilizou Olá data atual como uma chave de partição para dados de registo.  Isto resulta em todos os inserções Olá vai toohello partição último na tabela e sistema Olá não é possível o balanceamento de carga porque todos os escritas de paginações hello são curso toohello end da sua tabela.  Se o volume de Olá da partição do tráfego toothat excede o destino de escalabilidade de nível de partição Olá, em seguida, irá resultar na limitação.  É melhor tooensure que o tráfego é enviado toomultiple partições, Olá de balanceamento de carga tooenable pedidos entre a tabela.  

##### <a name="subheading29"></a>Dados de tráfego elevado
Se os resultados de esquema de criação de partições numa única partição o que tem apenas de dados que são muito mais utilizados que outras partições, pode também ver limitação como dessa partição se aproxima destino de escalabilidade Olá para uma única partição.  É melhor toomake certificar-se de que os resultados de esquema de partição em nenhum única partição aproximado metas de escalabilidade Olá.  

#### <a name="querying"></a>Consultar
Esta secção descreve comprovadas práticas para consultar o serviço de tabela Olá.  

##### <a name="subheading30"></a>Âmbito de consulta
Existem várias formas toospecify Olá intervalo tooquery de entidades.  Olá que se segue um debate do utiliza Olá de cada.  

Em geral, evite análises (consultas maiores do que uma única entidade), mas se deve analisar, tente tooorganize os dados para que as análises obtêm dados de Olá que precisar, sem análise ou devolver quantidades significativas de entidades que não precisa.  

###### <a name="point-queries"></a>Ponto de consultas
Uma consulta de ponto obtém exatamente uma entidade. Efetua este procedimento, especificando a chave de partição Olá e chave de linha de Olá tooretrieve de entidade. Estas consultas são muito eficientes e deve utilizar sempre que possível.  

###### <a name="partition-queries"></a>Consultas de partição
Uma consulta de partição é uma consulta que obtém um conjunto de dados que partilha uma chave de partição comuns. Normalmente, consulta Olá Especifica um intervalo de valores de chave de linha ou um intervalo de valores para algumas propriedades de entidade na chave de partição tooa de adição. Estas são menos eficientes do que o ponto de consultas e devem ser utilizadas com moderação.  

###### <a name="table-queries"></a>Consultas de tabela
Uma consulta de tabela é uma consulta que obtém um conjunto de entidades que partilham uma chave de partição comuns. Estas consultas não são eficientes e deve evitar se possível.  

##### <a name="subheading31"></a>Densidade de consulta
Outro fator chave na eficiência de consulta é o número de Olá de entidades devolvido como toohello em comparação com número de entidades toofind digitalizados Olá devolvido definida. Se a aplicação executa uma consulta de tabela com um filtro para um valor de propriedade que apenas 1% Olá dados partilhas de consulta Olá irá analisar 100 entidades para cada uma entidade devolve. Olá objetivos de escalabilidade da tabela abordados anteriormente todos os relacionados com o número de toohello de entidades analisados e não Olá número de entidades devolvido: uma densidade de consulta baixa pode facilmente causar Olá tabela serviço toothrottle a aplicação porque tem de analisar tantas entidade de Olá do tooretrieve de entidades que procura.  Consulte a secção de Olá abaixo no [denormalization](#subheading34) para obter mais informações sobre como tooavoid isto.  

##### <a name="limiting-hello-amount-of-data-returned"></a>Limitar a quantidade de dados devolvidos de Olá
###### <a name="subheading32"></a>Filtragem
Quando souber que uma consulta devolverá entidades que não precisa de na aplicação de cliente Olá, considere utilizar um tamanho de Olá tooreduce de filtro de Olá devolvida um conjunto. Ao entidades Olá devolvido não cliente toohello ainda contam para limites de escalabilidade Olá, o desempenho de aplicações irá melhorar devido ao tamanho do payload de rede Olá reduzido e Olá número reduzido de entidades que a aplicação cliente tem de processar .  Consulte acima nota no [densidade de consulta](#subheading31), no entanto – metas de escalabilidade Olá referem-se toohello número de entidades analisados, pelo que uma consulta, que filtra muitas entidades ainda poderá resultar em limitação, mesmo que algumas entidades são devolvidas.  

###### <a name="subheading33"></a>Projeção
Se a aplicação cliente tem apenas um conjunto limitado de propriedades de entidades de Olá na tabela, pode utilizar projeção toolimit Olá o tamanho de Olá devolvida um conjunto de dados. Tal como acontece com a filtragem, isto ajuda a carga na rede tooreduce e processamento de cliente.  

##### <a name="subheading34"></a>Denormalization
Ao contrário de trabalhar com bases de dados relacionais, hello comprovadas práticas de forma eficiente consultar os dados de tabela levar toodenormalizing os dados. Ou seja, duplicar Olá mesmos dados em várias entidades (um para cada chave podem utilizar dados de Olá toofind) toominimize Olá diversas entidades que uma consulta deve analisar toofind Olá dados Olá necessidades do cliente, em vez de ter tooscan grande número de entidades toofind dados Olá tem a sua aplicação.  Por exemplo, num Web site comércio eletrónico, poderá pretender toofind uma ordem tanto por ID de cliente Olá (Atribuir-me as ordens este cliente) e por data Olá (Atribuir-me ordens numa data).  O Table Storage, é melhor entidade de Olá toostore (ou uma referência tooit) duas vezes – uma vez com o nome da tabela, PK e RK toofacilitate a localizar por ID de cliente, uma vez toofacilitate encontrá-las por data Olá.  

#### <a name="insertupdatedelete"></a>Inserir/atualizar/eliminar
Esta secção descreve comprovadas práticas para entidades armazenadas no serviço de tabela Olá a modificar.  

##### <a name="subheading35"></a>Criação de batches
Transações de batches são conhecidas como transações de grupo de entidade (ETG) no Storage do Azure; todas as operações de Olá dentro de um ETG tem de estar numa única partição numa tabela individual. Sempre que possível, utilize ETGs tooperform introduções, atualizações e eliminações em lotes. Isto reduz o número de Olá de ida e volta a partir do seu servidor de toohello de aplicação de cliente, reduz o número de Olá de transações facturável (um ETG contagens como uma transação única para fins de faturação e pode conter segurança too100 operações de armazenamento) e permite atómico atualizações (todas as operações com êxito ou a totalidade falhar dentro de um ETG). Ambientes com altas latências, tais como dispositivos móveis irão beneficiar significativamente ETGs a utilizar.  

##### <a name="subheading36"></a>Upsert
Tabela de utilização **Upsert** operações sempre que possível. Existem dois tipos de **Upsert**, que podem ser mais eficiente do que um tradicional **inserir** e **atualização** operações:  

* **InsertOrMerge**: Utilize esta opção quando quiser tooupload um subconjunto de propriedades de entidade Olá, mas não tem a certeza se a entidade de Olá já existe. Se existir a entidade de Olá, esta chamada atualiza as propriedades de Olá incluídas no Olá **Upsert** operação e deixa de todas as propriedades existentes conforme forem, se hello entidade não existe, -insere a entidade Olá de novo. Isto é semelhantes toousing projecção numa consulta, só precisa de propriedades de Olá tooupload que estão a alterar.
* **InsertOrReplace**: Utilize esta opção quando quiser tooupload uma entidade completamente nova, mas não tem a certeza se já existe. Isto só deve utilizar quando sabe que Olá recentemente carregados entidade é inteiramente correta porque substitui entidade antigo Olá completamente. Por exemplo, pretende que a entidade de Olá tooupdate que armazena a localização do utilizador atual, independentemente se pretende ou não aplicação Olá tem armazenadas anteriormente os dados de localização para o utilizador Olá; Olá nova entidade de localização está concluída e não é necessário qualquer informação sobre qualquer entidade anterior.

##### <a name="subheading37"></a>Armazenar de dados de séries de uma única entidade
Por vezes, uma aplicação armazena uma série de dados que frequentemente necessita tooretrieve, uma vez: por exemplo, uma aplicação pode controlar a utilização da CPU ao longo do tempo na ordem tooplot um gráfico graduais dos dados de Olá do Olá últimas 24 horas. Uma abordagem é a entidade de uma tabela de toohave por hora, com cada entidade que representa uma hora específica e armazenar a utilização da CPU de Olá para essa hora. tooplot estes dados, aplicação Olá tem de entidades de Olá tooretrieve que contém dados Olá Olá 24 horas mais recentes.  

Em alternativa, a aplicação foi possível armazenar a utilização da CPU de Olá para cada hora como uma propriedade de diferente de uma única entidade: tooupdate cada hora, a aplicação pode utilizar um único **InsertOrMerge Upsert** chamar o valor de Olá tooupdate para Olá hora mais recente. dados de Olá tooplot, Olá aplicação só tem de tooretrieve uma única entidade em vez de 24, tornando-se para uma consulta muito eficiente (consulte acima debate sobre [consultar âmbito](#subheading30)).

##### <a name="subheading38"></a>Armazenar dados estruturados em blobs
Dados estruturados, por vezes, funciona como se deve passar nas tabelas, mas os intervalos de entidades sempre são obtidos em conjunto e pode ser inserido batch.  Um bom exemplo desta situação é um ficheiro de registo.  Neste caso, pode vários minutos de registos do batch, insira-as e, em seguida, são sempre obter alguns minutos de registos de cada vez, bem como.  Neste caso, para um desempenho, é melhor toouse blobs, em vez de tabelas, uma vez que pode reduzir significativamente o número de Olá de escritas/devolveu objetos, bem como Olá, normalmente, o número de pedidos que necessitam de efetuadas.  

## <a name="queues"></a>Filas
No toohello adição comprovada práticas para [todos os serviços](#allservices) descrito anteriormente, o seguinte Olá comprovada práticas aplicam-se o serviço de fila de toohello especificamente.  

### <a name="subheading39"></a>Limites de escalabilidade
Uma fila única pode processar aproximadamente 2.000 mensagens (de 1KB cada) por segundo (cada número AddMessage, GetMessage e DeleteMessage como uma mensagem aqui). Se isto é insuficiente para a sua aplicação, deve utilizar várias filas e distribuídos mensagens hello por-los.  

Ver os objetivos de escalabilidade atual em [metas de desempenho e escalabilidade do Storage do Azure](storage-scalability-targets.md).  

### <a name="subheading40"></a>Nagle desativado
Consulte a secção de Olá na configuração de tabela que descreve o algoritmo de Nagle Olá — algoritmo de Nagle Olá é geralmente incorreto para o desempenho de Olá de pedidos de fila, e deve desativá-lo.  

### <a name="subheading41"></a>Tamanho da mensagem
Fila de desempenho e escalabilidade fique à medida que aumenta de tamanho da mensagem. Deve colocar apenas Olá informações Olá recetor necessidades de uma mensagem.  

### <a name="subheading42"></a>Obtenção do batch
Pode obter segurança too32 mensagens numa fila numa única operação. Isto pode reduzir o número de Olá de e voltas da aplicação de cliente Olá, que é especialmente útil para ambientes, como dispositivos móveis, com latência elevada.  

### <a name="subheading43"></a>Intervalo de consulta da fila
Consultar a maioria das aplicações para mensagens a partir de uma fila, que pode ser uma das origens de maiores Olá de transações para essa aplicação. Selecione o intervalo de consulta da forma sensata: com demasiada frequência de consulta pode fazer com que a aplicação tooapproach metas de escalabilidade Olá para a fila de Olá. No entanto, ao 200 000 transações para $0.01 (momento Olá da escrita), um único processador consulta depois a cada segundo durante um mês seria custo inferior a 15 cents custos, por isso, não é normalmente um fator que afeta a sua escolha de intervalo de consulta.  

Para informações de custo atualizado, consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/).  

### <a name="subheading44"></a>UpdateMessage
Pode utilizar **UpdateMessage** tooincrease Olá invisibilidade tempo limite ou tooupdate informações de estado de uma mensagem. Embora seja poderosa, lembre-se de que cada **UpdateMessage** operação conta para o destino de escalabilidade Olá. No entanto, isto pode ser uma abordagem muito mais eficiente do que o fluxo de trabalho que passa uma tarefa de uma fila toohello em seguida, como cada passo da tarefa de Olá é concluído. Utilizar Olá **UpdateMessage** operação permite que a sua mensagem de estado de toohello do aplicação toosave Olá tarefa e, em seguida, continuar a trabalhar, em vez de mensagem de saudação novamente a colocação em fila para o passo seguinte do Olá da tarefa de Olá sempre que um passo é concluído.  

Para obter mais informações, consulte o artigo de Olá [como: alterar Olá conteúdo de uma mensagem em fila](storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message).  

### <a name="subheading45"></a>Arquitetura de aplicações
Deve utilizar filas toomake da arquitetura de aplicação escalável. seguinte Olá apresenta uma lista de algumas formas que pode utilizar a aplicação mais dimensionável toomake filas:  

* Pode utilizar registos de segurança de toocreate de filas do trabalho para processamento e uniforme saída cargas de trabalho na sua aplicação. Por exemplo, foi fila dos pedidos de trabalho que consomem muita do processador de tooperform de utilizadores, tais como o redimensionamento de imagens carregadas.
* Pode utilizar as partes de toodecouple de filas da sua aplicação para que pode dimensionamento independente. Por exemplo, uma web front-end foi colocar os resultados do inquérito dos utilizadores para uma fila para posterior análise e armazenamento. Pode adicionar que mais tooprocess de instâncias de função de trabalho Olá dados fila conforme necessário.  

## <a name="conclusion"></a>Conclusão
Este artigo discutidos alguns dos Olá mais comuns, comprovada práticas para otimizar o desempenho ao utilizar o armazenamento do Azure. Estamos a encorajar os respetivos aplicação relativamente a cada um dos Olá acima práticas de cada tooassess de programador da aplicação e considere agir em Olá recomendações tooget um excelente desempenho para as aplicações que utilizam o armazenamento do Azure.
