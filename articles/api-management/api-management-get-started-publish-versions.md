---
title: Publish versions of your API using Azure API Management | Microsoft Docs
description: Follow the steps of this tutorial to learn how to publish multiple versions in API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.custom: mvc
ms.topic: tutorial
ms.date: 06/15/2018
ms.author: apimpm
ms.openlocfilehash: a7e5051248a579b0943fa69620215b060bd1e235
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855772"
---
# <a name="publish-multiple-versions-of-your-api"></a><span data-ttu-id="4e49e-103">Publish multiple versions of your API</span><span class="sxs-lookup"><span data-stu-id="4e49e-103">Publish multiple versions of your API</span></span> 

<span data-ttu-id="4e49e-104">There are times when it is impractical to have all callers to your API use exactly the same version.</span><span class="sxs-lookup"><span data-stu-id="4e49e-104">There are times when it is impractical to have all callers to your API use exactly the same version.</span></span> <span data-ttu-id="4e49e-105">When callers want to upgrade to a later version, they want to be able to do this using an easy to understand approach.</span><span class="sxs-lookup"><span data-stu-id="4e49e-105">When callers want to upgrade to a later version, they want to be able to do this using an easy to understand approach.</span></span> <span data-ttu-id="4e49e-106">It is possible to do this using **versions** in Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="4e49e-106">It is possible to do this using **versions** in Azure API Management.</span></span> <span data-ttu-id="4e49e-107">For more information, see [Versions & revisions](https://blogs.msdn.microsoft.com/apimanagement/2017/09/14/versions-revisions/).</span><span class="sxs-lookup"><span data-stu-id="4e49e-107">For more information, see [Versions & revisions](https://blogs.msdn.microsoft.com/apimanagement/2017/09/14/versions-revisions/).</span></span>

<span data-ttu-id="4e49e-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="4e49e-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4e49e-109">Add a new version to an existing API</span><span class="sxs-lookup"><span data-stu-id="4e49e-109">Add a new version to an existing API</span></span>
> * <span data-ttu-id="4e49e-110">Choose a version scheme</span><span class="sxs-lookup"><span data-stu-id="4e49e-110">Choose a version scheme</span></span>
> * <span data-ttu-id="4e49e-111">Add the version to a product</span><span class="sxs-lookup"><span data-stu-id="4e49e-111">Add the version to a product</span></span>
> * <span data-ttu-id="4e49e-112">Browse the developer portal to see the version</span><span class="sxs-lookup"><span data-stu-id="4e49e-112">Browse the developer portal to see the version</span></span>

![Version shown on developer portal](media/api-management-getstarted-publish-versions/azure_portal.PNG)

## <a name="prerequisites"></a><span data-ttu-id="4e49e-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4e49e-114">Prerequisites</span></span>

* <span data-ttu-id="4e49e-115">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="4e49e-115">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>
* <span data-ttu-id="4e49e-116">Also, complete the following tutorial: [Import and publish your first API](import-and-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4e49e-116">Also, complete the following tutorial: [Import and publish your first API](import-and-publish.md).</span></span>

## <a name="add-a-new-version"></a><span data-ttu-id="4e49e-117">Add a new version</span><span class="sxs-lookup"><span data-stu-id="4e49e-117">Add a new version</span></span>

![API Context menu - add version](media/api-management-getstarted-publish-versions/AddVersionMenu.png)

1. <span data-ttu-id="4e49e-119">Select **Demo Conference API** from the API list.</span><span class="sxs-lookup"><span data-stu-id="4e49e-119">Select **Demo Conference API** from the API list.</span></span>
2. <span data-ttu-id="4e49e-120">Select the context menu (**...**) next to it.</span><span class="sxs-lookup"><span data-stu-id="4e49e-120">Select the context menu (**...**) next to it.</span></span>
3. <span data-ttu-id="4e49e-121">Select **+ Add Version**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-121">Select **+ Add Version**.</span></span>

    > [!TIP]
    > <span data-ttu-id="4e49e-122">Versions can also be enabled when you first create a new API - select **Version this API?** on the **Add API** screen.</span><span class="sxs-lookup"><span data-stu-id="4e49e-122">Versions can also be enabled when you first create a new API - select **Version this API?** on the **Add API** screen.</span></span>

## <a name="choose-a-versioning-scheme"></a><span data-ttu-id="4e49e-123">Choose a versioning scheme</span><span class="sxs-lookup"><span data-stu-id="4e49e-123">Choose a versioning scheme</span></span>

<span data-ttu-id="4e49e-124">Azure API Management allows you to choose the way in which you allow callers to specify which version of your API they want.</span><span class="sxs-lookup"><span data-stu-id="4e49e-124">Azure API Management allows you to choose the way in which you allow callers to specify which version of your API they want.</span></span> <span data-ttu-id="4e49e-125">You specify which API version to use by selecting a **versioning scheme**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-125">You specify which API version to use by selecting a **versioning scheme**.</span></span> <span data-ttu-id="4e49e-126">This scheme can be either **path, header or query string**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-126">This scheme can be either **path, header or query string**.</span></span> <span data-ttu-id="4e49e-127">In the following example, path is used to select the versioning scheme.</span><span class="sxs-lookup"><span data-stu-id="4e49e-127">In the following example, path is used to select the versioning scheme.</span></span>

![Add version screen](media/api-management-getstarted-publish-versions/AddVersion.PNG)

1. <span data-ttu-id="4e49e-129">Leave **path** selected as your **versioning scheme**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-129">Leave **path** selected as your **versioning scheme**.</span></span>
2. <span data-ttu-id="4e49e-130">Add **v1** as the **Name** and **Version identifier**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-130">Add **v1** as the **Name** and **Version identifier**.</span></span>

    > [!TIP]
    > <span data-ttu-id="4e49e-131">If you select **header** or **query string** as a versioning scheme, you need to provide an additional value - the name of the header or query string parameter.</span><span class="sxs-lookup"><span data-stu-id="4e49e-131">If you select **header** or **query string** as a versioning scheme, you need to provide an additional value - the name of the header or query string parameter.</span></span>

3. <span data-ttu-id="4e49e-132">Select **Create** to set up your new version.</span><span class="sxs-lookup"><span data-stu-id="4e49e-132">Select **Create** to set up your new version.</span></span>
4. <span data-ttu-id="4e49e-133">Underneath **Demo Conference API** in the API List, you now see two distinct APIs - **Original**, and **v1**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-133">Underneath **Demo Conference API** in the API List, you now see two distinct APIs - **Original**, and **v1**.</span></span>

    ![Versions listed under an API in the Azure portal](media/api-management-getstarted-publish-versions/VersionList.PNG)

    > [!Note]
    > <span data-ttu-id="4e49e-135">If you add a version to a non-versioned API, an **Original** will be automatically created - responding on the default URL.</span><span class="sxs-lookup"><span data-stu-id="4e49e-135">If you add a version to a non-versioned API, an **Original** will be automatically created - responding on the default URL.</span></span> <span data-ttu-id="4e49e-136">This ensures that any existing callers are not broken by the process of adding a version.</span><span class="sxs-lookup"><span data-stu-id="4e49e-136">This ensures that any existing callers are not broken by the process of adding a version.</span></span> <span data-ttu-id="4e49e-137">If you create a new API with versions enabled at the start, an Original is not created.</span><span class="sxs-lookup"><span data-stu-id="4e49e-137">If you create a new API with versions enabled at the start, an Original is not created.</span></span>

5. <span data-ttu-id="4e49e-138">You can now edit and configure **v1** as an API that is separate to **Original**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-138">You can now edit and configure **v1** as an API that is separate to **Original**.</span></span> <span data-ttu-id="4e49e-139">Changes to one version do not affect another.</span><span class="sxs-lookup"><span data-stu-id="4e49e-139">Changes to one version do not affect another.</span></span>

## <a name="add-the-version-to-a-product"></a><span data-ttu-id="4e49e-140">Add the version to a product</span><span class="sxs-lookup"><span data-stu-id="4e49e-140">Add the version to a product</span></span>

<span data-ttu-id="4e49e-141">In order for callers to see the new version, it must be added to a **product**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-141">In order for callers to see the new version, it must be added to a **product**.</span></span>

1. <span data-ttu-id="4e49e-142">Select **Products** from the classic deployment model page.</span><span class="sxs-lookup"><span data-stu-id="4e49e-142">Select **Products** from the classic deployment model page.</span></span>

    ![API Management Products](media/api-management-getstarted-publish-versions/Products.png)

2. <span data-ttu-id="4e49e-144">Select **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-144">Select **Unlimited**.</span></span>
3. <span data-ttu-id="4e49e-145">Select **APIs**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-145">Select **APIs**.</span></span>
4. <span data-ttu-id="4e49e-146">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-146">Select **Add**.</span></span>
5. <span data-ttu-id="4e49e-147">Select **Demo Conference API, Version v1**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-147">Select **Demo Conference API, Version v1**.</span></span>
6. <span data-ttu-id="4e49e-148">Navigate to the service management page and select **APIs**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-148">Navigate to the service management page and select **APIs**.</span></span>

## <a name="browse-the-developer-portal-to-see-the-version"></a><span data-ttu-id="4e49e-149">Browse the developer portal to see the version</span><span class="sxs-lookup"><span data-stu-id="4e49e-149">Browse the developer portal to see the version</span></span>

1. <span data-ttu-id="4e49e-150">Select **Developer Portal** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="4e49e-150">Select **Developer Portal** from the top menu.</span></span>
2. <span data-ttu-id="4e49e-151">Select **APIs**, notice that **Demo Conference API** shows **Original** and **v1** versions.</span><span class="sxs-lookup"><span data-stu-id="4e49e-151">Select **APIs**, notice that **Demo Conference API** shows **Original** and **v1** versions.</span></span>
3. <span data-ttu-id="4e49e-152">Select **v1**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-152">Select **v1**.</span></span>
4. <span data-ttu-id="4e49e-153">Notice the **Request URL** of the first operation in the list.</span><span class="sxs-lookup"><span data-stu-id="4e49e-153">Notice the **Request URL** of the first operation in the list.</span></span> <span data-ttu-id="4e49e-154">It shows that the API URL path includes **v1**.</span><span class="sxs-lookup"><span data-stu-id="4e49e-154">It shows that the API URL path includes **v1**.</span></span>

    ![API Context menu - add version](media/api-management-getstarted-publish-versions/developer_portal.png)

## <a name="next-steps"></a><span data-ttu-id="4e49e-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e49e-156">Next steps</span></span>

<span data-ttu-id="4e49e-157">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="4e49e-157">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4e49e-158">Add a new version to an existing API</span><span class="sxs-lookup"><span data-stu-id="4e49e-158">Add a new version to an existing API</span></span>
> * <span data-ttu-id="4e49e-159">Choose a version scheme</span><span class="sxs-lookup"><span data-stu-id="4e49e-159">Choose a version scheme</span></span> 
> * <span data-ttu-id="4e49e-160">Add the version to a product</span><span class="sxs-lookup"><span data-stu-id="4e49e-160">Add the version to a product</span></span>
> * <span data-ttu-id="4e49e-161">Browse the developer portal to see the version</span><span class="sxs-lookup"><span data-stu-id="4e49e-161">Browse the developer portal to see the version</span></span>

<span data-ttu-id="4e49e-162">Advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="4e49e-162">Advance to the next tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e49e-163">Customize the style of the Developer portal pages</span><span class="sxs-lookup"><span data-stu-id="4e49e-163">Customize the style of the Developer portal pages</span></span>](api-management-customize-styles.md)