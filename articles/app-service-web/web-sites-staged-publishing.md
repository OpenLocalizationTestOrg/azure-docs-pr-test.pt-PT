---
title: "aaaSet segurança ambientes para web apps no App Service do Azure de teste | Microsoft Docs"
description: "Saiba como toouse testado publicação para web apps no App Service do Azure."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Configurar ambientes no App Service do Azure de teste
<a name="Overview"></a>

Ao implementar a aplicação web, a aplicação web no Linux, back-end móvel e API Apps demasiado[do serviço de aplicações](http://go.microsoft.com/fwlink/?LinkId=529714), pode implementar o bloco de implementação separado de tooa em vez de ranhura de produção Olá predefinido quando em execução no Olá **padrão**ou **Premium** modo de plano de serviço de aplicações. As ranhuras de implementação são aplicações realmente em direto com os seus próprios nomes de anfitrião. Elementos de conteúdo e as configurações de aplicação podem ser trocados entre duas ranhuras de implementação, incluindo a ranhura de produção Olá. Implementar a ranhura de implementação da aplicação tooa tem Olá seguintes vantagens:

* Pode validar alterações de aplicações numa ranhura de implementação de teste antes de troca de ranhura de produção Olá.
* Implementar uma tooa a ranhura de aplicação pela primeira vez e trocar-o em produção assegura que todas as instâncias de ranhura Olá são preparadas antes de a ser alternados em produção. Isto elimina o período de indisponibilidade quando implementar a sua aplicação. redirecionamento de tráfego de Olá é totalmente integrado e não existem pedidos são ignorados devido a operações de comutação. Este fluxo de trabalho completo pode ser automatizado configurando [automática comutação](#Auto-Swap) quando a validação de pré-troca de não é necessária.
* Depois de uma troca ranhura Olá com a aplicação anteriormente faseada tem agora Olá anterior aplicação de produção. Se as alterações de Olá alternadas na ranhura de produção Olá não tem o aspeto esperado, pode realizar Olá que mesmo comutação imediatamente fazer uma cópia de tooget do "última conhecido boa o site".

Cada modo de plano de serviço de aplicações suporta um número diferente de ranhuras de implementação. suporta o modo da sua aplicação toofind limite o número de Olá de ranhuras, consulte [preços do App Service](https://azure.microsoft.com/pricing/details/app-service/).

* Quando a aplicação tiver várias ranhuras, não é possível alterar o modo de Olá.
* Dimensionamento não está disponível para ranhuras de não produção.
* Gestão de recursos ligado não é suportada para as ranhuras de não produção. No Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715) apenas, pode evitar esta potencial impacto na ranhura de produção, movendo temporariamente Olá ranhura de produção não tooa diferente do serviço de aplicações plano modo. Tenha em atenção que ranhura de produção não Olá novamente têm de partilhar Olá mesmo modo ranhura de produção Olá antes de pode trocar ranhuras de Olá dois.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Adicionar uma ranhura de implementação
aplicação Olá deve estar em execução Olá **padrão** ou **Premium** modo na ordem para tooenable várias ranhuras de implementação.

1. No Olá [Portal do Azure](https://portal.azure.com/), abra a aplicação [painel de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Escolha Olá **ranhuras de implementação** opção, em seguida, clique em **adicionar ranhura**.
   
    ![Adicionar uma nova ranhura de implementação][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Se a aplicação Olá já está a não ser Olá **padrão** ou **Premium** modo, receberá uma mensagem a indicar os modos de Olá suportado para ativar a publicação de teste. Neste momento, tiver Olá opção tooselect **atualizar** e navegue toohello **escala** separador da sua aplicação antes de continuar.
   > 
   > 
3. No Olá **adicionar uma ranhura** painel, dê um nome de ranhura Olá e selecionar se tooclone configuração de aplicação a partir de outro bloco de implementação existente. Clique em Olá toocontinue de marca de verificação.
   
    ![Origem de configuração][ConfigurationSource1]
   
    Olá pela primeira vez, adicionar uma ranhura, apenas terá duas opções: configuração de clone a partir da ranhura de predefinição Olá na produção ou não de todo.
    Depois de criar várias ranhuras, será tooclone capaz de configuração a partir de uma ranhura diferente Olá um na produção:
   
    ![Origens de configuração][MultipleConfigurationSources]
4. No painel de recursos da sua aplicação, clique em **ranhuras de implementação**, em seguida, clique uma tooopen da ranhura de implementação do painel de recursos nesse bloco, com um conjunto de métricas e a configuração, tal como qualquer outra aplicação. Olá nome de ranhura Olá é mostrado na parte superior de Olá de Olá painel tooremind Olá que está a visualizar a ranhura de implementação.
   
    ![Título da ranhura de implementação][StagingTitle]
5. Clique em URL da aplicação Olá no painel de ranhura Olá. Tenha em atenção a ranhura de implementação de Olá tem o seu próprio nome de anfitrião e também é uma aplicação em direto. toolimit acesso público toohello ranhura de implementação, consulte [aplicação Web do App Service – ranhuras de implementação de produção toonon de acesso web bloco](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

Não há nenhum conteúdo após a criação da ranhura de implementação. Pode implementar toohello ranhura de um ramo do repositório diferente ou um repositório completamente diferente. Também pode alterar a configuração da ranhura de Olá. Olá utilize publicar ou implementação de perfil de credenciais associadas ao bloco de implementação de Olá para as atualizações de conteúdo.  Por exemplo, pode [publicar toothis ranhura com o git](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Configuração para as ranhuras de implementação
Ao clonar a configuração a partir de outro bloco de implementação, a configuração clonado Olá é editável. Além disso, alguns elementos de configuração segue conteúdo Olá através de uma troca (não ranhura específica) enquanto outros elementos de configuração permanecerão no Olá mesmo espaço depois de uma troca (específica da ranhura). Olá listas seguintes mostram configuração Olá que será alterado quando trocar ranhuras.

**As definições que são trocadas**:

* Sockets de Web de definições gerais - por exemplo, a versão do framework, 32/64 bits,
* Definições de aplicação (pode ser configurado toostick tooa ranhura)
* Cadeias de ligação (pode ser configurado toostick tooa ranhura)
* Mapeamentos do processador
* Definições de monitorização e diagnóstico
* Conteúdo de WebJobs

**As definições que não estão a ser alternadas**:

* Pontos finais de publicação
* Nomes de domínio personalizados
* Certificados SSL e os enlaces
* Definições de dimensionamento
* Programadores de WebJobs

tooconfigure uma definição ou ligação cadeia toostick tooa ranhura de aplicação (não alternada) Olá acesso **definições da aplicação** painel para uma ranhura específica, em seguida, selecione Olá **ranhura definição** caixa Olá elementos de configuração que devem stick ranhura Olá. Tenha em atenção que um elemento de configuração marcar como ranhura específica tem efeito Olá estabelecer que o elemento não swappable como em todas as ranhuras de implementação de Olá associadas Olá aplicação.

![Definições de ranhura][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Trocar ranhuras de implementação 
Pode trocar ranhuras de implementação no Olá **descrição geral** ou **ranhuras de implementação** vista do painel de recursos da sua aplicação.

> [!IMPORTANT]
> Antes de trocar uma aplicação de uma ranhura de implementação em produção, certifique-se de que todas as definições específicas do bloco não estão configuradas exatamente como pretende que toohave-lo na Olá troca de destino.
> 
> 

1. tooswap ranhuras de implementação, clique em Olá **comutação** botão na barra de comando Olá da aplicação Olá ou na barra de comando Olá de uma ranhura de implementação.
   
    ![Botão de comutação][SwapButtonBar]

2. Certifique-se de que Olá troca troca de origem e o destino estão definidas corretamente. Normalmente, o destino de troca de Olá é ranhura de produção Olá. Clique em **OK** operação de Olá toocomplete. Quando concluída a operação de Olá, ranhuras de implementação de Olá tem sido alternadas.

    ![Concluir troca](./media/web-sites-staged-publishing/SwapImmediately.png)

    Para Olá **troca com pré-visualização** comutação tipo, consulte [troca com pré-visualização (fase multi swap)](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>Troca com pré-visualização (fase multi swap)

Troca com pré-visualização ou fase multi troca, simplificar a validação de elementos de configuração específicos da ranhura, tais como cadeias de ligação.
Para cargas de trabalho pesadas, pretende toovalidate Olá aplicação se comporta conforme esperado quando a configuração da ranhura de produção Olá é aplicada, e tem de executar essa validação *antes* aplicação Olá é alternada em produção. Troca com pré-visualização é o que precisa.

> [!NOTE]
> Troca com pré-visualização não é suportada nas web apps no Linux.

Quando utiliza Olá **troca com pré-visualização** opção (consulte [trocar ranhuras de implementação](#Swap)), serviço de aplicações Olá seguintes:

- Não é afetada mantém Olá destino ranhura inalterada existente, por isso, carga de trabalho em que ranhura (por exemplo, produção).
- Aplica os elementos de configuração de Olá de Olá destino ranhura toohello ranhura de origem, incluindo cadeias de ligação de específicos da ranhura de Olá e as definições de aplicação.
- Reinicia os processos de trabalho de Olá na ranhura de origem Olá utilizando estes elementos de configuração acima mencionados.
- Quando concluir troca Olá: move ranhura de origem de pré-warmed cópia de segurança Olá na ranhura de destino Olá. ranhura de destino Olá é movida para a ranhura de origem Olá como uma troca manual.
- Se cancelar a troca de Olá: volta elementos de configuração de Olá da ranhura de origem do Olá origem ranhura toohello.

Pode pré-visualizar exatamente como aplicação Olá irão comportar-se com a configuração da ranhura de destino Olá. Depois de concluir a validação, concluir troca Olá num passo separado. Este passo tem Olá adicionada vantagem de ranhura de origem de Olá já está preparada com configuração pretendida Olá e, os clientes não irão experimentar qualquer período de inatividade.  

Exemplos de Olá cmdlets Azure PowerShell disponíveis para comutação fase multi estão incluídos no Olá cmdlets Azure PowerShell para a secção de ranhuras de implementação.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Configurar a troca automática
Simplifica a troca automática cenários de DevOps onde pretende toocontinuously implementa a sua aplicação com zero frio e períodos de indisponibilidade para os clientes de fim da aplicação Olá. Quando uma ranhura de implementação está configurada para a troca automática em produção, sempre que enviar a ranhura de toothat de atualização de código, o serviço de aplicações será automaticamente a comutação aplicação Olá em produção, depois de já ter preparada na ranhura de Olá.

> [!IMPORTANT]
> Quando ativa a comutação automática para uma ranhura, certifique-se a configuração da ranhura Olá exatamente configuração de Olá que se destina a ranhura de destino Olá (normalmente, ranhura de produção Olá).
> 
> 

> [!NOTE]
> Troca automática não é suportada nas web apps no Linux.

É fácil a configuração automática de comutação para uma ranhura. Siga os passos de Olá abaixo:

1. No **ranhuras de implementação**, selecione uma ranhura de não produção e escolha **definições da aplicação** no painel de recursos que ranhura.  
   
    ![][Autoswap1]
2. Selecione **no** para **automática comutação**, selecione ranhura de destino pretendido de Olá no **automática trocar a ranhura**e clique em **guardar** na barra de comando Olá. Certifique-se a configuração para a ranhura de Olá exatamente configuração de Olá que se destina a ranhura de destino Olá.
   
    Olá **notificações** separador irá flash um verde **êxito** após a conclusão da operação de Olá.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest comutação automática para a sua aplicação, primeiro pode selecionar uma ranhura de destino de não produção no **automática trocar a ranhura** toobecome familiarizado com a funcionalidade de Olá.  
   > 
   > 
3. Execute uma ranhura de implementação de toothat de push de código. Troca automática irá ocorrer após um curto período de tempo e atualização Olá será apresentada no URL da ranhura de destino.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback uma aplicação de produção após a troca
Se os erros são identificados em produção após uma troca de ranhura, reversão ranhuras Olá tootheir back-Estados de pré-comutação de ao trocar ranhuras de Olá dois mesmo imediatamente.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Warm-up personalizado antes de comutação
Algumas aplicações podem exigir ações warm-up personalizado. Olá `applicationInitialization` elemento de configuração em Web. config permite-lhe toospecify inicialização personalizada ações toobe efetuada antes de que é recebido um pedido. operação de troca de Olá espera que este toocomplete warm-up personalizado. Eis um fragmento de Web. config de exemplo.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete uma ranhura de implementação
No painel de Olá para uma ranhura de implementação, o painel da ranhura de implementação Olá aberto, clique em **descrição geral** (página predefinida de Olá) e clique em **eliminar** na barra de comando Olá.  

![Eliminar uma ranhura de implementação][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Cmdlets do PowerShell do Azure para as ranhuras de implementação
O Azure PowerShell é um módulo que fornece toomanage de cmdlets do Azure através do Windows PowerShell, incluindo suporte para gerir as ranhuras de implementação no App Service do Azure.

* Para obter informações sobre como instalar e configurar o Azure PowerShell e sobre a autenticação do Azure PowerShell com a sua subscrição do Azure, consulte [como tooinstall e configurar o Microsoft Azure PowerShell](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Criar uma aplicação Web
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Criar uma ranhura de implementação
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Inicie uma troca com a revisão (fase multi swap) e aplicar a ranhura de toosource da configuração de ranhura de destino
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Cancelar uma troca pendente (troca com a revisão) e restaurar a configuração da ranhura de origem
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Trocar ranhuras de implementação
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Elimine o bloco de implementação
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Comandos de Interface de linha de comandos (CLI do Azure) do Azure para as ranhuras de implementação
Olá CLI do Azure fornece comandos de várias plataformas para trabalhar com o Azure, incluindo suporte para gerir as ranhuras de implementação do serviço de aplicações.

* Para obter instruções sobre como instalar e configurar hello CLI do Azure, incluindo informações sobre como tooconnect CLI do Azure tooyour subscrição do Azure, consulte [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md).
* chamar toolist Olá os comandos disponíveis para o App Service do Azure no Olá CLI do Azure, `azure site -h`.

> [!NOTE] 
> Para [Azure CLI 2.0](https://github.com/Azure/azure-cli) comandos para as ranhuras de implementação, consulte [ranhura de implementação do az appservice web](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>lista de sites do Azure
Para obter informações sobre as aplicações de Olá na subscrição atual Olá, chamar **a lista de sites do azure**, como no seguinte exemplo de Olá.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>criar o site do Azure
chamar toocreate uma ranhura de implementação, **do azure site criar** e especifique o nome de Olá de uma aplicação existente e nome de Olá da toocreate de ranhura Olá, como no seguinte exemplo de Olá.

`azure site create webappslotstest --slot staging`

controlo de origem tooenable para Olá nova ranhura, utilize Olá **– git** opção, como no seguinte exemplo de Olá.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>troca de site do Azure
toomake Olá ranhura de implementação atualizada Olá aplicação de produção, utilize Olá **troca de site do azure** comando tooperform uma operação de troca, como no seguinte exemplo de Olá. aplicação de produção Olá não irá ocorrer algum tempo, nem vai sofrer-uma arranque a frio.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>eliminação de site do Azure
toodelete uma ranhura de implementação que já não é necessário, utilize Olá **eliminação de site do azure** comando, como no seguinte exemplo de Olá.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Veja uma aplicação Web em ação. [Experimentar o App Service](https://azure.microsoft.com/try/app-service/) imediatamente e crie uma aplicação de arranque de curta duração — sem cartões de crédito, sem compromissos.
> 
> 

## <a name="next-steps"></a>Passos Seguintes
[Web do App Service do Azure aplicação – bloquear ranhuras de implementação de produção toonon de acesso web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[introdução tooApp serviço no Linux](./app-service-linux-intro.md)
[avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

