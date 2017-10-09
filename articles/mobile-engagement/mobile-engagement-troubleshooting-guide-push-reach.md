---
title: aaaAzure Mobile Engagement Troubleshooting Guide - Push/alcance
description: "Resolução de problemas de interação e a notificação do utilizador no Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>Guia de resolução de problemas Push e alcance
Olá seguem-se possíveis problemas que pode surgir com a forma como o Azure Mobile Engagement envia os utilizadores de tooyour informações.

## <a name="push-failures"></a>Falhas de push
### <a name="issue"></a>Problema
* Pushes não funcionam (na aplicação, fora da aplicação, ou ambos).

### <a name="causes"></a>Causas
* Necessário Olá SDK toofix demasiadas vezes uma push falha é uma indicação de que Azure Mobile Engagement, alcance ou outra funcionalidade avançada do Azure Mobile Engagement não estiver corretamente integrada ou que uma atualização é um problema conhecido com uma nova plataforma de dispositivo ou de SO.
* Teste apenas um push na aplicação e apenas um toodetermine de push de saída da aplicação se algo um problema na aplicação ou de aplicação.
* Teste a partir de Olá IU e Olá API como uma resolução de problemas toosee de passo estão disponíveis as informações de erro adicionais ambos os locais.
* Fora da aplicação pushes poderá não funcionam, a menos que o Azure Mobile Engagement e alcance estão integrados Olá SDK.
* Pushes não funcionará se certificados não são válidos ou estão a utilizar PROD vs. DEV corretamente (apenas iOS). (**Nota:** "fora da aplicação" notificações push poderão não ser entregues tooiOS, se tiver o desenvolvimento de Olá (desenvolvimento) e versões de produção (PROD) da aplicação instaladas no Olá mesmo dispositivo desde o token de segurança de Olá associado com o seu certificado poderá ser invalidado por Apple. tooresolve este problema, desinstale Olá DEV e PROD versões da aplicação e volte a instalar o apenas Olá uma versão no seu dispositivo.)
* Fora da aplicação contagens de push são processadas forma diferente em plataformas diferentes (iOS mostra menos informações ao Android se pushes nativos estão desativadas num dispositivo, Olá API pode fornecer mais informações que Olá IU no estatísticas de push).
* Fora da aplicação podem ser bloqueados pushes por clientes ao nível do SO (iOS e Android).
* Fora da aplicação pushes serão apresentadas como desativada no Olá da IU do Azure Mobile Engagement, se não são integrados corretamente, mas poderão falhar silenciosamente de Olá API.
* Na aplicação pushes poderá não funcionam, a menos que o Azure Mobile Engagement e alcance estão integrados Olá SDK.
* Pushes GCM e ADM não funcionará, a menos que o Azure Mobile Engagement e servidor específico Olá estão integrados no Olá SDK (apenas Android).
* Na aplicação de entrada e saída da aplicação pushes devem ser testadas separadamente toodetermine se for um problema de Push ou alcance.
* Na aplicação pushes requerem essa aplicação Olá ser aberta toobe recebido.
* Na aplicação pushes são, muitas vezes, o programa de configuração toobe filtrado por uma tag de informações de opção ou recusa uma aplicação.
* Se utilizar uma categoria personalizada no alcance toodisplay nas notificações na aplicação, terá de toofollow Olá correto ciclo de vida de notificação de Olá; caso contrário, não pode ser limpa a notificação de Olá quando o utilizador de Olá dispensá-lo.
* Se iniciar uma campanha com sem data de fim e um dispositivo recebe Olá na notificação da aplicação, mas não apresentá-lo ainda, Olá utilizador irá ainda receber Olá de notificação de Olá vez seguinte que iniciar sessão na aplicação Olá, mesmo se manualmente de fim campanha Olá.
* Para problemas com Olá Push API, confirme que pretende que o realmente toouse Olá API de Push em vez de Olá API de alcance (uma vez que Olá API de alcance é utilizado mais frequentemente) e que não estão confuso Olá ". o payload" e parâmetros de "notifier".
* Teste a sua campanha push com ambos os um dispositivo ligado através de Wi-Fi e 3G tooeliminate Olá ligação de rede como uma origem dos problemas possíveis.

## <a name="push-testing"></a>Push de teste
### <a name="issue"></a>Problema
* Pushes podem ser enviadas tooa dispositivo específico, com base num ID de dispositivo.

### <a name="causes"></a>Causas
* Dispositivos de teste são a configuração de forma diferente para cada plataforma, mas a causar um evento na sua aplicação num dispositivo de teste e procurando o ID do dispositivo no portal de Olá deverão funcionar toofind o ID do dispositivo para todas as plataformas.
* Dispositivos de teste funcionam de forma diferente com IDFA vs. IDFV (apenas iOS).

## <a name="push-customization"></a>Personalização de push
### <a name="issue"></a>Problema
* Avançadas push conteúdo item não funcionará (destaque, anel, Vibre, imagem, etc.).
* As ligações de pushes não funcionam (fora da aplicação, na aplicação, o Web site de tooa, tooa localização na aplicação).
* Mostrar de estatísticas de push que um push não foi enviada tooas muitas pessoas conforme esperado (demasiados ou insuficiente).
* Push duplicado e recebido duas vezes.
* Não é possível registar o dispositivo de teste para o Azure Mobile Engagement Pushes (com a sua própria aplicação Prod ou DEV).

### <a name="causes"></a>Causas
* toolink tooa localização específica na aplicação requer "categorias" (apenas Android).
* Profunda de ligar os esquemas de localização alternativa do tooredirect utilizadores tooan depois de clicar numa notificação push necessário toobe criada no e gerida pela sua aplicação e Olá SO do dispositivo não ao Mobile Engagement diretamente. (**Nota:** fora da aplicação notificações não é possível ligar diretamente tooin localizações de aplicação com o iOS como estes requisitos podem com Android.)
* Os servidores de imagem externo precisam toobe capaz de toouse HTTP "GET" e "HEAD" para visão pushes toowork (apenas Android).
* No seu código, pode desativar Olá de agente do Azure Mobile Engagement quando teclado Olá é aberto e ter o seu código reativar o agente do Azure Mobile Engagement Olá depois teclado Olá é fechado, para que hello teclado não afeta o aspecto de Olá do seu notificação (apenas iOS).
* Alguns itens não funcionam no simulações de teste, mas apenas as campanhas reais (de destaque, anel, Vibre, imagem, etc.).
* Não existem do lado do servidor, os dados são registados quando utiliza o botão de Olá demasiado "teste" pushes. Os dados são registados apenas para as campanhas real push.
* toohelp isolar o problema, resolver problemas com: testar, simular e uma campanha real, uma vez que cada funcionam forma ligeiramente diferente.
* Olá período de tempo que a "aplicação" e campanhas de "sempre" são agendada toorun pode que tenha efeito números de entrega, uma vez que uma campanha apenas serão entregues toousers que são "na aplicação" enquanto campanha Olá é executada (e os utilizadores que possuem as definições de dispositivo definida tooreceive notificações "fora da aplicação").
* Olá diferenças como identificador Android e iOS fora de notificações da aplicação torna difícil toodirectly comparam as estatísticas de push entre a versão Android e iOS Olá da sua aplicação. Android fornece mais informações de notificação de nível de SO que iOS. Android relatórios quando é recebida, clicada ou eliminada no Centro de notificações de Olá uma notificação nativa, mas o iOS não comunica esta informação, exceto se notificação Olá é clicada. 
* Olá principal motivo que números "premidos" são diferentes que diferente de "entregues" números de campanhas de alcance que "na aplicação" e "fora da aplicação" notificações são contadas diferente. "Na aplicação" notificações são processadas pelo Mobile Engagement, mas "fora da aplicação" notificações são processadas pelo centro de notificações de Olá no Olá SO do dispositivo.

## <a name="push-targeting"></a>Filtragem de push
### <a name="issue"></a>Problema
* Incorporada na filtragem não funciona conforme esperado.
* Filtragem de Tag as informações da aplicação não funciona conforme esperado.
* Filtragem de Geolocalização não funciona conforme esperado.
* As opções de idioma não funcionam conforme esperado.

### <a name="causes"></a>Causas
* Certifique-se de que carregou etiquetas de informações da aplicação através da IU do Azure Mobile Engagement de Olá ou API.
* Limitação Olá push velocidade push quota ou ao nível da aplicação Olá ou restritiva Olá público-alvo ao nível da campanha Olá pode impedir que uma pessoa de receber um push específico, mesmo que cumprem os critérios de filtragem. 
* A definição de um "idioma" é diferente de filtragem com base num país ou região, que também é diferente de filtragem com base no geolocalização com base numa localização de telefone ou a localização de GPS.
* mensagem de saudação no Olá "idioma predefinido" é enviada tooany cliente que não tenha o respetivo dispositivo definir tooone de idiomas alternativos Olá que especificar.

## <a name="push-scheduling"></a>Push de agendamento
### <a name="issue"></a>Problema
* Agendamento de push não funciona conforme esperado (enviado demasiado antecipada ou atrasada).

### <a name="causes"></a>Causas
* Fusos horários pode problemas com o agendamento, especialmente quando se utilizam o fuso horário dos utilizadores finais Olá.
* Funcionalidades avançadas de push podem atrasar pushes.
* Filtragem baseada no telefone definições (em vez de etiquetas de informações de aplicação) podem atrasar pushes uma vez que o Azure Mobile Engagement pode ter dados toorequest Olá em tempo real phone antes de enviar um push.
* As campanhas criadas sem uma data de fim armazenam Olá push localmente no dispositivo Olá e mostram Olá próxima vez que aplicação Olá é aberta, mesmo se campanha Olá manualmente seja terminada.
* Iniciar mais de uma campanha em Olá a mesmo tempo pode demorar um tooscan mais longo do tempo de base de utilizadores (tente tooonly início uma campanha de cada vez com um máximo de quatro, também apenas tooyour utilizadores ativos de destino para que os utilizadores antigos não tem toobe analisado).
* Se utilizar a opção de "Ignorar audiência; push será enviado toousers através de Olá API" Olá na secção "Campanha" Olá uma campanha de alcance campanha Olá não enviará automaticamente, terá de toosend-lo manualmente através de Olá API de alcance.
* Se utilizar uma categoria personalizada no alcance toodisplay nas notificações na aplicação, terá de toofollow Olá correto ciclo de vida de uma notificação; caso contrário, não pode ser limpa a notificação de Olá quando o utilizador de Olá dispensá-lo.

