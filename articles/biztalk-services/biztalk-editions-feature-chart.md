---
title: "aaaLearn sobre as funcionalidades nas edições dos BizTalk Services | Microsoft Docs"
description: "Compara Olá capacidades das edições do Olá BizTalk Services: gratuita, programador, básica, Standard e Premium. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>BizTalk Services: Gráfico de Edições

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Os BizTalk Services do Azure oferecem várias edições. Utilize este toodetermine artigo que edição é mais adequada às suas necessidades comerciais e de cenário.

## <a name="compare-hello-editions"></a>Comparar as edições de Olá
**Gratuita (Pré-visualização)**

Pode criar e gerir Ligações Híbridas. Uma ligação híbrida é uma forma fácil de tooconnect tooan um Web site do Azure no local o sistema, como o SQL Server.

**Programador**

Inclui Ligações Híbridas, processamento de mensagens EAI e EDI com um portal de gestão de parceiro comercial de utilização fácil e suporte para esquemas EDI comuns e processamentos EDI através de X12 e AS2. Pode criar cenários comuns de EAI ligando serviços em nuvem Olá com qualquer tooread de protocolos HTTP/S, REST, FTP, WCF e SFTP e escrever mensagens.  Utilize sistemas LOB de tooon local de conectividade com adaptadores SAP, Oracle eBusiness, Oracle DB, Siebel e o SQL Server de prontos a utilizar. Utilize um ambiente centrado no programador com as ferramentas do Visual Studio para desenvolvimento e implementação fáceis. Limitado toodevelopment e teste efeitos apenas com nenhum nível contrato serviço (SLA).

**Básica**

Inclui grande parte das capacidades de programador Olá com incrementos nas ligações de ligações híbridas, pontes EAI, nos contratos EDI e BizTalk Adapter Pack. Também oferece elevada disponibilidade e Olá opção tooscale com um contrato de nível de serviço (SLA).

**Standard**

Inclui todas as capacidades de básico Olá com incrementos nas ligações de ligações híbridas, pontes EAI, nos contratos EDI e BizTalk Adapter Pack. Também oferece elevada disponibilidade e Olá opção tooscale com um contrato de nível de serviço (SLA).

**Premium**

Inclui todas as capacidades de padrão de Olá com incrementos nas ligações de ligações híbridas, pontes EAI, nos contratos EDI e BizTalk Adapter Pack. Também inclui arquivamento, elevada disponibilidade e Olá opção tooscale com um contrato de nível de serviço (SLA).

## <a name="editions-chart"></a>Gráfico de edições
Olá tabela seguinte lista as diferenças de Olá.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Gratuita (Pré-visualização)</th>
        <th>Programador</th>
        <th>Básica</th>
        <th>Standard</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Preço inicial</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Preços dos Serviços BizTalk do Azure</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full">Calculadora de Preços do Azure</a></td>
</tr>
<tr>
<td><strong>Configuração mínima predefinida</strong></td>
<td>1 Unidade Gratuita</td>
<td>1 Unidade de Programador</td>
<td>1 Unidade Básica</td>
<td>1 Unidade Standard</td>
<td>1 Unidade Premium</td>
</tr>
<tr>
<td><strong>Dimensionamento</strong></td>
<td>Sem Dimensionamento</td>
<td>Sem Dimensionamento</td>
<td>Sim, em incrementos de 1 unidade Básica</td>
<td>Sim, em incrementos de 1 unidade Standard</td>
<td>Sim, em incrementos de 1 unidade Premium</td>
</tr>
<tr>
<td><strong>Aumento horizontal máximo permitido</strong></td>
<td>Sem Dimensionamento</td>
<td>Sem Dimensionamento</td>
<td>Unidades de too8</td>
<td>Unidades de too8</td>
<td>Unidades de too8</td>
</tr>
<tr>
<td><strong>Pontes EAI por unidade</strong></td>
<td>Não incluída</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
Inclui contratos TPM</td>
<td>Não incluído</td>
<td>Incluído. 10 contratos por unidade.</td>
<td>Incluído. 50 contratos por unidade.</td>
<td>Incluído. 250 contratos por unidade.</td>
<td>Incluído. 1000 contratos por unidade.</td>
</tr>
<tr>
<td><strong>Ligações Híbridas por unidade</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Transferência de Dados (GB) das Ligações Híbridas por Unidade</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>Sistemas LOB do tooon local de ligações do BizTalk Adapter Service</strong></td>
<td>Não incluída</td>
<td>1 ligação</td>
<td>2 ligações</td>
<td>5 ligações</td>
<td>25 ligações</td>
</tr>
<tr>
<td align="left"><strong>Sistemas/protocolos suportados:</strong>
<ul>
<li>HTTP</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Service Bus (SB)</li>
<li>Blob do Azure</li>
<li>APIs REST</li>
</ul>
</td>
<td>Não incluídos</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
</tr>
<tr>
<td><strong>Elevada disponibilidade</strong>
<br/><br/>
Para o Contrato de Nível de Serviço (SLA), veja <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Preços dos BizTalk Services do Azure</a>.
</td>
<td>Não incluída</td>
<td>Não incluída</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
</tr>
<tr>
<td><strong>Backup e restauro</strong></td>
<td>Não incluída</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
</tr>
<tr>
<td><strong>Controlo</strong></td>
<td>Não incluída</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
</tr>
<tr>
<td><strong>Arquivo</strong><br/><br/>
Inclui a Não Rejeição de Receção (NRR) e a transferência de mensagens controladas</td>
<td>Não incluída</td>
<td>Incluído</td>
<td>Não Incluído</td>
<td>Não Incluído</td>
<td>Incluído</td>
</tr>
<tr>
<td><strong>Utilização de código personalizado</strong></td>
<td>Não incluída</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
</tr>
<tr>
<td><strong>Utilização de transformações, incluindo XSLT personalizado</strong></td>
<td>Não incluída</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
<td>Incluído</td>
</tr>
</table>

> [!NOTE]
> Para resiliência contra falhas de hardware, a Elevada Disponibilidade implica ter várias VMs dentro de uma única Unidade BizTalk.
> 
> 

## <a name="faqs"></a>FAQs
#### <a name="what-is-a-biztalk-unit"></a>O que é uma unidade BizTalk?
Uma "unidade" é o nível atómico de Olá de uma implementação de BizTalk Services do Azure. Cada edição é fornecida com uma unidade com capacidade de computação e memória diferente. Por exemplo, uma unidade Básica tem mais computação do que uma unidade Programador, uma unidade Standard tem mais computação do que uma unidade Básica, e assim sucessivamente. Quando dimensiona um BizTalk Service, está a dimensionar em termos de unidades.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Qual é Olá diferença entre os BizTalk Services e a VM do BizTalk do Azure?
Os BizTalk Services fornecem uma arquitetura plataforma-como-um-serviço (PaaS) verdadeira para criar soluções de integração na nuvem de Olá. Com o modelo do Olá PaaS, foca-se completamente na lógica da aplicação Olá e deixe todas Olá tooMicrosoft de gestão de infraestrutura, incluindo:

* Não é necessário toomanage ou patch máquinas virtuais.
* A Microsoft garante a disponibilidade.
* Pode controlar o dimensionamento a pedido, solicitando mais ou menos capacidade através de Olá portal do Azure.

Em Virtual Machines do Azure, o BizTalk Server fornece uma arquitetura Infraestrutura-como-um-Serviço (IaaS). Criar máquinas virtuais e configurá-las exatamente como o seu ambiente no local, tornando mais fácil toorun aplicações na nuvem de Olá sem alterações de código. Com a IaaS, são ainda responsável pela configuração de máquinas virtuais Olá, gestão de máquinas de virtuais Olá (por exemplo, a instalação do software e a patches no SO) e arquitetura da aplicação Olá para elevada disponibilidade.

Se pretender criar novas soluções de integração para minimizar o esforço de gestão da infraestrutura, utilize os BizTalk Services. Se estiver à procura tooquickly migre as suas soluções BizTalk existentes ou à procura de um ambiente a pedido toodevelop e teste BizTalk Server para aplicações, utilize BizTalk Server para uma Máquina Virtual no Azure.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>O que é a diferença de Olá entre o BizTalk Adapter Service e as ligações híbridas?
Olá BizTalk Adapter Service é utilizado por um BizTalk Service do Azure. Olá BizTalk Adapter Service utiliza o sistema de linha de negócio (LOB) do Olá BizTalk Adapter Pack tooconnect tooan no local. Uma ligação híbrida permite tooconnect uma forma fácil e convenientemente aplicações do Azure, como Olá funcionalidade de Web Apps no App Service do Azure e o Mobile Services do Azure, tooan no local recursos.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>O que significa “Transferência de Dados (GB) das Ligações Híbridas por unidade”? Significa por minuto/hora/dia/semana/mês? O que acontece quando é atingido o limite de Olá?
Olá custo das ligações híbridas por unidade depende da edição do Olá dos BizTalk Services. Resumindo, os custos dependem do volume de dados que transfere. Por exemplo, a transferência de 10 GB de dados por dia tem um custo inferior à transferência de 100 GB diários. Olá utilize [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/?scenario=full) para os custos do BizTalk Services toodetermine específicos. Normalmente, Olá limites são impostos diariamente. Se exceder o limite de Olá, qualquer excesso será cobrado à taxa de Olá de $1 por GB.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>Quando crio um contrato nos BizTalk Services, por que motivo número Olá de pontes aceda cópias de segurança de dois em dois em vez de apenas um?
Cada contrato inclui duas pontes diferentes: uma ponte de comunicação no lado do envio e uma ponte de comunicação no lado da receção.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>O que acontece quando atinjo o limite de quota Olá Olá diversas pontes ou contratos?
São toodeploy não é possível pontes novas ou criar novos contratos. toodeploy mais, terá de tooscale toomore unidades do serviço de BizTalk Olá ou tooa de atualização de edição superior.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>Como migrar de um escalão dos BizTalk Services tooanother?
edição gratuita Olá não pode ser migrada ou 'expandidos' tooanother camada e não pode ser uma cópia de segurança e restaurar tooanother camada. Se precisar de outro escalão, crie um novo BizTalk Service com a camada Olá de novo. Todos os artefactos criados com a edição gratuita Olá, incluindo ligações híbridas, toobe necessidade recriada no Olá novo BizTalk Service. 

Para as restantes edições Olá, utilize Olá cópia de segurança e restauro para migrar os seus artefactos de um escalão tooanother. Por exemplo, cópia de segurança dos seus artefactos no escalão Standard Olá e, em seguida, restaurá-las a camada de Premium toohello. [BizTalk Services: Cópia de segurança e restaurar](biztalk-backup-restore.md) descreve os caminhos de migração de Olá suportado e lista os artefactos são uma cópia de segurança. Tenha em atenção que não são feitas cópias de segurança de Ligações Híbridas. Após a cópia de segurança e restaurar tooa novo escalão, em seguida, recriar as ligações híbridas de Olá.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Olá BizTalk Adapter Service está incluído no serviço de Olá? Como recebo o software de Olá?
Sim, estão incluídos no Olá SDK dos BizTalk Services do Azure Olá BizTalk Adapter Service com Olá BizTalk Adapter Pack [transferir](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Passos seguintes
BizTalk Services do Azure toocreate no hello do Azure, aceda demasiado[BizTalk Services: aprovisionamento com Olá portal do Azure](biztalk-provision-services.md). toostart criar aplicações, acedas demasiado[BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Recursos adicionais
* [BizTalk Services: Aprovisionamento com Olá portal do Azure](biztalk-provision-services.md)<br/>
* [Serviços BizTalk: Gráfico de Estado de Aprovisionamento](biztalk-service-state-chart.md)<br/>
* [Serviços BizTalk: Separadores Dashboard, Monitorizar e Dimensionar](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [Serviços BizTalk: Cópia de segurança e Restauro](biztalk-backup-restore.md)<br/>
* [Serviços BizTalk: limitação](biztalk-throttling-thresholds.md)<br/>
* [Serviços BizTalk: Nome e Chave do Emissor](biztalk-issuer-name-issuer-key.md)<br/>
* [Como posso começar a utilizar Olá SDK dos BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

