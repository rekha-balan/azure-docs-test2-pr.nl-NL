---
title: Using App-V apps with Azure RemoteApp| Microsoft Docs
description: Learn how to use App-V apps in Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 0e82c639ea7bfceb89f0cf9c59ab657a951f2d5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555748"
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="f5b89-103">Using App-V apps in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f5b89-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f5b89-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="f5b89-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f5b89-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="f5b89-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f5b89-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span><span class="sxs-lookup"><span data-stu-id="f5b89-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="f5b89-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span><span class="sxs-lookup"><span data-stu-id="f5b89-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="f5b89-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span><span class="sxs-lookup"><span data-stu-id="f5b89-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="f5b89-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f5b89-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="f5b89-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f5b89-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="f5b89-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span><span class="sxs-lookup"><span data-stu-id="f5b89-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="f5b89-112">Configuration options</span><span class="sxs-lookup"><span data-stu-id="f5b89-112">Configuration options</span></span> |  | <span data-ttu-id="f5b89-113">Positive</span><span class="sxs-lookup"><span data-stu-id="f5b89-113">Positive</span></span> | <span data-ttu-id="f5b89-114">Negative</span><span class="sxs-lookup"><span data-stu-id="f5b89-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f5b89-115">Delivery method</span><span class="sxs-lookup"><span data-stu-id="f5b89-115">Delivery method</span></span> |<span data-ttu-id="f5b89-116">Streaming (on-demand)</span><span class="sxs-lookup"><span data-stu-id="f5b89-116">Streaming (on-demand)</span></span> |<span data-ttu-id="f5b89-117">App is always the latest and fresh</span><span class="sxs-lookup"><span data-stu-id="f5b89-117">App is always the latest and fresh</span></span> |<span data-ttu-id="f5b89-118">First time latency</span><span class="sxs-lookup"><span data-stu-id="f5b89-118">First time latency</span></span> |
| <span data-ttu-id="f5b89-119">Mounted</span><span class="sxs-lookup"><span data-stu-id="f5b89-119">Mounted</span></span> |<span data-ttu-id="f5b89-120">Fastest; app is already present on the VM</span><span class="sxs-lookup"><span data-stu-id="f5b89-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="f5b89-121">Bloat - takes up image space (127 GB limit)</span><span class="sxs-lookup"><span data-stu-id="f5b89-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="f5b89-122">App location storage</span><span class="sxs-lookup"><span data-stu-id="f5b89-122">App location storage</span></span> |<span data-ttu-id="f5b89-123">Shared content</span><span class="sxs-lookup"><span data-stu-id="f5b89-123">Shared content</span></span> |<span data-ttu-id="f5b89-124">App runs in memory of Azure RemoteApp instance</span><span class="sxs-lookup"><span data-stu-id="f5b89-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="f5b89-125">Eats memory and good connection to streaming (file) server where the app resides</span><span class="sxs-lookup"><span data-stu-id="f5b89-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="f5b89-126">Disk (Cached)</span><span class="sxs-lookup"><span data-stu-id="f5b89-126">Disk (Cached)</span></span> |<span data-ttu-id="f5b89-127">Fast execution.</span><span class="sxs-lookup"><span data-stu-id="f5b89-127">Fast execution.</span></span> <span data-ttu-id="f5b89-128">App not dependent on availability of Content Source</span><span class="sxs-lookup"><span data-stu-id="f5b89-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="f5b89-129">Bloat - takes up image space (127 GB limit)</span><span class="sxs-lookup"><span data-stu-id="f5b89-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="f5b89-130">Targeting</span><span class="sxs-lookup"><span data-stu-id="f5b89-130">Targeting</span></span> |<span data-ttu-id="f5b89-131">User</span><span class="sxs-lookup"><span data-stu-id="f5b89-131">User</span></span> |<span data-ttu-id="f5b89-132">Requires full standalone App-V infrastructure</span><span class="sxs-lookup"><span data-stu-id="f5b89-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="f5b89-133">Global (machine)</span><span class="sxs-lookup"><span data-stu-id="f5b89-133">Global (machine)</span></span> |<span data-ttu-id="f5b89-134">Pre-publish or target using Publishing server</span><span class="sxs-lookup"><span data-stu-id="f5b89-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="f5b89-135">Need to update your Azure image if you want to update the app (huge).</span><span class="sxs-lookup"><span data-stu-id="f5b89-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="f5b89-136">Takes up some space on image.</span><span class="sxs-lookup"><span data-stu-id="f5b89-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="f5b89-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span><span class="sxs-lookup"><span data-stu-id="f5b89-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

