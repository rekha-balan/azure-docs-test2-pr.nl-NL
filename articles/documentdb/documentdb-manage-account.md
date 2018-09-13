---
title: Manage a DocumentDB account via the Azure Portal | Microsoft Docs
description: Learn how to manage your DocumentDB account via the Azure Portal. Find a guide on using the Azure Portal to view, copy, delete and access accounts.
keywords: Azure Portal, documentdb, azure, Microsoft azure
services: documentdb
documentationcenter: ''
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: kirillg
ms.openlocfilehash: 7df24573357efe8d75caac531a8a2771047e9bce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554058"
---
# <a name="how-to-manage-a-documentdb-account"></a><span data-ttu-id="7b6be-105">How to manage a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="7b6be-105">How to manage a DocumentDB account</span></span>
<span data-ttu-id="7b6be-106">Learn how to set global consistency, work with keys, and delete a DocumentDB account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7b6be-106">Learn how to set global consistency, work with keys, and delete a DocumentDB account in the Azure portal.</span></span>

## <a id="consistency"></a><span data-ttu-id="7b6be-107">Manage DocumentDB consistency settings</span><span class="sxs-lookup"><span data-stu-id="7b6be-107">Manage DocumentDB consistency settings</span></span>
<span data-ttu-id="7b6be-108">Selecting the right consistency level depends on the semantics of your application.</span><span class="sxs-lookup"><span data-stu-id="7b6be-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="7b6be-109">You should familiarize yourself with the available consistency levels in DocumentDB by reading [Using consistency levels to maximize availability and performance in DocumentDB][consistency].</span><span class="sxs-lookup"><span data-stu-id="7b6be-109">You should familiarize yourself with the available consistency levels in DocumentDB by reading [Using consistency levels to maximize availability and performance in DocumentDB][consistency].</span></span> <span data-ttu-id="7b6be-110">DocumentDB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-110">DocumentDB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="7b6be-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span><span class="sxs-lookup"><span data-stu-id="7b6be-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="7b6be-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="7b6be-113">The following simple steps show you how to select the default consistency level for your database account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-a-documentdb-account"></a><span data-ttu-id="7b6be-114">To specify the default consistency for a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="7b6be-114">To specify the default consistency for a DocumentDB account</span></span>
1. <span data-ttu-id="7b6be-115">In the [Azure portal](https://portal.azure.com/), access your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-115">In the [Azure portal](https://portal.azure.com/), access your DocumentDB account.</span></span>
2. <span data-ttu-id="7b6be-116">In the account blade, click **Default consistency**.</span><span class="sxs-lookup"><span data-stu-id="7b6be-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="7b6be-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7b6be-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="7b6be-118">![Default consistency session][5]</span><span class="sxs-lookup"><span data-stu-id="7b6be-118">![Default consistency session][5]</span></span>

## <a id="keys"></a><span data-ttu-id="7b6be-119">View, copy, and regenerate access keys</span><span class="sxs-lookup"><span data-stu-id="7b6be-119">View, copy, and regenerate access keys</span></span>
<span data-ttu-id="7b6be-120">When you create a DocumentDB account, the service generates two master access keys that can be used for authentication when the DocumentDB account is accessed.</span><span class="sxs-lookup"><span data-stu-id="7b6be-120">When you create a DocumentDB account, the service generates two master access keys that can be used for authentication when the DocumentDB account is accessed.</span></span> <span data-ttu-id="7b6be-121">By providing two access keys, DocumentDB enables you to regenerate the keys with no interruption to your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-121">By providing two access keys, DocumentDB enables you to regenerate the keys with no interruption to your DocumentDB account.</span></span> 

<span data-ttu-id="7b6be-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **DocumentDB account** blade to view, copy, and regenerate the access keys that are used to access your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **DocumentDB account** blade to view, copy, and regenerate the access keys that are used to access your DocumentDB account.</span></span>

![Azure Portal screenshot, Keys blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="7b6be-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](documentdb-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="7b6be-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](documentdb-import-data.md).</span></span>
> 
> 

<span data-ttu-id="7b6be-125">Read-only keys are also available on this blade.</span><span class="sxs-lookup"><span data-stu-id="7b6be-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="7b6be-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span><span class="sxs-lookup"><span data-stu-id="7b6be-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="7b6be-127">Copy an access key in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b6be-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="7b6be-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span><span class="sxs-lookup"><span data-stu-id="7b6be-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![View and copy an access key in the Azure Portal, Keys blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="7b6be-130">Regenerate access keys</span><span class="sxs-lookup"><span data-stu-id="7b6be-130">Regenerate access keys</span></span>
<span data-ttu-id="7b6be-131">You should change the access keys to your DocumentDB account periodically to help keep your connections more secure.</span><span class="sxs-lookup"><span data-stu-id="7b6be-131">You should change the access keys to your DocumentDB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="7b6be-132">Two access keys are assigned to enable you to maintain connections to the DocumentDB account using one access key while you regenerate the other access key.</span><span class="sxs-lookup"><span data-stu-id="7b6be-132">Two access keys are assigned to enable you to maintain connections to the DocumentDB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="7b6be-133">Regenerating your access keys affects any applications that are dependent on the current key.</span><span class="sxs-lookup"><span data-stu-id="7b6be-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="7b6be-134">All clients that use the access key to access the DocumentDB account must be updated to use the new key.</span><span class="sxs-lookup"><span data-stu-id="7b6be-134">All clients that use the access key to access the DocumentDB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="7b6be-135">If you have applications or cloud services using the DocumentDB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span><span class="sxs-lookup"><span data-stu-id="7b6be-135">If you have applications or cloud services using the DocumentDB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="7b6be-136">The following steps outline the process involved in rolling your keys.</span><span class="sxs-lookup"><span data-stu-id="7b6be-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="7b6be-137">Update the access key in your application code to reference the secondary access key of the DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-137">Update the access key in your application code to reference the secondary access key of the DocumentDB account.</span></span>
2. <span data-ttu-id="7b6be-138">Regenerate the primary access key for your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-138">Regenerate the primary access key for your DocumentDB account.</span></span> <span data-ttu-id="7b6be-139">In the [Azure Portal](https://portal.azure.com/), access your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-139">In the [Azure Portal](https://portal.azure.com/), access your DocumentDB account.</span></span>
3. <span data-ttu-id="7b6be-140">In the **DocumentDB Account** blade, click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="7b6be-140">In the **DocumentDB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="7b6be-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span><span class="sxs-lookup"><span data-stu-id="7b6be-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="7b6be-142">![Regenerate access keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="7b6be-142">![Regenerate access keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="7b6be-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span><span class="sxs-lookup"><span data-stu-id="7b6be-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="7b6be-144">Regenerate the secondary access key.</span><span class="sxs-lookup"><span data-stu-id="7b6be-144">Regenerate the secondary access key.</span></span>
   
    ![Regenerate access keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="7b6be-146">It can take several minutes before a newly generated key can be used to access your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-146">It can take several minutes before a newly generated key can be used to access your DocumentDB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="7b6be-147">Get the  connection string</span><span class="sxs-lookup"><span data-stu-id="7b6be-147">Get the  connection string</span></span>
<span data-ttu-id="7b6be-148">To retrieve your connection string, do the following:</span><span class="sxs-lookup"><span data-stu-id="7b6be-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="7b6be-149">In the [Azure portal](https://portal.azure.com), access your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-149">In the [Azure portal](https://portal.azure.com), access your DocumentDB account.</span></span>
2. <span data-ttu-id="7b6be-150">In the resource menu, click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="7b6be-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="7b6be-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span><span class="sxs-lookup"><span data-stu-id="7b6be-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="7b6be-152">If you are using the connection string in the [DocumentDB Database Migration Tool](documentdb-import-data.md), append the database name to the end of the connection string.</span><span class="sxs-lookup"><span data-stu-id="7b6be-152">If you are using the connection string in the [DocumentDB Database Migration Tool](documentdb-import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="7b6be-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="7b6be-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <a id="delete"></a> <span data-ttu-id="7b6be-154">Delete a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="7b6be-154">Delete a DocumentDB account</span></span>
<span data-ttu-id="7b6be-155">To remove a DocumentDB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span><span class="sxs-lookup"><span data-stu-id="7b6be-155">To remove a DocumentDB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![How to delete a DocumentDB account in the Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-manage-account/deleteaccount.png)

1. <span data-ttu-id="7b6be-157">In the [Azure portal](https://portal.azure.com/), access the DocumentDB account you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="7b6be-157">In the [Azure portal](https://portal.azure.com/), access the DocumentDB account you wish to delete.</span></span>
2. <span data-ttu-id="7b6be-158">On the **DocumentDB account** blade, right-click the account, and then click **Delete Account**.</span><span class="sxs-lookup"><span data-stu-id="7b6be-158">On the **DocumentDB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="7b6be-159">On the resulting confirmation blade, type the DocumentDB account name to confirm that you want to delete the account.</span><span class="sxs-lookup"><span data-stu-id="7b6be-159">On the resulting confirmation blade, type the DocumentDB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="7b6be-160">Click the **Delete** button.</span><span class="sxs-lookup"><span data-stu-id="7b6be-160">Click the **Delete** button.</span></span>

![How to delete a DocumentDB account in the Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-manage-account/delete-account-confirm.png)

## <a id="next"></a><span data-ttu-id="7b6be-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b6be-162">Next steps</span></span>
<span data-ttu-id="7b6be-163">Learn how to [get started with your DocumentDB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="7b6be-163">Learn how to [get started with your DocumentDB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[1]: ./media/documentdb-manage-account/documentdb_add_region-1.png
[2]: ./media/documentdb-manage-account/documentdb_add_region-2.png
[3]: ./media/documentdb-manage-account/documentdb_change_write_region-1.png
[4]: ./media/documentdb-manage-account/documentdb_change_write_region-2.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-manage-account/documentdb_change_consistency-1.png
[6]: ./media/documentdb-manage-account/chooseandsaveconsistency.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: https://azure.microsoft.com/documentation/articles/documentdb-consistency-levels/
[azureregions]: https://azure.microsoft.com/en-us/regions/#services
[offers]: https://azure.microsoft.com/en-us/pricing/details/documentdb/







