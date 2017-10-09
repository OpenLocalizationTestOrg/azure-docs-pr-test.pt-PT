---
title: "Descrição geral do suporte de dados dos serviços de transmissão em fluxo Endpoint aaaAzure | Microsoft Docs"
description: "Este tópico fornece uma descrição geral dos Media Services do Azure pontos finais de transmissão em fluxo."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>Descrição geral de pontos finais de transmissão em fluxo 

##<a name="overview"></a>Descrição geral

No Microsoft Azure dos Media Services (AMS), um **ponto final de transmissão em fluxo** representa um serviço de transmissão em fluxo que pode fornecer conteúdo diretamente tooa aplicação de leitor de cliente ou tooa rede de entrega de conteúdos (CDN) para uma maior distribuição. Os Media Services também fornecem uma integração perfeita CDN do Azure. fluxo de saída Olá num serviço StreamingEndpoint pode ser uma transmissão em fluxo em direto, um vídeo a pedido ou transferência progressiva do seu elemento na sua conta de Media Services. Cada conta de Media Services do Azure inclui um predefinido StreamingEndpoint. Lidam adicionais pode ser criados na conta de Olá. Existem duas versões do lidam, 1.0 e 2.0. A partir de com 10 de Janeiro de 2017, as contas recentemente criadas do AMS irão incluir versão 2.0 **predefinido** StreamingEndpoint. Adicional que adicionar a conta de toothis de pontos finais de transmissão em fluxo também será versão 2.0. Esta alteração não irá afetar as contas existentes Olá; lidam existente será versão 1.0 e pode ser atualizado tooversion 2.0. Com esta alteração vão ocorrer alterações de comportamento, faturação e funcionalidade (para obter mais informações, consulte Olá **tipos e versões de transmissão em fluxo** secção documentados abaixo).

Além disso, a partir da versão de Olá 2.15 (lançada em Janeiro de 2017), Media Services do Azure adicionado Olá seguir a entidade de ponto final de transmissão em fluxo propriedades toohello: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Para uma descrição geral detalhada destas propriedades, consulte [isto](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

Quando cria uma conta de Media Services do Azure uma predefinição de ponto final padrão de transmissão em fluxo é criado para si no Olá **parado** estado. Não é possível eliminar a predefinição de Olá ponto final de transmissão em fluxo. Dependendo da disponibilidade da CDN do Azure numa região de Olá direcionado Olá, por predefinição recém-criado predefinição ponto final de transmissão em fluxo também inclui "StandardVerizon" CDN integração do fornecedor. 

>[!NOTE]
>Integração da CDN do Azure pode ser desativada antes de iniciar Olá ponto final de transmissão em fluxo.

Este tópico fornece uma descrição geral das funcionalidades de principais de Olá que são fornecidos por pontos finais de transmissão em fluxo.

## <a name="streaming-types-and-versions"></a>Tipos de transmissão em fluxo e versões

### <a name="standardpremium-types-version-20"></a>Tipos de padrão/Premium (versão 2.0)

A partir da versão de Janeiro de 2017 Olá dos Media Services, tem dois tipos de transmissão em fluxo: **padrão** e **Premium**. Estes tipos são parte da versão de ponto final de transmissão em fluxo Olá "2.0".

Tipo|Descrição
---|---
**Standard**|Esta é a opção predefinida Olá que funciona para a maioria de Olá dos cenários de Olá.<br/>Com esta opção, obter o SLA/limitado, primeiro 15 dias depois de iniciar Olá ponto final de transmissão em fluxo está livre.<br/>Se criar mais de um pontos finais de transmissão em fluxo, apenas hello primeiro um é gratuito em Olá primeiro 15 dias, Olá outros são faturados assim que iniciá-los. <br/>Tenha em atenção que versão de avaliação gratuita só se aplica toonewly criada contas de serviços de suporte de dados e o ponto final de transmissão em fluxo predefinido. Pontos finais de transmissão em fluxo existentes e os pontos finais de transmissão em fluxo adicionalmente criados não inclui a avaliação gratuita período mesmo são atualizados tooversion 2.0 ou são criadas como versão 2.0.
**Premium**|Esta opção é adequada para profissionais cenários que necessitam de escala superior ou um controlo.<br/>SLA de variável com base na capacidade premium transmissão em fluxo unidade (SU) adquirida, dedicados pontos finais de transmissão em fluxo em direto num ambiente isolado e não competem para ter recursos.

Para obter mais informações, consulte Olá **transmissão em fluxo comparar tipos** secção a seguir.

### <a name="classic-type-version-10"></a>Tipo clássico (versão 1.0)

Para os utilizadores que criar contas de AMS versão 10 de Janeiro de 2017 toohello anterior, tem um **clássico** tipo de um ponto final de transmissão em fluxo. Este tipo faz parte de Olá "1.0" de versão do ponto final de transmissão em fluxo.

Se o **versão "1.0"** ponto final de transmissão em fluxo tem > = 1 premium de transmissão em fluxo unidades (SU), este será o ponto final de transmissão em fluxo premium e irá fornecer todas as funcionalidades de AMS (tal como Olá **padrão/Premium** tipo) sem quaisquer passos de configuração adicionais.

>[!NOTE]
>**Clássico** pontos finais de transmissão em fluxo (versão "1.0" e 0 SU), fornece funcionalidades limitadas e não inclui um SLA. Recomenda-se toomigrate demasiado**padrão** escreva tooget uma melhor experiência e toouse as funcionalidades de como o empacotamento dinâmico ou de encriptação e de outras funcionalidades que vêm com Olá **padrão** tipo. toomigrate toohello **padrão** escreva, visite toohello [portal do Azure](https://portal.azure.com/) e selecione **opção tooStandard**. Para obter mais informações sobre a migração, consulte Olá [migração](#migration-between-types) secção.
>
>Cuidado com que esta operação não pode ser revertida e tem um impacto de preço.
>
 
## <a name="comparing-streaming-types"></a>Comparar tipos de transmissão em fluxo

### <a name="versions"></a>Versões

|Tipo|StreamingEndpointVersion|ScaleUnits|CDN|Faturação|SLA| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|Clássica|1.0|0|ND|Gratuito|ND|
|Ponto Final de Transmissão em Fluxo Standard|2.0|0|Sim|Pago|Sim|
|Unidades de Transmissão em Fluxo Premium|1.0|>0|Sim|Pago|Sim|
|Unidades de Transmissão em Fluxo Premium|2.0|>0|Sim|Pago|Sim|

### <a name="features"></a>Funcionalidades

Funcionalidade|Standard|Premium
---|---|---
Liberte primeiro 15 dias| Sim |Não
Débito |Cópia de segurança too600 Mbps quando não for utilizada o CDN do Azure. Escalas CDN.|200 Mbps por transmissão em fluxo unidade (SU). Escalas CDN.
SLA | 99.9|99,9 (200 Mbps por SU).
CDN|CDN do Azure, terceiros CDN ou nenhum CDN.|CDN do Azure, terceiros CDN ou nenhum CDN.
A faturação é proporcional| Diariamente|Diariamente
Encriptação dinâmica|Sim|Sim
Empacotamento dinâmico|Sim|Sim
Escala|Dimensiona automaticamente cópias de segurança toohello direcionado débito.|Unidades de transmissão em fluxo adicionais
Anfitrião de filtragem/G20/personalizada IP|Sim|Sim
Transferência progressiva|Sim|Sim
Utilização recomendada |Recomenda a vasta maioria de Olá de cenários de transmissão em fluxo.|Utilização profissionais.<br/>Se considerar que poderá ter necessidades para além de padrão. Contacte-nos (amsstreaming microsoft.com,) se espera que um tamanho de audiência em simultâneo com mais de 50 000 visualizadores autorizados.


## <a name="migration-between-types"></a>Migração entre tipos

Do | demasiado| Ação
---|---|---
Clássica|Standard|É necessário tooopt-in
Clássica|Premium| Escala (adicional de unidades de transmissão em fluxo)
Padrão/Premium|Clássica|Não está disponível (se a versão do ponto final de transmissão em fluxo é 1.0. É permitido toochange tooclassic com definição scaleunits demasiado "0")
Padrão (com/sem CDN)|Premium com Olá mesmas configurações|Permitido no Olá **iniciado** estado. (através do portal do Azure)
Premium (com/sem CDN)|Standard com Olá mesmas configurações|Permitido no Olá **iniciado** Estado (através do portal do Azure)
Padrão (com/sem CDN)|Premium com configuração diferente|Permitido no Olá **parado** Estado (através do portal do Azure). Não é permitida no estado de execução de Olá.
Premium (com/sem CDN)|Standard com configuração diferente|Permitido no Olá **parado** Estado (através do portal do Azure). Não é permitida no estado de execução de Olá.
Versão 1.0 com SU > = 1 de CDN|Padrão/Premium não CDN|Permitido no Olá **parado** estado. Não é permitido no Olá **iniciado** estado.
Versão 1.0 com SU > = 1 de CDN|Standard com/sem CDN|Permitido no Olá **parado** estado. Não é permitido no Olá **iniciado** estado. Versão 1.0 CDN irá ser eliminado e nova criada e iniciado.
Versão 1.0 com SU > = 1 de CDN|Premium com/sem CDN|Permitido no Olá **parado** estado. Não é permitido no Olá **iniciado** estado. CDN clássico irá ser eliminado e nova criada e iniciado.

## <a name="next-steps"></a>Passos seguintes
Rever os percursos de aprendizagem dos Serviços de Multimédia

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

