---
title: "aaaInternet das práticas recomendadas de segurança de coisas | Microsoft Docs"
description: "artigo de Olá fornece uma lista organizada de Microsoft Internet das coisas segurança melhores práticas e recomendações gerais."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>Internet das coisas segurança melhores práticas
A infraestrutura de Internet das coisas (IoT) do proteger Olá é um undertaking crítico para todas as pessoas envolvidas com soluções de IoT. Devido ao número de Olá de dispositivos envolvidos e Olá a natureza distribuída destes dispositivos, o impacto de Olá um evento de segurança relacionadas com toocompromise de milhões de dispositivos de IoT não trivial e pode ter impacto ampla.

Por este motivo, a segurança de IoT tem uma abordagem de segurança em profundidade. Dados necessidades toobe segura na nuvem de Olá e dado que se move sobre redes públicas e privadas. Métodos necessário toobe no local toosecurely aprovisionar Olá dispositivos IoT próprios. Cada camada do dispositivo, toonetwork, toocloud oferece garantias ao rendimento segurança forte de necessidades de back-end.

Melhores práticas de IoT podem ser classificadas em Olá seguinte forma:

* Fabricante de hardware de IoT ou integrador
* Para programadores de solução IoT
* Implementador de solução IoT
* Operador de solução IoT

Este artigo resume [Internet das coisas melhores práticas de segurança](../iot-suite/iot-security-best-practices.md). Consulte o artigo toothat para obter informações mais detalhadas.

## <a name="iot-hardware-manufacturer-or-integrator"></a>Fabricante de hardware de IoT ou integrador
Se for um fabrico de hardware de IoT ou integrador de hardware, siga Olá melhores práticas abaixo:

* **Definir o âmbito de requisitos de hardware do toominimum**: estrutura de hardware Olá deve incluir funcionalidades mínimas necessárias para a operação de hardware de Olá e nada mais. 
* **Efetuar uma prova de adulteração de hardware**: criar no mecanismos toodetect físico adulteração de hardware, tais como abrir abrange de dispositivo Olá, removendo a parte do dispositivo Olá, etc. 
* **Criar em torno de hardware seguro**: se [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permitir, crie as funcionalidades de segurança, tais como a funcionalidade de arranque baseada no Trusted Platform Module TPM e de armazenamento seguro e encriptado.
* **Efetuar atualizações segura**: atualizar o firmware durante a duração do dispositivo Olá é inevitável.

## <a name="iot-solution-developer"></a>Para programadores de solução IoT
Siga Olá melhores práticas abaixo se for um programador de solução IoT:

* **Siga a metodologia de desenvolvimento de software segura**: desenvolver software segura requer a pensar sobre a segurança de inception Olá do projeto de Olá todos os implementação de tooits de forma Olá, teste e implementação de segurança de zero.
* **Escolha o software de código aberto com cuidado**: software open source para fornece uma oportunidade tooquickly desenvolver soluções.
* **Integrar com cuidado**: muitas das falhas de segurança de software Olá existem em limites de Olá das bibliotecas e APIs. 

## <a name="iot-solution-deployer"></a>Implementador de solução IoT
Siga Olá melhores práticas abaixo se for um implementador de solução IoT:

* **Implementar hardware de forma segura**: implementações de IoT podem exigir toobe hardware implementado em localizações não seguros, tais como espaços públicos ou regiões supervisionados.
* **Manter as chaves de autenticação seguros**: durante a implementação, cada dispositivo requer IDs de dispositivo e chaves de autenticação geradas pelo serviço de nuvem Olá associadas. Manter estas chaves fisicamente seguro, mesmo após a implementação de Olá. Qualquer tecla comprometida pode ser utilizada por um dispositivo malicioso toomasquerade como um dispositivo existente.

## <a name="iot-solution-operator"></a>Operador de solução IoT
Siga Olá melhores práticas abaixo se for um operador de solução IoT:

* **Manter os sistemas de cópias de segurança toodate**: Certifique-se de sistemas operativos de dispositivos e todos os controladores de dispositivo toohello atualizado de versões mais recentes. 
* **Proteger contra atividade maliciosa**: se permite que o sistema de operativo Olá, coloque as funcionalidades de software antivírus e antimalware mais recentes no Olá em cada sistema operativo do dispositivo. 
* **Auditoria frequentemente**: infraestrutura de IoT a auditoria de segurança relacionadas com problemas é chave quando a responder a incidentes de toosecurity.
* **Proteger fisicamente a infraestrutura de IoT Olá**: Olá pior de ataques de segurança contra a infraestrutura de IoT são iniciados toodevices acesso físico a utilizar.
* **Proteger credenciais na nuvem**: credenciais de autenticação em nuvem utilizadas para configurar e utilizar uma implementação de IoT são possivelmente acesso toogain da forma mais fácil do Olá e comprometer um sistema de IoT. 

