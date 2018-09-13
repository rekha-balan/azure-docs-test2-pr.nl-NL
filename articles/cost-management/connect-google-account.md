---
title: Connect a Google Cloud Platform account to Azure Cost Management | Microsoft Docs
description: Connect a Google Cloud Platform account to view cost and usage data in Cost Management repots.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 06/07/2018
ms.topic: conceptual
ms.service: cost-management
manager: dougeby
ms.custom: ''
ms.openlocfilehash: b6243d66af76ca58fd758237fab8303e3f7a2e00
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858023"
---
# <a name="connect-a-google-cloud-platform-account"></a><span data-ttu-id="31c04-103">Connect a Google Cloud Platform account</span><span class="sxs-lookup"><span data-stu-id="31c04-103">Connect a Google Cloud Platform account</span></span>

<span data-ttu-id="31c04-104">You can connect your existing Google Cloud Platform account to Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="31c04-104">You can connect your existing Google Cloud Platform account to Azure Cost Management.</span></span> <span data-ttu-id="31c04-105">After you connect your account to Cost Management, cost and usage data is available in Cost Management reports.</span><span class="sxs-lookup"><span data-stu-id="31c04-105">After you connect your account to Cost Management, cost and usage data is available in Cost Management reports.</span></span> <span data-ttu-id="31c04-106">This article helps you to configure and connect your Google account with Cost Management.</span><span class="sxs-lookup"><span data-stu-id="31c04-106">This article helps you to configure and connect your Google account with Cost Management.</span></span>

## <a name="collect-project-information"></a><span data-ttu-id="31c04-107">Collect project information</span><span class="sxs-lookup"><span data-stu-id="31c04-107">Collect project information</span></span>

<span data-ttu-id="31c04-108">You start by gathering information about your project.</span><span class="sxs-lookup"><span data-stu-id="31c04-108">You start by gathering information about your project.</span></span>

1. <span data-ttu-id="31c04-109">Sign in to the Google Cloud Platform console at [https://console.cloud.google.com](https://console.cloud.google.com).</span><span class="sxs-lookup"><span data-stu-id="31c04-109">Sign in to the Google Cloud Platform console at [https://console.cloud.google.com](https://console.cloud.google.com).</span></span>
2. <span data-ttu-id="31c04-110">Review the project information that you want to onboard to Cost Management and note the **Project name** and the **Project ID**.</span><span class="sxs-lookup"><span data-stu-id="31c04-110">Review the project information that you want to onboard to Cost Management and note the **Project name** and the **Project ID**.</span></span> <span data-ttu-id="31c04-111">Keep the information handy for later steps.</span><span class="sxs-lookup"><span data-stu-id="31c04-111">Keep the information handy for later steps.</span></span>  
    <span data-ttu-id="31c04-112">![Google Cloud Platform console](./media/connect-google-account/gcp-console01.png)</span><span class="sxs-lookup"><span data-stu-id="31c04-112">![Google Cloud Platform console](./media/connect-google-account/gcp-console01.png)</span></span>
3. <span data-ttu-id="31c04-113">If billing is not enabled and linked to your project, create a billing account.</span><span class="sxs-lookup"><span data-stu-id="31c04-113">If billing is not enabled and linked to your project, create a billing account.</span></span> <span data-ttu-id="31c04-114">For more information, see [Create a new billing account](https://cloud.google.com/billing/docs/how-to/manage-billing-account#create\_a\_new\_billing\_account).</span><span class="sxs-lookup"><span data-stu-id="31c04-114">For more information, see [Create a new billing account](https://cloud.google.com/billing/docs/how-to/manage-billing-account#create\_a\_new\_billing\_account).</span></span>

## <a name="enable-storage-bucket-billing-export"></a><span data-ttu-id="31c04-115">Enable storage bucket billing export</span><span class="sxs-lookup"><span data-stu-id="31c04-115">Enable storage bucket billing export</span></span>

<span data-ttu-id="31c04-116">Cost Management retrieves your Google billing data from a storage bucket.</span><span class="sxs-lookup"><span data-stu-id="31c04-116">Cost Management retrieves your Google billing data from a storage bucket.</span></span> <span data-ttu-id="31c04-117">Keep the **Bucket name** and **Report prefix** information handy for later use during Cost Management registration.</span><span class="sxs-lookup"><span data-stu-id="31c04-117">Keep the **Bucket name** and **Report prefix** information handy for later use during Cost Management registration.</span></span>

<span data-ttu-id="31c04-118">Using Google Cloud Storage to store usage reports incurs minimal fees.</span><span class="sxs-lookup"><span data-stu-id="31c04-118">Using Google Cloud Storage to store usage reports incurs minimal fees.</span></span> <span data-ttu-id="31c04-119">For more information, see [Cloud Storage Pricing](https://cloud.google.com/storage/pricing).</span><span class="sxs-lookup"><span data-stu-id="31c04-119">For more information, see [Cloud Storage Pricing](https://cloud.google.com/storage/pricing).</span></span>

1. <span data-ttu-id="31c04-120">If you have not enabled billing export to a file, follow the instructions at [How to enable billing export to a file](https://cloud.google.com/billing/docs/how-to/export-data-file#how_to_enable_billing_export_to_a_file).</span><span class="sxs-lookup"><span data-stu-id="31c04-120">If you have not enabled billing export to a file, follow the instructions at [How to enable billing export to a file](https://cloud.google.com/billing/docs/how-to/export-data-file#how_to_enable_billing_export_to_a_file).</span></span> <span data-ttu-id="31c04-121">You can use either JSON or CSV billing export format.</span><span class="sxs-lookup"><span data-stu-id="31c04-121">You can use either JSON or CSV billing export format.</span></span>
2. <span data-ttu-id="31c04-122">Otherwise, in the Google Cloud Platform console, navigate to **Billing** > **Billing export**.</span><span class="sxs-lookup"><span data-stu-id="31c04-122">Otherwise, in the Google Cloud Platform console, navigate to **Billing** > **Billing export**.</span></span> <span data-ttu-id="31c04-123">Note your billing **Bucket name** and **Report prefix**.</span><span class="sxs-lookup"><span data-stu-id="31c04-123">Note your billing **Bucket name** and **Report prefix**.</span></span>  
    <span data-ttu-id="31c04-124">![Billing export](./media/connect-google-account/billing-export.png)</span><span class="sxs-lookup"><span data-stu-id="31c04-124">![Billing export](./media/connect-google-account/billing-export.png)</span></span>

## <a name="enable-google-cloud-platform-apis"></a><span data-ttu-id="31c04-125">Enable Google Cloud Platform APIs</span><span class="sxs-lookup"><span data-stu-id="31c04-125">Enable Google Cloud Platform APIs</span></span>

<span data-ttu-id="31c04-126">To collect usage and asset information, Cost Management needs the following Google Cloud Platform APIs enabled:</span><span class="sxs-lookup"><span data-stu-id="31c04-126">To collect usage and asset information, Cost Management needs the following Google Cloud Platform APIs enabled:</span></span>

- <span data-ttu-id="31c04-127">BigQuery API</span><span class="sxs-lookup"><span data-stu-id="31c04-127">BigQuery API</span></span>
- <span data-ttu-id="31c04-128">Google Cloud SQL</span><span class="sxs-lookup"><span data-stu-id="31c04-128">Google Cloud SQL</span></span>
- <span data-ttu-id="31c04-129">Google Cloud Datastore API</span><span class="sxs-lookup"><span data-stu-id="31c04-129">Google Cloud Datastore API</span></span>
- <span data-ttu-id="31c04-130">Google Cloud Storage</span><span class="sxs-lookup"><span data-stu-id="31c04-130">Google Cloud Storage</span></span>
- <span data-ttu-id="31c04-131">Google Cloud Storage JSON API</span><span class="sxs-lookup"><span data-stu-id="31c04-131">Google Cloud Storage JSON API</span></span>
- <span data-ttu-id="31c04-132">Google Compute Engine API</span><span class="sxs-lookup"><span data-stu-id="31c04-132">Google Compute Engine API</span></span>

### <a name="enable-or-verify-apis"></a><span data-ttu-id="31c04-133">Enable or verify APIs</span><span class="sxs-lookup"><span data-stu-id="31c04-133">Enable or verify APIs</span></span>

1. <span data-ttu-id="31c04-134">In the Google Cloud Platform console, select the project that you want to register with Cost Management.</span><span class="sxs-lookup"><span data-stu-id="31c04-134">In the Google Cloud Platform console, select the project that you want to register with Cost Management.</span></span>
2. <span data-ttu-id="31c04-135">Navigate to **APIs & Services** > **Library**.</span><span class="sxs-lookup"><span data-stu-id="31c04-135">Navigate to **APIs & Services** > **Library**.</span></span>
3. <span data-ttu-id="31c04-136">Use search to find each previously listed API.</span><span class="sxs-lookup"><span data-stu-id="31c04-136">Use search to find each previously listed API.</span></span>
4. <span data-ttu-id="31c04-137">For each API, verify that **API enabled** is shown.</span><span class="sxs-lookup"><span data-stu-id="31c04-137">For each API, verify that **API enabled** is shown.</span></span> <span data-ttu-id="31c04-138">Otherwise, click **ENABLE**.</span><span class="sxs-lookup"><span data-stu-id="31c04-138">Otherwise, click **ENABLE**.</span></span>

## <a name="add-a-google-cloud-account-to-cost-management"></a><span data-ttu-id="31c04-139">Add a Google Cloud account to Cost Management</span><span class="sxs-lookup"><span data-stu-id="31c04-139">Add a Google Cloud account to Cost Management</span></span>

1. <span data-ttu-id="31c04-140">Open the Cloudyn portal from the Azure portal or navigate to [https://azure.cloudyn.com](https://azure.cloudyn.com/) and sign in.</span><span class="sxs-lookup"><span data-stu-id="31c04-140">Open the Cloudyn portal from the Azure portal or navigate to [https://azure.cloudyn.com](https://azure.cloudyn.com/) and sign in.</span></span>
2. <span data-ttu-id="31c04-141">Click **Settings** (cog symbol) and then select **Cloud Accounts**.</span><span class="sxs-lookup"><span data-stu-id="31c04-141">Click **Settings** (cog symbol) and then select **Cloud Accounts**.</span></span>
3. <span data-ttu-id="31c04-142">In **Accounts Management**, select the **Google Accounts** tab and then click **Add new +**.</span><span class="sxs-lookup"><span data-stu-id="31c04-142">In **Accounts Management**, select the **Google Accounts** tab and then click **Add new +**.</span></span>
4. <span data-ttu-id="31c04-143">In **Google Account Name**, enter the email address for the billing account then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="31c04-143">In **Google Account Name**, enter the email address for the billing account then click **Next**.</span></span>
5. <span data-ttu-id="31c04-144">In the Google authentication dialog, select or enter a Google account and then **ALLOW** cloudyn.com access to your account.</span><span class="sxs-lookup"><span data-stu-id="31c04-144">In the Google authentication dialog, select or enter a Google account and then **ALLOW** cloudyn.com access to your account.</span></span>
6. <span data-ttu-id="31c04-145">Add the request project information that you had previous noted.</span><span class="sxs-lookup"><span data-stu-id="31c04-145">Add the request project information that you had previous noted.</span></span> <span data-ttu-id="31c04-146">They include **Project ID**, **Project** name, **billing** bucket name, and **billing file** Report prefix then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="31c04-146">They include **Project ID**, **Project** name, **billing** bucket name, and **billing file** Report prefix then click **Save**.</span></span>  
    <span data-ttu-id="31c04-147">![Add Google project](./media/connect-google-account/add-project.png)</span><span class="sxs-lookup"><span data-stu-id="31c04-147">![Add Google project](./media/connect-google-account/add-project.png)</span></span>

<span data-ttu-id="31c04-148">Your Google account appears in the list of accounts and it should say **Authenticated**.</span><span class="sxs-lookup"><span data-stu-id="31c04-148">Your Google account appears in the list of accounts and it should say **Authenticated**.</span></span> <span data-ttu-id="31c04-149">Under it, your Google project name and ID should appear and have a green check mark symbol.</span><span class="sxs-lookup"><span data-stu-id="31c04-149">Under it, your Google project name and ID should appear and have a green check mark symbol.</span></span> <span data-ttu-id="31c04-150">Account Status should say **Completed**.</span><span class="sxs-lookup"><span data-stu-id="31c04-150">Account Status should say **Completed**.</span></span>

<span data-ttu-id="31c04-151">Within a few hours, Cost Management reports show Google cost and usage information.</span><span class="sxs-lookup"><span data-stu-id="31c04-151">Within a few hours, Cost Management reports show Google cost and usage information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31c04-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="31c04-152">Next steps</span></span>

- <span data-ttu-id="31c04-153">To learn more about Azure Cost Management, continue to the [Review usage and costs](./tutorial-review-usage.md) tutorial for Cost Management.</span><span class="sxs-lookup"><span data-stu-id="31c04-153">To learn more about Azure Cost Management, continue to the [Review usage and costs](./tutorial-review-usage.md) tutorial for Cost Management.</span></span>
