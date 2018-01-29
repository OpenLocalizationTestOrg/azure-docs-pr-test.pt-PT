---
title: "Configurar a localização de Recortador de suporte de dados do Azure | Microsoft Docs"
description: "Saiba mais sobre o suporte de localização e idiomas Recortador de suporte de dados do Azure suportada"
services: media-services
keywords: "Clip; subclip codificação; suporte de dados"
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: dd0fc87741befd92cc41d0129fafcbc64db7ec9e
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/07/2017
---
# <a name="configure-localization"></a>Configurar a localização
Recortador de suporte de dados do Azure está disponível em 18 idiomas. Para definir o idioma de widget, tem de definir o `language` parâmetro durante a inicialização. Passagem da cadeia de código de idioma pretendido na lista seguinte:
- Chinês (simplificado): zh-hans
- Chinês (tradicional): zh-hant
- Checo: cs
- Neerlandês, Flemish: nl
- Inglês: en
- Francês: fr
- Alemão: Alemanha
- Húngaro: hu
- Italiano:-
- Japonês: ja
- Coreano: ko
- Polaco: LP
- Português (Brasil): pt-br
- Português (Portugal): pt-pt
- Russo: ru
- Espanhol: es
- Sueco: sv
- Turco: tr

Para definir um dicionário de idioma personalizado ou expandir o dicionário de idioma predefinido, tem de definir o `languages` ou `extraLanguages` parâmetro, respetivamente. Transmita um dicionário personalizado utilizando o seguinte formato JSON:

```javascript
{
    '{language-code}': {
        '{message-id}': '{message}',
        ...
    }
    ...
}
```

Por exemplo, o exemplo seguinte define as cadeias localizadas em inglês:

```javascript
{
    'en': {
        'VideoPlayer.noPreview': 'No video preview',
        'VideoPlayer.loadAsset': 'You must provide a valid asset',
        'AssetsPanel.name': 'Name',
        'AssetsPanel.type': 'Asset type',
        'AssetsPanel.actions': 'Actions',
        'AssetsPanel.loading': 'Loading...',
        'AssetsPanel.duration': 'Duration',
        'AssetsPanel.resolution': 'Resolution',
        'AssetsPanel.pluralFiles': '{0} assets',
        'AssetsPanel.searchFiles': 'Search assets',
        'AssetsPanel.showTypes': 'Show:',
        'AssetsPanel.typesInfo': 'Rendered assets are actual MP4 files. Dynamic manifest filters are filters applied to a parent asset\'s video segment playlist.',
        'AssetsPanel.filterTypes': 'Filters',
        'AssetsPanel.assetTypes': 'Assets',
        'AssetsPanel.assetsAll': 'All',
        'AssetsPanel.addAsset': 'Add asset to the end',
        'AssetsPanel.addFilter': 'Add filter to the timeline',
        'AssetsPanel.invalidAsset': 'The metadata of this asset is not compatible with the other assets in the timeline',
        'AssetsPanel.addAssetWarning': 'Subclipping on assets with different resolutions may cause resolution autoscaling.',
        'AssetsPanel.live': 'LIVE',
        'AssetsPanel.unknown': 'UNKNOWN',
        'AssetsPanel.minimGapNotMet': 'The asset duration must be greater than the minimum clip duration ({0} seconds)',
        'VideoPlayer.openAdvancedSettings': 'Advanced settings',
        'VideoPlayer.singleBitrate': 'Single-bitrate MP4 (rendered)',
        'VideoPlayer.multiBitrate': 'Multi-bitrate MP4 (rendered)',
        'VideoPlayer.dynamicManifest': 'Dynamic manifest filter',
        'VideoPlayer.ErrorWithMessage': 'There was an error in the video player, code {0}, message: {1}',
        'Common.cancel': 'Cancel',
        'Common.OK': 'OK',
        'AdvancedSettings.framerate': 'Frame rate',
        'Dropdown.select': 'Select an option...',
        'InputAsset.RemoveInput': 'Remove source',
        'Zoom.startTime': 'Start time',
        'Zoom.endTime': 'End time',
        'VideoPlayer.subclips': 'Subclips:',
        'VideoPlayer.length': 'Clip length:',
        'Accordion.scrollLeft': 'Scroll to the left',
        'Accordion.scrollRight': 'Scroll to the right',
        'AdvancedSettings.title': 'Advanced settings',
        'AdvancedSettings.subclipName': 'Subclip name',
        'AdvancedSettings.subclipType': 'Subclipping mode',
        'AdvancedSettings.includeAudioTracks': 'Include audio tracks',
        'AdvancedSettings.subclipTypeInfo': 'Single-bitrate and multi-bitrate MP4s are frame accurate rendered assets. Dynamic manifest filters are group-of-pictures (GOP) accurate filters applied to a parent asset. Creating filters does not create a new asset and does not require encoding. Subclipping jobs on live assets are valid as long as their mark times are within the archive window of the parent asset. Filters are valid as long as the parent asset exists and mark times are within its archive window.',
        'AdvancedSettings.frameRateInfo': 'We autodetect frame rate under most scenarios. however, If we cannot autodetect, choose a frame rate from the dropdown for the selected asset(s).',
        'AdvancedSettings.frameRateError': 'Unable to determine frame rate',
        'AdvancedSettings.subclipNameInfo': 'Choose a name for your subclip.',
        'AdvancedSettings.singleAudioTrack': '1 audio track selected',
        'AdvancedSettings.allAudioTracks': 'All audio tracks selected',
        'AdvancedSettings.someAudioTracks': '{0} audio tracks selected',
        'AdvancedSettings.includeAllAudioTracks': 'Include all audio tracks',
        'AssetsPanel.loadingError': 'Failed to retreive assets from server.',
        'AssetsPanel.retry': 'Retry?',
        'CommandBar.prevFrameTitle': 'Move one frame backwards',
        'CommandBar.prevKeyFrameTitle': 'Move one GOP backwards',
        'CommandBar.cleanJob': 'Remove all assets',
        'CommandBar.cleanJobTitle': 'Remove all assets from timeline',
        'CommandBar.cleanJobMessage': 'This will empty all video clips from your timeline.',
        'CommandBar.update': 'Update filter',
        'CommandBar.createFilter': 'Create filter',
        'CommandBar.submit': 'Submit subclipper job',
        'CommandBar.jobErrorTitle': 'Operation failed',
        'CommandBar.jobErrorMessage': 'Your subclip failed to submit. Please try again.',
        'CommandBar.markInTitle': 'Set in at playhead',
        'CommandBar.markInPosition': 'Mark in timecode',
        'CommandBar.markOutTitle': 'Set out at playhead',
        'CommandBar.markOutPosition': 'Mark out timecode',
        'CommandBar.nextFrameTitle': 'Move one frame forward',
        'CommandBar.nextKeyFrameTitle': 'Move one GOP forward',
        'CommandBar.play': 'Play video',
        'CommandBar.pause': 'Pause video',
        'CommandBar.playPreviewTitle': 'Play subclip preview',
        'CommandBar.pausePreviewTitle': 'Pause subclip preview',
        'CommandBar.redoTitle': 'Redo last action',
        'CommandBar.removeAsset': 'Remove current asset',
        'CommandBar.undoTitle': 'Undo last action',
        'VideoPlayer.errorTitle': 'Error',
        'VideoPlayer.errorMessage': 'There was an error loading the selected asset.',
        'Timeline.markIn': 'Mark in bracket',
        'Timeline.markOut': 'Mark out bracket',
        'Timeline.playHead': 'Play head'
    }
}
```

## <a name="next-steps"></a>Passos seguintes
Consulte os passos seguintes para configurar o Recortador de suporte de dados do Azure:
- [Carregar recursos para o Recortador de suporte de dados do Azure](media-services-azure-media-clipper-load-assets.md)
- [Configurar os atalhos de teclado personalizado](media-services-azure-media-clipper-keyboard-shortcuts.md)
- [Submeter tarefas de recorte do Recortador](media-services-azure-media-clipper-submit-job.md)