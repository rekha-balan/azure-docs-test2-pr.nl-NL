---
title: Activate Azure subscriptions and accounts | Microsoft Docs
description: Enable access using Azure Resource Manager APIs for new and existing accounts and resolve common account problems.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 08/29/2018
ms.topic: quickstart
ms.service: cost-management
manager: dougeby
ms.custom: ''
ms.openlocfilehash: 120b678431c5e857e2da42e980d95dea85b93435
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871698"
---
# <a name="activate-azure-subscriptions-and-accounts-with-azure-cost-management"></a><span data-ttu-id="feef2-103">Activate Azure subscriptions and accounts with Azure Cost Management</span><span class="sxs-lookup"><span data-stu-id="feef2-103">Activate Azure subscriptions and accounts with Azure Cost Management</span></span>

<span data-ttu-id="feef2-104">Adding or updating your Azure Resource Manager credentials allows Azure Cost Management to discover all the accounts and subscriptions within your Azure Tenant.</span><span class="sxs-lookup"><span data-stu-id="feef2-104">Adding or updating your Azure Resource Manager credentials allows Azure Cost Management to discover all the accounts and subscriptions within your Azure Tenant.</span></span> <span data-ttu-id="feef2-105">If you also have Azure Diagnostics extension enabled on your virtual machines, then Azure Cost Management can collect extended metrics like CPU and memory.</span><span class="sxs-lookup"><span data-stu-id="feef2-105">If you also have Azure Diagnostics extension enabled on your virtual machines, then Azure Cost Management can collect extended metrics like CPU and memory.</span></span> <span data-ttu-id="feef2-106">This article describes how to enable access using Azure Resource Manager APIs for new and existing accounts.</span><span class="sxs-lookup"><span data-stu-id="feef2-106">This article describes how to enable access using Azure Resource Manager APIs for new and existing accounts.</span></span> <span data-ttu-id="feef2-107">It also describes how to resolve common account problems.</span><span class="sxs-lookup"><span data-stu-id="feef2-107">It also describes how to resolve common account problems.</span></span>

<span data-ttu-id="feef2-108">Azure Cost Management cannot access most of your Azure subscription data when the subscription is _unactivated_.</span><span class="sxs-lookup"><span data-stu-id="feef2-108">Azure Cost Management cannot access most of your Azure subscription data when the subscription is _unactivated_.</span></span> <span data-ttu-id="feef2-109">You must edit _unactivated_ accounts so that Azure Cost Management can access them.</span><span class="sxs-lookup"><span data-stu-id="feef2-109">You must edit _unactivated_ accounts so that Azure Cost Management can access them.</span></span>

## <a name="required-azure-permissions"></a><span data-ttu-id="feef2-110">Required Azure permissions</span><span class="sxs-lookup"><span data-stu-id="feef2-110">Required Azure permissions</span></span>

<span data-ttu-id="feef2-111">Specific permissions are needed to complete the procedures in this article.</span><span class="sxs-lookup"><span data-stu-id="feef2-111">Specific permissions are needed to complete the procedures in this article.</span></span> <span data-ttu-id="feef2-112">Either you or your tenant administrator must have both of the following permissions:</span><span class="sxs-lookup"><span data-stu-id="feef2-112">Either you or your tenant administrator must have both of the following permissions:</span></span>

- <span data-ttu-id="feef2-113">Permission to register the CloudynCollector application with your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="feef2-113">Permission to register the CloudynCollector application with your Azure AD tenant.</span></span>
- <span data-ttu-id="feef2-114">The ability to assign the application to a role in your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="feef2-114">The ability to assign the application to a role in your Azure subscriptions.</span></span>

<span data-ttu-id="feef2-115">In your Azure subscriptions, your accounts must have `Microsoft.Authorization/*/Write` access to assign the CloudynCollector application.</span><span class="sxs-lookup"><span data-stu-id="feef2-115">In your Azure subscriptions, your accounts must have `Microsoft.Authorization/*/Write` access to assign the CloudynCollector application.</span></span> <span data-ttu-id="feef2-116">This action is granted through the [Owner](../role-based-access-control/built-in-roles.md#owner) role or [User Access Administrator](../role-based-access-control/built-in-roles.md#user-access-administrator) role.</span><span class="sxs-lookup"><span data-stu-id="feef2-116">This action is granted through the [Owner](../role-based-access-control/built-in-roles.md#owner) role or [User Access Administrator](../role-based-access-control/built-in-roles.md#user-access-administrator) role.</span></span>

<span data-ttu-id="feef2-117">If your account is assigned the **Contributor** role, you do not have adequate permission to assign the application.</span><span class="sxs-lookup"><span data-stu-id="feef2-117">If your account is assigned the **Contributor** role, you do not have adequate permission to assign the application.</span></span> <span data-ttu-id="feef2-118">You receive an error when attempting to assign the CloudynCollector application to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="feef2-118">You receive an error when attempting to assign the CloudynCollector application to your Azure subscription.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="feef2-119">Check Azure Active Directory permissions</span><span class="sxs-lookup"><span data-stu-id="feef2-119">Check Azure Active Directory permissions</span></span>

1. <span data-ttu-id="feef2-120">Sign in into the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="feef2-120">Sign in into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="feef2-121">In the Azure portal, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="feef2-121">In the Azure portal, select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="feef2-122">In Azure Active Directory, select **User settings**.</span><span class="sxs-lookup"><span data-stu-id="feef2-122">In Azure Active Directory, select **User settings**.</span></span>
4. <span data-ttu-id="feef2-123">Check the **App registrations** option.</span><span class="sxs-lookup"><span data-stu-id="feef2-123">Check the **App registrations** option.</span></span>
    - <span data-ttu-id="feef2-124">If it is set to **Yes**, then non-administrator users can register AD apps.</span><span class="sxs-lookup"><span data-stu-id="feef2-124">If it is set to **Yes**, then non-administrator users can register AD apps.</span></span> <span data-ttu-id="feef2-125">This setting means any user in the Azure AD tenant can register an app.</span><span class="sxs-lookup"><span data-stu-id="feef2-125">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="feef2-126">You can proceed to Required Azure subscription permissions.</span><span class="sxs-lookup"><span data-stu-id="feef2-126">You can proceed to Required Azure subscription permissions.</span></span>  
    <span data-ttu-id="feef2-127">![App registrations](./media/activate-subs-accounts/app-register.png)</span><span class="sxs-lookup"><span data-stu-id="feef2-127">![App registrations](./media/activate-subs-accounts/app-register.png)</span></span>
    - <span data-ttu-id="feef2-128">If the **App registrations** option is set to **No**, then only tenant administrative users can register Azure Active Directory apps.</span><span class="sxs-lookup"><span data-stu-id="feef2-128">If the **App registrations** option is set to **No**, then only tenant administrative users can register Azure Active Directory apps.</span></span> <span data-ttu-id="feef2-129">Your tenant administrator must register the CloudynCollector application.</span><span class="sxs-lookup"><span data-stu-id="feef2-129">Your tenant administrator must register the CloudynCollector application.</span></span>


## <a name="add-an-account-or-update-a-subscription"></a><span data-ttu-id="feef2-130">Add an account or update a subscription</span><span class="sxs-lookup"><span data-stu-id="feef2-130">Add an account or update a subscription</span></span>

<span data-ttu-id="feef2-131">When you add an account update a subscription, you grant Azure Cost Management access to your Azure data.</span><span class="sxs-lookup"><span data-stu-id="feef2-131">When you add an account update a subscription, you grant Azure Cost Management access to your Azure data.</span></span>

### <a name="add-a-new-account-subscription"></a><span data-ttu-id="feef2-132">Add a new account (subscription)</span><span class="sxs-lookup"><span data-stu-id="feef2-132">Add a new account (subscription)</span></span>

1. <span data-ttu-id="feef2-133">In the Azure Cost Management portal, click the gear symbol in the upper-right and select **Cloud Accounts**.</span><span class="sxs-lookup"><span data-stu-id="feef2-133">In the Azure Cost Management portal, click the gear symbol in the upper-right and select **Cloud Accounts**.</span></span>
2. <span data-ttu-id="feef2-134">Click **Add new account** and the **Add new account** box appears.</span><span class="sxs-lookup"><span data-stu-id="feef2-134">Click **Add new account** and the **Add new account** box appears.</span></span> <span data-ttu-id="feef2-135">Enter the required information.</span><span class="sxs-lookup"><span data-stu-id="feef2-135">Enter the required information.</span></span>  
    <span data-ttu-id="feef2-136">![Add new account box](./media/activate-subs-accounts//add-new-account.png)</span><span class="sxs-lookup"><span data-stu-id="feef2-136">![Add new account box](./media/activate-subs-accounts//add-new-account.png)</span></span>

### <a name="update-a-subscription"></a><span data-ttu-id="feef2-137">Update a subscription</span><span class="sxs-lookup"><span data-stu-id="feef2-137">Update a subscription</span></span>

1. <span data-ttu-id="feef2-138">If you want to update an _unactivated_ subscription that already exists in Azure Cost Management in Accounts Management, click the edit pencil symbol to the right of the parent _tenant GUID_.</span><span class="sxs-lookup"><span data-stu-id="feef2-138">If you want to update an _unactivated_ subscription that already exists in Azure Cost Management in Accounts Management, click the edit pencil symbol to the right of the parent _tenant GUID_.</span></span> <span data-ttu-id="feef2-139">Subscriptions are grouped under a parent tenant, so avoid activating subscriptions individually.</span><span class="sxs-lookup"><span data-stu-id="feef2-139">Subscriptions are grouped under a parent tenant, so avoid activating subscriptions individually.</span></span>
    <span data-ttu-id="feef2-140">![Rediscover subscriptions](./media/activate-subs-accounts/existing-sub.png)</span><span class="sxs-lookup"><span data-stu-id="feef2-140">![Rediscover subscriptions](./media/activate-subs-accounts/existing-sub.png)</span></span>
2. <span data-ttu-id="feef2-141">If necessary, enter the Tenant ID.</span><span class="sxs-lookup"><span data-stu-id="feef2-141">If necessary, enter the Tenant ID.</span></span> <span data-ttu-id="feef2-142">If you don't know your Tenant ID, use the following steps to find it:</span><span class="sxs-lookup"><span data-stu-id="feef2-142">If you don't know your Tenant ID, use the following steps to find it:</span></span>
    1. <span data-ttu-id="feef2-143">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="feef2-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="feef2-144">In the Azure portal, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="feef2-144">In the Azure portal, select **Azure Active Directory**.</span></span>
    3. <span data-ttu-id="feef2-145">To get the tenant ID, select **Properties** for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="feef2-145">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span>
    4. <span data-ttu-id="feef2-146">Copy the Directory ID GUID.</span><span class="sxs-lookup"><span data-stu-id="feef2-146">Copy the Directory ID GUID.</span></span> <span data-ttu-id="feef2-147">This value is your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="feef2-147">This value is your tenant ID.</span></span>
    <span data-ttu-id="feef2-148">For more information, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="feef2-148">For more information, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
3. <span data-ttu-id="feef2-149">If necessary, select your Rate ID.</span><span class="sxs-lookup"><span data-stu-id="feef2-149">If necessary, select your Rate ID.</span></span> <span data-ttu-id="feef2-150">If you don't know your rate ID, use the following steps to find it.</span><span class="sxs-lookup"><span data-stu-id="feef2-150">If you don't know your rate ID, use the following steps to find it.</span></span>
    1. <span data-ttu-id="feef2-151">In the upper-right of the Azure portal, click your user information and then click **View my bill**.</span><span class="sxs-lookup"><span data-stu-id="feef2-151">In the upper-right of the Azure portal, click your user information and then click **View my bill**.</span></span>
    2. <span data-ttu-id="feef2-152">Under **Billing Account**, click **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="feef2-152">Under **Billing Account**, click **Subscriptions**.</span></span>
    3. <span data-ttu-id="feef2-153">Under **My subscriptions**, select the subscription.</span><span class="sxs-lookup"><span data-stu-id="feef2-153">Under **My subscriptions**, select the subscription.</span></span>
    4. <span data-ttu-id="feef2-154">Your rate ID is shown under **Offer ID**.</span><span class="sxs-lookup"><span data-stu-id="feef2-154">Your rate ID is shown under **Offer ID**.</span></span> <span data-ttu-id="feef2-155">Copy the Offer ID for the subscription.</span><span class="sxs-lookup"><span data-stu-id="feef2-155">Copy the Offer ID for the subscription.</span></span>
4. <span data-ttu-id="feef2-156">In the Add new account (or Edit Subscription) box, click **Save** (or **Next**).</span><span class="sxs-lookup"><span data-stu-id="feef2-156">In the Add new account (or Edit Subscription) box, click **Save** (or **Next**).</span></span> <span data-ttu-id="feef2-157">You're redirected to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="feef2-157">You're redirected to the Azure portal.</span></span>
5. <span data-ttu-id="feef2-158">Sign in to the portal.</span><span class="sxs-lookup"><span data-stu-id="feef2-158">Sign in to the portal.</span></span> <span data-ttu-id="feef2-159">Click **Accept** to authorize Azure Cost Management Collector access your Azure account.</span><span class="sxs-lookup"><span data-stu-id="feef2-159">Click **Accept** to authorize Azure Cost Management Collector access your Azure account.</span></span>

    <span data-ttu-id="feef2-160">You're redirected to the Azure Cost Management Accounts management page and your subscription is updated with **active** Account Status.</span><span class="sxs-lookup"><span data-stu-id="feef2-160">You're redirected to the Azure Cost Management Accounts management page and your subscription is updated with **active** Account Status.</span></span> <span data-ttu-id="feef2-161">It should display a green check mark symbol under the Resource Manager column.</span><span class="sxs-lookup"><span data-stu-id="feef2-161">It should display a green check mark symbol under the Resource Manager column.</span></span>

    <span data-ttu-id="feef2-162">If you don't see a green checkmark symbol for one or more of the subscriptions, it means that you do not have permissions to create the reader app (the CloudynCollector) for the subscription.</span><span class="sxs-lookup"><span data-stu-id="feef2-162">If you don't see a green checkmark symbol for one or more of the subscriptions, it means that you do not have permissions to create the reader app (the CloudynCollector) for the subscription.</span></span> <span data-ttu-id="feef2-163">A user with higher permissions for the subscription needs to repeat this process.</span><span class="sxs-lookup"><span data-stu-id="feef2-163">A user with higher permissions for the subscription needs to repeat this process.</span></span>

<span data-ttu-id="feef2-164">Watch the [Connecting to Azure Resource Manager with Azure Cost Management](https://youtu.be/oCIwvfBB6kk) video that walks through the process.</span><span class="sxs-lookup"><span data-stu-id="feef2-164">Watch the [Connecting to Azure Resource Manager with Azure Cost Management](https://youtu.be/oCIwvfBB6kk) video that walks through the process.</span></span>

>[!VIDEO https://www.youtube.com/embed/oCIwvfBB6kk?ecver=1]

## <a name="resolve-common-indirect-enterprise-set-up-problems"></a><span data-ttu-id="feef2-165">Resolve common indirect enterprise set-up problems</span><span class="sxs-lookup"><span data-stu-id="feef2-165">Resolve common indirect enterprise set-up problems</span></span>

<span data-ttu-id="feef2-166">When you first use the Azure Cost Management portal, you might see the following messages if you are an Enterprise Agreement or Cloud Solution Provider (CSP) user:</span><span class="sxs-lookup"><span data-stu-id="feef2-166">When you first use the Azure Cost Management portal, you might see the following messages if you are an Enterprise Agreement or Cloud Solution Provider (CSP) user:</span></span>

- <span data-ttu-id="feef2-167">*The specified API key is not a top level enrollment key* displayed in the  **Set Up Azure Cost Management**  wizard.</span><span class="sxs-lookup"><span data-stu-id="feef2-167">*The specified API key is not a top level enrollment key* displayed in the  **Set Up Azure Cost Management**  wizard.</span></span>
- <span data-ttu-id="feef2-168">*Direct Enrollment – No* displayed in the Enterprise Agreement portal.</span><span class="sxs-lookup"><span data-stu-id="feef2-168">*Direct Enrollment – No* displayed in the Enterprise Agreement portal.</span></span>
- <span data-ttu-id="feef2-169">*No usage data was found for the last 30 days. Please contact your distributor to make sure markup was enabled for your Azure account* displayed in the Azure Cost Management portal.</span><span class="sxs-lookup"><span data-stu-id="feef2-169">*No usage data was found for the last 30 days. Please contact your distributor to make sure markup was enabled for your Azure account* displayed in the Azure Cost Management portal.</span></span>

<span data-ttu-id="feef2-170">The preceding messages indicate that you purchased an Azure Enterprise Agreement through a reseller or CSP.</span><span class="sxs-lookup"><span data-stu-id="feef2-170">The preceding messages indicate that you purchased an Azure Enterprise Agreement through a reseller or CSP.</span></span> <span data-ttu-id="feef2-171">Your reseller or CSP needs to enable _markup_ for your Azure account so that you can view your data in Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="feef2-171">Your reseller or CSP needs to enable _markup_ for your Azure account so that you can view your data in Azure Cost Management.</span></span>

<span data-ttu-id="feef2-172">Here's how to fix the problems:</span><span class="sxs-lookup"><span data-stu-id="feef2-172">Here's how to fix the problems:</span></span>

1. <span data-ttu-id="feef2-173">Your reseller needs to enable _markup_ for your account.</span><span class="sxs-lookup"><span data-stu-id="feef2-173">Your reseller needs to enable _markup_ for your account.</span></span> <span data-ttu-id="feef2-174">For instructions, see the [Indirect Customer Onboarding Guide](https://ea.azure.com/api/v3Help/v2IndirectCustomerOnboardingGuide).</span><span class="sxs-lookup"><span data-stu-id="feef2-174">For instructions, see the [Indirect Customer Onboarding Guide](https://ea.azure.com/api/v3Help/v2IndirectCustomerOnboardingGuide).</span></span>
2. <span data-ttu-id="feef2-175">You generate the Azure Enterprise Agreement key for use with Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="feef2-175">You generate the Azure Enterprise Agreement key for use with Azure Cost Management.</span></span> <span data-ttu-id="feef2-176">For instructions, see [Register an Azure Enterprise Agreement and view cost data](https://docs.microsoft.com/azure/cost-management/quick-register-ea).</span><span class="sxs-lookup"><span data-stu-id="feef2-176">For instructions, see [Register an Azure Enterprise Agreement and view cost data](https://docs.microsoft.com/azure/cost-management/quick-register-ea).</span></span>

<span data-ttu-id="feef2-177">Before you can generate the Azure Enterprise Agreement API key to set up Azure Cost Management, you must enable the Azure Billing API by following the instructions at:</span><span class="sxs-lookup"><span data-stu-id="feef2-177">Before you can generate the Azure Enterprise Agreement API key to set up Azure Cost Management, you must enable the Azure Billing API by following the instructions at:</span></span>

- [<span data-ttu-id="feef2-178">Overview of Reporting APIs for Enterprise customers</span><span class="sxs-lookup"><span data-stu-id="feef2-178">Overview of Reporting APIs for Enterprise customers</span></span>](../billing/billing-enterprise-api.md)
- <span data-ttu-id="feef2-179">[Microsoft Azure enterprise portal Reporting API](https://ea.azure.com/helpdocs/reportingAPI) under **Enabling data access to the API**</span><span class="sxs-lookup"><span data-stu-id="feef2-179">[Microsoft Azure enterprise portal Reporting API](https://ea.azure.com/helpdocs/reportingAPI) under **Enabling data access to the API**</span></span>

<span data-ttu-id="feef2-180">You also might need to give department administrators, account owners, and enterprise administrators permissions to _view charges_ with the Billing API.</span><span class="sxs-lookup"><span data-stu-id="feef2-180">You also might need to give department administrators, account owners, and enterprise administrators permissions to _view charges_ with the Billing API.</span></span>

<span data-ttu-id="feef2-181">Only an Azure service administrator can enable Cost Management.</span><span class="sxs-lookup"><span data-stu-id="feef2-181">Only an Azure service administrator can enable Cost Management.</span></span> <span data-ttu-id="feef2-182">Co-administrator permissions are insufficient.</span><span class="sxs-lookup"><span data-stu-id="feef2-182">Co-administrator permissions are insufficient.</span></span> <span data-ttu-id="feef2-183">However, you can work around the administrator requirement.</span><span class="sxs-lookup"><span data-stu-id="feef2-183">However, you can work around the administrator requirement.</span></span> <span data-ttu-id="feef2-184">You can request that your Azure Active Directory administrator grant permission to authorize the **CloudynAzureCollector** with a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="feef2-184">You can request that your Azure Active Directory administrator grant permission to authorize the **CloudynAzureCollector** with a PowerShell script.</span></span> <span data-ttu-id="feef2-185">The following script grants permission to register the Azure Active Directory Service Principal **CloudynAzureCollector**.</span><span class="sxs-lookup"><span data-stu-id="feef2-185">The following script grants permission to register the Azure Active Directory Service Principal **CloudynAzureCollector**.</span></span> <span data-ttu-id="feef2-186">When successfully run, the operation ends with the browser showing the URL http://localhost:8080/CloudynJava.</span><span class="sxs-lookup"><span data-stu-id="feef2-186">When successfully run, the operation ends with the browser showing the URL http://localhost:8080/CloudynJava.</span></span>

```
#THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

#Tenant - enter your tenant ID or Name
$tenant = "<ReplaceWithYourTenantID>"

#Cloudyn Collector application ID
$appId = "83e638ef-7885-479f-bbe8-9150acccdb3d"

#URL to activate the consent screen
$url = "https://login.windows.net/"+$tenant+"/oauth2/authorize?api-version=1&response_type=code&client_id="+$appId+"&redirect_uri=http%3A%2F%2Flocalhost%3A8080%2FCloudynJava&prompt=consent"

#Choose your browser, the default is Internet Explorer

#Chrome
#[System.Diagnostics.Process]::Start("chrome.exe", "--incognito $url")

#Firefox
#[System.Diagnostics.Process]::Start("firefox.exe","-private-window $url" )

#IExplorer
[System.Diagnostics.Process]::Start("iexplore.exe","$url -private" )

```

## <a name="next-steps"></a><span data-ttu-id="feef2-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="feef2-187">Next steps</span></span>

- <span data-ttu-id="feef2-188">If you haven't already completed the first tutorial for Cost Management, read it at [Review usage and costs](tutorial-review-usage.md).</span><span class="sxs-lookup"><span data-stu-id="feef2-188">If you haven't already completed the first tutorial for Cost Management, read it at [Review usage and costs](tutorial-review-usage.md).</span></span>
