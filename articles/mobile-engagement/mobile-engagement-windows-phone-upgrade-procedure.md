---
title: Windows Phone Silverlight SDK Upgrade Procedures
description: Windows Phone Silverlight SDK Upgrade Procedures for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552591"
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="a270a-103">Windows Phone Silverlight SDK Upgrade Procedures</span><span class="sxs-lookup"><span data-stu-id="a270a-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="a270a-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span><span class="sxs-lookup"><span data-stu-id="a270a-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="a270a-105">You may have to follow several procedures if you missed several versions of the SDK.</span><span class="sxs-lookup"><span data-stu-id="a270a-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="a270a-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span><span class="sxs-lookup"><span data-stu-id="a270a-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="a270a-107">From 2.0.0 to 3.3.0</span><span class="sxs-lookup"><span data-stu-id="a270a-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="a270a-108">Test logs</span><span class="sxs-lookup"><span data-stu-id="a270a-108">Test logs</span></span>
<span data-ttu-id="a270a-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span><span class="sxs-lookup"><span data-stu-id="a270a-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="a270a-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span><span class="sxs-lookup"><span data-stu-id="a270a-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="a270a-111">From 1.1.1 to 2.0.0</span><span class="sxs-lookup"><span data-stu-id="a270a-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="a270a-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a270a-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a270a-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span><span class="sxs-lookup"><span data-stu-id="a270a-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="a270a-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span><span class="sxs-lookup"><span data-stu-id="a270a-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="a270a-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span><span class="sxs-lookup"><span data-stu-id="a270a-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="a270a-116">Nuget package</span><span class="sxs-lookup"><span data-stu-id="a270a-116">Nuget package</span></span>
<span data-ttu-id="a270a-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span><span class="sxs-lookup"><span data-stu-id="a270a-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="a270a-118">Applying Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a270a-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="a270a-119">The SDK uses the term `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="a270a-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="a270a-120">You need to update your project to match this change.</span><span class="sxs-lookup"><span data-stu-id="a270a-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="a270a-121">You need to uninstall your current Capptain nuget package.</span><span class="sxs-lookup"><span data-stu-id="a270a-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="a270a-122">Consider that all your changes in Capptain Resources folder will be removed.</span><span class="sxs-lookup"><span data-stu-id="a270a-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="a270a-123">If you want to keep those files then make a copy of them.</span><span class="sxs-lookup"><span data-stu-id="a270a-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="a270a-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span><span class="sxs-lookup"><span data-stu-id="a270a-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="a270a-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="a270a-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="a270a-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span><span class="sxs-lookup"><span data-stu-id="a270a-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="a270a-127">You have to clean your project references by deleting Capptain DLL references.</span><span class="sxs-lookup"><span data-stu-id="a270a-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="a270a-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span><span class="sxs-lookup"><span data-stu-id="a270a-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="a270a-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span><span class="sxs-lookup"><span data-stu-id="a270a-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="a270a-130">Please note that both xaml and cs files have to be updated.</span><span class="sxs-lookup"><span data-stu-id="a270a-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="a270a-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span><span class="sxs-lookup"><span data-stu-id="a270a-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="a270a-132">All Capptain namespaces have to be updated.</span><span class="sxs-lookup"><span data-stu-id="a270a-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="a270a-133">Before migration:</span><span class="sxs-lookup"><span data-stu-id="a270a-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="a270a-134">After migration:</span><span class="sxs-lookup"><span data-stu-id="a270a-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="a270a-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span><span class="sxs-lookup"><span data-stu-id="a270a-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="a270a-136">Before migration:</span><span class="sxs-lookup"><span data-stu-id="a270a-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="a270a-137">After migration:</span><span class="sxs-lookup"><span data-stu-id="a270a-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="a270a-138">For xaml files Capptain namespace and attributes also change.</span><span class="sxs-lookup"><span data-stu-id="a270a-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="a270a-139">Before migration:</span><span class="sxs-lookup"><span data-stu-id="a270a-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="a270a-140">After migration:</span><span class="sxs-lookup"><span data-stu-id="a270a-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="a270a-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span><span class="sxs-lookup"><span data-stu-id="a270a-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="a270a-142">Application ID / SDK Key</span><span class="sxs-lookup"><span data-stu-id="a270a-142">Application ID / SDK Key</span></span>
<span data-ttu-id="a270a-143">Engagement uses a connection string.</span><span class="sxs-lookup"><span data-stu-id="a270a-143">Engagement uses a connection string.</span></span> <span data-ttu-id="a270a-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span><span class="sxs-lookup"><span data-stu-id="a270a-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="a270a-145">You can set it up on your EngagementConfiguration file.</span><span class="sxs-lookup"><span data-stu-id="a270a-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="a270a-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span><span class="sxs-lookup"><span data-stu-id="a270a-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="a270a-147">Edit this file to specify:</span><span class="sxs-lookup"><span data-stu-id="a270a-147">Edit this file to specify:</span></span>

* <span data-ttu-id="a270a-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="a270a-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="a270a-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span><span class="sxs-lookup"><span data-stu-id="a270a-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="a270a-150">The connection string for your application is displayed in the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="a270a-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="a270a-151">Items name change</span><span class="sxs-lookup"><span data-stu-id="a270a-151">Items name change</span></span>
<span data-ttu-id="a270a-152">All items named *capptain* have been named *engagement*.</span><span class="sxs-lookup"><span data-stu-id="a270a-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="a270a-153">Similarly for *Capptain* to *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="a270a-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="a270a-154">Examples of commonly used Capptain items :</span><span class="sxs-lookup"><span data-stu-id="a270a-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="a270a-155">CapptainConfiguration now named EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="a270a-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="a270a-156">CapptainAgent now named EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="a270a-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="a270a-157">CapptainReach now named EngagementReach</span><span class="sxs-lookup"><span data-stu-id="a270a-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="a270a-158">CapptainHttpConfig now named EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="a270a-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="a270a-159">GetCapptainPageName now named GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="a270a-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="a270a-160">Note that rename also affects overridden methods.</span><span class="sxs-lookup"><span data-stu-id="a270a-160">Note that rename also affects overridden methods.</span></span>

