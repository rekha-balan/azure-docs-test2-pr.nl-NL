---
title: Create clips with Azure Media Clipper | Microsoft Docs
description: Overview of Azure Media Clipper, a tool for building media clips from assets
services: media-services
keywords: clip;subclip;encoding;media
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: f3822386d0d16b1feaf16853424329558a18f910
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867534"
---
# <a name="create-clips-with-azure-media-clipper"></a>Create clips with Azure Media Clipper
Azure Media Clipper is a free JavaScript library that enables web developers to provide their users with an interface for creating media clips. This tool can be integrated into any web page and provides APIs for loading assets and submitting clipping jobs.

Azure Media Clipper enables you to:
- Trim the pre-slate and post-slate from live archives 
- Compose video highlights from AMS live events, live archives, or fMP4 VOD files 
- Concatenate videos from multiple sources 
- Produce summary clips from your AMS media assets 
- Clip videos with frame accuracy 
- Generate dynamic manifest filters over existing live and VOD assets with group-of-pictures (GOP) accuracy 
- Produce encoding jobs against the assets in your media services account

To request new features, provide ideas or feedback, submit to [UserVoice for Azure Media Services](http://aka.ms/amsvoice/). If you have and specific issues, questions or find any bugs, drop the Media Services team a line at amcinfo@microsoft.com.

The following image illustrates the Clipper interface: ![Azure Media Clipper](media/media-services-azure-media-clipper-overview/media-services-azure-media-clipper-interface.PNG)

## <a name="release-notes"></a>Release notes
See the following list for the Clipper blog post, various known issues, and changelog for the latest release of the Clipper:
- [Blog post](https://azure.microsoft.com/blog/azure-media-clipper/)
- [Known issues list](https://amp.azure.net/libs/amc/latest/docs/known_issues.html)
- [Changelog](https://amp.azure.net/libs/amc/latest/docs/changelog.html)

## <a name="browser-support"></a>Browser support
Azure Media Clipper is built using modern HTML5 technologies and supports the following browsers:

- Microsoft Edge 13+
- Internet Explorer 11+
- Chrome 54+
- Safari 10+
- Firefox 50+

> [!NOTE]
> Only HTML5 playback of streams from Azure Media Services is currently supported.

## <a name="language-support"></a>Language support
The Clipper widget is available in the following 18 languages:
- Chinese (Simplified)
- Chinese (Traditional)
- Czech
- Dutch, Flemish
- English
- French
- German
- Hungarian
- Italian
- Japanese
- Korean
- Polish
- Portuguese (Brazil)
- Portuguese (Portugal)
- Russian
- Spanish
- Swedish
- Turkish

## <a name="next-steps"></a>Next steps
To get started using Azure Media Clipper, read the [getting started](media-services-azure-media-clipper-getting-started.md) article for details on how to deploy the widget.