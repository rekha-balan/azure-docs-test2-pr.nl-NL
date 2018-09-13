---
title: Computer Vision C# tutorial | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Connect to Cognitive Services Computer Vision from an ASP.NET Core web application.
services: cognitive-services
author: ghogen
manager: douge
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: conceptual
ms.date: 03/01/2018
ms.author: ghogen
ms.openlocfilehash: 76ca1215144a5caa40971e1eda23f6462f7bf27b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868477"
---
# <a name="connecting-to-cognitive-services-computer-vision-api-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="33304-103">Connecting to Cognitive Services Computer Vision API by using Connected Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="33304-103">Connecting to Cognitive Services Computer Vision API by using Connected Services in Visual Studio</span></span>

<span data-ttu-id="33304-104">By using the Cognitive Services Computer Vision API, you can extract rich information to categorize and process visual data, and perform machine-assisted moderation of images to help curate your services.</span><span class="sxs-lookup"><span data-stu-id="33304-104">By using the Cognitive Services Computer Vision API, you can extract rich information to categorize and process visual data, and perform machine-assisted moderation of images to help curate your services.</span></span>

<span data-ttu-id="33304-105">This article and its companion articles provide details for using the Visual Studio Connected Service feature for Cognitive Services Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="33304-105">This article and its companion articles provide details for using the Visual Studio Connected Service feature for Cognitive Services Computer Vision API.</span></span> <span data-ttu-id="33304-106">The capability is available in both Visual Studio 2017 15.7 or later, with the Cognitive Services extension installed.</span><span class="sxs-lookup"><span data-stu-id="33304-106">The capability is available in both Visual Studio 2017 15.7 or later, with the Cognitive Services extension installed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33304-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33304-107">Prerequisites</span></span>

- <span data-ttu-id="33304-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="33304-108">**An Azure subscription**.</span></span> <span data-ttu-id="33304-109">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33304-109">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="33304-110">**Visual Studio 2017 version 15.7** with the **Web Development** workload installed.</span><span class="sxs-lookup"><span data-stu-id="33304-110">**Visual Studio 2017 version 15.7** with the **Web Development** workload installed.</span></span> <span data-ttu-id="33304-111">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span><span class="sxs-lookup"><span data-stu-id="33304-111">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span></span>

[!INCLUDE [vs-install-cognitive-services-vsix](../../../includes/vs-install-cognitive-services-vsix.md)]

## <a name="add-support-to-your-project-for-cognitive-services-computer-vision-api"></a><span data-ttu-id="33304-112">Add support to your project for Cognitive Services Computer Vision API</span><span class="sxs-lookup"><span data-stu-id="33304-112">Add support to your project for Cognitive Services Computer Vision API</span></span>

1. <span data-ttu-id="33304-113">Create a new ASP.NET Core web project.</span><span class="sxs-lookup"><span data-stu-id="33304-113">Create a new ASP.NET Core web project.</span></span> <span data-ttu-id="33304-114">Use the Empty project template.</span><span class="sxs-lookup"><span data-stu-id="33304-114">Use the Empty project template.</span></span> 

1. <span data-ttu-id="33304-115">In **Solution Explorer**, choose **Add** > **Connected Service**.</span><span class="sxs-lookup"><span data-stu-id="33304-115">In **Solution Explorer**, choose **Add** > **Connected Service**.</span></span>
   <span data-ttu-id="33304-116">The Connected Service page appears with services you can add to your project.</span><span class="sxs-lookup"><span data-stu-id="33304-116">The Connected Service page appears with services you can add to your project.</span></span>

   ![Add Connected Service menu item](../media/vs-common/Connected-Service-Menu.PNG)

1. <span data-ttu-id="33304-118">In the menu of available services, choose **Cognitive Services Computer Vision API**.</span><span class="sxs-lookup"><span data-stu-id="33304-118">In the menu of available services, choose **Cognitive Services Computer Vision API**.</span></span>

   ![Choose the service to connect to](./media/vs-computer-vision-connected-service/Cog-Vision-Connected-Service-0.PNG)

   <span data-ttu-id="33304-120">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="33304-120">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span></span>

   ![Select your subscription](media/vs-computer-vision-connected-service/Cog-Vision-Connected-Service-1.PNG)

1. <span data-ttu-id="33304-122">Select the subscription you want to use, and then choose a name for the Computer Vision API, or choose the Edit link to modify the automatically generated name, choose the resource group, and the Pricing Tier.</span><span class="sxs-lookup"><span data-stu-id="33304-122">Select the subscription you want to use, and then choose a name for the Computer Vision API, or choose the Edit link to modify the automatically generated name, choose the resource group, and the Pricing Tier.</span></span>

   ![Edit connected service details](media/vs-computer-vision-connected-service/Cog-Vision-Connected-Service-2.PNG)

   <span data-ttu-id="33304-124">Follow the link for details on the pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="33304-124">Follow the link for details on the pricing tiers.</span></span>

1. <span data-ttu-id="33304-125">Choose Add to add supported for the Connected Service.</span><span class="sxs-lookup"><span data-stu-id="33304-125">Choose Add to add supported for the Connected Service.</span></span>
   <span data-ttu-id="33304-126">Visual Studio modifies your project to add the NuGet packages, configuration file entries, and other changes to support a connection the Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="33304-126">Visual Studio modifies your project to add the NuGet packages, configuration file entries, and other changes to support a connection the Computer Vision API.</span></span> <span data-ttu-id="33304-127">The Output Window shows the log of what is happening to your project.</span><span class="sxs-lookup"><span data-stu-id="33304-127">The Output Window shows the log of what is happening to your project.</span></span> <span data-ttu-id="33304-128">You should see something like the following:</span><span class="sxs-lookup"><span data-stu-id="33304-128">You should see something like the following:</span></span>

   ```output
   [4/26/2018 5:15:31.664 PM] Adding Computer Vision API to the project.
   [4/26/2018 5:15:32.084 PM] Creating new ComputerVision...
   [4/26/2018 5:15:32.153 PM] Creating new Resource Group...
   [4/26/2018 5:15:40.286 PM] Installing NuGet package 'Microsoft.Azure.CognitiveServices.Vision.ComputerVision' version 1.0.2-preview.
   [4/26/2018 5:15:44.117 PM] Retrieving keys...
   [4/26/2018 5:15:45.602 PM] Changing appsettings.json setting: ComputerVisionAPI_ServiceKey=<service key>
   [4/26/2018 5:15:45.606 PM] Changing appsettings.json setting: ComputerVisionAPI_ServiceEndPoint=https://australiaeast.api.cognitive.microsoft.com/vision/v2.0
   [4/26/2018 5:15:45.609 PM] Changing appsettings.json setting: ComputerVisionAPI_Name=WebApplication-Core-ComputerVision_ComputerVisionAPI
   [4/26/2018 5:15:46.747 PM] Successfully added Computer Vision API to the project.
   ```
 
## <a name="use-the-computer-vision-api-to-detect-attributes-of-an-image"></a><span data-ttu-id="33304-129">Use the Computer Vision API to detect attributes of an image</span><span class="sxs-lookup"><span data-stu-id="33304-129">Use the Computer Vision API to detect attributes of an image</span></span>

1. <span data-ttu-id="33304-130">Add the following using statements in Startup.cs.</span><span class="sxs-lookup"><span data-stu-id="33304-130">Add the following using statements in Startup.cs.</span></span>
 
   ```csharp
   using System.IO;
   using System.Text;
   using Microsoft.Extensions.Configuration;
   using System.Net.Http;
   using System.Net.Http.Headers;
   ```
 
1. <span data-ttu-id="33304-131">Add a configuration field, and add a constructor that initializes the configuration field in the `Startup` class to enable configuration in your program.</span><span class="sxs-lookup"><span data-stu-id="33304-131">Add a configuration field, and add a constructor that initializes the configuration field in the `Startup` class to enable configuration in your program.</span></span>

   ```csharp
      private IConfiguration configuration;

      public Startup(IConfiguration configuration)
      {
          this.configuration = configuration;
      }
   ```

1. <span data-ttu-id="33304-132">In the wwwroot folder in your project, add an images folder, and add an image file to your wwwroot folder.</span><span class="sxs-lookup"><span data-stu-id="33304-132">In the wwwroot folder in your project, add an images folder, and add an image file to your wwwroot folder.</span></span> <span data-ttu-id="33304-133">As an example, you can use one of the images on this [Computer Vision API page](https://azure.microsoft.com/services/cognitive-services/computer-vision/).</span><span class="sxs-lookup"><span data-stu-id="33304-133">As an example, you can use one of the images on this [Computer Vision API page](https://azure.microsoft.com/services/cognitive-services/computer-vision/).</span></span> <span data-ttu-id="33304-134">Right-click on one of the images, save to your local hard drive, then in Solution Explorer, right-click on the images folder, and choosee **Add** > **Existing Item** to add it to your project.</span><span class="sxs-lookup"><span data-stu-id="33304-134">Right-click on one of the images, save to your local hard drive, then in Solution Explorer, right-click on the images folder, and choosee **Add** > **Existing Item** to add it to your project.</span></span> <span data-ttu-id="33304-135">Your project should look something like this in Solution Explorer:</span><span class="sxs-lookup"><span data-stu-id="33304-135">Your project should look something like this in Solution Explorer:</span></span> 
  
   ![images folder with image file](media/vs-computer-vision-connected-service/Cog-Vision-Connected-Service-3.PNG) 

1. <span data-ttu-id="33304-137">Right-click on the image file, choose Properties, and then choose **Copy if newer**.</span><span class="sxs-lookup"><span data-stu-id="33304-137">Right-click on the image file, choose Properties, and then choose **Copy if newer**.</span></span> 

   ![Copy if newer](media/vs-computer-vision-connected-service/Cog-Vision-Connected-Service-5.PNG) 
 
1. <span data-ttu-id="33304-139">Replace the Configure method with the following code to access the Computer Vision API and test an image.</span><span class="sxs-lookup"><span data-stu-id="33304-139">Replace the Configure method with the following code to access the Computer Vision API and test an image.</span></span>

   ```csharp
        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            // TODO: Change this to your image's path on your site. 
            string imagePath = @"images/subway.png";

            // Enable static files such as image files. 
            app.UseStaticFiles();

            string visionApiKey = this.configuration["ComputerVisionAPI_ServiceKey"];
            string visionApiEndPoint = this.configuration["ComputerVisionAPI_ServiceEndPoint"];

            HttpClient client = new HttpClient();

            // Request headers.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", visionApiKey);

            // Request parameters. A third optional parameter is "details".
            string requestParameters = "visualFeatures=Categories,Description,Color&language=en";

            // Assemble the URI for the REST API Call.
            string uri = visionApiEndPoint + "/analyze" + "?" + requestParameters;

            HttpResponseMessage response;

            // Request body. Posts an image you've added to your site's images folder. 
            var fileInfo = env.WebRootFileProvider.GetFileInfo(imagePath);
            byte[] byteData = GetImageAsByteArray(fileInfo.PhysicalPath);

            string contentString = string.Empty;
            using (ByteArrayContent content = new ByteArrayContent(byteData))
            {
                // This example uses content type "application/octet-stream".
                // The other content types you can use are "application/json" and "multipart/form-data".
                content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");

                // Execute the REST API call.
                response = client.PostAsync(uri, content).Result;

                // Get the JSON response.
                contentString = response.Content.ReadAsStringAsync().Result;
            }

            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.Run(async (context) =>
            {
                await context.Response.WriteAsync("<h1>Cognitive Services Demo</h1>");
                await context.Response.WriteAsync($"<p><b>Test Image:</b></p>");
                await context.Response.WriteAsync($"<div><img src=\"" + imagePath + "\" /></div>");
                await context.Response.WriteAsync($"<p><b>Computer Vision API results:</b></p>");
                await context.Response.WriteAsync("<p>");
                await context.Response.WriteAsync(JsonPrettyPrint(contentString));
                await context.Response.WriteAsync("<p>");
            });
        }

   ```
    <span data-ttu-id="33304-140">The code here constructs a HTTP request with the URI and the image as binary content for a call to the Computer Vision REST API.</span><span class="sxs-lookup"><span data-stu-id="33304-140">The code here constructs a HTTP request with the URI and the image as binary content for a call to the Computer Vision REST API.</span></span>

1. <span data-ttu-id="33304-141">Add the helper functions GetImageAsByteArray and JsonPrettyPrint.</span><span class="sxs-lookup"><span data-stu-id="33304-141">Add the helper functions GetImageAsByteArray and JsonPrettyPrint.</span></span>

   ```csharp
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

            string INDENT_STRING = "    ";
            var indent = 0;
            var quoted = false;
            var sb = new StringBuilder();
            for (var i = 0; i < json.Length; i++)
            {
                var ch = json[i];
                switch (ch)
                {
                    case '{':
                    case '[':
                        sb.Append(ch);
                        if (!quoted)
                        {
                            sb.AppendLine();
                        }
                        break;
                    case '}':
                    case ']':
                        if (!quoted)
                        {
                            sb.AppendLine();
                        }
                        sb.Append(ch);
                        break;
                    case '"':
                        sb.Append(ch);
                        bool escaped = false;
                        var index = i;
                        while (index > 0 && json[--index] == '\\')
                            escaped = !escaped;
                        if (!escaped)
                            quoted = !quoted;
                        break;
                    case ',':
                        sb.Append(ch);
                        if (!quoted)
                        {
                            sb.AppendLine();
                        }
                        break;
                    case ':':
                        sb.Append(ch);
                        if (!quoted)
                            sb.Append(" ");
                        break;
                    default:
                        sb.Append(ch);
                        break;
                }
            }
            return sb.ToString();
        }
   ```

1. <span data-ttu-id="33304-142">Run the web application and see what Computer Vision API found in your image.</span><span class="sxs-lookup"><span data-stu-id="33304-142">Run the web application and see what Computer Vision API found in your image.</span></span>

   ![Computer Vision API image and formatted results](media/vs-computer-vision-connected-service/Cog-Vision-Connected-Service-4.PNG)  

## <a name="clean-up-resources"></a><span data-ttu-id="33304-144">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="33304-144">Clean up resources</span></span>

<span data-ttu-id="33304-145">When no longer needed, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="33304-145">When no longer needed, delete the resource group.</span></span> <span data-ttu-id="33304-146">This deletes the cognitive service and related resources.</span><span class="sxs-lookup"><span data-stu-id="33304-146">This deletes the cognitive service and related resources.</span></span> <span data-ttu-id="33304-147">To delete the resource group through the portal:</span><span class="sxs-lookup"><span data-stu-id="33304-147">To delete the resource group through the portal:</span></span>

1. <span data-ttu-id="33304-148">Enter the name of your resource group in the Search box at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="33304-148">Enter the name of your resource group in the Search box at the top of the portal.</span></span> <span data-ttu-id="33304-149">When you see the resource group used in this QuickStart in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="33304-149">When you see the resource group used in this QuickStart in the search results, select it.</span></span>
2. <span data-ttu-id="33304-150">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="33304-150">Select **Delete resource group**.</span></span>
3. <span data-ttu-id="33304-151">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="33304-151">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33304-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="33304-152">Next steps</span></span>

<span data-ttu-id="33304-153">Learn more about the Computer Vision API by reading the [Computer Vision API Documentation](Home.md).</span><span class="sxs-lookup"><span data-stu-id="33304-153">Learn more about the Computer Vision API by reading the [Computer Vision API Documentation](Home.md).</span></span>
