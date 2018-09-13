---
title: Quickstart - change model and train LUIS app using C# - Azure Cognitive Services | Microsoft Docs
description: In this C# quickstart, add example utterances to a Home Automation app and train the app. Example utterances are conversational user text mapped to an intent. By providing example utterances for intents, you teach LUIS what kinds of user-supplied text belongs to which intent.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/24/2018
ms.author: diberry
ms.openlocfilehash: 0c631fe281587c86f26643367aead14683b699df
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868448"
---
# <a name="quickstart-change-model-using-c"></a><span data-ttu-id="52d4a-105">Quickstart: Change model using C#</span><span class="sxs-lookup"><span data-stu-id="52d4a-105">Quickstart: Change model using C#</span></span>

[!INCLUDE [Quickstart introduction for change model](../../../includes/cognitive-services-luis-qs-change-model-intro-para.md)]

## <a name="prerequisites"></a><span data-ttu-id="52d4a-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="52d4a-106">Prerequisites</span></span>

[!INCLUDE [Quickstart prerequisites for changing model](../../../includes/cognitive-services-luis-qs-change-model-prereq.md)]
* <span data-ttu-id="52d4a-107">Latest [**Visual Studio Community edition**](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="52d4a-107">Latest [**Visual Studio Community edition**](https://www.visualstudio.com/downloads/).</span></span>
* <span data-ttu-id="52d4a-108">C# programming language installed.</span><span class="sxs-lookup"><span data-stu-id="52d4a-108">C# programming language installed.</span></span>
* <span data-ttu-id="52d4a-109">[JsonFormatterPlus](https://www.nuget.org/packages/JsonFormatterPlus) and [CommandLine](https://www.nuget.org/packages/CommandLineParser/) NuGet packages</span><span class="sxs-lookup"><span data-stu-id="52d4a-109">[JsonFormatterPlus](https://www.nuget.org/packages/JsonFormatterPlus) and [CommandLine](https://www.nuget.org/packages/CommandLineParser/) NuGet packages</span></span>

[!INCLUDE [Code is available in LUIS-Samples Github repo](../../../includes/cognitive-services-luis-qs-change-model-luis-repo-note.md)]

## <a name="example-utterances-json-file"></a><span data-ttu-id="52d4a-110">Example utterances JSON file</span><span class="sxs-lookup"><span data-stu-id="52d4a-110">Example utterances JSON file</span></span>

[!INCLUDE [Quickstart explanation of example utterance JSON file](../../../includes/cognitive-services-luis-qs-change-model-json-ex-utt.md)]

## <a name="create-quickstart-code"></a><span data-ttu-id="52d4a-111">Create quickstart code</span><span class="sxs-lookup"><span data-stu-id="52d4a-111">Create quickstart code</span></span> 

<span data-ttu-id="52d4a-112">In Visual Studio, create a new **Windows Classic Desktop Console** app using the .Net Framework.</span><span class="sxs-lookup"><span data-stu-id="52d4a-112">In Visual Studio, create a new **Windows Classic Desktop Console** app using the .Net Framework.</span></span> 

![Visual Studio project type](./media/luis-quickstart-cs-add-utterance/vs-project-type.png)

### <a name="add-the-systemweb-dependency"></a><span data-ttu-id="52d4a-114">Add the System.Web dependency</span><span class="sxs-lookup"><span data-stu-id="52d4a-114">Add the System.Web dependency</span></span>

<span data-ttu-id="52d4a-115">The Visual Studio project needs **System.Web**.</span><span class="sxs-lookup"><span data-stu-id="52d4a-115">The Visual Studio project needs **System.Web**.</span></span> <span data-ttu-id="52d4a-116">In the Solution Explorer, right-click on **References** and select **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="52d4a-116">In the Solution Explorer, right-click on **References** and select **Add Reference**.</span></span>

![Add System.web reference](./media/luis-quickstart-cs-add-utterance/system.web.png)

### <a name="add-other-dependencies"></a><span data-ttu-id="52d4a-118">Add other dependencies</span><span class="sxs-lookup"><span data-stu-id="52d4a-118">Add other dependencies</span></span>

<span data-ttu-id="52d4a-119">The Visual Studio project needs **JsonFormatterPlus** and **CommandLineParser**.</span><span class="sxs-lookup"><span data-stu-id="52d4a-119">The Visual Studio project needs **JsonFormatterPlus** and **CommandLineParser**.</span></span> <span data-ttu-id="52d4a-120">In the Solution Explorer, right-click on **References** and select **Manage NuGet Packages...**. Search for and add each of the two packages.</span><span class="sxs-lookup"><span data-stu-id="52d4a-120">In the Solution Explorer, right-click on **References** and select **Manage NuGet Packages...**. Search for and add each of the two packages.</span></span> 

![Add 3rd party dependencies](./media/luis-quickstart-cs-add-utterance/add-dependencies.png)


### <a name="write-the-c-code"></a><span data-ttu-id="52d4a-122">Write the C# code</span><span class="sxs-lookup"><span data-stu-id="52d4a-122">Write the C# code</span></span>
<span data-ttu-id="52d4a-123">The **Program.cs** file should be:</span><span class="sxs-lookup"><span data-stu-id="52d4a-123">The **Program.cs** file should be:</span></span>

```CSharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp3
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="52d4a-124">Add the dependencies.</span><span class="sxs-lookup"><span data-stu-id="52d4a-124">Add the dependencies.</span></span>

   [!code-csharp[Add the dependencies](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=1-11 "Add the dependencies")]


<span data-ttu-id="52d4a-125">Add the LUIS IDs and strings to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="52d4a-125">Add the LUIS IDs and strings to the **Program** class.</span></span>

   [!code-csharp[Add the LUIS IDs and strings](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=19-30&dedent=8 "Add the LUIS IDs and strings")]

<span data-ttu-id="52d4a-126">Add class to manage command-line parameters to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="52d4a-126">Add class to manage command-line parameters to the **Program** class.</span></span>

   [!code-csharp[Add class to manage command line parameters.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=32-46 "Add class to manage command-line parameters.")]

<span data-ttu-id="52d4a-127">Add the GET request method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="52d4a-127">Add the GET request method to the **Program** class.</span></span>

   [!code-csharp[Add the GET request.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=49-59 "Add the GET request.")]


<span data-ttu-id="52d4a-128">Add the POST request method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="52d4a-128">Add the POST request method to the **Program** class.</span></span> 

   [!code-csharp[Add the POST request.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=60-76 "Add the POST request.")]

<span data-ttu-id="52d4a-129">Add example utterances from file method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="52d4a-129">Add example utterances from file method to the **Program** class.</span></span>

   [!code-csharp[Add example utterances from file.
](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=77-86 "Add example utterances from file.
")]

<span data-ttu-id="52d4a-130">After the changes are applied to the model, train the model.</span><span class="sxs-lookup"><span data-stu-id="52d4a-130">After the changes are applied to the model, train the model.</span></span> <span data-ttu-id="52d4a-131">Add method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="52d4a-131">Add method to the **Program** class.</span></span>

   [!code-csharp[After the changes are applied to the model, train the model.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=87-96 "After the changes are applied to the model, train the model.")]

<span data-ttu-id="52d4a-132">Training may not complete immediately, check status to verify training is complete.</span><span class="sxs-lookup"><span data-stu-id="52d4a-132">Training may not complete immediately, check status to verify training is complete.</span></span> <span data-ttu-id="52d4a-133">Add method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="52d4a-133">Add method to the **Program** class.</span></span>

   [!code-csharp[Training may not complete immediately, check status to verify training is complete.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=97-103 "Training may not complete immediately, check status to verify training is complete.")]

<span data-ttu-id="52d4a-134">To manage command-line arguments, add the main code.</span><span class="sxs-lookup"><span data-stu-id="52d4a-134">To manage command-line arguments, add the main code.</span></span> <span data-ttu-id="52d4a-135">Add method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="52d4a-135">Add method to the **Program** class.</span></span>

   [!code-csharp[To manage command line arguments, add the main code.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=104-137 "To manage command-line arguments, add the main code.")]

### <a name="copy-utterancesjson-to-output-directory"></a><span data-ttu-id="52d4a-136">Copy utterances.json to output directory</span><span class="sxs-lookup"><span data-stu-id="52d4a-136">Copy utterances.json to output directory</span></span>

<span data-ttu-id="52d4a-137">In the Solution Explorer, right-click the `utterances.json` and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="52d4a-137">In the Solution Explorer, right-click the `utterances.json` and select **Properties**.</span></span> <span data-ttu-id="52d4a-138">In the properties windows, mark the **Build Action** of `Content`, and the **Copy to Output Directory** of `Copy Always`.</span><span class="sxs-lookup"><span data-stu-id="52d4a-138">In the properties windows, mark the **Build Action** of `Content`, and the **Copy to Output Directory** of `Copy Always`.</span></span>  

![Mark the JSON file as content](./media/luis-quickstart-cs-add-utterance/content-properties.png)

## <a name="build-code"></a><span data-ttu-id="52d4a-140">Build code</span><span class="sxs-lookup"><span data-stu-id="52d4a-140">Build code</span></span>

<span data-ttu-id="52d4a-141">Build the code in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52d4a-141">Build the code in Visual Studio.</span></span> 

## <a name="run-code"></a><span data-ttu-id="52d4a-142">Run code</span><span class="sxs-lookup"><span data-stu-id="52d4a-142">Run code</span></span>

<span data-ttu-id="52d4a-143">In the project's /bin/Debug directory, run the application from a command line.</span><span class="sxs-lookup"><span data-stu-id="52d4a-143">In the project's /bin/Debug directory, run the application from a command line.</span></span> 

```CMD
ConsoleApp\bin\Debug> ConsoleApp1.exe --add utterances.json --train --status
```

<span data-ttu-id="52d4a-144">This command-line displays the results of calling the add utterances API.</span><span class="sxs-lookup"><span data-stu-id="52d4a-144">This command-line displays the results of calling the add utterances API.</span></span> 

[!INCLUDE [Quickstart response from API calls](../../../includes/cognitive-services-luis-qs-change-model-json-results.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="52d4a-145">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="52d4a-145">Clean up resources</span></span>
<span data-ttu-id="52d4a-146">When you are done with the quickstart, remove all the files created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="52d4a-146">When you are done with the quickstart, remove all the files created in this quickstart.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="52d4a-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="52d4a-147">Next steps</span></span>
> [!div class="nextstepaction"] 
> [<span data-ttu-id="52d4a-148">Build a LUIS app programmatically</span><span class="sxs-lookup"><span data-stu-id="52d4a-148">Build a LUIS app programmatically</span></span>](luis-tutorial-node-import-utterances-csv.md) 