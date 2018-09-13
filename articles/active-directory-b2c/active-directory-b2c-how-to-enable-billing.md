---
title: How to Link an Azure Subscription to Azure AD B2C | Microsoft Docs
description: Step-by-step guide to enable billing for Azure AD B2C tenant into an Azure subscription.
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 3903dc75cbbcc0f9a0a9bf7af89b1894289a42eb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669183"
---
# <a name="linking-an-azure-subscription-to-an-azure-b2c-tenant-to-pay-for-usage-charges"></a><span data-ttu-id="34c60-103">Linking an Azure Subscription to an Azure B2C tenant to pay for usage charges</span><span class="sxs-lookup"><span data-stu-id="34c60-103">Linking an Azure Subscription to an Azure B2C tenant to pay for usage charges</span></span>

<span data-ttu-id="34c60-104">Ongoing usage charges for Azure Active Directory B2C (or Azure AD B2C) are billed to an Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="34c60-104">Ongoing usage charges for Azure Active Directory B2C (or Azure AD B2C) are billed to an Azure Subscription.</span></span> <span data-ttu-id="34c60-105">It is necessary for the tenant administrator to explicitly link the Azure AD B2C tenant to an Azure subscription after creating the B2C tenant itself.</span><span class="sxs-lookup"><span data-stu-id="34c60-105">It is necessary for the tenant administrator to explicitly link the Azure AD B2C tenant to an Azure subscription after creating the B2C tenant itself.</span></span>  <span data-ttu-id="34c60-106">This link is achieved by creating an Azure AD "B2C Tenant" resource in the target Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="34c60-106">This link is achieved by creating an Azure AD "B2C Tenant" resource in the target Azure subscription.</span></span> <span data-ttu-id="34c60-107">Many B2C tenants can be linked to a single Azure subscription along with other Azure resources (for example, VMs, Data storage, LogicApps)</span><span class="sxs-lookup"><span data-stu-id="34c60-107">Many B2C tenants can be linked to a single Azure subscription along with other Azure resources (for example, VMs, Data storage, LogicApps)</span></span>


> [!IMPORTANT]
> <span data-ttu-id="34c60-108">The latest information on usage billing and pricing for B2C is at the following page: [Azure AD B2C Pricing](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span><span class="sxs-lookup"><span data-stu-id="34c60-108">The latest information on usage billing and pricing for B2C is at the following page: [Azure AD B2C Pricing](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span></span>

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="34c60-109">Step 1 - Create an Azure AD B2C Tenant</span><span class="sxs-lookup"><span data-stu-id="34c60-109">Step 1 - Create an Azure AD B2C Tenant</span></span>

<span data-ttu-id="34c60-110">B2C tenant creation must be completed first.</span><span class="sxs-lookup"><span data-stu-id="34c60-110">B2C tenant creation must be completed first.</span></span> <span data-ttu-id="34c60-111">Skip this step if you have already created your target B2C Tenant.</span><span class="sxs-lookup"><span data-stu-id="34c60-111">Skip this step if you have already created your target B2C Tenant.</span></span> [<span data-ttu-id="34c60-112">Get started with Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="34c60-112">Get started with Azure AD B2C</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-b2c-get-started/)

## <a name="step-2---open-azure-portal-in-the-azure-ad-tenant-that-shows-your-azure-subscription"></a><span data-ttu-id="34c60-113">Step 2 - Open Azure portal in the Azure AD Tenant that shows your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="34c60-113">Step 2 - Open Azure portal in the Azure AD Tenant that shows your Azure subscription</span></span>
<span data-ttu-id="34c60-114">Navigate to portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="34c60-114">Navigate to portal.azure.com.</span></span> <span data-ttu-id="34c60-115">Switch to the Azure AD Tenant that shows the Azure subscription you would like to use.</span><span class="sxs-lookup"><span data-stu-id="34c60-115">Switch to the Azure AD Tenant that shows the Azure subscription you would like to use.</span></span> <span data-ttu-id="34c60-116">This Azure AD tenant is different from the B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="34c60-116">This Azure AD tenant is different from the B2C tenant.</span></span> <span data-ttu-id="34c60-117">Within the Azure portal, click the account name on the upper right of the dashboard to select the Azure AD Tenant.</span><span class="sxs-lookup"><span data-stu-id="34c60-117">Within the Azure portal, click the account name on the upper right of the dashboard to select the Azure AD Tenant.</span></span> <span data-ttu-id="34c60-118">An Azure subscription is needed to proceed.</span><span class="sxs-lookup"><span data-stu-id="34c60-118">An Azure subscription is needed to proceed.</span></span> [<span data-ttu-id="34c60-119">Get an Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="34c60-119">Get an Azure Subscription</span></span>](https://account.windowsazure.com/signup?showCatalog=True)

![Switching to your Azure AD Tenant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a><span data-ttu-id="34c60-121">Step 3 - Create a B2C Tenant resource in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="34c60-121">Step 3 - Create a B2C Tenant resource in Azure Marketplace</span></span>
<span data-ttu-id="34c60-122">Open Marketplace by clicking the Marketplace icon, or selecting the green "+" in the upper left corner of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="34c60-122">Open Marketplace by clicking the Marketplace icon, or selecting the green "+" in the upper left corner of the dashboard.</span></span>  <span data-ttu-id="34c60-123">Search for and select Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="34c60-123">Search for and select Azure Active Directory B2C.</span></span> <span data-ttu-id="34c60-124">Select Create.</span><span class="sxs-lookup"><span data-stu-id="34c60-124">Select Create.</span></span>
<span data-ttu-id="34c60-125">![Select Marketplace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-how-to-enable-billing/marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="34c60-125">![Select Marketplace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-how-to-enable-billing/marketplace.png)</span></span>

![Search AD B2C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

<span data-ttu-id="34c60-127">The Azure AD B2C Resource create dialog covers the following parameters:</span><span class="sxs-lookup"><span data-stu-id="34c60-127">The Azure AD B2C Resource create dialog covers the following parameters:</span></span>

1. <span data-ttu-id="34c60-128">Azure AD B2C Tenant – Select an Azure AD B2C Tenant from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="34c60-128">Azure AD B2C Tenant – Select an Azure AD B2C Tenant from the dropdown.</span></span>  <span data-ttu-id="34c60-129">Only eligible Azure AD B2C tenants show.</span><span class="sxs-lookup"><span data-stu-id="34c60-129">Only eligible Azure AD B2C tenants show.</span></span>  <span data-ttu-id="34c60-130">Eligible B2C tenants meet these conditions: You are the global administrator of the B2C tenant, and the B2C tenant is not currently associated to an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="34c60-130">Eligible B2C tenants meet these conditions: You are the global administrator of the B2C tenant, and the B2C tenant is not currently associated to an Azure subscription</span></span>

2. <span data-ttu-id="34c60-131">Azure AD B2C Resource name - is preselected to match the domain name of the B2C Tenant</span><span class="sxs-lookup"><span data-stu-id="34c60-131">Azure AD B2C Resource name - is preselected to match the domain name of the B2C Tenant</span></span>

3. <span data-ttu-id="34c60-132">Subscription - An active Azure subscription in which you are an administrator or a co-administrator.</span><span class="sxs-lookup"><span data-stu-id="34c60-132">Subscription - An active Azure subscription in which you are an administrator or a co-administrator.</span></span>  <span data-ttu-id="34c60-133">Multiple Azure AD B2C Tenants may be added to one Azure subscription</span><span class="sxs-lookup"><span data-stu-id="34c60-133">Multiple Azure AD B2C Tenants may be added to one Azure subscription</span></span>

4. <span data-ttu-id="34c60-134">Resource Group and Resource Group location - This artifact helps you organize multiple Azure resources.</span><span class="sxs-lookup"><span data-stu-id="34c60-134">Resource Group and Resource Group location - This artifact helps you organize multiple Azure resources.</span></span>  <span data-ttu-id="34c60-135">This choice has no impact on your B2C tenant location, performance, or billing status</span><span class="sxs-lookup"><span data-stu-id="34c60-135">This choice has no impact on your B2C tenant location, performance, or billing status</span></span>

5. <span data-ttu-id="34c60-136">Pin to dashboard for easiest access to your B2C tenant billing information and the B2C tenant settings ![Create B2C Resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span><span class="sxs-lookup"><span data-stu-id="34c60-136">Pin to dashboard for easiest access to your B2C tenant billing information and the B2C tenant settings ![Create B2C Resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span></span>

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a><span data-ttu-id="34c60-137">Step 4 - Manage your B2C Tenant resources (optional)</span><span class="sxs-lookup"><span data-stu-id="34c60-137">Step 4 - Manage your B2C Tenant resources (optional)</span></span>
<span data-ttu-id="34c60-138">Once deployment is complete, a new "B2C Tenant" resource is created in the target resource group and related Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="34c60-138">Once deployment is complete, a new "B2C Tenant" resource is created in the target resource group and related Azure subscription.</span></span>  <span data-ttu-id="34c60-139">You should see a new resource of type "B2C Tenant" added alongside your other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="34c60-139">You should see a new resource of type "B2C Tenant" added alongside your other Azure resources.</span></span>

![Create B2C Resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

<span data-ttu-id="34c60-141">By clicking the B2C tenant resource, you are able to</span><span class="sxs-lookup"><span data-stu-id="34c60-141">By clicking the B2C tenant resource, you are able to</span></span>
- <span data-ttu-id="34c60-142">Click Subscription name to review billing information.</span><span class="sxs-lookup"><span data-stu-id="34c60-142">Click Subscription name to review billing information.</span></span> <span data-ttu-id="34c60-143">See Billing & Usage.</span><span class="sxs-lookup"><span data-stu-id="34c60-143">See Billing & Usage.</span></span>
- <span data-ttu-id="34c60-144">Click Azure AD B2C Settings to open a new browser tab directly in to your B2C tenant Settings blade</span><span class="sxs-lookup"><span data-stu-id="34c60-144">Click Azure AD B2C Settings to open a new browser tab directly in to your B2C tenant Settings blade</span></span>
- <span data-ttu-id="34c60-145">Submit a support request</span><span class="sxs-lookup"><span data-stu-id="34c60-145">Submit a support request</span></span>
- <span data-ttu-id="34c60-146">Move your B2C tenant resource to another Azure Subscription, or to another Resource Group.</span><span class="sxs-lookup"><span data-stu-id="34c60-146">Move your B2C tenant resource to another Azure Subscription, or to another Resource Group.</span></span>  <span data-ttu-id="34c60-147">This choice changes which Azure subscription receives usage charges.</span><span class="sxs-lookup"><span data-stu-id="34c60-147">This choice changes which Azure subscription receives usage charges.</span></span>

![B2C Resource settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.PNG)

## <a name="known-issues"></a><span data-ttu-id="34c60-149">Known Issues</span><span class="sxs-lookup"><span data-stu-id="34c60-149">Known Issues</span></span>
- <span data-ttu-id="34c60-150">B2C Tenant deletion.</span><span class="sxs-lookup"><span data-stu-id="34c60-150">B2C Tenant deletion.</span></span> <span data-ttu-id="34c60-151">If a B2C Tenant is created, deleted, and re-created with the same domain name, please also delete and re-create the "Linking" resource with the same domain name.</span><span class="sxs-lookup"><span data-stu-id="34c60-151">If a B2C Tenant is created, deleted, and re-created with the same domain name, please also delete and re-create the "Linking" resource with the same domain name.</span></span>  <span data-ttu-id="34c60-152">You will find this "Linking" resource under "All resources" in the subscription tenant via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="34c60-152">You will find this "Linking" resource under "All resources" in the subscription tenant via the Azure portal.</span></span>
- <span data-ttu-id="34c60-153">Self-imposed restrictions on regional resource location.</span><span class="sxs-lookup"><span data-stu-id="34c60-153">Self-imposed restrictions on regional resource location.</span></span>  <span data-ttu-id="34c60-154">In rare cases, a user may have established a regional restriction for Azure resource creation.</span><span class="sxs-lookup"><span data-stu-id="34c60-154">In rare cases, a user may have established a regional restriction for Azure resource creation.</span></span>  <span data-ttu-id="34c60-155">This restriction may prevent the creation of the Link between an Azure subscription and a B2C Tenant.</span><span class="sxs-lookup"><span data-stu-id="34c60-155">This restriction may prevent the creation of the Link between an Azure subscription and a B2C Tenant.</span></span> <span data-ttu-id="34c60-156">To mitigate, please relax this restriction.</span><span class="sxs-lookup"><span data-stu-id="34c60-156">To mitigate, please relax this restriction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34c60-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="34c60-157">Next steps</span></span>
<span data-ttu-id="34c60-158">Once these steps are complete for each of your B2C tenants, your Azure subscription is billed in accordance with your Azure Direct or Enterprise Agreement details.</span><span class="sxs-lookup"><span data-stu-id="34c60-158">Once these steps are complete for each of your B2C tenants, your Azure subscription is billed in accordance with your Azure Direct or Enterprise Agreement details.</span></span>
- <span data-ttu-id="34c60-159">Review usage and billing within your selected Azure subscription</span><span class="sxs-lookup"><span data-stu-id="34c60-159">Review usage and billing within your selected Azure subscription</span></span>
- <span data-ttu-id="34c60-160">Review detailed day-by-day usage reports using the [Usage Reporting API](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)</span><span class="sxs-lookup"><span data-stu-id="34c60-160">Review detailed day-by-day usage reports using the [Usage Reporting API](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)</span></span>



<!--Reference style links - using these makes the source content way more readable than using inline links-->
[gog]: http://google.com/        
[yah]: http://search.yahoo.com/  
[msn]: http://search.msn.com/    






