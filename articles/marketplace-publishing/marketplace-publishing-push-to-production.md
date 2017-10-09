---
title: aaaDeploy toohello sua oferta Azure Marketplace | Microsoft Docs
description: "Saiba mais sobre e guiá Olá instruções toodeploy oferta – imagem de máquina virtual, o serviço de programador, serviço de dados, etc. - toohello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: ab0bb7c78020187505c2d5f09c4de246987ecd97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-offer-toohello-azure-marketplace"></a>Implementar a sua toohello oferta Azure Marketplace
Quando estiver satisfeito com a sua oferta (ou seja, tiver testado cenários de cliente, de marketing conteúdo, etc.) e estão pronto toolaunch, pedido **Push tooproduction** no Olá **publicar** separador.  

1. Olá quatro passos na página de instruções de Olá no Olá publicação portal deve ser concluída e a verde. Para ofertas de Máquina Virtual, certifique-se de que Olá seguir diretrizes são seguidos.
   
    ![desenho][img-pubportal-walkthru-checked]
2. Selecione Olá **publicar** separador lista de Olá na Olá deixado lado.
   
    ![desenho][img-pubportal-menu-publish]
3. Clique no botão de Olá **pedir aprovação toopush tooproduction**. Quando é feito pedido Olá, equipa de aprovação de Olá executa uma revisão final e, em seguida, a oferta estarão disponível na Olá Azure Marketplace.
   
    ![desenho][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> Em caso de máquinas virtuais, quando clica em Olá botão pedido de aprovação toopush tooproduction Olá os seguintes passos é efetuado por trás de cenas Olá. Será progresso de Olá tooview capaz de cada passo no separador de publicar Olá no Olá portal de publicação. Tem de verificar esta página num intervalo regular (até que o estado de Olá mostra "Apresentados") para qualquer informação de falha que precisam de correção da sua end.
> 
> * Em primeiro lugar, o pedido de produção passa toohello equipa de certificação que validar Olá vhd. No entanto, se atualizar a sua oferta já listada e tem um pedido de Olá no apenas alterações de marketing, em seguida, Olá certificação passo é ignorado.
> * No próximo passo Olá, o pedido de Olá vêm toohello equipa de validação de conteúdos que verifique Olá conteúdo de oferta de Olá de marketing.
> * Se forem efetuadas com êxito Olá os passos acima, oferta Olá for aprovada na produção. Neste momento, o estado de Olá tornar-se "listados" no portal de publicação Olá. No entanto, este estado de "Apresentados" não implica que o processo de Olá está concluído. Olá, seguindo os passos necessidade toobe concluída antes de oferta de Olá está disponível no Olá Azure Marketplace.
> * Quando for aprovada oferta Olá na produção no passo Olá acima, a replicação de início de oferta Olá em todos os Olá centros de dados do Azure. Geralmente, demora 24-48hours para Olá replicação toocomplete mas poderá demorar até tooa semana, consoante o tamanho do vhd Olá Olá. No entanto, se atualizar a sua oferta já listada e tem obteve a alteração de marketing apenas, em seguida, replicação de Olá é mais rápida.
> * Quando a replicação de Olá estiver concluída, em seguida, oferta Olá estarem disponível na Olá Azure Marketplace.
> 
> Pode sempre eliminar oferta Olá enquanto está a ser um **rascunho** Estado (ou seja, nunca **Push toostaging** ou **Push tooproduction**). No Olá **histórico** separador, clique em Olá **rejeitar rascunho** botão na parte inferior de Olá de Olá página toodelete um rascunho.
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a>Lista de verificação de produção para todas as ofertas de Máquina Virtual
* Certifique-se de que um parceiro de certificados do Microsoft Azure
* No separador de SKUs Olá, opção Olá "Ocultar esta SKU de Olá Marketplace porque deve sempre ser comprou através de um modelo de solução" deve ser marcado como Sim apenas se Olá SKU é uma parte de um modelo de solução. Em todos os Olá noutros casos, esta opção sempre deverá ser marcada como não.
* Lembre-se: A não deve alterar a definição de visibilidade SKU Olá depois Olá SKU está listado. Não é proporcionado suporte esta funcionalidade.
* Certifique-se de que logótipos Olá aderem diretrizes de logótipo toohello Azure Marketplace indicadas abaixo.
* Descrição de oferta e SKU não deve ser igual.
* Do SKU título e oferecem longo resumo não devem ser igual.
* Título de SKU e o resumo de oferta não devem ser igual.
* Não deve ser idênticos para uma oferta a SKUs de vários títulos de SKU.

**Diretrizes de logótipo do Azure Marketplace**

* Olá design do Azure tem uma paleta de cores simples. Manter número Olá de principal e secundário cores o logótipo baixa.
* cores de tema Olá de Olá portal do Azure estão em brancos e marcar a negrito. Por conseguinte, evite utilizar estes cores como cor de fundo de Olá da sua logótipos. Utilize algumas cor que iria tornar o seu logótipos prominent no Olá portal do Azure. Recomendamos simples de principal de cores. Se estiver a utilizar o fundo transparente, em seguida, certifique-se de que texto/logótipo de Olá não é branco ou marcar a negrito.
* Não utilize um fundo gradação logótipo Olá.
* Evite a colocação de texto, mesmo sua empresa ou o nome da marca, no logótipo Olá.
* Olá aspeto e funcionalidade do logótipo deve ser 'simples' e deve evitar gradações.
* não deve ser esticado logótipo Olá.

**Diretrizes adicionais para logótipo de heroína Olá:**

* logótipo de heroína Olá é opcional. publicador de Olá pode optar por não tooupload um logótipo de heroína. **Ícone de heroína Olá no entanto, uma vez carregado não pode ser eliminada do Olá portal de publicação. Nessa altura, parceiro Olá tem de seguir as diretrizes de Azure Marketplace Olá por ícones heroína oferta de Olá pessoa não será tooproduction aprovado.**
* Olá nome a apresentar do publicador, o título SKU e Olá oferecem resumo extenso são apresentados na cor branco do tipo de letra. Por conseguinte, deve evitar manter quaisquer cor leve em segundo plano de Olá de Olá heroína ícone. Negra, fundo branco e transparente não é permitido para ícones heroína.
* Olá nome de apresentação do publicador, título da SKU, tempo de resumo de oferta Olá e Olá criam botão estão incorporados através de programação no interior de logótipo de heroína Olá assim que a oferta de Olá fica listada. Por isso, não deve introduzir qualquer texto enquanto está a conceber o logótipo de heroína Olá. Basta deixe espaço em branco direita Olá porque texto hello (ou seja, nome a apresentar do publicador, título do SKU, tempo de resumo de oferta Olá) será incluído programaticamente por-nos através do mesmo. Olá o espaço em branco para texto Olá deve ser 415 x 100 no Olá direito (e é de deslocamento por 370px da esquerda Olá).

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a>Lista de verificação de produção adicionais para a máquina de Virtual já listadas oferece
* Verifique se já existir uma oferta com Olá mesmo oferecem nome da sua empresa. Se Sim, deve adicionar uma nova versão do Olá SKU na oferta existente do Olá em vez de criar uma nova oferta duplicada.
* Disco de dados não deve alterar entre duas versões de Olá mesmo SKU.
* Olá Azure Marketplace não suporta a alteração de Olá de preço listadas SKUS como tem impacto sobre faturação Olá de clientes existentes Olá. Certifique-se de que não altere Olá preços de SKUs de Olá listado regiões olá onde Olá SKU está disponível. No entanto, pode adicionar novos SKUs ou adicionar nova tooan de regiões existente SKU.

## <a name="next-steps"></a>Passos seguintes
Assim que a oferta de Olá fica em direto, teste Olá cliente cenários toovalidate que todos os contratos de Olá e funcionalidades funcionam corretamente no ambiente de produção Olá como ambiente de teste de Olá testada e validados no.

## <a name="see-also"></a>Consultar também
* [Introdução: como toopublish toohello uma oferta Azure Marketplace](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png
