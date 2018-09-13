---
title: Protect your API with Azure API Management | Microsoft Docs
description: Learn how to protect your API with quotas and throttling (rate-limiting) policies.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d7d9c9aa6607bd1a4bfbadd917fd2373d82217b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550456"
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="ca3c4-103">Protect your API with rate limits using Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ca3c4-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="ca3c4-104">This guide shows you how easy it is to add protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-104">This guide shows you how easy it is to add protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="ca3c4-105">In this tutorial, you will create a "Free Trial" API product that allows developers to make up to 10 calls per minute and up to a maximum of 200 calls per week to your API using the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-105">In this tutorial, you will create a "Free Trial" API product that allows developers to make up to 10 calls per minute and up to a maximum of 200 calls per week to your API using the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="ca3c4-106">You will then publish the API and test the rate limit policy.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-106">You will then publish the API and test the rate limit policy.</span></span>

<span data-ttu-id="ca3c4-107">For more advanced throttling scenarios using the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="ca3c4-107">For more advanced throttling scenarios using the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="ca3c4-108"><a name="create-product"> </a>To create a product</span><span class="sxs-lookup"><span data-stu-id="ca3c4-108"><a name="create-product"> </a>To create a product</span></span>
<span data-ttu-id="ca3c4-109">In this step, you will create a Free Trial product that does not require subscription approval.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="ca3c4-110">If you already have a product configured and want to use it for this tutorial, you can jump ahead to [Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow the tutorial from there using your product in place of the Free Trial product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-110">If you already have a product configured and want to use it for this tutorial, you can jump ahead to [Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow the tutorial from there using your product in place of the Free Trial product.</span></span>
> 
> 

<span data-ttu-id="ca3c4-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publisher portal][api-management-management-console]

> <span data-ttu-id="ca3c4-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="ca3c4-114">Click **Products** in the **API Management** menu on the left to display the **Products** page.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-114">Click **Products** in the **API Management** menu on the left to display the **Products** page.</span></span>

![Add product][api-management-add-product]

<span data-ttu-id="ca3c4-116">Click **Add product** to display the **Add new product** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-116">Click **Add product** to display the **Add new product** dialog box.</span></span>

![Add new product][api-management-new-product-window]

<span data-ttu-id="ca3c4-118">In the **Title** box, type **Free Trial**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-118">In the **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="ca3c4-119">In the **Description** box, type the following text: **Subscribers will be able to run 10 calls/minute up to a maximum of 200 calls/week after which access is denied.**</span><span class="sxs-lookup"><span data-stu-id="ca3c4-119">In the **Description** box, type the following text: **Subscribers will be able to run 10 calls/minute up to a maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="ca3c4-120">Products in API Management can be protected or open.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="ca3c4-121">Protected products must be subscribed to before they can be used.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-121">Protected products must be subscribed to before they can be used.</span></span> <span data-ttu-id="ca3c4-122">Open products can be used without a subscription.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="ca3c4-123">Ensure that **Require subscription** is selected to create a protected product that requires a subscription.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-123">Ensure that **Require subscription** is selected to create a protected product that requires a subscription.</span></span> <span data-ttu-id="ca3c4-124">This is the default setting.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-124">This is the default setting.</span></span>

<span data-ttu-id="ca3c4-125">If you want an administrator to review and accept or reject subscription attempts to this product, select **Require subscription approval**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-125">If you want an administrator to review and accept or reject subscription attempts to this product, select **Require subscription approval**.</span></span> <span data-ttu-id="ca3c4-126">If the check box is not selected, subscription attempts will be auto-approved.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-126">If the check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="ca3c4-127">In this example, subscriptions are automatically approved, so do not select the box.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-127">In this example, subscriptions are automatically approved, so do not select the box.</span></span>

<span data-ttu-id="ca3c4-128">To allow developer accounts to subscribe multiple times to the new product, select the **Allow multiple simultaneous subscriptions** check box.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-128">To allow developer accounts to subscribe multiple times to the new product, select the **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="ca3c4-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="ca3c4-130">After all values are entered, click **Save** to create the product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-130">After all values are entered, click **Save** to create the product.</span></span>

![Product added][api-management-product-added]

<span data-ttu-id="ca3c4-132">By default, new products are visible to users in the **Administrators** group.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-132">By default, new products are visible to users in the **Administrators** group.</span></span> <span data-ttu-id="ca3c4-133">We are going to add the **Developers** group.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-133">We are going to add the **Developers** group.</span></span> <span data-ttu-id="ca3c4-134">Click **Free Trial**, and then click the **Visibility** tab.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-134">Click **Free Trial**, and then click the **Visibility** tab.</span></span>

> <span data-ttu-id="ca3c4-135">In API Management, groups are used to manage the visibility of products to developers.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-135">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="ca3c4-136">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-136">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> <span data-ttu-id="ca3c4-137">For more information, see [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="ca3c4-137">For more information, see [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management].</span></span>
> 
> 

![Add developers group][api-management-add-developers-group]

<span data-ttu-id="ca3c4-139">Select the **Developers** check box, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-139">Select the **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="ca3c4-140"><a name="add-api"> </a>To add an API to the product</span><span class="sxs-lookup"><span data-stu-id="ca3c4-140"><a name="add-api"> </a>To add an API to the product</span></span>
<span data-ttu-id="ca3c4-141">In this step of the tutorial, we will add the Echo API to the new Free Trial product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-141">In this step of the tutorial, we will add the Echo API to the new Free Trial product.</span></span>

> <span data-ttu-id="ca3c4-142">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-142">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="ca3c4-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="ca3c4-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="ca3c4-144">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-144">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="ca3c4-146">Click **Add API to product**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-146">Click **Add API to product**.</span></span>

![Add API to product][api-management-add-api]

<span data-ttu-id="ca3c4-148">Select **Echo API**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-148">Select **Echo API**, and then click **Save**.</span></span>

![Add Echo API][api-management-add-echo-api]

## <span data-ttu-id="ca3c4-150"><a name="policies"> </a>To configure call rate limit and quota policies</span><span class="sxs-lookup"><span data-stu-id="ca3c4-150"><a name="policies"> </a>To configure call rate limit and quota policies</span></span>
<span data-ttu-id="ca3c4-151">Rate limits and quotas are configured in the policy editor.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-151">Rate limits and quotas are configured in the policy editor.</span></span> <span data-ttu-id="ca3c4-152">Click **Policies** under the **API Management** menu on the left.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-152">Click **Policies** under the **API Management** menu on the left.</span></span> <span data-ttu-id="ca3c4-153">In the **Product** list, click **Free Trial**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-153">In the **Product** list, click **Free Trial**.</span></span>

![Product policy][api-management-product-policy]

<span data-ttu-id="ca3c4-155">Click **Add Policy** to import the policy template and begin creating the rate limit and quota policies.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-155">Click **Add Policy** to import the policy template and begin creating the rate limit and quota policies.</span></span>

![Add policy][api-management-add-policy]

<span data-ttu-id="ca3c4-157">To insert policies, position the cursor into either the **inbound** or **outbound** section of the policy template.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-157">To insert policies, position the cursor into either the **inbound** or **outbound** section of the policy template.</span></span> <span data-ttu-id="ca3c4-158">Rate limit and quota policies are inbound policies, so position the cursor in the inbound element.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-158">Rate limit and quota policies are inbound policies, so position the cursor in the inbound element.</span></span>

![Policy editor][api-management-policy-editor-inbound]

<span data-ttu-id="ca3c4-160">The two policies we are adding in this tutorial are the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-160">The two policies we are adding in this tutorial are the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span>

![Policy statements][api-management-limit-policies]

<span data-ttu-id="ca3c4-162">After the cursor is positioned in the **inbound** policy element, click the arrow beside **Limit call rate per subscription** to insert its policy template.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-162">After the cursor is positioned in the **inbound** policy element, click the arrow beside **Limit call rate per subscription** to insert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="ca3c4-163">**Limit call rate per subscription** can be used at the product level and can also be used at the API and individual operation name levels.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-163">**Limit call rate per subscription** can be used at the product level and can also be used at the API and individual operation name levels.</span></span> <span data-ttu-id="ca3c4-164">In this tutorial, only product-level policies are used, so delete the **api** and **operation** elements from the **rate-limit** element, so only the outer **rate-limit** element remains, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-164">In this tutorial, only product-level policies are used, so delete the **api** and **operation** elements from the **rate-limit** element, so only the outer **rate-limit** element remains, as shown in the following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="ca3c4-165">In the Free Trial product, the maximum allowable call rate is 10 calls per minute, so type **10** as the value for the **calls** attribute, and **60** for the **renewal-period** attribute.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-165">In the Free Trial product, the maximum allowable call rate is 10 calls per minute, so type **10** as the value for the **calls** attribute, and **60** for the **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="ca3c4-166">To configure the **Set usage quota per subscription** policy, position your cursor immediately below the newly added **rate-limit** element within the **inbound** element, and then click the arrow to the left of **Set usage quota per subscription**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-166">To configure the **Set usage quota per subscription** policy, position your cursor immediately below the newly added **rate-limit** element within the **inbound** element, and then click the arrow to the left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="ca3c4-167">Because this policy is also intended to be at the product level, delete the **api** and **operation** name elements, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-167">Because this policy is also intended to be at the product level, delete the **api** and **operation** name elements, as shown in the following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="ca3c4-168">Quotas can be based on the number of calls per interval, bandwidth, or both.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-168">Quotas can be based on the number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="ca3c4-169">In this tutorial, we are not throttling based on bandwidth, so delete the **bandwidth** attribute.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-169">In this tutorial, we are not throttling based on bandwidth, so delete the **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="ca3c4-170">In the Free Trial product, the quota is 200 calls per week.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-170">In the Free Trial product, the quota is 200 calls per week.</span></span> <span data-ttu-id="ca3c4-171">Specify **200** as the value for the **calls** attribute, and then specify **604800** as the value for the **renewal-period** attribute.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-171">Specify **200** as the value for the **calls** attribute, and then specify **604800** as the value for the **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="ca3c4-172">Policy intervals are specified in seconds.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-172">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="ca3c4-173">To calculate the interval for a week, you can multiply the number of days (7) by the number of hours in a day (24) by the number of minutes in an hour (60) by the number of seconds in a minute (60): 7 \* 24 \* 60 \* 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-173">To calculate the interval for a week, you can multiply the number of days (7) by the number of hours in a day (24) by the number of minutes in an hour (60) by the number of seconds in a minute (60): 7 \* 24 \* 60 \* 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="ca3c4-174">When you have finished configuring the policy, it should match the following example.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-174">When you have finished configuring the policy, it should match the following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="ca3c4-175">After the desired policies are configured, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-175">After the desired policies are configured, click **Save**.</span></span>

![Save policy][api-management-policy-save]

## <span data-ttu-id="ca3c4-177"><a name="publish-product"> </a> To publish the product</span><span class="sxs-lookup"><span data-stu-id="ca3c4-177"><a name="publish-product"> </a> To publish the product</span></span>
<span data-ttu-id="ca3c4-178">Now that the the APIs are added and the policies are configured, the product must be published so that it can be used by developers.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-178">Now that the the APIs are added and the policies are configured, the product must be published so that it can be used by developers.</span></span> <span data-ttu-id="ca3c4-179">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-179">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="ca3c4-181">Click **Publish**, and then click **Yes, publish it** to confirm.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-181">Click **Publish**, and then click **Yes, publish it** to confirm.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="ca3c4-183"><a name="subscribe-account"> </a>To subscribe a developer account to the product</span><span class="sxs-lookup"><span data-stu-id="ca3c4-183"><a name="subscribe-account"> </a>To subscribe a developer account to the product</span></span>
<span data-ttu-id="ca3c4-184">Now that the product is published, it is available to be subscribed to and used by developers.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-184">Now that the product is published, it is available to be subscribed to and used by developers.</span></span>

> <span data-ttu-id="ca3c4-185">Administrators of an API Management instance are automatically subscribed to every product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-185">Administrators of an API Management instance are automatically subscribed to every product.</span></span> <span data-ttu-id="ca3c4-186">In this tutorial step, we will subscribe one of the non-administrator developer accounts to the Free Trial product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-186">In this tutorial step, we will subscribe one of the non-administrator developer accounts to the Free Trial product.</span></span> <span data-ttu-id="ca3c4-187">If your developer account is part of the Administrators role, then you can follow along with this step, even though you are already subscribed.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-187">If your developer account is part of the Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="ca3c4-188">Click **Users** on the **API Management** menu on the left, and then click the name of your developer account.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-188">Click **Users** on the **API Management** menu on the left, and then click the name of your developer account.</span></span> <span data-ttu-id="ca3c4-189">In this example, we are using the **Clayton Gragg** developer account.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-189">In this example, we are using the **Clayton Gragg** developer account.</span></span>

![Configure developer][api-management-configure-developer]

<span data-ttu-id="ca3c4-191">Click **Add Subscription**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-191">Click **Add Subscription**.</span></span>

![Add subscription][api-management-add-subscription-menu]

<span data-ttu-id="ca3c4-193">Select **Free Trial**, and then click **Subscribe**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-193">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Add subscription][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="ca3c4-195">In this tutorial, multiple simultaneous subscriptions are not enabled for the Free Trial product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-195">In this tutorial, multiple simultaneous subscriptions are not enabled for the Free Trial product.</span></span> <span data-ttu-id="ca3c4-196">If they were, you would be prompted to name the subscription, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-196">If they were, you would be prompted to name the subscription, as shown in the following example.</span></span>
> 
> 

![Add subscription][api-management-add-subscription-multiple]

<span data-ttu-id="ca3c4-198">After clicking **Subscribe**, the product appears in the **Subscription** list for the user.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-198">After clicking **Subscribe**, the product appears in the **Subscription** list for the user.</span></span>

![Subscription added][api-management-subscription-added]

## <span data-ttu-id="ca3c4-200"><a name="test-rate-limit"> </a>To call an operation and test the rate limit</span><span class="sxs-lookup"><span data-stu-id="ca3c4-200"><a name="test-rate-limit"> </a>To call an operation and test the rate limit</span></span>
<span data-ttu-id="ca3c4-201">Now that the Free Trial product is configured and published, we can call some operations and test the rate limit policy.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-201">Now that the Free Trial product is configured and published, we can call some operations and test the rate limit policy.</span></span>
<span data-ttu-id="ca3c4-202">Switch to the developer portal by clicking **Developer portal** in the upper-right menu.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-202">Switch to the developer portal by clicking **Developer portal** in the upper-right menu.</span></span>

![Developer portal][api-management-developer-portal-menu]

<span data-ttu-id="ca3c4-204">Click **APIs** in the top menu, and then click **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-204">Click **APIs** in the top menu, and then click **Echo API**.</span></span>

![Developer portal][api-management-developer-portal-api-menu]

<span data-ttu-id="ca3c4-206">Click **GET Resource**, and then click **Try it**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-206">Click **GET Resource**, and then click **Try it**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="ca3c4-208">Keep the default parameter values, and then select your subscription key for the Free Trial product.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-208">Keep the default parameter values, and then select your subscription key for the Free Trial product.</span></span>

![Subscription key][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="ca3c4-210">If you have multiple subscriptions, be sure to select the key for **Free Trial**, or else the policies that were configured in the previous steps won't be in effect.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-210">If you have multiple subscriptions, be sure to select the key for **Free Trial**, or else the policies that were configured in the previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="ca3c4-211">Click **Send**, and then view the response.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-211">Click **Send**, and then view the response.</span></span> <span data-ttu-id="ca3c4-212">Note the **Response status** of **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-212">Note the **Response status** of **200 OK**.</span></span>

![Operation results][api-management-http-get-results]

<span data-ttu-id="ca3c4-214">Click **Send** at a rate greater than the rate limit policy of 10 calls per minute.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-214">Click **Send** at a rate greater than the rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="ca3c4-215">After the rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-215">After the rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Operation results][api-management-http-get-429]

<span data-ttu-id="ca3c4-217">The **Response content** indicates the remaining interval before retries will be successful.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-217">The **Response content** indicates the remaining interval before retries will be successful.</span></span>

<span data-ttu-id="ca3c4-218">When the rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from the first of the 10 successful calls to the product before the rate limit was exceeded.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-218">When the rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from the first of the 10 successful calls to the product before the rate limit was exceeded.</span></span> <span data-ttu-id="ca3c4-219">In this example, the remaining interval is 54 seconds.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-219">In this example, the remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="ca3c4-220"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="ca3c4-220"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="ca3c4-221">Watch a demo of setting rate limits and quotas in the following video.</span><span class="sxs-lookup"><span data-stu-id="ca3c4-221">Watch a demo of setting rate limits and quotas in the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How to create and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers to a product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API to the product]: #add-api
[Publish the product]: #publish-product
[Subscribe a developer account to the product]: #subscribe-account
[Call an operation and test the rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota

























