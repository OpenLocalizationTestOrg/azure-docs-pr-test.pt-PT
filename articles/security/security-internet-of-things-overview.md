---
title: aaaSecure a Internet das coisas (IoT) no Azure | Microsoft Docs
description: " Azure internet dos serviços de coisas (IoT) oferecem uma vasta gama de capacidades. Este artigo ajuda-o a compreender como toosecure suas soluções de IoT no Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>Descrição geral de segurança da Internet das coisas
Azure internet dos serviços de coisas (IoT) oferecem uma vasta gama de capacidades. Estes serviços de nível empresarial permitem-lhe:

* Recolher dados de dispositivos
* Analisar fluxos de dados em movimento
* Armazenar e consultar grandes conjuntos de dados
* Visualizar dados em tempo real e dados históricos
* Integrar com sistemas de back-office

toodeliver estas capacidades, o Azure IoT Suite reúne vários Azure serviços com extensões personalizadas, como soluções pré-configuradas. Estas soluções pré-configuradas são implementações de base de padrões de solução IoT comuns que o ajudam a hora de Olá tooreduce que demorar toodeliver suas soluções de IoT. Utilizar kits de desenvolvimento de software de IoT Olá, pode personalizar e expandir estas soluções toomeet os seus requisitos. Também pode utilizar estas soluções como exemplos ou modelos quando estiver a desenvolver novas soluções de IoT.

Olá IoT do Azure suite é uma solução poderosa para as suas necessidades de IoT. No entanto, é importância upmost que as suas soluções de IoT concebidas com segurança em mente desde o início de Olá. Devido a Olá sheer número de dispositivos de IoT qualquer incidente de segurança pode tornar rapidamente um evento ampla com consequências significativas.

toohelp que compreende como toosecure suas soluções de IoT, temos Olá informações a seguir.

## <a name="security-architecture"></a>Arquitetura de segurança
Ao conceber um sistema, é importante toounderstand Olá ameaças toothat sistema e adicionar defesas adequadas em conformidade, como sistema de Olá é concebido e criado de. É importante toodesign Olá produto Olá início com segurança em mente, porque a compreender como um atacante poderá ser capaz de toocompromise um sistema de ajuda Certifique-se mitigações adequadas estão no local a partir do início de Olá.

Pode saber mais sobre a arquitetura de segurança de IoT através da leitura [Internet das coisas segurança arquitetura](../iot-suite/iot-security-architecture.md).

Este artigo aborda Olá os seguintes tópicos:

* [Segurança começa com um modelo de ameaça](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [Segurança de IoT](../iot-suite/iot-security-architecture.md#security-in-iot)
* [Olá de modelação de ameaça arquitetura de referência do IoT do Azure](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Segurança de Olá fundo cópias de segurança
Olá IoT pode representar um único segurança, privacidade e conformidade desafios toobusinesses em todo o mundo. Ao contrário de tecnologia de informático tradicional onde estes problemas está centrada no software e como é implementado, o IoT seja relativo o que acontece quando Olá informático e universos físico Olá convergir. Proteger soluções de IoT requer garantir segura de aprovisionamento de dispositivos, conectividade segura entre estes dispositivos e a nuvem de Olá e a proteção de proteger os dados na nuvem de Olá durante o processamento e armazenamento. Trabalhar com essas funcionalidades, no entanto, são dispositivos restrita de recursos, distribuição geográfica dos implementações e muitos dispositivos dentro de uma solução.

Pode saber como segurança toohandle nas seguintes áreas lendo [segurança da Internet das coisas de Olá fundo](../iot-suite/securing-iot-ground-up.md).

artigo de Olá aborda Olá os seguintes tópicos:

* [Proteger a infraestrutura de Olá fundo cópias de segurança](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure – segura IoT infraestrutura para a sua empresa](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>Melhores práticas
Proteger uma infraestrutura de IoT requer uma estratégia de segurança-na profundidade rigorosas. De proteger dados numa nuvem Olá, proteger a integridade dos dados enquanto em trânsito através de Olá internet pública, dispositivos de aprovisionamento de toosecurely, cada camada baseia-se maior garantia de segurança Olá infraestrutura global.

Pode saber sobre a segurança da Internet das coisas melhores práticas através da leitura [práticas recomendadas de segurança de Internet das coisas](../iot-suite/iot-security-best-practices.md).

artigo de Olá aborda Olá os seguintes tópicos:

* [Fabricante de hardware de IoT/integrador](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [Para programadores de solução IoT](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [Implementador de solução IoT](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [Operador de solução IoT](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
