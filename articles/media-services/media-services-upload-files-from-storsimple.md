---
title: Upload files into an Azure Media Services account from Azure StorSimple | Microsoft Docs
description: This article gives a brief overview of Azure StorSimple Data Manager. The article also links to tutorials that show you how to extract data from StorSimple and upload it as assets to an Azure Media Services account.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 866bc2c05acafa5ce6bf535bfce2de577cf98c0b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548793"
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="cb4a7-104">Upload files into an Azure Media Services account from Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="cb4a7-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="cb4a7-105">This article gives a brief overview of Azure StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="cb4a7-106">The article also links to tutorials that show you how to extract data from StorSimple and upload this data as assets to an Azure Media Services (AMS) account.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-106">The article also links to tutorials that show you how to extract data from StorSimple and upload this data as assets to an Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="cb4a7-107">Azure StorSimple Data Manager is currently in private preview.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="cb4a7-108">Overview</span><span class="sxs-lookup"><span data-stu-id="cb4a7-108">Overview</span></span>

<span data-ttu-id="cb4a7-109">In Media Services, you upload your digital files into an asset.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="cb4a7-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="cb4a7-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="cb4a7-112">The StorSimple device dedupes and compresses your data before sending it to the cloud making it very efficient for sending large files to the cloud.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-112">The StorSimple device dedupes and compresses your data before sending it to the cloud making it very efficient for sending large files to the cloud.</span></span> <span data-ttu-id="cb4a7-113">The [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you to extract data from StorSimple and present it as AMS assets.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-113">The [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you to extract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="cb4a7-114">Get started</span><span class="sxs-lookup"><span data-stu-id="cb4a7-114">Get started</span></span>

1. <span data-ttu-id="cb4a7-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want to transfer the assets.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want to transfer the assets.</span></span>
2. <span data-ttu-id="cb4a7-116">Sign up for Data Manager preview, as described in the [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-116">Sign up for Data Manager preview, as described in the [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="cb4a7-117">Create a StorSimple Data Manager account.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="cb4a7-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="cb4a7-119">When the job starts running, a storage queue is created.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-119">When the job starts running, a storage queue is created.</span></span> <span data-ttu-id="cb4a7-120">This queue is populated with messages about transformed blobs as they are ready.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="cb4a7-121">The name of this queue is the same as the name of the job definition.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-121">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="cb4a7-122">You can use this queue to determine when as asset is ready and call your desired Media Services operation to run on it.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-122">You can use this queue to determine when as asset is ready and call your desired Media Services operation to run on it.</span></span> <span data-ttu-id="cb4a7-123">For example, you can use this queue to trigger an Azure Function that has the necessary Media Services code in it.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-123">For example, you can use this queue to trigger an Azure Function that has the necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="cb4a7-124">See also</span><span class="sxs-lookup"><span data-stu-id="cb4a7-124">See also</span></span>

[<span data-ttu-id="cb4a7-125">Use the .Net SDK to trigger jobs in the Data Manager</span><span class="sxs-lookup"><span data-stu-id="cb4a7-125">Use the .Net SDK to trigger jobs in the Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="cb4a7-126">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="cb4a7-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cb4a7-127">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="cb4a7-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cb4a7-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb4a7-128">Next steps</span></span>

<span data-ttu-id="cb4a7-129">You can now encode your uploaded assets.</span><span class="sxs-lookup"><span data-stu-id="cb4a7-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="cb4a7-130">For more information, see [Encode assets](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="cb4a7-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
