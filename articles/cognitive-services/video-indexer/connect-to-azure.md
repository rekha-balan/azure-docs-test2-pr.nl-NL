---
title: Create a Video Indexer account connected to Azure | Microsoft Docs
description: This article shows how to create a Video Indexer account connected to Azure.
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 09/05/2018
ms.author: juliako
ms.openlocfilehash: c598fdae40b4552e1d4dc29b8558d82d0830160a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866347"
---
# <a name="create-a-video-indexer-account-connected-to-azure"></a><span data-ttu-id="ee933-103">Create a Video Indexer account connected to Azure</span><span class="sxs-lookup"><span data-stu-id="ee933-103">Create a Video Indexer account connected to Azure</span></span>

<span data-ttu-id="ee933-104">When creating a Video Indexer account, you can choose a free trial account (where you get a certain number of free indexing minutes) or a paid option (where you are not limited by the quota).</span><span class="sxs-lookup"><span data-stu-id="ee933-104">When creating a Video Indexer account, you can choose a free trial account (where you get a certain number of free indexing minutes) or a paid option (where you are not limited by the quota).</span></span> <span data-ttu-id="ee933-105">With free trial, Video Indexer provides up to 600 minutes of free indexing to website users and up to 2400 minutes of free indexing to API users.</span><span class="sxs-lookup"><span data-stu-id="ee933-105">With free trial, Video Indexer provides up to 600 minutes of free indexing to website users and up to 2400 minutes of free indexing to API users.</span></span> <span data-ttu-id="ee933-106">With paid option, you create a Video Indexer account that is connected to your Azure subscription and an Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="ee933-106">With paid option, you create a Video Indexer account that is connected to your Azure subscription and an Azure Media Services account.</span></span> <span data-ttu-id="ee933-107">You pay for minutes indexed as well as the Media Account related charges.</span><span class="sxs-lookup"><span data-stu-id="ee933-107">You pay for minutes indexed as well as the Media Account related charges.</span></span> 

<span data-ttu-id="ee933-108">This article shows how to create a Video Indexer account that's linked to an Azure subscription and an Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="ee933-108">This article shows how to create a Video Indexer account that's linked to an Azure subscription and an Azure Media Services account.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ee933-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ee933-109">Prerequisites</span></span>

* <span data-ttu-id="ee933-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ee933-110">An Azure subscription.</span></span> 

    <span data-ttu-id="ee933-111">If you don't have an Azure subscription yet, sign up for [Azure Free Trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ee933-111">If you don't have an Azure subscription yet, sign up for [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

* <span data-ttu-id="ee933-112">An Azure Active Directory (AD) domain.</span><span class="sxs-lookup"><span data-stu-id="ee933-112">An Azure Active Directory (AD) domain.</span></span> 

    <span data-ttu-id="ee933-113">If you don't have an Azure AD domain, create this domain with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ee933-113">If you don't have an Azure AD domain, create this domain with your Azure subscription.</span></span> <span data-ttu-id="ee933-114">For more information, see [Managing custom domain names in your Azure Active Directory](../../active-directory/users-groups-roles/domains-manage.md)</span><span class="sxs-lookup"><span data-stu-id="ee933-114">For more information, see [Managing custom domain names in your Azure Active Directory](../../active-directory/users-groups-roles/domains-manage.md)</span></span>

* <span data-ttu-id="ee933-115">A user and member in your Azure AD domain.</span><span class="sxs-lookup"><span data-stu-id="ee933-115">A user and member in your Azure AD domain.</span></span> <span data-ttu-id="ee933-116">You'll use this member when connecting your Video Indexer account to Azure.</span><span class="sxs-lookup"><span data-stu-id="ee933-116">You'll use this member when connecting your Video Indexer account to Azure.</span></span>

    <span data-ttu-id="ee933-117">This user should meet these criteria:</span><span class="sxs-lookup"><span data-stu-id="ee933-117">This user should meet these criteria:</span></span>

    * <span data-ttu-id="ee933-118">Be an Azure AD user with a work or school account, not a personal account, such as outlook.com, live.com, or hotmail.com.</span><span class="sxs-lookup"><span data-stu-id="ee933-118">Be an Azure AD user with a work or school account, not a personal account, such as outlook.com, live.com, or hotmail.com.</span></span>
        
        ![all AAD users](./media/create-account/all-aad-users.png)

    *  <span data-ttu-id="ee933-120">Be a member in your Azure subscription with either an Owner role, or both Contributor and User Access Administrator roles.</span><span class="sxs-lookup"><span data-stu-id="ee933-120">Be a member in your Azure subscription with either an Owner role, or both Contributor and User Access Administrator roles.</span></span> <span data-ttu-id="ee933-121">A user can be added twice, with 2 roles.</span><span class="sxs-lookup"><span data-stu-id="ee933-121">A user can be added twice, with 2 roles.</span></span> <span data-ttu-id="ee933-122">Once with Contributor and once with user Access Administrator.</span><span class="sxs-lookup"><span data-stu-id="ee933-122">Once with Contributor and once with user Access Administrator.</span></span>

        ![access control](./media/create-account/access-control-iam.png)

* <span data-ttu-id="ee933-124">Register the EventGrid resource provider using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ee933-124">Register the EventGrid resource provider using the Azure portal.</span></span>

    <span data-ttu-id="ee933-125">In the [Azure portal](https://portal.azure.com/), go to **Subscriptions** > [subscription] > **ResourceProviders** > **Microsoft.EventGrid**.</span><span class="sxs-lookup"><span data-stu-id="ee933-125">In the [Azure portal](https://portal.azure.com/), go to **Subscriptions** > [subscription] > **ResourceProviders** > **Microsoft.EventGrid**.</span></span> <span data-ttu-id="ee933-126">If not in the "Registered" state, click **Register**.</span><span class="sxs-lookup"><span data-stu-id="ee933-126">If not in the "Registered" state, click **Register**.</span></span> <span data-ttu-id="ee933-127">It takes a couple of minutes to register.</span><span class="sxs-lookup"><span data-stu-id="ee933-127">It takes a couple of minutes to register.</span></span> 

    ![EventGrid](./media/create-account/event-grid.png)

## <a name="connect-to-azure"></a><span data-ttu-id="ee933-129">Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="ee933-129">Connect to Azure</span></span>

1. <span data-ttu-id="ee933-130">Sign in to [https://www.videoindexer.ai/](https://www.videoindexer.ai/) and click on the **Connect to Azure** button:</span><span class="sxs-lookup"><span data-stu-id="ee933-130">Sign in to [https://www.videoindexer.ai/](https://www.videoindexer.ai/) and click on the **Connect to Azure** button:</span></span>

    ![connect to Azure](./media/create-account/connect-to-azure.png)

2. <span data-ttu-id="ee933-132">When the subscriptions list appears, select the subscription you want to use.</span><span class="sxs-lookup"><span data-stu-id="ee933-132">When the subscriptions list appears, select the subscription you want to use.</span></span> 

    ![connect Video Indexer to Azure](./media/create-account/connect-vi-to-azure-subscription.png)

3. <span data-ttu-id="ee933-134">Select an Azure region from the supported locations: West US 2, North Europe, or East Asia.</span><span class="sxs-lookup"><span data-stu-id="ee933-134">Select an Azure region from the supported locations: West US 2, North Europe, or East Asia.</span></span>
4. <span data-ttu-id="ee933-135">Under **Azure Media Services account**, choose one of these options:</span><span class="sxs-lookup"><span data-stu-id="ee933-135">Under **Azure Media Services account**, choose one of these options:</span></span>

    * <span data-ttu-id="ee933-136">To create a new Media Services account, select **Create new resource group**.</span><span class="sxs-lookup"><span data-stu-id="ee933-136">To create a new Media Services account, select **Create new resource group**.</span></span> <span data-ttu-id="ee933-137">Provide a name for your resource group.</span><span class="sxs-lookup"><span data-stu-id="ee933-137">Provide a name for your resource group.</span></span>

        <span data-ttu-id="ee933-138">Azure will create your new account in your subscription, including a new Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="ee933-138">Azure will create your new account in your subscription, including a new Azure Storage account.</span></span> <span data-ttu-id="ee933-139">Your new Media Services account has a default initial configuration with a Streaming Endpoint and 10 S3 Reserved Units.</span><span class="sxs-lookup"><span data-stu-id="ee933-139">Your new Media Services account has a default initial configuration with a Streaming Endpoint and 10 S3 Reserved Units.</span></span>
    * <span data-ttu-id="ee933-140">To use an existing Media Services account, select **Use existing resource**.</span><span class="sxs-lookup"><span data-stu-id="ee933-140">To use an existing Media Services account, select **Use existing resource**.</span></span> <span data-ttu-id="ee933-141">From the accounts list, select your account.</span><span class="sxs-lookup"><span data-stu-id="ee933-141">From the accounts list, select your account.</span></span>

        <span data-ttu-id="ee933-142">Your Media Services account must have the same region as your Video Indexer account.</span><span class="sxs-lookup"><span data-stu-id="ee933-142">Your Media Services account must have the same region as your Video Indexer account.</span></span> <span data-ttu-id="ee933-143">To minimize indexing duration and low throughput, adjust the type and number of Reserved Units to **10 S3 Reserved Units** in your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="ee933-143">To minimize indexing duration and low throughput, adjust the type and number of Reserved Units to **10 S3 Reserved Units** in your Media Services account.</span></span>
    * <span data-ttu-id="ee933-144">To manually configure your connection, click the **Switch to manual configuration**.</span><span class="sxs-lookup"><span data-stu-id="ee933-144">To manually configure your connection, click the **Switch to manual configuration**.</span></span> 
    
        <span data-ttu-id="ee933-145">You may want to manually configure your connection, if for some reason the automatic option fails to complete, or if your setup and configuration is different than the common cases, or you want to have full visibility and control over the settings.</span><span class="sxs-lookup"><span data-stu-id="ee933-145">You may want to manually configure your connection, if for some reason the automatic option fails to complete, or if your setup and configuration is different than the common cases, or you want to have full visibility and control over the settings.</span></span> 
        
        <span data-ttu-id="ee933-146">In the **Connect Video Indexer to an Azure subscription**, provide the following information.</span><span class="sxs-lookup"><span data-stu-id="ee933-146">In the **Connect Video Indexer to an Azure subscription**, provide the following information.</span></span>

        |<span data-ttu-id="ee933-147">Setting</span><span class="sxs-lookup"><span data-stu-id="ee933-147">Setting</span></span>|<span data-ttu-id="ee933-148">Description</span><span class="sxs-lookup"><span data-stu-id="ee933-148">Description</span></span>|
        |---|---|
        |<span data-ttu-id="ee933-149">Video Indexer account region</span><span class="sxs-lookup"><span data-stu-id="ee933-149">Video Indexer account region</span></span>|<span data-ttu-id="ee933-150">The name of the Video Indexer account region.</span><span class="sxs-lookup"><span data-stu-id="ee933-150">The name of the Video Indexer account region.</span></span> <span data-ttu-id="ee933-151">For better performance and lower costs, it is highly recommended to specify the name of the region where the Azure Media Services resource and Azure Storage account are located.</span><span class="sxs-lookup"><span data-stu-id="ee933-151">For better performance and lower costs, it is highly recommended to specify the name of the region where the Azure Media Services resource and Azure Storage account are located.</span></span> |
        |<span data-ttu-id="ee933-152">Azure Active Directory (AAD) tenant</span><span class="sxs-lookup"><span data-stu-id="ee933-152">Azure Active Directory (AAD) tenant</span></span>|<span data-ttu-id="ee933-153">The name of the Azure AD tenant, for example "contoso.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="ee933-153">The name of the Azure AD tenant, for example "contoso.onmicrosoft.com".</span></span> <span data-ttu-id="ee933-154">The tenant information can be retrieved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ee933-154">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="ee933-155">Place your cursor over the name of the signed-in user in the top right corner.</span><span class="sxs-lookup"><span data-stu-id="ee933-155">Place your cursor over the name of the signed-in user in the top right corner.</span></span>|
        |<span data-ttu-id="ee933-156">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="ee933-156">Subscription ID</span></span>|<span data-ttu-id="ee933-157">The Azure subscription under which this connection should be created.</span><span class="sxs-lookup"><span data-stu-id="ee933-157">The Azure subscription under which this connection should be created.</span></span> <span data-ttu-id="ee933-158">The subscription ID can be retrieved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ee933-158">The subscription ID can be retrieved from the Azure portal.</span></span> <span data-ttu-id="ee933-159">Click on **All services** in the left panel, and search for "subscriptions".</span><span class="sxs-lookup"><span data-stu-id="ee933-159">Click on **All services** in the left panel, and search for "subscriptions".</span></span> <span data-ttu-id="ee933-160">Select, **Subscriptions** and choose the desired ID from the list of your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="ee933-160">Select, **Subscriptions** and choose the desired ID from the list of your subscriptions.</span></span>|
        |<span data-ttu-id="ee933-161">Azure Media Services resource group name</span><span class="sxs-lookup"><span data-stu-id="ee933-161">Azure Media Services resource group name</span></span>|<span data-ttu-id="ee933-162">The name for the resource group in which to the Media Services account exists.</span><span class="sxs-lookup"><span data-stu-id="ee933-162">The name for the resource group in which to the Media Services account exists.</span></span>|
        |<span data-ttu-id="ee933-163">Media service resource name</span><span class="sxs-lookup"><span data-stu-id="ee933-163">Media service resource name</span></span>|<span data-ttu-id="ee933-164">The name of the Azure Media Services resource.</span><span class="sxs-lookup"><span data-stu-id="ee933-164">The name of the Azure Media Services resource.</span></span>|
        |<span data-ttu-id="ee933-165">Application ID</span><span class="sxs-lookup"><span data-stu-id="ee933-165">Application ID</span></span>|<span data-ttu-id="ee933-166">The Azure AD application ID with permissions for the specified Media Services account.</span><span class="sxs-lookup"><span data-stu-id="ee933-166">The Azure AD application ID with permissions for the specified Media Services account.</span></span> <span data-ttu-id="ee933-167">For more information, see [Use service principal authentication](../../media-services/previous/media-services-portal-get-started-with-aad.md#service-principal-authentication).</span><span class="sxs-lookup"><span data-stu-id="ee933-167">For more information, see [Use service principal authentication](../../media-services/previous/media-services-portal-get-started-with-aad.md#service-principal-authentication).</span></span>|
        |<span data-ttu-id="ee933-168">Application Key</span><span class="sxs-lookup"><span data-stu-id="ee933-168">Application Key</span></span>|<span data-ttu-id="ee933-169">For more information, see [Use service principal authentication](../../media-services/previous/media-services-portal-get-started-with-aad.md#service-principal-authentication).</span><span class="sxs-lookup"><span data-stu-id="ee933-169">For more information, see [Use service principal authentication](../../media-services/previous/media-services-portal-get-started-with-aad.md#service-principal-authentication).</span></span>|

5. <span data-ttu-id="ee933-170">When you're done, choose **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ee933-170">When you're done, choose **Connect**.</span></span> <span data-ttu-id="ee933-171">This operation might take up to a few minutes.</span><span class="sxs-lookup"><span data-stu-id="ee933-171">This operation might take up to a few minutes.</span></span> 

    <span data-ttu-id="ee933-172">After you're connected to Azure, your new Video Indexer account appears in the account list:</span><span class="sxs-lookup"><span data-stu-id="ee933-172">After you're connected to Azure, your new Video Indexer account appears in the account list:</span></span>

    ![new account](./media/create-account/new-account.png)

6. <span data-ttu-id="ee933-174">Browse to your new account:</span><span class="sxs-lookup"><span data-stu-id="ee933-174">Browse to your new account:</span></span> 

    ![Video Indexer account](./media/create-account/vi-account.png)

## <a name="considerations"></a><span data-ttu-id="ee933-176">Considerations</span><span class="sxs-lookup"><span data-stu-id="ee933-176">Considerations</span></span>

<span data-ttu-id="ee933-177">The following Azure Media Services related considerations apply:</span><span class="sxs-lookup"><span data-stu-id="ee933-177">The following Azure Media Services related considerations apply:</span></span>

* <span data-ttu-id="ee933-178">If you connected to a new Media Services account, you will see a new Resource Group, Media Services account, and a Storage account in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ee933-178">If you connected to a new Media Services account, you will see a new Resource Group, Media Services account, and a Storage account in your Azure subscription.</span></span>
* <span data-ttu-id="ee933-179">If you connected to a new Media Services account, Video Indexer will set the media **Reserved Units** to 10 S3 units:</span><span class="sxs-lookup"><span data-stu-id="ee933-179">If you connected to a new Media Services account, Video Indexer will set the media **Reserved Units** to 10 S3 units:</span></span>

    ![Media Services reserved units](./media/create-account/ams-reserved-units.png)

* <span data-ttu-id="ee933-181">If you connected to an existing Media Services account, Video Indexer does not change the existing media **Reserved Units** configuration.</span><span class="sxs-lookup"><span data-stu-id="ee933-181">If you connected to an existing Media Services account, Video Indexer does not change the existing media **Reserved Units** configuration.</span></span>

    <span data-ttu-id="ee933-182">You might need to adjust the type and number of media **Reserved Units**, according to your planned load.</span><span class="sxs-lookup"><span data-stu-id="ee933-182">You might need to adjust the type and number of media **Reserved Units**, according to your planned load.</span></span> <span data-ttu-id="ee933-183">Keep in mind that if your load is high and you don’t have enough units or speed, videos processing can result in timeout failures.</span><span class="sxs-lookup"><span data-stu-id="ee933-183">Keep in mind that if your load is high and you don’t have enough units or speed, videos processing can result in timeout failures.</span></span>

* <span data-ttu-id="ee933-184">If you connected to a new Media Services account, Video Indexer automatically starts the default **Streaming Endpoint** in it:</span><span class="sxs-lookup"><span data-stu-id="ee933-184">If you connected to a new Media Services account, Video Indexer automatically starts the default **Streaming Endpoint** in it:</span></span>

    ![Media Services streaming endpoint](./media/create-account/ams-streaming-endpoint.png)

* <span data-ttu-id="ee933-186">If you connected to an existing Media Services account, Video Indexer does not change the default Streaming Endpoint configuration.</span><span class="sxs-lookup"><span data-stu-id="ee933-186">If you connected to an existing Media Services account, Video Indexer does not change the default Streaming Endpoint configuration.</span></span> <span data-ttu-id="ee933-187">If there is no running **Streaming Endpoint**, you will not be able to watch videos from this Media Services account or in Video Indexer.</span><span class="sxs-lookup"><span data-stu-id="ee933-187">If there is no running **Streaming Endpoint**, you will not be able to watch videos from this Media Services account or in Video Indexer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee933-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee933-188">Next steps</span></span>

<span data-ttu-id="ee933-189">You can programmatically interact with your trial account and/or with your Video Indexer accounts that are connected to azure by following the instructions in: [Use APIs](video-indexer-use-apis.md).</span><span class="sxs-lookup"><span data-stu-id="ee933-189">You can programmatically interact with your trial account and/or with your Video Indexer accounts that are connected to azure by following the instructions in: [Use APIs](video-indexer-use-apis.md).</span></span>

<span data-ttu-id="ee933-190">You should use the same Azure AD user you used when connecting to Azure.</span><span class="sxs-lookup"><span data-stu-id="ee933-190">You should use the same Azure AD user you used when connecting to Azure.</span></span>


