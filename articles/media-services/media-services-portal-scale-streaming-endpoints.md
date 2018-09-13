---
title: Scale streaming endpoints with the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of scaling streaming endpoints with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: bbcaef70f10ec325a2ce637294b7e3c0a1d4da1c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556291"
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a>Scale streaming endpoints with the Azure portal
## <a name="overview"></a>Overview

> [!NOTE]
> To complete this tutorial, you need an Azure account. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

This topic is useful for customers who have **Streaming Endpoint** of the **Premium** type. For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.
 
When you have a **Premium** type, by default you get 1 streaming unit (SU). If you need to scale your streaming endpoint, follow the steps in this topic.

For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).

## <a name="scale-streaming-endpoints"></a>Scale streaming endpoints

To create and change the number of streaming units, do the following:

1. In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.
2. In the **Settings** window, select **Streaming endpoints**.
3. Click on the streaming endpoint that you want to scale. 
4. Move the slider to specify the number of streaming units.

![Streaming endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a>Next steps
Review Media Services learning paths.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


