---
title: " Upload files into a Media Services account using the Azure portal | Microsoft Docs"
description: This tutorial walks you through the steps of uploading files into a Media Services account using the Azure portal
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/13/2017
ms.author: juliako
ms.openlocfilehash: cda15d78962809f3eb84eddc935a04bb8e4dcf6d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563041"
---
# <a name="upload-files-into-a-media-services-account-using-the-azure-portal"></a>Upload files into a Media Services account using the Azure portal
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> To complete this tutorial, you need an Azure account. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/). 
> 


In Media Services, you upload your digital files into an asset. The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.


## <a name="upload-files"></a>Upload files

>[!NOTE]
>There is a limit to the maximum file size supported for processing in Media Services. Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.
>

1. In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.
2. On the **Settings** blade, click **Assets**.
   
    ![Upload files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-upload.png)
3. Click the **Upload** button.
   
    The **Upload a video asset** window appears.
   
   > [!NOTE]
   > There is no file size limitation.
   > 
   > 
4. Browse to the desired video on your computer, select it, and hit OK.  
   
    The upload starts and you can see the progress under the file name.  

Once the upload completes, you will see the new asset listed in the **Assets** window. 

## <a name="next-steps"></a>Next steps
You can now encode your uploaded assets. For more information, see [Encode assets](media-services-portal-encode.md).

You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container. For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


