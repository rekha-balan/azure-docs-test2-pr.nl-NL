---
title: Product templates in Azure API Management | Microsoft Docs
description: Learn how to customize the content of the product pages in the Azure API Management developer portal.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 36db99914da92ef0845c1ca20872ed19dce901f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670487"
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="ea53f-103">Product templates in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ea53f-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="ea53f-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span><span class="sxs-lookup"><span data-stu-id="ea53f-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="ea53f-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span><span class="sxs-lookup"><span data-stu-id="ea53f-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="ea53f-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="ea53f-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="ea53f-107">Product list</span><span class="sxs-lookup"><span data-stu-id="ea53f-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="ea53f-108">Product</span><span class="sxs-lookup"><span data-stu-id="ea53f-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="ea53f-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span><span class="sxs-lookup"><span data-stu-id="ea53f-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="ea53f-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span><span class="sxs-lookup"><span data-stu-id="ea53f-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="ea53f-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="ea53f-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <a name="ProductList"></a> <span data-ttu-id="ea53f-112">Product list</span><span class="sxs-lookup"><span data-stu-id="ea53f-112">Product list</span></span>  
 <span data-ttu-id="ea53f-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="ea53f-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="ea53f-114">![Products list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-product-templates/apim_productslisttemplatepage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="ea53f-114">![Products list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-product-templates/apim_productslisttemplatepage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ea53f-115">Default template</span><span class="sxs-lookup"><span data-stu-id="ea53f-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="ea53f-116">Controls</span><span class="sxs-lookup"><span data-stu-id="ea53f-116">Controls</span></span>  
 <span data-ttu-id="ea53f-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="ea53f-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ea53f-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="ea53f-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="ea53f-119">search-control</span><span class="sxs-lookup"><span data-stu-id="ea53f-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="ea53f-120">Data model</span><span class="sxs-lookup"><span data-stu-id="ea53f-120">Data model</span></span>  
  
|<span data-ttu-id="ea53f-121">Property</span><span class="sxs-lookup"><span data-stu-id="ea53f-121">Property</span></span>|<span data-ttu-id="ea53f-122">Type</span><span class="sxs-lookup"><span data-stu-id="ea53f-122">Type</span></span>|<span data-ttu-id="ea53f-123">Description</span><span class="sxs-lookup"><span data-stu-id="ea53f-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ea53f-124">Paging</span><span class="sxs-lookup"><span data-stu-id="ea53f-124">Paging</span></span>|<span data-ttu-id="ea53f-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span><span class="sxs-lookup"><span data-stu-id="ea53f-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="ea53f-126">The paging information for the products collection.</span><span class="sxs-lookup"><span data-stu-id="ea53f-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="ea53f-127">Filtering</span><span class="sxs-lookup"><span data-stu-id="ea53f-127">Filtering</span></span>|<span data-ttu-id="ea53f-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span><span class="sxs-lookup"><span data-stu-id="ea53f-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="ea53f-129">The filtering information for the products list page.</span><span class="sxs-lookup"><span data-stu-id="ea53f-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="ea53f-130">Products</span><span class="sxs-lookup"><span data-stu-id="ea53f-130">Products</span></span>|<span data-ttu-id="ea53f-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span><span class="sxs-lookup"><span data-stu-id="ea53f-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="ea53f-132">The products visible to the current user.</span><span class="sxs-lookup"><span data-stu-id="ea53f-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ea53f-133">Sample template data</span><span class="sxs-lookup"><span data-stu-id="ea53f-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <a name="Product"></a> <span data-ttu-id="ea53f-134">Product</span><span class="sxs-lookup"><span data-stu-id="ea53f-134">Product</span></span>  
 <span data-ttu-id="ea53f-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="ea53f-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="ea53f-136">![Developer portal product page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-product-templates/apim_productpage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="ea53f-136">![Developer portal product page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-product-templates/apim_productpage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ea53f-137">Default template</span><span class="sxs-lookup"><span data-stu-id="ea53f-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="ea53f-138">Controls</span><span class="sxs-lookup"><span data-stu-id="ea53f-138">Controls</span></span>  
 <span data-ttu-id="ea53f-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="ea53f-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ea53f-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="ea53f-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="ea53f-141">Data model</span><span class="sxs-lookup"><span data-stu-id="ea53f-141">Data model</span></span>  
  
|<span data-ttu-id="ea53f-142">Property</span><span class="sxs-lookup"><span data-stu-id="ea53f-142">Property</span></span>|<span data-ttu-id="ea53f-143">Type</span><span class="sxs-lookup"><span data-stu-id="ea53f-143">Type</span></span>|<span data-ttu-id="ea53f-144">Description</span><span class="sxs-lookup"><span data-stu-id="ea53f-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ea53f-145">Product</span><span class="sxs-lookup"><span data-stu-id="ea53f-145">Product</span></span>|[<span data-ttu-id="ea53f-146">Product</span><span class="sxs-lookup"><span data-stu-id="ea53f-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="ea53f-147">The specified product.</span><span class="sxs-lookup"><span data-stu-id="ea53f-147">The specified product.</span></span>|  
|<span data-ttu-id="ea53f-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="ea53f-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="ea53f-149">boolean</span><span class="sxs-lookup"><span data-stu-id="ea53f-149">boolean</span></span>|<span data-ttu-id="ea53f-150">Whether the current user is subscribed to this product.</span><span class="sxs-lookup"><span data-stu-id="ea53f-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="ea53f-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="ea53f-151">SubscriptionState</span></span>|<span data-ttu-id="ea53f-152">number</span><span class="sxs-lookup"><span data-stu-id="ea53f-152">number</span></span>|<span data-ttu-id="ea53f-153">The state of the subscription.</span><span class="sxs-lookup"><span data-stu-id="ea53f-153">The state of the subscription.</span></span> <span data-ttu-id="ea53f-154">Possible states are:</span><span class="sxs-lookup"><span data-stu-id="ea53f-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="ea53f-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span><span class="sxs-lookup"><span data-stu-id="ea53f-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="ea53f-156">-   `1 - active` – the subscription is active.</span><span class="sxs-lookup"><span data-stu-id="ea53f-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="ea53f-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span><span class="sxs-lookup"><span data-stu-id="ea53f-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="ea53f-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span><span class="sxs-lookup"><span data-stu-id="ea53f-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="ea53f-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span><span class="sxs-lookup"><span data-stu-id="ea53f-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="ea53f-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span><span class="sxs-lookup"><span data-stu-id="ea53f-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="ea53f-161">Limits</span><span class="sxs-lookup"><span data-stu-id="ea53f-161">Limits</span></span>|<span data-ttu-id="ea53f-162">array</span><span class="sxs-lookup"><span data-stu-id="ea53f-162">array</span></span>|<span data-ttu-id="ea53f-163">This property is deprecated and should not be used.</span><span class="sxs-lookup"><span data-stu-id="ea53f-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="ea53f-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="ea53f-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="ea53f-165">boolean</span><span class="sxs-lookup"><span data-stu-id="ea53f-165">boolean</span></span>|<span data-ttu-id="ea53f-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span><span class="sxs-lookup"><span data-stu-id="ea53f-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="ea53f-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="ea53f-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="ea53f-168">string</span><span class="sxs-lookup"><span data-stu-id="ea53f-168">string</span></span>|<span data-ttu-id="ea53f-169">If delegation is enabled, the delegated subscription URL.</span><span class="sxs-lookup"><span data-stu-id="ea53f-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="ea53f-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="ea53f-170">IsAgreed</span></span>|<span data-ttu-id="ea53f-171">boolean</span><span class="sxs-lookup"><span data-stu-id="ea53f-171">boolean</span></span>|<span data-ttu-id="ea53f-172">If the product has terms, whether the current user has agreed to the terms.</span><span class="sxs-lookup"><span data-stu-id="ea53f-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="ea53f-173">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="ea53f-173">Subscriptions</span></span>|<span data-ttu-id="ea53f-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span><span class="sxs-lookup"><span data-stu-id="ea53f-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="ea53f-175">The subscriptions to the product.</span><span class="sxs-lookup"><span data-stu-id="ea53f-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="ea53f-176">Apis</span><span class="sxs-lookup"><span data-stu-id="ea53f-176">Apis</span></span>|<span data-ttu-id="ea53f-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span><span class="sxs-lookup"><span data-stu-id="ea53f-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="ea53f-178">The APIs in this product.</span><span class="sxs-lookup"><span data-stu-id="ea53f-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="ea53f-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="ea53f-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="ea53f-180">boolean</span><span class="sxs-lookup"><span data-stu-id="ea53f-180">boolean</span></span>|<span data-ttu-id="ea53f-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span><span class="sxs-lookup"><span data-stu-id="ea53f-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="ea53f-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="ea53f-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="ea53f-183">boolean</span><span class="sxs-lookup"><span data-stu-id="ea53f-183">boolean</span></span>|<span data-ttu-id="ea53f-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span><span class="sxs-lookup"><span data-stu-id="ea53f-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ea53f-185">Sample template data</span><span class="sxs-lookup"><span data-stu-id="ea53f-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="ea53f-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea53f-186">Next steps</span></span>
<span data-ttu-id="ea53f-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ea53f-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>

