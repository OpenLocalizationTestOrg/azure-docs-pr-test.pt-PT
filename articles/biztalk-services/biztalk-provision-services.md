---
title: "aaaCreate BizTalk Services do Azure no portal do Azure de Olá | Microsoft Docs"
description: "Saiba como tooprovision ou criar os BizTalk Services do Azure no portal do Azure; de Olá MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Criar os BizTalk Services utilizando Olá portal do Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign no toohello portal do Azure, precisará de uma conta do Azure e subscrição do Azure. Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Veja [Avaliação Gratuita do Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Criar um Serviço BizTalk
Dependendo da edição que escolher Olá, nem todas as definições do BizTalk Service poderão estar disponíveis.

1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. No painel de navegação inferior de Olá, selecione **novo**:  
   ![Selecione o botão novo Olá][NEWButton]
3. Selecione **SERVIÇOS APLICACIONAIS** > **BIZTALK SERVICE** > **CRIAÇÃO PERSONALIZADA**:  
   ![Selecionar Serviço BizTalk e Criação Personalizada][NewBizTalkService]
4. Introduza as definições do BizTalk Service Olá:
   
    <table border="1">
    <tr>
    <td><strong>Nome do Serviço BizTalk</strong></td>
    <td>Pode introduzir qualquer nome específico. Alguns exemplos incluem:<br/><br/>
    <em>minhaempresa</em>.biztalk.windows.net<br/>
    <em>minhaaplicaçãominhaempresa</em>.biztalk.windows.net<br/>
    <em>minhaaplicação</em>.biztalk.windows.net<br/><br/>". w" é automaticamente adicionado toohello nome que introduzir. Esta ação cria um URL que é utilizado tooaccess seu BizTalk Service, como <strong>https://<em>MinhaAplicação</em>. w</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Edição</strong></td>
    <td>Se estiver na fase de teste/desenvolvimento Olá, escolha <strong>programador</strong>. Se estiver na fase de produção Olá, utilize Olá <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: gráfico de edições</a> toodetermine se <strong>Premium</strong>, <strong>padrão</strong>, ou <strong>Basic</strong>Olá escolha correto para o seu cenário de negócio.
    </td>
    </tr>
    <tr>
    <td><strong>Região</strong></td>
    <td>Selecione Olá região geográfica toohost seu BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>URL do domínio</strong></td>
    <td><strong>Opcional</strong>. Por predefinição, o URL do domínio Olá é <em>Nomedobiztalkservice</em>. w. Também pode introduzir um domínio personalizado. Por exemplo, se o seu domínio for <em>contoso</em>, pode introduzir: <br/><br/>
    <em>MinhaEmpresa</em>.contoso.com<br/>
    <em>MinhaAplicaçãoMinhaEmpresa</em>.contoso.com<br/>
    <em>MinhaAplicação</em>.contoso.com<br/>
    <em>NomeDoBizTalkService</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Selecione a seta seguinte Olá.
5. Introduza Olá armazenamento e as definições de base de dados:  <table border="1">
    <tr>
    <td><strong>Conta de armazenamento de monitorização/arquivo</strong></td>
    <td>Selecione uma conta de armazenamento existente ou crie uma nova. <br/><br/>Se criar uma nova conta de armazenamento, introduza Olá <strong>nome da conta de armazenamento</strong>.</td>
    </tr>
    <tr>
    <td><strong>Base de dados de controlo</strong></td>
    <td>Se utilizar uma SQL Database do Azure existente, esta não poderá ser utilizada por mais nenhum BizTalk Service. Terá de nome de início de sessão de Olá e a palavra-passe introduzida quando esse servidor de base de dados SQL do Azure foi criado.<br/><br/><strong>Sugestão</strong> criar base de dados de controlo de Olá e conta de armazenamento de monitorização/arquivo na Olá mesma região como Olá BizTalk Service.</td>
    </tr>
    </table>
Selecione a seta seguinte Olá.
6. Introduza as definições de base de dados de Olá:  <table border="1">
    <tr>
    <td><strong>Nome</strong></td>
    <td>Disponível quando <strong>criar uma nova instância de base de dados SQL</strong> está selecionado no ecrã anterior Olá.
    <br/><br/>
Introduza um toobe de nome de base de dados SQL utilizada pelo BizTalk Service.</td>
    </tr>
    <tr>
    <td><strong>Servidor</strong></td>
    <td>Disponível quando <strong>criar uma nova instância de base de dados SQL</strong> está selecionado no ecrã anterior Olá.
    <br/><br/>
Selecione um servidor da SQL Database existente ou crie um novo.</td>
    </tr>
    <tr>
    <td><strong>Nome de início de sessão do servidor</strong></td>
    <td>Introduza o nome de utilizador de início de sessão de Olá.</td>
    </tr>
    <tr>
    <td><strong>Palavra-passe de início de sessão do servidor</strong></td>
    <td>Introduza a palavra-passe de início de sessão de Olá.</td>
    </tr>
    <tr>
    <td><strong>Região</strong></td>
    <td>Disponível quando selecionar <strong>Criar uma nova instância da Base de dados SQL</strong>. Selecione Olá região geográfica toohost a base de dados do SQL Server.</td>
    </tr>
    </table>

Selecione o Assistente de Olá toocomplete do Olá marca de verificação. ícone de progresso Olá é apresentado:  
![O ícone de progresso é apresentado aquando da conclusão][ProgressComplete]

Quando terminar, Olá BizTalk Service do Azure é criado e estará pronto para as suas aplicações. predefinições de Olá são suficientes. Se pretender que as definições predefinidas da toochange Olá, selecione **BIZTALK SERVICES** no Olá painel de navegação esquerdo e, em seguida, selecione o seu BizTalk Service. Definições adicionais são apresentadas no Olá [separadores Dashboard, monitorização e dimensionamento](biztalk-dashboard-monitor-scale-tabs.md) na parte superior do Olá.

Dependendo do Estado Olá de Olá BizTalk Service, existem algumas operações que não não possível concluir. Para obter uma lista destas operações, visite demasiado[BizTalk Services gráfico de estado](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Passos pós-aprovisionamento
* [Instalar o certificado de Olá num computador local](#InstallCert)
* [Adicionar um certificado pronto para produção](#AddCert)
* [Obter o espaço de nomes de controlo de acesso de Olá](#ACS)

#### <a name="InstallCert"></a>Instalar o certificado de Olá num computador local
Como parte do aprovisionamento do BizTalk Service, é criado um certificado autoassinado e associado à sua subscrição do BizTalk Service. Tem de transferir este certificado e instalá-lo em computadores a partir de onde se implementar aplicações do BizTalk Service ou enviar mensagens tooa ponto final do BizTalk Service.

1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecione **BIZTALK SERVICES** no Olá painel de navegação esquerdo e, em seguida, selecione a subscrição do BizTalk Service.
3. Selecione Olá **Dashboard** separador.
4. Selecione **Transferir Certificado SSL**:  
   ![Modificar o Certificado SSL][QuickGlance]
5. Faça duplo clique Olá certificado e executar através de certificado do Olá assistente tooinstall Olá. Certifique-se instalar o certificado de Olá em Olá **autoridades de certificação de raiz fidedigna** armazenar.

#### <a name="AddCert"></a>Adicionar um certificado pronto para produção
Olá certificado autoassinado criado automaticamente quando criar os BizTalk Services destina-se em só a ambientes de desenvolvimento. Para cenários de produção, substitua-o pelo certificado pronto para produção.

1. No Olá **Dashboard** separador, selecione **atualizar certificado SSL**.
2. Procurar o certificado SSL privado tooyour (*CertificateName*. pfx) que inclui o nome do seu BizTalk Service, introduza a palavra-passe de Olá e, em seguida, clique em marca de verificação Olá.

#### <a name="ACS"></a>Obter o espaço de nomes de controlo de acesso de Olá
1. Inicie sessão no toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecione **BIZTALK SERVICES** no Olá painel de navegação esquerdo e, em seguida, selecione o seu BizTalk Service.
3. Na barra de tarefas Olá, selecione **informações de ligação**:  
   ![Selecionar Informações de Ligação][ACSConnectInfo]
4. Copie os valores do controlo de acesso de Olá.

Quando implementa um projeto dos BizTalk Services a partir do Visual Studio, introduza este espaço de nomes do Controlo de Acesso. espaço de nomes de controlo de acesso de Olá é criado automaticamente para o seu BizTalk Service.

os valores do controlo de acesso de Olá podem ser utilizados com qualquer aplicação. Quando é criado BizTalk Services do Azure, este espaço de nomes do controlo de acesso controla a autenticação de Olá à sua implementação do BizTalk Service. Selecione se pretende a subscrição de Olá toochange ou gerir o espaço de nomes de Olá, **do Active Directory** no Olá painel de navegação esquerdo e, em seguida, selecione o espaço de nomes. barra de tarefas Olá lista as suas opções.

Ao clicar em **gerir** abre Olá Portal de gestão do controlo de acesso. No Portal de gestão do controlo de acesso Olá, Olá BizTalk Service utiliza **identidades do serviço**:  
![Identidades do serviço de ACS no Olá Portal de gestão do controlo de acesso][ACSServiceIdentities]

Olá identidade de serviço de controlo de acesso é um conjunto de credenciais que permitem a aplicações ou tooauthenticate clientes diretamente com o controlo de acesso e receber um token.

> [!IMPORTANT]
> Olá BizTalk Service utiliza **proprietário** para uma identidade de serviço predefinido Olá e Olá **palavra-passe** valor. Se utilizar o valor de chave simétrica Olá em vez de Olá valor de palavra-passe, hello erro seguinte pode ocorrer.<br/><br/>*Não foi possível ligar a conta de serviço de gestão do controlo de acesso de toohello com Olá especificada credenciais*
> 
> 

Em [Gerir o Espaço de Nomes do ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx), pode ver uma lista de algumas diretrizes e recomendações.

## <a name="requirements-explained"></a>Requisitos explicados
Estes requisitos não se aplicam toohello edição gratuita.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Do que precisa</strong></td>
        <td><strong>Porque precisa</strong></td>
</tr>
<tr>
<td>Subscrição do Azure</td>
<td>subscrição de Olá determina quem pode iniciar sessão no toohello portal do Azure. o marcador de posição do Olá conta cria a subscrição de Olá em <a HREF="https://account.windowsazure.com/Subscriptions"> subscrições do Azure</a>.
<br/><br/>
Olá conta do Azure pode ter várias subscrições e pode ser gerida por qualquer pessoa autorizada. Por exemplo, o titular da conta do Azure cria uma subscrição designada <em>BizTalkServiceSubscription</em> e fornecem Olá administradores do BizTalk dentro da empresa (por exemplo, ContosoBTSAdmins@live.com) aceder à subscrição toothis. Neste cenário, os administradores do BizTalk Olá inicie sessão toohello portal do Azure e ter completos serviços do administrador direitos tooall Olá alojado na subscrição Olá, incluindo os BizTalk Services do Azure. Administradores do BizTalk Olá não são proprietários da conta do Azure de Olá, pelo que não tem acesso tooany as informações de faturação.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gerir subscrições e contas de armazenamento no portal do Azure de Olá</a> fornece mais informações.
</td>
</tr>
<tr>
<td>Base de Dados SQL do Azure</td>
<td>Armazena Olá tabelas, vistas e os procedimentos armazenados utilizados pelo BizTalk Service, incluindo dados de controlo de Olá de Olá.
<br/><br/>
Quando cria um BizTalk Service, pode utilizar um Servidor SQL do Azure existente, uma SQL Database do Azure ou criar automaticamente um novo servidor ou base de dados.
<br/><br/>
Olá escala de base de dados SQL é automaticamente configurado. Normalmente, dimensionamento do Olá predefinido é suficiente para um BizTalk Service. Escala de Olá alteração terá impactos nos preços. Veja <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Contas e Faturação na Base de Dados SQL do Azure</a>
<br/><br/>
<strong>Notas</strong>
<br/>
<ul>
<li> Quando cria uma nova Base de Dados e um novo Servidor SQL do Azure, os Serviços do Azure são automaticamente ativados. Olá BizTalk Service requer os serviços do Azure ativada.</li>
<li>Se criar uma nova base de dados do Azure SQL Server num servidor SQL do Azure existente, Olá regras de firewall de Olá Server não são alterados. Como resultado, é possível a que outros serviços do Azure não são permitidos bases de dados do servidor de acesso toohello.</li>
</ul>
</td>
</tr>
<tr>
<td>Espaço de nomes do Controlo de Acesso do Azure</td>
<td>É autenticado com o BizTalk Services do Azure. Quando implementa um projeto dos BizTalk Services a partir do Visual Studio, introduza este espaço de nomes do Controlo de Acesso. Quando cria um BizTalk Service, o espaço de nomes de controlo de acesso de Olá é criado automaticamente.</td>
</tr>

<tr>
<td>Conta de armazenamento do Azure</td>
<td>Fornecem acesso tootables, blobs e filas utilizados pelo seu seguinte do BizTalk Service toosave Olá:

<ul>
<li>Os ficheiros de registo Olá esse monitor BizTalk Service. Olá monitorização saída também é apresentada no Olá **monitorização** separador Olá portal do Azure.</li>
<li>Ao criar um contrato X12 ou AS2 entre parceiros, pode ativar Olá arquivo funcionalidade toostore as propriedades da mensagem. Estes dados são guardados no Olá conta de armazenamento.</li>
</ul>
<br/>
Quando cria um BizTalk Service, pode utilizar uma Conta de armazenamento existente ou criar automaticamente uma nova.
<br/><br/>
as definições de armazenamento de predefinido Olá são suficientes para um BizTalk Service.
<br/><br/>
Quando cria uma Conta de armazenamento, são criadas automaticamente uma Chave Primária e uma Chave Secundária. Estas chaves controlam o acesso tooyour conta de armazenamento. Olá BizTalk Service utiliza automaticamente Olá chave primária.
<br/><br/>
Para obter mais informações, veja <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Armazenamento</a>.
</td>
</tr>

<tr>
<td>Certificado SSL privado</td>
<td>
Quando cria um BizTalk Service do Azure, também é criado um URL HTTPS com o nome do seu BizTalk Service. Este URL é configurada automaticamente toouse um certificado autoassinado do apenas de desenvolvimento. Para a produção, precisa de um certificado SSL privado.
<br/><br/>
<strong>Informações importantes sobre o Certificado SSL</strong>

<ul>
<li>data de expiração do certificado Olá tem de ser inferior a cinco anos.</li>
<li>Todos os certificados privados requerem uma palavra-passe. Lembre-se desta palavra-passe e, como uma melhor prática, partilhe-a com os seus administradores.</li>
<li>Os certificados autoassinados são utilizados num ambiente de teste/desenvolvimento. Quando utilizar certificados autoassinados, importe o arquivo de certificados pessoais do Olá certificados tooyour e Olá arquivo de certificados de autoridades de certificação de raiz fidedigna.</li>
</ul>
<br/>Quando for enviada a autoridade de certificação de tooyour certificado pedido Olá produção, dê Olá seguintes propriedades do certificado:
<br/>

<ul>
<li><strong>Utilização de Chave Avançada</strong>: no mínimo, os Serviços BizTalk do Azure requerem a Autenticação do Servidor.</li>
<li><strong>Nome comum</strong>: introduza o nome de domínio completamente qualificado (FQDN) Olá do seu URL de serviço BizTalk do Azure. Veja <a HREF="#CreateService">Criar um BizTalk Service</a> neste artigo.</li>
</ul>
<br/>
Um certificado novo ou diferentes pode ser adicionado depois da criação Olá BizTalk Service.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>Ligações Híbridas
Quando cria um BizTalk Service do Azure, Olá **ligações híbridas** separador está disponível:

![Separador Ligações Híbridas][HybridConnectionTab]

As ligações híbridas são utilizada tooconnect um Azure site ou serviço móvel do Azure tooany no local recursos que utiliza uma porta TCP estática, como o SQL Server, MySQL, APIs da Web HTTP, os Mobile Services e a maioria dos serviços Web personalizados.  As ligações híbridas e Olá BizTalk Adapter Service são diferentes. Olá BizTalk Adapter Service é o sistema de linha de negócio (LOB) do tooconnect utilizados BizTalk Services do Azure tooan no local.

 Consulte [ligações híbridas](integration-hybrid-connection-overview.md) toolearn mais, incluindo criar e gerir ligações híbridas.

## <a name="next-steps"></a>Passos seguintes
Agora que é criado um BizTalk Service, familiarize-se com Olá diferentes [BizTalk Services: separadores Dashboard, monitorização e dimensionamento](biztalk-dashboard-monitor-scale-tabs.md). O BizTalk Service está pronto para as suas aplicações. toostart criar aplicações, acedas demasiado[BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Consultar também
* [Serviços BizTalk: Gráfico de Edições](biztalk-editions-feature-chart.md)<br/>
* [Serviços BizTalk: Gráfico de Estado](biztalk-service-state-chart.md)<br/>
* [Serviços BizTalk: Cópia de segurança e Restauro](biztalk-backup-restore.md)<br/>
* [Serviços BizTalk: limitação](biztalk-throttling-thresholds.md)<br/>
* [Serviços BizTalk: Nome e Chave do Emissor](biztalk-issuer-name-issuer-key.md)<br/>
* [Como posso começar a utilizar Olá SDK dos BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Ligações Híbridas](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
