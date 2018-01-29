---
title: Carregar recursos para o Recortador de suporte de dados do Azure | Microsoft Docs
description: Passos para carregar recursos para o Recortador de suporte de dados do Azure
services: media-services
keywords: "Clip; subclip codificação; suporte de dados"
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: 6a479218ff8bd5addf4273b23c06380859e0ea08
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/07/2017
---
# <a name="loading-assets-into-azure-media-clipper"></a>Carregar recursos para o Recortador de suporte de dados do Azure
Ativos podem ser carregados para o Recortador de suporte de dados do Azure por dois métodos:
1. Estaticamente transmitir numa biblioteca de recursos
2. Gerar dinamicamente uma lista de recursos através de API

## <a name="statically-load-videos-into-clipper"></a>Estaticamente carregar vídeos para Recortador
Carregue estaticamente vídeos para o Recortador para permitir que os utilizadores finais criar aplicações de clips sem selecionar vídeos a partir do painel de seleção de elemento.

Neste caso, que passa um conjunto de elementos estático para o Recortador. Cada elemento inclui um ID de recurso/filter AMS, nome, publicado URL de transmissão em fluxo. Se aplicável, um token de autenticação de proteção de conteúdos ou uma matriz de miniatura URLs podem ser passados. Se transmitido, as miniaturas são preenchidas na interface do. Em cenários em que a biblioteca de recurso é estático e em pequenos, pode passar no contrato ativo para cada recurso na biblioteca.

> [!NOTE]
> Quando o carregamento estaticamente recursos para o Recortador, ativos são adicionados **diretamente para a linha cronológica** e **painel de recurso não é composto**. O primeiro elemento é adicionado a linha cronológica e o resto dos ativos são empilhadas no lado direito da linha cronológica).

Para carregar uma biblioteca de elemento estático, utilize o **carregar** método para passar uma representação JSON de cada recurso. O exemplo de código seguinte ilustra a representação JSON para um recurso.

```javascript
var assets = [
    {
      /* Required: represents the Azure Media Services asset Id when "type" === "asset"; otherwise, represents the dynamic manifest asset filter Id ("type" === "filter")  */
      "id": "my-asset-or-dynamic-manifest-asset-filter-id",
    
      /* Required: represents the asset name as shown in the Clipper interface */
      "name": "My Asset or Dynamic Manifest Asset Filter Name",
    
      /* Required: must be one of the following values: "asset" or "filter" */
      /* NOTE: "asset" type represents a rendered asset; "filter" type represents a dynamic manifest asset filter */
      "type": "asset",
    
      /* Required */
      "source": {
    
        /* Required: represents the asset streaming locator, the base Smooth Streaming URL */
        "src": "//amssamples.streaming.mediaservices.windows.net/91492735-c523-432b-ba01-faba6c2206a2/AzureMediaServicesPromo.ism/manifest",
    
        /* Optional: default value "application/vnd.ms-sstr+xml" */
        "type": "application/vnd.ms-sstr+xml",
    
        /* Required: If the asset has content protection applied, then you must include an array with the different protection types along with the token to request the license/key; otherwise, provide an empty array */
        "protectionInfo": [{
            "type": "AES",
            "authenticationToken": "Bearer aes-token-placeholder"
          },
          {
            "type": "PlayReady",
            "authenticationToken": "Bearer playready-token-placeholder"
          },
          {
            "type": "Widevine",
            "authenticationToken": "Bearer widevine-token-placeholder"
          },
          {
            "type": "FairPlay",
            "certificateUrl": "//example/path/to/myfairplay.der",
            "authenticationToken": "Bearer fairplay-token-placeholder"
          }
        ]
      },
    
      /* Optional: array containing thumbnail URLs for the video. */
      /* NOTE: For the thumbnail URLs to work as expected in the Clipper timeline they must be evenly distributed across the video (based on the duration) and in chronological order within the array. */
      "thumbnails": [
        "//example/path/thumbnail_001.jpg",
        "//example/path/thumbnail_002.jpg",
        "//example/path/thumbnail_003.jpg",
        "//example/path/thumbnail_004.jpg",
        "//example/path/thumbnail_005.jpg"
        ]
    }
];

var subclipper = new subclipper({
    selector: '#root',
    restVersion: '2.0',
    submitSubclipCallback: onSubmitSubclip,
});
subclipper.ready(function () {
    subclipper.load(assets);
});

```

> [!NOTE]
> Recomenda-se a cadeia de chamar o método load() com o método de ready(handler) conforme mostrado no exemplo anterior. O exemplo anterior garante que a miniaplicação está preparada antes de carregar os recursos.

> [!NOTE]
> Para a miniatura URLs a funcionar conforme esperado na linha de tempo Recortador tem de ser uniformemente distribuídos entre o vídeo (com base na duração) e por ordem cronológica dentro da matriz. Pode utilizar o seguinte fragmento predefinido de JSON como uma referência de exemplo para a criação de imagens com o processador "Codificador de multimédia Standard":

```json
{
  "Start": "0",
  "Step": "00:00:05",
  "Range": "100%",
  "Type": "PngImage",
  "PngLayers": [
    {
      "Type": "PngLayer",
      "Width": 48,
      "Height": 26
    }
  ]
}
```

## <a name="dynamically-load-videos-in-clipper"></a>Dinamicamente, carregar vídeos no Recortador
Dinamicamente, carregar vídeos para o Recortador para permitir que os utilizadores finais selecionar os vídeos do painel de seleção de recurso para recortar contra.

Em alternativa, pode carregar recursos dinamicamente através de uma chamada de retorno. Em cenários onde ativos são gerados dinamicamente ou a biblioteca de grandes dimensões, deverá carregar através de chamada de retorno. Para carregar o recurso dinamicamente, tem de implementar a função de chamada de retorno onLoadAssets opcional. Esta função é passada para o Recortador em inicialização. Os ativos resolver devem cumprir o mesmo contrato que ativos estaticamente carregados. O exemplo de código seguinte ilustra a assinatura do método, a entrada esperada e o resultado esperado.

> [!NOTE]
> Quando o carregamento dinamicamente recursos para o Recortador, ativos são apresentados no **painel de seleção de elemento**.

```javascript
// Video Assets Pane Callback
    //
    // Filter Parameters:
    // - search: string value term that will be used in the back-end to filter assets by name.
    // - skip: int value used for pagination in the back-end that allows skipping a number of assets in the response.
    // - take: int value used for pagination in the back-end that allows defining the number of assets to include in the response.
    // - type: ('filter', 'asset') value that will be used in the back-end to filter assets by type.
    //
    // Returns: a Promise object that, when resolved, retuns an object containing an array of assets (input contract)
    //          that satisfies the filter parameters, plus optionally the total types of files available:
    // {
    //  total: 100,
    //  assets: [{...}],
    // }
    var onLoadAssets = function (search, skip, take, type) {
        var promise = new Promise(function (resolve, reject) {
            // TODO: implement the getAssetsFromBackend method to get the assets from the back-end using the filter parameters (search, skip, take, type).
            getAssetsFromBackend(search, skip, take, type)
                .then(function (assets) {
                    resolve({
                        total: assets.length,
                        assets: assets
                    });
                }).catch(function () {
                    reject(Error("error details"));
                });
        });
    
        return promise;
    };

    // Create widget instance:
    // - using a root element selector
    // - enabling the Video Assets panel by registering a callback in the 'assetsPanelLoaderCallback' option parameter.
    var widget = new subclipper({
        selector: '#root',

        // Enable the Video Assets panel in the widget to automatically load assets (input contract)
        assetsPanelLoaderCallback: onLoadAssets
    });

    // ...
    // The widget will automatically invoke the 'assetsPanelLoaderCallback' callback with the filter parameters specified by the user 
    // and load assets returned by the Promise into the Video Assets panel.
    // ...
```