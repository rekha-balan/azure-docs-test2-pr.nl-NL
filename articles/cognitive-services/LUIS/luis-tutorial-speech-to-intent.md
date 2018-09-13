---
title: Use Speech C# SDK with LUIS - Azure | Microsoft Docs
titleSuffix: Azure
description: Use the Speech C# SDK sample to speak into microphone and get LUIS intent and entities predictions returned.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 06/26/2018
ms.author: diberry
ms.openlocfilehash: aadca428fa076d697cc0f893673672850ddc27d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869509"
---
# <a name="integrate-speech-service"></a><span data-ttu-id="f2acf-103">Integrate Speech service</span><span class="sxs-lookup"><span data-stu-id="f2acf-103">Integrate Speech service</span></span>
<span data-ttu-id="f2acf-104">The [Speech service](https://docs.microsoft.com/azure/cognitive-services/Speech-Service/) allows you to use a single request to receive audio and return LUIS prediction JSON objects.</span><span class="sxs-lookup"><span data-stu-id="f2acf-104">The [Speech service](https://docs.microsoft.com/azure/cognitive-services/Speech-Service/) allows you to use a single request to receive audio and return LUIS prediction JSON objects.</span></span>

<span data-ttu-id="f2acf-105">In this article, you download and use a C# project in Visual Studio to speak an utterance into a microphone and receive LUIS prediction information.</span><span class="sxs-lookup"><span data-stu-id="f2acf-105">In this article, you download and use a C# project in Visual Studio to speak an utterance into a microphone and receive LUIS prediction information.</span></span> <span data-ttu-id="f2acf-106">The project uses the Speech [NuGet](https://www.nuget.org/packages/Microsoft.CognitiveServices.Speech/) package, already included as a reference.</span><span class="sxs-lookup"><span data-stu-id="f2acf-106">The project uses the Speech [NuGet](https://www.nuget.org/packages/Microsoft.CognitiveServices.Speech/) package, already included as a reference.</span></span> 

<span data-ttu-id="f2acf-107">For this article, you need a free [LUIS][LUIS] website account in order to import the application.</span><span class="sxs-lookup"><span data-stu-id="f2acf-107">For this article, you need a free [LUIS][LUIS] website account in order to import the application.</span></span>

## <a name="create-luis-endpoint-key"></a><span data-ttu-id="f2acf-108">Create LUIS endpoint key</span><span class="sxs-lookup"><span data-stu-id="f2acf-108">Create LUIS endpoint key</span></span>
<span data-ttu-id="f2acf-109">In the Azure portal, [create](luis-how-to-azure-subscription.md#create-luis-endpoint-key) a **Language Understanding** (LUIS) key.</span><span class="sxs-lookup"><span data-stu-id="f2acf-109">In the Azure portal, [create](luis-how-to-azure-subscription.md#create-luis-endpoint-key) a **Language Understanding** (LUIS) key.</span></span> 

## <a name="import-human-resources-luis-app"></a><span data-ttu-id="f2acf-110">Import Human Resources LUIS app</span><span class="sxs-lookup"><span data-stu-id="f2acf-110">Import Human Resources LUIS app</span></span>
<span data-ttu-id="f2acf-111">The intents, and utterances for this article are from the Human Resources LUIS app available from the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples) Github repository.</span><span class="sxs-lookup"><span data-stu-id="f2acf-111">The intents, and utterances for this article are from the Human Resources LUIS app available from the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples) Github repository.</span></span> <span data-ttu-id="f2acf-112">Download the [HumanResources.json](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/HumanResources.json) file, save it with the \*.json extension, and [import](luis-how-to-start-new-app.md#import-new-app) it into LUIS.</span><span class="sxs-lookup"><span data-stu-id="f2acf-112">Download the [HumanResources.json](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/HumanResources.json) file, save it with the \*.json extension, and [import](luis-how-to-start-new-app.md#import-new-app) it into LUIS.</span></span> 

<span data-ttu-id="f2acf-113">This app has intents, entities, and utterances related to the Human Resources domain.</span><span class="sxs-lookup"><span data-stu-id="f2acf-113">This app has intents, entities, and utterances related to the Human Resources domain.</span></span> <span data-ttu-id="f2acf-114">Example utterances include:</span><span class="sxs-lookup"><span data-stu-id="f2acf-114">Example utterances include:</span></span>

```
Who is John Smith's manager?
Who does John Smith manage?
Where is Form 123456?
Do I have any paid time off?
```

## <a name="add-keyphrase-prebuilt-entity"></a><span data-ttu-id="f2acf-115">Add KeyPhrase prebuilt entity</span><span class="sxs-lookup"><span data-stu-id="f2acf-115">Add KeyPhrase prebuilt entity</span></span>
<span data-ttu-id="f2acf-116">After importing the app, select **Entities**, then **Manage prebuilt entities**.</span><span class="sxs-lookup"><span data-stu-id="f2acf-116">After importing the app, select **Entities**, then **Manage prebuilt entities**.</span></span> <span data-ttu-id="f2acf-117">Add the **KeyPhrase** entity.</span><span class="sxs-lookup"><span data-stu-id="f2acf-117">Add the **KeyPhrase** entity.</span></span> <span data-ttu-id="f2acf-118">The KeyPhrase entity extracts key subject matter from the utterance.</span><span class="sxs-lookup"><span data-stu-id="f2acf-118">The KeyPhrase entity extracts key subject matter from the utterance.</span></span>

## <a name="train-and-publish-the-app"></a><span data-ttu-id="f2acf-119">Train and publish the app</span><span class="sxs-lookup"><span data-stu-id="f2acf-119">Train and publish the app</span></span>
1. <span data-ttu-id="f2acf-120">In the top, right navigation bar, select the **Train** button to train the LUIS app.</span><span class="sxs-lookup"><span data-stu-id="f2acf-120">In the top, right navigation bar, select the **Train** button to train the LUIS app.</span></span>

2. <span data-ttu-id="f2acf-121">Select **Publish** to go to the publish page.</span><span class="sxs-lookup"><span data-stu-id="f2acf-121">Select **Publish** to go to the publish page.</span></span> 

3. <span data-ttu-id="f2acf-122">At the bottom of the **Publish** page, add the LUIS key created in the [Create LUIS endpoint key](#create-luis-endpoint-key) section.</span><span class="sxs-lookup"><span data-stu-id="f2acf-122">At the bottom of the **Publish** page, add the LUIS key created in the [Create LUIS endpoint key](#create-luis-endpoint-key) section.</span></span>

4. <span data-ttu-id="f2acf-123">Publish the LUIS app by selecting the **Publish** button to the right of the Publish slot.</span><span class="sxs-lookup"><span data-stu-id="f2acf-123">Publish the LUIS app by selecting the **Publish** button to the right of the Publish slot.</span></span> 

  <span data-ttu-id="f2acf-124">On the **Publish** page, collect the app ID, publish region, and subscription ID of the LUIS key created in the  [Create LUIS endpoint key](#create-luis-endpoint-key) section.</span><span class="sxs-lookup"><span data-stu-id="f2acf-124">On the **Publish** page, collect the app ID, publish region, and subscription ID of the LUIS key created in the  [Create LUIS endpoint key](#create-luis-endpoint-key) section.</span></span> <span data-ttu-id="f2acf-125">You need to modify the code to use these values later in this article.</span><span class="sxs-lookup"><span data-stu-id="f2acf-125">You need to modify the code to use these values later in this article.</span></span> 

  <span data-ttu-id="f2acf-126">These values are all included in the endpoint URL at the bottom of the **Publish** page for the key you created.</span><span class="sxs-lookup"><span data-stu-id="f2acf-126">These values are all included in the endpoint URL at the bottom of the **Publish** page for the key you created.</span></span> 
  
  <span data-ttu-id="f2acf-127">Do **not** use the free starter key for this exercise.</span><span class="sxs-lookup"><span data-stu-id="f2acf-127">Do **not** use the free starter key for this exercise.</span></span> <span data-ttu-id="f2acf-128">Only a **Language Understanding** key created in the Azure portal will work for this exercise.</span><span class="sxs-lookup"><span data-stu-id="f2acf-128">Only a **Language Understanding** key created in the Azure portal will work for this exercise.</span></span> 

  <span data-ttu-id="f2acf-129">https://**REGION**.api.cognitive.microsoft.com/luis/v2.0/apps/**APPID**?subscription-key=**LUISKEY**&q=</span><span class="sxs-lookup"><span data-stu-id="f2acf-129">https://**REGION**.api.cognitive.microsoft.com/luis/v2.0/apps/**APPID**?subscription-key=**LUISKEY**&q=</span></span>

## <a name="audio-device"></a><span data-ttu-id="f2acf-130">Audio device</span><span class="sxs-lookup"><span data-stu-id="f2acf-130">Audio device</span></span>
<span data-ttu-id="f2acf-131">This article uses the audio device on your computer.</span><span class="sxs-lookup"><span data-stu-id="f2acf-131">This article uses the audio device on your computer.</span></span> <span data-ttu-id="f2acf-132">That can be a headset with microphone or a built-in audio device.</span><span class="sxs-lookup"><span data-stu-id="f2acf-132">That can be a headset with microphone or a built-in audio device.</span></span> <span data-ttu-id="f2acf-133">Check the audio input levels to see if you should speak louder than you normally would to have your speech detected by the audio device.</span><span class="sxs-lookup"><span data-stu-id="f2acf-133">Check the audio input levels to see if you should speak louder than you normally would to have your speech detected by the audio device.</span></span> 

## <a name="download-the-luis-sample-project"></a><span data-ttu-id="f2acf-134">Download the LUIS Sample project</span><span class="sxs-lookup"><span data-stu-id="f2acf-134">Download the LUIS Sample project</span></span>
 <span data-ttu-id="f2acf-135">Clone or download the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples) repository.</span><span class="sxs-lookup"><span data-stu-id="f2acf-135">Clone or download the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples) repository.</span></span> <span data-ttu-id="f2acf-136">Open the [Speech to intent project](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/tutorial-speech-intent-recognition) with Visual Studio and restore the NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="f2acf-136">Open the [Speech to intent project](https://github.com/Microsoft/LUIS-Samples/tree/master/documentation-samples/tutorial-speech-intent-recognition) with Visual Studio and restore the NuGet packages.</span></span> <span data-ttu-id="f2acf-137">The VS solution file is .\LUIS-Samples-master\documentation-samples\tutorial-speech-intent-recognition\csharp\csharp_samples.sln.</span><span class="sxs-lookup"><span data-stu-id="f2acf-137">The VS solution file is .\LUIS-Samples-master\documentation-samples\tutorial-speech-intent-recognition\csharp\csharp_samples.sln.</span></span>

<span data-ttu-id="f2acf-138">The Speech SDK is already included as a reference.</span><span class="sxs-lookup"><span data-stu-id="f2acf-138">The Speech SDK is already included as a reference.</span></span> 

<span data-ttu-id="f2acf-139">[![](./media/luis-tutorial-speech-to-intent/nuget-package.png "Screenshot of Visual Studio 2017 displaying Microsoft.CognitiveServices.Speech NuGet package")](./media/luis-tutorial-speech-to-intent/nuget-package.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="f2acf-139">[![](./media/luis-tutorial-speech-to-intent/nuget-package.png "Screenshot of Visual Studio 2017 displaying Microsoft.CognitiveServices.Speech NuGet package")](./media/luis-tutorial-speech-to-intent/nuget-package.png#lightbox)</span></span>

## <a name="modify-the-c-code"></a><span data-ttu-id="f2acf-140">Modify the C# code</span><span class="sxs-lookup"><span data-stu-id="f2acf-140">Modify the C# code</span></span>
<span data-ttu-id="f2acf-141">Open the **LUIS_samples.cs** file and change the following variables:</span><span class="sxs-lookup"><span data-stu-id="f2acf-141">Open the **LUIS_samples.cs** file and change the following variables:</span></span>

|<span data-ttu-id="f2acf-142">Variable name</span><span class="sxs-lookup"><span data-stu-id="f2acf-142">Variable name</span></span>|<span data-ttu-id="f2acf-143">Purpose</span><span class="sxs-lookup"><span data-stu-id="f2acf-143">Purpose</span></span>|
|--|--|
|<span data-ttu-id="f2acf-144">luisSubscriptionKey</span><span class="sxs-lookup"><span data-stu-id="f2acf-144">luisSubscriptionKey</span></span>|<span data-ttu-id="f2acf-145">Corresponds to endpoint URL's subscription-key value from Publish page</span><span class="sxs-lookup"><span data-stu-id="f2acf-145">Corresponds to endpoint URL's subscription-key value from Publish page</span></span>|
|<span data-ttu-id="f2acf-146">luisRegion</span><span class="sxs-lookup"><span data-stu-id="f2acf-146">luisRegion</span></span>|<span data-ttu-id="f2acf-147">Corresponds to endpoint URL's first subdomain</span><span class="sxs-lookup"><span data-stu-id="f2acf-147">Corresponds to endpoint URL's first subdomain</span></span>|
|<span data-ttu-id="f2acf-148">luisAppId</span><span class="sxs-lookup"><span data-stu-id="f2acf-148">luisAppId</span></span>|<span data-ttu-id="f2acf-149">Corresponds to endpoint URL's route following **apps/**</span><span class="sxs-lookup"><span data-stu-id="f2acf-149">Corresponds to endpoint URL's route following **apps/**</span></span>|

<span data-ttu-id="f2acf-150">[![](./media/luis-tutorial-speech-to-intent/change-variables.png "Screenshot of Visual Studio 2017 displaying LUIS_samples.cs variables")](./media/luis-tutorial-speech-to-intent/change-variables.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="f2acf-150">[![](./media/luis-tutorial-speech-to-intent/change-variables.png "Screenshot of Visual Studio 2017 displaying LUIS_samples.cs variables")](./media/luis-tutorial-speech-to-intent/change-variables.png#lightbox)</span></span>

<span data-ttu-id="f2acf-151">The file already has the Human Resources intents mapped.</span><span class="sxs-lookup"><span data-stu-id="f2acf-151">The file already has the Human Resources intents mapped.</span></span>

<span data-ttu-id="f2acf-152">[![](./media/luis-tutorial-speech-to-intent/intents.png "Screenshot of Visual Studio 2017 displaying LUIS_samples.cs intents")](./media/luis-tutorial-speech-to-intent/intents.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="f2acf-152">[![](./media/luis-tutorial-speech-to-intent/intents.png "Screenshot of Visual Studio 2017 displaying LUIS_samples.cs intents")](./media/luis-tutorial-speech-to-intent/intents.png#lightbox)</span></span>

<span data-ttu-id="f2acf-153">Build and run the app.</span><span class="sxs-lookup"><span data-stu-id="f2acf-153">Build and run the app.</span></span> 

## <a name="test-code-with-utterance"></a><span data-ttu-id="f2acf-154">Test code with utterance</span><span class="sxs-lookup"><span data-stu-id="f2acf-154">Test code with utterance</span></span>
<span data-ttu-id="f2acf-155">Select **1** and speak into the microphone "Who is the manager of John Smith".</span><span class="sxs-lookup"><span data-stu-id="f2acf-155">Select **1** and speak into the microphone "Who is the manager of John Smith".</span></span>

```cmd
1. Speech recognition of LUIS intent.
0. Stop.
Your choice: 1
LUIS...
Say something...
ResultId:cc83cebc9d6040d5956880bcdc5f5a98 Status:Recognized IntentId:<GetEmployeeOrgChart> Recognized text:<Who is the manager of John Smith?> Recognized Json:{"DisplayText":"Who is the manager of John Smith?","Duration":25700000,"Offset":9200000,"RecognitionStatus":"Success"}. LanguageUnderstandingJson:{
  "query": "Who is the manager of John Smith?",
  "topScoringIntent": {
    "intent": "GetEmployeeOrgChart",
    "score": 0.617331
  },
  "entities": [
    {
      "entity": "manager of john smith",
      "type": "builtin.keyPhrase",
      "startIndex": 11,
      "endIndex": 31
    }
  ]
}

Recognition done. Your Choice:

```

<span data-ttu-id="f2acf-156">The correct intent, **GetEmployeeOrgChart**, was found with a 61% confidence.</span><span class="sxs-lookup"><span data-stu-id="f2acf-156">The correct intent, **GetEmployeeOrgChart**, was found with a 61% confidence.</span></span> <span data-ttu-id="f2acf-157">The keyPhrase entity was returned.</span><span class="sxs-lookup"><span data-stu-id="f2acf-157">The keyPhrase entity was returned.</span></span> 

<span data-ttu-id="f2acf-158">The Speech SDK returns the entire LUIS response.</span><span class="sxs-lookup"><span data-stu-id="f2acf-158">The Speech SDK returns the entire LUIS response.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="f2acf-159">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f2acf-159">Clean up resources</span></span>
<span data-ttu-id="f2acf-160">When no longer needed, delete the LUIS HumanResources app.</span><span class="sxs-lookup"><span data-stu-id="f2acf-160">When no longer needed, delete the LUIS HumanResources app.</span></span> <span data-ttu-id="f2acf-161">To do so, select the ellipsis (***...***) button to the right of the app name in the app list, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f2acf-161">To do so, select the ellipsis (***...***) button to the right of the app name in the app list, select **Delete**.</span></span> <span data-ttu-id="f2acf-162">On the pop-up dialog **Delete app?**, select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="f2acf-162">On the pop-up dialog **Delete app?**, select **Ok**.</span></span>

<span data-ttu-id="f2acf-163">Remember to delete the LUIS-Samples directory when you are done using the sample code.</span><span class="sxs-lookup"><span data-stu-id="f2acf-163">Remember to delete the LUIS-Samples directory when you are done using the sample code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2acf-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2acf-164">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2acf-165">Integrate LUIS with a BOT</span><span class="sxs-lookup"><span data-stu-id="f2acf-165">Integrate LUIS with a BOT</span></span>](luis-csharp-tutorial-build-bot-framework-sample.md)

[LUIS]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-reference-regions#luis-website