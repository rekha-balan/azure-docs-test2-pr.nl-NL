---
title: Azure Content Moderator SDK for .NET helper method | Microsoft Docs
description: How to return a Content Moderator client using Azure Content Moderator SDK for .NET
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/04/2018
ms.author: sajagtap
ms.openlocfilehash: 36f2124708731f78f34849d8210ed39ea8f59140
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870083"
---
# <a name="helper-code-to-return-a-content-moderator-client"></a><span data-ttu-id="30bc8-103">Helper code to return a Content Moderator client</span><span class="sxs-lookup"><span data-stu-id="30bc8-103">Helper code to return a Content Moderator client</span></span>

<span data-ttu-id="30bc8-104">This article provides information and code samples to help you get started using the Content Moderator SDK for .NET to create a Content Moderator client for your subscription.</span><span class="sxs-lookup"><span data-stu-id="30bc8-104">This article provides information and code samples to help you get started using the Content Moderator SDK for .NET to create a Content Moderator client for your subscription.</span></span>

<span data-ttu-id="30bc8-105">The library is used by other quickstarts in this section.</span><span class="sxs-lookup"><span data-stu-id="30bc8-105">The library is used by other quickstarts in this section.</span></span>

<span data-ttu-id="30bc8-106">This article assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="30bc8-106">This article assumes that you are already familiar with Visual Studio and C#.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30bc8-107">This class library contains code intended for demonstration purposes only.</span><span class="sxs-lookup"><span data-stu-id="30bc8-107">This class library contains code intended for demonstration purposes only.</span></span>
> <span data-ttu-id="30bc8-108">If you adapt this code for use in production, use a secure method of storing and using your Content Moderator subscription key.</span><span class="sxs-lookup"><span data-stu-id="30bc8-108">If you adapt this code for use in production, use a secure method of storing and using your Content Moderator subscription key.</span></span>

## <a name="sign-up-for-content-moderator-services"></a><span data-ttu-id="30bc8-109">Sign up for Content Moderator services</span><span class="sxs-lookup"><span data-stu-id="30bc8-109">Sign up for Content Moderator services</span></span>

<span data-ttu-id="30bc8-110">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="30bc8-110">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span></span>
<span data-ttu-id="30bc8-111">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span><span class="sxs-lookup"><span data-stu-id="30bc8-111">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span></span>

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="30bc8-112">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="30bc8-112">Create your Visual Studio project</span></span>

1. <span data-ttu-id="30bc8-113">Create a new **Class Library (.NET Framework)** project.</span><span class="sxs-lookup"><span data-stu-id="30bc8-113">Create a new **Class Library (.NET Framework)** project.</span></span>

   <span data-ttu-id="30bc8-114">In the sample code, I named the project **ModeratorHelper**.</span><span class="sxs-lookup"><span data-stu-id="30bc8-114">In the sample code, I named the project **ModeratorHelper**.</span></span>

1. <span data-ttu-id="30bc8-115">Add a reference to the **System.Configuration** Framework assembly.</span><span class="sxs-lookup"><span data-stu-id="30bc8-115">Add a reference to the **System.Configuration** Framework assembly.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="30bc8-116">Install required packages</span><span class="sxs-lookup"><span data-stu-id="30bc8-116">Install required packages</span></span>

<span data-ttu-id="30bc8-117">Install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="30bc8-117">Install the following NuGet packages:</span></span>

- <span data-ttu-id="30bc8-118">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="30bc8-118">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="30bc8-119">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="30bc8-119">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="30bc8-120">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="30bc8-120">Newtonsoft.Json</span></span>

### <a name="create-the-content-moderator-client"></a><span data-ttu-id="30bc8-121">Create the Content Moderator client</span><span class="sxs-lookup"><span data-stu-id="30bc8-121">Create the Content Moderator client</span></span>

<span data-ttu-id="30bc8-122">Replace the contents of the ModeratorHelper.cs file with the following code:</span><span class="sxs-lookup"><span data-stu-id="30bc8-122">Replace the contents of the ModeratorHelper.cs file with the following code:</span></span>

    using Microsoft.CognitiveServices.ContentModerator;

    namespace ModeratorHelper
    {
    /// <summary>
    /// Wraps the creation and configuration of a Content Moderator client.
    /// </summary>
    /// <remarks>This class library contains insecure code. If you adapt this 
    /// code for use in production, use a secure method of storing and using
    /// your Content Moderator subscription key.</remarks>
    public static class Clients
    {
        /// <summary>
        /// The region/location for your Content Moderator account, 
        /// for example, westus.
        /// </summary>
        private static readonly string AzureRegion = "myRegion";

        /// <summary>
        /// The base URL fragment for Content Moderator calls.
        /// </summary>
        private static readonly string AzureBaseURL =
            $"{AzureRegion}.api.cognitive.microsoft.com";

        /// <summary>
        /// Your Content Moderator subscription key.
        /// </summary>
        private static readonly string CMSubscriptionKey = "myKey";

        /// <summary>
        /// Returns a new Content Moderator client for your subscription.
        /// </summary>
        /// <returns>The new client.</returns>
        /// <remarks>The <see cref="ContentModeratorClient"/> is disposable.
        /// When you have finished using the client,
        /// you should dispose of it either directly or indirectly. </remarks>
        public static ContentModeratorClient NewClient()
        {
            // Create and initialize an instance of the Content Moderator API wrapper.
            ContentModeratorClient client = new ContentModeratorClient(new ApiKeyServiceClientCredentials(CMSubscriptionKey));

            client.BaseUrl = AzureBaseURL;
            return client;
        }
    }
    }


> [!IMPORTANT]
> <span data-ttu-id="30bc8-123">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span><span class="sxs-lookup"><span data-stu-id="30bc8-123">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span></span>

<span data-ttu-id="30bc8-124">You now have a quick way to create a Content Moderator client for your subscription.</span><span class="sxs-lookup"><span data-stu-id="30bc8-124">You now have a quick way to create a Content Moderator client for your subscription.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30bc8-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="30bc8-125">Next steps</span></span>

<span data-ttu-id="30bc8-126">[Download the Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span><span class="sxs-lookup"><span data-stu-id="30bc8-126">[Download the Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span></span>
