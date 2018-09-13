---
title: Understand versioning in LUIS - Azure | Microsoft Docs
description: Learn how to use versions to manage changes in Language Understanding (LUIS)
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/13/2018
ms.author: diberry
ms.openlocfilehash: 17abe383d3074d636605c3b1b91927f89f7dd896
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966124"
---
# <a name="versions"></a><span data-ttu-id="24835-103">Versions</span><span class="sxs-lookup"><span data-stu-id="24835-103">Versions</span></span>
<span data-ttu-id="24835-104">Create different models of the same app with [versions](luis-how-to-manage-versions.md).</span><span class="sxs-lookup"><span data-stu-id="24835-104">Create different models of the same app with [versions](luis-how-to-manage-versions.md).</span></span> 

## <a name="version-id"></a><span data-ttu-id="24835-105">Version ID</span><span class="sxs-lookup"><span data-stu-id="24835-105">Version ID</span></span>
<span data-ttu-id="24835-106">The version ID consists of characters, digits or '.' and cannot be longer than 10 characters.</span><span class="sxs-lookup"><span data-stu-id="24835-106">The version ID consists of characters, digits or '.' and cannot be longer than 10 characters.</span></span>

## <a name="initial-version"></a><span data-ttu-id="24835-107">Initial version</span><span class="sxs-lookup"><span data-stu-id="24835-107">Initial version</span></span>
<span data-ttu-id="24835-108">The initial version (0.1) is the default active version.</span><span class="sxs-lookup"><span data-stu-id="24835-108">The initial version (0.1) is the default active version.</span></span> 

## <a name="active-version"></a><span data-ttu-id="24835-109">Active version</span><span class="sxs-lookup"><span data-stu-id="24835-109">Active version</span></span>
<span data-ttu-id="24835-110">To [set a version](luis-how-to-manage-versions.md#set-active-version) as the active means it is currently edited and tested in the [LUIS](luis-reference-regions.md) website.</span><span class="sxs-lookup"><span data-stu-id="24835-110">To [set a version](luis-how-to-manage-versions.md#set-active-version) as the active means it is currently edited and tested in the [LUIS](luis-reference-regions.md) website.</span></span> <span data-ttu-id="24835-111">Set a version as active to access its data, make updates, as well as to test and publish it.</span><span class="sxs-lookup"><span data-stu-id="24835-111">Set a version as active to access its data, make updates, as well as to test and publish it.</span></span>

<span data-ttu-id="24835-112">The name of the currently active version is displayed in the top, left panel after the app name.</span><span class="sxs-lookup"><span data-stu-id="24835-112">The name of the currently active version is displayed in the top, left panel after the app name.</span></span> 

<span data-ttu-id="24835-113">[ ![Change active version](./media/luis-concept-version/version-in-nav-bar-inline.png) ](./media/luis-concept-version/version-in-nav-bar-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="24835-113">[ ![Change active version](./media/luis-concept-version/version-in-nav-bar-inline.png) ](./media/luis-concept-version/version-in-nav-bar-expanded.png#lightbox)</span></span>

## <a name="versions-and-publishing-slots"></a><span data-ttu-id="24835-114">Versions and publishing slots</span><span class="sxs-lookup"><span data-stu-id="24835-114">Versions and publishing slots</span></span>
<span data-ttu-id="24835-115">You publish to either the stage and product slots.</span><span class="sxs-lookup"><span data-stu-id="24835-115">You publish to either the stage and product slots.</span></span> <span data-ttu-id="24835-116">Each slot can have a different version or the same version.</span><span class="sxs-lookup"><span data-stu-id="24835-116">Each slot can have a different version or the same version.</span></span> <span data-ttu-id="24835-117">This is useful for verifying changes between model versions via the endpoint, which is available to bots or other LUIS calling applications.</span><span class="sxs-lookup"><span data-stu-id="24835-117">This is useful for verifying changes between model versions via the endpoint, which is available to bots or other LUIS calling applications.</span></span> 

## <a name="clone-a-version"></a><span data-ttu-id="24835-118">Clone a version</span><span class="sxs-lookup"><span data-stu-id="24835-118">Clone a version</span></span>
<span data-ttu-id="24835-119">Clone a version to create a copy of an existing version and save it as a new version.</span><span class="sxs-lookup"><span data-stu-id="24835-119">Clone a version to create a copy of an existing version and save it as a new version.</span></span> <span data-ttu-id="24835-120">Clone a version to use the same content of the existing version as a starting point for the new version.</span><span class="sxs-lookup"><span data-stu-id="24835-120">Clone a version to use the same content of the existing version as a starting point for the new version.</span></span> <span data-ttu-id="24835-121">Once you clone a version, the new version becomes the **active** version.</span><span class="sxs-lookup"><span data-stu-id="24835-121">Once you clone a version, the new version becomes the **active** version.</span></span> 

## <a name="import-and-export-a-version"></a><span data-ttu-id="24835-122">Import and export a version</span><span class="sxs-lookup"><span data-stu-id="24835-122">Import and export a version</span></span>
<span data-ttu-id="24835-123">You can import a version at the app level.</span><span class="sxs-lookup"><span data-stu-id="24835-123">You can import a version at the app level.</span></span> <span data-ttu-id="24835-124">That version becomes the active version and used the version ID in the "versionId" property of the app file.</span><span class="sxs-lookup"><span data-stu-id="24835-124">That version becomes the active version and used the version ID in the "versionId" property of the app file.</span></span> <span data-ttu-id="24835-125">You can also import at the version level into an existing app.</span><span class="sxs-lookup"><span data-stu-id="24835-125">You can also import at the version level into an existing app.</span></span> <span data-ttu-id="24835-126">The new version becomes the active version.</span><span class="sxs-lookup"><span data-stu-id="24835-126">The new version becomes the active version.</span></span> 

<span data-ttu-id="24835-127">You can export a version at the app level or you can export a version at the version level.</span><span class="sxs-lookup"><span data-stu-id="24835-127">You can export a version at the app level or you can export a version at the version level.</span></span> <span data-ttu-id="24835-128">The only difference is that the app-level exported version is the currently active version while at the version level, you can choose any version to export on the **[Settings](luis-how-to-manage-versions.md)** page.</span><span class="sxs-lookup"><span data-stu-id="24835-128">The only difference is that the app-level exported version is the currently active version while at the version level, you can choose any version to export on the **[Settings](luis-how-to-manage-versions.md)** page.</span></span> 

<span data-ttu-id="24835-129">The exported file does not contain machine-learned information because the app is retrained after it is imported.</span><span class="sxs-lookup"><span data-stu-id="24835-129">The exported file does not contain machine-learned information because the app is retrained after it is imported.</span></span> <span data-ttu-id="24835-130">The exported file does not contain collaborators -- you need to add these back once the version is imported into the new app.</span><span class="sxs-lookup"><span data-stu-id="24835-130">The exported file does not contain collaborators -- you need to add these back once the version is imported into the new app.</span></span>

## <a name="export-each-version-as-app-backup"></a><span data-ttu-id="24835-131">Export each version as app backup</span><span class="sxs-lookup"><span data-stu-id="24835-131">Export each version as app backup</span></span>
<span data-ttu-id="24835-132">In order to back up your LUIS app, export each version on the **[Settings](luis-how-to-manage-versions.md)** page.</span><span class="sxs-lookup"><span data-stu-id="24835-132">In order to back up your LUIS app, export each version on the **[Settings](luis-how-to-manage-versions.md)** page.</span></span>

## <a name="delete-a-version"></a><span data-ttu-id="24835-133">Delete a version</span><span class="sxs-lookup"><span data-stu-id="24835-133">Delete a version</span></span>
<span data-ttu-id="24835-134">You can delete all versions except the active version from the Versions list on Settings page.</span><span class="sxs-lookup"><span data-stu-id="24835-134">You can delete all versions except the active version from the Versions list on Settings page.</span></span> 

## <a name="version-availability-at-the-endpoint"></a><span data-ttu-id="24835-135">Version availability at the endpoint</span><span class="sxs-lookup"><span data-stu-id="24835-135">Version availability at the endpoint</span></span>
<span data-ttu-id="24835-136">Trained versions are not automatically available at your app [endpoint](luis-glossary.md#endpoint).</span><span class="sxs-lookup"><span data-stu-id="24835-136">Trained versions are not automatically available at your app [endpoint](luis-glossary.md#endpoint).</span></span> <span data-ttu-id="24835-137">You must [publish](luis-how-to-publish-app.md) or republish a version in order for it to be available at your app endpoint.</span><span class="sxs-lookup"><span data-stu-id="24835-137">You must [publish](luis-how-to-publish-app.md) or republish a version in order for it to be available at your app endpoint.</span></span> <span data-ttu-id="24835-138">You can publish to **Staging** and **Production**, giving you up to two versions of the app available at the endpoint.</span><span class="sxs-lookup"><span data-stu-id="24835-138">You can publish to **Staging** and **Production**, giving you up to two versions of the app available at the endpoint.</span></span> <span data-ttu-id="24835-139">If you need more versions of the app available at an endpoint, you should export the version and reimport to a new app.</span><span class="sxs-lookup"><span data-stu-id="24835-139">If you need more versions of the app available at an endpoint, you should export the version and reimport to a new app.</span></span> <span data-ttu-id="24835-140">The new app has a different app ID.</span><span class="sxs-lookup"><span data-stu-id="24835-140">The new app has a different app ID.</span></span>

## <a name="collaborators"></a><span data-ttu-id="24835-141">Collaborators</span><span class="sxs-lookup"><span data-stu-id="24835-141">Collaborators</span></span>
<span data-ttu-id="24835-142">The owner and all [collaborators](luis-how-to-collaborate.md) have full access to all versions of the app.</span><span class="sxs-lookup"><span data-stu-id="24835-142">The owner and all [collaborators](luis-how-to-collaborate.md) have full access to all versions of the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24835-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="24835-143">Next steps</span></span>

<span data-ttu-id="24835-144">See how to add [versioning](luis-how-to-manage-versions.md) on the app settings page.</span><span class="sxs-lookup"><span data-stu-id="24835-144">See how to add [versioning](luis-how-to-manage-versions.md) on the app settings page.</span></span> 

<span data-ttu-id="24835-145">Learn how to design [intents](luis-concept-intent.md) into the model.</span><span class="sxs-lookup"><span data-stu-id="24835-145">Learn how to design [intents](luis-concept-intent.md) into the model.</span></span>