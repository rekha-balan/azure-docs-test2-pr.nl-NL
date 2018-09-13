---
title: How to create and publish a product in Azure API Management
description: Learn how to create and publish products in Azure API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 47d81b5c4612d699b616bfc763b09fb9028206e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552998"
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="e027a-103">How to create and publish a product in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="e027a-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="e027a-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span><span class="sxs-lookup"><span data-stu-id="e027a-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="e027a-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span><span class="sxs-lookup"><span data-stu-id="e027a-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="e027a-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span><span class="sxs-lookup"><span data-stu-id="e027a-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="e027a-107"><a name="create-product"> </a>Create a product</span><span class="sxs-lookup"><span data-stu-id="e027a-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="e027a-108">Operations are added and configured to an API in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="e027a-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="e027a-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="e027a-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publisher portal][api-management-management-console]

> <span data-ttu-id="e027a-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="e027a-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="e027a-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span><span class="sxs-lookup"><span data-stu-id="e027a-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Products][api-management-products]

![New product][api-management-add-new-product]

<span data-ttu-id="e027a-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span><span class="sxs-lookup"><span data-stu-id="e027a-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="e027a-116">Products in API Management can be **Open** or **Protected**.</span><span class="sxs-lookup"><span data-stu-id="e027a-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="e027a-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span><span class="sxs-lookup"><span data-stu-id="e027a-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="e027a-118">Check **Require subscription** to create a protected product that requires a subscription.</span><span class="sxs-lookup"><span data-stu-id="e027a-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="e027a-119">This is the default setting.</span><span class="sxs-lookup"><span data-stu-id="e027a-119">This is the default setting.</span></span>

<span data-ttu-id="e027a-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span><span class="sxs-lookup"><span data-stu-id="e027a-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="e027a-121">If the box is unchecked, subscription attempts will be auto-approved.</span><span class="sxs-lookup"><span data-stu-id="e027a-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="e027a-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="e027a-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="e027a-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span><span class="sxs-lookup"><span data-stu-id="e027a-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="e027a-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span><span class="sxs-lookup"><span data-stu-id="e027a-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Unlimited multiple subscriptions][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="e027a-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span><span class="sxs-lookup"><span data-stu-id="e027a-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="e027a-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span><span class="sxs-lookup"><span data-stu-id="e027a-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Four multiple subscriptions][api-management-four-multiple-subscriptions]

<span data-ttu-id="e027a-129">Once all new product options are configured, click **Save** to create the new product.</span><span class="sxs-lookup"><span data-stu-id="e027a-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Products][api-management-products-page]

> <span data-ttu-id="e027a-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span><span class="sxs-lookup"><span data-stu-id="e027a-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="e027a-132">To configure a product, click on the product name in the **Products** tab.</span><span class="sxs-lookup"><span data-stu-id="e027a-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="e027a-133"><a name="add-apis"> </a>Add APIs to a product</span><span class="sxs-lookup"><span data-stu-id="e027a-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="e027a-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span><span class="sxs-lookup"><span data-stu-id="e027a-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="e027a-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span><span class="sxs-lookup"><span data-stu-id="e027a-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Summary][api-management-new-product-summary]

<span data-ttu-id="e027a-137">Before publishing your product you need to add one or more APIs.</span><span class="sxs-lookup"><span data-stu-id="e027a-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="e027a-138">To do this, click **Add API to product**.</span><span class="sxs-lookup"><span data-stu-id="e027a-138">To do this, click **Add API to product**.</span></span>

![Add APIs][api-management-add-apis-to-product]

<span data-ttu-id="e027a-140">Select the desired APIs and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e027a-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="e027a-141"><a name="add-description"> </a>Add descriptive information to a product</span><span class="sxs-lookup"><span data-stu-id="e027a-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="e027a-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span><span class="sxs-lookup"><span data-stu-id="e027a-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="e027a-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span><span class="sxs-lookup"><span data-stu-id="e027a-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Product settings][api-management-product-settings]

<span data-ttu-id="e027a-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span><span class="sxs-lookup"><span data-stu-id="e027a-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="e027a-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span><span class="sxs-lookup"><span data-stu-id="e027a-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="e027a-147">By default all product subscriptions are granted automatically.</span><span class="sxs-lookup"><span data-stu-id="e027a-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="e027a-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span><span class="sxs-lookup"><span data-stu-id="e027a-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="e027a-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span><span class="sxs-lookup"><span data-stu-id="e027a-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="e027a-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span><span class="sxs-lookup"><span data-stu-id="e027a-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="e027a-151"><a name="publish-product"> </a>Publish a product</span><span class="sxs-lookup"><span data-stu-id="e027a-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="e027a-152">Before the APIs in a product can be called, the product must be published.</span><span class="sxs-lookup"><span data-stu-id="e027a-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="e027a-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span><span class="sxs-lookup"><span data-stu-id="e027a-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="e027a-154">To make a previously published product private, click **Unpublish**.</span><span class="sxs-lookup"><span data-stu-id="e027a-154">To make a previously published product private, click **Unpublish**.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="e027a-156"><a name="make-visible"> </a>Make a product visible to developers</span><span class="sxs-lookup"><span data-stu-id="e027a-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="e027a-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span><span class="sxs-lookup"><span data-stu-id="e027a-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Product visibility][api-management-product-visiblity]

<span data-ttu-id="e027a-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e027a-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="e027a-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="e027a-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="e027a-161"><a name="view-subscribers"> </a>View subscribers to a product</span><span class="sxs-lookup"><span data-stu-id="e027a-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="e027a-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span><span class="sxs-lookup"><span data-stu-id="e027a-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="e027a-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span><span class="sxs-lookup"><span data-stu-id="e027a-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="e027a-164">In this example no developers have yet subscribed to the product.</span><span class="sxs-lookup"><span data-stu-id="e027a-164">In this example no developers have yet subscribed to the product.</span></span>

![Developers][api-management-developer-list]

## <span data-ttu-id="e027a-166"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="e027a-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="e027a-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span><span class="sxs-lookup"><span data-stu-id="e027a-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="e027a-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="e027a-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="e027a-169">For more information about working with products, see the following video.</span><span class="sxs-lookup"><span data-stu-id="e027a-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 












