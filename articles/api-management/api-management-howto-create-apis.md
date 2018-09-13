---
title: How to create APIs in Azure API Management
description: Learn how to create and configure APIs in Azure API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 4cf84b25ac2510149abc3e68b4e740aa4dda68ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554688"
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="ddd22-103">How to create APIs in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ddd22-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="ddd22-104">An API in API Management represents a set of operations that can be invoked by client applications.</span><span class="sxs-lookup"><span data-stu-id="ddd22-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="ddd22-105">New APIs are created in the publisher portal, and then the desired operations are added.</span><span class="sxs-lookup"><span data-stu-id="ddd22-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="ddd22-106">Once the operations are added, the API is added to a product and can be published.</span><span class="sxs-lookup"><span data-stu-id="ddd22-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="ddd22-107">Once an API is published, it can be subscribed to and used by developers.</span><span class="sxs-lookup"><span data-stu-id="ddd22-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="ddd22-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span><span class="sxs-lookup"><span data-stu-id="ddd22-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="ddd22-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="ddd22-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="ddd22-110"><a name="create-new-api"> </a>Create a new API</span><span class="sxs-lookup"><span data-stu-id="ddd22-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="ddd22-111">APIs are created and configured in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="ddd22-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="ddd22-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="ddd22-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publisher portal][api-management-management-console]

> <span data-ttu-id="ddd22-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ddd22-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="ddd22-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span><span class="sxs-lookup"><span data-stu-id="ddd22-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![Create API][api-management-create-api]

<span data-ttu-id="ddd22-117">Use the **Add new API** window to configure the new API.</span><span class="sxs-lookup"><span data-stu-id="ddd22-117">Use the **Add new API** window to configure the new API.</span></span>

![Add new API][api-management-add-new-api]

<span data-ttu-id="ddd22-119">The following fields are used to configure the new API.</span><span class="sxs-lookup"><span data-stu-id="ddd22-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="ddd22-120">**Web API name** provides a unique and descriptive name for the API.</span><span class="sxs-lookup"><span data-stu-id="ddd22-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="ddd22-121">It is displayed in the developer and publisher portals.</span><span class="sxs-lookup"><span data-stu-id="ddd22-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="ddd22-122">**Web service URL** references the HTTP service implementing the API.</span><span class="sxs-lookup"><span data-stu-id="ddd22-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="ddd22-123">API management forwards requests to this address.</span><span class="sxs-lookup"><span data-stu-id="ddd22-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="ddd22-124">**Web API URL suffix** is appended to the base URL for the API management service.</span><span class="sxs-lookup"><span data-stu-id="ddd22-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="ddd22-125">The base URL is common for all APIs hosted by an API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="ddd22-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="ddd22-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span><span class="sxs-lookup"><span data-stu-id="ddd22-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="ddd22-127">**Web API URL scheme** determines which protocols can be used to access the API.</span><span class="sxs-lookup"><span data-stu-id="ddd22-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="ddd22-128">HTTPs is specified by default.</span><span class="sxs-lookup"><span data-stu-id="ddd22-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="ddd22-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span><span class="sxs-lookup"><span data-stu-id="ddd22-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="ddd22-130">This step can be repeated multiple times to add the API to multiple products.</span><span class="sxs-lookup"><span data-stu-id="ddd22-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="ddd22-131">Once the desired values are configured, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ddd22-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="ddd22-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="ddd22-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![API summary][api-management-api-summary]

## <span data-ttu-id="ddd22-134"><a name="configure-api-settings"> </a>Configure API settings</span><span class="sxs-lookup"><span data-stu-id="ddd22-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="ddd22-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span><span class="sxs-lookup"><span data-stu-id="ddd22-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="ddd22-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span><span class="sxs-lookup"><span data-stu-id="ddd22-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="ddd22-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span><span class="sxs-lookup"><span data-stu-id="ddd22-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![API settings][api-management-api-settings]

<span data-ttu-id="ddd22-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab. The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span><span class="sxs-lookup"><span data-stu-id="ddd22-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab. The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="ddd22-140">To use HTTP basic authentication, simply enter the desired credentials.</span><span class="sxs-lookup"><span data-stu-id="ddd22-140">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="ddd22-141">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="ddd22-141">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="ddd22-142">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="ddd22-142">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="ddd22-143">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="ddd22-143">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Basic authentication settings][api-management-api-settings-credentials]

<span data-ttu-id="ddd22-145">Click **Save** to save any changes you make to the API settings.</span><span class="sxs-lookup"><span data-stu-id="ddd22-145">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="ddd22-146"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="ddd22-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="ddd22-147">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span><span class="sxs-lookup"><span data-stu-id="ddd22-147">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="ddd22-148">For more information, see the following articles.</span><span class="sxs-lookup"><span data-stu-id="ddd22-148">For more information, see the following articles.</span></span>

* <span data-ttu-id="ddd22-149">[How to add operations to an API][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="ddd22-149">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="ddd22-150">[How to create and publish a product][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="ddd22-150">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-create-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md






