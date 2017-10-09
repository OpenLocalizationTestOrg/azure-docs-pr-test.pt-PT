---
title: aaaUsing do Azure para importar/exportar tootransfer dados tooand do armazenamento de BLOBs | Microsoft Docs
description: "Saiba como toocreate importar e exportar tarefas no portal do Azure para transferir dados tooand do armazenamento de BLOBs de Olá."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 0be486a4badf2127b4613f3e9664e4cd308d3298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Utilizar o armazenamento de Olá importação/exportação do Microsoft Azure service tootransfer dados tooblob
Olá serviço importar/exportar do Azure permite-lhe toosecurely transferem grandes quantidades de armazenamento de BLOBs de tooAzure dados pelo envio unidades de disco rígido tooan Datacenter do Azure. Também pode utilizar estes dados tootransfer do serviço de armazenamento de Blobs do Azure toohard unidades de disco e são enviados site no local de tooyour. Este serviço é adequado em situações em que pretende tootransfer vários terabytes (TB) de tooor de dados do Azure, mas o carregamento ou transferência de rede Olá infeasible devido toolimited largura de banda ou elevada os custos de rede.

serviço de Olá requer unidades de disco rígido deve BitLocker encriptado para segurança Olá dos seus dados. o serviço de Olá suporta tanto Olá clássica e do Azure Resource Manager contas de armazenamento (camada standard e esporádico) presentes em todas as regiões de Olá do Azure público. Tem a são enviados tooone de unidades de disco rígido de localizações de Olá suportada especificadas neste artigo.

Neste artigo, pode obter mais informações sobre como tooship unidades para copiar o tooand de dados do Blob storage do Azure e do serviço de importação/exportação do Azure Olá.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>Quando posso utilizar o serviço de importação/exportação do Azure Olá?
Considere utilizar o serviço importar/exportar do Azure ao carregar a transferência de dados através de rede de Olá está demasiado lenta, ou obter largura de banda de rede adicional é proibitivos em termos de custo.

Pode utilizar este serviço, tal como nos cenários:

* Migrar dados toohello na nuvem: mover rapidamente grandes quantidades de dados tooAzure e o custo de forma eficaz.
* Distribuição de conteúdo: rapidamente enviar dados tooyour sites de cliente.
* Cópia de segurança: Efetuar cópias de segurança da sua toostore de dados no local no armazenamento de Blobs do Azure.
* Recuperação de dados: recuperar grande quantidade de dados armazenados no blob storage e o tiver entregar a localização do tooyour no local.

## <a name="prerequisites"></a>Pré-requisitos
Nesta secção é uma lista Olá pré-requisitos necessários toouse este serviço. Reveja-los cuidadosamente antes de envio suas unidades.

### <a name="storage-account"></a>Conta de armazenamento
Tem de ter uma subscrição do Azure existente e um ou mais contas toouse Olá importar/exportar serviço de armazenamento. Cada tarefa pode ser utilizado tootransfer dados tooor de apenas uma conta de armazenamento. Por outras palavras, uma tarefa de importação/exportação único não pode abranger várias várias contas de armazenamento. Para obter informações sobre como criar uma nova conta de armazenamento, consulte [como tooCreate uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>Tipos de BLOBs
Pode utilizar dados do Azure para importar/exportar serviço toocopy demasiado**bloco** blobs ou **página** blobs. Por outro lado, só pode exportar **bloco** blobs, **página** blobs ou **acrescentar** blobs storage do Azure utilizar este serviço.

### <a name="job"></a>Tarefa
processo de Olá toobegin de importar tooor exportar a partir do Blob storage, tem primeiro de criar uma tarefa de. Uma tarefa pode ser uma tarefa de importação ou uma tarefa de exportação:

* Crie uma tarefa de importação quando pretender que os dados de tootransfer tiver tooblobs no local na sua conta do storage do Azure.
* Criar uma tarefa de exportação quando pretender que os dados de tootransfer atualmente armazenados como os blobs na sua unidades de toohard de conta de armazenamento que são fornecidos tooyou.s quando cria uma tarefa, notificá Olá para importar/exportar serviço que lhe irá enviar um ou mais difícil unidades tooan do Azure Centro de dados.

* Para uma tarefa de importação, será de envio unidades de disco rígido que contém os dados.
* Para uma tarefa de exportação, será de envio unidades de disco rígido em branco.
* Pode enviar a cópia de unidades de disco rígido too10 por tarefa.

Pode criar uma importação ou exportação tarefa utilizando Olá portal do Azure ou Olá [API de REST de importação/exportação do Azure Storage](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>Ferramenta de WAImportExport
Olá primeiro passo para criar um **importar** tarefa é tooprepare as unidades que serão enviadas para importação. tooprepare suas unidades, deve ligar tooa servidor local e execute Olá WAImportExport ferramenta no servidor local Olá. Esta ferramenta WAImportExport facilita a copiar a unidade de toohello de dados, encriptação de dados de Olá na unidade de Olá com o BitLocker e ficheiros do diário de unidade de Olá a gerar.

ficheiros do diário de alterações de Olá armazenam informações básicas sobre a tarefa e a unidade como o número de série da unidade e o nome da conta de armazenamento. Este ficheiro de diário de alterações não é armazenado na unidade de Olá. É utilizado durante a criação da tarefa de importação. Passo a passo detalhes sobre a criação da tarefa são fornecidas neste artigo.

ferramenta de WAImportExport Olá só é compatível com o sistema de operativo do Windows de 64 bits. Consulte Olá [sistema operativo](#operating-system) na secção versões específicas de SO suportada.

Transferir a versão mais recente do Olá do Olá [WAImportExport ferramenta](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Para obter mais detalhes sobre como utilizar hello WAImportExport ferramenta, consulte Olá [Using Olá WAImportExport ferramenta](storage-import-export-tool-how-to.md).

>[!NOTE]
>**A versão anterior:** pode [transferir WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) versão do Olá ferramenta e consulte demasiado[guia de utilização de WAImportExpot V1](storage-import-export-tool-how-to-v1.md). WAImportExpot V1 versão da ferramenta de Olá fornece suporte para **preparar discos quando são escritos dados já previamente no disco toohello**. Também terá de ferramenta toouse WAImportExpot V1 se Olá a chave apenas disponível é a chave SAS.

>

### <a name="hard-disk-drives"></a>Unidades de disco rígido
Apenas 2,5 polegada SSD ou 2,5" ou 3.5" SATA II ou HDD interno III são suportados para utilização com Olá serviço de importação/exportação. Uma tarefa de importação/exportação única pode ter um máximo de 10 HDD/SSD e HDD cada individuais/SSD pode ser de qualquer tamanho. Grande número de unidades de serem distribuído por várias tarefas e não existe nenhum limites no número de Olá de tarefas que podem ser criadas. 

Para tarefas de importação, apenas Olá primeiro volume de dados na unidade de Olá será processado. volume de dados de Olá deve ser formatado com NTFS.

> [!IMPORTANT]
> Unidades de disco rígido externas que vêm com um adaptador USB incorporado não são suportadas por este serviço. Além disso, o disco de Olá dentro de maiúsculas e minúsculas de Olá de um HDD externo não pode ser utilizado; Não envie HDDs externos.
> 
> 

Segue-se que uma lista de externos adaptors USB utilizado toocopy dados toointernal HDDs. Anker 68UPSATAA - 02BU Anker 68UPSHHDS BU Startech SATADOCK22UE Orico 6628SUS3-C-BK (6628 série) Thermaltake BlacX frequente troca SATA externo rígido unidade ancoragem estação (2.0 de USB & eSATA)

### <a name="encryption"></a>Encriptação
dados de Olá na unidade de Olá tem de ser encriptados utilizando a encriptação de unidade BitLocker. Esta ação protege os dados enquanto esta se encontra em trânsito.

Para tarefas de importação, existem dois encriptação de Olá de tooperform formas. Olá forma primeira é a opção de Olá de toospecify ao utilizar o ficheiro CSV de conjunto de dados ao executar a ferramenta de WAImportExport Olá durante a preparação de unidade. Olá forma segundo é tooenable a encriptação BitLocker manualmente na unidade de Olá e especifica chave de encriptação de Olá no Olá driveset CSV ao executar a linha de comandos de ferramenta WAImportExport durante a preparação de unidade.

Para as tarefas de exportação, depois dos dados copiados toohello unidades, serviço Olá encriptar unidade Olá utilizar o BitLocker antes de envio-back tooyou. chave de encriptação de Olá será fornecido tooyou através de Olá portal do Azure.  

### <a name="operating-system"></a>Sistema Operativo
Pode utilizar um dos Olá 64-bit sistemas operativos tooprepare Olá unidade de disco rígido utilizando Olá WAImportExport ferramenta antes do envio Olá unidade tooAzure os seguintes:

Windows 7 Enterprise, Ultimate do Windows 7, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Todos estes sistemas operativos suportam a encriptação de unidade BitLocker.

### <a name="locations"></a>Localizações
Olá serviço importar/exportar do Azure suporta a cópia de dados tooand entre todas as contas de armazenamento do Azure público. Pode enviar tooone de unidades de disco rígido de Olá seguintes localizações. Se a sua conta do storage está numa localização pública do Azure que não for especificada aqui, uma localização alternativa de envio será fornecida quando estiver a criar utilizando a tarefa Olá Olá portal do Azure ou Olá API de REST de importação/exportação.

Suportado envio localizações:

* EUA Leste
* EUA Oeste
* EUA Leste 2
* EUA Oeste 2
* EUA Central
* EUA Centro-Norte
* EUA Centro-Sul
* EUA Centro-Oeste
* Europa do Norte
* Europa Ocidental
* Ásia Oriental
* Sudeste Asiático
* Leste da Austrália
* Sudeste da Austrália
* Oeste do Japão
* Leste do Japão
* Índia Central
* Sul da Índia
* Índia Ocidental
* Canadá Central
* Leste do Canadá
* Sul do Brasil
* Coreia Central
* Gov (US) - Virginia
* Gov (US) - Iowa
* US DoD Leste
* US DoD Centro
* Leste da China
* China Norte
* Reino Unido Sul

### <a name="shipping"></a>Envio
**O envio de unidades toohello Centro de dados:**

Ao criar uma tarefa de importação ou exportação, irá ser fornecido que um endereço de envio de um dos Olá suportado localizações tooship suas unidades. Olá envio endereço fornecido dependerá da localização de Olá da sua conta de armazenamento, mas não pode ser Olá igual à sua localização da conta de armazenamento.

Pode utilizar os operadores como FedEx, DHL, UPS ou Olá nos serviço Postal tooship sua toohello unidades endereço de envio.

**Unidades de envio do Centro de dados de Olá:**

Ao criar uma tarefa de importação ou exportação, tem de fornecer um endereço do remetente para Microsoft toouse quando efetuar uma cópia envio Olá unidades depois de concluída a tarefa. Certifique-se que fornecer um endereço de retorno válido tooavoid atrasos no processamento.

Pode utilizar a operadora à sua escolha na ordem tooforward incorporadas Olá disco. operadora Olá deve ter o controlo apropriado na cadeia de toomaintain de ordem de custody. Tem também de fornecer uma operadora FedEx ou DHL válida toobe número conta utilizada pela Microsoft para unidades de Olá volta de envio. Um número de conta FedEx é necessário para envio unidades novamente a partir do Olá E.U.A. e localizações de Europa. Um número de conta DHL é necessário para unidades de envio anterior a partir de localizações Ásia e da Austrália. Pode criar um [FedEx](http://www.fedex.com/us/oadr/) (para E.U.A. e Europa) ou [DHL](http://www.dhl.com/) (Ásia e da Austrália) operadora a conta se não tiver um. Se já tiver um número de conta operadora, verifique se é válido.

No seus pacotes de envio, tem de seguir os termos de Olá em [termos de serviço do Microsoft Azure](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Tenha em atenção que Olá físico suporte de dados que são envio poderá ter limites internacional toocross. É responsável por assegurar que os dados e suportes de dados físicos são importados e/ou exportados de acordo com as leis aplicáveis Olá. Antes de envio suporte de dados físico Olá, verificar com o seu tooverify advisers os dados e suportes de dados legalmente podem ser fornecidos toohello identificado Centro de dados. Isto irá ajudar tooensure que atinge Microsoft atempadamente. Por exemplo, qualquer pacote que será entre limites internacionais tem um toobe fatura comerciais acompanhado com o pacote de Olá (exceto se cruzamento entre limites dentro da União Europeia). Pode imprimir uma cópia manchas fatura comercial de Olá do Web site da operadora. Exemplo de faturas comerciais são [fatura comerciais DHL](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) e [fatura comerciais FedEx](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Certifique-se de que a Microsoft tem não foi indicado como exportador Olá.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Como funciona o Olá serviço importar/exportar do Azure?
Pode transferir dados entre o site no local e o armazenamento de Blobs do Azure utilizando o serviço de importação/exportação do Azure Olá através da criação de tarefas e envio de unidades de disco rígido tooan Datacenter do Azure. Cada unidade de disco rígido que são enviados está associada uma única tarefa. Cada tarefa está associada uma única conta de armazenamento. Olá revisão [secção pré-requisitos](#pre-requisites) cuidadosamente toolearn sobre especificações Olá este tipos de BLOBs de serviço suportado, tais como, os tipos de disco, as localizações e envio.

Nesta secção descrevem num Olá de nível elevado os passos importar e exportar tarefas. Mais adiante Olá [secção início rápido](#quick-start), iremos fornecer instruções passo a passo toocreate uma importação e exportação tarefa.

### <a name="inside-an-import-job"></a>Dentro de uma tarefa de importação
Um nível elevado, uma tarefa de importação envolve Olá os seguintes passos:

* Determinar Olá dados toobe importado e, Olá número de unidades que precisa.
* Identifique Olá localização de blob de destino para os seus dados no Blob storage.
* Utilize Olá WAImportExport ferramenta toocopy tooone os dados ou mais unidades de disco rígido e encriptá-los com o BitLocker.
* Criar uma tarefa de importação na sua conta de armazenamento de destino utilizando Olá portal do Azure ou Olá API de REST de importação/exportação. Se utilizar o portal do Azure de Olá, carregar ficheiros do diário de unidade de Olá.
* Forneça o endereço do remetente Olá e operadora conta toobe número utilizado para envio Olá unidades back tooyou.
* Incorporadas toohello unidades de disco rígido Olá endereço fornecido durante a criação da tarefa de envio.
* Atualize a entrega de Olá controlo número nos detalhes de tarefa de importação de Olá e submeter a tarefa de importação de Olá.
* Unidades são recebidas e processadas no Centro de dados do Azure Olá.
* Unidades são fornecidas com o seu operadora conta toohello endereço do remetente fornecido na tarefa de importação de Olá.
  
    ![Figura 1:Import fluxo de trabalho](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>Dentro de uma tarefa de exportação
Um nível elevado, uma tarefa de exportação envolve Olá os seguintes passos:

* Determine Olá dados toobe exportado e Olá número de unidades que precisa.
* Identifique os blobs de origem Olá ou caminhos do contentor dos seus dados no Blob storage.
* Criar uma tarefa de exportação na sua conta de armazenamento de origem utilizando Olá portal do Azure ou Olá API de REST de importação/exportação.
* Especifique Olá blobs de origem ou tarefa de exportação de caminhos do contentor dos seus dados no Olá.
* Forneça Olá retorno endereço e operadora número da conta para toobe utilizado para envio Olá unidades back tooyou.
* Incorporadas toohello unidades de disco rígido Olá endereço fornecido durante a criação da tarefa de envio.
* Atualize a entrega de Olá controlo número nos detalhes de tarefa de exportação de Olá e submeter a tarefa de exportação de Olá.
* unidades de Olá são recebidas e processadas no Centro de dados do Azure Olá.
* unidades de Olá são encriptadas com BitLocker; chaves de Olá estão disponíveis através de Olá portal do Azure.  
* unidades de Olá são fornecidas com o seu operadora conta toohello endereço do remetente fornecido na tarefa de importação de Olá.
  
    ![Figura 2:Export fluxo de trabalho](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>Visualizar o estado de tarefa e unidade
Pode controlar o estado de Olá da sua importação ou exportar tarefas de Olá portal do Azure. Clique em Olá **importar/exportar** separador. Uma lista das suas tarefas serão apresentados na página Olá.

![Vista de estado da tarefa](./media/storage-import-export-service/jobstate.png)

Irá ver um dos Olá seguintes Estados das tarefas, dependendo de onde a unidade está no processo de Olá.

| Estado da tarefa | Descrição |
|:--- |:--- |
| Criação | Depois de uma tarefa é criada, o estado é definido tooCreating. Enquanto está em Olá Estado criar tarefa de Olá, hello serviço importar/exportar assume Olá unidades não foram fornecidos toohello Centro de dados. Uma tarefa poderá permanecer num Estado de criar Olá para cópia de segurança tootwo semanas, após o qual é automaticamente eliminado pelo serviço de Olá. |
| Envio | Depois de enviar o pacote, deve atualizar Olá controlo informações Olá portal do Azure.  Isto irá ativar a tarefa Olá para "Envio". tarefa de Olá permanecerá no estado de envio de Olá para cópia de segurança tootwo semanas. 
| Foi recebido | Depois de todas as unidades foram recebidas no Centro de dados de Olá, irá definir estado da tarefa Olá toohello recebidos. |
| Transferência de | Depois de pelo menos uma unidade começou a processar, estado da tarefa Olá será definido toohello Transferring. Ver Estados de unidade de Olá secção abaixo para obter informações detalhadas. |
| Empacotamento | Depois de todas as unidades concluiu o processamento, tarefa Olá será colocada no estado de empacotamento de Olá até Olá unidades são fornecido tooyou back. |
| Foi concluída | Depois de todas as unidades de terem sido fornecidos back toohello cliente, se a tarefa de Olá tiver sido concluída sem erros, em seguida, a tarefa de Olá será definida toohello estado concluído. tarefa de Olá será eliminada automaticamente após 90 dias no Olá estado concluído. |
| Fechado | Depois de todas as unidades de terem sido fornecidos back toohello cliente, se tiverem sido erros durante o processamento de Olá da tarefa de Olá, em seguida, tarefa Olá será definida toohello de estado fechado. tarefa de Olá será eliminada automaticamente após 90 dias no estado fechado Olá. |

tabela de Olá abaixo descreve Olá o ciclo de vida de uma unidade individuais, que passa através de uma tarefa de importação ou exportação. estado atual do Olá de cada unidade numa tarefa agora é visível no Olá portal do Azure.
Olá tabela seguinte descreve cada Estado de cada unidade de uma tarefa pode pass-through.

| Unidade de estado | Descrição |
|:--- |:--- |
| Especificado | Para uma tarefa de importação, quando a tarefa de Olá é criada a partir Olá portal do Azure, o estado inicial Olá uma unidade é Olá especificado estado. Para uma tarefa de exportação, uma vez que não unidade é especificada quando Olá tarefa é criada, o estado da unidade inicial Olá é Olá recebidos estado. |
| Foi recebido | unidade de Olá passa toohello recebidos estado quando o operador de serviço de importação/exportação Olá processou unidades Olá que foram recebidas do Olá da empresa para uma tarefa de importação de envio. Para uma tarefa de exportação, o estado da unidade inicial de Olá é Olá recebidos estado. |
| NeverReceived | unidade de Olá irá mover toohello NeverReceived estado quando chegar a esse pacote Olá para uma tarefa, mas o pacote de Olá não contém a unidade de Olá. Pode também mover uma unidade para este estado se duas semanas, uma vez que o serviço de Olá recebeu informações de envio de Olá, mas o pacote de Olá ainda não chegaram Centro de dados de Olá. |
| Transferência de | Uma unidade irá mover toohello Transferring estado quando o serviço de Olá começa dados tootransfer Olá unidade tooWindows Storage do Azure. |
| Foi concluída | Uma unidade irá mover toohello estado concluído quando o serviço de Olá com êxito tenha transferido todos os dados de Olá sem erros.
| CompletedMoreInfo | Uma unidade irá mover toohello CompletedMoreInfo estado ao serviço de Olá encontrou alguns problemas ao copiar dados a partir de ou toohello unidade. informações de Olá podem incluir erros, avisos e mensagens informativas sobre substituir blobs.
| ShippedBack | unidade de Olá irá mover toohello ShippedBack estado quando tem sido enviada do endereço devolvido de toohello back do Centro de dados Olá. |

Esta imagem do portal do Azure de Olá apresenta o estado de unidade de Olá de uma tarefa de exemplo:

![Vista de estado de unidade](./media/storage-import-export-service/drivestate.png)

Olá tabela seguinte descreve Olá unidade falha Estados e as ações de Olá executadas para cada Estado.

| Unidade de estado | Evento | Resolução / passo seguinte |
|:--- |:--- |:--- |
| NeverReceived | Uma unidade que está marcada como NeverReceived (porque não foi recebida como parte da shipment da tarefa de Olá) chega no shipment outro. | equipa de operações de Olá irá mover Olá unidade toohello Estado Received. |
| N/D | Uma unidade que não faz parte de qualquer tarefa chega ao centro de dados de Olá como parte de outra tarefa. | unidade de Olá será marcada como uma unidade adicional e será devolvida toohello cliente quando a tarefa de Olá associada ao pacote original Olá for concluída. |

### <a name="time-tooprocess-job"></a>Tarefa de tooprocess de tempo
Olá período de tempo que demora tooprocess uma tarefa de importação/exportação varia dependendo de fatores diferentes, tais como o tempo de envio, tipo de tarefa, escreva e o tamanho dos Olá dados que está a ser copiados e Olá tamanho dos discos de Olá fornecido. Olá serviço importar/exportar não tem um SLA mas após discos Olá são recebidos serviço Olá strives toocomplete Olá cópia dentro de 7 dias too10. Pode utilizar o progresso da tarefa Olá REST API tootrack Olá mais detalhadamente. Não há um parâmetro concluído percentagem Olá operação de lista de tarefas que lhe dá uma indicação de progresso de cópia. Entrar toous se precisar de uma estimativa toocomplete uma tarefa de importação/exportação crítico de tempo.

### <a name="pricing"></a>Preços
**Taxa de processamento de unidade**

Há uma taxa de processamento de unidade para cada unidade processada como parte da sua importação ou exportação tarefa. Ver detalhes de Olá no Olá [preços do Azure para importar/exportar](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Os custos de envio**

Quando são enviados unidades tooAzure, paga Olá operadora de envio de toohello de custo de envio. Quando a Microsoft devolve Olá unidades tooyou, Olá custo de envio é cobrada conta operadora toohello fornecido no momento de Olá da criação da tarefa.

**Custos de transação**

Não existem sem custos de transação ao importar dados para armazenamento de Blobs. encargos associados à saída padrão Olá são aplicáveis quando os dados são exportados do armazenamento de Blobs. Para obter mais detalhes sobre os custos de transação, consulte [preços de transferência de dados.](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Guia de Introdução
Nesta secção, iremos fornecer instruções passo a passo para criação de uma importação e uma tarefa de exportação. Certifique-se de que cumpre todos os Olá [pré-requisitos](#pre-requisites) antes de prosseguir.

> [!IMPORTANT]
> serviço de Olá suporta uma conta de armazenamento standard por importar ou exportar a tarefa e não suporta contas de armazenamento premium. 
> 
> 
## <a name="create-an-import-job"></a>Criar uma tarefa de importação
Crie uma importação tarefa toocopy dados tooyour conta do storage do Azure a partir de discos rígidos por uma ou mais unidades que contêm dados toohello especificado de centro de dados de envio. Olá tarefa de importação transmite detalhes sobre unidades de disco rígido, toobe dados copiados, conta de armazenamento de destino e o envio de serviços de informação toohello importar/exportar do Azure. Criar uma tarefa de importação é um processo de três passos. Em primeiro lugar, prepare a unidades utilizando a ferramenta de WAImportExport Olá. Segundo, submeta uma tarefa de importação utilizando Olá portal do Azure. Terceira, são enviados Olá unidades toohello endereço fornecido durante Olá de criação e atualização de tarefa de envio informações na sua detalhes da tarefa de envio.   

### <a name="prepare-your-drives"></a>Preparar as suas unidades
Olá primeiro passo quando importar os dados utilizando o serviço de importação/exportação do Azure Olá tooprepare suas unidades utilizando a ferramenta de WAImportExport Olá. Siga os passos de Olá abaixo tooprepare suas unidades.

1. Identifica Olá dados toobe importado. Isto pode dever-se ao diretórios e ficheiros autónomos no servidor local Olá ou uma partilha de rede.  
2. Determine o número de Olá de unidades que precisa de, dependendo do tamanho total dos dados de Olá. Obter Olá necessário diversas polegada 2,5 SSD ou 2,5" ou 3.5" SATA II ou III unidades de disco rígido.
3. Identifica a conta de armazenamento de destino Olá, contentor, diretórios virtuais e os blobs.
4.  Determine os diretórios de Olá e/ou de ficheiros autónomo que serão copiado tooeach de disco rígido.
5.  Crie Olá ficheiros CSV para o conjunto de dados e driveset.
    
    **Ficheiro CSV de conjunto de dados**
    
    Segue-se um exemplo de ficheiro CSV de conjunto de dados de exemplo:
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    Olá acima exemplo, 100M_1.csv.txt serão copiados toohello raiz do contentor de Olá com o nome "containername". Se o nome de contentor Olá "containername" não existir, será criada. Todos os ficheiros e pastas sob 50M_original será toocontainername recursivamente copiada. Irá ser mantida a estrutura de pastas.

    Saiba mais sobre [preparar ficheiro CSV do conjunto de dados de Olá](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **Lembre-se**: por predefinição, os dados de Olá serão importados como Blobs de blocos. Pode utilizar dados de valor de campo tooimport Olá BlobType como Blobs de páginas. Por exemplo, se estiver a importar os ficheiros VHD que serão montados como discos numa VM do Azure, tem de importá-los como Blobs de páginas.

    **Ficheiro Driveset CSV**

    valor Olá driveset Olá sinalizador é um ficheiro CSV que contém a lista de Olá de letras de unidade discos toowhich Olá estão mapeadas para que Olá ferramenta toocorrectly escolha lista Olá de toobe discos preparado. 

    Segue-se exemplo Olá driveset um ficheiro CSV:
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    No Olá acima exemplo, presume-se que os dois discos estão anexados e básicos NTFS volumes com letra de volume G:\ e H:\ foram criados. ferramenta de Olá irá formatar e encriptar o disco de Olá que aloja H:\ e irá não formatar ou não encriptar o disco de Olá G:\ do volume de alojamento.

    Saiba mais sobre [preparar um ficheiro CSV driveset Olá](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Olá utilize [WAImportExport ferramenta](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy tooone os dados ou mais unidades de disco rígido.
7.  Pode especificar "Encriptar" no campo de encriptação no drivset CSV tooenable a encriptação BitLocker na unidade de disco de rígido Olá. Em alternativa, pode também ativar a encriptação BitLocker manualmente na unidade de disco de rígido Olá e especificar "AlreadyEncrypted" e fornecer a chave de Olá no Olá driveset CSV ao executar a ferramenta de Olá.

8. Não modifique dados Olá em unidades de disco de rígido Olá ou ficheiros do diário de alterações de Olá depois de concluir a preparação de disco.

> [!IMPORTANT]
> Cada unidade de disco rígido, preparar resultará num ficheiro diário de alterações. Quando estiver a criar tarefa de importação de Olá utilizando Olá portal do Azure, tem de carregar todos os ficheiros do diário de alterações de Olá de unidades de Olá que fazem parte dessa tarefa de importação. Unidades sem diário de alterações não serão possível processar os ficheiros.
> 
>

Abaixo são comandos Olá e exemplos para preparar a unidade de disco de rígido Olá utilizando WAImportExport ferramenta.

Ferramenta de WAImportExport PrepImport comando para Olá primeiro de copiar diretórios toocopy de sessão e/ou os ficheiros com uma nova sessão de cópia:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Importar exemplo 1**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Ordem demasiado**adicionar mais unidades**, um pode criar um novo ficheiro de driveset e execute o comando de Olá tal como indicado abaixo. Para copiar subsequentes sessões toohello diferentes unidades de disco superior ao especificado no ficheiro. csv de InitialDriveset, especifique um novo ficheiro CSV driveset e fornecê-lo como um parâmetro de toohello valor "AdditionalDriveSet". Olá utilize **mesmo ficheiro de diário** nome e fornecem um **novo ID de sessão**. formato de Olá do ficheiro AdditionalDriveset CSV é igual ao formato InitialDriveSet.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Importar exemplo 2**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

Na ordem tooadd dados adicionais toohello driveset mesmo, a ferramenta WAImportExport PrepImport comando pode ser invocada para cópia subsequentes sessões toocopy adicionais/diretório de ficheiros: para toohello do sessões de cópia subsequentes unidades de disco de rígido mesmo especificado no . Csv de InitialDriveset de ficheiros, especifique Olá **mesmo ficheiro de diário** nome e fornecem um **novo ID de sessão**; não há nenhuma chave de conta de armazenamento do necessidade tooprovide Olá.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Importar exemplo 3**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Ver mais detalhes sobre como utilizar a ferramenta de WAImportExport Olá no [preparar unidades de disco rígido para importação](storage-import-export-tool-preparing-hard-drives-import.md).

Além disso, consulte toohello [unidades de disco rígido tooprepare do fluxo de trabalho para uma tarefa de importação de exemplo](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) para obter mais instruções passo a passo.  

### <a name="create-hello-import-job"></a>Criar tarefa de importação de Olá
1. Depois de ter preparado a unidade, navegue até tooyour a conta de armazenamento no Olá portal do Azure e ver Olá Dashboard. Em **relance rápida**, clique em **criar uma tarefa de importação**. Reveja os passos de Olá e selecione Olá tooindicate de caixa de verificação que preparou a unidade e de que tem o ficheiro de diário de alterações de disco Olá disponível.
2. No passo 1, forneça as informações de contacto para Olá responsável para esta tarefa de importação e um endereço de retorno válido. Se desejar toosave dados de registo verboso para a tarefa de importação de Olá, verifique a opção de Olá demasiado**guardar Olá registo verboso no contentor de blob meu 'waimportexport'**.
3. No passo 2, carregar ficheiros do diário de unidade Olá que obteve durante o passo de preparação do Olá unidade. Precisará de um ficheiro de tooupload para cada unidade que está preparado.
   
   ![Criar tarefa de importação - passo 3](./media/storage-import-export-service/import-job-03.png)
4. No passo 3, introduza um nome descritivo para a tarefa de importação de Olá. Tenha em atenção que o nome de Olá que introduzir pode conter apenas letras minúsculas, números, hífenes e carateres de sublinhado, tem de começar com uma letra e não pode conter espaços. Irá utilizar o nome de Olá escolher tootrack as tarefas enquanto estiverem em curso e depois de serem concluídas.
   
   Em seguida, selecione a região do Centro de dados da lista de Olá. região de centro de dados de Olá indicará toowhich tem de enviar o pacote de endereços e do Centro de dados de Olá. Consulte as FAQ de Olá abaixo para obter mais informações.
5. No passo 4, selecione a retorno operadora Olá lista e introduza o seu número de conta operadora. A Microsoft irá utilizar esta conta tooship Olá unidades back tooyou assim que a tarefa de importação estiver concluída.
   
   Se tiver o seu número de controlo, selecione a operadora de entrega da lista de Olá e introduza o seu número de controlo.
   
   Se não tiver um controlo número ainda, escolha **posso irá fornecer as minhas informações de envio para esta tarefa de importação depois posso fornecidos meu pacote**, em seguida, conclua o processo de importação de Olá.
6. devolver o número do seu controlo depois fornecidos seu pacote de tooenter toohello **importar/exportar** página para a sua conta de armazenamento no Olá portal do Azure, selecione a tarefa Olá lista e escolha **informações de envio de mensagens em fila**. Navegue através do Assistente de Olá e introduza o seu número de controlo no passo 2.
   
    Se Olá controlo número não for atualizado no 2 semanas de criação de tarefa Olá, a tarefa de Olá irá expirar.
   
    Se a tarefa de Olá está num Estado de criar, envio ou Transferring Olá, também pode atualizar o número de conta operadora no passo 2 do Assistente de Olá. Quando a tarefa de Olá está num Estado de empacotamento de Olá, não é possível atualizar o seu número de conta operadora para essa tarefa.
7. Pode controlar o progresso da tarefa no dashboard do portal Olá. Consulte o que significa cada Estado de tarefa na secção anterior Olá por [visualizar o estado da tarefa](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Criar uma tarefa de exportação
Crie um Olá de toonotify de tarefa de exportação serviço importar/exportar que que irá enviar um ou mais unidades vazio toohello Datacenter para que os dados podem ser exportados a partir do seu unidades de toohello de conta de armazenamento e unidades de Olá, em seguida, enviado tooyou.

### <a name="prepare-your-drives"></a>Preparar as suas unidades
Verificações prévias seguintes são recomendadas para preparar a unidades para uma tarefa de exportação:

1. Verifique o número de Olá de discos necessários utilizando o comando de PreviewExport da ferramenta de WAImportExport Olá. Para obter mais informações, consulte [pré-visualização utilização da unidade para uma tarefa de exportação](https://msdn.microsoft.com/library/azure/dn722414.aspx). Ajuda a utilização da unidade de blobs de Olá selecionou de pré-visualização, com base no tamanho Olá de unidades de Olá vai toouse.
2. Verifique se o pode leitura/escrita toohello o disco rígido que será enviada para a tarefa de exportação de Olá.

### <a name="create-hello-export-job"></a>Criar tarefa de exportação de Olá
1. toocreate uma tarefa de exportação, navegue tooyour a conta de armazenamento no Olá portal do Azure e ver Olá Dashboard. Em **relance rápida**, clique em **criar uma tarefa de exportação** e continuar através do Assistente de Olá.
2. No passo 2, forneça as informações de contacto para Olá responsável para esta tarefa de exportação. Se desejar toosave dados de registo verboso para a tarefa de exportação de Olá, verifique a opção de Olá demasiado**guardar Olá registo verboso no contentor de blob meu 'waimportexport'**.
3. No passo 3, especifique qual blob unidades ou unidade de dados pretende tooexport da sua conta de armazenamento tooyour em branco. Pode escolher tooexport todos os dados de BLOBs numa conta do storage Olá ou pode especificar que blobs ou define de blobs tooexport.
   
   toospecify tooexport um blob, utilize Olá **igual a** Seletor e especificar Olá caminho relativo toohello do blob, começando com o nome do contentor Olá. Utilize *$root* recipiente-raiz toospecify Olá.
   
   toospecify todos os blobs começando com um prefixo, utilize Olá **começa por** Seletor e especifique o prefixo de Olá, começando com uma barra '/'. prefixo de Olá poderá prefixo Olá do nome do contentor Olá, o nome do contentor completa de Olá ou o nome de contentor completa de Olá seguido de prefixo de Olá do nome do blob Olá.
   
   Olá, a tabela seguinte mostra exemplos de caminhos de blob válido:
   
   | Seletor | Caminho do blob | Descrição |
   | --- | --- | --- |
   | Começa por |/ |Exporta todos os blobs na conta do storage Olá |
   | Começa por |/$root / |Exporta todos os blobs no contentor de raiz de Olá |
   | Começa por |/Book |Exporta todos os blobs em qualquer contentor que começa com o prefixo **livro** |
   | Começa por |/Music/ |Exporta todos os blobs no contentor **música** |
   | Começa por |música/love |Exporta todos os blobs no contentor **música** que começam com prefixo **adoram** |
   | Igual a demasiado|$root/logo.bmp |Blob de exportações **logo.bmp** no recipiente-raiz Olá |
   | Igual a demasiado|videos/Story.mp4 |Blob de exportações **story.mp4** no contentor **vídeos** |
   
   Tem de fornecer caminhos de blob Olá nos formatos válidos de tooavoid erros durante o processamento, conforme mostrado nesta captura de ecrã.
   
   ![Criar tarefa de exportação - passo 3](./media/storage-import-export-service/export-job-03.png)
4. No passo 4, introduza um nome descritivo para a tarefa de exportação de Olá. introduzir o nome de Olá pode conter apenas letras minúsculas, números, hífenes e carateres de sublinhado, tem de começar com uma letra e não pode conter espaços.
   
   região de centro de dados de Olá indicará toowhich de centro de dados de Olá tem de enviar o pacote. Consulte as FAQ de Olá abaixo para obter mais informações.
5. No passo 5, selecione a retorno operadora Olá lista e introduza o seu número de conta operadora. A Microsoft irá utilizar esta conta tooship a unidades de fazer uma cópia de tooyou depois de concluída a tarefa de exportação.
   
   Se tiver o seu número de controlo, selecione a operadora de entrega da lista de Olá e introduza o seu número de controlo.
   
   Se não tiver um controlo número ainda, escolha **posso irá fornecer as minhas informações de envio para esta tarefa de exportação depois posso fornecidos meu pacote**, em seguida, conclua o processo de exportação de Olá.
6. devolver o número do seu controlo depois fornecidos seu pacote de tooenter toohello **importar/exportar** página para a sua conta de armazenamento no Olá portal do Azure, selecione a tarefa Olá lista e escolha **informações de envio de mensagens em fila**. Navegue através do Assistente de Olá e introduza o seu número de controlo no passo 2.
   
    Se Olá controlo número não for atualizado no 2 semanas de criação de tarefa Olá, a tarefa de Olá irá expirar.
   
    Se a tarefa de Olá está num Estado de criar, envio ou Transferring Olá, também pode atualizar o número de conta operadora no passo 2 do Assistente de Olá. Quando a tarefa de Olá está num Estado de empacotamento de Olá, não é possível atualizar o seu número de conta operadora para essa tarefa.
   
   > [!NOTE]
   > Se Olá blob toobe exportado está a ser utilizada no momento de Olá de copiar a unidade de toohard, o serviço importar/exportar do Azure irá tirar um instantâneo de instantâneo de Olá de blob e copie Olá.
   > 
   > 
7. Pode controlar o progresso da tarefa no dashboard de Olá no Olá portal do Azure. Consulte o que significa cada Estado de tarefa na secção anterior Olá em "ver o estado da tarefa".
8. Depois de receber Olá unidades com os seus dados exportados, pode ver e copiar chaves de BitLocker de Olá geradas pelo serviço de Olá para a unidade. Navegue tooyour conta do storage no portal do Azure de Olá e clique Olá separador de importação/exportação. Selecione a tarefa de exportação Olá lista e clique no botão Ver as chaves de Olá. chaves do BitLocker Olá aparecem da seguinte forma:
   
   ![Ver as chaves de BitLocker para a tarefa de exportação](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Leia secção das FAQ de Olá abaixo como abrange perguntas mais comuns Olá clientes encontrarem ao utilizar este serviço.

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

**Pode copiar File storage do Azure com o serviço de importação/exportação do Azure Olá?**

Não, Olá serviço importar/exportar do Azure suporta apenas Blobs de blocos e Blobs de páginas. Todos os outros tipos de armazenamento, incluindo o armazenamento de ficheiros do Azure, o Table Storage e o armazenamento de filas não são suportados.

**Serviço de importação/exportação do Azure Olá está disponível para subscrições de CSP?**

Serviço de importação/exportação do Azure suporta subscrições de CSP.

**Posso ignorar passo de preparação de unidade de Olá para uma tarefa de importação ou pode preparar uma unidade sem copiar?**

Qualquer unidade que pretende que tooship para importar os dados deve estar preparada utilizando a ferramenta de Azure WAImportExport Olá. Tem de utilizar unidade toohello de dados toocopy Olá WAImportExport ferramenta.

**É necessário tooperform qualquer preparação do disco durante a criação de uma tarefa de exportação?**

Não existem, mas algumas verificações prévias são recomendadas. Verifique o número de Olá de discos necessários utilizando o comando de PreviewExport da ferramenta de WAImportExport Olá. Para obter mais informações, consulte [pré-visualização utilização da unidade para uma tarefa de exportação](https://msdn.microsoft.com/library/azure/dn722414.aspx). Ajuda a utilização da unidade de blobs de Olá selecionou de pré-visualização, com base no tamanho Olá de unidades de Olá vai toouse. Também se de que pode ler a partir do e escrita toohello unidade de disco rígido que será enviada para Olá exportar tarefa.

**O que acontece se enviar acidentalmente um HDD que não é compatível com toohello suportada requisitos?**

Centro de dados do Azure de Olá devolverá unidade Olá que não é compatível com toohello suportado requisitos tooyou. Se apenas algumas das unidades de Olá no pacote de Olá cumpre os requisitos de suporte de Olá, essas unidades serão processadas e serão devolvidas unidades Olá que não cumprem os requisitos de Olá tooyou.

**Pode cancelar a minha tarefa?**

Pode cancelar uma tarefa quando o estado está a criar ou do envio.

**Quanto pode ver estado Olá as tarefas concluídas no Olá portal do Azure?**

Pode ver o estado de Olá para concluído as tarefas de cópia de segurança too90 dias. As tarefas concluídas serão eliminadas após 90 dias.

**Se posso pretende tooimport ou exportar mais de 10 unidades, o que devo fazer?**

Uma importação ou exportação tarefa pode referenciar apenas 10 unidades numa tarefa única para o serviço de importação/exportação Olá. Se quiser tooship mais de 10 unidades, pode criar várias tarefas. Olá, unidades que estejam associadas a Olá mesma tarefa deve ser enviada em conjunto no mesmo pacote.
A Microsoft oferece orientação e assistência quando a capacidade de dados abrange várias disco importar tarefas. Contacte bulkimport@microsoft.com para obter mais informações

**Olá serviço formato Olá unidades antes de a devolvê-las?**

Não. Todas as unidades estão encriptadas com o BitLocker.

**Pode comprar unidades de tarefas de importação/exportação do Microsoft?**

Não. Terá de tooship as seus próprios unidades para ambos importar e exportar tarefas.

* * Como aceder a dados que são importados por este serviço * *

dados de Olá na sua conta de armazenamento do Azure podem ser acedidos através de Olá Portal do Azure ou utilizar uma ferramenta autónoma chamado Explorador de armazenamento. https://Docs.microsoft.com/en-us/Azure/vs-Azure-Tools-Storage-Manage-with-Storage-Explorer 

**Após a conclusão da tarefa de importação de Olá, o que irá meu aspeto de dados, como na conta do storage Olá? A minha hierarquia directory preservada?**

Quando preparar um disco rígido para uma tarefa de importação, destino Olá é especificado por campo de DstBlobPathOrPrefix Olá no conjunto de dados CSV. Este é o contentor de destino Olá no toowhich de conta de armazenamento de Olá dados do disco rígido Olá são copiados. Dentro deste contentor de destino, diretórios virtuais são criados para as pastas do disco rígido Olá e blobs são criados para ficheiros. 

**Se a unidade de Olá tem ficheiros que já existem na minha conta de armazenamento, o serviço de Olá substituirá os blobs existentes na minha conta de armazenamento?**

Quando preparar a unidade de Olá, pode especificar se os ficheiros do destino de Olá devem ser substituídos ou ignoradas utilizando o campo de Olá no ficheiro CSV de conjunto de dados chamado disposição: < mudar o nome | substituir o não | substituir >. Por predefinição, o serviço de Olá irá mudar o nome de novos ficheiros de Olá em vez de substituir blobs existentes.

**Ferramenta de WAImportExport Olá é compatível com os sistemas operativos de 32 bits?**
Não. ferramenta de WAImportExport Olá só é compatível com sistemas de operativos do Windows de 64 bits. Consulte a secção de sistemas operativos toohello Olá [pré-requisitos](#pre-requisites) para uma lista completa das versões de SO suportadas.

**Deve posso incluir qualquer coisa que não a unidade de disco de rígido Olá na minha pacote?**

. São enviados apenas as unidades de disco rígido. Não inclua itens, como os cabos de alimentação de energia ou cabos USB.

**É necessário tooship meu unidades utilizando FedEx ou DHL?**

Pode enviar unidades toohello Datacenter utilizando qualquer operadora conhecida como FedEx, DHL, UPS ou nos serviço Postal. No entanto, para envio Olá unidades back tooyou do Centro de dados de Olá, tem de fornecer um número de conta FedEx no Olá E.U.A. e EU ou um número de conta DHL Olá Ásia e regiões da Austrália.

**Existem restrições com envio internationally minha unidade?**

Tenha em atenção que Olá físico suporte de dados que são envio poderá ter limites internacional toocross. É responsável por assegurar que os dados e suportes de dados físicos são importados e/ou exportados de acordo com as leis aplicáveis Olá. Antes do envio suporte de dados físico Olá, de verificação com o seu tooverify consultores que os dados e suportes de dados podem legalmente ser enviada toohello identificado Centro de dados. Isto irá ajudar tooensure que atinge Microsoft atempadamente.

**Ao criar uma tarefa, Olá endereço de envio é uma localização diferente do meu localização da conta de armazenamento. O que devo fazer?**

Algumas localizações de conta de armazenamento são mapeada tooalternate localizações de envio. Anteriormente, localizações de envio disponíveis também podem ser tooalternate temporariamente mapeada localizações. Verifique sempre Olá endereço fornecido durante a criação da tarefa antes da unidades de envio de envio.

**Quando a minha unidade do envio, operadora Olá pede-lhe Olá dados center endereço e phone número de contacto. O que posso fornece?**

Olá, número de telefone e o DC endereço é fornecido como parte da criação da tarefa.

**Posso utilizar caixas de correio do Olá do Azure para importar/exportar serviço toocopy PST e SharePoint dados tooO365?**

Consulte demasiado[ficheiros de importação PST ou SharePoint dados tooOffice 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**Posso utilizar toocopy de serviço do Azure para importar/exportar Olá meu toohello offline cópias de segurança de serviço de cópia de segurança do Azure?**

Consulte demasiado[fluxo de trabalho de cópia de segurança Offline no Backup do Azure](../../backup/backup-azure-backup-import-export.md).

**O que é o número máximo Olá de HDD no um shipment?**

Qualquer número de HDDs pode estar num shipment e se os discos de Olá pertencerem toomultiple tarefas recomenda-se demasiado um) ter discos Olá etiquetados com nomes de tarefa Olá correspondente. b) as tarefas de Olá de atualização com um número de controlo de com -1, o sufixo-2 etc.
  
**O que é Olá máximo BLOBs de blocos e o tamanho do Blob de página suportados por disco importação/exportação?**

Tamanho do Blob de bloco máximo é aproximadamente 4.768TB ou 5,000,000 MB.
Tamanho do Blob de página máximo é 1TB.

**Disco para importar/exportar suporta a encriptação AES 256?**

Serviço de importação/exportação do Azure por predefinição encripta com a encriptação bitlocker AES 128, mas isto pode ser aumentada tooAES 256 ao encriptar manualmente com o bitlocker antes de dados são copiados. 

Se utilizar [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), segue-se um comando de exemplo
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Se utilizar [WAImportExport ferramenta](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) especificar "AlreadyEncrypted" e fornecer a chave de Olá no Olá driveset CSV.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Passos seguintes

* [Configurar a ferramenta de WAImportExport Olá](storage-import-export-tool-how-to.md)
* [Transferência de dados com Olá utilitário de linha de comandos AzCopy](storage-use-azcopy.md)
* [Exemplo de API de REST de exportação de importação do Azure](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

