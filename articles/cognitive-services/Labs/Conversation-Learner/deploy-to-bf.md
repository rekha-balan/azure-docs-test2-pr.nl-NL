---
title: How to deploy a Conversation Learner bot - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to deploy a Conversation Learner bot.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 83e1fbfeee75534757dcb3c0275ca881e1eea517
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968128"
---
# <a name="how-to-deploy-a-conversation-learner-bot"></a><span data-ttu-id="54097-103">How to deploy a Conversation Learner bot</span><span class="sxs-lookup"><span data-stu-id="54097-103">How to deploy a Conversation Learner bot</span></span>

<span data-ttu-id="54097-104">This document explains how to deploy a Conversation Learner bot -- either locally, or into Azure.</span><span class="sxs-lookup"><span data-stu-id="54097-104">This document explains how to deploy a Conversation Learner bot -- either locally, or into Azure.</span></span>

## <a name="prerequisite-determine-the-model-id"></a><span data-ttu-id="54097-105">Prerequisite: determine the model ID</span><span class="sxs-lookup"><span data-stu-id="54097-105">Prerequisite: determine the model ID</span></span> 

<span data-ttu-id="54097-106">To run a bot outside of the Conversation Learner UI, you must set the Conversation Learner model ID that the bot will use -- i.e., the ID of the machine learning model in the Conversation Learner cloud.</span><span class="sxs-lookup"><span data-stu-id="54097-106">To run a bot outside of the Conversation Learner UI, you must set the Conversation Learner model ID that the bot will use -- i.e., the ID of the machine learning model in the Conversation Learner cloud.</span></span>  <span data-ttu-id="54097-107">(By contrast, when running the bot through the Conversation Learner UI, the UI chooses which model ID.).</span><span class="sxs-lookup"><span data-stu-id="54097-107">(By contrast, when running the bot through the Conversation Learner UI, the UI chooses which model ID.).</span></span>  

<span data-ttu-id="54097-108">Here's how to obtain the model ID:</span><span class="sxs-lookup"><span data-stu-id="54097-108">Here's how to obtain the model ID:</span></span>

1. <span data-ttu-id="54097-109">Start your bot and the Conversation Learner UI.</span><span class="sxs-lookup"><span data-stu-id="54097-109">Start your bot and the Conversation Learner UI.</span></span>  <span data-ttu-id="54097-110">See the Quickstart guide for full instructions; to summarize:</span><span class="sxs-lookup"><span data-stu-id="54097-110">See the Quickstart guide for full instructions; to summarize:</span></span>

    <span data-ttu-id="54097-111">In one command window:</span><span class="sxs-lookup"><span data-stu-id="54097-111">In one command window:</span></span>

    ```
    [open a command window]
    cd my-bot
    npm start
    ```

    <span data-ttu-id="54097-112">In anther command window</span><span class="sxs-lookup"><span data-stu-id="54097-112">In anther command window</span></span>

    ```bash
    [open second command prompt window]
    cd cl-bot-01
    npm run ui
    ```

2. <span data-ttu-id="54097-113">Open browser to http://localhost:5050</span><span class="sxs-lookup"><span data-stu-id="54097-113">Open browser to http://localhost:5050</span></span> 

3. <span data-ttu-id="54097-114">Click on the Conversation Learner model you want to get the ID for</span><span class="sxs-lookup"><span data-stu-id="54097-114">Click on the Conversation Learner model you want to get the ID for</span></span>

4. <span data-ttu-id="54097-115">Click on "Settings" in the nav bar on the left.</span><span class="sxs-lookup"><span data-stu-id="54097-115">Click on "Settings" in the nav bar on the left.</span></span>

5. <span data-ttu-id="54097-116">The "Model ID" GUID is displayed near the top of the page.</span><span class="sxs-lookup"><span data-stu-id="54097-116">The "Model ID" GUID is displayed near the top of the page.</span></span>

## <a name="option-1-deploying-a-conversation-learner-bot-to-run-locally"></a><span data-ttu-id="54097-117">Option 1: Deploying a Conversation Learner bot to run locally</span><span class="sxs-lookup"><span data-stu-id="54097-117">Option 1: Deploying a Conversation Learner bot to run locally</span></span>

<span data-ttu-id="54097-118">This deploys a bot to your local machine, and shows how you can access it using the Bot Framework emulator.</span><span class="sxs-lookup"><span data-stu-id="54097-118">This deploys a bot to your local machine, and shows how you can access it using the Bot Framework emulator.</span></span>

### <a name="configure-your-bot-for-access-outside-the-conversation-learner-ui"></a><span data-ttu-id="54097-119">Configure your bot for access outside the Conversation Learner UI</span><span class="sxs-lookup"><span data-stu-id="54097-119">Configure your bot for access outside the Conversation Learner UI</span></span>

<span data-ttu-id="54097-120">When running a bot locally, add the Application ID to the bot's `.env` file:</span><span class="sxs-lookup"><span data-stu-id="54097-120">When running a bot locally, add the Application ID to the bot's `.env` file:</span></span>

    ```
    CONVERSATION_LEARNER_MODEL_ID=<YOUR_MODEL_ID>
    ```

<span data-ttu-id="54097-121">Then, start your bot:</span><span class="sxs-lookup"><span data-stu-id="54097-121">Then, start your bot:</span></span>

    ```
    [open a command window]
    cd my-bot
    npm start
    ```

<span data-ttu-id="54097-122">The bot is now running locally.</span><span class="sxs-lookup"><span data-stu-id="54097-122">The bot is now running locally.</span></span>  <span data-ttu-id="54097-123">You can access it with the Bot Framework emulator.</span><span class="sxs-lookup"><span data-stu-id="54097-123">You can access it with the Bot Framework emulator.</span></span>

### <a name="download-and-install-the-emulator"></a><span data-ttu-id="54097-124">Download and install the emulator</span><span class="sxs-lookup"><span data-stu-id="54097-124">Download and install the emulator</span></span>

    ```
    git clone https://github.com/Microsoft/BotFramework-Emulator
    npm install
    npm run build
    npm start
    ```

### <a name="connect-the-emulator-to-your-bot"></a><span data-ttu-id="54097-125">Connect the emulator to your bot</span><span class="sxs-lookup"><span data-stu-id="54097-125">Connect the emulator to your bot</span></span>

1. <span data-ttu-id="54097-126">In the upper left of the emulator, in the box "Enter your endpoint URL", enter `http://127.0.0.1:3978/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="54097-126">In the upper left of the emulator, in the box "Enter your endpoint URL", enter `http://127.0.0.1:3978/api/messages`.</span></span>  <span data-ttu-id="54097-127">Leave the other fields blank, and click "Connect".</span><span class="sxs-lookup"><span data-stu-id="54097-127">Leave the other fields blank, and click "Connect".</span></span>

2. <span data-ttu-id="54097-128">You are now conversing with your bot.</span><span class="sxs-lookup"><span data-stu-id="54097-128">You are now conversing with your bot.</span></span>

## <a name="option-2-deploy-to-azure"></a><span data-ttu-id="54097-129">Option 2: Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="54097-129">Option 2: Deploy to Azure</span></span>

<span data-ttu-id="54097-130">Publish your Conversation Learner bot similar to the same way you would publish any other bot.</span><span class="sxs-lookup"><span data-stu-id="54097-130">Publish your Conversation Learner bot similar to the same way you would publish any other bot.</span></span> <span data-ttu-id="54097-131">At a high level, you upload your code to a hosted website, set the appropriate configuration values, and then register the bot with various channels.</span><span class="sxs-lookup"><span data-stu-id="54097-131">At a high level, you upload your code to a hosted website, set the appropriate configuration values, and then register the bot with various channels.</span></span> <span data-ttu-id="54097-132">Detailed instructions are in this video showing how to publish your bot using Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="54097-132">Detailed instructions are in this video showing how to publish your bot using Azure Bot Service.</span></span>

<span data-ttu-id="54097-133">Once the bot is deployed and running you can connect different channels to it such as Facebook, Teams, Skype etc using an Azure Bot Channel Registration.</span><span class="sxs-lookup"><span data-stu-id="54097-133">Once the bot is deployed and running you can connect different channels to it such as Facebook, Teams, Skype etc using an Azure Bot Channel Registration.</span></span> <span data-ttu-id="54097-134">For documentation on that process see: https://docs.microsoft.com/en-us/bot-framework/bot-service-quickstart-registration</span><span class="sxs-lookup"><span data-stu-id="54097-134">For documentation on that process see: https://docs.microsoft.com/en-us/bot-framework/bot-service-quickstart-registration</span></span>

<span data-ttu-id="54097-135">Below are step-by-step instructions for deploying a Conversation Learner Bot to Azure.</span><span class="sxs-lookup"><span data-stu-id="54097-135">Below are step-by-step instructions for deploying a Conversation Learner Bot to Azure.</span></span>  <span data-ttu-id="54097-136">These instructions assume that your bot source is available from a cloud-based source such as Azure DevOps Services, GitHub, BitBucket, or OneDrive, and will configure your bot for continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="54097-136">These instructions assume that your bot source is available from a cloud-based source such as Azure DevOps Services, GitHub, BitBucket, or OneDrive, and will configure your bot for continuous deployment.</span></span>

1. <span data-ttu-id="54097-137">Log into the Azure portal at https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="54097-137">Log into the Azure portal at https://portal.azure.com</span></span>

2. <span data-ttu-id="54097-138">Create a new "Web App Bot" resource</span><span class="sxs-lookup"><span data-stu-id="54097-138">Create a new "Web App Bot" resource</span></span> 

    1. <span data-ttu-id="54097-139">Give the bot a name</span><span class="sxs-lookup"><span data-stu-id="54097-139">Give the bot a name</span></span>
    2. <span data-ttu-id="54097-140">Click on "Bot Template", choose "Node.js", choose "Basic", then click on the "Select" button</span><span class="sxs-lookup"><span data-stu-id="54097-140">Click on "Bot Template", choose "Node.js", choose "Basic", then click on the "Select" button</span></span>
    3. <span data-ttu-id="54097-141">Click on "create" to create the Web App Bot.</span><span class="sxs-lookup"><span data-stu-id="54097-141">Click on "create" to create the Web App Bot.</span></span>
    4. <span data-ttu-id="54097-142">Wait for the Web App Bot resource to be created.</span><span class="sxs-lookup"><span data-stu-id="54097-142">Wait for the Web App Bot resource to be created.</span></span>

3. <span data-ttu-id="54097-143">In the Azure portal, edit the Web App Bot resource you just created.</span><span class="sxs-lookup"><span data-stu-id="54097-143">In the Azure portal, edit the Web App Bot resource you just created.</span></span>

    1. <span data-ttu-id="54097-144">Click on "Application Settings" nav item on the left</span><span class="sxs-lookup"><span data-stu-id="54097-144">Click on "Application Settings" nav item on the left</span></span>
    1. <span data-ttu-id="54097-145">Scroll down to the "App Settings" section</span><span class="sxs-lookup"><span data-stu-id="54097-145">Scroll down to the "App Settings" section</span></span>
    2. <span data-ttu-id="54097-146">Add these settings:</span><span class="sxs-lookup"><span data-stu-id="54097-146">Add these settings:</span></span>

        <span data-ttu-id="54097-147">Environment variable</span><span class="sxs-lookup"><span data-stu-id="54097-147">Environment variable</span></span> | <span data-ttu-id="54097-148">value</span><span class="sxs-lookup"><span data-stu-id="54097-148">value</span></span>
        --- | --- 
        <span data-ttu-id="54097-149">CONVERSATION_LEARNER_SERVICE_URI</span><span class="sxs-lookup"><span data-stu-id="54097-149">CONVERSATION_LEARNER_SERVICE_URI</span></span> | <span data-ttu-id="54097-150">"https://westus.api.cognitive.microsoft.com/conversationlearner/v1.0/"</span><span class="sxs-lookup"><span data-stu-id="54097-150">"https://westus.api.cognitive.microsoft.com/conversationlearner/v1.0/"</span></span>
        <span data-ttu-id="54097-151">CONVERSATION_LEARNER_MODEL_ID</span><span class="sxs-lookup"><span data-stu-id="54097-151">CONVERSATION_LEARNER_MODEL_ID</span></span>      | <span data-ttu-id="54097-152">Application Id GUID, obtained from the Conversation Learner UI under the "settings" for the model></span><span class="sxs-lookup"><span data-stu-id="54097-152">Application Id GUID, obtained from the Conversation Learner UI under the "settings" for the model></span></span>
        <span data-ttu-id="54097-153">LUIS_AUTHORING_KEY</span><span class="sxs-lookup"><span data-stu-id="54097-153">LUIS_AUTHORING_KEY</span></span>               | <span data-ttu-id="54097-154">LUIS authoring key for this model</span><span class="sxs-lookup"><span data-stu-id="54097-154">LUIS authoring key for this model</span></span>
    
    4. <span data-ttu-id="54097-155">Click on "Save" near the top of the page</span><span class="sxs-lookup"><span data-stu-id="54097-155">Click on "Save" near the top of the page</span></span>
    5. <span data-ttu-id="54097-156">Open "Build" nav item on the left</span><span class="sxs-lookup"><span data-stu-id="54097-156">Open "Build" nav item on the left</span></span>
    6. <span data-ttu-id="54097-157">Click on "Configure continuous deployment"</span><span class="sxs-lookup"><span data-stu-id="54097-157">Click on "Configure continuous deployment"</span></span> 
    7. <span data-ttu-id="54097-158">Click on the "Setup" icon under deployments</span><span class="sxs-lookup"><span data-stu-id="54097-158">Click on the "Setup" icon under deployments</span></span>
    8. <span data-ttu-id="54097-159">Click on "Required Settings"</span><span class="sxs-lookup"><span data-stu-id="54097-159">Click on "Required Settings"</span></span>
    9. <span data-ttu-id="54097-160">Select the source where your bot code is available, and configure the source.</span><span class="sxs-lookup"><span data-stu-id="54097-160">Select the source where your bot code is available, and configure the source.</span></span>
