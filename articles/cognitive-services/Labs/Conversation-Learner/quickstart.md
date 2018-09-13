---
title: How to create a Conversation Learner model using Node.js - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: Learn how to create a Conversation Learner model using Node.js.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: bc0cf0900ec9f87c75091b3bf219d92e0859aa1f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871200"
---
# <a name="create-a-conversation-learner-model-using-nodejs"></a><span data-ttu-id="1805c-103">Create a Conversation Learner model using Node.js</span><span class="sxs-lookup"><span data-stu-id="1805c-103">Create a Conversation Learner model using Node.js</span></span>

<span data-ttu-id="1805c-104">Conversation Learner reduces the complexity of building bots.</span><span class="sxs-lookup"><span data-stu-id="1805c-104">Conversation Learner reduces the complexity of building bots.</span></span> <span data-ttu-id="1805c-105">It enables a hybrid development work-flow allowing hand-written code and machine learning to reduce the amount of code required to write bots.</span><span class="sxs-lookup"><span data-stu-id="1805c-105">It enables a hybrid development work-flow allowing hand-written code and machine learning to reduce the amount of code required to write bots.</span></span> <span data-ttu-id="1805c-106">Certain fixed parts of your model, such as checking if the user is logged in, or making an API request to check store inventory, can still be coded.</span><span class="sxs-lookup"><span data-stu-id="1805c-106">Certain fixed parts of your model, such as checking if the user is logged in, or making an API request to check store inventory, can still be coded.</span></span> <span data-ttu-id="1805c-107">However, other changes in state and action selection can be learned from example dialogs given by the domain expert or developer.</span><span class="sxs-lookup"><span data-stu-id="1805c-107">However, other changes in state and action selection can be learned from example dialogs given by the domain expert or developer.</span></span>

## <a name="invitation-required"></a><span data-ttu-id="1805c-108">Invitation required</span><span class="sxs-lookup"><span data-stu-id="1805c-108">Invitation required</span></span>

<span data-ttu-id="1805c-109">*An invitation is required to access Project Conversation Learner.*</span><span class="sxs-lookup"><span data-stu-id="1805c-109">*An invitation is required to access Project Conversation Learner.*</span></span>

<span data-ttu-id="1805c-110">Project Conversation Learner consists of an SDK you add to your bot, and a cloud service which the SDK accesses for machine learning.</span><span class="sxs-lookup"><span data-stu-id="1805c-110">Project Conversation Learner consists of an SDK you add to your bot, and a cloud service which the SDK accesses for machine learning.</span></span>  <span data-ttu-id="1805c-111">At present, access to the Project Conversation Leaner cloud service requires an invitation.</span><span class="sxs-lookup"><span data-stu-id="1805c-111">At present, access to the Project Conversation Leaner cloud service requires an invitation.</span></span>  <span data-ttu-id="1805c-112">If you haven't been invited already, [request an invitation](https://aka.ms/conversation-learner-request-invite).</span><span class="sxs-lookup"><span data-stu-id="1805c-112">If you haven't been invited already, [request an invitation](https://aka.ms/conversation-learner-request-invite).</span></span>  <span data-ttu-id="1805c-113">If you have not received an invitation, you will be unable to access the cloud API.</span><span class="sxs-lookup"><span data-stu-id="1805c-113">If you have not received an invitation, you will be unable to access the cloud API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1805c-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1805c-114">Prerequisites</span></span>

- <span data-ttu-id="1805c-115">Node 8.5.0 or higher and npm 5.3.0 or higher.</span><span class="sxs-lookup"><span data-stu-id="1805c-115">Node 8.5.0 or higher and npm 5.3.0 or higher.</span></span> <span data-ttu-id="1805c-116">Install from [https://nodejs.org](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="1805c-116">Install from [https://nodejs.org](https://nodejs.org).</span></span>
  
- <span data-ttu-id="1805c-117">LUIS authoring key:</span><span class="sxs-lookup"><span data-stu-id="1805c-117">LUIS authoring key:</span></span>

  1. <span data-ttu-id="1805c-118">Log into [http://www.luis.ai](http://www.luis.ai).</span><span class="sxs-lookup"><span data-stu-id="1805c-118">Log into [http://www.luis.ai](http://www.luis.ai).</span></span>

  2. <span data-ttu-id="1805c-119">Click on your name in the upper right, then on "settings"</span><span class="sxs-lookup"><span data-stu-id="1805c-119">Click on your name in the upper right, then on "settings"</span></span>

  3. <span data-ttu-id="1805c-120">Authoring key is shown on the resulting page</span><span class="sxs-lookup"><span data-stu-id="1805c-120">Authoring key is shown on the resulting page</span></span>

  <span data-ttu-id="1805c-121">(Your LUIS authoring key serves 2 roles.</span><span class="sxs-lookup"><span data-stu-id="1805c-121">(Your LUIS authoring key serves 2 roles.</span></span>  <span data-ttu-id="1805c-122">First, it will serve as your Conversation Learner authoring key.</span><span class="sxs-lookup"><span data-stu-id="1805c-122">First, it will serve as your Conversation Learner authoring key.</span></span>  <span data-ttu-id="1805c-123">Second, Conversation Learner uses LUIS for entity extraction; the LUIS authoring key is used to create LUIS models on your behalf)</span><span class="sxs-lookup"><span data-stu-id="1805c-123">Second, Conversation Learner uses LUIS for entity extraction; the LUIS authoring key is used to create LUIS models on your behalf)</span></span>

- <span data-ttu-id="1805c-124">Google Chrome web browser.</span><span class="sxs-lookup"><span data-stu-id="1805c-124">Google Chrome web browser.</span></span> <span data-ttu-id="1805c-125">Install from [https://www.google.com/chrome/index.html](https://www.google.com/chrome/index.html).</span><span class="sxs-lookup"><span data-stu-id="1805c-125">Install from [https://www.google.com/chrome/index.html](https://www.google.com/chrome/index.html).</span></span>

- <span data-ttu-id="1805c-126">git.</span><span class="sxs-lookup"><span data-stu-id="1805c-126">git.</span></span> <span data-ttu-id="1805c-127">Install from [https://git-scm.com/downloads](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1805c-127">Install from [https://git-scm.com/downloads](https://git-scm.com/downloads).</span></span>

- <span data-ttu-id="1805c-128">VSCode.</span><span class="sxs-lookup"><span data-stu-id="1805c-128">VSCode.</span></span> <span data-ttu-id="1805c-129">Install from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="1805c-129">Install from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span> <span data-ttu-id="1805c-130">Note this is recommended, not required.</span><span class="sxs-lookup"><span data-stu-id="1805c-130">Note this is recommended, not required.</span></span>

## <a name="quick-start"></a><span data-ttu-id="1805c-131">Quick start</span><span class="sxs-lookup"><span data-stu-id="1805c-131">Quick start</span></span> 

1. <span data-ttu-id="1805c-132">Install and build:</span><span class="sxs-lookup"><span data-stu-id="1805c-132">Install and build:</span></span>

    ```bash    
    git clone https://github.com/Microsoft/ConversationLearner-Samples cl-bot-01
    cd cl-bot-01
    npm install
    npm run build
    ```

    > [!NOTE]
    > <span data-ttu-id="1805c-133">During `npm install`, you can ignore this error if it occurs: `gyp ERR! stack Error: Can't find Python executable`</span><span class="sxs-lookup"><span data-stu-id="1805c-133">During `npm install`, you can ignore this error if it occurs: `gyp ERR! stack Error: Can't find Python executable`</span></span>

2. <span data-ttu-id="1805c-134">Configure:</span><span class="sxs-lookup"><span data-stu-id="1805c-134">Configure:</span></span>

   <span data-ttu-id="1805c-135">Create a file called `.env` in the directory `cl-bot-01`.</span><span class="sxs-lookup"><span data-stu-id="1805c-135">Create a file called `.env` in the directory `cl-bot-01`.</span></span>  <span data-ttu-id="1805c-136">The contents of the file should be:</span><span class="sxs-lookup"><span data-stu-id="1805c-136">The contents of the file should be:</span></span>

   ```
   NODE_ENV=development
   LUIS_AUTHORING_KEY=<your LUIS authoring key>
   ```

3. <span data-ttu-id="1805c-137">Start bot:</span><span class="sxs-lookup"><span data-stu-id="1805c-137">Start bot:</span></span>

    ```
    npm start
    ```

    <span data-ttu-id="1805c-138">This runs the generic empty bot in `cl-bot-01/src/app.ts`.</span><span class="sxs-lookup"><span data-stu-id="1805c-138">This runs the generic empty bot in `cl-bot-01/src/app.ts`.</span></span>

3. <span data-ttu-id="1805c-139">Run Conversation Learner UI:</span><span class="sxs-lookup"><span data-stu-id="1805c-139">Run Conversation Learner UI:</span></span>

    ```bash
    [open second command prompt window]
    cd cl-bot-01
    npm run ui
    ```

4. <span data-ttu-id="1805c-140">Open browser to http://localhost:5050</span><span class="sxs-lookup"><span data-stu-id="1805c-140">Open browser to http://localhost:5050</span></span> 

<span data-ttu-id="1805c-141">You're now using Conversation Learner and can create and teach a Conversation Learner model.</span><span class="sxs-lookup"><span data-stu-id="1805c-141">You're now using Conversation Learner and can create and teach a Conversation Learner model.</span></span>  

> [!NOTE]
> <span data-ttu-id="1805c-142">At launch, Project Conversation Learner is available by invitation.</span><span class="sxs-lookup"><span data-stu-id="1805c-142">At launch, Project Conversation Learner is available by invitation.</span></span>  <span data-ttu-id="1805c-143">If http://localhost:5050 shows an HTTP `403` error, this means your account has not been invited.</span><span class="sxs-lookup"><span data-stu-id="1805c-143">If http://localhost:5050 shows an HTTP `403` error, this means your account has not been invited.</span></span>  <span data-ttu-id="1805c-144">Please [request an invitation](https://aka.ms/conversation-learner-request-invite).</span><span class="sxs-lookup"><span data-stu-id="1805c-144">Please [request an invitation](https://aka.ms/conversation-learner-request-invite).</span></span>

## <a name="tutorials-demos-and-switching-between-bots"></a><span data-ttu-id="1805c-145">Tutorials, demos, and switching between bots</span><span class="sxs-lookup"><span data-stu-id="1805c-145">Tutorials, demos, and switching between bots</span></span>

<span data-ttu-id="1805c-146">The instructions above started the generic empty bot.</span><span class="sxs-lookup"><span data-stu-id="1805c-146">The instructions above started the generic empty bot.</span></span>  <span data-ttu-id="1805c-147">To run a tutorial or demo bot instead:</span><span class="sxs-lookup"><span data-stu-id="1805c-147">To run a tutorial or demo bot instead:</span></span>

1. <span data-ttu-id="1805c-148">If you have the Conversation Learner web UI open, return to the list of models at http://localhost:5050/home.</span><span class="sxs-lookup"><span data-stu-id="1805c-148">If you have the Conversation Learner web UI open, return to the list of models at http://localhost:5050/home.</span></span>
    
2. <span data-ttu-id="1805c-149">If another bot is running (like `npm start` or `npm run demo-pizza`), stop it.</span><span class="sxs-lookup"><span data-stu-id="1805c-149">If another bot is running (like `npm start` or `npm run demo-pizza`), stop it.</span></span>  <span data-ttu-id="1805c-150">You do not need to stop the UI process, or close the web browser.</span><span class="sxs-lookup"><span data-stu-id="1805c-150">You do not need to stop the UI process, or close the web browser.</span></span>

3. <span data-ttu-id="1805c-151">Run a demo bot from the command line (step 2 above).</span><span class="sxs-lookup"><span data-stu-id="1805c-151">Run a demo bot from the command line (step 2 above).</span></span>  <span data-ttu-id="1805c-152">Demos include:</span><span class="sxs-lookup"><span data-stu-id="1805c-152">Demos include:</span></span>

  ```bash
  npm run tutorial-general
  npm run tutorial-entity-detection
  npm run tutorial-session-callbacks
  npm run tutorial-api-calls
  npm run tutorial-hybrid
  npm run demo-password
  npm run demo-pizza
  npm run demo-storage
  npm run demo-vrapp
  ```

4. <span data-ttu-id="1805c-153">If you're not already, switch to the Conversation Learner web UI in Chrome by loading http://localhost:5050/home.</span><span class="sxs-lookup"><span data-stu-id="1805c-153">If you're not already, switch to the Conversation Learner web UI in Chrome by loading http://localhost:5050/home.</span></span> 

5. <span data-ttu-id="1805c-154">Click on "Import tutorials" (only needs to be done once).</span><span class="sxs-lookup"><span data-stu-id="1805c-154">Click on "Import tutorials" (only needs to be done once).</span></span>  <span data-ttu-id="1805c-155">This will take about a minute and will copy the Conversation Learner models for all the tutorials into your Conversation Learner account.</span><span class="sxs-lookup"><span data-stu-id="1805c-155">This will take about a minute and will copy the Conversation Learner models for all the tutorials into your Conversation Learner account.</span></span>

6. <span data-ttu-id="1805c-156">Click on the demo model in the Conversation Learner UI that corresponds to the demo you started.</span><span class="sxs-lookup"><span data-stu-id="1805c-156">Click on the demo model in the Conversation Learner UI that corresponds to the demo you started.</span></span>

<span data-ttu-id="1805c-157">Source files for the demos are in `cl-bot-01/src/demos`</span><span class="sxs-lookup"><span data-stu-id="1805c-157">Source files for the demos are in `cl-bot-01/src/demos`</span></span>

## <a name="create-a-bot-which-includes-back-end-code"></a><span data-ttu-id="1805c-158">Create a bot which includes back-end code</span><span class="sxs-lookup"><span data-stu-id="1805c-158">Create a bot which includes back-end code</span></span>

1. <span data-ttu-id="1805c-159">If you have the Conversation Learner web UI open, return to the list of models at http://localhost:5050/home.</span><span class="sxs-lookup"><span data-stu-id="1805c-159">If you have the Conversation Learner web UI open, return to the list of models at http://localhost:5050/home.</span></span>
    
2. <span data-ttu-id="1805c-160">If a bot is running (like `npm run demo-pizza`), stop it.</span><span class="sxs-lookup"><span data-stu-id="1805c-160">If a bot is running (like `npm run demo-pizza`), stop it.</span></span>  <span data-ttu-id="1805c-161">You do not need to stop the UI process, or close the web browser.</span><span class="sxs-lookup"><span data-stu-id="1805c-161">You do not need to stop the UI process, or close the web browser.</span></span>

3. <span data-ttu-id="1805c-162">If desired, edit code in `cl-bot-01/src/app.ts`.</span><span class="sxs-lookup"><span data-stu-id="1805c-162">If desired, edit code in `cl-bot-01/src/app.ts`.</span></span>

4. <span data-ttu-id="1805c-163">Rebuild and re-start bot:</span><span class="sxs-lookup"><span data-stu-id="1805c-163">Rebuild and re-start bot:</span></span>

    ```bash    
    npm run build
    npm start
    ```

5. <span data-ttu-id="1805c-164">If you're not already, switch to the Conversation Learner web UI in Chrome by loading http://localhost:5050/home.</span><span class="sxs-lookup"><span data-stu-id="1805c-164">If you're not already, switch to the Conversation Learner web UI in Chrome by loading http://localhost:5050/home.</span></span> 

6. <span data-ttu-id="1805c-165">Create a new Conversation Learner model in the UI, and start teaching.</span><span class="sxs-lookup"><span data-stu-id="1805c-165">Create a new Conversation Learner model in the UI, and start teaching.</span></span>

7. <span data-ttu-id="1805c-166">To make code changes in `cl-bot-01/src/app.ts`, repeat the steps above, starting from step 2.</span><span class="sxs-lookup"><span data-stu-id="1805c-166">To make code changes in `cl-bot-01/src/app.ts`, repeat the steps above, starting from step 2.</span></span>

## <a name="vscode"></a><span data-ttu-id="1805c-167">VSCode</span><span class="sxs-lookup"><span data-stu-id="1805c-167">VSCode</span></span>

<span data-ttu-id="1805c-168">In VSCode, there are run configurations for each demo, and for the "Empty bot" in `cl-bot-01/src/app.ts`.</span><span class="sxs-lookup"><span data-stu-id="1805c-168">In VSCode, there are run configurations for each demo, and for the "Empty bot" in `cl-bot-01/src/app.ts`.</span></span>  <span data-ttu-id="1805c-169">Open the `cl-bot-01` folder in VSCode.</span><span class="sxs-lookup"><span data-stu-id="1805c-169">Open the `cl-bot-01` folder in VSCode.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="1805c-170">Advanced configuration</span><span class="sxs-lookup"><span data-stu-id="1805c-170">Advanced configuration</span></span>

<span data-ttu-id="1805c-171">There is a template `.env.example` file shows what environment variables you may set to configure the samples.</span><span class="sxs-lookup"><span data-stu-id="1805c-171">There is a template `.env.example` file shows what environment variables you may set to configure the samples.</span></span>

<span data-ttu-id="1805c-172">You can adjust these ports to avoid conflicts between other services running on your machine by adding a `.env` file to root of project:</span><span class="sxs-lookup"><span data-stu-id="1805c-172">You can adjust these ports to avoid conflicts between other services running on your machine by adding a `.env` file to root of project:</span></span>

```bash
cp .env.example .env
```

<span data-ttu-id="1805c-173">This uses the standard configuration, which lets you run your bot locally, and start using Conversation Learner.</span><span class="sxs-lookup"><span data-stu-id="1805c-173">This uses the standard configuration, which lets you run your bot locally, and start using Conversation Learner.</span></span>  <span data-ttu-id="1805c-174">(Later on, to deploy your bot to the Bot Framework, some edits to this file will be needed.)</span><span class="sxs-lookup"><span data-stu-id="1805c-174">(Later on, to deploy your bot to the Bot Framework, some edits to this file will be needed.)</span></span>

## <a name="support"></a><span data-ttu-id="1805c-175">Support</span><span class="sxs-lookup"><span data-stu-id="1805c-175">Support</span></span>

- <span data-ttu-id="1805c-176">Tag questions on [Stack Overflow](https://stackoverflow.com) with "microsoft cognitive"</span><span class="sxs-lookup"><span data-stu-id="1805c-176">Tag questions on [Stack Overflow](https://stackoverflow.com) with "microsoft cognitive"</span></span>
- <span data-ttu-id="1805c-177">Request a feature on our [User Voice page](https://aka.ms/conversation-learner-uservoice)</span><span class="sxs-lookup"><span data-stu-id="1805c-177">Request a feature on our [User Voice page](https://aka.ms/conversation-learner-uservoice)</span></span>
- <span data-ttu-id="1805c-178">Open an issue on our [github repo](https://github.com/Microsoft/ConversationLearner-Samples)</span><span class="sxs-lookup"><span data-stu-id="1805c-178">Open an issue on our [github repo](https://github.com/Microsoft/ConversationLearner-Samples)</span></span>

## <a name="contributing"></a><span data-ttu-id="1805c-179">Contributing</span><span class="sxs-lookup"><span data-stu-id="1805c-179">Contributing</span></span>

<span data-ttu-id="1805c-180">This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).</span><span class="sxs-lookup"><span data-stu-id="1805c-180">This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).</span></span> <span data-ttu-id="1805c-181">For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.</span><span class="sxs-lookup"><span data-stu-id="1805c-181">For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.</span></span>

## <a name="source-repositories"></a><span data-ttu-id="1805c-182">Source repositories</span><span class="sxs-lookup"><span data-stu-id="1805c-182">Source repositories</span></span>

- [<span data-ttu-id="1805c-183">conversationlearner-samples</span><span class="sxs-lookup"><span data-stu-id="1805c-183">conversationlearner-samples</span></span>](https://github.com/Microsoft/ConversationLearner-Samples)
- [<span data-ttu-id="1805c-184">conversationlearner-sdk</span><span class="sxs-lookup"><span data-stu-id="1805c-184">conversationlearner-sdk</span></span>](https://github.com/Microsoft/ConversationLearner-SDK)
- [<span data-ttu-id="1805c-185">conversationlearner-models</span><span class="sxs-lookup"><span data-stu-id="1805c-185">conversationlearner-models</span></span>](https://github.com/Microsoft/ConversationLearner-Models)
- [<span data-ttu-id="1805c-186">conversationlearner-ui</span><span class="sxs-lookup"><span data-stu-id="1805c-186">conversationlearner-ui</span></span>](https://github.com/Microsoft/ConversationLearner-UI)
- [<span data-ttu-id="1805c-187">conversationlearner-webchat</span><span class="sxs-lookup"><span data-stu-id="1805c-187">conversationlearner-webchat</span></span>](https://github.com/Microsoft/ConversationLearner-WebChat)

## <a name="next-steps"></a><span data-ttu-id="1805c-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="1805c-188">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1805c-189">Hello world</span><span class="sxs-lookup"><span data-stu-id="1805c-189">Hello world</span></span>](./tutorials/1-hello-world.md)
