---
title: "aplicação de autenticação aaaMicrosoft ajuda e suporte | Microsoft Docs"
description: Fornece uma lista de perguntas mais frequentes e responde toohello relacionados Authentication do Microsoft app e o Azure multi-factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f04d5bce-e99e-4f75-82d1-ef6369be3402
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: afba9b59ccaac60d022e8516fcf573dcfbf68af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-authenticator-app-faq"></a>Aplicação de autenticação do Microsoft FAQ

Este artigo responde a questões recorrentes que recebemos sobre Olá Microsoft Authenticator aplicação. Se não vir uma pergunta de tooyour de resposta, aceda toohello [fórum de aplicação do Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp). Além disso, temos outro FAQ sobre uma funcionalidade específica na aplicação Olá, [iniciar sessão com o seu telefone FAQ](microsoft-authenticator-app-phone-signin-faq.md).

Olá Microsoft Authenticator aplicação substituída Olá do Azure Authenticator e Olá recomenda-se aplicações ao utilizar o Azure multi-factor Authentication. aplicação do Microsoft Authenticator Olá está disponível para [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

### <a name="what-are-hello-codes-in-hello-app-for-why-does-hello-number-keep-counting-down"></a>Quais são os códigos de Olá na aplicação Olá para? Por que motivo número Olá manter contando?

Quando abrir a aplicação do Microsoft Authenticator Olá, ver as contas de Olá que adicionou e um número de dígitos de seis ou oito por cada um deles. Poderá ver um temporizador de 30 segundo contando para baixo.

Estes códigos são utilizados quando iniciar sessão na conta tooyour. Depois de introduzir o nome de utilizador e palavra-passe, poderá ser-lhe pedido tooenter um código de verificação. Abra Olá Microsoft Authenticator aplicação e copie Olá código que está atualmente a ser mostrada. Introduza esse código Olá toofinish de página de início de sessão.

motivo de Olá códigos Olá alteração cada 30 segundos é para que nunca utilize Olá mesmo código duas vezes. Não é como uma palavra-passe que está a deveria tooremember. ideia Olá é apenas alguém com phone tooyour de acesso a conhecer o seu código de verificação.

códigos de Olá não necessitam de internet ou de dados, pelo que não tem tooworry relacionada com phone serviço toosign. Quando fechar aplicação Olá, não continuar em execução em segundo plano de Olá e não drenar da bateria. Pode fechar aplicação Olá e ignorá-lo até Olá próxima vez que iniciar sessão.  

### <a name="i-only-get-notifications-when-i-have-hello-app-open-if-hello-app-isnt-open-i-dont-get-any-notifications"></a>Apenas receber notificações tenho aplicação Olá abrir. Se a aplicação Olá não estiver aberta, posso não obter quaisquer notificações.

Se receber notificações, mas não fazer ruído ou Vibre, apesar da alteração do toque na, verifique as definições de aplicação Olá primeiro. Ativar som de toouse de aplicação Olá ou Vibre com o respetivas notificações.

Se não obtiver as notificações de todo, verifique Olá seguintes casos:

- É o seu telefone no modo silenciosos ou não efetue Disturb? Desse modo pode manter as aplicações de envio de notificações.
- Pode receber notificações de outras aplicações? Caso contrário, poderão existir um problema com ligações de rede de Olá no seu telemóvel ou canal de notificações de Olá do Android ou Apple. Pode resolver opção primeiro Olá nas suas definições de telefone, mas poderá ser necessário fornecedor de serviços de tooyour tootalk para obter ajuda com a segunda opção de Olá.
- Pode receber notificações para algumas contas na aplicação Olá, mas não a outros utilizadores? Se Sim, remover a conta de problemáticas de Olá da sua aplicação e adicione-a novamente tooenable notificações de push. 

Se tiver tentou estas sugestões de resolução de problemas, mas ainda está a ter problemas, envie-nos registos de diagnóstico. Aceda a definições de aplicação toohello, em seguida, selecione **ajuda e comentários** e **enviar registos de**. Em seguida, aceda toohello [fórum de aplicação do Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) e informe-no que problema está a ver e que medidas já tentou até ao momento. 

### <a name="im-already-using-hello-microsoft-authenticator-application-for-verification-codes-how-do-i-switch-tooone-click-push-notifications"></a>Olá aplicação Microsoft Authenticator já estiver a utilizar para códigos de verificação. Como mudar a notificações de push tooone clique?
Aprovar um início de sessão através de notificação push só está disponível para contas Microsoft pessoais ou de trabalho contas escolares ou profissionais Microsoft, não para contas de terceiros como o Google ou o Facebook. Se tiver uma empresa ou escola conta Microsoft, a organização pode escolher toodisable esta opção.

Se utilizar uma conta Microsoft para a sua conta pessoal e quiser tooswitch através de notificações de toopush, terá de tooadd sua conta novamente. Volte a registar dispositivos Olá com a sua conta e configurar as notificações push.  

Se utilizar o Microsoft Authenticator para a sua conta escolar ou profissional, em seguida, decide a sua organização se tooallow notificações de um clique.

### <a name="do-one-click-push-notifications-work-for-non-microsoft-accounts"></a>Notificações push de um clique funcionam para contas de terceiros?
Não, as notificações push funcionam apenas com contas Microsoft e contas do Azure Active Directory. Se a sua empresa ou escola utiliza contas do Azure AD, estes podem desativar esta funcionalidade.  

### <a name="i-restored-my-device-from-a-backup-and-my-account-codes-are-missing-or-not-working-what-happened"></a>Posso restaurado o meu dispositivo a partir de uma cópia de segurança e códigos a minha conta estão em falta ou não está a funcionar. O que aconteceu?
Por motivos de segurança, iremos não restaurar as contas de cópias de segurança da aplicação.  Depois de restaurar aplicação Olá, elimine as contas e adicioná-los novamente.

### <a name="i-got-a-new-device-how-do-i-remove-hello-microsoft-authenticator-app-from-my-old-device-and-move-toohello-new-one"></a>Posso obteve um novo dispositivo. Como remover a aplicação do Microsoft Authenticator Olá meu dispositivo antigo e mover toohello novo?
Adicionar Olá Microsoft Authenticator tooa novo dispositivo de aplicação não automaticamente removê-lo de todos os outros dispositivos. toomanage os dispositivos que estão configurados para a sua conta, visite Olá mesmo Web site que utiliza a verificação de toomanage e escolher tooremove aplicações antigas.

Para contas Microsoft pessoais, este Web site está a [segurança da conta](https://account.microsoft.com/security) página. Para contas Microsoft escolar ou profissional, este Web site poderá ser um [MyApps](https://myapps.microsoft.com) ou um portal personalizado que configurou sua organização.

### <a name="how-do-i-remove-an-account-from-hello-app"></a>Como remover uma conta a partir da aplicação Olá?
* iOS: a partir do ecrã principal de Olá, percorra a esquerda num mosaico de conta. Selecione **Eliminar**.
* Windows Phone: A partir do ecrã principal de Olá, selecione botão do menu Olá, em seguida, **edita contas**. Toque em Olá **X** nome da conta toohello seguinte.
* Android: A partir do ecrã principal de Olá, selecione botão do menu Olá, em seguida, **edita contas**. Toque em Olá **X** nome da conta toohello seguinte.

Se tiver um dispositivo que está registado com a sua organização, poderá ter toocomplete tooremove um passo adicional a sua conta. Nestes dispositivos, a aplicação do Microsoft Authenticator Olá é automaticamente registada como um administrador do dispositivo. Se quiser toocompletely desinstalação Olá aplicação, terá de toofirst anular o registo da aplicação Olá nas definições de aplicação Olá.

### <a name="why-does-hello-app-request-so-many-permissions"></a>Por que razão a aplicação Olá pedido tantas permissões?
Eis uma lista completa das permissões, pode pedir e como são utilizados na aplicação Olá. permissões específicas Olá que vir dependem do tipo de Olá do telemóvel que tem.

* **Câmara**: utilizamos os códigos de tooscan QR câmara quando adicionar uma conta de terceiros, escolar ou profissional.
* **Contactos e phone**: quando iniciar sessão com a sua conta Microsoft pessoal, vamos experimentar processo de Olá toosimplify ao localizar as contas existentes que utiliza no seu telemóvel.
* **SMS**: quando inicia sessão com a sua conta Microsoft pessoal para Olá pela primeira vez, temos toomake certificar-se de que a corresponde ao número de telefone Olá um temos no registo. Enviar-lhe um telefone de toohello de mensagem de texto onde transferiu Olá aplicação. mensagem de saudação contém um código de verificação 8 de 6 dígitos. Em vez de pedir-lhe toofind este código e introduza-o na aplicação Olá, que encontrar na mensagem de texto de saudação por si.
* **Desenhar através de outras aplicações**: quando recebem uma notificação tooverify sua identidade, iremos apresentar a essa notificação através de qualquer outra aplicação pode estar em execução.
* **Receba dados de Olá internet**: Esta permissão é necessária para enviar notificações.
* **Impedir que o telefone suspensão**: se registar o seu dispositivo com a sua organização, podem alterar esta política no seu telemóvel.
* **Controlar vibration**: pode escolher se pretende que um vibration sempre que recebe uma notificação tooverify sua identidade.
* **Utilize hardware de identificação digital**: algumas contas profissional e escolar exigem um PIN adicional, sempre que confirme a sua identidade. processo de Olá toomake mais fácil, iremos permitem-lhe toouse sua impressão digital em vez de introduzir Olá PIN.
* **Ver as ligações de rede**: ao adicionar uma conta Microsoft, aplicação Olá requer a ligação de rede/à internet.
* **Ler conteúdo de Olá do seu armazenamento**: Esta permissão só é utilizada quando comunicar um problema técnico através das definições de aplicação Olá. Algumas informações do seu armazenamento são recolhidas problema de Olá toodiagnose.
* **Acesso de rede total**: Esta permissão é necessária para enviar notificações tooverify sua identidade.
* **São executados no arranque**: se reiniciar o seu telemóvel, esta permissão garante que continuam a receber notificações tooverify sua identidade.

### <a name="why-does-hello-microsoft-authenticator-app-allow-you-tooapprove-a-request-without-unlocking-hello-device"></a>Por que motivo Olá aplicação de autenticação da Microsoft permite-lhe tooapprove um pedido sem o dispositivo de Olá desbloqueio?

Não tem toounlock que a verificação de tooapprove dispositivo pedidos porque tudo o que precisa tooprove é que tem o seu telemóvel consigo. Verificação de dois passos requer comprovar duas coisas – uma coisa que conhece e uma coisa que precisa. Olá que sabe que é a palavra-passe. Olá que tiver é o seu telefone (configurado com a aplicação do Microsoft Authenticator Olá e registado como uma prova de MFA). Por conseguinte, ter phone Olá e aprovar o pedido de Olá Olá, cumpre os critérios de segundo fator de Olá de autenticação. 

### <a name="what-does-hello-lock-icon-in-hello-account-list-mean"></a>O que significa ícone de cadeado Olá na lista de contas de Olá?

ícone de cadeado Olá indica que o dispositivo Olá está registado no Azure AD e registado toohello conta. Registo de dispositivos para iOS ocorre durante a inscrição no Microsoft Intune.

## <a name="next-steps"></a>Passos seguintes

### <a name="contact-us"></a>Contacte-nos
Se a sua pergunta não foi respondida aqui, queremos toohear do utilizador. Aceda toohello [fórum de aplicação do Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) toopost sua pergunta e obter ajudam da Comunidade Olá ou deixam um comentário nesta página.


### <a name="related-topics"></a>Tópicos relacionados
* [Sobre a verificação de dois passos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) para contas Microsoft
* [Problemas com verificação de dois passos](multi-factor-authentication-end-user-troubleshoot.md) para a sua conta escolar ou profissional?
* [Utilizar Olá Microsoft Authenticator toosign no através do telemóvel](microsoft-authenticator-app-phone-signin-faq.md)

