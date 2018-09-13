---
title: Create an Azure Media Services Job input from a local file | Microsoft Docs
description: This topic shows how to create a job input from a local file.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: 94e7192e13397ad8ec973d92f4c538f430c9cd60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865516"
---
# <a name="create-a-job-input-from-a-local-file"></a>Create a job input from a local file

In Media Services v3, when you submit Jobs to process your videos, you have to tell Media Services where to find the input video. The input video can be stored as a Media Service Asset, in which case you create an input asset based on a file (stored locally or in Azure Blob storage). This topic shows how to create a job input from a local file. For a full example, see this [github sample](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs).

## <a name="net-sample"></a>.NET sample

The following code shows how to create an input asset and use it as the input for the job. The CreateInputAsset function performs the following actions:

* Creates the Asset 
* Gets a writable [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) to the Asset’s [container in storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet?tabs=windows#upload-blobs-to-the-container)
* Uploads the file into the container in storage using the SAS URL

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#CreateInputAsset)]

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#SubmitJob)]

## <a name="next-steps"></a>Next steps

[Create a job input from an HTTP(s) URL](job-input-from-http-how-to.md).
