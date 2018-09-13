---
title: Update your Azure RemoteApp collection | Microsoft Docs
description: Learn how to update your Azure RemoteApp collection
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
editor: ''
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 41c8a13ebd008ed4f9d8a5399bf8e272bf0fd7b2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564678"
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="004d3-103">Update a collection in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="004d3-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="004d3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="004d3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="004d3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="004d3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="004d3-106">There will come a time, inevitably, when you need to update the apps or image in your Azure RemoteApp collection.</span><span class="sxs-lookup"><span data-stu-id="004d3-106">There will come a time, inevitably, when you need to update the apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="004d3-107">If you are using one of the images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span><span class="sxs-lookup"><span data-stu-id="004d3-107">If you are using one of the images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="004d3-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining the image and apps.</span><span class="sxs-lookup"><span data-stu-id="004d3-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining the image and apps.</span></span> <span data-ttu-id="004d3-109">If you need to update your image or any of the apps inside it, you need to create a new, updated version of the image, and then replace the existing image in your collection with this new updated image.</span><span class="sxs-lookup"><span data-stu-id="004d3-109">If you need to update your image or any of the apps inside it, you need to create a new, updated version of the image, and then replace the existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="004d3-110">So, how do you go about updating your collection?</span><span class="sxs-lookup"><span data-stu-id="004d3-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="004d3-111">It's fairly straightforward:</span><span class="sxs-lookup"><span data-stu-id="004d3-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="004d3-112">Update the image that you used in your collection.</span><span class="sxs-lookup"><span data-stu-id="004d3-112">Update the image that you used in your collection.</span></span> <span data-ttu-id="004d3-113">Apply any patches or updates needed, and then save it with a new name.</span><span class="sxs-lookup"><span data-stu-id="004d3-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="004d3-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image to RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="004d3-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image to RemoteApp.</span></span>
3. <span data-ttu-id="004d3-115">Now, on the collection page, click **Update**.</span><span class="sxs-lookup"><span data-stu-id="004d3-115">Now, on the collection page, click **Update**.</span></span>
4. <span data-ttu-id="004d3-116">Choose the new image from the **Template Image** list.</span><span class="sxs-lookup"><span data-stu-id="004d3-116">Choose the new image from the **Template Image** list.</span></span>
5. <span data-ttu-id="004d3-117">Here's the tricky part - you need to decide how to deal with any users that are currently using an app in the collection.</span><span class="sxs-lookup"><span data-stu-id="004d3-117">Here's the tricky part - you need to decide how to deal with any users that are currently using an app in the collection.</span></span> <span data-ttu-id="004d3-118">You have the following choices:</span><span class="sxs-lookup"><span data-stu-id="004d3-118">You have the following choices:</span></span>
   
   * <span data-ttu-id="004d3-119">**Give users 60 minutes after the update**.</span><span class="sxs-lookup"><span data-stu-id="004d3-119">**Give users 60 minutes after the update**.</span></span> <span data-ttu-id="004d3-120">As soon as the update is finished, Azure RemoteApp will display a message to any active users telling them to save their work and log off and log back in.</span><span class="sxs-lookup"><span data-stu-id="004d3-120">As soon as the update is finished, Azure RemoteApp will display a message to any active users telling them to save their work and log off and log back in.</span></span> <span data-ttu-id="004d3-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span><span class="sxs-lookup"><span data-stu-id="004d3-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="004d3-122">Users can immediately log back on.</span><span class="sxs-lookup"><span data-stu-id="004d3-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="004d3-123">**Sign users out immediately**.</span><span class="sxs-lookup"><span data-stu-id="004d3-123">**Sign users out immediately**.</span></span> <span data-ttu-id="004d3-124">As soon as the update is finished, log off all users automatically without any warning.</span><span class="sxs-lookup"><span data-stu-id="004d3-124">As soon as the update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="004d3-125">If you choose this option, users might lose data.</span><span class="sxs-lookup"><span data-stu-id="004d3-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="004d3-126">However, they can reconnect to the app immediately.</span><span class="sxs-lookup"><span data-stu-id="004d3-126">However, they can reconnect to the app immediately.</span></span>
6. <span data-ttu-id="004d3-127">Click the check mark to start the update.</span><span class="sxs-lookup"><span data-stu-id="004d3-127">Click the check mark to start the update.</span></span>

