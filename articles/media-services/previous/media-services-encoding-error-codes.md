---
title: Azure Media Services encoding error codes | Microsoft Docs
description: This topic lists error codes that could be returned in case an error was encountered during the encoding task execution..
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 7a1733175f796a0d8c0c0d4247b2db2dd47e4674
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856685"
---
# <a name="encoding-error-codes"></a><span data-ttu-id="79c84-103">Encoding error codes</span><span class="sxs-lookup"><span data-stu-id="79c84-103">Encoding error codes</span></span>

<span data-ttu-id="79c84-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span><span class="sxs-lookup"><span data-stu-id="79c84-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="79c84-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="79c84-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="79c84-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span><span class="sxs-lookup"><span data-stu-id="79c84-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="79c84-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="79c84-107">ErrorDetail.Code</span></span> | <span data-ttu-id="79c84-108">Possible causes for error</span><span class="sxs-lookup"><span data-stu-id="79c84-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="79c84-109">Unknown</span><span class="sxs-lookup"><span data-stu-id="79c84-109">Unknown</span></span> |<span data-ttu-id="79c84-110">Unknown error while executing the task</span><span class="sxs-lookup"><span data-stu-id="79c84-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="79c84-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="79c84-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="79c84-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span><span class="sxs-lookup"><span data-stu-id="79c84-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="79c84-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="79c84-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="79c84-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span><span class="sxs-lookup"><span data-stu-id="79c84-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="79c84-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="79c84-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="79c84-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span><span class="sxs-lookup"><span data-stu-id="79c84-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="79c84-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="79c84-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="79c84-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span><span class="sxs-lookup"><span data-stu-id="79c84-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="79c84-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="79c84-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="79c84-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span><span class="sxs-lookup"><span data-stu-id="79c84-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="79c84-121">For example, trying to produce an audio-only output from an asset that has only video</span><span class="sxs-lookup"><span data-stu-id="79c84-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="79c84-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="79c84-122">ErrorProcessingTask</span></span> |<span data-ttu-id="79c84-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span><span class="sxs-lookup"><span data-stu-id="79c84-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="79c84-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="79c84-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="79c84-125">Category of errors when uploading the output asset</span><span class="sxs-lookup"><span data-stu-id="79c84-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="79c84-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="79c84-126">ErrorCancelingTask</span></span> |<span data-ttu-id="79c84-127">Category of errors to cover failures when attempting to cancel the Task</span><span class="sxs-lookup"><span data-stu-id="79c84-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="79c84-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="79c84-128">TransientError</span></span> |<span data-ttu-id="79c84-129">Category of errors to cover transient issues (eg.</span><span class="sxs-lookup"><span data-stu-id="79c84-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="79c84-130">temporary networking issues with Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="79c84-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="79c84-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="79c84-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="79c84-132">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="79c84-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="79c84-133">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="79c84-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="79c84-134">Related articles</span><span class="sxs-lookup"><span data-stu-id="79c84-134">Related articles</span></span>
* [<span data-ttu-id="79c84-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span><span class="sxs-lookup"><span data-stu-id="79c84-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="79c84-136">Quotas and Limitations</span><span class="sxs-lookup"><span data-stu-id="79c84-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
