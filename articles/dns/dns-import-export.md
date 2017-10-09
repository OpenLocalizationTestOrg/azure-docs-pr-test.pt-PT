---
title: "aaaImport e exportar uma zona de domínio do ficheiro tooAzure DNS utilizando a CLI do Azure 1.0 | Microsoft Docs"
description: Saiba como tooimport e exportar um DNS zona ficheiro tooAzure DNS ao utilizar a CLI do Azure 1.0
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Importar e exportar um ficheiro de zona DNS utilizando Olá CLI do Azure 1.0 

Este artigo explica como como tooimport e exportar ficheiros de zona DNS para utilizar o DNS do Azure Olá CLI do Azure 1.0.

## <a name="introduction-toodns-zone-migration"></a>Migração de zona de tooDNS de introdução

Um ficheiro de zona DNS é um ficheiro de texto que contém os detalhes de cada registo de sistema de nomes de domínio (DNS) na zona de Olá. Segue um formato de padrão, tornando adequado para transferir os registos DNS entre sistemas DNS. Utilizando um ficheiro de zona é um rápido, fiável e uma forma conveniente tootransfer uma zona DNS ou a sair DNS do Azure.

O DNS do Azure suporta a importar e exportar ficheiros de zona utilizando Olá interface de linha de comandos (CLI) do Azure. Importar de ficheiro de zona é **não** atualmente suportados através do Azure PowerShell ou Olá portal do Azure.

Olá CLI do Azure 1.0 é uma ferramenta de linha de comandos de várias plataformas utilizada para gestão de serviços do Azure. Está disponível para a plataformas Windows, Mac e Linux Olá de Olá [página de transferências do Azure](https://azure.microsoft.com/downloads/). Suporte em várias plataformas é importante para importar e exportar ficheiros de zona, porque Olá software de servidor de nome mais comuns, [VINCULAR](https://www.isc.org/downloads/bind/), normalmente, é executado no Linux.

> [!NOTE]
> Não existem atualmente duas versões do Olá CLI do Azure. CLI1.0 baseia-se no Node.js e tem de comandos a partir "azure".
> CLI2.0 baseia-se no Python e tem de começar com "az" de comandos. Ao importar de ficheiro de zona é suportado em ambas as versões, recomendamos que utilize comandos CLI1.0 Olá, conforme descrito nesta página.

## <a name="obtain-your-existing-dns-zone-file"></a>Obter o ficheiro de zona DNS existente

Antes de importar um ficheiro de zona DNS no DNS do Azure, terá de tooobtain uma cópia do ficheiro de zona Olá. origem deste ficheiro Olá depende em que zona DNS Olá está alojada atualmente.

* Se a zona DNS for alojada por um serviço de parceiro (por exemplo, um de domínios, o fornecedor de alojamento DNS dedicado ou o fornecedor de nuvem alternativo), que o serviço deve fornecer o ficheiro de zona DNS toodownload Olá Olá capacidade.
* Se a sua zona DNS estiver alojada no DNS do Windows, a pasta de predefinida de Olá para ficheiros de zona Olá é **%systemroot%\system32\dns**. ficheiro de zona do Olá caminho completo tooeach também mostra no Olá **geral** separador da consola do DNS Olá.
* Se a sua zona DNS estiver alojada utilizando o ENLACE, localização Olá do ficheiro de zona Olá para cada zona é especificada no ficheiro de configuração de ENLACE Olá **named.conf**.

> [!NOTE]
> Ficheiros de zona transferidos da GoDaddy tem um formato ligeiramente não padrão. É necessário toocorrect isto antes de importar estes ficheiros de zona no DNS do Azure.
>
> Nomes DNS no Olá RDATA de cada registo DNS estão especificados como nomes totalmente qualificados, mas não têm um terminar "." Isto significa que são interpretados por outros sistemas DNS como nomes relativos. Terá de tooedit Olá zona ficheiro tooappend Olá terminar "." tootheir nomes antes de importá-los no DNS do Azure.
>
> Por exemplo, Olá Registro CNAME "www 3600 em CNAME contoso.com" deve ser alterada demasiado "www 3600 CNAME em contoso.com."
> (com um terminar ".").

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Importar um ficheiro de zona DNS para o DNS do Azure

Importar um ficheiro de zona cria uma nova zona no DNS do Azure se ainda não existir. Se já existir uma zona de Olá, hello conjuntos de registos no ficheiro de zona Olá têm de ser intercalados com conjuntos de registos existente Olá.

### <a name="merge-behavior"></a>Comportamento de intercalação

* Por predefinição, os conjuntos de registos existentes e novos são intercalados. Os registos idênticos dentro de um conjunto de registo intercalado são anular duplicados.
* Em alternativa, especificando Olá `--force` opção, Olá substitui do processo de importação conjuntos de registos existente com novos conjuntos de registos. Conjuntos de registos existentes que não têm um registo correspondente definido no ficheiro de zona importado de Olá não são removidos.
* Quando os conjuntos de registos são intercalados, hello tempo toolive (TTL) pré-existentes de conjuntos de registos é utilizado. Quando `--force` é utilizado, Olá TTL do novo conjunto de registos Olá é utilizado.
* Início de parâmetros de autoridade (SOA) (exceto `host`) sempre são obtidas a partir do ficheiro de zona importado Olá, independentemente `--force` é utilizado. Da mesma forma, para Olá nome servidor conjunto de registos no vértice da zona de Olá, hello TTL é sempre retirado do ficheiro de zona importado Olá.
* Um registo CNAME importado não substituir um CNAME existente com Olá, a menos que o mesmo nome de registo Olá `--force` parâmetro for especificado.
* Quando for um conflito entre um registo CNAME e outro registo do mesmo nome mas diferentes de Olá escreva (independentemente de qual é existente ou nova), o registo existente Olá é mantido. Isto é independente da utilização de Olá de `--force`.

### <a name="additional-information-about-importing"></a>Informações adicionais sobre como importar

Olá notas seguintes fornecem detalhes técnicos adicionais sobre a zona de Olá importar processo.

* Olá `$TTL` diretiva é opcional e é suportada. Quando não existe nenhum `$TTL` diretiva é atribuída, os registos sem um valor de TTL explícito são importados predefinir tooa TTL de 3600 segundos. Quando dois regista no hello mesmo conjunto de registos especifique TTLs diferentes, é utilizado o valor mais baixo Olá.
* Olá `$ORIGIN` diretiva é opcional e é suportada. Quando não existe nenhum `$ORIGIN` estiver definido, predefinição Olá utilizado o valor é o nome da zona Olá conforme especificado na linha de comandos Olá (juntamente com a terminar Olá ".").
* Olá `$INCLUDE` e `$GENERATE` diretivas não são suportadas.
* Estes tipos de registos são suportados: A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.
* Olá registo SOA é automaticamente criada pelo DNS do Azure quando é criada uma zona. Quando importar um ficheiro de zona, todos os parâmetros SOA são obtidos a partir do ficheiro de zona Olá *exceto* Olá `host` parâmetro. Este parâmetro utiliza o valor de Olá fornecido pelo DNS do Azure. Isto acontece porque este parâmetro deve referir-se o servidor de nome principal de toohello fornecido pelo DNS do Azure.
* também, o registo de servidor de nome de Olá definido no vértice da zona de Olá é criado automaticamente pelo DNS do Azure quando Olá zona é criada. Apenas hello TTL deste conjunto de registos é importado. Estes registos contenham nomes dos servidores de nome Olá fornecidos pelo DNS do Azure. dados do registo Olá não são substituídos pelos valores Olá contidos no ficheiro de zona importado Olá.
* Durante a pré-visualização pública, o DNS do Azure suporta apenas registos TXT de cadeia única. Os registos TXT multistring são ser too255 concatenada e truncada carateres.

### <a name="cli-format-and-values"></a>Formato CLI e valores

formato de Olá do Olá CLI do Azure comando tooimport uma zona DNS é:

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Valores:

* `<resource group>`é o nome de Olá Olá do grupo de recursos para a zona de Olá no DNS do Azure.
* `<zone name>`é o nome de Olá da zona de Olá.
* `<zone file name>`é Olá/nome de caminho de Olá zona ficheiro toobe importado.

Se não existir uma zona com este nome no grupo de recursos de Olá, é criado para si. Se hello zona já existir, hello conjuntos de registos importados são intercalados com os conjuntos de registos existentes. toooverwrite Olá existente conjuntos de registos, utilize Olá `--force` opção.

formato de Olá tooverify de um ficheiro de zona sem realmente importá-lo, utilize Olá `--parse-only` opção.

### <a name="step-1-import-a-zone-file"></a>Passo 1. Importar um ficheiro de zona

tooimport um ficheiro de zona para a zona de Olá **contoso.com**.

1. Inicie sessão no tooyour subscrição do Azure utilizando Olá CLI do Azure 1.0.

    ```azurecli
    azure login
    ```

2. Selecione a subscrição de olá onde pretende toocreate a nova zona DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. O DNS do Azure é um serviço de só de Gestor de recursos do Azure, para que Olá CLI do Azure tem de ser desativados tooResource Manager modo.

    ```azurecli
    azure config mode arm
    ```

4. Antes de utilizar o serviço de DNS do Azure Olá, tem de registar o fornecedor de recursos do subscrição toouse Olá Network. (Esta é uma operação única para cada subscrição.)

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Se ainda não tiver uma, terá também de toocreate um grupo de recursos do Resource Manager.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. zona de Olá tooimport **contoso.com** do ficheiro de Olá **contoso.com.txt** para uma nova zona DNS no grupo de recursos de Olá **myresourcegroup**, execute o comando de Olá `azure network dns zone import`.<BR>Este comando carrega o ficheiro de zona Olá e analisá-lo. comando Olá executa uma série de comandos na zona de Olá de toocreate de serviço DNS do Azure Olá e conjuntos de todos os registos de Olá na zona de Olá. comando Olá comunica o progresso na janela de consola Olá, juntamente com quaisquer erros ou avisos. Porque os conjuntos de registos são criados em série, poderá demorar alguns minutos tooimport um ficheiro de zona grandes.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>Passo 2. Certifique-se a zona de Olá

tooverify Olá zona DNS depois de importar o ficheiro de Olá, pode utilizar qualquer um dos seguintes métodos de Olá:

* Pode listar os registos de Olá utilizando Olá os seguintes comandos da CLI do Azure:

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* Pode listar os registos de Olá utilizando o cmdlet do PowerShell Olá `Get-AzureRmDnsRecordSet`.
* Pode utilizar `nslookup` tooverify resolução de nomes para os registos de Olá. Porque zona Olá não delegada ainda, terá de servidores de nomes de DNS do Azure corretos do toospecify Olá explicitamente. Olá exemplo seguinte mostra como tooretrieve Olá nomes de servidor atribuído toohello zona. IT também mostra como tooquery Olá "www" registar utilizando `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>Passo 3. Atualizar delegação de DNS

Depois de ter verificado que zona Olá foi importada corretamente, tem de tooupdate Olá DNS delegação toopoint toohello nomes DNS do Azure que servidores. Para obter mais informações, consulte o artigo de Olá [atualizar delegação de DNS Olá](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Exportar um ficheiro de zona DNS do DNS do Azure

formato de Olá do Olá CLI do Azure comando tooimport uma zona DNS é:

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Valores:

* `<resource group>`é o nome de Olá Olá do grupo de recursos para a zona de Olá no DNS do Azure.
* `<zone name>`é o nome de Olá da zona de Olá.
* `<zone file name>`é Olá/nome de caminho de Olá zona ficheiro toobe exportado.

Como a importação de zona Olá, terá primeiro toosign no, escolha a sua subscrição e configurar o modo de Gestor de recursos de toouse Olá CLI do Azure.

### <a name="tooexport-a-zone-file"></a>tooexport um ficheiro de zona

1. Inicie sessão no tooyour subscrição do Azure utilizando Olá CLI do Azure.

    ```azurecli
    azure login
    ```

2. Selecione a subscrição de olá onde pretende toocreate sua zona DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. O DNS do Azure é um serviço de só de Gestor de recursos do Azure. Olá CLI do Azure tem de ser desativados tooResource Manager modo.

    ```azurecli
    azure config mode arm
    ```

4. tooexport Olá zona DNS do Azure existente **contoso.com** no grupo de recursos **myresourcegroup** toohello ficheiro **contoso.com.txt** (na pasta atual Olá), execute `azure network dns zone export`. Este comando chamadas Olá tooenumerate de serviço DNS do Azure conjuntos de registos na zona de Olá e exporte o ficheiro de zona do Olá resultados tooa compatível com o ENLACE.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
