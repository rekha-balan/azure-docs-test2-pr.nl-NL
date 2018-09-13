---
title: Configure Azure Media Clipper localization | Microsoft Docs
description: Learn about Azure Media Clipper supported languages and localization support
services: media-services
keywords: clip;subclip;encoding;media
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: dd0fc87741befd92cc41d0129fafcbc64db7ec9e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969258"
---
# <a name="configure-localization"></a><span data-ttu-id="fc98c-104">Configure localization</span><span class="sxs-lookup"><span data-stu-id="fc98c-104">Configure localization</span></span>
<span data-ttu-id="fc98c-105">Azure Media Clipper is available in 18 languages.</span><span class="sxs-lookup"><span data-stu-id="fc98c-105">Azure Media Clipper is available in 18 languages.</span></span> <span data-ttu-id="fc98c-106">To set the widget language, you must define the `language` parameter during initialization.</span><span class="sxs-lookup"><span data-stu-id="fc98c-106">To set the widget language, you must define the `language` parameter during initialization.</span></span> <span data-ttu-id="fc98c-107">Pass in the desired language code string from the following list:</span><span class="sxs-lookup"><span data-stu-id="fc98c-107">Pass in the desired language code string from the following list:</span></span>
- <span data-ttu-id="fc98c-108">Chinese (Simplified): zh-hans</span><span class="sxs-lookup"><span data-stu-id="fc98c-108">Chinese (Simplified): zh-hans</span></span>
- <span data-ttu-id="fc98c-109">Chinese (Traditional): zh-hant</span><span class="sxs-lookup"><span data-stu-id="fc98c-109">Chinese (Traditional): zh-hant</span></span>
- <span data-ttu-id="fc98c-110">Czech: cs</span><span class="sxs-lookup"><span data-stu-id="fc98c-110">Czech: cs</span></span>
- <span data-ttu-id="fc98c-111">Dutch, Flemish: nl</span><span class="sxs-lookup"><span data-stu-id="fc98c-111">Dutch, Flemish: nl</span></span>
- <span data-ttu-id="fc98c-112">English: en</span><span class="sxs-lookup"><span data-stu-id="fc98c-112">English: en</span></span>
- <span data-ttu-id="fc98c-113">French: fr</span><span class="sxs-lookup"><span data-stu-id="fc98c-113">French: fr</span></span>
- <span data-ttu-id="fc98c-114">German: de</span><span class="sxs-lookup"><span data-stu-id="fc98c-114">German: de</span></span>
- <span data-ttu-id="fc98c-115">Hungarian: hu</span><span class="sxs-lookup"><span data-stu-id="fc98c-115">Hungarian: hu</span></span>
- <span data-ttu-id="fc98c-116">Italian: it</span><span class="sxs-lookup"><span data-stu-id="fc98c-116">Italian: it</span></span>
- <span data-ttu-id="fc98c-117">Japanese: ja</span><span class="sxs-lookup"><span data-stu-id="fc98c-117">Japanese: ja</span></span>
- <span data-ttu-id="fc98c-118">Korean: ko</span><span class="sxs-lookup"><span data-stu-id="fc98c-118">Korean: ko</span></span>
- <span data-ttu-id="fc98c-119">Polish: pl</span><span class="sxs-lookup"><span data-stu-id="fc98c-119">Polish: pl</span></span>
- <span data-ttu-id="fc98c-120">Portuguese (Brazil): pt-br</span><span class="sxs-lookup"><span data-stu-id="fc98c-120">Portuguese (Brazil): pt-br</span></span>
- <span data-ttu-id="fc98c-121">Portuguese (Portugal): pt-pt</span><span class="sxs-lookup"><span data-stu-id="fc98c-121">Portuguese (Portugal): pt-pt</span></span>
- <span data-ttu-id="fc98c-122">Russian: ru</span><span class="sxs-lookup"><span data-stu-id="fc98c-122">Russian: ru</span></span>
- <span data-ttu-id="fc98c-123">Spanish: es</span><span class="sxs-lookup"><span data-stu-id="fc98c-123">Spanish: es</span></span>
- <span data-ttu-id="fc98c-124">Swedish: sv</span><span class="sxs-lookup"><span data-stu-id="fc98c-124">Swedish: sv</span></span>
- <span data-ttu-id="fc98c-125">Turkish: tr</span><span class="sxs-lookup"><span data-stu-id="fc98c-125">Turkish: tr</span></span>

<span data-ttu-id="fc98c-126">To set a custom language dictionary or extend the default language dictionary, you must define the `languages` or `extraLanguages` parameter, respectively.</span><span class="sxs-lookup"><span data-stu-id="fc98c-126">To set a custom language dictionary or extend the default language dictionary, you must define the `languages` or `extraLanguages` parameter, respectively.</span></span> <span data-ttu-id="fc98c-127">Pass in a custom dictionary using the following JSON format:</span><span class="sxs-lookup"><span data-stu-id="fc98c-127">Pass in a custom dictionary using the following JSON format:</span></span>

```javascript
{
    '{language-code}': {
        '{message-id}': '{message}',
        ...
    }
    ...
}
```

<span data-ttu-id="fc98c-128">For example, the following sample defines the localized English strings:</span><span class="sxs-lookup"><span data-stu-id="fc98c-128">For example, the following sample defines the localized English strings:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fc98c-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc98c-129">Next steps</span></span>
<span data-ttu-id="fc98c-130">See the next steps for configuring Azure Media Clipper:</span><span class="sxs-lookup"><span data-stu-id="fc98c-130">See the next steps for configuring Azure Media Clipper:</span></span>
- [<span data-ttu-id="fc98c-131">Loading assets into Azure Media Clipper</span><span class="sxs-lookup"><span data-stu-id="fc98c-131">Loading assets into Azure Media Clipper</span></span>](media-services-azure-media-clipper-load-assets.md)
- [<span data-ttu-id="fc98c-132">Configuring custom keyboard shortcuts</span><span class="sxs-lookup"><span data-stu-id="fc98c-132">Configuring custom keyboard shortcuts</span></span>](media-services-azure-media-clipper-keyboard-shortcuts.md)
- [<span data-ttu-id="fc98c-133">Submitting clipping jobs from the Clipper</span><span class="sxs-lookup"><span data-stu-id="fc98c-133">Submitting clipping jobs from the Clipper</span></span>](media-services-azure-media-clipper-submit-job.md)