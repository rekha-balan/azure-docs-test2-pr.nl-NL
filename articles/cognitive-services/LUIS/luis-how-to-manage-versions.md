---
title: Manage versions in LUIS apps in Azure | Microsoft Docs
description: Learn how to manage versions in Language Understanding (LUIS) applications.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/29/2017
ms.author: diberry
ms.openlocfilehash: 4941cf533f1b860ead07a416d5af6f62a1978305
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871663"
---
# <a name="manage-versions"></a><span data-ttu-id="602ee-103">Manage versions</span><span class="sxs-lookup"><span data-stu-id="602ee-103">Manage versions</span></span>

<span data-ttu-id="602ee-104">Each time you work on the model, create a different [version](luis-concept-version.md) of the app.</span><span class="sxs-lookup"><span data-stu-id="602ee-104">Each time you work on the model, create a different [version](luis-concept-version.md) of the app.</span></span> 

## <a name="set-active-version"></a><span data-ttu-id="602ee-105">Set active version</span><span class="sxs-lookup"><span data-stu-id="602ee-105">Set active version</span></span>
<span data-ttu-id="602ee-106">To work with versions, open your app by selecting its name on **My Apps** page, and then select **Settings** in the top bar.</span><span class="sxs-lookup"><span data-stu-id="602ee-106">To work with versions, open your app by selecting its name on **My Apps** page, and then select **Settings** in the top bar.</span></span>

![Versions page](./media/luis-how-to-manage-versions/settings.png)

<span data-ttu-id="602ee-108">The **Settings** page allows you to configure settings for the entire app including versions, and collaborators.</span><span class="sxs-lookup"><span data-stu-id="602ee-108">The **Settings** page allows you to configure settings for the entire app including versions, and collaborators.</span></span> 

## <a name="clone-a-version"></a><span data-ttu-id="602ee-109">Clone a version</span><span class="sxs-lookup"><span data-stu-id="602ee-109">Clone a version</span></span>
1. <span data-ttu-id="602ee-110">On the **Settings** page, after the App Settings and Collaborators sections, find the row with the version you want to clone.</span><span class="sxs-lookup"><span data-stu-id="602ee-110">On the **Settings** page, after the App Settings and Collaborators sections, find the row with the version you want to clone.</span></span> <span data-ttu-id="602ee-111">Select the ellipsis (***...***) button on the far-right.</span><span class="sxs-lookup"><span data-stu-id="602ee-111">Select the ellipsis (***...***) button on the far-right.</span></span> 

    ![Version row properties](./media/luis-how-to-manage-versions/version-section.png)

2. <span data-ttu-id="602ee-113">Select **Clone** from the list.</span><span class="sxs-lookup"><span data-stu-id="602ee-113">Select **Clone** from the list.</span></span>

    ![Version row properties choice](./media/luis-how-to-manage-versions/version-three-dots-modal.png)

3. <span data-ttu-id="602ee-115">In the **Clone version** dialog box, type a name for the new version such as "0.2".</span><span class="sxs-lookup"><span data-stu-id="602ee-115">In the **Clone version** dialog box, type a name for the new version such as "0.2".</span></span>

   ![Clone Version dialog box](./media/luis-how-to-manage-versions/version-clone-version-dialog.png)
 
 > [!NOTE]
 > <span data-ttu-id="602ee-117">Version ID can consist only of characters, digits or '.' and cannot be longer than 10 characters.</span><span class="sxs-lookup"><span data-stu-id="602ee-117">Version ID can consist only of characters, digits or '.' and cannot be longer than 10 characters.</span></span>
 
 <span data-ttu-id="602ee-118">A new version with the specified name is created and set as the active version.</span><span class="sxs-lookup"><span data-stu-id="602ee-118">A new version with the specified name is created and set as the active version.</span></span>
 
  ![Version is created and added to the list](./media/luis-how-to-manage-versions/new-version.png)

 > [!NOTE]
 > <span data-ttu-id="602ee-120">As shown in the preceding image, a published version is associated with a colored mark, indicating the type of slot where it has been published: Production (green), Staging (red) and both (black).</span><span class="sxs-lookup"><span data-stu-id="602ee-120">As shown in the preceding image, a published version is associated with a colored mark, indicating the type of slot where it has been published: Production (green), Staging (red) and both (black).</span></span> <span data-ttu-id="602ee-121">The training and publishing dates are displayed for each published version.</span><span class="sxs-lookup"><span data-stu-id="602ee-121">The training and publishing dates are displayed for each published version.</span></span>

## <a name="set-active-version"></a><span data-ttu-id="602ee-122">Set active version</span><span class="sxs-lookup"><span data-stu-id="602ee-122">Set active version</span></span>
1. <span data-ttu-id="602ee-123">On the **Settings** page, in the **Versions** list, select the ellipsis (***...***) button at the far right.</span><span class="sxs-lookup"><span data-stu-id="602ee-123">On the **Settings** page, in the **Versions** list, select the ellipsis (***...***) button at the far right.</span></span>

2. <span data-ttu-id="602ee-124">From the pop-up list, select **Set as active**.</span><span class="sxs-lookup"><span data-stu-id="602ee-124">From the pop-up list, select **Set as active**.</span></span>

    ![Set active version](./media/luis-how-to-manage-versions/set-active-version.png)

    <span data-ttu-id="602ee-126">The active version is highlighted by a light blue color, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="602ee-126">The active version is highlighted by a light blue color, as shown in the following screenshot:</span></span>

    ![The active version](./media/luis-how-to-manage-versions/set-active-version-done.png) 


## <a name="import-version"></a><span data-ttu-id="602ee-128">Import version</span><span class="sxs-lookup"><span data-stu-id="602ee-128">Import version</span></span>
<span data-ttu-id="602ee-129">You can import a version from a JSON file.</span><span class="sxs-lookup"><span data-stu-id="602ee-129">You can import a version from a JSON file.</span></span> <span data-ttu-id="602ee-130">Once you import a version, the new version becomes the active version.</span><span class="sxs-lookup"><span data-stu-id="602ee-130">Once you import a version, the new version becomes the active version.</span></span>

<span data-ttu-id="602ee-131">**To import a version:**</span><span class="sxs-lookup"><span data-stu-id="602ee-131">**To import a version:**</span></span>

1. <span data-ttu-id="602ee-132">On the **Settings** page, select **Import new version** button.</span><span class="sxs-lookup"><span data-stu-id="602ee-132">On the **Settings** page, select **Import new version** button.</span></span>

    ![Import Button](./media/luis-how-to-manage-versions/import-version.png)

2. <span data-ttu-id="602ee-134">Select **browse** and choose the JSON file.</span><span class="sxs-lookup"><span data-stu-id="602ee-134">Select **browse** and choose the JSON file.</span></span>

    ![Import version dialog](./media/luis-how-to-manage-versions/import-version-dialog.png)

<span data-ttu-id="602ee-136">You only need to set a version ID if the version in the JSON file already exists in the app.</span><span class="sxs-lookup"><span data-stu-id="602ee-136">You only need to set a version ID if the version in the JSON file already exists in the app.</span></span>

## <a name="export-version"></a><span data-ttu-id="602ee-137">Export version</span><span class="sxs-lookup"><span data-stu-id="602ee-137">Export version</span></span>
<span data-ttu-id="602ee-138">You can export a version to a JSON file.</span><span class="sxs-lookup"><span data-stu-id="602ee-138">You can export a version to a JSON file.</span></span>

<span data-ttu-id="602ee-139">**To export a version:**</span><span class="sxs-lookup"><span data-stu-id="602ee-139">**To export a version:**</span></span>

1. <span data-ttu-id="602ee-140">On the **Settings** page, in the **Versions** list, select the ellipsis (***...***) button at the far right.</span><span class="sxs-lookup"><span data-stu-id="602ee-140">On the **Settings** page, in the **Versions** list, select the ellipsis (***...***) button at the far right.</span></span>

2. <span data-ttu-id="602ee-141">Select **Export** in the pop-up list of actions and select where you want to save the file.</span><span class="sxs-lookup"><span data-stu-id="602ee-141">Select **Export** in the pop-up list of actions and select where you want to save the file.</span></span>

## <a name="delete-a-version"></a><span data-ttu-id="602ee-142">Delete a version</span><span class="sxs-lookup"><span data-stu-id="602ee-142">Delete a version</span></span>
<span data-ttu-id="602ee-143">You can delete versions, but you have to keep at least one version of the app.</span><span class="sxs-lookup"><span data-stu-id="602ee-143">You can delete versions, but you have to keep at least one version of the app.</span></span> <span data-ttu-id="602ee-144">You can delete all versions except the active version.</span><span class="sxs-lookup"><span data-stu-id="602ee-144">You can delete all versions except the active version.</span></span> 

1. <span data-ttu-id="602ee-145">On the **Settings** page, in the **Versions** list, select the ellipsis (***...***) button at the far right.</span><span class="sxs-lookup"><span data-stu-id="602ee-145">On the **Settings** page, in the **Versions** list, select the ellipsis (***...***) button at the far right.</span></span>

2. <span data-ttu-id="602ee-146">Select **Delete** in the pop-up list of actions and select where you want to save the file.</span><span class="sxs-lookup"><span data-stu-id="602ee-146">Select **Delete** in the pop-up list of actions and select where you want to save the file.</span></span>

    ![Delete version confirmation](./media/luis-how-to-manage-versions/delete-menu.png) 


## <a name="rename-a-version"></a><span data-ttu-id="602ee-148">Rename a version</span><span class="sxs-lookup"><span data-stu-id="602ee-148">Rename a version</span></span>
<span data-ttu-id="602ee-149">You can rename versions as long as the version name is not already in use.</span><span class="sxs-lookup"><span data-stu-id="602ee-149">You can rename versions as long as the version name is not already in use.</span></span>  

1. <span data-ttu-id="602ee-150">On the **Settings** page, in the **Versions** list, select the ellipsis (***...***) button at the far right.</span><span class="sxs-lookup"><span data-stu-id="602ee-150">On the **Settings** page, in the **Versions** list, select the ellipsis (***...***) button at the far right.</span></span>

2. <span data-ttu-id="602ee-151">Select **Rename** in the pop-up list of actions.</span><span class="sxs-lookup"><span data-stu-id="602ee-151">Select **Rename** in the pop-up list of actions.</span></span>

3. <span data-ttu-id="602ee-152">Enter the new version name and select **Done**.</span><span class="sxs-lookup"><span data-stu-id="602ee-152">Enter the new version name and select **Done**.</span></span>

    ![Rename version confirmation](./media/luis-how-to-manage-versions/rename-popup.png) 
