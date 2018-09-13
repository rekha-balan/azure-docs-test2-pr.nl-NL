---
title: Quickstart change model and train LUIS app using Node.js - Azure Cognitive Services | Microsoft Docs
description: In this Node.js quickstart, add example utterances to a Home Automation app and train the app. Example utterances are conversational user text mapped to an intent. By providing example utterances for intents, you teach LUIS what kinds of user-supplied text belongs to which intent.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: diberry
ms.openlocfilehash: fbd8b467fa3894d9cf58e1c8cb78ee00ebd0965e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857714"
---
# <a name="quickstart-change-model-using-nodejs"></a><span data-ttu-id="1dad1-105">Quickstart: Change model using Node.js</span><span class="sxs-lookup"><span data-stu-id="1dad1-105">Quickstart: Change model using Node.js</span></span>

[!INCLUDE [Quickstart introduction for change model](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="1dad1-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1dad1-106">Prerequisites</span></span>

[!INCLUDE [Quickstart prerequisites for changing model](../../../includes/cognitive-services-luis-qs-change-model-prereq.md)]
* <span data-ttu-id="1dad1-107">Latest [**Node.js**](https://nodejs.org/en/download/) with NPM.</span><span class="sxs-lookup"><span data-stu-id="1dad1-107">Latest [**Node.js**](https://nodejs.org/en/download/) with NPM.</span></span>
* <span data-ttu-id="1dad1-108">NPM dependencies for this article: [**request**](https://www.npmjs.com/package/request), [**request-promise**](https://www.npmjs.com/package/request-promise), [**fs-extra**](https://www.npmjs.com/package/fs-extra).</span><span class="sxs-lookup"><span data-stu-id="1dad1-108">NPM dependencies for this article: [**request**](https://www.npmjs.com/package/request), [**request-promise**](https://www.npmjs.com/package/request-promise), [**fs-extra**](https://www.npmjs.com/package/fs-extra).</span></span>  
* <span data-ttu-id="1dad1-109">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="1dad1-109">[Visual Studio Code](https://code.visualstudio.com/).</span></span>

[!INCLUDE [Code is available in LUIS-Samples Github repo](../../../includes/cognitive-services-luis-qs-change-model-luis-repo-note.md)]

## <a name="example-utterances-json-file"></a><span data-ttu-id="1dad1-110">Example utterances JSON file</span><span class="sxs-lookup"><span data-stu-id="1dad1-110">Example utterances JSON file</span></span>

[!INCLUDE [Quickstart explanation of example utterance JSON file](../../../includes/cognitive-services-luis-qs-change-model-json-ex-utt.md)]

## <a name="create-quickstart-code"></a><span data-ttu-id="1dad1-111">Create quickstart code</span><span class="sxs-lookup"><span data-stu-id="1dad1-111">Create quickstart code</span></span> 

<span data-ttu-id="1dad1-112">Add the NPM dependencies to the file named `add-utterances.js`.</span><span class="sxs-lookup"><span data-stu-id="1dad1-112">Add the NPM dependencies to the file named `add-utterances.js`.</span></span>

   [!code-javascript[NPM Dependencies](~/samples-luis/documentation-samples/quickstarts/change-model/node/add-utterances.js?range=8-11 "NPM Dependencies")]

<span data-ttu-id="1dad1-113">Add the LUIS constants to the file.</span><span class="sxs-lookup"><span data-stu-id="1dad1-113">Add the LUIS constants to the file.</span></span> <span data-ttu-id="1dad1-114">Copy the following code and change to your authoring key, application ID, and version ID.</span><span class="sxs-lookup"><span data-stu-id="1dad1-114">Copy the following code and change to your authoring key, application ID, and version ID.</span></span>

   [!code-javascript[LUIS key and IDs](~/samples-luis/documentation-samples/quickstarts/change-model/node/add-utterances.js?range=13-22 "LUIS key and IDs")]

<span data-ttu-id="1dad1-115">Add the name and location of the upload file containing your utterances.</span><span class="sxs-lookup"><span data-stu-id="1dad1-115">Add the name and location of the upload file containing your utterances.</span></span> 

   [!code-javascript[Add upload file](~/samples-luis/documentation-samples/quickstarts/change-model/node/add-utterances.js?range=24-26 "Add upload file")]

<span data-ttu-id="1dad1-116">Add method and object for `addUtterance` function.</span><span class="sxs-lookup"><span data-stu-id="1dad1-116">Add method and object for `addUtterance` function.</span></span>

   [!code-javascript[Add configuration information for adding utterance](~/samples-luis/documentation-samples/quickstarts/change-model/node/add-utterances.js?range=28-67 "Add configuration information for adding utterance")]

<span data-ttu-id="1dad1-117">Add method and object for `train` function.</span><span class="sxs-lookup"><span data-stu-id="1dad1-117">Add method and object for `train` function.</span></span>

   [!code-javascript[Add configuration information for training LUIS](~/samples-luis/documentation-samples/quickstarts/change-model/node/add-utterances.js?range=69-101 "Add configuration information for training LUIS")]

<span data-ttu-id="1dad1-118">Add the function `sendUtteranceToApi` to send and receive HTTP calls.</span><span class="sxs-lookup"><span data-stu-id="1dad1-118">Add the function `sendUtteranceToApi` to send and receive HTTP calls.</span></span> 

   [!code-javascript[Send the HTTP request](~/samples-luis/documentation-samples/quickstarts/change-model/node/add-utterances.js?range=103-119 "Send the HTTP request")]

<span data-ttu-id="1dad1-119">Add the **main** code that chooses which action.</span><span class="sxs-lookup"><span data-stu-id="1dad1-119">Add the **main** code that chooses which action.</span></span>

   [!code-javascript[Main function](~/samples-luis/documentation-samples/quickstarts/change-model/node/add-utterances.js?range=121-143 "Main function")]

### <a name="install-dependencies"></a><span data-ttu-id="1dad1-120">Install dependencies</span><span class="sxs-lookup"><span data-stu-id="1dad1-120">Install dependencies</span></span>

<span data-ttu-id="1dad1-121">Create `package.json` file with the following text:</span><span class="sxs-lookup"><span data-stu-id="1dad1-121">Create `package.json` file with the following text:</span></span>

   [!code-json[Package.json](~/samples-luis/documentation-samples/quickstarts/change-model/node/package.json "Package.json")]

<span data-ttu-id="1dad1-122">On the command-line, from the directory that has the package.json, install dependencies with NPM: `npm install`.</span><span class="sxs-lookup"><span data-stu-id="1dad1-122">On the command-line, from the directory that has the package.json, install dependencies with NPM: `npm install`.</span></span>

## <a name="run-code"></a><span data-ttu-id="1dad1-123">Run code</span><span class="sxs-lookup"><span data-stu-id="1dad1-123">Run code</span></span>

<span data-ttu-id="1dad1-124">Run the application from a command-line with Node.js.</span><span class="sxs-lookup"><span data-stu-id="1dad1-124">Run the application from a command-line with Node.js.</span></span>

<span data-ttu-id="1dad1-125">Calling `npm start`adds the utterances, trains, and gets training status.</span><span class="sxs-lookup"><span data-stu-id="1dad1-125">Calling `npm start`adds the utterances, trains, and gets training status.</span></span>

```CMD
> npm start 
```

<span data-ttu-id="1dad1-126">This command-line displays the results of calling the add utterances API.</span><span class="sxs-lookup"><span data-stu-id="1dad1-126">This command-line displays the results of calling the add utterances API.</span></span> 

[!INCLUDE [Quickstart response from API calls](../../../includes/cognitive-services-luis-qs-change-model-json-results.md)]


## <a name="clean-up-resources"></a><span data-ttu-id="1dad1-127">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1dad1-127">Clean up resources</span></span>

<span data-ttu-id="1dad1-128">When you are done with the quickstart, remove all the files created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="1dad1-128">When you are done with the quickstart, remove all the files created in this quickstart.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1dad1-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="1dad1-129">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="1dad1-130">Build a LUIS app programmatically</span><span class="sxs-lookup"><span data-stu-id="1dad1-130">Build a LUIS app programmatically</span></span>](luis-tutorial-node-import-utterances-csv.md)