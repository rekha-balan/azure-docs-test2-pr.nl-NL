---
title: Quickstart change model and train LUIS app using Java - Azure Cognitive Services | Microsoft Docs
description: In this Java quickstart, add example utterances to a Home Automation app and train the app. Example utterances are conversational user text mapped to an intent. By providing example utterances for intents, you teach LUIS what kinds of user-supplied text belongs to which intent.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: diberry
ms.openlocfilehash: ddb22bce77dda55ad6e83efa8c0ca2c476f78836
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871104"
---
# <a name="quickstart-change-model-using-java"></a><span data-ttu-id="c5eb1-105">Quickstart: Change model using Java</span><span class="sxs-lookup"><span data-stu-id="c5eb1-105">Quickstart: Change model using Java</span></span> 

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="c5eb1-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c5eb1-106">Prerequisites</span></span>

[!INCLUDE [Quickstart prerequisites for endpoint](../../../includes/cognitive-services-luis-qs-change-model-prereq.md)]
* <span data-ttu-id="c5eb1-107">[JDK SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html)  (Java Development Kit, Standard Edition)</span><span class="sxs-lookup"><span data-stu-id="c5eb1-107">[JDK SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html)  (Java Development Kit, Standard Edition)</span></span>
* <span data-ttu-id="c5eb1-108">[Google's GSON JSON library](https://github.com/google/gson).</span><span class="sxs-lookup"><span data-stu-id="c5eb1-108">[Google's GSON JSON library](https://github.com/google/gson).</span></span>

[!INCLUDE [Quickstart note about code repository](../../../includes/cognitive-services-luis-qs-change-model-luis-repo-note.md)]

## <a name="example-utterances-json-file"></a><span data-ttu-id="c5eb1-109">Example utterances JSON file</span><span class="sxs-lookup"><span data-stu-id="c5eb1-109">Example utterances JSON file</span></span>

[!INCLUDE [Quickstart explanation of example utterance JSON file](../../../includes/cognitive-services-luis-qs-change-model-json-ex-utt.md)]

## <a name="create-quickstart-code"></a><span data-ttu-id="c5eb1-110">Create quickstart code</span><span class="sxs-lookup"><span data-stu-id="c5eb1-110">Create quickstart code</span></span>

1. <span data-ttu-id="c5eb1-111">Add the Java dependencies to the file named `AddUtterances.java`.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-111">Add the Java dependencies to the file named `AddUtterances.java`.</span></span>

   [!code-java[Java Dependencies](~/samples-luis/documentation-samples/quickstarts/change-model/java/AddUtterances.java?range=23-26 "Java Dependencies")]

2. <span data-ttu-id="c5eb1-112">Create `AddUtterances` class.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-112">Create `AddUtterances` class.</span></span> <span data-ttu-id="c5eb1-113">This class contains all code snippets that follow.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-113">This class contains all code snippets that follow.</span></span>

    ```Java
    public class AddUtterances {
        // Insert code here
    }
    ```

3. <span data-ttu-id="c5eb1-114">Add the LUIS constants to the class.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-114">Add the LUIS constants to the class.</span></span> <span data-ttu-id="c5eb1-115">Copy the following code and change to your authoring key, application ID, and version ID.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-115">Copy the following code and change to your authoring key, application ID, and version ID.</span></span>

   [!code-java[LUIS-based IDs](~/samples-luis/documentation-samples/quickstarts/change-model/java/AddUtterances.java?range=33-44 "LUIS-based IDs")]

4. <span data-ttu-id="c5eb1-116">Add the method to call into the LUIS API to the AddUtterances class.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-116">Add the method to call into the LUIS API to the AddUtterances class.</span></span> 

   [!code-java[HTTP request to LUIS](~/samples-luis/documentation-samples/quickstarts/change-model/java/AddUtterances.java?range=46-168 "HTTP request to LUIS")]

5. <span data-ttu-id="c5eb1-117">Add the method for the HTTP response from the LUIS API to the AddUtterances class.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-117">Add the method for the HTTP response from the LUIS API to the AddUtterances class.</span></span>

   [!code-java[HTTP response from LUIS](~/samples-luis/documentation-samples/quickstarts/change-model/java/AddUtterances.java?range=170-202 "HTTP response from LUIS")]

6. <span data-ttu-id="c5eb1-118">Add exception handling to the AddUtterances class.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-118">Add exception handling to the AddUtterances class.</span></span> 

   [!code-java[Exception Handling](~/samples-luis/documentation-samples/quickstarts/change-model/java/AddUtterances.java?range=205-243 "Exception Handling")]

7. <span data-ttu-id="c5eb1-119">Add the main function to the AddUtterances class.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-119">Add the main function to the AddUtterances class.</span></span>

   [!code-java[Add main function](~/samples-luis/documentation-samples/quickstarts/change-model/java/AddUtterances.java?range=245-278 "Add main function")]

## <a name="build-code"></a><span data-ttu-id="c5eb1-120">Build code</span><span class="sxs-lookup"><span data-stu-id="c5eb1-120">Build code</span></span>

<span data-ttu-id="c5eb1-121">Compile AddUtterance with the dependencies</span><span class="sxs-lookup"><span data-stu-id="c5eb1-121">Compile AddUtterance with the dependencies</span></span>

```CMD
> javac -classpath gson-2.8.2.jar AddUtterances.java
```

## <a name="run-code"></a><span data-ttu-id="c5eb1-122">Run code</span><span class="sxs-lookup"><span data-stu-id="c5eb1-122">Run code</span></span>
<span data-ttu-id="c5eb1-123">Calling `AddUtterance` with no arguments adds the LUIS utterances to the app, without training it.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-123">Calling `AddUtterance` with no arguments adds the LUIS utterances to the app, without training it.</span></span>

```CMD
> java -classpath .;gson-2.8.2.jar AddUtterances
```

<span data-ttu-id="c5eb1-124">This command-line displays the results of calling the add utterances API.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-124">This command-line displays the results of calling the add utterances API.</span></span> 

[!INCLUDE [Quickstart response from API calls](../../../includes/cognitive-services-luis-qs-change-model-json-results.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c5eb1-125">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c5eb1-125">Clean up resources</span></span>
<span data-ttu-id="c5eb1-126">When you are done with the quickstart, remove all the files created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="c5eb1-126">When you are done with the quickstart, remove all the files created in this quickstart.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c5eb1-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5eb1-127">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="c5eb1-128">Build a LUIS app programmatically</span><span class="sxs-lookup"><span data-stu-id="c5eb1-128">Build a LUIS app programmatically</span></span>](luis-tutorial-node-import-utterances-csv.md) 