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
# <a name="create-a-job-input-from-a-local-file"></a><span data-ttu-id="7956d-103">Create a job input from a local file</span><span class="sxs-lookup"><span data-stu-id="7956d-103">Create a job input from a local file</span></span>

<span data-ttu-id="7956d-104">In Media Services v3, when you submit Jobs to process your videos, you have to tell Media Services where to find the input video.</span><span class="sxs-lookup"><span data-stu-id="7956d-104">In Media Services v3, when you submit Jobs to process your videos, you have to tell Media Services where to find the input video.</span></span> <span data-ttu-id="7956d-105">The input video can be stored as a Media Service Asset, in which case you create an input asset based on a file (stored locally or in Azure Blob storage).</span><span class="sxs-lookup"><span data-stu-id="7956d-105">The input video can be stored as a Media Service Asset, in which case you create an input asset based on a file (stored locally or in Azure Blob storage).</span></span> <span data-ttu-id="7956d-106">This topic shows how to create a job input from a local file.</span><span class="sxs-lookup"><span data-stu-id="7956d-106">This topic shows how to create a job input from a local file.</span></span> <span data-ttu-id="7956d-107">For a full example, see this [github sample](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="7956d-107">For a full example, see this [github sample](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs).</span></span>

## <a name="net-sample"></a><span data-ttu-id="7956d-108">.NET sample</span><span class="sxs-lookup"><span data-stu-id="7956d-108">.NET sample</span></span>

<span data-ttu-id="7956d-109">The following code shows how to create an input asset and use it as the input for the job.</span><span class="sxs-lookup"><span data-stu-id="7956d-109">The following code shows how to create an input asset and use it as the input for the job.</span></span> <span data-ttu-id="7956d-110">The CreateInputAsset function performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="7956d-110">The CreateInputAsset function performs the following actions:</span></span>

* <span data-ttu-id="7956d-111">Creates the Asset</span><span class="sxs-lookup"><span data-stu-id="7956d-111">Creates the Asset</span></span> 
* <span data-ttu-id="7956d-112">Gets a writable [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) to the Asset’s [container in storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet?tabs=windows#upload-blobs-to-the-container)</span><span class="sxs-lookup"><span data-stu-id="7956d-112">Gets a writable [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) to the Asset’s [container in storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet?tabs=windows#upload-blobs-to-the-container)</span></span>
* <span data-ttu-id="7956d-113">Uploads the file into the container in storage using the SAS URL</span><span class="sxs-lookup"><span data-stu-id="7956d-113">Uploads the file into the container in storage using the SAS URL</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#CreateInputAsset)]

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#SubmitJob)]

## <a name="next-steps"></a><span data-ttu-id="7956d-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="7956d-114">Next steps</span></span>

<span data-ttu-id="7956d-115">[Create a job input from an HTTP(s) URL](job-input-from-http-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="7956d-115">[Create a job input from an HTTP(s) URL](job-input-from-http-how-to.md).</span></span>
