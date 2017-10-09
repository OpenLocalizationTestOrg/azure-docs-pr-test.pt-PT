---
title: "Computação aaaAzure - extensão de diagnóstico do Linux | Microsoft Docs"
description: "Como tooconfigure Olá métricas de toocollect de extensão de diagnóstico Linux do Azure (LAD) e eventos de registo de VMs do Linux em execução no Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Utilize registos e as métricas de toomonitor de extensão de diagnóstico do Linux

Este documento descreve a versão 3.0 e mais recente de Olá extensão de diagnóstico do Linux.

> [!IMPORTANT]
> Para obter informações sobre a versão mais antiga e 2.3, consulte [neste documento](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Introdução

Olá extensão de diagnóstico do Linux ajuda a um utilizador monitor Olá estado de funcionamento de uma VM com Linux em execução no Microsoft Azure. Tem Olá seguintes capacidades:

* Recolhe métricas de desempenho do sistema de Olá VM e armazena-os numa tabela específica numa conta do storage designada.
* Obtém o registo de eventos do syslog e armazena-os numa tabela específica no Olá designada de conta de armazenamento.
* Permite que os utilizadores toocustomize Olá dados as métricas que são recolhidas e a ser carregadas.
* Permite a instalações de syslog do utilizadores toocustomize Olá e níveis de gravidade dos eventos que são recolhidos e a ser carregados.
* Permite que os utilizadores tooupload especificado ficheiros tooa armazenamento designado tabela de registo de.
* Suporta o envio de métricas e registo de eventos tooarbitrary EventHub pontos finais e a formatados em JSON blobs no Olá designada de conta de armazenamento.

Esta extensão funciona com ambos os modelos de implementação do Azure.

## <a name="installing-hello-extension-in-your-vm"></a>Instalação da extensão Olá em VM

Pode ativar esta extensão utilizando cmdlets do Azure PowerShell Olá, scripts da CLI do Azure ou modelos de implementação do Azure. Para obter mais informações, consulte [extensões funcionalidades](./extensions-features.md).

Olá portal do Azure não pode ser utilizado tooenable ou configurar LAD 3.0. Em vez disso, instala e configura versão 2.3. Gráficos de portais do Azure e alertas de trabalham com dados de ambas as versões da extensão de Olá.

Estas instruções de instalação e um [configuração de exemplo transferível](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configurar LAD 3.0 para:

* captura e arquivo Olá mesmas métricas que foram fornecidas pelo LAD 2.3;
* captura de um conjunto de métricas de sistema de ficheiros, novo tooLAD 3.0; útil
* captura de coleção de syslog Olá predefinida ativada por LAD 2.3;
* Ative Olá experiência do portal do Azure para charting e alertas nas métricas VM.

configuração transferível Olá é apenas um exemplo; Modifique-toosuit as suas próprias necessidades.

### <a name="prerequisites"></a>Pré-requisitos

* **Agente Linux do Azure versão 2.2.0 ou posterior**. A maioria das imagens de galeria do Azure VM Linux incluem versão 2.2.7 ou posterior. Executar `/usr/sbin/waagent -version` versão de Olá tooconfirm instalado Olá VM. Se Olá VM estiver a executar uma versão mais antiga do agente do convidado Olá, siga [estas instruções](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate-lo.
* **CLI do Azure**. [Configurar Olá Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) ambiente no seu computador.
* Olá wget comando, se ainda não tiver: executar `sudo apt-get install wget`.
* Uma subscrição do Azure existente e um armazenamento existente contas dentro da mesma dados de Olá toostore.

### <a name="sample-installation"></a>Instalação de exemplo

Preencha os parâmetros corretos Olá no Olá primeiro três linhas, em seguida, execute este script como raiz:

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

URL de Olá para configuração de exemplo de Olá e o respetivo conteúdo, é toochange do requerente. Transfira uma cópia do ficheiro JSON Olá definições do portal e personalizá-lo para as suas necessidades. Qualquer modelos ou automatização que constrói, deve utilizar a sua cópia, em vez de a transferir esse URL cada vez.

### <a name="updating-hello-extension-settings"></a>A atualizar as definições de extensão de Olá

Depois de alterou a sua protegido ou definições público, implementá-las toohello VM executando Olá mesmo comando. Se nada alterado nas definições de Olá, definições de Olá atualizado são enviadas toohello extensão. LAD reloads configuração Olá e reinicia si próprio.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Migração a partir de versões anteriores da extensão de Olá

Olá a versão mais recente da extensão de Olá **3.0**. **Todas as versões antigas (2) foram preteridas e pode ser anuladas nesta ou após 31 de Julho de 2018**.

> [!IMPORTANT]
> Esta extensão apresenta a configuração de toohello de alterações de quebra de extensão de Olá. Um essa alteração foi efetuada a segurança de Olá tooimprove da extensão de Olá; como resultado, efeitos compatibilidade com 2 não foi possível manter. Além disso, Olá publicador de extensão para esta extensão é diferente do publicador Olá para as versões do Olá 2. x.
>
> toomigrate de 2. x toothis nova versão da extensão de Olá, tem de desinstalar extensão antigo do Olá (em nome do publicador antigo Olá), em seguida, instalar versão 3 Olá extensão.

Recomendações:

* Instale a extensão de Olá com a atualização de versões de secundárias automática ativada.
  * No modelo de implementação clássica VMs, especifique '3.*' como versão de Olá se estiver a instalar extensão Olá através da CLI XPLAT do Azure ou do Powershell.
  * Na implementação do Azure Resource Manager modelo VMs, incluir ' "autoUpgradeMinorVersion": true' no modelo de implementação de VM Olá.
* Utilize uma conta de armazenamento nova/diferente para LAD 3.0. Existem várias incompatibilidades pequenas entre LAD 2.3 e LAD 3.0 que tornam uma conta troublesome de partilha:
  * LAD 3.0 armazena eventos syslog numa tabela com um nome diferente.
  * counterSpecifier Olá cadeias para `builtin` métricas diferem no LAD 3.0.

## <a name="protected-settings"></a>Definições protegidas

Este conjunto de informações de configuração contém informações confidenciais que devem ser protegidas a partir da vista pública, por exemplo, as credenciais do armazenamento. Estas definições são transmitido tooand armazenada pela extensão de Olá em formato encriptado.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Nome | Valor
---- | -----
storageAccountName | nome de Olá Olá da conta de armazenamento na qual os dados são escritos pela extensão de Olá.
storageAccountEndPoint | ponto final de Olá (opcional) identificar nuvem Olá no qual Olá conta de armazenamento existe. Se esta definição estiver ausente, LAD predefinições toohello nuvem pública do Azure, `https://core.windows.net`. toouse uma conta de armazenamento em Datacenters do Azure, Azure Government ou Azure China, definir este valor em conformidade.
storageAccountSasToken | Um [token SAS de conta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) para serviços Blob e a tabela (`ss='bt'`), toocontainers aplicáveis e objetos (`srt='co'`), que concede adiciona, criar, listar, atualizar e permissões de escrita (`sp='acluw'`). Efetue *não* incluem Olá leading pergunta-interrogação (?).
mdsdHttpProxy | (opcional) HTTP proxy informações necessárias tooenable Olá extensão tooconnect toohello especificar conta de armazenamento e de ponto final.
sinksConfig | (opcional) Detalhes de destinos alternativos toowhich métricas e eventos podem ser fornecidos. detalhes específicos do Olá de cada sink de dados suportados pela extensão de Olá são abordados nas secções de Olá que se seguem.

Pode criar facilmente Olá necessário token SAS através de Olá portal do Azure.

1. Selecione toowhich de conta de armazenamento para fins gerais de Olá pretende Olá extensão toowrite
1. Selecione "Assinatura de acesso partilhado" de Olá definições parte menu à esquerda Olá
1. Certifique-secções apropriadas Olá conforme descritos anteriormente
1. Clique no botão de "SAS gerar" Olá.

![Imagem](./media/diagnostic-extension/make_sas.png)

Olá cópia gerado SAS no campo de storageAccountSasToken Olá; Remova a marca de pergunta leading Olá ("?").

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Esta secção opcional define adicionais destinos de extensão de Olá toowhich envia informações de Olá recolhe. matriz de "sink" Olá contém um objeto para cada sink de dados adicionais. Olá determina o atributo "tipo" Olá outros atributos no objeto de Olá.

Elemento | Valor
------- | -----
nome | Uma cadeia utilizada toorefer toothis sink noutro local na configuração da extensão Olá.
tipo | tipo de Olá do sink que está a ser definido. Determina a Olá outros valores (se aplicável) em instâncias deste tipo.

Versão 3.0 do Olá extensão de diagnóstico do Linux suporta dois tipos de receptores: EventHub e JsonBlob.

#### <a name="hello-eventhub-sink"></a>receptor de EventHub Olá

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

entrada de "sasURL" Olá contém Olá URL completo, incluindo o token SAS, para Olá dados do Hub de eventos toowhich deve ser publicado. LAD requer uma SAS nomenclatura uma política que ativa Olá enviar afirmações. Um exemplo:

* Criar um espaço de nomes de Event Hubs chamado`contosohub`
* Criar um Hub de eventos no espaço de nomes de Olá chamado`syslogmsgs`
* Criar uma política de acesso partilhado no Olá com o nome de Hub de eventos `writer` que permite Olá afirmações de envio

Se tiver criado uma SAS boa até à meia-noite UTC em 1 de Janeiro de 2018, o valor de sasURL Olá pode ser:

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Para obter mais informações sobre a criação de tokens SAS para os Event Hubs, consulte [esta página web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>receptor de JsonBlob Olá

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Dados direcionado tooa JsonBlob sink é armazenado em blobs no armazenamento do Azure. Cada instância de LAD cria um blob a cada hora para cada nome de sink. Cada blob contém sempre uma matriz JSON é sintaticamente válida do objeto. Novas entradas atomically são adicionadas toohello matriz. Os BLOBs são armazenados num contentor com o mesmo nome como sink Olá de Olá. Olá regras de armazenamento do Azure para os nomes de contentor do blob aplicam toohello nomes de JsonBlob sinks: entre 3 e 63 carateres ASCII alfanuméricos minúsculos ou travessões.

## <a name="public-settings"></a>Definições de público

Esta estrutura contém vários blocos de definições que controlam as informações de Olá recolhidas pela extensão de Olá. Cada definição é opcional. Se especificar `ladCfg`, também tem de especificar `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Elemento | Valor
------- | -----
StorageAccount | nome de Olá Olá da conta de armazenamento na qual os dados são escritos pela extensão de Olá. Tem de ser Olá mesmo nome como está especificado no Olá [protegidos definições](#protected-settings).
mdsdHttpProxy | (opcional) Mesmo do Olá [protegidos definições](#protected-settings). valor pública Olá é substituída pelo valor de privada Olá, se definir. Colocar as definições de proxy que contêm um segredo, tais como uma palavra-passe no Olá [protegidos definições](#protected-settings).

elementos de restantes Olá são descritos em detalhe no Olá secções a seguir.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Esta recolha de Olá de controlos de estrutura opcional de métricas e registos para entrega toohello dados de serviço e tooother de métricas de Azure sinks. Tem de especificar um `performanceCounters` ou `syslogEvents` ou ambos. Tem de especificar Olá `metrics` estrutura.

Elemento | Valor
------- | -----
eventVolume | (opcional) Controlos Olá número de partições criadas numa tabela de armazenamento Olá. Tem de ser um dos `"Large"`, `"Medium"`, ou `"Small"`. Se não for especificado, o valor predefinido de Olá é `"Medium"`.
sampleRateInSeconds | intervalo predefinido de Olá (opcional) entre a coleção de métricas (unaggregated) não processadas. frequência de amostragem Olá mais pequena suportada é 15 segundos. Se não for especificado, o valor predefinido de Olá é `15`.

#### <a name="metrics"></a>metrics

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Elemento | Valor
------- | -----
resourceId | ID de recurso do Azure Resource Manager Olá do Olá VM ou de dimensionamento da máquina virtual Olá definir Olá toowhich que VM pertence. Esta definição tem de ser também especificado se qualquer sink JsonBlob é utilizado numa configuração de Olá.
scheduledTransferPeriod | frequência de Olá que métricas agregadas são toobe calculado e transferidos tooAzure métricas, expressado como um intervalo de tempo é 8601. período de transferência mais pequeno Olá é 60 segundos, ou seja, PT1M. Tem de especificar pelo menos um scheduledTransferPeriod.

Exemplos de Olá métricas especificadas na secção de performanceCounters Olá são recolhidas a cada 15 segundos ou a taxa de exemplo de Olá explicitamente definida para o contador de Olá. Se forem apresentados vários scheduledTransferPeriod frequências (tal como no exemplo de Olá), cada agregação é calculada independentemente.

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Esta secção opcional controla coleção Olá de métricas. Exemplos não processados são agregados para cada [scheduledTransferPeriod](#metrics) tooproduce estes valores:

* média
* mínimo
* Máximo
* recolhido o último valor
* Contagem de amostras em bruto utilizado agregado de Olá toocompute

Elemento | Valor
------- | -----
sinks | (opcional) Uma lista separada por vírgulas dos nomes do sinks toowhich que LAD envia resultados métricos agregados. Todas as métricas agregadas são publicados tooeach listado sink. Consulte [sinksConfig](#sinksconfig). Exemplo: `"EHsink1, myjsonsink"`.
tipo | Identifica o fornecedor de real Olá de métrica de Olá.
Classe | Em conjunto com ". o contador" identifica métrica específica do Olá no espaço de nomes do fornecedor de Olá.
Contador | Em conjunto com "class", identifica métrica específica do Olá no espaço de nomes do fornecedor de Olá.
counterSpecifier | Identifica a métrica específica do Olá no espaço de nomes do Olá métricas do Azure.
Condição | (opcional) Aplica-se de uma instância específica de métrica de Olá Olá objeto toowhich de seleciona ou seleciona Olá agregação em todas as instâncias desse objeto. Para obter mais informações, consulte Olá [ `builtin` as definições de métrica](#metrics-supported-by-builtin).
sampleRate | É o intervalo de 8601 que define a taxa de Olá que são recolhidos exemplos não processados para esta métrica. Se não definir o intervalo de coleção de Olá é definido por valor Olá [sampleRateInSeconds](#ladcfg). frequência de amostragem suportados mais curta do Olá é 15 segundos (PT15S).
unidade | Deve ser um estas cadeias: "Count", "Bytes", "Segundos", "Percentagem", "CountPerSecond", "BytesPerSecond", "Millisecond". Define a unidade de Olá para a métrica de Olá. Os consumidores de dados de Olá recolhido esperam Olá recolhidos dados valores toomatch esta unidade. LAD ignora este campo.
displayName | Olá etiqueta (no idioma de Olá especificado por região associada Olá definição) toobe ligado toothis dados no Azure métricas. LAD ignora este campo.

counterSpecifier Olá é um identificador arbitrário. Os consumidores de métricas, como Olá charting portal do Azure e os alertas funcionalidade, utilizam counterSpecifier como Olá "chave", que identifica uma métrica ou uma instância de uma métrica. Para `builtin` métricas, recomendamos que utilize valores counterSpecifier que começam com `/builtin/`. Se está a recolher uma instância específica de uma métrica, recomendamos que ligue o identificador de Olá do valor de counterSpecifier Olá instância toohello. Alguns exemplos:

* `/builtin/Processor/PercentIdleTime`-Tempo inativo, Considerando todos os núcleos
* `/builtin/Disk/FreeSpace(/mnt)`-Espaço para o sistema de ficheiros do Olá /mnt
* `/builtin/Disk/FreeSpace`-Espaço Considerando todos os sistemas de ficheiros instalados montados

Nem LAD nem Olá portal do Azure espera Olá counterSpecifier valor toomatch qualquer padrão. Ser consistente na forma como pode construir valores de counterSpecifier.

Quando especificar `performanceCounters`, LAD escreve sempre tabela tooa de dados no armazenamento do Azure. Pode ter Olá mesmo dados escritos tooJSON blobs e/ou os Event Hubs, mas não é possível desativar a tabela de tooa armazenar dados. Todas as instâncias de Olá extensão de diagnóstico configurada toouse Olá a mesma conta de armazenamento, nome e o ponto final de adicionam os seus toohello métricas e registos mesma tabela. Se estiver a escrever VMs demasiados toohello pode limitar a mesma partição de tabela, Azure escreve toothat partição. eventVolume Olá definição faz com que as entradas toobe distribuídos por 1 (breve), 10 (mediano) ou 100 partições de diferentes (grande). Normalmente, "Médio" é suficiente tooensure tráfego não é limitado. funcionalidade de métricas de Azure Olá de Olá portal do Azure utiliza dados Olá nesta gráficos de tooproduce de tabela ou tootrigger alertas. nome da tabela Olá é concatenação Olá estas cadeias de:

* `WADMetrics`
* Olá "scheduledTransferPeriod" para Olá agregado valores armazenados na tabela de Olá
* `P10DV2S`
* Uma data, no formato de Olá "AAAAMMDD", que altera a cada 10 dias

Os exemplos incluem `WADMetricsPT1HP10DV2S20170410` e `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Esta secção opcional controla coleção Olá de eventos de registo de syslog. Se for omitida secção Olá, eventos syslog não são capturados de todo.

a coleção de syslogEventConfiguration Olá tem uma entrada para cada função do syslog de interesse. Se minSeverity "NONE" para uma determinada instalação ou se essa função não aparece no elemento de Olá de todo, não há eventos de instalação de que são capturados.

Elemento | Valor
------- | -----
sinks | Uma lista separada por vírgulas dos nomes do sinks registo individuais toowhich eventos são publicados. Todos os eventos de registo correspondentes restrições de Olá no syslogEventConfiguration são publicados tooeach listado sink. Exemplo: "EHforsyslog"
facilityName | Um nome de função do syslog (tal como "registo\_utilizador" ou "registo\_LOCAL0"). Consulte a secção "instalações" Olá Olá [página de man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para obter uma lista completa Olá.
minSeverity | Um nível de gravidade syslog (tal como "registo\_ERR" ou "registo\_informações"). Consulte a secção "nível de" Olá Olá [página de man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para obter uma lista completa Olá. extensão de Olá captura eventos enviados toohello instalações em especificados, ou acima Olá nível.

Quando especificar `syslogEvents`, LAD escreve sempre tabela tooa de dados no armazenamento do Azure. Pode ter Olá mesmo dados escritos tooJSON blobs e/ou os Event Hubs, mas não é possível desativar a tabela de tooa armazenar dados. Olá comportamento para esta tabela de criação de partições é Olá igual à descrita para `performanceCounters`. nome da tabela Olá é concatenação Olá estas cadeias de:

* `LinuxSyslog`
* Uma data, no formato de Olá "AAAAMMDD", que altera a cada 10 dias

Os exemplos incluem `LinuxSyslog20170410` e `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Esta secção opcional controla a execução de arbitrários [OMI](https://github.com/Microsoft/omi) consultas.

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Elemento | Valor
------- | -----
Espaço de nomes | (opcional) Olá OMI espaço de nomes no qual Olá consulta deve ser executada. Se não for indicado, o valor predefinido de Olá é "raiz/scx", implementado por Olá [fornecedores de plataforma do System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
consulta | Olá toobe consulta OMI foi executado.
Tabela | tabela de armazenamento do Azure Olá (opcional), no Olá designada de conta de armazenamento (consulte [protegidos definições](#protected-settings)).
frequência | número de Olá (opcional) de segundos entre a execução da consulta de Olá. Valor predefinido é de 300 (5 minutos) valor mínimo é de 15 segundos.
sinks | (opcional) Uma lista separada por vírgulas dos nomes dos resultados métrica não processados exemplo toowhich sinks adicionais deve ser publicada. Nenhuma agregação destes exemplos em bruto é calculada por extensão Olá ou por métricas do Azure.

O "tabela" ou "sinks" ou ambos, tem de ser especificados.

### <a name="filelogs"></a>fileLogs

Capturar Olá de controlos de ficheiros de registo. LAD captura novas linhas de texto que estes são escritos no ficheiro toohello e escreve-as linhas tootable e/ou qualquer sinks especificados (JsonBlob ou EventHub).

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Elemento | Valor
------- | -----
ficheiro | nome do caminho completo Olá da toobe de ficheiro de registo Olá observada e capturadas. Olá pathname tem o nome num único ficheiro; -Não é um diretório de nomes ou conter carateres universais.
Tabela | tabela de armazenamento do Azure Olá (opcional), no armazenamento de Olá designada de conta (conforme especificado na configuração de Olá protegido), em que novas linhas de Olá "seguimento" do ficheiro de Olá é escritos.
sinks | (opcional) Enviar uma lista separada por vírgulas dos nomes das linhas de registo de toowhich sinks adicionais.

O "tabela" ou "sinks" ou ambos, tem de ser especificados.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Métricas suportadas pelo fornecedor de builtin Olá

fornecedor de métrica de builtin Olá é uma origem de métricas mais interessante tooa conjunto amplo de utilizadores. Estas métricas enquadram-se a cinco classes abrangentes:

* Processador
* Memória
* Rede
* Sistema de ficheiros
* Disco

### <a name="builtin-metrics-for-hello-processor-class"></a>métricas de Builtin para Olá classe de processador

classe de processador de métricas de Olá fornece informações sobre a utilização do processador no Olá VM. Ao agregar percentagens, o resultado Olá é média Olá em todas as CPUs. No core dois VM, se um núcleo 100% ocupado e Olá outro era 100% inativo, Olá comunicadas que percentidletime seria 50. Se cada principal era 50% ocupado para Olá mesmo período, Olá comunicadas resultado também seria 50. Numa quatro core VM, com um núcleo 100% ocupado e Olá outros inativo, Olá comunicadas que percentidletime seria 75.

Contador | Significado
------- | -------
PercentIdleTime | Percentagem de tempo durante a janela de agregação de Olá que processadores foram ao executar o ciclo de inatividade de kernel Olá
percentProcessorTime | Percentagem de tempo de execução de um thread não inativo
PercentIOWaitTime | Percentagem de tempo à espera de e/s operações toocomplete
PercentInterruptTime | Percentagem de tempo de execução de hardware/software interrupções e DPCs (chamadas de procedimento diferidas)
PercentUserTime | De tempo não inativo durante a janela de agregação de Olá, percentagem de Olá de tempo despendido num utilizador mais com prioridade normal
PercentNiceTime | De tempo não inativo, Olá percentagem gasta em lowered prioridade (nice)
PercentPrivilegedTime | De tempo não inativo, Olá percentagem gasta no modo privilegiado (kernel)

Olá primeiro quatro contadores devem soma too100%. Olá últimos três contadores também soma too100%; Estes subdividir Olá soma de PercentProcessorTime, PercentIOWaitTime e PercentInterruptTime.

Definir tooobtain uma métrica único agregada para todos os processadores, `"condition": "IsAggregate=TRUE"`. tooobtain uma métrica para um processador específico, tal como o segundo processador lógico Olá de um quatro principais VM, defina `"condition": "Name=\\"1\\""`. Os números de processador lógico estão no intervalo de Olá `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>métricas de Builtin para Olá classe de memória

classe de memória de métricas de Olá fornece informações sobre a utilização da memória, paginação e trocar.

Contador | Significado
------- | -------
AvailableMemory | Memória física disponível no MiB
PercentAvailableMemory | Memória física disponível como uma percentagem do total de memória
UsedMemory | Na utilização memória física (MiB)
PercentUsedMemory | Em utilização memória física como percentagem do total de memória
PagesPerSec | Paginação total (leitura/escrita)
PagesReadPerSec | Páginas de ler a partir da cópia de arquivo (ficheiro de troca, os ficheiros de programa, ficheiro mapeado, etc.)
PagesWrittenPerSec | Páginas escritas toobacking armazenam (ficheiro de comutação, ficheiro mapeado, etc.)
AvailableSwap | Espaço de comutação utilizado (MiB)
PercentAvailableSwap | Espaço de comutação utilizado como uma percentagem de comutação total
UsedSwap | Na utilização de espaço de comutação (MiB)
PercentUsedSwap | Em utilização de espaço de comutação como uma percentagem de comutação total

Esta classe de métricas tem apenas uma única instância. atributo de "condição" Olá sem outras definições útil e deve ser omitido.

### <a name="builtin-metrics-for-hello-network-class"></a>métricas de Builtin para Olá classe de rede

classe de rede de métricas de Olá fornece informações sobre a atividade de rede em interfaces de rede individuais desde o arranque. LAD não expõe as métricas de largura de banda, que podem ser obtidas a partir de métricas de anfitrião.

Contador | Significado
------- | -------
BytesTransmitted | Total de bytes enviados desde o arranque
BytesReceived | Total de bytes recebidos desde o arranque
BytesTotal | Total de bytes enviadas ou recebidas desde o arranque
PacketsTransmitted | Total de pacotes enviados desde o arranque
PacketsReceived | Total de pacotes recebidos desde o arranque
TotalRxErrors | Número de recebe erros desde o arranque
TotalTxErrors | Número de erros de transmitir desde o arranque
TotalCollisions | Número de colisões é comunicado pelo portas de rede Olá desde o arranque

 Embora esta classe é instanced, LAD não suporta a captura as métricas da rede agregadas em todos os dispositivos de rede. métricas de Olá tooobtain para uma interface específica, tal como eth0, defina `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>métricas de Builtin para Olá classe do sistema de ficheiros

classe de sistema de ficheiros de métricas de Olá fornece informações sobre a utilização do sistema de ficheiros. Valores absoluto e percentagem são comunicados como seriam tooan apresentadas comum utilizador (não raiz).

Contador | Significado
------- | -------
FreeSpace | Espaço em disco disponível em bytes
UsedSpace | Espaço em disco em bytes utilizado
PercentFreeSpace | Percentagem de espaço livre
PercentUsedSpace | Percentagem de espaço utilizado
PercentFreeInodes | Percentagem de inodes não utilizadas
PercentUsedInodes | Percentagem de inodes alocado (em utilização) somadas em todos os sistemas de ficheiros instalados
BytesReadPerSecond | Bytes lidos por segundo
BytesWrittenPerSecond | Bytes escritos por segundo
BytesPerSecond | Bytes lidos ou escritos por segundo
ReadsPerSecond | Operações de leitura por segundo
WritesPerSecond | Operações por segundo de escrita
TransfersPerSecond | Operações de leitura ou escrita por segundo

Valores agregados em todos os sistemas de ficheiros podem ser obtidos através da definição `"condition": "IsAggregate=True"`. Os valores de um sistema de ficheiros montado específico, tal como "/ mnt", pode ser obtido através da definição `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>métricas de Builtin para Olá classe do disco

classe de disco de métricas de Olá fornece informações sobre a utilização do dispositivo de disco. Estas estatísticas aplicam toohello toda a unidade. Se existirem vários sistemas de ficheiros num dispositivo, os contadores de Olá desse dispositivo são, efetivamente, agregados em todos eles.

Contador | Significado
------- | -------
ReadsPerSecond | Operações de leitura por segundo
WritesPerSecond | Operações por segundo de escrita
TransfersPerSecond | Totais operações por segundo
AverageReadTime | Segundos média por operação de leitura
AverageWriteTime | Segundos média por operação de escrita
AverageTransferTime | Segundos média por operação
AverageDiskQueueLength | Número médio de operações de disco em fila
ReadBytesPerSecond | Número de bytes lidos por segundo
WriteBytesPerSecond | Número de bytes escritos por segundo
BytesPerSecond | Número de bytes lidos ou escritos por segundo

Valores agregados em todos os discos podem ser obtidos através da definição `"condition": "IsAggregate=True"`. informações de tooget para um dispositivo específico (por exemplo, dev/sdf1), definir `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Instalar e configurar LAD 3.0 através da CLI

Pressupondo que as definições de protegidos estão no ficheiro de Olá PrivateConfig.json e as informações de configuração pública estão a ser PublicConfig.json, execute este comando:

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

comando Olá parte do princípio de que está a utilizar o modo de gestão de recursos do Azure (arm) Olá de Olá CLI do Azure. tooconfigure LAD para implementação clássica VMs (ASM) do modelo, mude demasiado "asm" modo (`azure config mode asm`) e omitir o nome do grupo de recursos Olá no comando Olá. Para obter mais informações, consulte Olá [documentação da CLI de plataforma](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Uma configuração de exemplo LAD 3.0

Com base no Olá anterior a uma configuração de extensão de LAD 3.0 de exemplo com alguma explicação sobre as definições, aqui. tooapply caso tooyour deste exemplo, deve utilizar o seu próprio nome de conta de armazenamento, SAS token de conta e tokens EventHubs SAS.

### <a name="privateconfigjson"></a>PrivateConfig.json

Configuram estas definições privadas:

* uma conta de armazenamento
* um token SAS conta correspondente
* vários sinks (JsonBlob ou EventHubs com SAS tokens)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Estas definições públicas causam LAD para:

* Carregue as métricas de tempo de processador de percentagem e utilizado--espaço em disco toohello `WADMetrics*` tabela
* Carregar mensagens do syslog instalações "utilizador" e a gravidade "informações" toohello `LinuxSyslog*` tabela
* Carregar em bruto OMI consulta resultados (PercentProcessorTime e PercentIdleTime) toohello denominado `LinuxCPU` tabela
* Carregar anexadas linhas no ficheiro `/var/log/myladtestlog` toohello `MyLadTestLog` tabela

Em cada caso, os dados também são carregados para:

* Armazenamento de Blobs do Azure (nome do contentor é definido no sink de JsonBlob Olá)
* Ponto final de EventHubs (conforme especificado no receptor de EventHubs Olá)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Olá `resourceId` no Olá configuração tem de corresponder ao que de dimensionamento de máquina virtual VM ou Olá Olá definida.

* Métricas de plataforma do Azure charting e alertas sabe Olá resourceId de Olá VM que está a trabalhar. Dados de Olá toofind-espera para a VM utilizando a chave de pesquisa do Olá resourceId Olá.
* Se utilizar o dimensionamento automático do Azure, Olá resourceId na configuração de dimensionamento automático de Olá tem de corresponder ao resourceId Olá utilizado pelo LAD.
* Olá resourceId está incorporado no Olá os nomes de JsonBlobs escritas pelo LAD.

## <a name="view-your-data"></a>Ver os seus dados

Utilizar dados de desempenho do Olá tooview portal do Azure ou definir alertas:

![Imagem](./media/diagnostic-extension/graph_metrics.png)

Olá `performanceCounters` sempre os dados são armazenados uma tabela de armazenamento do Azure. APIs de armazenamento do Azure estão disponíveis para vários idiomas e plataformas.

Os dados enviados tooJsonBlob sinks são armazenados em blobs na conta do storage Olá com o nome no Olá [protegidos definições](#protected-settings). Pode consumir dados de BLOBs de Olá utilizando as APIs de armazenamento de Blobs do Azure.

Além disso, pode utilizar estes dados de Olá de tooaccess de ferramentas da IU no armazenamento do Azure:

* Explorador de servidores do Visual Studio.
* [Explorador de armazenamento do Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Explorador de armazenamento do Azure").

Este instantâneo de uma sessão do Explorador de armazenamento do Microsoft Azure mostra Olá gerado tabelas de armazenamento do Azure e contentores de uma extensão de LAD 3.0 configurada corretamente na VM de teste. imagem de Olá não corresponde exatamente ao hello [exemplo de configuração LAD 3.0](#an-example-lad-30-configuration).

![Imagem](./media/diagnostic-extension/stg_explorer.png)

Consulte Olá relevante [EventHubs documentação](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn como tooconsume mensagens publicadas tooan EventHubs endpoint.

## <a name="next-steps"></a>Passos seguintes

* Criar métricas alertas no [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) recolher com base nas métricas Olá.
* Criar [monitorização gráficos](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para as métricas.
* Saiba como demasiado[criar um conjunto de dimensionamento de máquina virtual](/azure/virtual-machines/linux/tutorial-create-vmss) utilizando o dimensionamento automático toocontrol de métricas.
