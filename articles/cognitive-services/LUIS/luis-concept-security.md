---
title: Understand access to LUIS applications - Azure | Microsoft Docs
description: Learn how to access LUIS authoring.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 05/07/2018
ms.author: diberry
ms.openlocfilehash: fddffbcabba753e9ef214f924d5ff2cee38427a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867117"
---
# <a name="authoring-and-endpoint-user-access"></a><span data-ttu-id="82279-103">Authoring and endpoint user access</span><span class="sxs-lookup"><span data-stu-id="82279-103">Authoring and endpoint user access</span></span>
<span data-ttu-id="82279-104">Authoring access is available for owners and collaborators.</span><span class="sxs-lookup"><span data-stu-id="82279-104">Authoring access is available for owners and collaborators.</span></span> <span data-ttu-id="82279-105">For a private app, endpoint access is available for owners and collaborators.</span><span class="sxs-lookup"><span data-stu-id="82279-105">For a private app, endpoint access is available for owners and collaborators.</span></span> <span data-ttu-id="82279-106">For a public app, endpoint access is available to everyone that has their own LUIS account and has the public app's ID.</span><span class="sxs-lookup"><span data-stu-id="82279-106">For a public app, endpoint access is available to everyone that has their own LUIS account and has the public app's ID.</span></span> 

## <a name="access-to-authoring"></a><span data-ttu-id="82279-107">Access to authoring</span><span class="sxs-lookup"><span data-stu-id="82279-107">Access to authoring</span></span>
<span data-ttu-id="82279-108">Access to the app from the [LUIS](luis-reference-regions.md#luis-website) website or the [authoring APIs](https://aka.ms/luis-authoring-apis) is controlled by the owner of the app.</span><span class="sxs-lookup"><span data-stu-id="82279-108">Access to the app from the [LUIS](luis-reference-regions.md#luis-website) website or the [authoring APIs](https://aka.ms/luis-authoring-apis) is controlled by the owner of the app.</span></span> 

<span data-ttu-id="82279-109">The owner and all collaborators have access to author the app.</span><span class="sxs-lookup"><span data-stu-id="82279-109">The owner and all collaborators have access to author the app.</span></span> 

|<span data-ttu-id="82279-110">Authoring access includes</span><span class="sxs-lookup"><span data-stu-id="82279-110">Authoring access includes</span></span>|<span data-ttu-id="82279-111">Notes</span><span class="sxs-lookup"><span data-stu-id="82279-111">Notes</span></span>|
|--|--|
|<span data-ttu-id="82279-112">Add or remove endpoint keys</span><span class="sxs-lookup"><span data-stu-id="82279-112">Add or remove endpoint keys</span></span>||
|<span data-ttu-id="82279-113">Exporting version</span><span class="sxs-lookup"><span data-stu-id="82279-113">Exporting version</span></span>||
|<span data-ttu-id="82279-114">Export endpoint logs</span><span class="sxs-lookup"><span data-stu-id="82279-114">Export endpoint logs</span></span>||
|<span data-ttu-id="82279-115">Importing version</span><span class="sxs-lookup"><span data-stu-id="82279-115">Importing version</span></span>||
|<span data-ttu-id="82279-116">Make app public</span><span class="sxs-lookup"><span data-stu-id="82279-116">Make app public</span></span>|<span data-ttu-id="82279-117">When an app is public, anyone with an authoring or endpoint key can query the app.</span><span class="sxs-lookup"><span data-stu-id="82279-117">When an app is public, anyone with an authoring or endpoint key can query the app.</span></span>|
|<span data-ttu-id="82279-118">Modify model</span><span class="sxs-lookup"><span data-stu-id="82279-118">Modify model</span></span>|
|<span data-ttu-id="82279-119">Publish</span><span class="sxs-lookup"><span data-stu-id="82279-119">Publish</span></span>|
|<span data-ttu-id="82279-120">Review endpoint utterances for [active learning](luis-how-to-review-endoint-utt.md)</span><span class="sxs-lookup"><span data-stu-id="82279-120">Review endpoint utterances for [active learning](luis-how-to-review-endoint-utt.md)</span></span>|
|<span data-ttu-id="82279-121">Train</span><span class="sxs-lookup"><span data-stu-id="82279-121">Train</span></span>|

## <a name="access-to-endpoint"></a><span data-ttu-id="82279-122">Access to endpoint</span><span class="sxs-lookup"><span data-stu-id="82279-122">Access to endpoint</span></span>
<span data-ttu-id="82279-123">Access to the endpoint to query LUIS is controlled by the **Public** setting of the app on the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="82279-123">Access to the endpoint to query LUIS is controlled by the **Public** setting of the app on the **Settings** page.</span></span> <span data-ttu-id="82279-124">A private app's endpoint query is checked for an authorized key with remaining quota hits.</span><span class="sxs-lookup"><span data-stu-id="82279-124">A private app's endpoint query is checked for an authorized key with remaining quota hits.</span></span> <span data-ttu-id="82279-125">A public app's endpoint query has to also provide an endpoint key (from whoever is making the query) which is also checked for remaining quota hits.</span><span class="sxs-lookup"><span data-stu-id="82279-125">A public app's endpoint query has to also provide an endpoint key (from whoever is making the query) which is also checked for remaining quota hits.</span></span> 

<span data-ttu-id="82279-126">The endpoint key is passed either in the querystring of the GET request or the header of the POST request.</span><span class="sxs-lookup"><span data-stu-id="82279-126">The endpoint key is passed either in the querystring of the GET request or the header of the POST request.</span></span>

![Set app to public](./media/luis-concept-security/set-application-as-public.png)

### <a name="private-app-endpoint-security"></a><span data-ttu-id="82279-128">Private app endpoint security</span><span class="sxs-lookup"><span data-stu-id="82279-128">Private app endpoint security</span></span>
<span data-ttu-id="82279-129">A private app's endpoint is only available to the following:</span><span class="sxs-lookup"><span data-stu-id="82279-129">A private app's endpoint is only available to the following:</span></span>

|<span data-ttu-id="82279-130">Key and user</span><span class="sxs-lookup"><span data-stu-id="82279-130">Key and user</span></span>|<span data-ttu-id="82279-131">Explanation</span><span class="sxs-lookup"><span data-stu-id="82279-131">Explanation</span></span>|
|--|--|--|
|<span data-ttu-id="82279-132">Owner's authoring key</span><span class="sxs-lookup"><span data-stu-id="82279-132">Owner's authoring key</span></span>| <span data-ttu-id="82279-133">Up to 1000 endpoint hits</span><span class="sxs-lookup"><span data-stu-id="82279-133">Up to 1000 endpoint hits</span></span>|
|<span data-ttu-id="82279-134">Collaborators' authoring keys</span><span class="sxs-lookup"><span data-stu-id="82279-134">Collaborators' authoring keys</span></span>| <span data-ttu-id="82279-135">Up to 1000 endpoint hits</span><span class="sxs-lookup"><span data-stu-id="82279-135">Up to 1000 endpoint hits</span></span>|
|<span data-ttu-id="82279-136">Endpoint keys added from **[Publish](luis-how-to-publish-app.md)** page</span><span class="sxs-lookup"><span data-stu-id="82279-136">Endpoint keys added from **[Publish](luis-how-to-publish-app.md)** page</span></span>|<span data-ttu-id="82279-137">Owner and collaborators can add endpoint keys</span><span class="sxs-lookup"><span data-stu-id="82279-137">Owner and collaborators can add endpoint keys</span></span>|

<span data-ttu-id="82279-138">Other authoring or endpoint keys have **no** access.</span><span class="sxs-lookup"><span data-stu-id="82279-138">Other authoring or endpoint keys have **no** access.</span></span>

### <a name="public-app-endpoint-access"></a><span data-ttu-id="82279-139">Public app endpoint access</span><span class="sxs-lookup"><span data-stu-id="82279-139">Public app endpoint access</span></span>
<span data-ttu-id="82279-140">Configure the app as **public** on the **Settings** page of the app.</span><span class="sxs-lookup"><span data-stu-id="82279-140">Configure the app as **public** on the **Settings** page of the app.</span></span> <span data-ttu-id="82279-141">Once an app is configured as public, _any_ valid LUIS authoring key or LUIS endpoint key can query your app, as long as the key has not used the entire endpoint quota.</span><span class="sxs-lookup"><span data-stu-id="82279-141">Once an app is configured as public, _any_ valid LUIS authoring key or LUIS endpoint key can query your app, as long as the key has not used the entire endpoint quota.</span></span>

<span data-ttu-id="82279-142">A user who is not an owner or collaborator, can only access a public app if given the app ID.</span><span class="sxs-lookup"><span data-stu-id="82279-142">A user who is not an owner or collaborator, can only access a public app if given the app ID.</span></span> <span data-ttu-id="82279-143">LUIS doesn't have a public _market_ or other way to search for a public app.</span><span class="sxs-lookup"><span data-stu-id="82279-143">LUIS doesn't have a public _market_ or other way to search for a public app.</span></span>  

## <a name="microsoft-user-accounts"></a><span data-ttu-id="82279-144">Microsoft user accounts</span><span class="sxs-lookup"><span data-stu-id="82279-144">Microsoft user accounts</span></span>
<span data-ttu-id="82279-145">Authors and collaborators can add keys to LUIS on the Publish page.</span><span class="sxs-lookup"><span data-stu-id="82279-145">Authors and collaborators can add keys to LUIS on the Publish page.</span></span> <span data-ttu-id="82279-146">The Microsoft user account that creates the LUIS key in the Azure portal needs to be either the app owner or an app collaborator.</span><span class="sxs-lookup"><span data-stu-id="82279-146">The Microsoft user account that creates the LUIS key in the Azure portal needs to be either the app owner or an app collaborator.</span></span> 

<span data-ttu-id="82279-147">See [Azure Active Directory tenant user](luis-how-to-collaborate.md#azure-active-directory-tenant-user) to learn more about Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="82279-147">See [Azure Active Directory tenant user](luis-how-to-collaborate.md#azure-active-directory-tenant-user) to learn more about Active Directory user accounts.</span></span> 

<!--
### Individual consent
If the Microsoft user account is part of an Azure Active Directory (AAD), and the active directory doesn't allow users to give consent, then you can provide individual consent as part of the login process. 

### Administrator consent
If the Microsoft user account is part of an Azure Active Directory (AAD), and the active directory doesn't allow users to give consent, then the administrator can give individual consent via the method discussed in this [blog](https://blogs.technet.microsoft.com/tfg/2017/10/15/english-tips-to-manage-azure-ad-users-consent-to-applications-using-azure-ad-graph-api/). 
-->
## <a name="securing-the-endpoint"></a><span data-ttu-id="82279-148">Securing the endpoint</span><span class="sxs-lookup"><span data-stu-id="82279-148">Securing the endpoint</span></span> 
<span data-ttu-id="82279-149">You can control who can see your LUIS endpoint key by calling it in a server-to-server environment.</span><span class="sxs-lookup"><span data-stu-id="82279-149">You can control who can see your LUIS endpoint key by calling it in a server-to-server environment.</span></span> <span data-ttu-id="82279-150">If you are using LUIS from a bot, the connection between the bot and LUIS is already secure.</span><span class="sxs-lookup"><span data-stu-id="82279-150">If you are using LUIS from a bot, the connection between the bot and LUIS is already secure.</span></span> <span data-ttu-id="82279-151">If you are calling the LUIS endpoint directly, you should create a server-side API (such as an Azure [function](https://azure.microsoft.com/services/functions/)) with controlled access (such as [AAD](https://azure.microsoft.com/services/active-directory/)).</span><span class="sxs-lookup"><span data-stu-id="82279-151">If you are calling the LUIS endpoint directly, you should create a server-side API (such as an Azure [function](https://azure.microsoft.com/services/functions/)) with controlled access (such as [AAD](https://azure.microsoft.com/services/active-directory/)).</span></span> <span data-ttu-id="82279-152">When the server-side API is called and authentication and authorization are verified, pass the call on to LUIS.</span><span class="sxs-lookup"><span data-stu-id="82279-152">When the server-side API is called and authentication and authorization are verified, pass the call on to LUIS.</span></span> <span data-ttu-id="82279-153">While this strategy doesn’t prevent man-in-the-middle attacks, it obfuscates your endpoint from your users, allows you to track access, and allows you to add endpoint response logging (such as [Application Insights](https://azure.microsoft.com/services/application-insights/)).</span><span class="sxs-lookup"><span data-stu-id="82279-153">While this strategy doesn’t prevent man-in-the-middle attacks, it obfuscates your endpoint from your users, allows you to track access, and allows you to add endpoint response logging (such as [Application Insights](https://azure.microsoft.com/services/application-insights/)).</span></span>  

## <a name="security-compliance"></a><span data-ttu-id="82279-154">Security Compliance</span><span class="sxs-lookup"><span data-stu-id="82279-154">Security Compliance</span></span>
<span data-ttu-id="82279-155">LUIS successfully completed the ISO 27001:2013 and ISO 27018:2014 audit with ZERO non-conformities (findings) in the audit report.</span><span class="sxs-lookup"><span data-stu-id="82279-155">LUIS successfully completed the ISO 27001:2013 and ISO 27018:2014 audit with ZERO non-conformities (findings) in the audit report.</span></span> <span data-ttu-id="82279-156">Additionally, LUIS also obtained the CSA STAR Certification with the highest possible Gold Award for the maturity capability assessment.</span><span class="sxs-lookup"><span data-stu-id="82279-156">Additionally, LUIS also obtained the CSA STAR Certification with the highest possible Gold Award for the maturity capability assessment.</span></span> <span data-ttu-id="82279-157">Azure is the only major public cloud service provider to earn this certification.</span><span class="sxs-lookup"><span data-stu-id="82279-157">Azure is the only major public cloud service provider to earn this certification.</span></span> <span data-ttu-id="82279-158">For more details, you can find the LUIS included in the updated scope statement in Azure’s main [compliance overview](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942) document that is referenced on [Trust Center](https://www.microsoft.com/en-us/trustcenter/compliance/iso-iec-27001) ISO pages.</span><span class="sxs-lookup"><span data-stu-id="82279-158">For more details, you can find the LUIS included in the updated scope statement in Azure’s main [compliance overview](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942) document that is referenced on [Trust Center](https://www.microsoft.com/en-us/trustcenter/compliance/iso-iec-27001) ISO pages.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="82279-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="82279-159">Next steps</span></span>

<span data-ttu-id="82279-160">See [Best Practices](luis-concept-best-practices.md) to learn how to use intents and entities for the best predictions.</span><span class="sxs-lookup"><span data-stu-id="82279-160">See [Best Practices](luis-concept-best-practices.md) to learn how to use intents and entities for the best predictions.</span></span>
