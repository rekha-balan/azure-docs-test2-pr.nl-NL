---
title: Interactive Map Search with Azure Maps | Microsoft Docs
description: Azure Quickstart - Launch a demo interactive map search using Azure Maps
author: dsk-2015
ms.author: dkshir
ms.date: 05/07/2018
ms.topic: quickstart
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 002d9820cb4414d8f33cdd362e28f31e7e8b6273
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871121"
---
# <a name="launch-an-interactive-search-map-using-azure-maps"></a><span data-ttu-id="eed37-103">Launch an interactive search map using Azure Maps</span><span class="sxs-lookup"><span data-stu-id="eed37-103">Launch an interactive search map using Azure Maps</span></span>

<span data-ttu-id="eed37-104">This article demonstrates the capabilities of Azure Maps to create a map that gives users an interactive search experience.</span><span class="sxs-lookup"><span data-stu-id="eed37-104">This article demonstrates the capabilities of Azure Maps to create a map that gives users an interactive search experience.</span></span> <span data-ttu-id="eed37-105">It walks you through the basic steps of creating your own Maps account and getting your account key to use in the demo web application.</span><span class="sxs-lookup"><span data-stu-id="eed37-105">It walks you through the basic steps of creating your own Maps account and getting your account key to use in the demo web application.</span></span> 

<span data-ttu-id="eed37-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="eed37-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="eed37-107">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="eed37-107">Log in to the Azure portal</span></span>

<span data-ttu-id="eed37-108">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eed37-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-account-and-get-your-key"></a><span data-ttu-id="eed37-109">Create an account and get your key</span><span class="sxs-lookup"><span data-stu-id="eed37-109">Create an account and get your key</span></span>

1. <span data-ttu-id="eed37-110">In the upper left-hand corner of the [Azure portal](https://portal.azure.com), click **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="eed37-110">In the upper left-hand corner of the [Azure portal](https://portal.azure.com), click **Create a resource**.</span></span>
2. <span data-ttu-id="eed37-111">In the *Search the Marketplace* box, type **Maps**.</span><span class="sxs-lookup"><span data-stu-id="eed37-111">In the *Search the Marketplace* box, type **Maps**.</span></span>
3. <span data-ttu-id="eed37-112">From the *Results*, select **Maps**.</span><span class="sxs-lookup"><span data-stu-id="eed37-112">From the *Results*, select **Maps**.</span></span> <span data-ttu-id="eed37-113">Click **Create** button that appears below the map.</span><span class="sxs-lookup"><span data-stu-id="eed37-113">Click **Create** button that appears below the map.</span></span> 
4. <span data-ttu-id="eed37-114">On the **Create Maps Account** page, enter the following values:</span><span class="sxs-lookup"><span data-stu-id="eed37-114">On the **Create Maps Account** page, enter the following values:</span></span>
    - <span data-ttu-id="eed37-115">The *Name* of your new account.</span><span class="sxs-lookup"><span data-stu-id="eed37-115">The *Name* of your new account.</span></span> 
    - <span data-ttu-id="eed37-116">The *Subscription* that you want to use for this account.</span><span class="sxs-lookup"><span data-stu-id="eed37-116">The *Subscription* that you want to use for this account.</span></span>
    - <span data-ttu-id="eed37-117">The *Resource group* for this account.</span><span class="sxs-lookup"><span data-stu-id="eed37-117">The *Resource group* for this account.</span></span> <span data-ttu-id="eed37-118">You may choose to *Create new* or *Use existing* resource group.</span><span class="sxs-lookup"><span data-stu-id="eed37-118">You may choose to *Create new* or *Use existing* resource group.</span></span>
    - <span data-ttu-id="eed37-119">Select the *Resource group location*.</span><span class="sxs-lookup"><span data-stu-id="eed37-119">Select the *Resource group location*.</span></span>
    - <span data-ttu-id="eed37-120">Read the *License* and *Privacy Statement*, and check the checkbox to accept the terms.</span><span class="sxs-lookup"><span data-stu-id="eed37-120">Read the *License* and *Privacy Statement*, and check the checkbox to accept the terms.</span></span> 
    - <span data-ttu-id="eed37-121">Finally, click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="eed37-121">Finally, click the **Create** button.</span></span>

    ![Create Maps account in portal](./media/quick-demo-map-app/create-account.png)

5. <span data-ttu-id="eed37-123">Once your account is successfully created, open it and find the settings section of the account menu.</span><span class="sxs-lookup"><span data-stu-id="eed37-123">Once your account is successfully created, open it and find the settings section of the account menu.</span></span> <span data-ttu-id="eed37-124">Click **Keys** to view the primary and secondary keys for your Azure Maps account.</span><span class="sxs-lookup"><span data-stu-id="eed37-124">Click **Keys** to view the primary and secondary keys for your Azure Maps account.</span></span> <span data-ttu-id="eed37-125">Copy the **Primary Key** value to your local clipboard to use in the following section.</span><span class="sxs-lookup"><span data-stu-id="eed37-125">Copy the **Primary Key** value to your local clipboard to use in the following section.</span></span> 

## <a name="download-the-application"></a><span data-ttu-id="eed37-126">Download the application</span><span class="sxs-lookup"><span data-stu-id="eed37-126">Download the application</span></span>

1. <span data-ttu-id="eed37-127">Download or copy the contents of the file [interactiveSearch.html](https://github.com/Azure-Samples/azure-maps-samples/blob/master/src/interactiveSearch.html).</span><span class="sxs-lookup"><span data-stu-id="eed37-127">Download or copy the contents of the file [interactiveSearch.html](https://github.com/Azure-Samples/azure-maps-samples/blob/master/src/interactiveSearch.html).</span></span>
2. <span data-ttu-id="eed37-128">Save the contents of this file locally as **AzureMapDemo.html** and open it in a text editor.</span><span class="sxs-lookup"><span data-stu-id="eed37-128">Save the contents of this file locally as **AzureMapDemo.html** and open it in a text editor.</span></span>
3. <span data-ttu-id="eed37-129">Search for the string `<insert-key>`, and replace it with the **Primary Key** value obtained in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="eed37-129">Search for the string `<insert-key>`, and replace it with the **Primary Key** value obtained in the preceding section.</span></span> 


## <a name="launch-the-application"></a><span data-ttu-id="eed37-130">Launch the application</span><span class="sxs-lookup"><span data-stu-id="eed37-130">Launch the application</span></span>

1. <span data-ttu-id="eed37-131">Open the file **AzureMapDemo.html** in a browser of your choice.</span><span class="sxs-lookup"><span data-stu-id="eed37-131">Open the file **AzureMapDemo.html** in a browser of your choice.</span></span>
2. <span data-ttu-id="eed37-132">Observe the map shown of Los Angeles city.</span><span class="sxs-lookup"><span data-stu-id="eed37-132">Observe the map shown of Los Angeles city.</span></span> <span data-ttu-id="eed37-133">Zoom in and out to see how the map automatically renders with more or less information depending on the zoom level.</span><span class="sxs-lookup"><span data-stu-id="eed37-133">Zoom in and out to see how the map automatically renders with more or less information depending on the zoom level.</span></span> 
3. <span data-ttu-id="eed37-134">Change the default center of the map.</span><span class="sxs-lookup"><span data-stu-id="eed37-134">Change the default center of the map.</span></span> <span data-ttu-id="eed37-135">In the **AzureMapDemo.html** file, search for the variable named **center**.</span><span class="sxs-lookup"><span data-stu-id="eed37-135">In the **AzureMapDemo.html** file, search for the variable named **center**.</span></span> <span data-ttu-id="eed37-136">Replace the longitute, latitude pair value for this variable with the new values **[-74.0060, 40.7128]**.</span><span class="sxs-lookup"><span data-stu-id="eed37-136">Replace the longitute, latitude pair value for this variable with the new values **[-74.0060, 40.7128]**.</span></span> <span data-ttu-id="eed37-137">Save the file and refresh your browser.</span><span class="sxs-lookup"><span data-stu-id="eed37-137">Save the file and refresh your browser.</span></span> 
3. <span data-ttu-id="eed37-138">Try out the interactive search experience.</span><span class="sxs-lookup"><span data-stu-id="eed37-138">Try out the interactive search experience.</span></span> <span data-ttu-id="eed37-139">In the search box on the upper left corner of the demo web application, search for **restaurants**.</span><span class="sxs-lookup"><span data-stu-id="eed37-139">In the search box on the upper left corner of the demo web application, search for **restaurants**.</span></span> 
4. <span data-ttu-id="eed37-140">Move your mouse over the list of addresses/locations that appear below the search box, and notice how the corresponding pin on the map pops out information about that location.</span><span class="sxs-lookup"><span data-stu-id="eed37-140">Move your mouse over the list of addresses/locations that appear below the search box, and notice how the corresponding pin on the map pops out information about that location.</span></span> <span data-ttu-id="eed37-141">For privacy of private businesses, fictitious names and addresses are shown.</span><span class="sxs-lookup"><span data-stu-id="eed37-141">For privacy of private businesses, fictitious names and addresses are shown.</span></span> 

    ![Interactive Search web application](./media/quick-demo-map-app/interactive-search.png)


## <a name="clean-up-resources"></a><span data-ttu-id="eed37-143">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="eed37-143">Clean up resources</span></span>

<span data-ttu-id="eed37-144">The tutorials go into detail about how to use and configure Maps with your account.</span><span class="sxs-lookup"><span data-stu-id="eed37-144">The tutorials go into detail about how to use and configure Maps with your account.</span></span> <span data-ttu-id="eed37-145">If you plan to continue to the tutorials, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="eed37-145">If you plan to continue to the tutorials, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="eed37-146">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="eed37-146">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart.</span></span>

1. <span data-ttu-id="eed37-147">Close the browser running the **AzureMapDemo.html** web application.</span><span class="sxs-lookup"><span data-stu-id="eed37-147">Close the browser running the **AzureMapDemo.html** web application.</span></span>
2. <span data-ttu-id="eed37-148">From the left-hand menu in the Azure portal, click **All resources** and then select your Maps account.</span><span class="sxs-lookup"><span data-stu-id="eed37-148">From the left-hand menu in the Azure portal, click **All resources** and then select your Maps account.</span></span> <span data-ttu-id="eed37-149">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="eed37-149">At the top of the **All resources** blade, click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eed37-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="eed37-150">Next steps</span></span>

<span data-ttu-id="eed37-151">In this Quickstart, you created your Maps account and launched a demo app.</span><span class="sxs-lookup"><span data-stu-id="eed37-151">In this Quickstart, you created your Maps account and launched a demo app.</span></span> <span data-ttu-id="eed37-152">To learn how to create your own application using the Maps APIs, continue to the following tutorial.</span><span class="sxs-lookup"><span data-stu-id="eed37-152">To learn how to create your own application using the Maps APIs, continue to the following tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eed37-153">Search for points of interest with Maps</span><span class="sxs-lookup"><span data-stu-id="eed37-153">Search for points of interest with Maps</span></span>](./tutorial-search-location.md)

<span data-ttu-id="eed37-154">For more code examples and an interactive coding experience, see below How-to guides.</span><span class="sxs-lookup"><span data-stu-id="eed37-154">For more code examples and an interactive coding experience, see below How-to guides.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eed37-155">How to search for an address using Azure Maps REST APIs</span><span class="sxs-lookup"><span data-stu-id="eed37-155">How to search for an address using Azure Maps REST APIs</span></span>](./how-to-search-for-address.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="eed37-156">How to use Azure Maps map control</span><span class="sxs-lookup"><span data-stu-id="eed37-156">How to use Azure Maps map control</span></span>](./how-to-use-map-control.md)
