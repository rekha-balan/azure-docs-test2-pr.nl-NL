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
# <a name="quickstart-change-model-using-c"></a>Quickstart: Change model using C#

[!INCLUDE [Quickstart introduction for change model](../../../includes/cognitive-services-luis-qs-change-model-intro-para.md)]

## <a name="prerequisites"></a>Prerequisites

[!INCLUDE [Quickstart prerequisites for changing model](../../../includes/cognitive-services-luis-qs-change-model-prereq.md)]
* Latest [**Visual Studio Community edition**](https://www.visualstudio.com/downloads/).
* C# programming language installed.
* [JsonFormatterPlus](https://www.nuget.org/packages/JsonFormatterPlus) and [CommandLine](https://www.nuget.org/packages/CommandLineParser/) NuGet packages

[!INCLUDE [Code is available in LUIS-Samples Github repo](../../../includes/cognitive-services-luis-qs-change-model-luis-repo-note.md)]

## <a name="example-utterances-json-file"></a>Example utterances JSON file

[!INCLUDE [Quickstart explanation of example utterance JSON file](../../../includes/cognitive-services-luis-qs-change-model-json-ex-utt.md)]

## <a name="create-quickstart-code"></a>Create quickstart code 

In Visual Studio, create a new **Windows Classic Desktop Console** app using the .Net Framework. 

![Visual Studio project type](./media/luis-quickstart-cs-add-utterance/vs-project-type.png)

### <a name="add-the-systemweb-dependency"></a>Add the System.Web dependency

The Visual Studio project needs **System.Web**. In the Solution Explorer, right-click on **References** and select **Add Reference**.

![Add System.web reference](./media/luis-quickstart-cs-add-utterance/system.web.png)

### <a name="add-other-dependencies"></a>Add other dependencies

The Visual Studio project needs **JsonFormatterPlus** and **CommandLineParser**. In the Solution Explorer, right-click on **References** and select **Manage NuGet Packages...**. Search for and add each of the two packages. 

![Add 3rd party dependencies](./media/luis-quickstart-cs-add-utterance/add-dependencies.png)


### <a name="write-the-c-code"></a>Write the C# code
The **Program.cs** file should be:

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

Add the dependencies.

   [!code-csharp[Add the dependencies](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=1-11 "Add the dependencies")]


Add the LUIS IDs and strings to the **Program** class.

   [!code-csharp[Add the LUIS IDs and strings](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=19-30&dedent=8 "Add the LUIS IDs and strings")]

Add class to manage command-line parameters to the **Program** class.

   [!code-csharp[Add class to manage command line parameters.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=32-46 "Add class to manage command-line parameters.")]

Add the GET request method to the **Program** class.

   [!code-csharp[Add the GET request.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=49-59 "Add the GET request.")]


Add the POST request method to the **Program** class. 

   [!code-csharp[Add the POST request.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=60-76 "Add the POST request.")]

Add example utterances from file method to the **Program** class.

   [!code-csharp[Add example utterances from file.
](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=77-86 "Add example utterances from file.
")]

After the changes are applied to the model, train the model. Add method to the **Program** class.

   [!code-csharp[After the changes are applied to the model, train the model.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=87-96 "After the changes are applied to the model, train the model.")]

Training may not complete immediately, check status to verify training is complete. Add method to the **Program** class.

   [!code-csharp[Training may not complete immediately, check status to verify training is complete.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=97-103 "Training may not complete immediately, check status to verify training is complete.")]

To manage command-line arguments, add the main code. Add method to the **Program** class.

   [!code-csharp[To manage command line arguments, add the main code.](~/samples-luis/documentation-samples/quickstarts/change-model/csharp/ConsoleApp1/Program.cs?range=104-137 "To manage command-line arguments, add the main code.")]

### <a name="copy-utterancesjson-to-output-directory"></a>Copy utterances.json to output directory

In the Solution Explorer, right-click the `utterances.json` and select **Properties**. In the properties windows, mark the **Build Action** of `Content`, and the **Copy to Output Directory** of `Copy Always`.  

![Mark the JSON file as content](./media/luis-quickstart-cs-add-utterance/content-properties.png)

## <a name="build-code"></a>Build code

Build the code in Visual Studio. 

## <a name="run-code"></a>Run code

In the project's /bin/Debug directory, run the application from a command line. 

```CMD
ConsoleApp\bin\Debug> ConsoleApp1.exe --add utterances.json --train --status
```

This command-line displays the results of calling the add utterances API. 

[!INCLUDE [Quickstart response from API calls](../../../includes/cognitive-services-luis-qs-change-model-json-results.md)]

## <a name="clean-up-resources"></a>Clean up resources
When you are done with the quickstart, remove all the files created in this quickstart. 

## <a name="next-steps"></a>Next steps
> [!div class="nextstepaction"] 
> [Build a LUIS app programmatically](luis-tutorial-node-import-utterances-csv.md) 