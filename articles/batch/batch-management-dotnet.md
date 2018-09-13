---
title: Manage Batch account resources with the client library for .NET - Azure | Microsoft Docs
description: Create, delete, and modify Azure Batch account resources with the Batch Management .NET library.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 03/15/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f635bbd8652b97c1067473e56565bf7c6520a2ba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553003"
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="980d0-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span><span class="sxs-lookup"><span data-stu-id="980d0-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](batch-account-create-portal.md)
> * [Batch Management .NET](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="980d0-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span><span class="sxs-lookup"><span data-stu-id="980d0-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="980d0-107">**Create and delete Batch accounts** within any region.</span><span class="sxs-lookup"><span data-stu-id="980d0-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="980d0-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span><span class="sxs-lookup"><span data-stu-id="980d0-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="980d0-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span><span class="sxs-lookup"><span data-stu-id="980d0-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="980d0-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span><span class="sxs-lookup"><span data-stu-id="980d0-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="980d0-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span><span class="sxs-lookup"><span data-stu-id="980d0-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="980d0-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span><span class="sxs-lookup"><span data-stu-id="980d0-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="980d0-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span><span class="sxs-lookup"><span data-stu-id="980d0-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="980d0-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span><span class="sxs-lookup"><span data-stu-id="980d0-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="980d0-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span><span class="sxs-lookup"><span data-stu-id="980d0-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="980d0-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span><span class="sxs-lookup"><span data-stu-id="980d0-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal]. For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="980d0-119">Create and delete Batch accounts</span><span class="sxs-lookup"><span data-stu-id="980d0-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="980d0-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span><span class="sxs-lookup"><span data-stu-id="980d0-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="980d0-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span><span class="sxs-lookup"><span data-stu-id="980d0-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="980d0-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span><span class="sxs-lookup"><span data-stu-id="980d0-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="980d0-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="980d0-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed. For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="980d0-126">Retrieve and regenerate account keys</span><span class="sxs-lookup"><span data-stu-id="980d0-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="980d0-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="980d0-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="980d0-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="980d0-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> You can create a streamlined connection workflow for your management applications. First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys]. Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="980d0-132">Check Azure subscription and Batch account quotas</span><span class="sxs-lookup"><span data-stu-id="980d0-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="980d0-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span><span class="sxs-lookup"><span data-stu-id="980d0-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="980d0-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="980d0-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="980d0-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="980d0-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="980d0-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span><span class="sxs-lookup"><span data-stu-id="980d0-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="980d0-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span><span class="sxs-lookup"><span data-stu-id="980d0-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="980d0-138">Check an Azure subscription for Batch account quotas</span><span class="sxs-lookup"><span data-stu-id="980d0-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="980d0-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span><span class="sxs-lookup"><span data-stu-id="980d0-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="980d0-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span><span class="sxs-lookup"><span data-stu-id="980d0-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="980d0-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span><span class="sxs-lookup"><span data-stu-id="980d0-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="980d0-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span><span class="sxs-lookup"><span data-stu-id="980d0-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="980d0-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="980d0-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="980d0-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span><span class="sxs-lookup"><span data-stu-id="980d0-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="980d0-145">Check a Batch account for compute resource quotas</span><span class="sxs-lookup"><span data-stu-id="980d0-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="980d0-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span><span class="sxs-lookup"><span data-stu-id="980d0-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="980d0-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="980d0-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="980d0-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span><span class="sxs-lookup"><span data-stu-id="980d0-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal]. For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="980d0-151">Use Azure AD with Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="980d0-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="980d0-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span><span class="sxs-lookup"><span data-stu-id="980d0-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="980d0-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="980d0-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="980d0-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="980d0-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="980d0-155">Sample project on GitHub</span><span class="sxs-lookup"><span data-stu-id="980d0-155">Sample project on GitHub</span></span>

<span data-ttu-id="980d0-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span><span class="sxs-lookup"><span data-stu-id="980d0-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="980d0-157">The AccountManagment sample application demonstrates the following operations:</span><span class="sxs-lookup"><span data-stu-id="980d0-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="980d0-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="980d0-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="980d0-159">If the user is not already signed in, they are prompted for their Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="980d0-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="980d0-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span><span class="sxs-lookup"><span data-stu-id="980d0-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="980d0-161">The user can select a subscription from the list if it contains more than one subscription.</span><span class="sxs-lookup"><span data-stu-id="980d0-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="980d0-162">Get credentials associated with the selected subscription.</span><span class="sxs-lookup"><span data-stu-id="980d0-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="980d0-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span><span class="sxs-lookup"><span data-stu-id="980d0-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="980d0-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="980d0-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="980d0-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span><span class="sxs-lookup"><span data-stu-id="980d0-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="980d0-166">Create a Batch account in the new resource group.</span><span class="sxs-lookup"><span data-stu-id="980d0-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="980d0-167">Get the newly created account from the Batch service.</span><span class="sxs-lookup"><span data-stu-id="980d0-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="980d0-168">Print the account keys for the new account.</span><span class="sxs-lookup"><span data-stu-id="980d0-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="980d0-169">Regenerate a new primary key for the account.</span><span class="sxs-lookup"><span data-stu-id="980d0-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="980d0-170">Print the quota information for the account.</span><span class="sxs-lookup"><span data-stu-id="980d0-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="980d0-171">Print the quota information for the subscription.</span><span class="sxs-lookup"><span data-stu-id="980d0-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="980d0-172">Print all accounts within the subscription.</span><span class="sxs-lookup"><span data-stu-id="980d0-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="980d0-173">Delete newly created account.</span><span class="sxs-lookup"><span data-stu-id="980d0-173">Delete newly created account.</span></span>
7. <span data-ttu-id="980d0-174">Delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="980d0-174">Delete the resource group.</span></span>

<span data-ttu-id="980d0-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="980d0-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="980d0-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="980d0-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="980d0-177">Follow the steps provided in [Authenticate Batch management applications with Azure AD](batch-aad-auth.md#use-azure-ad-with-batch-service-solutions).</span><span class="sxs-lookup"><span data-stu-id="980d0-177">Follow the steps provided in [Authenticate Batch management applications with Azure AD](batch-aad-auth.md#use-azure-ad-with-batch-service-solutions).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
