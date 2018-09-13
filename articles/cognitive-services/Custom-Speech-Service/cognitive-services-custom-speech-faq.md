---
title: Frequently asked questions for the Custom Speech Service on Azure | Microsoft Docs
description: Here are answers to the most popular questions about the Custom Speech Service.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 11/21/2016
ms.author: panosper
ms.openlocfilehash: a929869b36387b3257b672308ceca36c84ff8cae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868689"
---
# <a name="custom-speech-service-frequently-asked-questions"></a><span data-ttu-id="02078-103">Custom Speech Service Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="02078-103">Custom Speech Service Frequently Asked Questions</span></span>

<span data-ttu-id="02078-104">If you can't find answers to your questions in this FAQ, try asking the Custom Speech Service community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) and [UserVoice](https://cognitive.uservoice.com/)</span><span class="sxs-lookup"><span data-stu-id="02078-104">If you can't find answers to your questions in this FAQ, try asking the Custom Speech Service community on [StackOverflow](https://stackoverflow.com/questions/tagged/project-oxford+or+microsoft-cognitive) and [UserVoice](https://cognitive.uservoice.com/)</span></span>

## <a name="general"></a><span data-ttu-id="02078-105">General</span><span class="sxs-lookup"><span data-stu-id="02078-105">General</span></span>

<span data-ttu-id="02078-106">**Question**: How will I know when the processing of my data set or model is complete?</span><span class="sxs-lookup"><span data-stu-id="02078-106">**Question**: How will I know when the processing of my data set or model is complete?</span></span>

<span data-ttu-id="02078-107">**Answer**: Currently, the status of the model or data set in the table is the only want to know.</span><span class="sxs-lookup"><span data-stu-id="02078-107">**Answer**: Currently, the status of the model or data set in the table is the only want to know.</span></span>
<span data-ttu-id="02078-108">When the processing is complete, the status will be "Ready".</span><span class="sxs-lookup"><span data-stu-id="02078-108">When the processing is complete, the status will be "Ready".</span></span>
<span data-ttu-id="02078-109">We are working on improved methods for communication processing status, such as email notification.</span><span class="sxs-lookup"><span data-stu-id="02078-109">We are working on improved methods for communication processing status, such as email notification.</span></span>

<span data-ttu-id="02078-110">**Question**: Can I create more than one model at a time?</span><span class="sxs-lookup"><span data-stu-id="02078-110">**Question**: Can I create more than one model at a time?</span></span>

<span data-ttu-id="02078-111">**Answer**: There is no limit to how many models are in your collection but only one can be created at a time on each page.</span><span class="sxs-lookup"><span data-stu-id="02078-111">**Answer**: There is no limit to how many models are in your collection but only one can be created at a time on each page.</span></span>
<span data-ttu-id="02078-112">For example, you cannot start a language model creation process if there is currently a language model in the process stage.</span><span class="sxs-lookup"><span data-stu-id="02078-112">For example, you cannot start a language model creation process if there is currently a language model in the process stage.</span></span>
<span data-ttu-id="02078-113">You can, however, have an acoustic model and a language model processing at the same time.</span><span class="sxs-lookup"><span data-stu-id="02078-113">You can, however, have an acoustic model and a language model processing at the same time.</span></span> 

<span data-ttu-id="02078-114">**Question**: I realized I made a mistake.</span><span class="sxs-lookup"><span data-stu-id="02078-114">**Question**: I realized I made a mistake.</span></span> <span data-ttu-id="02078-115">How do I cancel my data import or model creation that’s in progress?</span><span class="sxs-lookup"><span data-stu-id="02078-115">How do I cancel my data import or model creation that’s in progress?</span></span> 

<span data-ttu-id="02078-116">**Answer**: Currently you cannot roll back a acoustic or language adaptation process.</span><span class="sxs-lookup"><span data-stu-id="02078-116">**Answer**: Currently you cannot roll back a acoustic or language adaptation process.</span></span>
<span data-ttu-id="02078-117">Imported data can be deleted after the import has been completed</span><span class="sxs-lookup"><span data-stu-id="02078-117">Imported data can be deleted after the import has been completed</span></span>

<span data-ttu-id="02078-118">**Question**: What is the difference between the Search & Dictation Models and the Conversational Models?</span><span class="sxs-lookup"><span data-stu-id="02078-118">**Question**: What is the difference between the Search & Dictation Models and the Conversational Models?</span></span>

<span data-ttu-id="02078-119">**Answer**: There are two Base Acoustic & Language Models to choose from in the Custom Speech Service.</span><span class="sxs-lookup"><span data-stu-id="02078-119">**Answer**: There are two Base Acoustic & Language Models to choose from in the Custom Speech Service.</span></span>
<span data-ttu-id="02078-120">search queries, or dictation.</span><span class="sxs-lookup"><span data-stu-id="02078-120">search queries, or dictation.</span></span> <span data-ttu-id="02078-121">The Microsoft Conversational AM is appropriate for recognizing speech spoken in a conversational style.</span><span class="sxs-lookup"><span data-stu-id="02078-121">The Microsoft Conversational AM is appropriate for recognizing speech spoken in a conversational style.</span></span>
<span data-ttu-id="02078-122">This type of speech is typically directed at another person, such as in call centers or meetings.</span><span class="sxs-lookup"><span data-stu-id="02078-122">This type of speech is typically directed at another person, such as in call centers or meetings.</span></span>

<span data-ttu-id="02078-123">**Question**: Can I update my existing model (model stacking)?</span><span class="sxs-lookup"><span data-stu-id="02078-123">**Question**: Can I update my existing model (model stacking)?</span></span>

<span data-ttu-id="02078-124">**Answer**: We do not offer the ability to update an existing model with new data.</span><span class="sxs-lookup"><span data-stu-id="02078-124">**Answer**: We do not offer the ability to update an existing model with new data.</span></span>
<span data-ttu-id="02078-125">If you have a new data set and you want to customize an existing model you must re-adapt it with the new data and the old data set that you used.</span><span class="sxs-lookup"><span data-stu-id="02078-125">If you have a new data set and you want to customize an existing model you must re-adapt it with the new data and the old data set that you used.</span></span>
<span data-ttu-id="02078-126">The old and new data sets must be combined in a single .zip (if it is acoustic data) or a .txt file if it is language data Once adaptation is done the new updated model needs to be de-deployed to obtain a new endpoint</span><span class="sxs-lookup"><span data-stu-id="02078-126">The old and new data sets must be combined in a single .zip (if it is acoustic data) or a .txt file if it is language data Once adaptation is done the new updated model needs to be de-deployed to obtain a new endpoint</span></span>

<span data-ttu-id="02078-127">**Question**: What if I need higher concurrency than the default value.</span><span class="sxs-lookup"><span data-stu-id="02078-127">**Question**: What if I need higher concurrency than the default value.</span></span> 

<span data-ttu-id="02078-128">**Answer**: You can scale up your model in increments of 5 concurrent requests which we call Scale Units.</span><span class="sxs-lookup"><span data-stu-id="02078-128">**Answer**: You can scale up your model in increments of 5 concurrent requests which we call Scale Units.</span></span> <span data-ttu-id="02078-129">Each Scale unit guarantees that your model can process 5 audio stream simultaneously.</span><span class="sxs-lookup"><span data-stu-id="02078-129">Each Scale unit guarantees that your model can process 5 audio stream simultaneously.</span></span> <span data-ttu-id="02078-130">You can buy up to 100 Scale units (or 500 concurrent requests).</span><span class="sxs-lookup"><span data-stu-id="02078-130">You can buy up to 100 Scale units (or 500 concurrent requests).</span></span>

<span data-ttu-id="02078-131">Please contact us if you require higher than that.</span><span class="sxs-lookup"><span data-stu-id="02078-131">Please contact us if you require higher than that.</span></span>

<span data-ttu-id="02078-132">**Question**: Can I download my model and run it locally?</span><span class="sxs-lookup"><span data-stu-id="02078-132">**Question**: Can I download my model and run it locally?</span></span>

<span data-ttu-id="02078-133">**Answer**: We do not enable models to be downloaded and executed locally.</span><span class="sxs-lookup"><span data-stu-id="02078-133">**Answer**: We do not enable models to be downloaded and executed locally.</span></span>

<span data-ttu-id="02078-134">**Question**: Are my requests logged?</span><span class="sxs-lookup"><span data-stu-id="02078-134">**Question**: Are my requests logged?</span></span>

<span data-ttu-id="02078-135">**Answer**: You have a choice during the creation of a deployment to switch off tracing, at which point no audio or transcriptions will be logged.</span><span class="sxs-lookup"><span data-stu-id="02078-135">**Answer**: You have a choice during the creation of a deployment to switch off tracing, at which point no audio or transcriptions will be logged.</span></span> <span data-ttu-id="02078-136">Otherwise requests are typically logged in Azure in secure storage.</span><span class="sxs-lookup"><span data-stu-id="02078-136">Otherwise requests are typically logged in Azure in secure storage.</span></span> <span data-ttu-id="02078-137">If you have further privacy concerns that prohibit you from using the Custom Speech Service please contact us.</span><span class="sxs-lookup"><span data-stu-id="02078-137">If you have further privacy concerns that prohibit you from using the Custom Speech Service please contact us.</span></span>

## <a name="importing-data"></a><span data-ttu-id="02078-138">Importing Data</span><span class="sxs-lookup"><span data-stu-id="02078-138">Importing Data</span></span>

<span data-ttu-id="02078-139">**Question**: What is the limit on the size of the data set?</span><span class="sxs-lookup"><span data-stu-id="02078-139">**Question**: What is the limit on the size of the data set?</span></span> <span data-ttu-id="02078-140">Why?</span><span class="sxs-lookup"><span data-stu-id="02078-140">Why?</span></span> 

<span data-ttu-id="02078-141">**Answer**: The current limit for a data set is 2 GB, due to the restriction on the size of a file for HTTP upload.</span><span class="sxs-lookup"><span data-stu-id="02078-141">**Answer**: The current limit for a data set is 2 GB, due to the restriction on the size of a file for HTTP upload.</span></span> 

<span data-ttu-id="02078-142">**Question**: Can I zip my text files in order to upload a larger text file?</span><span class="sxs-lookup"><span data-stu-id="02078-142">**Question**: Can I zip my text files in order to upload a larger text file?</span></span> 

<span data-ttu-id="02078-143">**Answer**: No, currently only uncompressed text files are allowed.</span><span class="sxs-lookup"><span data-stu-id="02078-143">**Answer**: No, currently only uncompressed text files are allowed.</span></span>

<span data-ttu-id="02078-144">**Question**: The data report says there were failed utterances.</span><span class="sxs-lookup"><span data-stu-id="02078-144">**Question**: The data report says there were failed utterances.</span></span> <span data-ttu-id="02078-145">Is this a problem?</span><span class="sxs-lookup"><span data-stu-id="02078-145">Is this a problem?</span></span>

<span data-ttu-id="02078-146">**Answer**: If only a few utterances failed to be imported successfully, this is not a problem.</span><span class="sxs-lookup"><span data-stu-id="02078-146">**Answer**: If only a few utterances failed to be imported successfully, this is not a problem.</span></span>
<span data-ttu-id="02078-147">If the vast majority of the utterances in an acoustic or language data set (e.g. >95%) are successfully imported, the data set can be usable.</span><span class="sxs-lookup"><span data-stu-id="02078-147">If the vast majority of the utterances in an acoustic or language data set (e.g. >95%) are successfully imported, the data set can be usable.</span></span> <span data-ttu-id="02078-148">However, it is recommended that you try to understand why the utterances failed and fix the problems.</span><span class="sxs-lookup"><span data-stu-id="02078-148">However, it is recommended that you try to understand why the utterances failed and fix the problems.</span></span>
<span data-ttu-id="02078-149">Most common problems, such as formatting errors, are easy to fix.</span><span class="sxs-lookup"><span data-stu-id="02078-149">Most common problems, such as formatting errors, are easy to fix.</span></span> 

## <a name="creating-am"></a><span data-ttu-id="02078-150">Creating AM</span><span class="sxs-lookup"><span data-stu-id="02078-150">Creating AM</span></span>

<span data-ttu-id="02078-151">**Question**: How much acoustic data do I need?</span><span class="sxs-lookup"><span data-stu-id="02078-151">**Question**: How much acoustic data do I need?</span></span>

<span data-ttu-id="02078-152">**Answer**: We recommend starting with 30 minutes to one hour of acoustic data</span><span class="sxs-lookup"><span data-stu-id="02078-152">**Answer**: We recommend starting with 30 minutes to one hour of acoustic data</span></span>

<span data-ttu-id="02078-153">**Question**: What sort of data should I collect?</span><span class="sxs-lookup"><span data-stu-id="02078-153">**Question**: What sort of data should I collect?</span></span>

<span data-ttu-id="02078-154">**Answer**: You should collect data that's as close to the application scenario and use case as possible.</span><span class="sxs-lookup"><span data-stu-id="02078-154">**Answer**: You should collect data that's as close to the application scenario and use case as possible.</span></span>
<span data-ttu-id="02078-155">This means the data collection should match the target application and users in terms of device or devices, environments, and types of speakers.</span><span class="sxs-lookup"><span data-stu-id="02078-155">This means the data collection should match the target application and users in terms of device or devices, environments, and types of speakers.</span></span> <span data-ttu-id="02078-156">In general, you should collect data from as broad a range of speakers as possible.</span><span class="sxs-lookup"><span data-stu-id="02078-156">In general, you should collect data from as broad a range of speakers as possible.</span></span> 

<span data-ttu-id="02078-157">**Question**: How should I collect it?</span><span class="sxs-lookup"><span data-stu-id="02078-157">**Question**: How should I collect it?</span></span> 

<span data-ttu-id="02078-158">**Answer**: You can create a standalone data collection application or use some off the shelf audio recording software.</span><span class="sxs-lookup"><span data-stu-id="02078-158">**Answer**: You can create a standalone data collection application or use some off the shelf audio recording software.</span></span>
<span data-ttu-id="02078-159">You can also create a version of your application that logs the audio data and uses that.</span><span class="sxs-lookup"><span data-stu-id="02078-159">You can also create a version of your application that logs the audio data and uses that.</span></span> 

<span data-ttu-id="02078-160">**Question**: Do I need to transcribe adaptation data myself?</span><span class="sxs-lookup"><span data-stu-id="02078-160">**Question**: Do I need to transcribe adaptation data myself?</span></span> 

<span data-ttu-id="02078-161">**Answer**: The data must be transcribed.</span><span class="sxs-lookup"><span data-stu-id="02078-161">**Answer**: The data must be transcribed.</span></span> <span data-ttu-id="02078-162">You can transcribe it yourself or use a professional transcription service.</span><span class="sxs-lookup"><span data-stu-id="02078-162">You can transcribe it yourself or use a professional transcription service.</span></span> <span data-ttu-id="02078-163">Some of these use professional transcribers and others use crowdsourcing.</span><span class="sxs-lookup"><span data-stu-id="02078-163">Some of these use professional transcribers and others use crowdsourcing.</span></span> <span data-ttu-id="02078-164">We can also recommend a transcription service upon request.</span><span class="sxs-lookup"><span data-stu-id="02078-164">We can also recommend a transcription service upon request.</span></span>

<span data-ttu-id="02078-165">**Question**: How long does it take to create a custom acoustic model?</span><span class="sxs-lookup"><span data-stu-id="02078-165">**Question**: How long does it take to create a custom acoustic model?</span></span>

<span data-ttu-id="02078-166">**Answer**: The processing time for creating a custom acoustic model is about the same as the length of the acoustic data set.</span><span class="sxs-lookup"><span data-stu-id="02078-166">**Answer**: The processing time for creating a custom acoustic model is about the same as the length of the acoustic data set.</span></span>
<span data-ttu-id="02078-167">So, a customized acoustic model created from a five hour data set will take about five hours to process.</span><span class="sxs-lookup"><span data-stu-id="02078-167">So, a customized acoustic model created from a five hour data set will take about five hours to process.</span></span> 

## <a name="offline-testing"></a><span data-ttu-id="02078-168">Offline Testing</span><span class="sxs-lookup"><span data-stu-id="02078-168">Offline Testing</span></span>

<span data-ttu-id="02078-169">**Question**: Can I perform offline testing of my custom acoustic model using a custom language model?</span><span class="sxs-lookup"><span data-stu-id="02078-169">**Question**: Can I perform offline testing of my custom acoustic model using a custom language model?</span></span>

<span data-ttu-id="02078-170">**Answer**: Yes, just select the custom language model in the drop down when you set up the offline test</span><span class="sxs-lookup"><span data-stu-id="02078-170">**Answer**: Yes, just select the custom language model in the drop down when you set up the offline test</span></span>

<span data-ttu-id="02078-171">**Question**: Can I perform offline testing of my custom language model using a custom acoustic model?</span><span class="sxs-lookup"><span data-stu-id="02078-171">**Question**: Can I perform offline testing of my custom language model using a custom acoustic model?</span></span>

<span data-ttu-id="02078-172">**Answer**: Yes, just select the custom acoustic model in the drop-down menu when you set up the offline test.</span><span class="sxs-lookup"><span data-stu-id="02078-172">**Answer**: Yes, just select the custom acoustic model in the drop-down menu when you set up the offline test.</span></span>

<span data-ttu-id="02078-173">**Question**: What is Word Error Rate and how is it computed?</span><span class="sxs-lookup"><span data-stu-id="02078-173">**Question**: What is Word Error Rate and how is it computed?</span></span>

<span data-ttu-id="02078-174">**Answer**: Word Error Rate is the evaluation metric for speech recognition.</span><span class="sxs-lookup"><span data-stu-id="02078-174">**Answer**: Word Error Rate is the evaluation metric for speech recognition.</span></span> <span data-ttu-id="02078-175">It is counted as the total number of errors, which includes insertions, deletions, and substitutions, divided by the total number of words in the reference transcription.</span><span class="sxs-lookup"><span data-stu-id="02078-175">It is counted as the total number of errors, which includes insertions, deletions, and substitutions, divided by the total number of words in the reference transcription.</span></span>

<span data-ttu-id="02078-176">**Question**: I now know the test results of my custom model, is this a good or bad number?</span><span class="sxs-lookup"><span data-stu-id="02078-176">**Question**: I now know the test results of my custom model, is this a good or bad number?</span></span>

<span data-ttu-id="02078-177">**Answer**: The results show a comparison between the baseline model and the one you customized.</span><span class="sxs-lookup"><span data-stu-id="02078-177">**Answer**: The results show a comparison between the baseline model and the one you customized.</span></span>
<span data-ttu-id="02078-178">You should aim to beat the baseline model to make the customization worthwhile</span><span class="sxs-lookup"><span data-stu-id="02078-178">You should aim to beat the baseline model to make the customization worthwhile</span></span>

<span data-ttu-id="02078-179">**Question**: How do I figure out the WER of the base models, so I can see if there was improvement?</span><span class="sxs-lookup"><span data-stu-id="02078-179">**Question**: How do I figure out the WER of the base models, so I can see if there was improvement?</span></span> 

<span data-ttu-id="02078-180">**Answer**: The offline test results show accuracy of baseline accuracy of the custom model and the improvement over baseline</span><span class="sxs-lookup"><span data-stu-id="02078-180">**Answer**: The offline test results show accuracy of baseline accuracy of the custom model and the improvement over baseline</span></span>

## <a name="creating-lm"></a><span data-ttu-id="02078-181">Creating LM</span><span class="sxs-lookup"><span data-stu-id="02078-181">Creating LM</span></span>

<span data-ttu-id="02078-182">**Question**: How much text data do I need to upload?</span><span class="sxs-lookup"><span data-stu-id="02078-182">**Question**: How much text data do I need to upload?</span></span>

<span data-ttu-id="02078-183">**Answer**: This is a difficult question to give a precise answer to, as it depends on how different the vocabulary and phrases used in your application are from the starting language models.</span><span class="sxs-lookup"><span data-stu-id="02078-183">**Answer**: This is a difficult question to give a precise answer to, as it depends on how different the vocabulary and phrases used in your application are from the starting language models.</span></span> <span data-ttu-id="02078-184">For all new words, it is useful to provide as many examples as possible of the usage of those words.</span><span class="sxs-lookup"><span data-stu-id="02078-184">For all new words, it is useful to provide as many examples as possible of the usage of those words.</span></span> <span data-ttu-id="02078-185">For common phrases that are used in your application, including those in the language data is also useful as it tells the system to listen for these terms as well.</span><span class="sxs-lookup"><span data-stu-id="02078-185">For common phrases that are used in your application, including those in the language data is also useful as it tells the system to listen for these terms as well.</span></span>
<span data-ttu-id="02078-186">It is common to have at least one hundred and typically several hundred utterances in the language data set or more.</span><span class="sxs-lookup"><span data-stu-id="02078-186">It is common to have at least one hundred and typically several hundred utterances in the language data set or more.</span></span>
<span data-ttu-id="02078-187">Also if certain types \* of queries are expected to be more common than others, you can insert multiple copies of the common queries in the data set.</span><span class="sxs-lookup"><span data-stu-id="02078-187">Also if certain types \* of queries are expected to be more common than others, you can insert multiple copies of the common queries in the data set.</span></span>

<span data-ttu-id="02078-188">**Question**: Can I just upload a list of words?</span><span class="sxs-lookup"><span data-stu-id="02078-188">**Question**: Can I just upload a list of words?</span></span>

<span data-ttu-id="02078-189">**Answer**: Uploading a list of words will get the words into to vocabulary but not teach the system how the words are typically used.</span><span class="sxs-lookup"><span data-stu-id="02078-189">**Answer**: Uploading a list of words will get the words into to vocabulary but not teach the system how the words are typically used.</span></span>
<span data-ttu-id="02078-190">By providing full or partial utterances (sentences or phrases of things users are likely to say) the language model can learn the new words and how they are used.</span><span class="sxs-lookup"><span data-stu-id="02078-190">By providing full or partial utterances (sentences or phrases of things users are likely to say) the language model can learn the new words and how they are used.</span></span> <span data-ttu-id="02078-191">The custom language model is good not just for getting new words in the system but also for adjusting the likelihood of known words for your application.</span><span class="sxs-lookup"><span data-stu-id="02078-191">The custom language model is good not just for getting new words in the system but also for adjusting the likelihood of known words for your application.</span></span> <span data-ttu-id="02078-192">Providing full utterances helps the system learn this.</span><span class="sxs-lookup"><span data-stu-id="02078-192">Providing full utterances helps the system learn this.</span></span> 

-----

 * [<span data-ttu-id="02078-193">Overview</span><span class="sxs-lookup"><span data-stu-id="02078-193">Overview</span></span>](cognitive-services-custom-speech-home.md)
 * [<span data-ttu-id="02078-194">Started</span><span class="sxs-lookup"><span data-stu-id="02078-194">Started</span></span>](cognitive-services-custom-speech-get-started.md)
 * [<span data-ttu-id="02078-195">Glossary</span><span class="sxs-lookup"><span data-stu-id="02078-195">Glossary</span></span>](cognitive-services-custom-speech-glossary.md)
