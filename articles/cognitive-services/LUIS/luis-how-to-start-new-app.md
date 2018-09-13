---
title: Create a new app with LUIS | Microsoft Docs
description: Create and manage your applications on the Language Understanding (LUIS) webpage.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 04/17/2018
ms.author: diberry
ms.openlocfilehash: 3adeecd4a4e2040a92689b7c92be9630c9a0d93b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856381"
---
# <a name="create-an-app"></a><span data-ttu-id="d7870-103">Create an app</span><span class="sxs-lookup"><span data-stu-id="d7870-103">Create an app</span></span>
<span data-ttu-id="d7870-104">You create a new app in different ways:</span><span class="sxs-lookup"><span data-stu-id="d7870-104">You create a new app in different ways:</span></span> 

* <span data-ttu-id="d7870-105">[Start](#create-new-app) with an empty app and create intents, utterances, and entities.</span><span class="sxs-lookup"><span data-stu-id="d7870-105">[Start](#create-new-app) with an empty app and create intents, utterances, and entities.</span></span>
* <span data-ttu-id="d7870-106">[Start](#create-new-app) with an empty app and add a [prebuilt domain](luis-how-to-use-prebuilt-domains.md).</span><span class="sxs-lookup"><span data-stu-id="d7870-106">[Start](#create-new-app) with an empty app and add a [prebuilt domain](luis-how-to-use-prebuilt-domains.md).</span></span>
* <span data-ttu-id="d7870-107">[Import a LUIS app](#import-new-app) from a JSON file that already contains intents, utterances, and entities.</span><span class="sxs-lookup"><span data-stu-id="d7870-107">[Import a LUIS app](#import-new-app) from a JSON file that already contains intents, utterances, and entities.</span></span>

## <a name="what-is-an-app"></a><span data-ttu-id="d7870-108">What is an app</span><span class="sxs-lookup"><span data-stu-id="d7870-108">What is an app</span></span>
<span data-ttu-id="d7870-109">The app contains [versions](luis-how-to-manage-versions.md) of your model as well as any [collaborators](luis-how-to-collaborate.md) for the app.</span><span class="sxs-lookup"><span data-stu-id="d7870-109">The app contains [versions](luis-how-to-manage-versions.md) of your model as well as any [collaborators](luis-how-to-collaborate.md) for the app.</span></span> <span data-ttu-id="d7870-110">When you create the app, you select the culture ([language](luis-supported-languages.md)) which **cannot be changed later**.</span><span class="sxs-lookup"><span data-stu-id="d7870-110">When you create the app, you select the culture ([language](luis-supported-languages.md)) which **cannot be changed later**.</span></span> 

<span data-ttu-id="d7870-111">The default version of a new app is "0.1."</span><span class="sxs-lookup"><span data-stu-id="d7870-111">The default version of a new app is "0.1."</span></span> 

<span data-ttu-id="d7870-112">You can create and manage your applications on **My Apps** page.</span><span class="sxs-lookup"><span data-stu-id="d7870-112">You can create and manage your applications on **My Apps** page.</span></span> <span data-ttu-id="d7870-113">You can always access this page by selecting **My apps** on the top navigation bar of the [LUIS](luis-reference-regions.md) website.</span><span class="sxs-lookup"><span data-stu-id="d7870-113">You can always access this page by selecting **My apps** on the top navigation bar of the [LUIS](luis-reference-regions.md) website.</span></span> 

<span data-ttu-id="d7870-114">[![](media/luis-create-new-app/apps-list.png "Screenshot of List of apps")](media/luis-create-new-app/apps-list.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d7870-114">[![](media/luis-create-new-app/apps-list.png "Screenshot of List of apps")](media/luis-create-new-app/apps-list.png#lightbox)</span></span>

## <a name="create-new-app"></a><span data-ttu-id="d7870-115">Create new app</span><span class="sxs-lookup"><span data-stu-id="d7870-115">Create new app</span></span>

1. <span data-ttu-id="d7870-116">On **My Apps** page, select **Create new app**.</span><span class="sxs-lookup"><span data-stu-id="d7870-116">On **My Apps** page, select **Create new app**.</span></span>
2. <span data-ttu-id="d7870-117">In the dialog box, name your application "TravelAgent".</span><span class="sxs-lookup"><span data-stu-id="d7870-117">In the dialog box, name your application "TravelAgent".</span></span>

    ![Create new app dialog](./media/luis-create-new-app/create-app.png)

3. <span data-ttu-id="d7870-119">Choose your application culture (for TravelAgent app, choose English), and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="d7870-119">Choose your application culture (for TravelAgent app, choose English), and then select **Done**.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="d7870-120">The culture cannot be changed once the application is created.</span><span class="sxs-lookup"><span data-stu-id="d7870-120">The culture cannot be changed once the application is created.</span></span> 

## <a name="import-new-app"></a><span data-ttu-id="d7870-121">Import new app</span><span class="sxs-lookup"><span data-stu-id="d7870-121">Import new app</span></span>
<span data-ttu-id="d7870-122">You can set the name (50 char max), version (10 char max), and description of an app in the JSON file.</span><span class="sxs-lookup"><span data-stu-id="d7870-122">You can set the name (50 char max), version (10 char max), and description of an app in the JSON file.</span></span> <span data-ttu-id="d7870-123">Examples of application JSON files are available at [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/Examples-BookFlight).</span><span class="sxs-lookup"><span data-stu-id="d7870-123">Examples of application JSON files are available at [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/Examples-BookFlight).</span></span>

1. <span data-ttu-id="d7870-124">On **My Apps** page, select **Import new app**.</span><span class="sxs-lookup"><span data-stu-id="d7870-124">On **My Apps** page, select **Import new app**.</span></span>
2. <span data-ttu-id="d7870-125">In the **Import new app** dialog, select the JSON file defining the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="d7870-125">In the **Import new app** dialog, select the JSON file defining the LUIS app.</span></span>

    ![Import a new app dialog](./media/luis-create-new-app/import-app.png)

## <a name="export-app"></a><span data-ttu-id="d7870-127">Export app</span><span class="sxs-lookup"><span data-stu-id="d7870-127">Export app</span></span>
1. <span data-ttu-id="d7870-128">On **My Apps** page, select the ellipsis (***...***) at the end of the app row.</span><span class="sxs-lookup"><span data-stu-id="d7870-128">On **My Apps** page, select the ellipsis (***...***) at the end of the app row.</span></span>

    <span data-ttu-id="d7870-129">[![](media/luis-create-new-app/apps-list.png "Screenshot of pop-up dialog of per-app actions")](media/luis-create-new-app/three-dots.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="d7870-129">[![](media/luis-create-new-app/apps-list.png "Screenshot of pop-up dialog of per-app actions")](media/luis-create-new-app/three-dots.png#lightbox)</span></span>

2. <span data-ttu-id="d7870-130">Select **Export app** from the menu.</span><span class="sxs-lookup"><span data-stu-id="d7870-130">Select **Export app** from the menu.</span></span> 

## <a name="rename-app"></a><span data-ttu-id="d7870-131">Rename app</span><span class="sxs-lookup"><span data-stu-id="d7870-131">Rename app</span></span>

1. <span data-ttu-id="d7870-132">On **My Apps** page, select the ellipsis (***...***) at the end of the app row.</span><span class="sxs-lookup"><span data-stu-id="d7870-132">On **My Apps** page, select the ellipsis (***...***) at the end of the app row.</span></span> 
2. <span data-ttu-id="d7870-133">Select **Rename** from the menu.</span><span class="sxs-lookup"><span data-stu-id="d7870-133">Select **Rename** from the menu.</span></span>
3. <span data-ttu-id="d7870-134">Enter the new name of the app and select **Done**.</span><span class="sxs-lookup"><span data-stu-id="d7870-134">Enter the new name of the app and select **Done**.</span></span>

## <a name="delete-app"></a><span data-ttu-id="d7870-135">Delete app</span><span class="sxs-lookup"><span data-stu-id="d7870-135">Delete app</span></span>

> [!CAUTION]
> <span data-ttu-id="d7870-136">You are deleting the app for all collaborators and the owner.</span><span class="sxs-lookup"><span data-stu-id="d7870-136">You are deleting the app for all collaborators and the owner.</span></span> <span data-ttu-id="d7870-137">[Export](#export-app) the app before deleting it.</span><span class="sxs-lookup"><span data-stu-id="d7870-137">[Export](#export-app) the app before deleting it.</span></span> 

1. <span data-ttu-id="d7870-138">On **My Apps** page, select the ellipsis (***...***) at the end of the app row.</span><span class="sxs-lookup"><span data-stu-id="d7870-138">On **My Apps** page, select the ellipsis (***...***) at the end of the app row.</span></span> 
2. <span data-ttu-id="d7870-139">Select **Delete** from the menu.</span><span class="sxs-lookup"><span data-stu-id="d7870-139">Select **Delete** from the menu.</span></span>
3. <span data-ttu-id="d7870-140">Select **Ok** in the confirmation window.</span><span class="sxs-lookup"><span data-stu-id="d7870-140">Select **Ok** in the confirmation window.</span></span>

## <a name="export-endpoint-logs"></a><span data-ttu-id="d7870-141">Export endpoint logs</span><span class="sxs-lookup"><span data-stu-id="d7870-141">Export endpoint logs</span></span>
<span data-ttu-id="d7870-142">The logs contain the Query, UTC time, and LUIS JSON response.</span><span class="sxs-lookup"><span data-stu-id="d7870-142">The logs contain the Query, UTC time, and LUIS JSON response.</span></span>

1. <span data-ttu-id="d7870-143">On **My Apps** page, select the ellipsis (***...***) at the end of the app row.</span><span class="sxs-lookup"><span data-stu-id="d7870-143">On **My Apps** page, select the ellipsis (***...***) at the end of the app row.</span></span> 
2. <span data-ttu-id="d7870-144">Select **Export endpoint logs** from the menu.</span><span class="sxs-lookup"><span data-stu-id="d7870-144">Select **Export endpoint logs** from the menu.</span></span>

```
Query,UTC DateTime,Response
text i'm driving and will be 30 minutes late to the meeting,02/13/2018 15:18:43,"{""query"":""text I'm driving and will be 30 minutes late to the meeting"",""intents"":[{""intent"":""None"",""score"":0.111048922},{""intent"":""SendMessage"",""score"":0.987501}],""entities"":[{""entity"":""i ' m driving and will be 30 minutes late to the meeting"",""type"":""Message"",""startIndex"":5,""endIndex"":58,""score"":0.162995353}]}"
```

## <a name="next-steps"></a><span data-ttu-id="d7870-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7870-145">Next steps</span></span>

<span data-ttu-id="d7870-146">Your first task in the app is to [add intents](luis-how-to-add-intents.md).</span><span class="sxs-lookup"><span data-stu-id="d7870-146">Your first task in the app is to [add intents](luis-how-to-add-intents.md).</span></span>