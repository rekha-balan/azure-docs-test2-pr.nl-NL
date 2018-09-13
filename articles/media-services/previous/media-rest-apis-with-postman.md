---
title: Configure Postman for Azure Media Services REST API calls
description: Learn how to configure Postman for Media Services REST API calls.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/04/2017
ms.author: juliako
ms.openlocfilehash: 72b110cac8d4945c958d760ff98e2da2f2796b62
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871510"
---
# <a name="configure-postman-for-media-services-rest-api-calls"></a><span data-ttu-id="7c0cf-103">Configure Postman for Media Services REST API calls</span><span class="sxs-lookup"><span data-stu-id="7c0cf-103">Configure Postman for Media Services REST API calls</span></span>

<span data-ttu-id="7c0cf-104">This tutorial shows you how to configure **Postman** so it can be used to call Azure Media Services (AMS) REST APIs.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-104">This tutorial shows you how to configure **Postman** so it can be used to call Azure Media Services (AMS) REST APIs.</span></span> <span data-ttu-id="7c0cf-105">The tutorial shows how to import environment and collection files into **Postman**.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-105">The tutorial shows how to import environment and collection files into **Postman**.</span></span> <span data-ttu-id="7c0cf-106">The collection contains grouped definitions of HTTP requests that call Azure Media Services (AMS) REST APIs.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-106">The collection contains grouped definitions of HTTP requests that call Azure Media Services (AMS) REST APIs.</span></span> <span data-ttu-id="7c0cf-107">The environment file contains variables that are used by the collection.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-107">The environment file contains variables that are used by the collection.</span></span>

<span data-ttu-id="7c0cf-108">This environment and collection is used in articles that show how to achieve various tasks with Azure Media Services REST APIs.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-108">This environment and collection is used in articles that show how to achieve various tasks with Azure Media Services REST APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c0cf-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c0cf-109">Prerequisites</span></span>

- <span data-ttu-id="7c0cf-110">Install the [Postman](https://www.getpostman.com/) REST client to execute the REST APIs shown in some of the AMS REST tutorials.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-110">Install the [Postman](https://www.getpostman.com/) REST client to execute the REST APIs shown in some of the AMS REST tutorials.</span></span> 

    <span data-ttu-id="7c0cf-111">We are using **Postman** but any REST tool would be suitable.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-111">We are using **Postman** but any REST tool would be suitable.</span></span> <span data-ttu-id="7c0cf-112">Other alternatives are: **Visual Studio Code** with the REST plugin or **Telerik Fiddler**.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-112">Other alternatives are: **Visual Studio Code** with the REST plugin or **Telerik Fiddler**.</span></span> 

## <a name="configure-the-environment"></a><span data-ttu-id="7c0cf-113">Configure the environment</span><span class="sxs-lookup"><span data-stu-id="7c0cf-113">Configure the environment</span></span> 

1. <span data-ttu-id="7c0cf-114">Create a .json file that contains the environment variables used in AMS tutorials.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-114">Create a .json file that contains the environment variables used in AMS tutorials.</span></span> <span data-ttu-id="7c0cf-115">Name the file (for example, **AzureMediaServices.postman_environment.json**).</span><span class="sxs-lookup"><span data-stu-id="7c0cf-115">Name the file (for example, **AzureMediaServices.postman_environment.json**).</span></span> <span data-ttu-id="7c0cf-116">Open the file and paste the code that defines the Postman environment from [this code listing](postman-environment.md).</span><span class="sxs-lookup"><span data-stu-id="7c0cf-116">Open the file and paste the code that defines the Postman environment from [this code listing](postman-environment.md).</span></span> 
2. <span data-ttu-id="7c0cf-117">Open the **Postman**.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-117">Open the **Postman**.</span></span>
3. <span data-ttu-id="7c0cf-118">On the right of the screen, select the **Manage environment** option.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-118">On the right of the screen, select the **Manage environment** option.</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postman-create-env.png)
4. <span data-ttu-id="7c0cf-120">From the **Manage environment** dialog, click **Import**.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-120">From the **Manage environment** dialog, click **Import**.</span></span>
5. <span data-ttu-id="7c0cf-121">Browse and select the **AzureMediaServices.postman_environment.json** file.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-121">Browse and select the **AzureMediaServices.postman_environment.json** file.</span></span>
6. <span data-ttu-id="7c0cf-122">The **AzureMedia** environment is added.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-122">The **AzureMedia** environment is added.</span></span>
7. <span data-ttu-id="7c0cf-123">Close the dialog.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-123">Close the dialog.</span></span>
8. <span data-ttu-id="7c0cf-124">Select the **AzureMedia** environment.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-124">Select the **AzureMedia** environment.</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postman-choose-env.png)

## <a name="configure-the-collection"></a><span data-ttu-id="7c0cf-126">Configure the collection</span><span class="sxs-lookup"><span data-stu-id="7c0cf-126">Configure the collection</span></span>

1. <span data-ttu-id="7c0cf-127">Create a .json file that contains the **Postman** collection with all the operations that are needed to upload a file to Media Services.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-127">Create a .json file that contains the **Postman** collection with all the operations that are needed to upload a file to Media Services.</span></span> <span data-ttu-id="7c0cf-128">Name the file (for example, **AzureMediaServicesOperations.postman_collection.json**).</span><span class="sxs-lookup"><span data-stu-id="7c0cf-128">Name the file (for example, **AzureMediaServicesOperations.postman_collection.json**).</span></span> <span data-ttu-id="7c0cf-129">Open the file and paste the code that defines the **Postman** collection from [this code listing](postman-collection.md).</span><span class="sxs-lookup"><span data-stu-id="7c0cf-129">Open the file and paste the code that defines the **Postman** collection from [this code listing](postman-collection.md).</span></span>
2. <span data-ttu-id="7c0cf-130">Click **Import** to import the collection file.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-130">Click **Import** to import the collection file.</span></span>
3. <span data-ttu-id="7c0cf-131">Choose the **AzureMediaServicesOperations.postman_collection.json** file.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-131">Choose the **AzureMediaServicesOperations.postman_collection.json** file.</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postman-import-collection.png)

## <a name="next-steps"></a><span data-ttu-id="7c0cf-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c0cf-133">Next steps</span></span>

<span data-ttu-id="7c0cf-134">Check out the [upload assets](media-services-rest-upload-files.md) article.</span><span class="sxs-lookup"><span data-stu-id="7c0cf-134">Check out the [upload assets](media-services-rest-upload-files.md) article.</span></span>  
