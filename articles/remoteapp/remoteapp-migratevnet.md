---
title: How to migrate from a RemoteApp VNET to an Azure VNET | Microsoft Docs
description: Learn how to migrate from a RemoteApp VNET to an Azure VNET
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548755"
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="6108e-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span><span class="sxs-lookup"><span data-stu-id="6108e-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6108e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="6108e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6108e-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="6108e-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6108e-106">Good news!</span><span class="sxs-lookup"><span data-stu-id="6108e-106">Good news!</span></span> <span data-ttu-id="6108e-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span><span class="sxs-lookup"><span data-stu-id="6108e-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="6108e-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span><span class="sxs-lookup"><span data-stu-id="6108e-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="6108e-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span><span class="sxs-lookup"><span data-stu-id="6108e-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="6108e-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="6108e-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="6108e-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="6108e-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="6108e-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="6108e-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="6108e-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span><span class="sxs-lookup"><span data-stu-id="6108e-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="6108e-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span><span class="sxs-lookup"><span data-stu-id="6108e-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="6108e-115">(Use the **Create with VNET** option, not **Quick Create**.)</span><span class="sxs-lookup"><span data-stu-id="6108e-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="6108e-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="6108e-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="6108e-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="6108e-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="6108e-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span><span class="sxs-lookup"><span data-stu-id="6108e-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="6108e-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span><span class="sxs-lookup"><span data-stu-id="6108e-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="6108e-120">Delete *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="6108e-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="6108e-121">Delete *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="6108e-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="6108e-122">And, you’re done!</span><span class="sxs-lookup"><span data-stu-id="6108e-122">And, you’re done!</span></span>

<span data-ttu-id="6108e-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span><span class="sxs-lookup"><span data-stu-id="6108e-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="6108e-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span><span class="sxs-lookup"><span data-stu-id="6108e-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="6108e-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span><span class="sxs-lookup"><span data-stu-id="6108e-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="6108e-126">Delete *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="6108e-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="6108e-127">Delete *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="6108e-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="6108e-128">And now, you’re done!</span><span class="sxs-lookup"><span data-stu-id="6108e-128">And now, you’re done!</span></span>

<span data-ttu-id="6108e-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="6108e-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

