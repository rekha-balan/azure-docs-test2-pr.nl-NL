---
title: Managing user data with Conversation Learner - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to manage user data with Conversation Learner.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: f9de4377857188a8cf483321654fb857e428c7f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856759"
---
# <a name="managing-user-data"></a><span data-ttu-id="b2ae0-103">Managing user data</span><span class="sxs-lookup"><span data-stu-id="b2ae0-103">Managing user data</span></span>

<span data-ttu-id="b2ae0-104">This page describes what the Conversation Learner cloud service logs when conducting dialogs with end users.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-104">This page describes what the Conversation Learner cloud service logs when conducting dialogs with end users.</span></span>  <span data-ttu-id="b2ae0-105">It also describes how to associate Conversation Learner logs with user IDs, so that you can retrieve or delete all logs associated with a particular user.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-105">It also describes how to associate Conversation Learner logs with user IDs, so that you can retrieve or delete all logs associated with a particular user.</span></span>

## <a name="overview-of-end-user-data-logging"></a><span data-ttu-id="b2ae0-106">Overview of end-user data logging</span><span class="sxs-lookup"><span data-stu-id="b2ae0-106">Overview of end-user data logging</span></span>

<span data-ttu-id="b2ae0-107">By default, the Conversation Learner cloud service logs interactions between end users and your bot.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-107">By default, the Conversation Learner cloud service logs interactions between end users and your bot.</span></span>  <span data-ttu-id="b2ae0-108">These logs are important for improving your bot, enabling you to identify cases where your bot extracted the incorrect entity or selected the incorrect action.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-108">These logs are important for improving your bot, enabling you to identify cases where your bot extracted the incorrect entity or selected the incorrect action.</span></span>  <span data-ttu-id="b2ae0-109">These errors can then be corrected by going to the "Log Dialogs" page of the UI, making corrections, and storing this corrected dialog as a new train dialog.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-109">These errors can then be corrected by going to the "Log Dialogs" page of the UI, making corrections, and storing this corrected dialog as a new train dialog.</span></span> <span data-ttu-id="b2ae0-110">For more information, see the tutorial on "Log Dialogs."</span><span class="sxs-lookup"><span data-stu-id="b2ae0-110">For more information, see the tutorial on "Log Dialogs."</span></span>

## <a name="how-to-disable-logging"></a><span data-ttu-id="b2ae0-111">How to disable logging</span><span class="sxs-lookup"><span data-stu-id="b2ae0-111">How to disable logging</span></span>

<span data-ttu-id="b2ae0-112">You can control whether conversations with end users are on the "Settings" page for your Conversation Learner model.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-112">You can control whether conversations with end users are on the "Settings" page for your Conversation Learner model.</span></span>  <span data-ttu-id="b2ae0-113">There is a checkbox for "Log Conversations."</span><span class="sxs-lookup"><span data-stu-id="b2ae0-113">There is a checkbox for "Log Conversations."</span></span>  <span data-ttu-id="b2ae0-114">By unchecking this box, conversations with end users will not be logged.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-114">By unchecking this box, conversations with end users will not be logged.</span></span>

## <a name="what-is-logged"></a><span data-ttu-id="b2ae0-115">What is logged</span><span class="sxs-lookup"><span data-stu-id="b2ae0-115">What is logged</span></span> 

<span data-ttu-id="b2ae0-116">In log dialogs, Conversation Learner stores the user input, entity values, selected actions, and timestamps for each turn.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-116">In log dialogs, Conversation Learner stores the user input, entity values, selected actions, and timestamps for each turn.</span></span>  <span data-ttu-id="b2ae0-117">These logs are stored for a period of time, and then discarded (see the help page on "Default value and boundaries" for details).</span><span class="sxs-lookup"><span data-stu-id="b2ae0-117">These logs are stored for a period of time, and then discarded (see the help page on "Default value and boundaries" for details).</span></span>  

<span data-ttu-id="b2ae0-118">Conversation Learner creates a unique ID for each logged dialog.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-118">Conversation Learner creates a unique ID for each logged dialog.</span></span>  <span data-ttu-id="b2ae0-119">Conversation Learner does *not* store a user identifier with logged dialogs.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-119">Conversation Learner does *not* store a user identifier with logged dialogs.</span></span>  

## <a name="associating-logged-dialogs-with-a-user-id"></a><span data-ttu-id="b2ae0-120">Associating logged dialogs with a user ID</span><span class="sxs-lookup"><span data-stu-id="b2ae0-120">Associating logged dialogs with a user ID</span></span>

<span data-ttu-id="b2ae0-121">It is often important to be able to associate logged dialogs with the ID of the user -- for example, to be able to retrieve or delete logged dialogs from a particular user.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-121">It is often important to be able to associate logged dialogs with the ID of the user -- for example, to be able to retrieve or delete logged dialogs from a particular user.</span></span>  <span data-ttu-id="b2ae0-122">Since Conversation Learner does not store a user identifier, this association needs to be maintained by the developer's code.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-122">Since Conversation Learner does not store a user identifier, this association needs to be maintained by the developer's code.</span></span>  

<span data-ttu-id="b2ae0-123">To create this mapping, obtain the ID of the logged dialog in `EntityDetectionCallback`; then in your bot's storage, store the association between the user ID and this logged dialog.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-123">To create this mapping, obtain the ID of the logged dialog in `EntityDetectionCallback`; then in your bot's storage, store the association between the user ID and this logged dialog.</span></span>  

```
cl.EntityDetectionCallback(async (text: string, memoryManager: ClientMemoryManager): Promise<void> => {

    // Get user and session info
    var sessionData = memoryManager.SessionInfo();

    // sessionData.sessionId is the ID of this logged dialog.
    // In your bot-specific datastore, store an association
    // bewteen your user identifier and this session ID.
    console.log(sessionData.logDialogId)

    // sessionData.userId and sessionData.userName are the 
    // user ID and user name as defined by the channel the user
    // is on (eg, Skype, Teams, Facebook Messenger, etc.).
    // For some channels, this will be undefined.
    // This information is NOT stored with the logged dialog.
    console.log(sessionData.userId);
    console.log(sessionData.userName);

})
```

## <a name="headers-for-http-calls"></a><span data-ttu-id="b2ae0-124">Headers for HTTP calls</span><span class="sxs-lookup"><span data-stu-id="b2ae0-124">Headers for HTTP calls</span></span>

<span data-ttu-id="b2ae0-125">In each of the HTTP calls below, add the following header:</span><span class="sxs-lookup"><span data-stu-id="b2ae0-125">In each of the HTTP calls below, add the following header:</span></span>

```
Ocp-Apim-Subscription-Key=<LUIS_AUTHORING_KEY>
```

<span data-ttu-id="b2ae0-126">where `<LUIS_AUTHORING_KEY>` is the LUIS authoring key used to access your Conversation Learner Applications.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-126">where `<LUIS_AUTHORING_KEY>` is the LUIS authoring key used to access your Conversation Learner Applications.</span></span>

## <a name="how-to-obtain-raw-data-for-a-logged-dialog"></a><span data-ttu-id="b2ae0-127">How to obtain raw data for a logged dialog</span><span class="sxs-lookup"><span data-stu-id="b2ae0-127">How to obtain raw data for a logged dialog</span></span>

<span data-ttu-id="b2ae0-128">To obtain the raw data for a log dialog, you can use this HTTP call:</span><span class="sxs-lookup"><span data-stu-id="b2ae0-128">To obtain the raw data for a log dialog, you can use this HTTP call:</span></span>

```
GET https://westus.api.cognitive.microsoft.com/conversationlearner/v1.0/app/<appId>/logdialog/<logDialogId>
```

<span data-ttu-id="b2ae0-129">Where `<appId>` is the GUID for this Conversation Learner model, and `<logDialgoId>` is the ID of the log dialog you want to retrieve.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-129">Where `<appId>` is the GUID for this Conversation Learner model, and `<logDialgoId>` is the ID of the log dialog you want to retrieve.</span></span>  

> [!NOTE]
> <span data-ttu-id="b2ae0-130">Log dialogs may be edited by the developer, and then stored as train dialogs.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-130">Log dialogs may be edited by the developer, and then stored as train dialogs.</span></span>  <span data-ttu-id="b2ae0-131">When this is done, Conversation Learner stores the ID of the "source" log dialog with the train dialog.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-131">When this is done, Conversation Learner stores the ID of the "source" log dialog with the train dialog.</span></span>  <span data-ttu-id="b2ae0-132">Further, a train dialog can be "branched" in the UI; if a train dialog has an associated source log dialog ID, then branches from that train dialog will be marked with the same log dialog ID.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-132">Further, a train dialog can be "branched" in the UI; if a train dialog has an associated source log dialog ID, then branches from that train dialog will be marked with the same log dialog ID.</span></span>

<span data-ttu-id="b2ae0-133">To obtain all train dialogs that were derived from a log dialog, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-133">To obtain all train dialogs that were derived from a log dialog, follow these steps.</span></span>

<span data-ttu-id="b2ae0-134">First, retrieve all train dialogs:</span><span class="sxs-lookup"><span data-stu-id="b2ae0-134">First, retrieve all train dialogs:</span></span>

```
GET https://westus.api.cognitive.microsoft.com/conversationlearner/v1.0/app/<appId>/traindialogs
```

<span data-ttu-id="b2ae0-135">Where `<appId>` is the GUID for this Conversation Learner model.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-135">Where `<appId>` is the GUID for this Conversation Learner model.</span></span>  

<span data-ttu-id="b2ae0-136">This returns all train dialogs.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-136">This returns all train dialogs.</span></span>  <span data-ttu-id="b2ae0-137">Search this list for the associated `sourceLogDialogId`, and note the associated `trainDialogId`.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-137">Search this list for the associated `sourceLogDialogId`, and note the associated `trainDialogId`.</span></span> 

<span data-ttu-id="b2ae0-138">To a single train dialog by ID:</span><span class="sxs-lookup"><span data-stu-id="b2ae0-138">To a single train dialog by ID:</span></span>

```
GET https://westus.api.cognitive.microsoft.com/conversationlearner/v1.0/app/<appId>/traindialog/<trainDialogId>
```

<span data-ttu-id="b2ae0-139">Where `<appId>` is the GUID for this Conversation Learner model, and `<trainDialogId>` is the ID of the train dialog you want to retrieve.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-139">Where `<appId>` is the GUID for this Conversation Learner model, and `<trainDialogId>` is the ID of the train dialog you want to retrieve.</span></span>  

## <a name="how-to-delete-a-logged-dialog"></a><span data-ttu-id="b2ae0-140">How to delete a logged dialog</span><span class="sxs-lookup"><span data-stu-id="b2ae0-140">How to delete a logged dialog</span></span>

<span data-ttu-id="b2ae0-141">If you wish to delete a log dialog given its ID, you can use this HTTP call:</span><span class="sxs-lookup"><span data-stu-id="b2ae0-141">If you wish to delete a log dialog given its ID, you can use this HTTP call:</span></span>

```
DELETE https://westus.api.cognitive.microsoft.com/conversationlearner/v1.0/app/<appId>/logdialog/<logDialogId>
```

<span data-ttu-id="b2ae0-142">Where `<appId>` is the GUID for this Conversation Learner model, and `<logDialogId>` is the ID of the log dialog you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-142">Where `<appId>` is the GUID for this Conversation Learner model, and `<logDialogId>` is the ID of the log dialog you wish to delete.</span></span> 

<span data-ttu-id="b2ae0-143">If you wish to delete a train dialog given its ID, you can use this HTTP call:</span><span class="sxs-lookup"><span data-stu-id="b2ae0-143">If you wish to delete a train dialog given its ID, you can use this HTTP call:</span></span>

```
DELETE https://westus.api.cognitive.microsoft.com/conversationlearner/v1.0/app/<appId>/traindialog/<trainDialogId>
```

<span data-ttu-id="b2ae0-144">Where `<appId>` is the GUID for this Conversation Learner model, and `<trainDialogId>` is the ID of the train dialog you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="b2ae0-144">Where `<appId>` is the GUID for this Conversation Learner model, and `<trainDialogId>` is the ID of the train dialog you wish to delete.</span></span> 
