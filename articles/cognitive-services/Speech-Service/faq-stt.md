---
title: Frequently asked questions about the Speech to Text service in Azure
description: Get answers to the most popular questions about the Speech to Text service.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: PanosPeriorellis
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 06/11/2018
ms.author: panosper
ms.openlocfilehash: 31515d6867fc5524df1b081932dd2a28b0cf989c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868578"
---
# <a name="speech-to-text-frequently-asked-questions"></a><span data-ttu-id="ff1de-103">Speech to Text frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="ff1de-103">Speech to Text frequently asked questions</span></span>

<span data-ttu-id="ff1de-104">If you can't find answers to your questions in this FAQ, check out [other support options](support.md).</span><span class="sxs-lookup"><span data-stu-id="ff1de-104">If you can't find answers to your questions in this FAQ, check out [other support options](support.md).</span></span>

## <a name="general"></a><span data-ttu-id="ff1de-105">General</span><span class="sxs-lookup"><span data-stu-id="ff1de-105">General</span></span>

<span data-ttu-id="ff1de-106">**Q: What is the difference between a baseline model and a custom Speech to Text model?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-106">**Q: What is the difference between a baseline model and a custom Speech to Text model?**</span></span>

<span data-ttu-id="ff1de-107">**A**: A baseline model has been trained by using Microsoft-owned data and is already deployed in the cloud.</span><span class="sxs-lookup"><span data-stu-id="ff1de-107">**A**: A baseline model has been trained by using Microsoft-owned data and is already deployed in the cloud.</span></span>  <span data-ttu-id="ff1de-108">You can use a custom model to adapt a model to better fit a specific environment that has specific ambient noise or language.</span><span class="sxs-lookup"><span data-stu-id="ff1de-108">You can use a custom model to adapt a model to better fit a specific environment that has specific ambient noise or language.</span></span> <span data-ttu-id="ff1de-109">Factory floors, cars, or noisy streets would require an adapted acoustic model.</span><span class="sxs-lookup"><span data-stu-id="ff1de-109">Factory floors, cars, or noisy streets would require an adapted acoustic model.</span></span> <span data-ttu-id="ff1de-110">Topics like biology, physics, radiology, product names, and custom acronyms would require an adapted language model.</span><span class="sxs-lookup"><span data-stu-id="ff1de-110">Topics like biology, physics, radiology, product names, and custom acronyms would require an adapted language model.</span></span>

<span data-ttu-id="ff1de-111">**Q: Where do I start if I want to use a baseline model?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-111">**Q: Where do I start if I want to use a baseline model?**</span></span>

<span data-ttu-id="ff1de-112">**A**: First, get a [subscription key](get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ff1de-112">**A**: First, get a [subscription key](get-started.md).</span></span> <span data-ttu-id="ff1de-113">If you want to make REST calls to the predeployed baseline models, see the [REST APIs](rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="ff1de-113">If you want to make REST calls to the predeployed baseline models, see the [REST APIs](rest-apis.md).</span></span> <span data-ttu-id="ff1de-114">If you want to use WebSockets, [download the SDK](speech-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ff1de-114">If you want to use WebSockets, [download the SDK](speech-sdk.md).</span></span>

<span data-ttu-id="ff1de-115">**Q: Do I always need to build a custom speech model?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-115">**Q: Do I always need to build a custom speech model?**</span></span>

<span data-ttu-id="ff1de-116">**A**: No.</span><span class="sxs-lookup"><span data-stu-id="ff1de-116">**A**: No.</span></span> <span data-ttu-id="ff1de-117">If your application uses generic, day-to-day language, you don't need to customize a model.</span><span class="sxs-lookup"><span data-stu-id="ff1de-117">If your application uses generic, day-to-day language, you don't need to customize a model.</span></span> <span data-ttu-id="ff1de-118">If your application is used in an environment where there's little or no background noise, you don't need to customize a model.</span><span class="sxs-lookup"><span data-stu-id="ff1de-118">If your application is used in an environment where there's little or no background noise, you don't need to customize a model.</span></span> 

<span data-ttu-id="ff1de-119">You can deploy baseline and customized models in the portal and then run accuracy tests against them.</span><span class="sxs-lookup"><span data-stu-id="ff1de-119">You can deploy baseline and customized models in the portal and then run accuracy tests against them.</span></span> <span data-ttu-id="ff1de-120">You can use this feature to measure the accuracy of a baseline model versus a custom model.</span><span class="sxs-lookup"><span data-stu-id="ff1de-120">You can use this feature to measure the accuracy of a baseline model versus a custom model.</span></span>

<span data-ttu-id="ff1de-121">**Q: How will I know when processing for my dataset or model is complete?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-121">**Q: How will I know when processing for my dataset or model is complete?**</span></span>

<span data-ttu-id="ff1de-122">**A**: Currently, the status of the model or dataset in the table is the only way to know.</span><span class="sxs-lookup"><span data-stu-id="ff1de-122">**A**: Currently, the status of the model or dataset in the table is the only way to know.</span></span> <span data-ttu-id="ff1de-123">When the processing is complete, the status is **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="ff1de-123">When the processing is complete, the status is **Succeeded**.</span></span>

<span data-ttu-id="ff1de-124">**Q: Can I create more than one model?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-124">**Q: Can I create more than one model?**</span></span>

<span data-ttu-id="ff1de-125">**A**: There's no limit on the number of models you can have in your collection.</span><span class="sxs-lookup"><span data-stu-id="ff1de-125">**A**: There's no limit on the number of models you can have in your collection.</span></span>

<span data-ttu-id="ff1de-126">**Q: I realized I made a mistake. How do I cancel my data import or model creation that’s in progress?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-126">**Q: I realized I made a mistake. How do I cancel my data import or model creation that’s in progress?**</span></span>

<span data-ttu-id="ff1de-127">**A**: Currently, you can't roll back an acoustic or language adaptation process.</span><span class="sxs-lookup"><span data-stu-id="ff1de-127">**A**: Currently, you can't roll back an acoustic or language adaptation process.</span></span> <span data-ttu-id="ff1de-128">You can delete imported data and models when they're in a terminal state.</span><span class="sxs-lookup"><span data-stu-id="ff1de-128">You can delete imported data and models when they're in a terminal state.</span></span>

<span data-ttu-id="ff1de-129">**Q: What's the difference between the Search and Dictation model and the Conversational model?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-129">**Q: What's the difference between the Search and Dictation model and the Conversational model?**</span></span>

<span data-ttu-id="ff1de-130">**A**: You can choose from more than one baseline model in the Speech service.</span><span class="sxs-lookup"><span data-stu-id="ff1de-130">**A**: You can choose from more than one baseline model in the Speech service.</span></span> <span data-ttu-id="ff1de-131">The Conversational model is useful for recognizing speech that is spoken in a conversational style.</span><span class="sxs-lookup"><span data-stu-id="ff1de-131">The Conversational model is useful for recognizing speech that is spoken in a conversational style.</span></span> <span data-ttu-id="ff1de-132">This model is ideal for transcribing phone calls.</span><span class="sxs-lookup"><span data-stu-id="ff1de-132">This model is ideal for transcribing phone calls.</span></span> <span data-ttu-id="ff1de-133">The Search and Dictation model is ideal for voice-triggered apps.</span><span class="sxs-lookup"><span data-stu-id="ff1de-133">The Search and Dictation model is ideal for voice-triggered apps.</span></span> <span data-ttu-id="ff1de-134">The Universal model is a new model that aims to address both scenarios.</span><span class="sxs-lookup"><span data-stu-id="ff1de-134">The Universal model is a new model that aims to address both scenarios.</span></span>

<span data-ttu-id="ff1de-135">**Q: Can I update my existing model (model stacking)?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-135">**Q: Can I update my existing model (model stacking)?**</span></span>

<span data-ttu-id="ff1de-136">**A**: You can't update an existing model.</span><span class="sxs-lookup"><span data-stu-id="ff1de-136">**A**: You can't update an existing model.</span></span> <span data-ttu-id="ff1de-137">As a solution, combine the old dataset with the new dataset and readapt.</span><span class="sxs-lookup"><span data-stu-id="ff1de-137">As a solution, combine the old dataset with the new dataset and readapt.</span></span>

<span data-ttu-id="ff1de-138">The old dataset and the new dataset must be combined in a single .zip file (for acoustic data) or in a .txt file (for language data).</span><span class="sxs-lookup"><span data-stu-id="ff1de-138">The old dataset and the new dataset must be combined in a single .zip file (for acoustic data) or in a .txt file (for language data).</span></span> <span data-ttu-id="ff1de-139">When adaptation is finished, the new, updated model needs to be redeployed to obtain a new endpoint</span><span class="sxs-lookup"><span data-stu-id="ff1de-139">When adaptation is finished, the new, updated model needs to be redeployed to obtain a new endpoint</span></span>

<span data-ttu-id="ff1de-140">**Q: What if I need higher concurrency for my deployed model than what is offered in the portal?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-140">**Q: What if I need higher concurrency for my deployed model than what is offered in the portal?**</span></span> 

<span data-ttu-id="ff1de-141">**A**: You can scale up your model in increments of 20 concurrent requests.</span><span class="sxs-lookup"><span data-stu-id="ff1de-141">**A**: You can scale up your model in increments of 20 concurrent requests.</span></span> 

<span data-ttu-id="ff1de-142">Contact us if you require a higher scale.</span><span class="sxs-lookup"><span data-stu-id="ff1de-142">Contact us if you require a higher scale.</span></span>

<span data-ttu-id="ff1de-143">**Q: Can I download my model and run it locally?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-143">**Q: Can I download my model and run it locally?**</span></span>

<span data-ttu-id="ff1de-144">**A**: Models can't be downloaded and executed locally.</span><span class="sxs-lookup"><span data-stu-id="ff1de-144">**A**: Models can't be downloaded and executed locally.</span></span>

<span data-ttu-id="ff1de-145">**Q: Are my requests logged?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-145">**Q: Are my requests logged?**</span></span>

<span data-ttu-id="ff1de-146">**A**: You have a choice when you create a deployment to switch off tracing.</span><span class="sxs-lookup"><span data-stu-id="ff1de-146">**A**: You have a choice when you create a deployment to switch off tracing.</span></span> <span data-ttu-id="ff1de-147">At that point, no audio or transcriptions will be logged.</span><span class="sxs-lookup"><span data-stu-id="ff1de-147">At that point, no audio or transcriptions will be logged.</span></span> <span data-ttu-id="ff1de-148">Otherwise, requests are typically logged in Azure in secure storage.</span><span class="sxs-lookup"><span data-stu-id="ff1de-148">Otherwise, requests are typically logged in Azure in secure storage.</span></span> 

<span data-ttu-id="ff1de-149">If you have further privacy concerns that prohibit you from using the custom Speech service, contact one of the support channels.</span><span class="sxs-lookup"><span data-stu-id="ff1de-149">If you have further privacy concerns that prohibit you from using the custom Speech service, contact one of the support channels.</span></span>

## <a name="importing-data"></a><span data-ttu-id="ff1de-150">Importing data</span><span class="sxs-lookup"><span data-stu-id="ff1de-150">Importing data</span></span>

<span data-ttu-id="ff1de-151">**Q: What is the limit on the size of a dataset, and why is it the limit?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-151">**Q: What is the limit on the size of a dataset, and why is it the limit?**</span></span>

<span data-ttu-id="ff1de-152">**A**: The current limit for a dataset is 2 GB.</span><span class="sxs-lookup"><span data-stu-id="ff1de-152">**A**: The current limit for a dataset is 2 GB.</span></span> <span data-ttu-id="ff1de-153">The limit is due to the restriction on the size of a file for HTTP upload.</span><span class="sxs-lookup"><span data-stu-id="ff1de-153">The limit is due to the restriction on the size of a file for HTTP upload.</span></span> 

<span data-ttu-id="ff1de-154">**Q: Can I zip my text files so I can upload a larger text file?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-154">**Q: Can I zip my text files so I can upload a larger text file?**</span></span> 

<span data-ttu-id="ff1de-155">**A**: No.</span><span class="sxs-lookup"><span data-stu-id="ff1de-155">**A**: No.</span></span> <span data-ttu-id="ff1de-156">Currently, only uncompressed text files are allowed.</span><span class="sxs-lookup"><span data-stu-id="ff1de-156">Currently, only uncompressed text files are allowed.</span></span>

<span data-ttu-id="ff1de-157">**Q: The data report says there were failed utterances. What is the issue?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-157">**Q: The data report says there were failed utterances. What is the issue?**</span></span>

<span data-ttu-id="ff1de-158">**A**: Failing to upload 100 percent of the utterances in a file is not a problem.</span><span class="sxs-lookup"><span data-stu-id="ff1de-158">**A**: Failing to upload 100 percent of the utterances in a file is not a problem.</span></span> <span data-ttu-id="ff1de-159">If the vast majority of the utterances in an acoustic or language dataset (for example, more than 95 percent) are successfully imported, the dataset can be usable.</span><span class="sxs-lookup"><span data-stu-id="ff1de-159">If the vast majority of the utterances in an acoustic or language dataset (for example, more than 95 percent) are successfully imported, the dataset can be usable.</span></span> <span data-ttu-id="ff1de-160">However, we recommend that you try to understand why the utterances failed and fix the problems.</span><span class="sxs-lookup"><span data-stu-id="ff1de-160">However, we recommend that you try to understand why the utterances failed and fix the problems.</span></span> <span data-ttu-id="ff1de-161">Most common problems, such as formatting errors, are easy to fix.</span><span class="sxs-lookup"><span data-stu-id="ff1de-161">Most common problems, such as formatting errors, are easy to fix.</span></span> 

## <a name="creating-an-acoustic-model"></a><span data-ttu-id="ff1de-162">Creating an acoustic model</span><span class="sxs-lookup"><span data-stu-id="ff1de-162">Creating an acoustic model</span></span>

<span data-ttu-id="ff1de-163">**Q: How much acoustic data do I need?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-163">**Q: How much acoustic data do I need?**</span></span>

<span data-ttu-id="ff1de-164">**A**: We recommend starting with between 30 minutes and one hour of acoustic data.</span><span class="sxs-lookup"><span data-stu-id="ff1de-164">**A**: We recommend starting with between 30 minutes and one hour of acoustic data.</span></span>

<span data-ttu-id="ff1de-165">**Q: What data should I collect?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-165">**Q: What data should I collect?**</span></span>

<span data-ttu-id="ff1de-166">**A**: Collect data that's as close to the application scenario and use case as possible.</span><span class="sxs-lookup"><span data-stu-id="ff1de-166">**A**: Collect data that's as close to the application scenario and use case as possible.</span></span> <span data-ttu-id="ff1de-167">The data collection should match the target application and users in terms of device or devices, environments, and types of speakers.</span><span class="sxs-lookup"><span data-stu-id="ff1de-167">The data collection should match the target application and users in terms of device or devices, environments, and types of speakers.</span></span> <span data-ttu-id="ff1de-168">In general, you should collect data from as broad a range of speakers as possible.</span><span class="sxs-lookup"><span data-stu-id="ff1de-168">In general, you should collect data from as broad a range of speakers as possible.</span></span> 

<span data-ttu-id="ff1de-169">**Q: How should I collect acoustic data?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-169">**Q: How should I collect acoustic data?**</span></span>

<span data-ttu-id="ff1de-170">**A**: You can create a standalone data collection application or use off-the-shelf audio recording software.</span><span class="sxs-lookup"><span data-stu-id="ff1de-170">**A**: You can create a standalone data collection application or use off-the-shelf audio recording software.</span></span> <span data-ttu-id="ff1de-171">You can also create a version of your application that logs the audio data and then uses the data.</span><span class="sxs-lookup"><span data-stu-id="ff1de-171">You can also create a version of your application that logs the audio data and then uses the data.</span></span> 

<span data-ttu-id="ff1de-172">**Q: Do I need to transcribe adaptation data myself?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-172">**Q: Do I need to transcribe adaptation data myself?**</span></span>

<span data-ttu-id="ff1de-173">**A**: Yes!</span><span class="sxs-lookup"><span data-stu-id="ff1de-173">**A**: Yes!</span></span> <span data-ttu-id="ff1de-174">You can transcribe it yourself or use a professional transcription service.</span><span class="sxs-lookup"><span data-stu-id="ff1de-174">You can transcribe it yourself or use a professional transcription service.</span></span> <span data-ttu-id="ff1de-175">Some users prefer professional transcribers and others use crowdsourcing or do the transcriptions themselves.</span><span class="sxs-lookup"><span data-stu-id="ff1de-175">Some users prefer professional transcribers and others use crowdsourcing or do the transcriptions themselves.</span></span>

## <a name="accuracy-testing"></a><span data-ttu-id="ff1de-176">Accuracy testing</span><span class="sxs-lookup"><span data-stu-id="ff1de-176">Accuracy testing</span></span>

<span data-ttu-id="ff1de-177">**Q: Can I perform offline testing of my custom acoustic model by using a custom language model?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-177">**Q: Can I perform offline testing of my custom acoustic model by using a custom language model?**</span></span>

<span data-ttu-id="ff1de-178">**A**: Yes, just select the custom language model in the drop-down menu when you set up the offline test.</span><span class="sxs-lookup"><span data-stu-id="ff1de-178">**A**: Yes, just select the custom language model in the drop-down menu when you set up the offline test.</span></span>

<span data-ttu-id="ff1de-179">**Q: Can I perform offline testing of my custom language model by using a custom acoustic model?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-179">**Q: Can I perform offline testing of my custom language model by using a custom acoustic model?**</span></span>

<span data-ttu-id="ff1de-180">**A**: Yes, just select the custom acoustic model in the drop-down menu when you set up the offline test.</span><span class="sxs-lookup"><span data-stu-id="ff1de-180">**A**: Yes, just select the custom acoustic model in the drop-down menu when you set up the offline test.</span></span>

<span data-ttu-id="ff1de-181">**Q: What is word error rate (WER) and how is it computed?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-181">**Q: What is word error rate (WER) and how is it computed?**</span></span>

<span data-ttu-id="ff1de-182">**A**: WER is the evaluation metric for speech recognition.</span><span class="sxs-lookup"><span data-stu-id="ff1de-182">**A**: WER is the evaluation metric for speech recognition.</span></span> <span data-ttu-id="ff1de-183">WER is counted as the total number of errors, which includes insertions, deletions, and substitutions, divided by the total number of words in the reference transcription.</span><span class="sxs-lookup"><span data-stu-id="ff1de-183">WER is counted as the total number of errors, which includes insertions, deletions, and substitutions, divided by the total number of words in the reference transcription.</span></span> <span data-ttu-id="ff1de-184">For more information, see [word error rate](https://en.wikipedia.org/wiki/Word_error_rate).</span><span class="sxs-lookup"><span data-stu-id="ff1de-184">For more information, see [word error rate](https://en.wikipedia.org/wiki/Word_error_rate).</span></span>

<span data-ttu-id="ff1de-185">**Q: How do I determine whether the results of an accuracy test are good?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-185">**Q: How do I determine whether the results of an accuracy test are good?**</span></span>

<span data-ttu-id="ff1de-186">**A**: The results show a comparison between the baseline model and the model you customized.</span><span class="sxs-lookup"><span data-stu-id="ff1de-186">**A**: The results show a comparison between the baseline model and the model you customized.</span></span> <span data-ttu-id="ff1de-187">You should aim to beat the baseline model to make customization worthwhile.</span><span class="sxs-lookup"><span data-stu-id="ff1de-187">You should aim to beat the baseline model to make customization worthwhile.</span></span>

<span data-ttu-id="ff1de-188">**Q: How do I determine the WER of a base model so I can see if there was an improvement?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-188">**Q: How do I determine the WER of a base model so I can see if there was an improvement?**</span></span> 

<span data-ttu-id="ff1de-189">**A**: The offline test results show the baseline accuracy of the custom model and the improvement over baseline.</span><span class="sxs-lookup"><span data-stu-id="ff1de-189">**A**: The offline test results show the baseline accuracy of the custom model and the improvement over baseline.</span></span>

## <a name="creating-a-language-model"></a><span data-ttu-id="ff1de-190">Creating a language model</span><span class="sxs-lookup"><span data-stu-id="ff1de-190">Creating a language model</span></span>

<span data-ttu-id="ff1de-191">**Q: How much text data do I need to upload?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-191">**Q: How much text data do I need to upload?**</span></span>

<span data-ttu-id="ff1de-192">**A**: It depends on how different the vocabulary and phrases used in your application are from the starting language models.</span><span class="sxs-lookup"><span data-stu-id="ff1de-192">**A**: It depends on how different the vocabulary and phrases used in your application are from the starting language models.</span></span> <span data-ttu-id="ff1de-193">For all new words, it's useful to provide as many examples as possible of the usage of those words.</span><span class="sxs-lookup"><span data-stu-id="ff1de-193">For all new words, it's useful to provide as many examples as possible of the usage of those words.</span></span> <span data-ttu-id="ff1de-194">For common phrases that are used in your application, including phrases in the language data is also useful because it tells the system to also listen for these terms.</span><span class="sxs-lookup"><span data-stu-id="ff1de-194">For common phrases that are used in your application, including phrases in the language data is also useful because it tells the system to also listen for these terms.</span></span> <span data-ttu-id="ff1de-195">It's common to have at least 100, and typically several hundred or more utterances in the language dataset.</span><span class="sxs-lookup"><span data-stu-id="ff1de-195">It's common to have at least 100, and typically several hundred or more utterances in the language dataset.</span></span> <span data-ttu-id="ff1de-196">Also, if some types of queries are expected to be more common than others, you can insert multiple copies of the common queries in the dataset.</span><span class="sxs-lookup"><span data-stu-id="ff1de-196">Also, if some types of queries are expected to be more common than others, you can insert multiple copies of the common queries in the dataset.</span></span>

<span data-ttu-id="ff1de-197">**Q: Can I just upload a list of words?**</span><span class="sxs-lookup"><span data-stu-id="ff1de-197">**Q: Can I just upload a list of words?**</span></span>

<span data-ttu-id="ff1de-198">**A**: Uploading a list of words will add the words to the vocabulary, but it won't teach the system how the words are typically used.</span><span class="sxs-lookup"><span data-stu-id="ff1de-198">**A**: Uploading a list of words will add the words to the vocabulary, but it won't teach the system how the words are typically used.</span></span> <span data-ttu-id="ff1de-199">By providing full or partial utterances (sentences or phrases of things that users are likely to say), the language model can learn the new words and how they are used.</span><span class="sxs-lookup"><span data-stu-id="ff1de-199">By providing full or partial utterances (sentences or phrases of things that users are likely to say), the language model can learn the new words and how they are used.</span></span> <span data-ttu-id="ff1de-200">The custom language model is good not only for adding new words to the system, but also for adjusting the likelihood of known words for your application.</span><span class="sxs-lookup"><span data-stu-id="ff1de-200">The custom language model is good not only for adding new words to the system, but also for adjusting the likelihood of known words for your application.</span></span> <span data-ttu-id="ff1de-201">Providing full utterances helps the system learn better.</span><span class="sxs-lookup"><span data-stu-id="ff1de-201">Providing full utterances helps the system learn better.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ff1de-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff1de-202">Next steps</span></span>

* [<span data-ttu-id="ff1de-203">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="ff1de-203">Troubleshooting</span></span>](troubleshooting.md)
* [<span data-ttu-id="ff1de-204">Release notes</span><span class="sxs-lookup"><span data-stu-id="ff1de-204">Release notes</span></span>](releasenotes.md)
