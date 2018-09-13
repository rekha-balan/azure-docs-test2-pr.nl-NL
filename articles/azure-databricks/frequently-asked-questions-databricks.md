---
title: 'Azure Databricks: Common questions and help | Microsoft Docs'
description: Get answers to common questions and troubleshooting information about Azure Databricks.
services: azure-databricks
documentationcenter: ''
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: c3ba235c60480c38a21ee3264c54b4a4dcdea340
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865127"
---
# <a name="frequently-asked-questions-about-azure-databricks"></a><span data-ttu-id="b2978-103">Frequently asked questions about Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="b2978-103">Frequently asked questions about Azure Databricks</span></span>

<span data-ttu-id="b2978-104">This article lists the top queries you might have related to Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="b2978-104">This article lists the top queries you might have related to Azure Databricks.</span></span> <span data-ttu-id="b2978-105">It also lists some common problems you might have while using Databricks.</span><span class="sxs-lookup"><span data-stu-id="b2978-105">It also lists some common problems you might have while using Databricks.</span></span> <span data-ttu-id="b2978-106">For more information, see [What is Azure Databricks](what-is-azure-databricks.md).</span><span class="sxs-lookup"><span data-stu-id="b2978-106">For more information, see [What is Azure Databricks](what-is-azure-databricks.md).</span></span> 

## <a name="can-i-use-my-own-keys-for-local-encryption"></a><span data-ttu-id="b2978-107">Can I use my own keys for local encryption?</span><span class="sxs-lookup"><span data-stu-id="b2978-107">Can I use my own keys for local encryption?</span></span> 
<span data-ttu-id="b2978-108">In the current release, using your own keys from Azure Key Vault is not supported.</span><span class="sxs-lookup"><span data-stu-id="b2978-108">In the current release, using your own keys from Azure Key Vault is not supported.</span></span> 

## <a name="can-i-use-azure-virtual-networks-with-databricks"></a><span data-ttu-id="b2978-109">Can I use Azure virtual networks with Databricks?</span><span class="sxs-lookup"><span data-stu-id="b2978-109">Can I use Azure virtual networks with Databricks?</span></span>
<span data-ttu-id="b2978-110">A new virtual network is created as part of Databricks provisioning.</span><span class="sxs-lookup"><span data-stu-id="b2978-110">A new virtual network is created as part of Databricks provisioning.</span></span> <span data-ttu-id="b2978-111">In this release, you cannot use your own Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="b2978-111">In this release, you cannot use your own Azure virtual network.</span></span>

## <a name="how-do-i-access-azure-data-lake-store-from-a-notebook"></a><span data-ttu-id="b2978-112">How do I access Azure Data Lake Store from a notebook?</span><span class="sxs-lookup"><span data-stu-id="b2978-112">How do I access Azure Data Lake Store from a notebook?</span></span> 

<span data-ttu-id="b2978-113">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b2978-113">Follow these steps:</span></span>
1. <span data-ttu-id="b2978-114">In Azure Active Directory (Azure AD), provision a service principal, and record its key.</span><span class="sxs-lookup"><span data-stu-id="b2978-114">In Azure Active Directory (Azure AD), provision a service principal, and record its key.</span></span>
1. <span data-ttu-id="b2978-115">Assign the necessary permissions to the service principal in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b2978-115">Assign the necessary permissions to the service principal in Data Lake Store.</span></span>
1. <span data-ttu-id="b2978-116">To access a file in Data Lake Store, use the service principal credentials in Notebook.</span><span class="sxs-lookup"><span data-stu-id="b2978-116">To access a file in Data Lake Store, use the service principal credentials in Notebook.</span></span>

<span data-ttu-id="b2978-117">For more information, see [Use Data Lake Store with Azure Databricks](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-datalake.html).</span><span class="sxs-lookup"><span data-stu-id="b2978-117">For more information, see [Use Data Lake Store with Azure Databricks](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-datalake.html).</span></span>

## <a name="fix-common-problems"></a><span data-ttu-id="b2978-118">Fix common problems</span><span class="sxs-lookup"><span data-stu-id="b2978-118">Fix common problems</span></span>

<span data-ttu-id="b2978-119">Here are a few problems you might encounter with Databricks.</span><span class="sxs-lookup"><span data-stu-id="b2978-119">Here are a few problems you might encounter with Databricks.</span></span>

### <a name="issue-this-subscription-is-not-registered-to-use-the-namespace-microsoftdatabricks"></a><span data-ttu-id="b2978-120">Issue: This subscription is not registered to use the namespace ‘Microsoft.Databricks’</span><span class="sxs-lookup"><span data-stu-id="b2978-120">Issue: This subscription is not registered to use the namespace ‘Microsoft.Databricks’</span></span>

#### <a name="error-message"></a><span data-ttu-id="b2978-121">Error message</span><span class="sxs-lookup"><span data-stu-id="b2978-121">Error message</span></span>

<span data-ttu-id="b2978-122">"This subscription is not registered to use the namespace ‘Microsoft.Databricks’.</span><span class="sxs-lookup"><span data-stu-id="b2978-122">"This subscription is not registered to use the namespace ‘Microsoft.Databricks’.</span></span> <span data-ttu-id="b2978-123">See https://aka.ms/rps-not-found for how to register subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b2978-123">See https://aka.ms/rps-not-found for how to register subscriptions.</span></span> <span data-ttu-id="b2978-124">(Code: MissingSubscriptionRegistration)"</span><span class="sxs-lookup"><span data-stu-id="b2978-124">(Code: MissingSubscriptionRegistration)"</span></span>

#### <a name="solution"></a><span data-ttu-id="b2978-125">Solution</span><span class="sxs-lookup"><span data-stu-id="b2978-125">Solution</span></span>

1. <span data-ttu-id="b2978-126">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b2978-126">Go to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="b2978-127">Select **Subscriptions**, the subscription you are using, and then **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="b2978-127">Select **Subscriptions**, the subscription you are using, and then **Resource providers**.</span></span> 
1. <span data-ttu-id="b2978-128">In the list of resource providers, against **Microsoft.Databricks**, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="b2978-128">In the list of resource providers, against **Microsoft.Databricks**, select **Register**.</span></span> <span data-ttu-id="b2978-129">You must have the contributor or owner role on the subscription to register the resource provider.</span><span class="sxs-lookup"><span data-stu-id="b2978-129">You must have the contributor or owner role on the subscription to register the resource provider.</span></span>


### <a name="issue-your-account-email-does-not-have-the-owner-or-contributor-role-on-the-databricks-workspace-resource-in-the-azure-portal"></a><span data-ttu-id="b2978-130">Issue: Your account {email} does not have the owner or contributor role on the Databricks workspace resource in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b2978-130">Issue: Your account {email} does not have the owner or contributor role on the Databricks workspace resource in the Azure portal</span></span>

#### <a name="error-message"></a><span data-ttu-id="b2978-131">Error message</span><span class="sxs-lookup"><span data-stu-id="b2978-131">Error message</span></span>

<span data-ttu-id="b2978-132">"Your account {email} does not have Owner or Contributor role on the Databricks workspace resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2978-132">"Your account {email} does not have Owner or Contributor role on the Databricks workspace resource in the Azure portal.</span></span> <span data-ttu-id="b2978-133">This error can also occur if you are a guest user in the tenant.</span><span class="sxs-lookup"><span data-stu-id="b2978-133">This error can also occur if you are a guest user in the tenant.</span></span> <span data-ttu-id="b2978-134">Ask your administrator to grant you access or add you as a user directly in the Databricks workspace."</span><span class="sxs-lookup"><span data-stu-id="b2978-134">Ask your administrator to grant you access or add you as a user directly in the Databricks workspace."</span></span> 

#### <a name="solution"></a><span data-ttu-id="b2978-135">Solution</span><span class="sxs-lookup"><span data-stu-id="b2978-135">Solution</span></span>

<span data-ttu-id="b2978-136">The following are a couple of solutions to this issue:</span><span class="sxs-lookup"><span data-stu-id="b2978-136">The following are a couple of solutions to this issue:</span></span>

* <span data-ttu-id="b2978-137">To initialize the tenant, you must be signed in as a regular user of the tenant, not as a guest user.</span><span class="sxs-lookup"><span data-stu-id="b2978-137">To initialize the tenant, you must be signed in as a regular user of the tenant, not as a guest user.</span></span> <span data-ttu-id="b2978-138">You must also have a contributor role on the Databricks workspace resource.</span><span class="sxs-lookup"><span data-stu-id="b2978-138">You must also have a contributor role on the Databricks workspace resource.</span></span> <span data-ttu-id="b2978-139">You can grant a user access from the **Access control (IAM)** tab within your Databricks workspace in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2978-139">You can grant a user access from the **Access control (IAM)** tab within your Databricks workspace in the Azure portal.</span></span>

* <span data-ttu-id="b2978-140">This error might also occur if your email domain name is assigned to multiple directories in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2978-140">This error might also occur if your email domain name is assigned to multiple directories in Azure AD.</span></span> <span data-ttu-id="b2978-141">To work around this issue, create a new user in the directory that contains the subscription with your Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="b2978-141">To work around this issue, create a new user in the directory that contains the subscription with your Databricks workspace.</span></span>

    <span data-ttu-id="b2978-142">a.</span><span class="sxs-lookup"><span data-stu-id="b2978-142">a.</span></span> <span data-ttu-id="b2978-143">In the Azure portal, go to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2978-143">In the Azure portal, go to Azure AD.</span></span> <span data-ttu-id="b2978-144">Select **Users and Groups** > **Add a user**.</span><span class="sxs-lookup"><span data-stu-id="b2978-144">Select **Users and Groups** > **Add a user**.</span></span>

    <span data-ttu-id="b2978-145">b.</span><span class="sxs-lookup"><span data-stu-id="b2978-145">b.</span></span> <span data-ttu-id="b2978-146">Add a user with an `@<tenant_name>.onmicrosoft.com` email instead of `@<your_domain>` email.</span><span class="sxs-lookup"><span data-stu-id="b2978-146">Add a user with an `@<tenant_name>.onmicrosoft.com` email instead of `@<your_domain>` email.</span></span> <span data-ttu-id="b2978-147">You can find this option in **Custom Domains**, under Azure AD in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2978-147">You can find this option in **Custom Domains**, under Azure AD in the Azure portal.</span></span>
    
    <span data-ttu-id="b2978-148">c.</span><span class="sxs-lookup"><span data-stu-id="b2978-148">c.</span></span> <span data-ttu-id="b2978-149">Grant this new user the **Contributor** role on the Databricks workspace resource.</span><span class="sxs-lookup"><span data-stu-id="b2978-149">Grant this new user the **Contributor** role on the Databricks workspace resource.</span></span>
    
    <span data-ttu-id="b2978-150">d.</span><span class="sxs-lookup"><span data-stu-id="b2978-150">d.</span></span> <span data-ttu-id="b2978-151">Sign in to the Azure portal with the new user, and find the Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="b2978-151">Sign in to the Azure portal with the new user, and find the Databricks workspace.</span></span>
    
    <span data-ttu-id="b2978-152">e.</span><span class="sxs-lookup"><span data-stu-id="b2978-152">e.</span></span> <span data-ttu-id="b2978-153">Launch the Databricks workspace as this user.</span><span class="sxs-lookup"><span data-stu-id="b2978-153">Launch the Databricks workspace as this user.</span></span>


### <a name="issue-your-account-email-has-not-been-registered-in-databricks"></a><span data-ttu-id="b2978-154">Issue: Your account {email} has not been registered in Databricks</span><span class="sxs-lookup"><span data-stu-id="b2978-154">Issue: Your account {email} has not been registered in Databricks</span></span> 

#### <a name="solution"></a><span data-ttu-id="b2978-155">Solution</span><span class="sxs-lookup"><span data-stu-id="b2978-155">Solution</span></span>

<span data-ttu-id="b2978-156">If you did not create the workspace, and you are added as a user, contact the person who created the workspace.</span><span class="sxs-lookup"><span data-stu-id="b2978-156">If you did not create the workspace, and you are added as a user, contact the person who created the workspace.</span></span> <span data-ttu-id="b2978-157">Have that person add you by using the Azure Databricks Admin Console.</span><span class="sxs-lookup"><span data-stu-id="b2978-157">Have that person add you by using the Azure Databricks Admin Console.</span></span> <span data-ttu-id="b2978-158">For instructions, see [Adding and managing users](https://docs.azuredatabricks.net/administration-guide/admin-settings/users.html).</span><span class="sxs-lookup"><span data-stu-id="b2978-158">For instructions, see [Adding and managing users](https://docs.azuredatabricks.net/administration-guide/admin-settings/users.html).</span></span> <span data-ttu-id="b2978-159">If you created the workspace and still you get this error, try selecting **Initialize Workspace** again from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2978-159">If you created the workspace and still you get this error, try selecting **Initialize Workspace** again from the Azure portal.</span></span>

### <a name="issue-cloud-provider-launch-failure-while-setting-up-the-cluster-publicipcountlimitreached"></a><span data-ttu-id="b2978-160">Issue: Cloud provider launch failure while setting up the cluster (PublicIPCountLimitReached)</span><span class="sxs-lookup"><span data-stu-id="b2978-160">Issue: Cloud provider launch failure while setting up the cluster (PublicIPCountLimitReached)</span></span>

#### <a name="error-message"></a><span data-ttu-id="b2978-161">Error message</span><span class="sxs-lookup"><span data-stu-id="b2978-161">Error message</span></span>

<span data-ttu-id="b2978-162">"Cloud Provider Launch Failure: A cloud provider error was encountered while setting up the cluster.</span><span class="sxs-lookup"><span data-stu-id="b2978-162">"Cloud Provider Launch Failure: A cloud provider error was encountered while setting up the cluster.</span></span> <span data-ttu-id="b2978-163">For more information, see the Databricks guide.</span><span class="sxs-lookup"><span data-stu-id="b2978-163">For more information, see the Databricks guide.</span></span> <span data-ttu-id="b2978-164">Azure error code: PublicIPCountLimitReached.</span><span class="sxs-lookup"><span data-stu-id="b2978-164">Azure error code: PublicIPCountLimitReached.</span></span> <span data-ttu-id="b2978-165">Azure error message: Cannot create more than 60 public IP addresses for this subscription in this region."</span><span class="sxs-lookup"><span data-stu-id="b2978-165">Azure error message: Cannot create more than 60 public IP addresses for this subscription in this region."</span></span>

#### <a name="solution"></a><span data-ttu-id="b2978-166">Solution</span><span class="sxs-lookup"><span data-stu-id="b2978-166">Solution</span></span>

<span data-ttu-id="b2978-167">Databricks clusters use one public IP address per node.</span><span class="sxs-lookup"><span data-stu-id="b2978-167">Databricks clusters use one public IP address per node.</span></span> <span data-ttu-id="b2978-168">If your subscription has already used all its public IPs, you should [request to increase the quota](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request).</span><span class="sxs-lookup"><span data-stu-id="b2978-168">If your subscription has already used all its public IPs, you should [request to increase the quota](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request).</span></span> <span data-ttu-id="b2978-169">Choose **Quota** as the **Issue Type**, and **Networking: ARM** as the **Quota Type**.</span><span class="sxs-lookup"><span data-stu-id="b2978-169">Choose **Quota** as the **Issue Type**, and **Networking: ARM** as the **Quota Type**.</span></span> <span data-ttu-id="b2978-170">In **Details**, request a Public IP Address quota increase.</span><span class="sxs-lookup"><span data-stu-id="b2978-170">In **Details**, request a Public IP Address quota increase.</span></span> <span data-ttu-id="b2978-171">For example, if your limit is currently 60, and you want to create a 100-node cluster, request a limit increase to 160.</span><span class="sxs-lookup"><span data-stu-id="b2978-171">For example, if your limit is currently 60, and you want to create a 100-node cluster, request a limit increase to 160.</span></span>

### <a name="issue-a-second-type-of-cloud-provider-launch-failure-while-setting-up-the-cluster-missingsubscriptionregistration"></a><span data-ttu-id="b2978-172">Issue: A second type of cloud provider launch failure while setting up the cluster (MissingSubscriptionRegistration)</span><span class="sxs-lookup"><span data-stu-id="b2978-172">Issue: A second type of cloud provider launch failure while setting up the cluster (MissingSubscriptionRegistration)</span></span>

#### <a name="error-message"></a><span data-ttu-id="b2978-173">Error message</span><span class="sxs-lookup"><span data-stu-id="b2978-173">Error message</span></span>

<span data-ttu-id="b2978-174">"Cloud Provider Launch Failure: A cloud provider error was encountered while setting up the cluster.</span><span class="sxs-lookup"><span data-stu-id="b2978-174">"Cloud Provider Launch Failure: A cloud provider error was encountered while setting up the cluster.</span></span> <span data-ttu-id="b2978-175">For more information, see the Databricks guide.</span><span class="sxs-lookup"><span data-stu-id="b2978-175">For more information, see the Databricks guide.</span></span>
<span data-ttu-id="b2978-176">Azure error code: MissingSubscriptionRegistration Azure error message: The subscription is not registered to use namespace 'Microsoft.Compute'.</span><span class="sxs-lookup"><span data-stu-id="b2978-176">Azure error code: MissingSubscriptionRegistration Azure error message: The subscription is not registered to use namespace 'Microsoft.Compute'.</span></span> <span data-ttu-id="b2978-177">See https://aka.ms/rps-not-found for how to register subscriptions."</span><span class="sxs-lookup"><span data-stu-id="b2978-177">See https://aka.ms/rps-not-found for how to register subscriptions."</span></span>

#### <a name="solution"></a><span data-ttu-id="b2978-178">Solution</span><span class="sxs-lookup"><span data-stu-id="b2978-178">Solution</span></span>

1. <span data-ttu-id="b2978-179">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b2978-179">Go to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="b2978-180">Select **Subscriptions**, the subscription you are using, and then **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="b2978-180">Select **Subscriptions**, the subscription you are using, and then **Resource providers**.</span></span> 
1. <span data-ttu-id="b2978-181">In the list of resource providers, against **Microsoft.Compute**, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="b2978-181">In the list of resource providers, against **Microsoft.Compute**, select **Register**.</span></span> <span data-ttu-id="b2978-182">You must have the contributor or owner role on the subscription to register the resource provider.</span><span class="sxs-lookup"><span data-stu-id="b2978-182">You must have the contributor or owner role on the subscription to register the resource provider.</span></span>

<span data-ttu-id="b2978-183">For more detailed instructions, see [Resource providers and types](../azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="b2978-183">For more detailed instructions, see [Resource providers and types](../azure-resource-manager/resource-manager-supported-services.md).</span></span>

### <a name="issue-azure-databricks-needs-permissions-to-access-resources-in-your-organization-that-only-an-admin-can-grant"></a><span data-ttu-id="b2978-184">Issue: Azure Databricks needs permissions to access resources in your organization that only an admin can grant.</span><span class="sxs-lookup"><span data-stu-id="b2978-184">Issue: Azure Databricks needs permissions to access resources in your organization that only an admin can grant.</span></span>

#### <a name="background"></a><span data-ttu-id="b2978-185">Background</span><span class="sxs-lookup"><span data-stu-id="b2978-185">Background</span></span>

<span data-ttu-id="b2978-186">Azure Databricks is integrated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2978-186">Azure Databricks is integrated with Azure AD.</span></span> <span data-ttu-id="b2978-187">This enables you to set permissions within Azure Databricks (for example, on notebooks or clusters) by specifying users from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2978-187">This enables you to set permissions within Azure Databricks (for example, on notebooks or clusters) by specifying users from Azure AD.</span></span> <span data-ttu-id="b2978-188">For Azure Databricks to be able to list the names of the users from your Azure AD, it requires read permission to that information.</span><span class="sxs-lookup"><span data-stu-id="b2978-188">For Azure Databricks to be able to list the names of the users from your Azure AD, it requires read permission to that information.</span></span> <span data-ttu-id="b2978-189">This requires a consent.</span><span class="sxs-lookup"><span data-stu-id="b2978-189">This requires a consent.</span></span> <span data-ttu-id="b2978-190">If the consent is not already available, you see the error.</span><span class="sxs-lookup"><span data-stu-id="b2978-190">If the consent is not already available, you see the error.</span></span>

#### <a name="solution"></a><span data-ttu-id="b2978-191">Solution</span><span class="sxs-lookup"><span data-stu-id="b2978-191">Solution</span></span>

<span data-ttu-id="b2978-192">Log in as a global administrator to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2978-192">Log in as a global administrator to the Azure portal.</span></span> <span data-ttu-id="b2978-193">For Azure Active Directory, go to the **User Settings** tab and make sure **Users can consent to apps accessing company data on their behalf** is set to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="b2978-193">For Azure Active Directory, go to the **User Settings** tab and make sure **Users can consent to apps accessing company data on their behalf** is set to **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2978-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2978-194">Next steps</span></span>

- [<span data-ttu-id="b2978-195">Quickstart: Get started with Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="b2978-195">Quickstart: Get started with Azure Databricks</span></span>](quickstart-create-databricks-workspace-portal.md)
- [<span data-ttu-id="b2978-196">What is Azure Databricks?</span><span class="sxs-lookup"><span data-stu-id="b2978-196">What is Azure Databricks?</span></span>](what-is-azure-databricks.md)

