---
title: How to check job progress using REST API | Microsoft Docs
description: Learn how to track job progress.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: a1a1f956-c035-448a-af9c-5ac15fcce9dd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2017
ms.author: juliako
ms.openlocfilehash: 0065b12c9ee01bddef664e5c78a4e40af759826a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865662"
---
# <a name="how-to-check-job-progress"></a><span data-ttu-id="c8483-103">How to: check job progress</span><span class="sxs-lookup"><span data-stu-id="c8483-103">How to: check job progress</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-check-job-progress.md)
> * [.NET](media-services-check-job-progress.md)
> * [REST](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="c8483-107">When you run jobs, you often require a way to track job progress.</span><span class="sxs-lookup"><span data-stu-id="c8483-107">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="c8483-108">You can find out the Job status by using the Job's State property.</span><span class="sxs-lookup"><span data-stu-id="c8483-108">You can find out the Job status by using the Job's State property.</span></span> <span data-ttu-id="c8483-109">For more information on the State property, see [Job Entity Properties](https://docs.microsoft.com/rest/api/media/operations/job#job_entity_properties).</span><span class="sxs-lookup"><span data-stu-id="c8483-109">For more information on the State property, see [Job Entity Properties](https://docs.microsoft.com/rest/api/media/operations/job#job_entity_properties).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="c8483-110">Connect to Media Services</span><span class="sxs-lookup"><span data-stu-id="c8483-110">Connect to Media Services</span></span>

<span data-ttu-id="c8483-111">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="c8483-111">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 


## <a name="check-job-progress"></a><span data-ttu-id="c8483-112">Check job progress</span><span class="sxs-lookup"><span data-stu-id="c8483-112">Check job progress</span></span>

<span data-ttu-id="c8483-113">Request:</span><span class="sxs-lookup"><span data-stu-id="c8483-113">Request:</span></span>

    GET https://media.windows.net/api/Jobs()?$filter=Id%20eq%20'nb%3Ajid%3AUUID%3Af3c43f94-327f-2347-90bb-3bf79f8559f1'&$top=1 HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    Host: media.windows.net



<span data-ttu-id="c8483-114">Response:</span><span class="sxs-lookup"><span data-stu-id="c8483-114">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 450
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d9b83c57-e26c-4d10-a20b-2be634c4b6a8
    request-id: 91d2be35-20ed-4e1c-a147-e82cd000c193
    x-ms-request-id: 91d2be35-20ed-4e1c-a147-e82cd000c193
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains

    {"odata.metadata":"https://media.windows.net/api/$metadata#Jobs","value":[{"Id":"nb:jid:UUID:f3c43f94-327f-2347-90bb-3bf79f8559f1","Name":"Encoding BigBuckBunny into to H264 Adaptive Bitrate MP4 Set 720p","Created":"2015-02-11T01:46:08.897","LastModified":"2015-02-11T01:46:08.897","EndTime":null,"Priority":0,"RunningDuration":0.0,"StartTime":"2015-02-11T01:46:16.58","State":2,"TemplateId":null,"JobNotificationSubscriptions":[]}]} 


## <a name="media-services-learning-paths"></a><span data-ttu-id="c8483-115">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="c8483-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8483-116">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c8483-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c8483-117">See also</span><span class="sxs-lookup"><span data-stu-id="c8483-117">See also</span></span>

[<span data-ttu-id="c8483-118">Media Services operations REST API overview</span><span class="sxs-lookup"><span data-stu-id="c8483-118">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)
