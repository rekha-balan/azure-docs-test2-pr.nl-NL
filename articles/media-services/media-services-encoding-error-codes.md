---
title: Azure Media Services encoding error codes | Microsoft Docs
description: This topic lists error codes that could be returned in case an error was encountered during the encoding task execution..
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: d1e6421404d9c8845eb3ccd30d84c0c8cf5930b8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563775"
---
# <a name="encoding-error-codes"></a><span data-ttu-id="ce379-103">Encoding error codes</span><span class="sxs-lookup"><span data-stu-id="ce379-103">Encoding error codes</span></span>

<span data-ttu-id="ce379-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span><span class="sxs-lookup"><span data-stu-id="ce379-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="ce379-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="ce379-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="ce379-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span><span class="sxs-lookup"><span data-stu-id="ce379-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="ce379-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="ce379-107">ErrorDetail.Code</span></span> | <span data-ttu-id="ce379-108">Possible causes for error</span><span class="sxs-lookup"><span data-stu-id="ce379-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="ce379-109">Unknown</span><span class="sxs-lookup"><span data-stu-id="ce379-109">Unknown</span></span> |<span data-ttu-id="ce379-110">Unknown error while executing the task</span><span class="sxs-lookup"><span data-stu-id="ce379-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="ce379-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="ce379-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="ce379-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span><span class="sxs-lookup"><span data-stu-id="ce379-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="ce379-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="ce379-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="ce379-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span><span class="sxs-lookup"><span data-stu-id="ce379-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="ce379-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="ce379-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="ce379-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span><span class="sxs-lookup"><span data-stu-id="ce379-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="ce379-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="ce379-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="ce379-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span><span class="sxs-lookup"><span data-stu-id="ce379-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="ce379-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="ce379-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="ce379-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span><span class="sxs-lookup"><span data-stu-id="ce379-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="ce379-121">For example, trying to produce an audio-only output from an asset that has only video</span><span class="sxs-lookup"><span data-stu-id="ce379-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="ce379-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="ce379-122">ErrorProcessingTask</span></span> |<span data-ttu-id="ce379-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span><span class="sxs-lookup"><span data-stu-id="ce379-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="ce379-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="ce379-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="ce379-125">Category of errors when uploading the output asset</span><span class="sxs-lookup"><span data-stu-id="ce379-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="ce379-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="ce379-126">ErrorCancelingTask</span></span> |<span data-ttu-id="ce379-127">Category of errors to cover failures when attempting to cancel the Task</span><span class="sxs-lookup"><span data-stu-id="ce379-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="ce379-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="ce379-128">TransientError</span></span> |<span data-ttu-id="ce379-129">Category of errors to cover transient issues (eg.</span><span class="sxs-lookup"><span data-stu-id="ce379-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="ce379-130">temporary networking issues with Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="ce379-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="ce379-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="ce379-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ce379-132">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="ce379-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ce379-133">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="ce379-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="ce379-134">Related articles</span><span class="sxs-lookup"><span data-stu-id="ce379-134">Related articles</span></span>
* [<span data-ttu-id="ce379-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span><span class="sxs-lookup"><span data-stu-id="ce379-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="ce379-136">Quotas and Limitations</span><span class="sxs-lookup"><span data-stu-id="ce379-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
