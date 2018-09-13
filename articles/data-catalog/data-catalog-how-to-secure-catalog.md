---
title: How to secure access to Azure Data Catalog
description: This article explain how to secure data catalog and its data assets.
services: data-catalog
author: steelanddata
ms.author: maroche
ms.service: data-catalog
ms.topic: conceptual
ms.date: 01/18/2018
ms.openlocfilehash: 6b82c71154edfe5fedab3b92e25c11007820c15c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857385"
---
# <a name="how-to-secure-access-to-data-catalog-and-data-assets"></a><span data-ttu-id="65c5d-103">How to secure access to data catalog and data assets</span><span class="sxs-lookup"><span data-stu-id="65c5d-103">How to secure access to data catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="65c5d-104">This feature is available only in the standard edition of Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="65c5d-104">This feature is available only in the standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="65c5d-105">Azure Data Catalog allows you to specify who can access the data catalog and what operations (register, annotate, take ownership) they can perform on metadata in the catalog.</span><span class="sxs-lookup"><span data-stu-id="65c5d-105">Azure Data Catalog allows you to specify who can access the data catalog and what operations (register, annotate, take ownership) they can perform on metadata in the catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="65c5d-106">Catalog users and permissions</span><span class="sxs-lookup"><span data-stu-id="65c5d-106">Catalog users and permissions</span></span>
<span data-ttu-id="65c5d-107">To give a user or a group the access to a data catalog and set permissions:</span><span class="sxs-lookup"><span data-stu-id="65c5d-107">To give a user or a group the access to a data catalog and set permissions:</span></span>

1. <span data-ttu-id="65c5d-108">On the [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="65c5d-108">On the [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on the toolbar.</span></span>

    ![data catalog - settings](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="65c5d-110">In the settings page, expand the **Catalog Users** section.</span><span class="sxs-lookup"><span data-stu-id="65c5d-110">In the settings page, expand the **Catalog Users** section.</span></span>
    <span data-ttu-id="65c5d-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="65c5d-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="65c5d-112">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="65c5d-112">Click **Add**.</span></span>
4. <span data-ttu-id="65c5d-113">Enter the fully qualified **user name** or name of the **security group** in the Azure Active Directory (AAD) associated with the catalog.</span><span class="sxs-lookup"><span data-stu-id="65c5d-113">Enter the fully qualified **user name** or name of the **security group** in the Azure Active Directory (AAD) associated with the catalog.</span></span> <span data-ttu-id="65c5d-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span><span class="sxs-lookup"><span data-stu-id="65c5d-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="65c5d-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="65c5d-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="65c5d-116">Press **ENTER** or **TAB** out of the text box.</span><span class="sxs-lookup"><span data-stu-id="65c5d-116">Press **ENTER** or **TAB** out of the text box.</span></span> 
6.  <span data-ttu-id="65c5d-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned to these users or groups by default.</span><span class="sxs-lookup"><span data-stu-id="65c5d-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned to these users or groups by default.</span></span> <span data-ttu-id="65c5d-118">That is, the user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="65c5d-118">That is, the user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="65c5d-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="65c5d-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="65c5d-120">To give a user or group only the read access to the catalog, clear the **annotate** option for that user or group.</span><span class="sxs-lookup"><span data-stu-id="65c5d-120">To give a user or group only the read access to the catalog, clear the **annotate** option for that user or group.</span></span> <span data-ttu-id="65c5d-121">When you do so, the user or group cannot annotate data assets in the catalog but they can view them.</span><span class="sxs-lookup"><span data-stu-id="65c5d-121">When you do so, the user or group cannot annotate data assets in the catalog but they can view them.</span></span> 
8.  <span data-ttu-id="65c5d-122">To deny a user or group from registering data assets, clear the **register** option for that user or group.</span><span class="sxs-lookup"><span data-stu-id="65c5d-122">To deny a user or group from registering data assets, clear the **register** option for that user or group.</span></span>
9.  <span data-ttu-id="65c5d-123">To deny a user from taking ownership of a data asset, clear the **take ownership** option for that user or group.</span><span class="sxs-lookup"><span data-stu-id="65c5d-123">To deny a user from taking ownership of a data asset, clear the **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="65c5d-124">To delete a user/group from catalog users, click **x** for the user/group at the bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="65c5d-124">To delete a user/group from catalog users, click **x** for the user/group at the bottom of the list.</span></span> 
    <span data-ttu-id="65c5d-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="65c5d-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="65c5d-126">We recommend that you add security groups to catalog users rather than adding users directly and assign permissions.</span><span class="sxs-lookup"><span data-stu-id="65c5d-126">We recommend that you add security groups to catalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="65c5d-127">Then, add users to the security groups that match their roles and their required access to the catalog.</span><span class="sxs-lookup"><span data-stu-id="65c5d-127">Then, add users to the security groups that match their roles and their required access to the catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="65c5d-128">Special considerations</span><span class="sxs-lookup"><span data-stu-id="65c5d-128">Special considerations</span></span>

- <span data-ttu-id="65c5d-129">The permissions assigned to security groups are additive.</span><span class="sxs-lookup"><span data-stu-id="65c5d-129">The permissions assigned to security groups are additive.</span></span> <span data-ttu-id="65c5d-130">Say, a user is in two groups.</span><span class="sxs-lookup"><span data-stu-id="65c5d-130">Say, a user is in two groups.</span></span> <span data-ttu-id="65c5d-131">One group has annotate permissions and other group does not have annotate permissions.</span><span class="sxs-lookup"><span data-stu-id="65c5d-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="65c5d-132">Then, user has annotate permissions.</span><span class="sxs-lookup"><span data-stu-id="65c5d-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="65c5d-133">The permissions assigned explicitly to a user override the permissions assigned to groups to which the user belongs.</span><span class="sxs-lookup"><span data-stu-id="65c5d-133">The permissions assigned explicitly to a user override the permissions assigned to groups to which the user belongs.</span></span> <span data-ttu-id="65c5d-134">In the previous example, say, you explicitly added the user to catalog users and do not assign annotate permissions.</span><span class="sxs-lookup"><span data-stu-id="65c5d-134">In the previous example, say, you explicitly added the user to catalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="65c5d-135">The user cannot annotate data assets even though the user is a member of a group that does have annotate permissions.</span><span class="sxs-lookup"><span data-stu-id="65c5d-135">The user cannot annotate data assets even though the user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65c5d-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="65c5d-136">Next steps</span></span>
- [<span data-ttu-id="65c5d-137">Get started with Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="65c5d-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

