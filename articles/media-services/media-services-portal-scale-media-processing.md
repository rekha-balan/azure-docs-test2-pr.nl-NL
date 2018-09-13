---
title: " Scale Media Processing using the Azure portal | Microsoft Docs"
description: This tutorial walks you through the steps of scaling Media Processing using the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: juliako
ms.openlocfilehash: a1cdaae82b7135a5108e8f846e32b98a3ba4892f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671264"
---
# <a name="change-the-reserved-unit-type"></a>Change the reserved unit type
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Overview
> [!IMPORTANT]
> Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.
> 
> 

## <a name="scale-media-processing"></a>Scale media processing
To change the reserved unit type and the number of reserved units, do the following:

1. In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.
2. In the **Settings** window, select **Media reserved units**.
   
    To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider.
   
    To change the **RESERVED UNIT TYPE**, press S1, S2, or S3.
   
    ![Processors page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Press the SAVE button to save your changes.
   
    The new reserved units are allocated when you press SAVE.

## <a name="next-steps"></a>Next steps
Review Media Services learning paths.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


