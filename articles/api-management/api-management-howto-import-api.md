---
title: Import an API into Azure API Management | Microsoft Docs
description: Learn how to import an API and its operations into Azure API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 95ab7cd4c6710c1315acf74588a25c736af31ca0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553406"
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="ce42c-103">How to import the definition of an API with operations in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ce42c-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="ce42c-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span><span class="sxs-lookup"><span data-stu-id="ce42c-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="ce42c-105">APIs and their operations can be imported using the following formats.</span><span class="sxs-lookup"><span data-stu-id="ce42c-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="ce42c-106">WADL</span><span class="sxs-lookup"><span data-stu-id="ce42c-106">WADL</span></span>
* <span data-ttu-id="ce42c-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="ce42c-107">Swagger</span></span>

<span data-ttu-id="ce42c-108">This guide shows how create a new API and import its operations in one step.</span><span class="sxs-lookup"><span data-stu-id="ce42c-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="ce42c-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="ce42c-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="ce42c-110"><a name="import-api"> </a>Import an API</span><span class="sxs-lookup"><span data-stu-id="ce42c-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="ce42c-111">APIs are created and configured in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="ce42c-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="ce42c-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="ce42c-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="ce42c-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ce42c-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Publisher portal][api-management-management-console]

<span data-ttu-id="ce42c-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span><span class="sxs-lookup"><span data-stu-id="ce42c-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![Import API][api-management-import-apis]

<span data-ttu-id="ce42c-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span><span class="sxs-lookup"><span data-stu-id="ce42c-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="ce42c-118">**From clipboard** allows you to paste the API specification into the designated text box.</span><span class="sxs-lookup"><span data-stu-id="ce42c-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="ce42c-119">**From file** allows you to browse to and select the file that contains the API specification.</span><span class="sxs-lookup"><span data-stu-id="ce42c-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="ce42c-120">**From URL** allows you to supply the URL to the specification for the API.</span><span class="sxs-lookup"><span data-stu-id="ce42c-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Import API format][api-management-import-api-clipboard]

<span data-ttu-id="ce42c-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span><span class="sxs-lookup"><span data-stu-id="ce42c-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="ce42c-123">The following formats are supported.</span><span class="sxs-lookup"><span data-stu-id="ce42c-123">The following formats are supported.</span></span>

* <span data-ttu-id="ce42c-124">WADL</span><span class="sxs-lookup"><span data-stu-id="ce42c-124">WADL</span></span>
* <span data-ttu-id="ce42c-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="ce42c-125">Swagger</span></span>

<span data-ttu-id="ce42c-126">Next, enter a **Web API URL suffix**.</span><span class="sxs-lookup"><span data-stu-id="ce42c-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="ce42c-127">This is appended to the base URL for your API management service.</span><span class="sxs-lookup"><span data-stu-id="ce42c-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="ce42c-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span><span class="sxs-lookup"><span data-stu-id="ce42c-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="ce42c-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span><span class="sxs-lookup"><span data-stu-id="ce42c-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="ce42c-130">Once all values are entered, click **Save** to create the API and the associated operations.</span><span class="sxs-lookup"><span data-stu-id="ce42c-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="ce42c-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ce42c-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="ce42c-132"><a name="export-api"> </a> Export an API</span><span class="sxs-lookup"><span data-stu-id="ce42c-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="ce42c-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="ce42c-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="ce42c-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span><span class="sxs-lookup"><span data-stu-id="ce42c-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![Export API][api-management-export-api]

<span data-ttu-id="ce42c-136">APIs can be exported using WADL or Swagger.</span><span class="sxs-lookup"><span data-stu-id="ce42c-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="ce42c-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span><span class="sxs-lookup"><span data-stu-id="ce42c-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Export API format][api-management-export-api-format]

## <span data-ttu-id="ce42c-139"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="ce42c-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="ce42c-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span><span class="sxs-lookup"><span data-stu-id="ce42c-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="ce42c-141">For more information, see the following guides.</span><span class="sxs-lookup"><span data-stu-id="ce42c-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="ce42c-142">[How to configure API settings][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="ce42c-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="ce42c-143">[How to create and publish a product][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="ce42c-143">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings





