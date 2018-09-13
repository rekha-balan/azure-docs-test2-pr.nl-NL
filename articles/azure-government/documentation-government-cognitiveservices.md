---
title: Cognitive Services on Azure Government | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: yujhongmicrosoft
manager: zakramer
ms.assetid: cba97199-851d-43ae-a75a-c601f3f81601
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 10/09/2017
ms.author: yujhong
ms.openlocfilehash: 32fb046133f2678a3e54a3cec80fd04ffaa48927
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866091"
---
# <a name="cognitive-services-on-azure-government--computer-vision-face-translator-text-apis"></a><span data-ttu-id="a4224-103">Cognitive Services on Azure Government – Computer Vision, Face, Translator Text APIs</span><span class="sxs-lookup"><span data-stu-id="a4224-103">Cognitive Services on Azure Government – Computer Vision, Face, Translator Text APIs</span></span>

<span data-ttu-id="a4224-104">To see an overview of Cognitive Services on Azure Government, [click here](documentation-government-services-aiandcognitiveservices.md).</span><span class="sxs-lookup"><span data-stu-id="a4224-104">To see an overview of Cognitive Services on Azure Government, [click here](documentation-government-services-aiandcognitiveservices.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4224-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4224-105">Prerequisites</span></span>
* <span data-ttu-id="a4224-106">Install and Configure [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.4.0)</span><span class="sxs-lookup"><span data-stu-id="a4224-106">Install and Configure [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.4.0)</span></span>
* <span data-ttu-id="a4224-107">Connect [PowerShell with Azure Government](documentation-government-get-started-connect-with-ps.md)</span><span class="sxs-lookup"><span data-stu-id="a4224-107">Connect [PowerShell with Azure Government](documentation-government-get-started-connect-with-ps.md)</span></span>

## <a name="part-1-provision-cognitive-services-accounts"></a><span data-ttu-id="a4224-108">Part 1: Provision Cognitive Services Accounts</span><span class="sxs-lookup"><span data-stu-id="a4224-108">Part 1: Provision Cognitive Services Accounts</span></span>

<span data-ttu-id="a4224-109">In order to access any of the Cognitive Services APIs, you must first provision a Cognitive Services account for each of the APIs you want to access.</span><span class="sxs-lookup"><span data-stu-id="a4224-109">In order to access any of the Cognitive Services APIs, you must first provision a Cognitive Services account for each of the APIs you want to access.</span></span> <span data-ttu-id="a4224-110">**Cognitive Services is not yet supported in the Azure Government Portal**, but you can use Azure PowerShell to access the APIs and services.</span><span class="sxs-lookup"><span data-stu-id="a4224-110">**Cognitive Services is not yet supported in the Azure Government Portal**, but you can use Azure PowerShell to access the APIs and services.</span></span> 

> [!NOTE]
> <span data-ttu-id="a4224-111">You must go through the process of creating an account and retrieving a key(explained below) **for each** of the APIs you want to access.</span><span class="sxs-lookup"><span data-stu-id="a4224-111">You must go through the process of creating an account and retrieving a key(explained below) **for each** of the APIs you want to access.</span></span>
> 
> 

1. <span data-ttu-id="a4224-112">Make sure that you have the **Cognitive Services resource provider registered on your account**.</span><span class="sxs-lookup"><span data-stu-id="a4224-112">Make sure that you have the **Cognitive Services resource provider registered on your account**.</span></span> 

<span data-ttu-id="a4224-113">You can do this by **running the following PowerShell command:**</span><span class="sxs-lookup"><span data-stu-id="a4224-113">You can do this by **running the following PowerShell command:**</span></span>

   ```PowerShell
   Get-AzureRmResourceProvider
   ```
   <span data-ttu-id="a4224-114">If you do **not see `Microsoft.CognitiveServices`**, you have to register the resource provider by **running the following command**:</span><span class="sxs-lookup"><span data-stu-id="a4224-114">If you do **not see `Microsoft.CognitiveServices`**, you have to register the resource provider by **running the following command**:</span></span>
   ```PowerShell
   Register-AzureRmResourceProvider -ProviderNamespace Microsoft.CognitiveServices
   ```
2. <span data-ttu-id="a4224-115">In the PowerShell command below, replace "rg-name", "name-of-your-api", and "location-of-resourcegroup" with your relevant account information.</span><span class="sxs-lookup"><span data-stu-id="a4224-115">In the PowerShell command below, replace "rg-name", "name-of-your-api", and "location-of-resourcegroup" with your relevant account information.</span></span> 

   <span data-ttu-id="a4224-116">Replace the "type of API" tag with any of the three following APIs you want to access:</span><span class="sxs-lookup"><span data-stu-id="a4224-116">Replace the "type of API" tag with any of the three following APIs you want to access:</span></span>
       * <span data-ttu-id="a4224-117">ComputerVision</span><span class="sxs-lookup"><span data-stu-id="a4224-117">ComputerVision</span></span>
       * <span data-ttu-id="a4224-118">Face</span><span class="sxs-lookup"><span data-stu-id="a4224-118">Face</span></span>
       * <span data-ttu-id="a4224-119">TextTranslation</span><span class="sxs-lookup"><span data-stu-id="a4224-119">TextTranslation</span></span>

   ```PowerShell
   New-AzureRmCognitiveServicesAccount -ResourceGroupName 'rg-name' -name 'name-of-your-api' -Type <type of API> -SkuName S0 -Location 'location-of-resourcegroup'
   ```
   <span data-ttu-id="a4224-120">Example:</span><span class="sxs-lookup"><span data-stu-id="a4224-120">Example:</span></span> 

   ```PowerShell
   New-AzureRmCognitiveServicesAccount -ResourceGroupName 'resourcegrouptest' -name 'myFaceAPI' -Type Face -SkuName S0 -Location 'usgovvirginia'
   ```

   <span data-ttu-id="a4224-121">After you run the command, you should see something like this:</span><span class="sxs-lookup"><span data-stu-id="a4224-121">After you run the command, you should see something like this:</span></span> 

   ![cog1](./media/documentation-government-cognitiveservices-img1.png)

3. <span data-ttu-id="a4224-123">Copy and save the "Endpoint" attribute somewhere as you will need it when making calls to the API.</span><span class="sxs-lookup"><span data-stu-id="a4224-123">Copy and save the "Endpoint" attribute somewhere as you will need it when making calls to the API.</span></span> 

### <a name="retrieve-account-key"></a><span data-ttu-id="a4224-124">Retrieve Account Key</span><span class="sxs-lookup"><span data-stu-id="a4224-124">Retrieve Account Key</span></span>

<span data-ttu-id="a4224-125">You must retrieve an account key to access the specific API.</span><span class="sxs-lookup"><span data-stu-id="a4224-125">You must retrieve an account key to access the specific API.</span></span> 

<span data-ttu-id="a4224-126">In the PowerShell command below, replace the "youraccountname" tag with the name that you gave the Account that you created above.</span><span class="sxs-lookup"><span data-stu-id="a4224-126">In the PowerShell command below, replace the "youraccountname" tag with the name that you gave the Account that you created above.</span></span> <span data-ttu-id="a4224-127">Replace the 'rg-name' tag with the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="a4224-127">Replace the 'rg-name' tag with the name of your resource group.</span></span>

```PowerShell
Get-AzureRmCognitiveServicesAccountKey -Name <youraccountname> -ResourceGroupName 'rg-name'
```

<span data-ttu-id="a4224-128">Example:</span><span class="sxs-lookup"><span data-stu-id="a4224-128">Example:</span></span>
```PowerShell
Get-AzureRmCognitiveServicesAccountKey -Name myFaceAPI -ResourceGroupName 'resourcegrouptest'
```
<span data-ttu-id="a4224-129">Copy and save the first key somewhere as you will need it to make calls to the API.</span><span class="sxs-lookup"><span data-stu-id="a4224-129">Copy and save the first key somewhere as you will need it to make calls to the API.</span></span>

![cog2](./media/documentation-government-cognitiveservices-img2.png)

<span data-ttu-id="a4224-131">Now you are ready to make calls to the APIs.</span><span class="sxs-lookup"><span data-stu-id="a4224-131">Now you are ready to make calls to the APIs.</span></span> 

## <a name="part-2-api-quickstarts"></a><span data-ttu-id="a4224-132">Part 2: API Quickstarts</span><span class="sxs-lookup"><span data-stu-id="a4224-132">Part 2: API Quickstarts</span></span> 
<span data-ttu-id="a4224-133">The Quickstarts below will help you to get started with the APIs available through Cognitive Services in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="a4224-133">The Quickstarts below will help you to get started with the APIs available through Cognitive Services in Azure Government.</span></span>

## <a name="computer-vision-api"></a><span data-ttu-id="a4224-134">Computer Vision API</span><span class="sxs-lookup"><span data-stu-id="a4224-134">Computer Vision API</span></span>
### <a name="prerequisites"></a><span data-ttu-id="a4224-135">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4224-135">Prerequisites</span></span>

* <span data-ttu-id="a4224-136">Get the Microsoft Computer Vision API Windows SDK [here](https://github.com/Microsoft/Cognitive-vision-windows).</span><span class="sxs-lookup"><span data-stu-id="a4224-136">Get the Microsoft Computer Vision API Windows SDK [here](https://github.com/Microsoft/Cognitive-vision-windows).</span></span>

* <span data-ttu-id="a4224-137">Make sure Visual Studio has been installed:</span><span class="sxs-lookup"><span data-stu-id="a4224-137">Make sure Visual Studio has been installed:</span></span>
    -   <span data-ttu-id="a4224-138">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span><span class="sxs-lookup"><span data-stu-id="a4224-138">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>
    
    >[!NOTE] 
    > <span data-ttu-id="a4224-139">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio         2017 tools for Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a4224-139">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio         2017 tools for Azure Functions.</span></span> <span data-ttu-id="a4224-140">You can update the tools from the **Tools** menu under **Extensions and Updates...** >          **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span><span class="sxs-lookup"><span data-stu-id="a4224-140">You can update the tools from the **Tools** menu under **Extensions and Updates...** >          **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 
    >
    >
    
### <a name="variations"></a><span data-ttu-id="a4224-141">Variations</span><span class="sxs-lookup"><span data-stu-id="a4224-141">Variations</span></span>
* <span data-ttu-id="a4224-142">The URI for accessing the Face API in Azure Government is :</span><span class="sxs-lookup"><span data-stu-id="a4224-142">The URI for accessing the Face API in Azure Government is :</span></span>
   - `https://(resource-group-location).api.cognitive.microsoft.us/face/v1.0`
   - <span data-ttu-id="a4224-143">The main difference between this URI and the URI used in Commercial Azure is the ending of **.us** and the location at the beginning of the uri</span><span class="sxs-lookup"><span data-stu-id="a4224-143">The main difference between this URI and the URI used in Commercial Azure is the ending of **.us** and the location at the beginning of the uri</span></span>


### <span data-ttu-id="a4224-144">Analyze an Image With Computer Vision API using C# <a name="AnalyzeImage"> </a></span><span class="sxs-lookup"><span data-stu-id="a4224-144">Analyze an Image With Computer Vision API using C# <a name="AnalyzeImage"> </a></span></span>

<span data-ttu-id="a4224-145">With the [Analyze Image method](https://westcentralus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="a4224-145">With the [Analyze Image method](https://westcentralus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="a4224-146">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="a4224-146">You can upload an image or specify an image URL and choose which features to return, including:</span></span>
* <span data-ttu-id="a4224-147">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="a4224-147">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="a4224-148">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="a4224-148">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="a4224-149">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="a4224-149">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="a4224-150">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="a4224-150">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="a4224-151">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="a4224-151">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="a4224-152">The category defined in this [taxonomy](../cognitive-services/computer-vision/category-taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="a4224-152">The category defined in this [taxonomy](../cognitive-services/computer-vision/category-taxonomy.md).</span></span>
* <span data-ttu-id="a4224-153">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="a4224-153">Does the image contain adult or sexually suggestive content?</span></span>

### <a name="analyze-an-image-c-example-request"></a><span data-ttu-id="a4224-154">Analyze an image C# example request</span><span class="sxs-lookup"><span data-stu-id="a4224-154">Analyze an image C# example request</span></span>

1. <span data-ttu-id="a4224-155">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4224-155">Create a new Console solution in Visual Studio.</span></span>
2. <span data-ttu-id="a4224-156">Replace Program.cs with the following code.</span><span class="sxs-lookup"><span data-stu-id="a4224-156">Replace Program.cs with the following code.</span></span>
3. <span data-ttu-id="a4224-157">Change the `uriBase` to the "Endpoint" attribute that you saved from Part 1, and keep the "/analyze" after the endpoint.</span><span class="sxs-lookup"><span data-stu-id="a4224-157">Change the `uriBase` to the "Endpoint" attribute that you saved from Part 1, and keep the "/analyze" after the endpoint.</span></span>
4. <span data-ttu-id="a4224-158">Replace the `subscriptionKey` value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="a4224-158">Replace the `subscriptionKey` value with your valid subscription key.</span></span>
5. <span data-ttu-id="a4224-159">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a4224-159">Run the program.</span></span>

```csharp
using System;
using System.IO;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;

namespace VisionApp1
{
        static class Program
        {
            // **********************************************
            // *** Update or verify the following values. ***
            // **********************************************

            // Replace the subscriptionKey string value with your valid subscription key.
            const string subscriptionKey = "<subscription key>";

            //Copy and paste the "Endpoint" attribute that you saved before into the uriBase string "/analyze" at the end. 
            //Example: https://virginia.api.cognitive.microsoft.us/vision/v1.0/analyze
  
            const string uriBase = "<endpoint>/analyze";
            
            static void Main()
            {
                // Get the path and filename to process from the user.
                Console.WriteLine("Analyze an image:");
                Console.Write("Enter the path to an image you wish to analyze: ");
                string imageFilePath = Console.ReadLine();

                // Execute the REST API call.
                MakeAnalysisRequest(imageFilePath);

                Console.WriteLine("\nPlease wait a moment for the results to appear. Then, press Enter to exit...\n");
                Console.ReadLine();
            }


            /// <summary>
            /// Gets the analysis of the specified image file by using the Computer Vision REST API.
            /// </summary>
            /// <param name="imageFilePath">The image file.</param>
            static async void MakeAnalysisRequest(string imageFilePath)
            {
                HttpClient client = new HttpClient();

                // Request headers.
                client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", subscriptionKey);

                // Request parameters. A third optional parameter is "details".
                string requestParameters = "visualFeatures=Categories,Description,Color&language=en";

                // Assemble the URI for the REST API Call.
                string uri = uriBase + "?" + requestParameters;

                HttpResponseMessage response;

                // Request body. Posts a locally stored JPEG image.
                byte[] byteData = GetImageAsByteArray(imageFilePath);

                using (ByteArrayContent content = new ByteArrayContent(byteData))
                {
                    // This example uses content type "application/octet-stream".
                    // The other content types you can use are "application/json" and "multipart/form-data".
                    content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");

                    // Execute the REST API call.
                    response = await client.PostAsync(uri, content);

                    // Get the JSON response.
                    string contentString = await response.Content.ReadAsStringAsync();

                    // Display the JSON response.
                    Console.WriteLine("\nResponse:\n");
                    Console.WriteLine(JsonPrettyPrint(contentString));
                }
            }


            /// <summary>
            /// Returns the contents of the specified file as a byte array.
            /// </summary>
            /// <param name="imageFilePath">The image file to read.</param>
            /// <returns>The byte array of the image data.</returns>
            static byte[] GetImageAsByteArray(string imageFilePath)
            {
                FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
                BinaryReader binaryReader = new BinaryReader(fileStream);
                return binaryReader.ReadBytes((int)fileStream.Length);
            }


            /// <summary>
            /// Formats the given JSON string by adding line breaks and indents.
            /// </summary>
            /// <param name="json">The raw JSON string to format.</param>
            /// <returns>The formatted JSON string.</returns>
            static string JsonPrettyPrint(string json)
            {
                if (string.IsNullOrEmpty(json))
                    return string.Empty;

                json = json.Replace(Environment.NewLine, "").Replace("\t", "");

                StringBuilder sb = new StringBuilder();
                bool quote = false;
                bool ignore = false;
                int offset = 0;
                int indentLength = 3;

                foreach (char ch in json)
                {
                    switch (ch)
                    {
                        case '"':
                            if (!ignore) quote = !quote;
                            break;
                        case '\'':
                            if (quote) ignore = !ignore;
                            break;
                    }

                    if (quote)
                        sb.Append(ch);
                    else
                    {
                        switch (ch)
                        {
                            case '{':
                            case '[':
                                sb.Append(ch);
                                sb.Append(Environment.NewLine);
                                sb.Append(new string(' ', ++offset * indentLength));
                                break;
                            case '}':
                            case ']':
                                sb.Append(Environment.NewLine);
                                sb.Append(new string(' ', --offset * indentLength));
                                sb.Append(ch);
                                break;
                            case ',':
                                sb.Append(ch);
                                sb.Append(Environment.NewLine);
                                sb.Append(new string(' ', offset * indentLength));
                                break;
                            case ':':
                                sb.Append(ch);
                                sb.Append(' ');
                                break;
                            default:
                                if (ch != ' ') sb.Append(ch);
                                break;
                        }
                    }
                }

                return sb.ToString().Trim();
            }
        }
    }
```
### <a name="analyze-an-image-response"></a><span data-ttu-id="a4224-160">Analyze an Image response</span><span class="sxs-lookup"><span data-stu-id="a4224-160">Analyze an Image response</span></span>

<span data-ttu-id="a4224-161">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="a4224-161">A successful response is returned in JSON.</span></span> <span data-ttu-id="a4224-162">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="a4224-162">Following is an example of a successful response:</span></span>

```json

{
   "categories": [
      {
         "name": "people_baby",
         "score": 0.52734375
      },
      {
         "name": "people_young",
         "score": 0.4375
      }
   ],
   "description": {
      "tags": [
         "person",
         "indoor",
         "clothing",
         "woman",
         "white",
         "table",
         "food",
         "girl",
         "smiling",
         "posing",
         "holding",
         "black",
         "sitting",
         "young",
         "plate",
         "hair",
         "wearing",
         "cake",
         "large",
         "shirt",
         "dress",
         "eating",
         "standing",
         "blue"
      ],
      "captions": [
         {
            "text": "a woman posing for a picture",
            "confidence": 0.460196158842535
         }
      ]
   },
   "requestId": "7c20cc50-f5eb-453b-abb5-98378917431c",
   "metadata": {
      "width": 721,
      "height": 960,
      "format": "Jpeg"
   },
   "color": {
      "dominantColorForeground": "Black",
      "dominantColorBackground": "White",
      "dominantColors": [
         "White"
      ],
      "accentColor": "7C4F57",
      "isBWImg": false
   }
}
```
<span data-ttu-id="a4224-163">For more information, please see [public documentation](../cognitive-services/computer-vision/index.yml) and [public API documentation](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) for Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="a4224-163">For more information, please see [public documentation](../cognitive-services/computer-vision/index.yml) and [public API documentation](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) for Computer Vision API.</span></span>

## <a name="face-api"></a><span data-ttu-id="a4224-164">Face API</span><span class="sxs-lookup"><span data-stu-id="a4224-164">Face API</span></span>
### <a name="prerequisites"></a><span data-ttu-id="a4224-165">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4224-165">Prerequisites</span></span>
* <span data-ttu-id="a4224-166">Get the Microsoft Face API Windows SDK [here](https://www.nuget.org/packages/Microsoft.ProjectOxford.Face/)</span><span class="sxs-lookup"><span data-stu-id="a4224-166">Get the Microsoft Face API Windows SDK [here](https://www.nuget.org/packages/Microsoft.ProjectOxford.Face/)</span></span>

* <span data-ttu-id="a4224-167">Make sure Visual Studio has been installed:</span><span class="sxs-lookup"><span data-stu-id="a4224-167">Make sure Visual Studio has been installed:</span></span>
    -   <span data-ttu-id="a4224-168">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span><span class="sxs-lookup"><span data-stu-id="a4224-168">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>
    
    >[!NOTE] 
    > <span data-ttu-id="a4224-169">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio         2017 tools for Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a4224-169">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio         2017 tools for Azure Functions.</span></span> <span data-ttu-id="a4224-170">You can update the tools from the **Tools** menu under **Extensions and Updates...** >          **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span><span class="sxs-lookup"><span data-stu-id="a4224-170">You can update the tools from the **Tools** menu under **Extensions and Updates...** >          **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 
    >
    >
    
### <a name="variations"></a><span data-ttu-id="a4224-171">Variations</span><span class="sxs-lookup"><span data-stu-id="a4224-171">Variations</span></span> 
* <span data-ttu-id="a4224-172">The URI for accessing the Face API in Azure Government is :</span><span class="sxs-lookup"><span data-stu-id="a4224-172">The URI for accessing the Face API in Azure Government is :</span></span>
   - `https://(resource-group-location).api.cognitive.microsoft.us/face/v1.0`
   - <span data-ttu-id="a4224-173">The main difference between this URI and the URI used in Commercial Azure is the ending of **.us** and the location at the beginning of the uri</span><span class="sxs-lookup"><span data-stu-id="a4224-173">The main difference between this URI and the URI used in Commercial Azure is the ending of **.us** and the location at the beginning of the uri</span></span>

### <span data-ttu-id="a4224-174">Detect Faces in images with Face API using C# <a name="Detect"> </a></span><span class="sxs-lookup"><span data-stu-id="a4224-174">Detect Faces in images with Face API using C# <a name="Detect"> </a></span></span>
<span data-ttu-id="a4224-175">Use the [Face - Detect method](https://westcentralus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:</span><span class="sxs-lookup"><span data-stu-id="a4224-175">Use the [Face - Detect method](https://westcentralus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:</span></span>
* <span data-ttu-id="a4224-176">Face ID: Unique ID used in several Face API scenarios.</span><span class="sxs-lookup"><span data-stu-id="a4224-176">Face ID: Unique ID used in several Face API scenarios.</span></span> 
* <span data-ttu-id="a4224-177">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span><span class="sxs-lookup"><span data-stu-id="a4224-177">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span></span>
* <span data-ttu-id="a4224-178">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span><span class="sxs-lookup"><span data-stu-id="a4224-178">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span></span>
* <span data-ttu-id="a4224-179">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span><span class="sxs-lookup"><span data-stu-id="a4224-179">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span></span> 

### <a name="face-detect-c-example-request"></a><span data-ttu-id="a4224-180">Face detect C# example request</span><span class="sxs-lookup"><span data-stu-id="a4224-180">Face detect C# example request</span></span>

<span data-ttu-id="a4224-181">The sample is written in C# using the Face API client library.</span><span class="sxs-lookup"><span data-stu-id="a4224-181">The sample is written in C# using the Face API client library.</span></span> 

1. <span data-ttu-id="a4224-182">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4224-182">Create a new Console solution in Visual Studio.</span></span>
2. <span data-ttu-id="a4224-183">Replace Program.cs with the following code.</span><span class="sxs-lookup"><span data-stu-id="a4224-183">Replace Program.cs with the following code.</span></span>
3. <span data-ttu-id="a4224-184">Replace the `subscriptionKey` value with the key value that you retrieved above.</span><span class="sxs-lookup"><span data-stu-id="a4224-184">Replace the `subscriptionKey` value with the key value that you retrieved above.</span></span>
4. <span data-ttu-id="a4224-185">Change the `uriBase` value to the "Endpoint" attribute you retrieved above.</span><span class="sxs-lookup"><span data-stu-id="a4224-185">Change the `uriBase` value to the "Endpoint" attribute you retrieved above.</span></span>
5. <span data-ttu-id="a4224-186">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a4224-186">Run the program.</span></span>
6. <span data-ttu-id="a4224-187">Enter the path to an image on your hard drive.</span><span class="sxs-lookup"><span data-stu-id="a4224-187">Enter the path to an image on your hard drive.</span></span>

```csharp

using System;
using System.IO;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;

namespace FaceApp1
{

    static class Program
    {
        // **********************************************
        // *** Update or verify the following values. ***
        // **********************************************
         
        // Replace the subscriptionKey string value with your valid subscription key.
        const string subscriptionKey = "<subscription key>";

        //Copy and paste the "Endpoint" attribute that you saved before into the uriBase string "/detect" at the end. 
        //Example: https://virginia.api.cognitive.microsoft.us/face/v1.0/detect
        const string uriBase ="<endpoint>/detect";

        static void Main()
        {
            // Get the path and filename to process from the user.
            Console.WriteLine("Detect faces:");
            Console.Write("Enter the path to an image with faces that you wish to analzye: ");
            string imageFilePath = Console.ReadLine();

            // Execute the REST API call.
            MakeAnalysisRequest(imageFilePath);

            Console.WriteLine("\nPlease wait a moment for the results to appear. Then, press Enter to exit...\n");
            Console.ReadLine();
        }


        /// <summary>
        /// Gets the analysis of the specified image file by using the Computer Vision REST API.
        /// </summary>
        /// <param name="imageFilePath">The image file.</param>
        static async void MakeAnalysisRequest(string imageFilePath)
        {
            HttpClient client = new HttpClient();

            // Request headers.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", subscriptionKey);

            // Request parameters. A third optional parameter is "details".
            string requestParameters = "returnfaceId=true&returnfaceLandmarks=false&returnfaceAttributes=age,gender,headPose,smile,facialHair,glasses,emotion";

            // Assemble the URI for the REST API Call.
            string uri = uriBase + "?" + requestParameters;

            HttpResponseMessage response;

            // Request body. Posts a locally stored JPEG image.
            byte[] byteData = GetImageAsByteArray(imageFilePath);

            using (ByteArrayContent content = new ByteArrayContent(byteData))
            {
                // This example uses content type "application/octet-stream".
                // The other content types you can use are "application/json" and "multipart/form-data".
                content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");

                // Execute the REST API call.
                response = await client.PostAsync(uri, content);

                // Get the JSON response.
                string contentString = await response.Content.ReadAsStringAsync();

                // Display the JSON response.
                Console.WriteLine("\nResponse:\n");
                Console.WriteLine(JsonPrettyPrint(contentString));
            }
        }


        /// <summary>
        /// Returns the contents of the specified file as a byte array.
        /// </summary>
        /// <param name="imageFilePath">The image file to read.</param>
        /// <returns>The byte array of the image data.</returns>
        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }


        /// <summary>
        /// Formats the given JSON string by adding line breaks and indents.
        /// </summary>
        /// <param name="json">The raw JSON string to format.</param>
        /// <returns>The formatted JSON string.</returns>
        static string JsonPrettyPrint(string json)
        {
            if (string.IsNullOrEmpty(json))
                return string.Empty;

            json = json.Replace(Environment.NewLine, "").Replace("\t", "");

            StringBuilder sb = new StringBuilder();
            bool quote = false;
            bool ignore = false;
            int offset = 0;
            int indentLength = 3;

            foreach (char ch in json)
            {
                switch (ch)
                {
                    case '"':
                        if (!ignore) quote = !quote;
                        break;
                    case '\'':
                        if (quote) ignore = !ignore;
                        break;
                }

                if (quote)
                    sb.Append(ch);
                else
                {
                    switch (ch)
                    {
                        case '{':
                        case '[':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', ++offset * indentLength));
                            break;
                        case '}':
                        case ']':
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', --offset * indentLength));
                            sb.Append(ch);
                            break;
                        case ',':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', offset * indentLength));
                            break;
                        case ':':
                            sb.Append(ch);
                            sb.Append(' ');
                            break;
                        default:
                            if (ch != ' ') sb.Append(ch);
                            break;
                    }
                }
            }

            return sb.ToString().Trim();
        }
    }
}
```
### <a name="face-detect-response"></a><span data-ttu-id="a4224-188">Face detect response</span><span class="sxs-lookup"><span data-stu-id="a4224-188">Face detect response</span></span>

<span data-ttu-id="a4224-189">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="a4224-189">A successful response is returned in JSON.</span></span> <span data-ttu-id="a4224-190">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="a4224-190">Following is an example of a successful response:</span></span> 

```json
Response:
[
   {
      "faceId": "0ed7f4db-1207-40d4-be2e-84694e42d682",
      "faceRectangle": {
         "top": 60,
         "left": 83,
         "width": 361,
         "height": 361
      },
      "faceAttributes": {
         "smile": 0.284,
         "headPose": {
            "pitch": 0.0,
            "roll": -12.2,
            "yaw": -16.7
         },
         "gender": "female",
         "age": 16.5,
         "facialHair": {
            "moustache": 0.0,
            "beard": 0.0,
            "sideburns": 0.0
         },
         "glasses": "NoGlasses",
         "emotion": {
            "anger": 0.003,
            "contempt": 0.001,
            "disgust": 0.001,
            "fear": 0.002,
            "happiness": 0.284,
            "neutral": 0.694,
            "sadness": 0.012,
            "surprise": 0.004
         }
      }
   }
]
```
<span data-ttu-id="a4224-191">For more information, please see [public documentation](../cognitive-services/Face/index.yml), and [public API documentation](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) for Face API.</span><span class="sxs-lookup"><span data-stu-id="a4224-191">For more information, please see [public documentation](../cognitive-services/Face/index.yml), and [public API documentation](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) for Face API.</span></span>

## <a name="text-translation-api"></a><span data-ttu-id="a4224-192">Text Translation API</span><span class="sxs-lookup"><span data-stu-id="a4224-192">Text Translation API</span></span> 
### <a name="prerequisites"></a><span data-ttu-id="a4224-193">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4224-193">Prerequisites</span></span>

* <span data-ttu-id="a4224-194">Make sure Visual Studio has been installed:</span><span class="sxs-lookup"><span data-stu-id="a4224-194">Make sure Visual Studio has been installed:</span></span>
    -   <span data-ttu-id="a4224-195">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span><span class="sxs-lookup"><span data-stu-id="a4224-195">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>
    
    >[!NOTE] 
    > <span data-ttu-id="a4224-196">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio         2017 tools for Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a4224-196">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio         2017 tools for Azure Functions.</span></span> <span data-ttu-id="a4224-197">You can update the tools from the **Tools** menu under **Extensions and Updates...** >          **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span><span class="sxs-lookup"><span data-stu-id="a4224-197">You can update the tools from the **Tools** menu under **Extensions and Updates...** >          **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 
    >
    >
    
### <a name="variations"></a><span data-ttu-id="a4224-198">Variations</span><span class="sxs-lookup"><span data-stu-id="a4224-198">Variations</span></span>
* <span data-ttu-id="a4224-199">The URI for accessing the Text Translation API in Azure Government is:</span><span class="sxs-lookup"><span data-stu-id="a4224-199">The URI for accessing the Text Translation API in Azure Government is:</span></span> 
   - `https://dev.microsofttranslator.us/translate?api-version=3.0`
### <a name="text-translation-method"></a><span data-ttu-id="a4224-200">Text Translation Method</span><span class="sxs-lookup"><span data-stu-id="a4224-200">Text Translation Method</span></span>
<span data-ttu-id="a4224-201">This sample will use the [Text Translation - Translate method](../cognitive-services/translator/reference/v3-0-translate.md) to translate a string of text from a language into another specified language.</span><span class="sxs-lookup"><span data-stu-id="a4224-201">This sample will use the [Text Translation - Translate method](../cognitive-services/translator/reference/v3-0-translate.md) to translate a string of text from a language into another specified language.</span></span> <span data-ttu-id="a4224-202">There are multiple [language codes](https://api.cognitive.microsofttranslator.com/languages?api-version=3.0&scope=translation,dictionary,transliteration) that can be used with the Text Translation API.</span><span class="sxs-lookup"><span data-stu-id="a4224-202">There are multiple [language codes](https://api.cognitive.microsofttranslator.com/languages?api-version=3.0&scope=translation,dictionary,transliteration) that can be used with the Text Translation API.</span></span> 

### <a name="text-translation-c-example-request"></a><span data-ttu-id="a4224-203">Text Translation C# example request</span><span class="sxs-lookup"><span data-stu-id="a4224-203">Text Translation C# example request</span></span>

<span data-ttu-id="a4224-204">The sample is written in C#.</span><span class="sxs-lookup"><span data-stu-id="a4224-204">The sample is written in C#.</span></span> 

1. <span data-ttu-id="a4224-205">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4224-205">Create a new Console solution in Visual Studio.</span></span>
2. <span data-ttu-id="a4224-206">Replace Program.cs with the corresponding code below.</span><span class="sxs-lookup"><span data-stu-id="a4224-206">Replace Program.cs with the corresponding code below.</span></span>
3. <span data-ttu-id="a4224-207">Replace the `subscriptionKey` value with the key value that you retrieved above.</span><span class="sxs-lookup"><span data-stu-id="a4224-207">Replace the `subscriptionKey` value with the key value that you retrieved above.</span></span>
4. <span data-ttu-id="a4224-208">Replace the `text` value with text that you want to translate.</span><span class="sxs-lookup"><span data-stu-id="a4224-208">Replace the `text` value with text that you want to translate.</span></span>
5. <span data-ttu-id="a4224-209">Run the program.</span><span class="sxs-lookup"><span data-stu-id="a4224-209">Run the program.</span></span>

<span data-ttu-id="a4224-210">You can also test out different languages and texts by replacing the "text", "from", and "to" variables in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="a4224-210">You can also test out different languages and texts by replacing the "text", "from", and "to" variables in Program.cs.</span></span> 

```csharp
using System;
using Microsoft.Azure.CognitiveServices.Language.TextAnalytics;
using Microsoft.Azure.CognitiveServices.Language.TextAnalytics.Models;
using System.Collections.Generic;
using Microsoft.Rest;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;
using System.Net;
using System.IO;
using Newtonsoft.Json;
using System.Text;

namespace TextTranslator
{
    class Program
    {
        static string host = "https://dev.microsofttranslator.us";
        static string path = "/translate?api-version=3.0";
        // Translate to German.
        static string params_ = "&to=de";

        static string uri = host + path + params_;

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "PASTE KEY HERE";

        static string text = "Hello world!";

        async static void Translate()
        {
            System.Object[] body = new System.Object[] { new { Text = text } };
            var requestBody = JsonConvert.SerializeObject(body);

            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(requestBody, Encoding.UTF8, "application/json");
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();
                var result = JsonConvert.SerializeObject(JsonConvert.DeserializeObject(responseBody), Formatting.Indented);

                Console.OutputEncoding = UnicodeEncoding.UTF8;
                Console.WriteLine(result);
            }
        }

        static void Main(string[] args)
        {
            Translate();
            Console.ReadLine();
        }
    }
}
```
<span data-ttu-id="a4224-211">For more information, please see [public documentation](../cognitive-services/translator/translator-info-overview.md) and [public API documentation](https://docs.microsoft.com/azure/cognitive-services/Translator/reference/v3-0-reference) for Translator Text API.</span><span class="sxs-lookup"><span data-stu-id="a4224-211">For more information, please see [public documentation](../cognitive-services/translator/translator-info-overview.md) and [public API documentation](https://docs.microsoft.com/azure/cognitive-services/Translator/reference/v3-0-reference) for Translator Text API.</span></span>

### <a name="next-steps"></a><span data-ttu-id="a4224-212">Next Steps</span><span class="sxs-lookup"><span data-stu-id="a4224-212">Next Steps</span></span>
* <span data-ttu-id="a4224-213">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span><span class="sxs-lookup"><span data-stu-id="a4224-213">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span></span>
* <span data-ttu-id="a4224-214">Get help on Stack Overflow by using the "[azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)" tag</span><span class="sxs-lookup"><span data-stu-id="a4224-214">Get help on Stack Overflow by using the "[azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)" tag</span></span>
* <span data-ttu-id="a4224-215">Give us feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span><span class="sxs-lookup"><span data-stu-id="a4224-215">Give us feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span></span>
