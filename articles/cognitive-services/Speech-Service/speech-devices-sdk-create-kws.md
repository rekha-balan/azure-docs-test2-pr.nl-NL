---
title: Create a custom wake word
description: Learn how to create a custom wake word for the Speech Devices SDK.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 04/28/2018
ms.author: v-jerkin
ms.openlocfilehash: e1a74828213b595e6955a750904de7a3c2a5a865
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869513"
---
# <a name="create-a-custom-wake-word-by-using-the-speech-service"></a><span data-ttu-id="e1f92-103">Create a custom wake word by using the Speech service</span><span class="sxs-lookup"><span data-stu-id="e1f92-103">Create a custom wake word by using the Speech service</span></span>

<span data-ttu-id="e1f92-104">Your device is always listening for a wake word (or phrase).</span><span class="sxs-lookup"><span data-stu-id="e1f92-104">Your device is always listening for a wake word (or phrase).</span></span> <span data-ttu-id="e1f92-105">For example, "Hey Cortana" is a wake word for the Cortana assistant.</span><span class="sxs-lookup"><span data-stu-id="e1f92-105">For example, "Hey Cortana" is a wake word for the Cortana assistant.</span></span> <span data-ttu-id="e1f92-106">When the user says the wake word, the device sends all subsequent audio to the cloud, until the user stops speaking.</span><span class="sxs-lookup"><span data-stu-id="e1f92-106">When the user says the wake word, the device sends all subsequent audio to the cloud, until the user stops speaking.</span></span> <span data-ttu-id="e1f92-107">Customizing your wake word is an effective way to differentiate your device and strengthen your branding.</span><span class="sxs-lookup"><span data-stu-id="e1f92-107">Customizing your wake word is an effective way to differentiate your device and strengthen your branding.</span></span>

<span data-ttu-id="e1f92-108">In this article, you learn how to create a custom wake word for your device.</span><span class="sxs-lookup"><span data-stu-id="e1f92-108">In this article, you learn how to create a custom wake word for your device.</span></span>

## <a name="choose-an-effective-wake-word"></a><span data-ttu-id="e1f92-109">Choose an effective wake word</span><span class="sxs-lookup"><span data-stu-id="e1f92-109">Choose an effective wake word</span></span>

<span data-ttu-id="e1f92-110">Consider the following guidelines when you choose a wake word:</span><span class="sxs-lookup"><span data-stu-id="e1f92-110">Consider the following guidelines when you choose a wake word:</span></span>

* <span data-ttu-id="e1f92-111">Your wake word should be an English word or a phrase.</span><span class="sxs-lookup"><span data-stu-id="e1f92-111">Your wake word should be an English word or a phrase.</span></span> <span data-ttu-id="e1f92-112">It should take no longer than two seconds to say.</span><span class="sxs-lookup"><span data-stu-id="e1f92-112">It should take no longer than two seconds to say.</span></span>

* <span data-ttu-id="e1f92-113">Words of 4 to 7 syllables work best.</span><span class="sxs-lookup"><span data-stu-id="e1f92-113">Words of 4 to 7 syllables work best.</span></span> <span data-ttu-id="e1f92-114">For example, "Hey, Computer" is a good wake word.</span><span class="sxs-lookup"><span data-stu-id="e1f92-114">For example, "Hey, Computer" is a good wake word.</span></span> <span data-ttu-id="e1f92-115">Just "Hey" is a poor one.</span><span class="sxs-lookup"><span data-stu-id="e1f92-115">Just "Hey" is a poor one.</span></span>

* <span data-ttu-id="e1f92-116">Wake words should follow common English pronunciation rules.</span><span class="sxs-lookup"><span data-stu-id="e1f92-116">Wake words should follow common English pronunciation rules.</span></span>

* <span data-ttu-id="e1f92-117">A unique or even a made-up word that follows common English pronunciation rules might reduce false positives.</span><span class="sxs-lookup"><span data-stu-id="e1f92-117">A unique or even a made-up word that follows common English pronunciation rules might reduce false positives.</span></span> <span data-ttu-id="e1f92-118">For example, "computerama" might be a good wake word.</span><span class="sxs-lookup"><span data-stu-id="e1f92-118">For example, "computerama" might be a good wake word.</span></span>

* <span data-ttu-id="e1f92-119">Do not choose a common word.</span><span class="sxs-lookup"><span data-stu-id="e1f92-119">Do not choose a common word.</span></span> <span data-ttu-id="e1f92-120">For example, "eat" and "go" are words that people say frequently in ordinary conversation.</span><span class="sxs-lookup"><span data-stu-id="e1f92-120">For example, "eat" and "go" are words that people say frequently in ordinary conversation.</span></span> <span data-ttu-id="e1f92-121">They might be false triggers for your device.</span><span class="sxs-lookup"><span data-stu-id="e1f92-121">They might be false triggers for your device.</span></span>

* <span data-ttu-id="e1f92-122">Avoid using a wake word that might have alternative pronunciations.</span><span class="sxs-lookup"><span data-stu-id="e1f92-122">Avoid using a wake word that might have alternative pronunciations.</span></span> <span data-ttu-id="e1f92-123">Users would have to know the "right" pronunciation to get their device to respond.</span><span class="sxs-lookup"><span data-stu-id="e1f92-123">Users would have to know the "right" pronunciation to get their device to respond.</span></span> <span data-ttu-id="e1f92-124">For example, "509" can be pronounced "five zero nine," "five oh nine," or "five hundred and nine."</span><span class="sxs-lookup"><span data-stu-id="e1f92-124">For example, "509" can be pronounced "five zero nine," "five oh nine," or "five hundred and nine."</span></span> <span data-ttu-id="e1f92-125">"R.E.I."</span><span class="sxs-lookup"><span data-stu-id="e1f92-125">"R.E.I."</span></span> <span data-ttu-id="e1f92-126">can be pronounced "r-e-i" or "ray."</span><span class="sxs-lookup"><span data-stu-id="e1f92-126">can be pronounced "r-e-i" or "ray."</span></span> <span data-ttu-id="e1f92-127">"Live" can be pronounced "/līv/" or "/liv/".</span><span class="sxs-lookup"><span data-stu-id="e1f92-127">"Live" can be pronounced "/līv/" or "/liv/".</span></span>

* <span data-ttu-id="e1f92-128">Do not use special characters, symbols, or digits.</span><span class="sxs-lookup"><span data-stu-id="e1f92-128">Do not use special characters, symbols, or digits.</span></span> <span data-ttu-id="e1f92-129">For example, "Go#" and "20 + cats" would not be good wake words.</span><span class="sxs-lookup"><span data-stu-id="e1f92-129">For example, "Go#" and "20 + cats" would not be good wake words.</span></span> <span data-ttu-id="e1f92-130">However, "go sharp" or "twenty plus cats" might work.</span><span class="sxs-lookup"><span data-stu-id="e1f92-130">However, "go sharp" or "twenty plus cats" might work.</span></span> <span data-ttu-id="e1f92-131">You can still use the symbols in your branding and use marketing and documentation to reinforce the proper pronunciation.</span><span class="sxs-lookup"><span data-stu-id="e1f92-131">You can still use the symbols in your branding and use marketing and documentation to reinforce the proper pronunciation.</span></span>

> [!NOTE]
> <span data-ttu-id="e1f92-132">If you choose a trademarked word as your wake word, be sure that you own that trademark or that you have permission from the trademark owner to use the word.</span><span class="sxs-lookup"><span data-stu-id="e1f92-132">If you choose a trademarked word as your wake word, be sure that you own that trademark or that you have permission from the trademark owner to use the word.</span></span> <span data-ttu-id="e1f92-133">Microsoft is not liable for any legal issues that might arise from your choice of wake word.</span><span class="sxs-lookup"><span data-stu-id="e1f92-133">Microsoft is not liable for any legal issues that might arise from your choice of wake word.</span></span>

## <a name="create-your-wake-word"></a><span data-ttu-id="e1f92-134">Create your wake word</span><span class="sxs-lookup"><span data-stu-id="e1f92-134">Create your wake word</span></span>

<span data-ttu-id="e1f92-135">Before you can use a custom wake word with your device, you must create the wake word by using the Microsoft Custom Wake Word Generation service.</span><span class="sxs-lookup"><span data-stu-id="e1f92-135">Before you can use a custom wake word with your device, you must create the wake word by using the Microsoft Custom Wake Word Generation service.</span></span> <span data-ttu-id="e1f92-136">After you provide a wake word, the service produces a file that you deploy to your development kit to enable your wake word on your device.</span><span class="sxs-lookup"><span data-stu-id="e1f92-136">After you provide a wake word, the service produces a file that you deploy to your development kit to enable your wake word on your device.</span></span>

1. <span data-ttu-id="e1f92-137">Go to the [Custom Speech service portal](https://cris.ai/).</span><span class="sxs-lookup"><span data-stu-id="e1f92-137">Go to the [Custom Speech service portal](https://cris.ai/).</span></span>

2. <span data-ttu-id="e1f92-138">Create a new account with the email address at which you received the invitation for Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1f92-138">Create a new account with the email address at which you received the invitation for Azure Active Directory.</span></span> 

    ![Create a new account](media/speech-devices-sdk/wake-word-1.png)
 
3.  <span data-ttu-id="e1f92-140">After you sign in, fill out the form, and then select **Start my journey**.</span><span class="sxs-lookup"><span data-stu-id="e1f92-140">After you sign in, fill out the form, and then select **Start my journey**.</span></span>

    ![Successfully signed in](media/speech-devices-sdk/wake-word-3.png)
 
4. <span data-ttu-id="e1f92-142">The **Custom Wake Word** page is not available to the public, so there is no link that takes you there.</span><span class="sxs-lookup"><span data-stu-id="e1f92-142">The **Custom Wake Word** page is not available to the public, so there is no link that takes you there.</span></span> <span data-ttu-id="e1f92-143">Select or paste in this link instead: https://cris.ai/customkws.</span><span class="sxs-lookup"><span data-stu-id="e1f92-143">Select or paste in this link instead: https://cris.ai/customkws.</span></span>

    ![The Custom Wake Word page is hidden](media/speech-devices-sdk/wake-word-4.png)
 
6. <span data-ttu-id="e1f92-145">Type in the wake word of your choice, and then select **Submit the word**.</span><span class="sxs-lookup"><span data-stu-id="e1f92-145">Type in the wake word of your choice, and then select **Submit the word**.</span></span>

    ![Enter your wake word](media/speech-devices-sdk/wake-word-5.png)
 
7. <span data-ttu-id="e1f92-147">It might take a few minutes for the files to be generated.</span><span class="sxs-lookup"><span data-stu-id="e1f92-147">It might take a few minutes for the files to be generated.</span></span> <span data-ttu-id="e1f92-148">You should see a spinning circle in your browser window.</span><span class="sxs-lookup"><span data-stu-id="e1f92-148">You should see a spinning circle in your browser window.</span></span> <span data-ttu-id="e1f92-149">After a moment, an information bar appears, asking you to download a .zip file.</span><span class="sxs-lookup"><span data-stu-id="e1f92-149">After a moment, an information bar appears, asking you to download a .zip file.</span></span>

    ![Receiving the .zip file](media/speech-devices-sdk/wake-word-6.png)

8. <span data-ttu-id="e1f92-151">Save the .zip file to your computer.</span><span class="sxs-lookup"><span data-stu-id="e1f92-151">Save the .zip file to your computer.</span></span> <span data-ttu-id="e1f92-152">You need this file to deploy the custom wake word to the development kit.</span><span class="sxs-lookup"><span data-stu-id="e1f92-152">You need this file to deploy the custom wake word to the development kit.</span></span> <span data-ttu-id="e1f92-153">To deploy the custom wake word, follow the instructions in [Get started with the Speech Devices SDK](speech-devices-sdk-qsg.md).</span><span class="sxs-lookup"><span data-stu-id="e1f92-153">To deploy the custom wake word, follow the instructions in [Get started with the Speech Devices SDK](speech-devices-sdk-qsg.md).</span></span>

9. <span data-ttu-id="e1f92-154">Select **Sign out.**</span><span class="sxs-lookup"><span data-stu-id="e1f92-154">Select **Sign out.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1f92-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1f92-155">Next steps</span></span>

<span data-ttu-id="e1f92-156">To get started, get a [free Azure account](https://azure.microsoft.com/free/) and sign up for the Speech Devices SDK.</span><span class="sxs-lookup"><span data-stu-id="e1f92-156">To get started, get a [free Azure account](https://azure.microsoft.com/free/) and sign up for the Speech Devices SDK.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1f92-157">Sign up for the Speech Devices SDK</span><span class="sxs-lookup"><span data-stu-id="e1f92-157">Sign up for the Speech Devices SDK</span></span>](get-speech-devices-sdk.md)

