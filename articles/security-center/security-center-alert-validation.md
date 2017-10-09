---
title: "aaaAlerts validação no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda-o a alertas de segurança de Olá toovalidate no Centro de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Validação de Alertas no Centro de Segurança do Azure
Este documento ajuda-o a saber como tooverify se o sistema está configurado corretamente para alertas do Centro de segurança do Azure.

## <a name="what-are-security-alerts"></a>O que são alertas de segurança?
Automaticamente o Centro de segurança recolhe, analisa e integra-se os dados de registo de recursos do Azure, rede Olá e soluções de parceiros ligadas, como soluções de proteção de ponto final e firewall, toodetect e alerta, toothreats. Leitura [toosecurity está a responder e gerir alertas no Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) para obter mais informações sobre alertas de segurança e ler [Noções sobre alertas de segurança no Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn mais sobre Olá diferentes tipos de alertas.

## <a name="alert-validation"></a>Validação de alertas
Após instalação do agente do Centro de segurança no seu computador, siga os passos de Olá abaixo do computador olá onde pretende que o recurso de Olá atacado toobe de alerta de Olá:

1. Copie o ambiente de trabalho de um computador toohello executável (por exemplo calc.exe) ou outro diretório da sua comodidade.
2. Mudar o nome deste ficheiro demasiado**ASC_AlertTest_662jfi039N.exe**.
3. Abra a linha de comandos Olá e executar este ficheiro com um argumento (apenas um nome argumento falsificados), tal como: *ASC_AlertTest_662jfi039N.exe - foo*
4. Aguarde 5 minutos too10 e abra alertas do Centro de segurança. Não existe deve encontrar um alerta toofollowing semelhante uma:

    ![Validação de Alertas](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

Ao rever este alerta, certifique-se de campo Olá argumentos auditoria ativada é apresentado como true. Se mostra FALSO, terá de argumentos da linha de comandos tooenable auditoria. Pode ativar esta opção utilizando Olá seguinte linha de comandos:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>Consultar também
Este artigo introduzida toohello processo de validação de alertas. Agora que está familiarizado com esta validação, experimente Olá seguintes artigos:

* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Saiba como toomanage alertas e respondeu toosecurity incidentes no Centro de segurança.
* [Monitorização de estado de funcionamento de segurança no Centro de Segurança do Azure](security-center-monitoring.md). Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Compreender os alertas de segurança no Centro de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Saiba mais sobre os diferentes tipos Olá de alertas de segurança.
* [Guia de Resolução de Problemas do Centro de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Saiba como tootroubleshoot comuns problemas no Centro de segurança. 
* [Centro de Segurança do Azure FAQ (FAQ do Centro de Segurança do Azure)](security-center-faq.md). Localize perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/). Encontre mensagens do blogue acerca da segurança e conformidade do Azure.

