---
title: Use revisions to make non-breaking changes safely in Azure API Management | Microsoft Docs
description: Follow the steps of this tutorial to learn how to make non-breaking changes using revisions in API Management.
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
ms.openlocfilehash: c1c884e05d357db7e23574dbd31f206d6c3fe23c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871569"
---
# <a name="use-revisions-to-make-non-breaking-changes-safely"></a><span data-ttu-id="ff476-103">Use revisions to make non-breaking changes safely</span><span class="sxs-lookup"><span data-stu-id="ff476-103">Use revisions to make non-breaking changes safely</span></span>
<span data-ttu-id="ff476-104">When your API is ready to go and starts to be used by developers, you eventually need to make changes to that API and at the same time not disrupt callers of your API.</span><span class="sxs-lookup"><span data-stu-id="ff476-104">When your API is ready to go and starts to be used by developers, you eventually need to make changes to that API and at the same time not disrupt callers of your API.</span></span> <span data-ttu-id="ff476-105">It's also useful to let developers know about the changes you made.</span><span class="sxs-lookup"><span data-stu-id="ff476-105">It's also useful to let developers know about the changes you made.</span></span> <span data-ttu-id="ff476-106">We can do this in Azure API Management using **revisions**.</span><span class="sxs-lookup"><span data-stu-id="ff476-106">We can do this in Azure API Management using **revisions**.</span></span> <span data-ttu-id="ff476-107">For more information, see [Versions & revisions](https://blogs.msdn.microsoft.com/apimanagement/2017/09/14/versions-revisions/) and [API Versioning with Azure API Management](https://blogs.msdn.microsoft.com/apimanagement/2017/09/13/api-versioning-with-azure-api-management/).</span><span class="sxs-lookup"><span data-stu-id="ff476-107">For more information, see [Versions & revisions](https://blogs.msdn.microsoft.com/apimanagement/2017/09/14/versions-revisions/) and [API Versioning with Azure API Management](https://blogs.msdn.microsoft.com/apimanagement/2017/09/13/api-versioning-with-azure-api-management/).</span></span>

<span data-ttu-id="ff476-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="ff476-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ff476-109">Add a new revision</span><span class="sxs-lookup"><span data-stu-id="ff476-109">Add a new revision</span></span>
> * <span data-ttu-id="ff476-110">Make non-breaking changes to your revision</span><span class="sxs-lookup"><span data-stu-id="ff476-110">Make non-breaking changes to your revision</span></span>
> * <span data-ttu-id="ff476-111">Make your revision current and add a change log entry</span><span class="sxs-lookup"><span data-stu-id="ff476-111">Make your revision current and add a change log entry</span></span>
> * <span data-ttu-id="ff476-112">Browse the developer portal to see changes and change log</span><span class="sxs-lookup"><span data-stu-id="ff476-112">Browse the developer portal to see changes and change log</span></span>

![Change Log on the Developer Portal](media/api-management-getstarted-revise-api/azure_portal.PNG)

## <a name="prerequisites"></a><span data-ttu-id="ff476-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff476-114">Prerequisites</span></span>

+ <span data-ttu-id="ff476-115">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="ff476-115">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>
+ <span data-ttu-id="ff476-116">Also, complete the following tutorial: [Import and publish your first API](import-and-publish.md).</span><span class="sxs-lookup"><span data-stu-id="ff476-116">Also, complete the following tutorial: [Import and publish your first API](import-and-publish.md).</span></span>

## <a name="add-a-new-revision"></a><span data-ttu-id="ff476-117">Add a new revision</span><span class="sxs-lookup"><span data-stu-id="ff476-117">Add a new revision</span></span>

1. <span data-ttu-id="ff476-118">Select **APIs** page.</span><span class="sxs-lookup"><span data-stu-id="ff476-118">Select **APIs** page.</span></span>
2. <span data-ttu-id="ff476-119">Select **Demo Conference API** from the API list (or other API to which you want to add revisions).</span><span class="sxs-lookup"><span data-stu-id="ff476-119">Select **Demo Conference API** from the API list (or other API to which you want to add revisions).</span></span>
3. <span data-ttu-id="ff476-120">Click the **Revisions** tab from the menu near the top of the page.</span><span class="sxs-lookup"><span data-stu-id="ff476-120">Click the **Revisions** tab from the menu near the top of the page.</span></span>
4. <span data-ttu-id="ff476-121">Select **+ Add Revision**</span><span class="sxs-lookup"><span data-stu-id="ff476-121">Select **+ Add Revision**</span></span>

    > [!TIP]
    > <span data-ttu-id="ff476-122">You can also choose **Add Revision** in the context menu (**...**) of the API.</span><span class="sxs-lookup"><span data-stu-id="ff476-122">You can also choose **Add Revision** in the context menu (**...**) of the API.</span></span>
    
    ![Revisions menu near top of screen](media/api-management-getstarted-revise-api/TopMenu.PNG)

5. <span data-ttu-id="ff476-124">Provide a description for your new revision, to help remember what it will be used for.</span><span class="sxs-lookup"><span data-stu-id="ff476-124">Provide a description for your new revision, to help remember what it will be used for.</span></span>
6. <span data-ttu-id="ff476-125">Select **Create**</span><span class="sxs-lookup"><span data-stu-id="ff476-125">Select **Create**</span></span>
7. <span data-ttu-id="ff476-126">Your new revision is now created.</span><span class="sxs-lookup"><span data-stu-id="ff476-126">Your new revision is now created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff476-127">Your original API remains in **Revision 1**.</span><span class="sxs-lookup"><span data-stu-id="ff476-127">Your original API remains in **Revision 1**.</span></span> <span data-ttu-id="ff476-128">This is the revision your users continue to call, until you choose to make a different revision current.</span><span class="sxs-lookup"><span data-stu-id="ff476-128">This is the revision your users continue to call, until you choose to make a different revision current.</span></span>

## <a name="make-non-breaking-changes-to-your-revision"></a><span data-ttu-id="ff476-129">Make non-breaking changes to your revision</span><span class="sxs-lookup"><span data-stu-id="ff476-129">Make non-breaking changes to your revision</span></span>

1. <span data-ttu-id="ff476-130">Select **Demo Conference API** from the API list.</span><span class="sxs-lookup"><span data-stu-id="ff476-130">Select **Demo Conference API** from the API list.</span></span>
2. <span data-ttu-id="ff476-131">Select the **Design** tab near the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="ff476-131">Select the **Design** tab near the top of the screen.</span></span>
3. <span data-ttu-id="ff476-132">Notice that the **revision selector** (directly above the design tab) shows **Revision 2** as currently selected.</span><span class="sxs-lookup"><span data-stu-id="ff476-132">Notice that the **revision selector** (directly above the design tab) shows **Revision 2** as currently selected.</span></span>

    > [!TIP]
    > <span data-ttu-id="ff476-133">Use the revision selector to switch between revisions that you wish to work on.</span><span class="sxs-lookup"><span data-stu-id="ff476-133">Use the revision selector to switch between revisions that you wish to work on.</span></span>

4. <span data-ttu-id="ff476-134">Select **+ Add Operation**.</span><span class="sxs-lookup"><span data-stu-id="ff476-134">Select **+ Add Operation**.</span></span>
5. <span data-ttu-id="ff476-135">Set your new operation to be **POST**, and the Name, Display Name and URL of the operation as **test**.</span><span class="sxs-lookup"><span data-stu-id="ff476-135">Set your new operation to be **POST**, and the Name, Display Name and URL of the operation as **test**.</span></span>
6. <span data-ttu-id="ff476-136">**Save** your new operation.</span><span class="sxs-lookup"><span data-stu-id="ff476-136">**Save** your new operation.</span></span>
7. <span data-ttu-id="ff476-137">We have now made a change to **Revision 2**.</span><span class="sxs-lookup"><span data-stu-id="ff476-137">We have now made a change to **Revision 2**.</span></span> <span data-ttu-id="ff476-138">Use the **Revision Selector** near the top of the page to switch back to **Revision 1**.</span><span class="sxs-lookup"><span data-stu-id="ff476-138">Use the **Revision Selector** near the top of the page to switch back to **Revision 1**.</span></span>
8. <span data-ttu-id="ff476-139">Notice that your new operation does not appear in **Revision 1**.</span><span class="sxs-lookup"><span data-stu-id="ff476-139">Notice that your new operation does not appear in **Revision 1**.</span></span> 

## <a name="make-your-revision-current-and-add-a-change-log-entry"></a><span data-ttu-id="ff476-140">Make your revision current and add a change log entry</span><span class="sxs-lookup"><span data-stu-id="ff476-140">Make your revision current and add a change log entry</span></span>

1. <span data-ttu-id="ff476-141">Select the **Revisions** tab from the menu near the top of the page.</span><span class="sxs-lookup"><span data-stu-id="ff476-141">Select the **Revisions** tab from the menu near the top of the page.</span></span>

    ![The revision menu on the revision screen.](media/api-management-getstarted-revise-api/RevisionsMenu.PNG)
2. <span data-ttu-id="ff476-143">Open the context menu (**...**) for **Revision 2**.</span><span class="sxs-lookup"><span data-stu-id="ff476-143">Open the context menu (**...**) for **Revision 2**.</span></span>
3. <span data-ttu-id="ff476-144">Select **Make Current**.</span><span class="sxs-lookup"><span data-stu-id="ff476-144">Select **Make Current**.</span></span>
4. <span data-ttu-id="ff476-145">Check **Post to Public Change log for this API**, if you want to post notes about this change.</span><span class="sxs-lookup"><span data-stu-id="ff476-145">Check **Post to Public Change log for this API**, if you want to post notes about this change.</span></span> <span data-ttu-id="ff476-146">Provide a description for your change that developers see, for example: **Testing revisions. Added new "test" operation.**</span><span class="sxs-lookup"><span data-stu-id="ff476-146">Provide a description for your change that developers see, for example: **Testing revisions. Added new "test" operation.**</span></span>
5. <span data-ttu-id="ff476-147">**Revision 2** is now current.</span><span class="sxs-lookup"><span data-stu-id="ff476-147">**Revision 2** is now current.</span></span>

## <a name="browse-the-developer-portal-to-see-changes-and-change-log"></a><span data-ttu-id="ff476-148">Browse the developer portal to see changes and change log</span><span class="sxs-lookup"><span data-stu-id="ff476-148">Browse the developer portal to see changes and change log</span></span>

1. <span data-ttu-id="ff476-149">In the Azure portal, select **APIs**.</span><span class="sxs-lookup"><span data-stu-id="ff476-149">In the Azure portal, select **APIs**.</span></span>
2. <span data-ttu-id="ff476-150">Select **Developer Portal** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="ff476-150">Select **Developer Portal** from the top menu.</span></span>
3. <span data-ttu-id="ff476-151">Select **APIs**, and then select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="ff476-151">Select **APIs**, and then select **Demo Conference API**.</span></span>
4. <span data-ttu-id="ff476-152">Notice your new **test** operation is now available.</span><span class="sxs-lookup"><span data-stu-id="ff476-152">Notice your new **test** operation is now available.</span></span>
5. <span data-ttu-id="ff476-153">Select **API Change History** from below the API name.</span><span class="sxs-lookup"><span data-stu-id="ff476-153">Select **API Change History** from below the API name.</span></span>
6. <span data-ttu-id="ff476-154">Notice that your change log entry appears in this list.</span><span class="sxs-lookup"><span data-stu-id="ff476-154">Notice that your change log entry appears in this list.</span></span>

    ![Developer portal](media/api-management-getstarted-revise-api/developer_portal.PNG)

## <a name="next-steps"></a><span data-ttu-id="ff476-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff476-156">Next steps</span></span>

<span data-ttu-id="ff476-157">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="ff476-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ff476-158">Add a new revision</span><span class="sxs-lookup"><span data-stu-id="ff476-158">Add a new revision</span></span>
> * <span data-ttu-id="ff476-159">Make non-breaking changes to your revision</span><span class="sxs-lookup"><span data-stu-id="ff476-159">Make non-breaking changes to your revision</span></span>
> * <span data-ttu-id="ff476-160">Make your revision current and add a change log entry</span><span class="sxs-lookup"><span data-stu-id="ff476-160">Make your revision current and add a change log entry</span></span>
> * <span data-ttu-id="ff476-161">Browse the developer portal to see changes and change log</span><span class="sxs-lookup"><span data-stu-id="ff476-161">Browse the developer portal to see changes and change log</span></span>

<span data-ttu-id="ff476-162">Advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="ff476-162">Advance to the next tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff476-163">Publish multiple versions of your API</span><span class="sxs-lookup"><span data-stu-id="ff476-163">Publish multiple versions of your API</span></span>](api-management-get-started-publish-versions.md)
