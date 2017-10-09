---
title: aaaViewing e modificar Hostnames | Microsoft Docs
description: "Como tooview e alteração de nomes de anfitrião para máquinas virtuais do Azure, web e funções de trabalho para resolução de nomes"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Ver e modificar os nomes de anfitrião
tooallow sua toobe de instâncias de função referenciada por nome de anfitrião, tem de definir Olá valor para o nome de anfitrião Olá no ficheiro de configuração do serviço de Olá para cada função. Pode fazê-lo ao adicionar toohello de nome de anfitrião Olá pretendido **vmName** atributo de Olá **função** elemento. Olá, valor de Olá **vmName** atributo é utilizado como base para o nome de anfitrião Olá de cada instância de função. Por exemplo, se **vmName** é *webrole* e existem três instâncias de função, os nomes de anfitrião de Olá de instâncias de Olá *webrole0*, *webrole1* , e *webrole2*. Não é necessário toospecify um nome de anfitrião para máquinas virtuais no ficheiro de configuração de Olá, porque o nome de anfitrião Olá para uma máquina virtual é preenchido com base no nome da máquina virtual Olá. Para obter mais informações sobre como configurar um serviço do Microsoft Azure, consulte [esquema de configuração de serviço do Azure (. cscfg ficheiro)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>Ver os nomes de anfitrião
Pode ver os nomes de anfitrião de Olá de máquinas virtuais e instâncias de função num serviço em nuvem, utilizando qualquer uma das ferramentas de Olá abaixo.

### <a name="azure-portal"></a>Portal do Azure
Pode utilizar Olá [portal do Azure](http://portal.azure.com) nomes de anfitrião de Olá tooview para máquinas virtuais no painel de descrição geral de Olá para uma máquina virtual. Tenha em atenção que Olá painel mostra um valor para **nome** e **nome de anfitrião**. Apesar de estarem inicialmente Olá mesmo, a alteração de nome de anfitrião Olá não irá alterar o nome de Olá da máquina virtual de Olá ou instância de função.

Instâncias de função também podem ser visualizadas no Olá portal do Azure, mas quando listar as instâncias de Olá num serviço em nuvem, o nome de anfitrião Olá não é apresentado. Verá um nome para cada instância, mas esse nome não representa o nome de anfitrião Olá.

### <a name="service-configuration-file"></a>Ficheiro de configuração de serviço
Pode transferir o ficheiro de configuração do serviço de Olá para um serviço implementado de Olá **configurar** painel de serviço de Olá do Olá portal do Azure. Em seguida, pode procurar Olá **vmName** atributo para Olá **nome da função** nome de anfitrião do elemento toosee Olá. Tenha em atenção que este nome de anfitrião é utilizado como base para o nome de anfitrião Olá de cada instância de função. Por exemplo, se **vmName** é *webrole* e existem três instâncias de função, os nomes de anfitrião de Olá de instâncias de Olá *webrole0*, *webrole1* , e *webrole2*.

### <a name="remote-desktop"></a>Ambiente de trabalho remoto
Depois de ativar o ambiente de trabalho remoto (Windows), comunicação remota do Windows PowerShell (Windows), ou ligações de SSH (Linux e Windows) tooyour máquinas de virtuais ou instâncias de função, pode ver o nome de anfitrião de Olá partir de uma ligação de ambiente de trabalho remoto Active Directory de várias formas:

* Escreva o nome do anfitrião na linha de comandos de Olá ou SSH terminal.
* Escreva o ipconfig/todas as na comando Olá (apenas Windows) de linha de comandos.
* Nome do computador Olá vista no sistema de Olá definições (apenas Windows).

### <a name="azure-service-management-rest-api"></a>REST API de gestão de serviço do Azure
De um cliente REST, siga estas instruções:

1. Certifique-se de que tem um toohello de tooconnect de certificado de cliente portal do Azure. tooobtain um certificado de cliente, siga os passos de Olá apresentados [como: transferir e importar definições de publicação e informações de subscrição](https://msdn.microsoft.com/library/dn385850.aspx). 
2. Defina uma entrada de cabeçalho x-ms-version com um valor de 2013-11-01 com o nome.
3. Enviar um pedido no Olá seguinte formato: https://management.core.windows.net/\<subscrition id\>/services/hostedservices/\<nome do serviço\>? detalhes incorporar = true
4. Procure Olá **HostName** elemento para cada **RoleInstance** elemento.

> [!WARNING]
> Também pode ver o sufixo de domínio interno de Olá do serviço em nuvem da resposta de chamada REST de Olá verificando Olá **InternalDnsSuffix** elemento, ou executando o ipconfig/todas as numa linha de comandos numa sessão de ambiente de trabalho remoto (Windows) ou, em execução cat /etc/resolv.conf de um terminal SSH (Linux).
> 
> 

## <a name="modifying-a-hostname"></a>Modificar um nome de anfitrião
Pode modificar o nome de anfitrião de Olá para qualquer máquina virtual ou instância de função através do carregamento de um ficheiro de configuração do serviço modificado ou mudar o nome de computador Olá partir de uma sessão de ambiente de trabalho remoto.

## <a name="next-steps"></a>Passos seguintes
[Resolução de nomes (DNS)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Esquema de configuração do serviço do Azure (. cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Esquema de configuração de rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Especifique as definições de DNS a utilizar ficheiros de configuração de rede](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

