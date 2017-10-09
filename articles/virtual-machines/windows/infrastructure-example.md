---
title: "aaaExample instruções de infraestrutura do Azure | Microsoft Docs"
description: "Saiba mais sobre Olá chaves design e implementação diretrizes para implementar uma infraestrutura de exemplo no Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a>Instruções de infraestrutura do Azure de exemplo para VMs do Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Este artigo explica de conceção de uma infraestrutura de aplicação de exemplo. Iremos detalhe conceber uma infraestrutura para uma loja online simple que reúne todas as diretrizes de Olá e decisões à volta de convenções de nomenclatura, conjuntos de disponibilidade, redes virtuais e Balanceadores de carga e a implementação, na verdade, as máquinas virtuais (VMs).

## <a name="example-workload"></a>Carga de trabalho de exemplo
Adventure Works Cycles pretende toobuild uma aplicação da loja online no Azure que é composta por:

* Dois servidores IIS que executem cliente Olá front-end numa camada web
* Dois servidores IIS processar dados e as ordens de uma camada de aplicação
* Duas instâncias do Microsoft SQL Server com grupos de Disponibilidade AlwaysOn (dois servidores do SQL Server e um testemunho de nó maioria) para armazenar dados de produto e as ordens numa camada de base de dados
* Dois controladores de domínio do Active Directory para contas de cliente e fornecedores uma camada de autenticação
* Todos os servidores de Olá estão localizados em duas sub-redes:
  * uma sub-rede para servidores de web de Olá front-end 
  * uma sub-rede de back-end para servidores de aplicação Olá, cluster do SQL Server e os controladores de domínio

![Diagrama de diferentes camadas para a infraestrutura de aplicação](./media/infrastructure-example/example-tiers.png)

Entrada segura tráfego web tem de ser com balanceamento de carga entre servidores de web de Olá clientes procurar loja online Olá. Ordem de processamento de tráfego num formulário de Olá de pedidos de HTTP da web de Olá servidores devem ser balanceados entre servidores de aplicação Olá. Além disso, a infraestrutura de Olá têm de ser concebida para elevada disponibilidade.

design resultante Olá tem de incorporar:

* Uma conta e subscrição do Azure
* Um grupo de recursos única
* Managed Disks do Azure
* Uma rede virtual com duas sub-redes
* Conjuntos de disponibilidade para Olá VMs com uma função semelhante
* Máquinas virtuais

Todos os Olá acima siga estas convenções de nomenclatura:

* Adventure Works Cycles utiliza **[carga de trabalho IT]-[localização]-[recursos do Azure]** como prefixo
  * Neste exemplo, "**azos**" (Azure on-line loja) é Olá nome de carga de trabalho de TI e "**utilizar**" (EUA Leste 2) é a localização de Olá
* Redes virtuais utilizam AZOS-utilização-VN**[número]**
* Conjuntos de disponibilidade utilizam azos-utilizar-como-**[função]**
* Nomes de máquina virtual utilizar azos-utilizar-vm -**[vmname]**

## <a name="azure-subscriptions-and-accounts"></a>Contas e as subscrições do Azure
Adventure Works Cycles está a utilizar a subscrição do Enterprise, com o nome de subscrição no Adventure Works Enterprise, tooprovide faturação para esta carga de trabalho IT.

## <a name="storage"></a>Armazenamento
Adventure Works Cycles determinar que utilizam discos gerida do Azure. Durante a criação de VMs, ambas as camadas de armazenamento disponível armazenamento são utilizadas:

* **Armazenamento Standard** para servidores de web de Olá, servidores de aplicações e controladores de domínio e os respetivos discos de dados.
* **Armazenamento Premium** para Olá VMs do SQL Server e os respetivos discos de dados.

## <a name="virtual-network-and-subnets"></a>Rede virtual e sub-redes
Porque a rede virtual Olá não precisa de rede no local do conectividade em curso toohello Adventure ciclos de trabalho, estes decidiu numa rede virtual apenas na nuvem.

Estes criaram uma rede virtual apenas na nuvem com Olá definições Olá portal do Azure a utilizar os seguintes:

* Nome: AZOS-utilização-VN01
* Localização: EUA Leste 2
* Espaço de endereços de rede virtual: 10.0.0.0/8
* Primeira sub-rede:
  * Nome: front-end
  * Espaço de endereços: 10.0.1.0/24
* Segunda sub-rede:
  * Nome: back-end
  * Espaço de endereços: 10.0.2.0/24

## <a name="availability-sets"></a>Conjuntos de disponibilidade
toomaintain elevada disponibilidade de todos os escalões de quatro da respetiva loja online, Adventure Works Cycles assim sendo, optou em quatro conjuntos de disponibilidade:

* **azos utilize como web** para servidores de web de Olá
* **azos utilize como aplicação** Olá para servidores de aplicações
* **azos utilize como sql** para Olá servidores SQL
* **azos utilize como dc** Olá para controladores de domínio

## <a name="virtual-machines"></a>Máquinas virtuais
Adventure Works Cycles decidir Olá os seguintes nomes para as respetivas VMs do Azure:

* **azos-utilização-vm-web01** para o primeiro servidor de web Olá
* **azos-utilização-vm-web02** para o segundo servidor de web Olá
* **azos-utilização-vm-app01** para o primeiro servidor de aplicação Olá
* **azos-utilização-vm-app02** para o segundo servidor de aplicação Olá
* **azos-utilização-vm-sql01** para o servidor do SQL Server primeiro Olá num cluster de Olá
* **azos-utilização-vm-sql02** para o servidor do SQL Server segundo Olá num cluster de Olá
* **azos-utilização-vm-dc01** Olá primeiro controlador de domínio
* **azos-utilização-vm-dc02** Olá segundo controlador de domínio

Segue-se a configuração resultante Olá.

![Infraestrutura de aplicação final implementada no Azure](./media/infrastructure-example/example-config.png)

Incorpora esta configuração:

* Uma rede virtual apenas na nuvem com duas sub-redes (front-end e back-end)
* Discos do Azure gerida com discos Standard e Premium
* Quatro conjuntos de disponibilidade, um para cada camada do loja online Olá
* máquinas virtuais Olá de camadas de Olá quatro
* Um conjunto com balanceamento de carga externo para o tráfego de web baseado em HTTPS de servidores web do Olá Internet toohello
* Conjunto para o tráfego de web não encriptada de servidores de aplicações de toohello de servidores web Olá com balanceamento de uma carga interno
* Um grupo de recursos única