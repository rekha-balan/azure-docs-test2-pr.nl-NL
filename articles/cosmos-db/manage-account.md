---
title: Manage an Azure Cosmos DB account via the Azure Portal | Microsoft Docs
description: Learn how to manage your Azure Cosmos DB account via the Azure Portal. Find a guide on using the Azure Portal to view, copy, delete and access accounts.
keywords: Azure Portal, azure, Microsoft azure
services: cosmos-db
author: kirillg
manager: kfile
editor: cgronlun
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 11/28/2017
ms.author: kirillg
ms.openlocfilehash: 8b28143dc92fa526b631baf6d47e4a9f2367ee0e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869283"
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="64773-105">How to manage an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="64773-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="64773-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="64773-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <a id="consistency"></a><span data-ttu-id="64773-107">Manage Azure Cosmos DB consistency settings</span><span class="sxs-lookup"><span data-stu-id="64773-107">Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="64773-108">Selecting the right consistency level depends on the semantics of your application.</span><span class="sxs-lookup"><span data-stu-id="64773-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="64773-109">Familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span><span class="sxs-lookup"><span data-stu-id="64773-109">Familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="64773-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span><span class="sxs-lookup"><span data-stu-id="64773-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="64773-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span><span class="sxs-lookup"><span data-stu-id="64773-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="64773-112">On the other hand, the relaxed consistency levels - bounded staleness, session, or eventual enable you to associate any number of Azure regions with your database account.</span><span class="sxs-lookup"><span data-stu-id="64773-112">On the other hand, the relaxed consistency levels - bounded staleness, session, or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="64773-113">The following simple steps show you how to select the default consistency level for your database account.</span><span class="sxs-lookup"><span data-stu-id="64773-113">The following simple steps show you how to select the default consistency level for your database account.</span></span>

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="64773-114">To specify the default consistency for an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="64773-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="64773-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="64773-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="64773-116">In the account page, click **Default consistency**.</span><span class="sxs-lookup"><span data-stu-id="64773-116">In the account page, click **Default consistency**.</span></span>
3. <span data-ttu-id="64773-117">In the **Default Consistency** page, select the new consistency level and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="64773-117">In the **Default Consistency** page, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="64773-118">![Default consistency session][5]</span><span class="sxs-lookup"><span data-stu-id="64773-118">![Default consistency session][5]</span></span>

## <a id="keys"></a><span data-ttu-id="64773-119">View, copy, and regenerate access keys and passwords</span><span class="sxs-lookup"><span data-stu-id="64773-119">View, copy, and regenerate access keys and passwords</span></span>
<span data-ttu-id="64773-120">When you create an Azure Cosmos DB account, the service generates two master access keys (or two passwords for MongoDB API accounts) that can be used for authentication when the Azure Cosmos DB account is accessed.</span><span class="sxs-lookup"><span data-stu-id="64773-120">When you create an Azure Cosmos DB account, the service generates two master access keys (or two passwords for MongoDB API accounts) that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="64773-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="64773-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="64773-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** page from the resource menu on the **Azure Cosmos DB account** page to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="64773-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** page from the resource menu on the **Azure Cosmos DB account** page to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span> <span data-ttu-id="64773-123">For MongoDB API accounts, access the **Connection String** page from the resource menu to view, copy, and regenerate the passwords that are used to access your account.</span><span class="sxs-lookup"><span data-stu-id="64773-123">For MongoDB API accounts, access the **Connection String** page from the resource menu to view, copy, and regenerate the passwords that are used to access your account.</span></span>

![Azure portal screenshot, Keys page](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="64773-125">The **Keys** page also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="64773-125">The **Keys** page also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="64773-126">Read-only keys are also available on this page.</span><span class="sxs-lookup"><span data-stu-id="64773-126">Read-only keys are also available on this page.</span></span> <span data-ttu-id="64773-127">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span><span class="sxs-lookup"><span data-stu-id="64773-127">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-or-password-in-the-azure-portal"></a><span data-ttu-id="64773-128">Copy an access key or password in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="64773-128">Copy an access key or password in the Azure portal</span></span>
<span data-ttu-id="64773-129">On the **Keys** page (or **Connection string** page for MongoDB API accounts), click the **Copy** button to the right of the key or password you wish to copy.</span><span class="sxs-lookup"><span data-stu-id="64773-129">On the **Keys** page (or **Connection string** page for MongoDB API accounts), click the **Copy** button to the right of the key or password you wish to copy.</span></span>

![View and copy an access key in the Azure portal, Keys page](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys-and-passwords"></a><span data-ttu-id="64773-131">Regenerate access keys and passwords</span><span class="sxs-lookup"><span data-stu-id="64773-131">Regenerate access keys and passwords</span></span>
<span data-ttu-id="64773-132">You should change the access keys (and passwords for MongoDB API accounts) to your Azure Cosmos DB account periodically to help keep your connections more secure.</span><span class="sxs-lookup"><span data-stu-id="64773-132">You should change the access keys (and passwords for MongoDB API accounts) to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="64773-133">Two access keys/passwords are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span><span class="sxs-lookup"><span data-stu-id="64773-133">Two access keys/passwords are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="64773-134">Regenerating your access keys affects any applications that are dependent on the current key.</span><span class="sxs-lookup"><span data-stu-id="64773-134">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="64773-135">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span><span class="sxs-lookup"><span data-stu-id="64773-135">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="64773-136">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span><span class="sxs-lookup"><span data-stu-id="64773-136">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="64773-137">The following steps outline the process involved in rolling your keys/passwords.</span><span class="sxs-lookup"><span data-stu-id="64773-137">The following steps outline the process involved in rolling your keys/passwords.</span></span>

1. <span data-ttu-id="64773-138">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="64773-138">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="64773-139">Regenerate the primary access key for your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="64773-139">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="64773-140">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="64773-140">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="64773-141">In the **Azure Cosmos DB Account** page, click **Keys** (or **Connection String** for MongoDB accounts\*\*).</span><span class="sxs-lookup"><span data-stu-id="64773-141">In the **Azure Cosmos DB Account** page, click **Keys** (or **Connection String** for MongoDB accounts\*\*).</span></span>
4. <span data-ttu-id="64773-142">On the **Keys**/**Connection String** page, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span><span class="sxs-lookup"><span data-stu-id="64773-142">On the **Keys**/**Connection String** page, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="64773-143">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="64773-143">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="64773-144">Once you have verified that the new key is available for use (approximately five minutes after regeneration), update the access key in your application code to reference the new primary access key.</span><span class="sxs-lookup"><span data-stu-id="64773-144">Once you have verified that the new key is available for use (approximately five minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="64773-145">Regenerate the secondary access key.</span><span class="sxs-lookup"><span data-stu-id="64773-145">Regenerate the secondary access key.</span></span>
   
    ![Regenerate access keys](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="64773-147">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="64773-147">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the-connection-string"></a><span data-ttu-id="64773-148">Get the connection string</span><span class="sxs-lookup"><span data-stu-id="64773-148">Get the connection string</span></span>
<span data-ttu-id="64773-149">To retrieve your connection string, do the following:</span><span class="sxs-lookup"><span data-stu-id="64773-149">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="64773-150">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="64773-150">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="64773-151">In the resource menu, click **Keys** (or **Connection String** for MongoDB API accounts).</span><span class="sxs-lookup"><span data-stu-id="64773-151">In the resource menu, click **Keys** (or **Connection String** for MongoDB API accounts).</span></span>
3. <span data-ttu-id="64773-152">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span><span class="sxs-lookup"><span data-stu-id="64773-152">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="64773-153">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span><span class="sxs-lookup"><span data-stu-id="64773-153">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="64773-154">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="64773-154">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <a id="delete"></a> <span data-ttu-id="64773-155">Delete an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="64773-155">Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="64773-156">To remove an Azure Cosmos DB account from the Azure portal that you are no longer using, right-click the account name, and click **Delete account**.</span><span class="sxs-lookup"><span data-stu-id="64773-156">To remove an Azure Cosmos DB account from the Azure portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![How to delete an Azure Cosmos DB account in the Azure portal](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="64773-158">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="64773-158">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="64773-159">On the **Azure Cosmos DB account** page, right-click the account, and then click **Delete Account**.</span><span class="sxs-lookup"><span data-stu-id="64773-159">On the **Azure Cosmos DB account** page, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="64773-160">On the resulting confirmation page, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span><span class="sxs-lookup"><span data-stu-id="64773-160">On the resulting confirmation page, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="64773-161">Click the **Delete** button.</span><span class="sxs-lookup"><span data-stu-id="64773-161">Click the **Delete** button.</span></span>

![How to delete an Azure Cosmos DB account in the Azure portal](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a><span data-ttu-id="64773-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="64773-163">Next steps</span></span>
<span data-ttu-id="64773-164">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="64773-164">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
