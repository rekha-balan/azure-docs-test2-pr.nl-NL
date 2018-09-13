---
title: Face API C# tutorial | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Create a simple Windows app that uses the Cognitive Services Face API to detect features of faces in an image.
services: cognitive-services
author: ghogen
manager: douge
ms.service: cognitive-services
ms.component: face-api
ms.topic: conceptual
ms.date: 05/07/2018
ms.author: ghogen
ms.openlocfilehash: b51760f889db27aa25e54582070ee7d3adcf66f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967248"
---
# <a name="connecting-to-cognitive-services-face-api-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="0b54f-103">Connecting to Cognitive Services Face API by using Connected Services in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b54f-103">Connecting to Cognitive Services Face API by using Connected Services in Visual Studio</span></span>

<span data-ttu-id="0b54f-104">By using the Cognitive Services Face API, you can detect, analyze, organize, and tag faces in photos.</span><span class="sxs-lookup"><span data-stu-id="0b54f-104">By using the Cognitive Services Face API, you can detect, analyze, organize, and tag faces in photos.</span></span>

<span data-ttu-id="0b54f-105">This article and its companion articles provide details for using the Visual Studio Connected Service feature for Cognitive Services Face API.</span><span class="sxs-lookup"><span data-stu-id="0b54f-105">This article and its companion articles provide details for using the Visual Studio Connected Service feature for Cognitive Services Face API.</span></span> <span data-ttu-id="0b54f-106">The capability is available in both Visual Studio 2017 15.7 or later, with the Cognitive Services extension installed.</span><span class="sxs-lookup"><span data-stu-id="0b54f-106">The capability is available in both Visual Studio 2017 15.7 or later, with the Cognitive Services extension installed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b54f-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0b54f-107">Prerequisites</span></span>

- <span data-ttu-id="0b54f-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="0b54f-108">**An Azure subscription**.</span></span> <span data-ttu-id="0b54f-109">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b54f-109">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="0b54f-110">**Visual Studio 2017 version 15.7** with the **Web Development** workload installed.</span><span class="sxs-lookup"><span data-stu-id="0b54f-110">**Visual Studio 2017 version 15.7** with the **Web Development** workload installed.</span></span> <span data-ttu-id="0b54f-111">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span><span class="sxs-lookup"><span data-stu-id="0b54f-111">[Download it now](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span></span>

[!INCLUDE [vs-install-cognitive-services-vsix](../../../includes/vs-install-cognitive-services-vsix.md)]

## <a name="create-a-project-and-add-support-for-cognitive-services-face-api"></a><span data-ttu-id="0b54f-112">Create a project and add support for Cognitive Services Face API</span><span class="sxs-lookup"><span data-stu-id="0b54f-112">Create a project and add support for Cognitive Services Face API</span></span>

1. <span data-ttu-id="0b54f-113">Create a new ASP.NET Core web project.</span><span class="sxs-lookup"><span data-stu-id="0b54f-113">Create a new ASP.NET Core web project.</span></span> <span data-ttu-id="0b54f-114">Use the Empty project template.</span><span class="sxs-lookup"><span data-stu-id="0b54f-114">Use the Empty project template.</span></span> 

1. <span data-ttu-id="0b54f-115">In **Solution Explorer**, choose **Add** > **Connected Service**.</span><span class="sxs-lookup"><span data-stu-id="0b54f-115">In **Solution Explorer**, choose **Add** > **Connected Service**.</span></span>
   <span data-ttu-id="0b54f-116">The Connected Service page appears with services you can add to your project.</span><span class="sxs-lookup"><span data-stu-id="0b54f-116">The Connected Service page appears with services you can add to your project.</span></span>

   ![Add Connected Service menu item](./media/vs-face-connected-service/Connected-Service-Menu.PNG)

1. <span data-ttu-id="0b54f-118">In the menu of available services, choose **Cognitive Services Face API**.</span><span class="sxs-lookup"><span data-stu-id="0b54f-118">In the menu of available services, choose **Cognitive Services Face API**.</span></span>

   ![Choose the service to connect to](./media/vs-face-connected-service/Cog-Face-Connected-Service-0.PNG)

   <span data-ttu-id="0b54f-120">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="0b54f-120">If you've signed into Visual Studio, and have an Azure subscription associated with your account, a page appears with a dropdown list with your subscriptions.</span></span>

   ![Select your subscription](media/vs-face-connected-service/Cog-Face-Connected-Service-1.PNG)

1. <span data-ttu-id="0b54f-122">Select the subscription you want to use, and then choose a name for the Face API, or choose the Edit link to modify the automatically generated name, choose the resource group, and the Pricing Tier.</span><span class="sxs-lookup"><span data-stu-id="0b54f-122">Select the subscription you want to use, and then choose a name for the Face API, or choose the Edit link to modify the automatically generated name, choose the resource group, and the Pricing Tier.</span></span>

   ![Edit connected service details](media/vs-face-connected-service/Cog-Face-Connected-Service-2.PNG)

   <span data-ttu-id="0b54f-124">Follow the link for details on the pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="0b54f-124">Follow the link for details on the pricing tiers.</span></span>

1. <span data-ttu-id="0b54f-125">Choose Add to add supported for the Connected Service.</span><span class="sxs-lookup"><span data-stu-id="0b54f-125">Choose Add to add supported for the Connected Service.</span></span>
   <span data-ttu-id="0b54f-126">Visual Studio modifies your project to add the NuGet packages, configuration file entries, and other changes to support a connection the Face API.</span><span class="sxs-lookup"><span data-stu-id="0b54f-126">Visual Studio modifies your project to add the NuGet packages, configuration file entries, and other changes to support a connection the Face API.</span></span>

## <a name="use-the-face-api-to-detect-attributes-of-faces-in-an-image"></a><span data-ttu-id="0b54f-127">Use the Face API to detect attributes of faces in an image</span><span class="sxs-lookup"><span data-stu-id="0b54f-127">Use the Face API to detect attributes of faces in an image</span></span>

1. <span data-ttu-id="0b54f-128">Add the following using statements in Startup.cs.</span><span class="sxs-lookup"><span data-stu-id="0b54f-128">Add the following using statements in Startup.cs.</span></span>
 
   ```csharp
   using System.IO;
   using System.Text;
   using Microsoft.Extensions.Configuration;
   using System.Net.Http;
   using System.Net.Http.Headers;
   ```
 
1. <span data-ttu-id="0b54f-129">Add a configuration field, and add a constructor that initializes the configuration field in Startup class to enable Configuration in your program.</span><span class="sxs-lookup"><span data-stu-id="0b54f-129">Add a configuration field, and add a constructor that initializes the configuration field in Startup class to enable Configuration in your program.</span></span>

   ```csharp
      private IConfiguration configuration;

      public Startup(IConfiguration configuration)
      {
          this.configuration = configuration;
      }
   ```

1. <span data-ttu-id="0b54f-130">In the wwwroot folder in your project, add an images folder, and add an image file to your wwwroot folder.</span><span class="sxs-lookup"><span data-stu-id="0b54f-130">In the wwwroot folder in your project, add an images folder, and add an image file to your wwwroot folder.</span></span> <span data-ttu-id="0b54f-131">As an example, you can use one of the images on this [Face API page](https://azure.microsoft.com/services/cognitive-services/face/).</span><span class="sxs-lookup"><span data-stu-id="0b54f-131">As an example, you can use one of the images on this [Face API page](https://azure.microsoft.com/services/cognitive-services/face/).</span></span> <span data-ttu-id="0b54f-132">Right click on one of the images, save to your local hard drive, then in Solution Explorer, right-click on the images folder, and choosee **Add** > **Existing Item** to add it to your project.</span><span class="sxs-lookup"><span data-stu-id="0b54f-132">Right click on one of the images, save to your local hard drive, then in Solution Explorer, right-click on the images folder, and choosee **Add** > **Existing Item** to add it to your project.</span></span> <span data-ttu-id="0b54f-133">Your project should look something like this in Solution Explorer:</span><span class="sxs-lookup"><span data-stu-id="0b54f-133">Your project should look something like this in Solution Explorer:</span></span>
 
   ![images folder with image file](media/vs-face-connected-service/Cog-Face-Connected-Service-6.PNG)

1. <span data-ttu-id="0b54f-135">Right-click on the image file, choose Properties, and then choose **Copy if newer**.</span><span class="sxs-lookup"><span data-stu-id="0b54f-135">Right-click on the image file, choose Properties, and then choose **Copy if newer**.</span></span>

   ![Copy if newer](media/vs-face-connected-service/Cog-Face-Connected-Service-5.PNG)
 
1. <span data-ttu-id="0b54f-137">Replace the Configure method with the following code to access the Face API and test an image.</span><span class="sxs-lookup"><span data-stu-id="0b54f-137">Replace the Configure method with the following code to access the Face API and test an image.</span></span> <span data-ttu-id="0b54f-138">Change the imagePath string to the correct path and filename for your face image.</span><span class="sxs-lookup"><span data-stu-id="0b54f-138">Change the imagePath string to the correct path and filename for your face image.</span></span>

   ```csharp
    // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            // TODO: Change this to your image's path on your site.
            string imagePath = @"images/face1.png";

            // Enable static files such as image files.
            app.UseStaticFiles();

            string faceApiKey = this.configuration["FaceAPI_ServiceKey"];
            string faceApiEndPoint = this.configuration["FaceAPI_ServiceEndPoint"];

            HttpClient client = new HttpClient();

            // Request headers.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", faceApiKey);

            // Request parameters. A third optional parameter is "details".
            string requestParameters = "returnFaceId=true&returnFaceLandmarks=false&returnFaceAttributes=age,gender,headPose,smile,facialHair,glasses,emotion,hair,makeup,occlusion,accessories,blur,exposure,noise";

            // Assemble the URI for the REST API Call.
            string uri = faceApiEndPoint + "/detect?" + requestParameters;

            // Request body. Posts an image you've added to your site's images folder.
            var fileInfo = env.WebRootFileProvider.GetFileInfo(imagePath);
            var byteData = GetImageAsByteArray(fileInfo.PhysicalPath);

            string contentStringFace = string.Empty;
            using (ByteArrayContent content = new ByteArrayContent(byteData))
            {
                // This example uses content type "application/octet-stream".
                // The other content types you can use are "application/json" and "multipart/form-data".
                content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");

                // Execute the REST API call.
                var response = client.PostAsync(uri, content).Result;

                // Get the JSON response.
                contentStringFace = response.Content.ReadAsStringAsync().Result;
            }

            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.Run(async (context) =>
            {
                await context.Response.WriteAsync($"<p><b>Face Image:</b></p>");
                await context.Response.WriteAsync($"<div><img src=\"" + imagePath + "\" /></div>");
                await context.Response.WriteAsync($"<p><b>Face detection API results:</b></p>");
                await context.Response.WriteAsync("<p>");
                await context.Response.WriteAsync(JsonPrettyPrint(contentStringFace));
                await context.Response.WriteAsync("<p>");
            });
        }
   ```
    <span data-ttu-id="0b54f-139">The code in this step constructs a HTTP request with a call to the Face REST API, using the key you added when you added the connected service.</span><span class="sxs-lookup"><span data-stu-id="0b54f-139">The code in this step constructs a HTTP request with a call to the Face REST API, using the key you added when you added the connected service.</span></span>

1. <span data-ttu-id="0b54f-140">Add the helper functions GetImageAsByteArray and JsonPrettyPrint.</span><span class="sxs-lookup"><span data-stu-id="0b54f-140">Add the helper functions GetImageAsByteArray and JsonPrettyPrint.</span></span>

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

1. <span data-ttu-id="0b54f-141">Run the web application and see what Face API found in the image.</span><span class="sxs-lookup"><span data-stu-id="0b54f-141">Run the web application and see what Face API found in the image.</span></span>
 
   ![Face API image and formatted results](media/vs-face-connected-service/Cog-Face-Connected-Service-4.PNG)

## <a name="clean-up-resources"></a><span data-ttu-id="0b54f-143">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0b54f-143">Clean up resources</span></span>

<span data-ttu-id="0b54f-144">When no longer needed, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="0b54f-144">When no longer needed, delete the resource group.</span></span> <span data-ttu-id="0b54f-145">This deletes the cognitive service and related resources.</span><span class="sxs-lookup"><span data-stu-id="0b54f-145">This deletes the cognitive service and related resources.</span></span> <span data-ttu-id="0b54f-146">To delete the resource group through the portal:</span><span class="sxs-lookup"><span data-stu-id="0b54f-146">To delete the resource group through the portal:</span></span>

1. <span data-ttu-id="0b54f-147">Enter the name of your resource group in the Search box at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="0b54f-147">Enter the name of your resource group in the Search box at the top of the portal.</span></span> <span data-ttu-id="0b54f-148">When you see the resource group used in this QuickStart in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="0b54f-148">When you see the resource group used in this QuickStart in the search results, select it.</span></span>
1. <span data-ttu-id="0b54f-149">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="0b54f-149">Select **Delete resource group**.</span></span>
1. <span data-ttu-id="0b54f-150">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="0b54f-150">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b54f-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="0b54f-151">Next steps</span></span>

<span data-ttu-id="0b54f-152">Learn more about the Face API by reading the [Face API Documentation](Overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b54f-152">Learn more about the Face API by reading the [Face API Documentation](Overview.md).</span></span>
