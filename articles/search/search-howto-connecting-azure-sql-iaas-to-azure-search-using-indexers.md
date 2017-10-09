---
title: "aaaSQL VM ligação tooAzure pesquisa | Microsoft Docs"
description: "Ativar ligações encriptadas e configurar Olá firewall tooallow ligações tooSQL servidor uma máquina virtual do Azure (VM) de um indexador na Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Configurar uma ligação a partir de um tooSQL do indexador de Azure Search Server numa VM do Azure
Conforme indicado no [tooAzure de ligar a base de dados de SQL do Azure a procura utilizando indexadores](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), criação de indexadores contra **do SQL Server em VMs do Azure** (ou **VMs do SQL do Azure** para abreviar) é suportado pela pesquisa do Azure, mas existem alguns pré-requisitos relacionadas com segurança tootake care of primeiro. 

**Duração de tarefa:** cerca de 30 minutos, assumindo que já instalado um certificado no Olá VM.

## <a name="enable-encrypted-connections"></a>Ativar ligações encriptadas
A pesquisa do Azure necessita de um canal encriptado para todos os pedidos de indexador através de uma ligação à internet pública. Esta secção lista Olá passos toomake este trabalho.

1. Verificar as propriedades de Olá de Olá certificado tooverify Olá nome do requerente é o nome de domínio completamente qualificado (FQDN) Olá de Olá VM do Azure. Pode utilizar uma ferramenta como CertUtils ou Olá propriedades de Olá tooview snap-in de certificados. Pode obter Olá FQDN a partir Essentials secção do painel de Olá, VM serviço, Olá **etiqueta de nome de endereço de IP público/DNS** campo, no Olá [portal do Azure](https://portal.azure.com/).
   
   * Para VMs criadas utilizando Olá mais recente **Resource Manager** modelo, Olá FQDN é formatada como `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Para as VMs mais antigas, criadas como um **clássico** VM, Olá FQDN é formatado como `<your-cloud-service-name.cloudapp.net>`. 
2. Para configurar SQL Server toouse Olá utilizando Olá Editor de registo (regedit). 
   
    Apesar do Gestor de configuração do SQL Server é frequentemente utilizado para esta tarefa, não é possível utilizá-lo para este cenário. Não irá localizar Olá importou o certificado porque Olá FQDN do Olá VM no Azure não corresponde ao hello FQDN, conforme determinado pela Olá VM (identifica domínio Olá como computador local Olá ou toowhich de domínio de rede de Olá que é associado). Quando os nomes não corresponderem, utilize o certificado do regedit toospecify Olá.
   
   * No regedit, procure a chave de registo toothis: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Olá `[MSSQL13.MSSQLSERVER]` parte varia com base no nome de versão e instância. 
   * Defina o valor de Olá de Olá **certificado** toohello chave **thumbprint** do certificado SSL Olá importados toohello VM.
     
     Existem várias formas tooget Olá impressão digital, algumas melhor do que outras pessoas. Se copiar de Olá **certificados** snap-in MMC,, provavelmente, selecionará um caráter à esquerda invisível [conforme descrito neste artigo de suporte](https://support.microsoft.com/kb/2023869/), que resulta num erro quando tenta uma ligação. Existem várias soluções para corrigir este problema. Olá mais fácil é toobackspace ativação pós-falha e, em seguida, volte a escrever primeiro caráter de Olá de Olá thumbprint tooremove Olá à esquerda caráter no campo de valor de chave Olá regedit. Em alternativa, pode utilizar um thumbprint de Olá toocopy ferramenta diferentes.
3. Conceda permissões de conta de serviço toohello. 
   
    Certifique-se Olá conta de serviço do SQL Server é concedido permissões adequadas na chave privada Olá do certificado SSL Olá. Se overlook neste passo, não irá iniciar o SQL Server. Pode utilizar Olá **certificados** snap-in ou **CertUtils** para esta tarefa.
4. Reinicie o serviço do SQL Server Olá.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>Configurar a conectividade do SQL Server no Olá VM
Depois de configurar a ligação de Olá encriptado necessária para a Azure Search, existem configuração adicional passos intrínseco tooSQL Server em VMs do Azure. Se não tiver o feito, Olá passo seguinte consiste em configuração de toofinish utilizando um dos seguintes artigos:

* Para um **Resource Manager** VM, consulte [ligar tooa Máquina Virtual do servidor SQL no Azure com o Resource Manager](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* Para um **clássico** VM, consulte [ligar tooa Máquina Virtual do servidor SQL no Azure clássico](../virtual-machines/windows/classic/sql-connect.md).

Em particular, reveja a secção de Olá cada artigo para "que ligam através de Olá internet".

## <a name="configure-hello-network-security-group-nsg"></a>Configurar Olá grupo de segurança de rede (NSG)
Não é pouco usual tooconfigure Olá NSG e ponto final do Azure correspondente ou lista de controlo de acesso (ACL) toomake partes de tooother acessível sua VM do Azure. Possibilidades são que tiver terminado antes tooallow o seus próprios tooyour de tooconnect de lógica de aplicação VM do SQL do Azure. É igual para um tooyour de ligação da Azure Search VM do SQL do Azure. 

ligações de Olá abaixo fornecem instruções sobre a configuração do NSG para implementações de VM. Utilize estas instruções que tooacl um ponto final da Azure SEarch com base no respetivo endereço IP.

> [!NOTE]
> Para em segundo plano, consulte [que é um grupo de segurança de rede?](../virtual-network/virtual-networks-nsg.md)
> 
> 

* Para um **Resource Manager** VM, consulte [como toocreate NSGs para implementações de ARM](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* Para um **clássico** VM, consulte [como toocreate NSGs para implementações clássicas](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

Endereçamento IP pode apresentam alguns desafios que são facilmente ultrapassar se tem conhecimento do problema Olá e possíveis soluções. secções restantes Olá fornecem recomendações para lidar com problemas relacionados tooIP endereços Olá ACL.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Restringir o endereço IP do serviço de pesquisa do acesso toohello
Recomendamos vivamente que restringir o endereço IP do Olá acesso toohello do seu serviço de pesquisa na Olá ACL em vez de efetuar as VMs do Azure SQL Server ao nível abrir tooany pedidos de ligação. Pode encontrar facilmente Olá IP endereço efetuando Olá FQDN (por exemplo, `<your-search-service-name>.search.windows.net`) do seu serviço de pesquisa.

#### <a name="managing-ip-address-fluctuations"></a>Gerir flutuações de endereço IP
Se o serviço de pesquisa tem apenas uma unidade de pesquisa (ou seja, uma réplica e uma partição), o endereço IP de Olá será alterado durante a reinicialização de rotina do serviço, invalidar uma ACL existente com o endereço IP do seu serviço de pesquisa.

Erro de conectividade subsequentes tooavoid unidirecional Olá é toouse mais do que uma réplica e uma partição na Azure Search. Se o fizer, aumenta o custo de Olá, mas que também resolve problema de endereço IP de Olá. Na Azure Search, endereços IP não alterar quando tem mais do que uma unidade de pesquisa.

Uma abordagem segundo é tooallow Olá ligação toofail e, em seguida, reconfigurar Olá ACLs no Olá NSG. Em média, que pode esperar toochange de endereços IP cada algumas semanas. Para os clientes que efetue a indexação controlada de forma pouco frequente, esta abordagem poderá ser viável.

Uma abordagem de viável (mas não segura particularmente) terceira é toospecify Olá intervalo de endereços IP Olá região do Azure onde o serviço de pesquisa está aprovisionado. lista de Olá de intervalos de IP a partir do qual os endereços IP públicos são atribuídos recursos de tooAzure está publicada no [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Incluir Olá da Azure Search endereços IP portal
Se estiver a utilizar Olá toocreate do portal do Azure, um indexador, lógica portal do Azure Search também precisa de acesso tooyour VM do Azure SQL durante a hora de criação. Endereços IP portais de pesquisa do Azure podem ser encontrados efetuando `stamp2.search.ext.azure.com`.

## <a name="next-steps"></a>Passos seguintes
Com a configuração fora de forma Olá, agora pode especificar um SQL Server numa VM do Azure como origem de dados de Olá para um indexador de Azure Search. Consulte [tooAzure de ligar a base de dados de SQL do Azure a procura utilizando indexadores](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) para obter mais informações.

