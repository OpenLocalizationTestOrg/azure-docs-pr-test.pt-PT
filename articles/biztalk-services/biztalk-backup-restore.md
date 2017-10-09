---
title: "aaaCreate e restaurar uma cópia de segurança nos BizTalk Services | Microsoft Docs"
description: "BizTalk Services inclui a cópia de segurança e restauro. Saiba como toocreate e restaurar uma cópia de segurança e determinar o que obtém uma cópia de segurança. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>BizTalk Services: Cópia de segurança e Restauro

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

BizTalk Services do Azure inclui capacidades de cópia de segurança e restauro. Este tópico descreve como toobackup e restauro dos BizTalk Services utilizando Olá portal clássico do Azure.

Também pode criar uma cópia dos BizTalk Services utilizando Olá [API de REST do BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=325584). 

> [!NOTE]
> As ligações híbridas não são guardados em cópia de segurança, independentemente da edição de Olá. Tem de recriar as ligações híbridas.


## <a name="before-you-begin"></a>Antes de começar
* Cópia de segurança e restauro poderão não estar disponíveis em todas as edições. Consulte [dos BizTalk Services: gráfico de edições](biztalk-editions-feature-chart.md).
* Utilizar Olá portal clássico do Azure, pode criar uma cópia de segurança a pedido ou criar uma cópia de segurança agendada. 
* Conteúdo de cópia de segurança pode ser restaurada toohello mesmo serviço BizTalk ou tooa novo BizTalk Service. toorestore Olá BizTalk Service com o mesmo nome, Olá existente BizTalk Service têm de ser eliminado de Olá e nome de Olá tem de estar disponível. Depois de eliminar um BizTalk Service, pode demorar mais tempo do que pretendia para Olá o mesmo nome toobe disponível. Se não puder aguardar Olá mesmo nome toobe disponível, em seguida, restaure tooa novo BizTalk Service.
* BizTalk Services pode ser restaurada toohello mesma edição ou uma edição superior. Restaurar os BizTalk Services tooa edição inferior, de quando foi feita a cópia de segurança de Olá, não é suportada.
  
    Por exemplo, uma cópia de segurança utilizando Olá que edição básica pode ser restaurada toohello edição Premium. Uma cópia de segurança utilizando Olá que Premium Edition não pode ser restaurada toohello Standard Edition.
* números de controlo de EDI Olá são cópias de segurança toomaintain continuidade de números de controlo de Olá. Se as mensagens são processadas após a última cópia de segurança Olá, este conteúdo de cópia de segurança a restaurar pode fazer com que os números de controlo duplicado.
* Se um lote tem mensagens Active Directory, processo de batch de Olá **antes** executar uma cópia de segurança. Ao criar uma cópia de segurança (como necessários ou agendada), as mensagens em lotes nunca são armazenadas. 
  
    **Se uma cópia de segurança foi efetuada com o Active Directory mensagens num batch, estas mensagens não são cópia de segurança e, por conseguinte, foram perdidas.**
* Opcional: No Portal de serviços de BizTalk Olá, pare a quaisquer operações de gestão.

## <a name="create-a-backup"></a>Criar uma cópia de segurança
Uma cópia de segurança pode ser executada em qualquer altura e é totalmente controlada por si. Esta secção lista Olá passos toocreate cópias de segurança utilizando Olá clássico do Azure portal, incluindo:

[Numa cópia de segurança a pedido](#backupnow)

[Agendar uma cópia de segurança](#backupschedule)

#### <a name="backupnow"></a>Numa cópia de segurança a pedido
1. No portal clássico do Azure Olá, selecione **BizTalk Services**, e, em seguida, selecione Olá pretende toobackup do BizTalk Service.
2. No Olá **Dashboard** separador, selecione **cópia de segurança** em Olá parte inferior da página Olá.
3. Introduza um nome de cópia de segurança. Por exemplo, introduza *myBizTalkService*BU*data*.
4. Escolha uma conta do blob storage e a cópia de segurança do Olá selecione marca de verificação toostart Olá.

Uma vez concluída a cópia de segurança de Olá, é criado um contentor com o nome de cópia de segurança Olá que introduzir na conta do storage Olá. Este contentor contém a configuração de cópia de segurança do BizTalk Service.

#### <a name="backupschedule"></a>Agendar uma cópia de segurança
1. No portal clássico do Azure Olá, selecione **BizTalk Services**, selecione Olá nome do BizTalk Service pretende cópia de segurança do tooschedule Olá e, em seguida, selecione Olá **configurar** separador.
2. Conjunto Olá **estado de cópia de segurança** demasiado**automática**. 
3. Selecione Olá **conta de armazenamento** toostore Olá cópia de segurança, introduza Olá **frequência** toocreate Olá cópias de segurança, cópias de segurança e quanto tookeep Olá (**retenção dias**):
   
    ![][AutomaticBU]
   
    **Notas**     
   
   * No **retenção dias**, o período de retenção de Olá tem de ser superior à frequência de cópia de segurança de Olá.
   * Selecione **mantenha sempre, pelo menos, uma cópia de segurança**, mesmo se for passado Olá período de retenção.
4. Selecione **Guardar**.

Quando uma tarefa de cópia de segurança agendada é executada, cria um contentor (dados de cópia de segurança toostore) na conta do storage Olá que introduziu. nome de Olá do contentor de Olá é denominado *nome-data / hora de BizTalk Service*. 

Se Olá dashboard do BizTalk Service mostra um **falha** Estado:

![Último Estado de cópia de segurança agendado][BackupStatus] 

ligação de Olá abre Olá registos de operação de serviços de gestão toohelp resolver problemas. Consulte [BizTalk Services: resolver problemas com os registos de operações](http://go.microsoft.com/fwlink/p/?LinkId=391211).

## <a name="restore"></a>Restauro
Pode restaurar cópias de segurança de Olá portal clássico do Azure ou de Olá [API REST do serviço BizTalk restaurar](http://go.microsoft.com/fwlink/p/?LinkID=325582). Esta secção lista Olá passos toorestore através do portal clássico Olá.

#### <a name="before-restoring-a-backup"></a>Antes de restaurar uma cópia de segurança
* Novo controlo, arquivar e arquivos de monitorização, podem ser introduzidos ao restaurar um BizTalk Service.
* Olá mesmo EDI Runtime serem restaurados. cópia de segurança do Olá EDI Runtime armazena os números de controlo de Olá. os números de controlo de Olá restaurada estão na sequência do momento de Olá da cópia de segurança de Olá. Se as mensagens são processadas após a última cópia de segurança Olá, este conteúdo de cópia de segurança a restaurar pode fazer com que os números de controlo duplicado.

#### <a name="restore-a-backup"></a>Restaurar uma cópia de segurança
1. No portal clássico do Azure Olá, selecione **novo** > **serviços aplicacionais** > **BizTalk Service** > **restaurar** :
   
    ![Restaurar uma cópia de segurança][Restore]
2. No **URL de cópia de segurança**, selecione o ícone da pasta Olá e expanda a conta de armazenamento do Azure Olá que arquivos Olá cópia de segurança de configuração de BizTalk Service. Expanda o contentor de Olá e no painel direito Olá, selecione Olá correspondente a cópia de segurança ficheiro. txt. 
   <br/><br/>
   Selecione **abra**.
3. No Olá **restaurar o BizTalk Service** página, introduza um **nome do BizTalk Service** e certifique-se Olá **URL do domínio**, **edição**e **Região** para Olá restaurada BizTalk Service. **Criar uma nova instância de base de dados do SQL Server** para Olá da base de dados de controlo:
   
    ![][RestoreBizTalkService]
   
    Selecione a seta seguinte Olá.
4. Verifique o nome de Olá da base de dados SQL de Olá, introduza o servidor físico olá onde será criada a base de dados SQL de Olá e uma nome de utilizador/palavra-passe para esse servidor.

    Se pretender que a edição de base de dados SQL do tooconfigure Olá, tamanho e outras propriedades, selecione **configurar definições avançadas da base de dados**. 

    Selecione a seta seguinte Olá.

1. Criar uma nova conta de armazenamento ou introduza uma conta de armazenamento existente para Olá BizTalk Service.
2. Selecione o restauro de Olá toostart do Olá marca de verificação.

Depois do restauro de Olá concluir com êxito, um novo serviço BizTalk é listado num estado suspenso na página de BizTalk Services Olá na Olá portal clássico do Azure.

### <a name="postrestore"></a>Depois de restaurar uma cópia de segurança
Olá BizTalk Service está sempre restaurada num **suspenso** estado. Neste estado, pode efetuar alterações de configuração antes do novo ambiente do Olá está funcional, incluindo:

* Se tiver criado Olá SDK dos BizTalk Services do Azure a utilizar aplicações do BizTalk Service, terá as credenciais de controlo de acesso (ACS) de Olá tootooupdate no toowork aplicações com o ambiente de Olá restaurada.
* Restaurar tooreplicate um BizTalk Service num ambiente existente do BizTalk Service. Nesta situação, se existirem contratos configurados no portal de BizTalk Services original Olá que utilizam uma pasta de origem FTP, poderá ser necessário contratos de Olá tooupdate no Olá recentemente restaurado ambiente toouse uma pasta FTP de origem diferente. Caso contrário, poderão existir dois contratos diferentes tentar toopull Olá a mesma mensagem.
* Se os tiver restaurado toohave vários ambientes do BizTalk Service, certifique-se de que Olá correto ambiente Olá Visual Studio aplicações, os cmdlets do PowerShell, REST APIs ou APIs de OM de gestão de parceiros comerciais de destino.
* É uma boa prática tooconfigure automatizada as cópias de segurança ambiente de serviço BizTalk Olá recentemente restaurado.

toostart Olá BizTalk Service na Olá portal clássico do Azure, selecione de Olá restaurada BizTalk Service e selecione **retomar** na barra de tarefas Olá. 

## <a name="what-gets-backed-up"></a>O que obtém uma cópia de segurança
Quando é criada uma cópia de segurança, hello seguintes itens são uma cópia de segurança:

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>Itens de cópia de segurança</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Portal de serviços do BizTalk do Azure</strong></td>
</tr> 
<tr>
<td>Configuração e o tempo de execução</td> 
<td>
<ul>
<li>Detalhes de parceiros e perfil</li>
<li>Contratos de parceiros</li>
<li>Assemblagens personalizadas implementadas</li>
<li>Pontes implementado</li>
<li>Certificados</li>
<li>Transformações implementadas</li>
<li>Pipelines</li>
<li>Modelos criados e guardados no Olá Portal de serviços BizTalk</li>
<li>X12 mapeamentos ST01 e GS01</li>
<li>Números de controlo (EDI)</li>
<li>Valores de AS2 mensagem Dinâmicas</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Serviço BizTalk do Azure</strong></td>
</tr> 
<tr>
<td>Certificado SSL</td> 
<td>
<ul>
<li>Dados de certificado SSL</li>
<li>Palavra-passe de certificado SSL</li>
</ul>
</td>
</tr> 
<tr>
<td>Definições do BizTalk Service</td> 
<td>
<ul>
<li>Contagem de unidades de escala</li>
<li>Edição</li>
<li>Versão do produto</li>
<li>Região/Datacenter</li>
<li>Espaço de nomes de serviço de controlo (ACS) de acesso e a chave</li>
<li>Cadeia de ligação de base de dados de controlo</li>
<li>Cadeia de ligação de conta de armazenamento de arquivo</li>
<li>Cadeia de ligação de conta de armazenamento de monitorização</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>Itens adicionais</strong></td>
</tr> 
<tr>
<td>Base de dados de controlo</td> 
<td>Quando é criado Olá BizTalk Service, os detalhes da base de dados de controlo de Olá são introduzidos, incluindo Olá SQL Database do Azure e o nome de base de dados de controlo de Olá. Olá controlo a base de dados não é automaticamente uma cópia de segurança.
<br/><br/>
<strong>Importante</strong><br/>
Se Olá base de dados de controlo é eliminado e Olá necessidades de base de dados recuperadas, tem de existir uma cópia de segurança anterior. Se não existir uma cópia de segurança, Olá base de dados de controlo e os respetivos dados não são recuperáveis. Nesta situação, criar uma nova base de dados de controlo Olá com o mesmo nome de base de dados. Recomenda-se a Georreplicação.</td>
</tr> 
</table>

## <a name="next"></a>Seguinte
BizTalk Services do Azure toocreate no hello do Azure clássica, aceda demasiado[BizTalk Services: portal clássico do Azure de utilizar o aprovisionamento](http://go.microsoft.com/fwlink/p/?LinkID=302280). toostart criar aplicações, acedas demasiado[BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Veja Também
* [Serviço de cópia de segurança de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Restaurar o BizTalk Service a partir de cópia de segurança](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Os BizTalk Services: Programador, básicas, Standard e Premium gráfico de edições](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk Services: Portal clássico do Azure através de aprovisionamento](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Serviços BizTalk: Gráfico de Estado de Aprovisionamento](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Serviços BizTalk: Separadores Dashboard, Monitorizar e Dimensionar](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Serviços BizTalk: limitação](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Serviços BizTalk: Nome e Chave do Emissor](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Como posso começar a utilizar Olá SDK dos BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

