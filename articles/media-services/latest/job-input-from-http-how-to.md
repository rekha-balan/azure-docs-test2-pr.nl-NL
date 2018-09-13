---
title: Create an Azure Media Services Job input from an HTTP(s) URL | Microsoft Docs
description: This topic shows how to create a job input from an HTTP(s) URL.
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
ms.openlocfilehash: d429665de64dacc5818d1d26c2a9029531cd39b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857202"
---
# <a name="create-a-job-input-from-an-https-url"></a><span data-ttu-id="0af25-103">Create a job input from an HTTP(s) URL</span><span class="sxs-lookup"><span data-stu-id="0af25-103">Create a job input from an HTTP(s) URL</span></span>

<span data-ttu-id="0af25-104">In Media Services v3, when you submit Jobs to process your videos, you have to tell Media Services where to find the input video.</span><span class="sxs-lookup"><span data-stu-id="0af25-104">In Media Services v3, when you submit Jobs to process your videos, you have to tell Media Services where to find the input video.</span></span> <span data-ttu-id="0af25-105">One of the options is to specify an HTTP(s) URL as a job input (as shown in this example).</span><span class="sxs-lookup"><span data-stu-id="0af25-105">One of the options is to specify an HTTP(s) URL as a job input (as shown in this example).</span></span> <span data-ttu-id="0af25-106">For a full example, see this [github sample](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="0af25-106">For a full example, see this [github sample](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs).</span></span>

## <a name="net-sample"></a><span data-ttu-id="0af25-107">.Net sample</span><span class="sxs-lookup"><span data-stu-id="0af25-107">.Net sample</span></span>

<span data-ttu-id="0af25-108">The following code shows how to create a job with an HTTPS URL input.</span><span class="sxs-lookup"><span data-stu-id="0af25-108">The following code shows how to create a job with an HTTPS URL input.</span></span>

[!code-csharp[Main](../../../media-services-v3-dotnet-quickstarts/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs#SubmitJob)]

## <a name="next-steps"></a><span data-ttu-id="0af25-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="0af25-109">Next steps</span></span>

<span data-ttu-id="0af25-110">[Create a job input from a local file](job-input-from-local-file-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="0af25-110">[Create a job input from a local file](job-input-from-local-file-how-to.md).</span></span>
