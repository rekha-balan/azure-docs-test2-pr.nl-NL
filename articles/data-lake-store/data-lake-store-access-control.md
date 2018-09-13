---
title: Overview of access control in Data Lake Store | Microsoft Docs
description: Understand how access control works in Azure Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/06/2017
ms.author: nitinme
ms.openlocfilehash: 76880b0733c510a878058b6353ccb110979241f3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549188"
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="49c8f-103">Access control in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49c8f-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="49c8f-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from the POSIX access control model.</span><span class="sxs-lookup"><span data-stu-id="49c8f-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from the POSIX access control model.</span></span> <span data-ttu-id="49c8f-105">This article summarizes the basics of the access control model for Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49c8f-105">This article summarizes the basics of the access control model for Data Lake Store.</span></span> <span data-ttu-id="49c8f-106">To learn more about the HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="49c8f-106">To learn more about the HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="49c8f-107">Access control lists on files and folders</span><span class="sxs-lookup"><span data-stu-id="49c8f-107">Access control lists on files and folders</span></span>

<span data-ttu-id="49c8f-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span><span class="sxs-lookup"><span data-stu-id="49c8f-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="49c8f-109">**Access ACLs**: These control access to an object.</span><span class="sxs-lookup"><span data-stu-id="49c8f-109">**Access ACLs**: These control access to an object.</span></span> <span data-ttu-id="49c8f-110">Files and folders both have Access ACLs.</span><span class="sxs-lookup"><span data-stu-id="49c8f-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="49c8f-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine the Access ACLs for any child items that are created under that folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine the Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="49c8f-112">Files do not have Default ACLs.</span><span class="sxs-lookup"><span data-stu-id="49c8f-112">Files do not have Default ACLs.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="49c8f-114">Both Access ACLs and Default ACLs have the same structure.</span><span class="sxs-lookup"><span data-stu-id="49c8f-114">Both Access ACLs and Default ACLs have the same structure.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="49c8f-116">Changing the Default ACL on a parent does not affect the Access ACL or Default ACL of child items that already exist.</span><span class="sxs-lookup"><span data-stu-id="49c8f-116">Changing the Default ACL on a parent does not affect the Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="49c8f-117">Users and identities</span><span class="sxs-lookup"><span data-stu-id="49c8f-117">Users and identities</span></span>

<span data-ttu-id="49c8f-118">Every file and folder has distinct permissions for these identities:</span><span class="sxs-lookup"><span data-stu-id="49c8f-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="49c8f-119">The owning user of the file</span><span class="sxs-lookup"><span data-stu-id="49c8f-119">The owning user of the file</span></span>
* <span data-ttu-id="49c8f-120">The owning group</span><span class="sxs-lookup"><span data-stu-id="49c8f-120">The owning group</span></span>
* <span data-ttu-id="49c8f-121">Named users</span><span class="sxs-lookup"><span data-stu-id="49c8f-121">Named users</span></span>
* <span data-ttu-id="49c8f-122">Named groups</span><span class="sxs-lookup"><span data-stu-id="49c8f-122">Named groups</span></span>
* <span data-ttu-id="49c8f-123">All other users</span><span class="sxs-lookup"><span data-stu-id="49c8f-123">All other users</span></span>

<span data-ttu-id="49c8f-124">The identities of users and groups are Azure Active Directory (Azure AD) identities.</span><span class="sxs-lookup"><span data-stu-id="49c8f-124">The identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="49c8f-125">So unless otherwise noted, a "user," in the context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span><span class="sxs-lookup"><span data-stu-id="49c8f-125">So unless otherwise noted, a "user," in the context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="49c8f-126">Permissions</span><span class="sxs-lookup"><span data-stu-id="49c8f-126">Permissions</span></span>

<span data-ttu-id="49c8f-127">The permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="49c8f-127">The permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in the following table:</span></span>

|            |    <span data-ttu-id="49c8f-128">File</span><span class="sxs-lookup"><span data-stu-id="49c8f-128">File</span></span>     |   <span data-ttu-id="49c8f-129">Folder</span><span class="sxs-lookup"><span data-stu-id="49c8f-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="49c8f-130">**Read (R)**</span><span class="sxs-lookup"><span data-stu-id="49c8f-130">**Read (R)**</span></span> | <span data-ttu-id="49c8f-131">Can read the contents of a file</span><span class="sxs-lookup"><span data-stu-id="49c8f-131">Can read the contents of a file</span></span> | <span data-ttu-id="49c8f-132">Requires **Read** and **Execute** to list the contents of the folder</span><span class="sxs-lookup"><span data-stu-id="49c8f-132">Requires **Read** and **Execute** to list the contents of the folder</span></span>|
| <span data-ttu-id="49c8f-133">**Write (W)**</span><span class="sxs-lookup"><span data-stu-id="49c8f-133">**Write (W)**</span></span> | <span data-ttu-id="49c8f-134">Can write or append to a file</span><span class="sxs-lookup"><span data-stu-id="49c8f-134">Can write or append to a file</span></span> | <span data-ttu-id="49c8f-135">Requires **Write** and **Execute** to create child items in a folder</span><span class="sxs-lookup"><span data-stu-id="49c8f-135">Requires **Write** and **Execute** to create child items in a folder</span></span> |
| <span data-ttu-id="49c8f-136">**Execute (X)**</span><span class="sxs-lookup"><span data-stu-id="49c8f-136">**Execute (X)**</span></span> | <span data-ttu-id="49c8f-137">Does not mean anything in the context of Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49c8f-137">Does not mean anything in the context of Data Lake Store</span></span> | <span data-ttu-id="49c8f-138">Required to traverse the child items of a folder</span><span class="sxs-lookup"><span data-stu-id="49c8f-138">Required to traverse the child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="49c8f-139">Short forms for permissions</span><span class="sxs-lookup"><span data-stu-id="49c8f-139">Short forms for permissions</span></span>

<span data-ttu-id="49c8f-140">**RWX** is used to indicate **Read + Write + Execute**.</span><span class="sxs-lookup"><span data-stu-id="49c8f-140">**RWX** is used to indicate **Read + Write + Execute**.</span></span> <span data-ttu-id="49c8f-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, the sum of which represents the permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, the sum of which represents the permissions.</span></span> <span data-ttu-id="49c8f-142">Following are some examples.</span><span class="sxs-lookup"><span data-stu-id="49c8f-142">Following are some examples.</span></span>

| <span data-ttu-id="49c8f-143">Numeric form</span><span class="sxs-lookup"><span data-stu-id="49c8f-143">Numeric form</span></span> | <span data-ttu-id="49c8f-144">Short form</span><span class="sxs-lookup"><span data-stu-id="49c8f-144">Short form</span></span> |      <span data-ttu-id="49c8f-145">What it means</span><span class="sxs-lookup"><span data-stu-id="49c8f-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="49c8f-146">7</span><span class="sxs-lookup"><span data-stu-id="49c8f-146">7</span></span>            | <span data-ttu-id="49c8f-147">RWX</span><span class="sxs-lookup"><span data-stu-id="49c8f-147">RWX</span></span>        | <span data-ttu-id="49c8f-148">Read + Write + Execute</span><span class="sxs-lookup"><span data-stu-id="49c8f-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="49c8f-149">5</span><span class="sxs-lookup"><span data-stu-id="49c8f-149">5</span></span>            | <span data-ttu-id="49c8f-150">R-X</span><span class="sxs-lookup"><span data-stu-id="49c8f-150">R-X</span></span>        | <span data-ttu-id="49c8f-151">Read + Execute</span><span class="sxs-lookup"><span data-stu-id="49c8f-151">Read + Execute</span></span>         |
| <span data-ttu-id="49c8f-152">4</span><span class="sxs-lookup"><span data-stu-id="49c8f-152">4</span></span>            | <span data-ttu-id="49c8f-153">R--</span><span class="sxs-lookup"><span data-stu-id="49c8f-153">R--</span></span>        | <span data-ttu-id="49c8f-154">Read</span><span class="sxs-lookup"><span data-stu-id="49c8f-154">Read</span></span>                   |
| <span data-ttu-id="49c8f-155">0</span><span class="sxs-lookup"><span data-stu-id="49c8f-155">0</span></span>            | ---        | <span data-ttu-id="49c8f-156">No permissions</span><span class="sxs-lookup"><span data-stu-id="49c8f-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="49c8f-157">Permissions do not inherit</span><span class="sxs-lookup"><span data-stu-id="49c8f-157">Permissions do not inherit</span></span>

<span data-ttu-id="49c8f-158">In the POSIX-style model that's used by Data Lake Store, permissions for an item are stored on the item itself.</span><span class="sxs-lookup"><span data-stu-id="49c8f-158">In the POSIX-style model that's used by Data Lake Store, permissions for an item are stored on the item itself.</span></span> <span data-ttu-id="49c8f-159">In other words, permissions for an item cannot be inherited from the parent items.</span><span class="sxs-lookup"><span data-stu-id="49c8f-159">In other words, permissions for an item cannot be inherited from the parent items.</span></span>

## <a name="common-scenarios-related-to-permissions"></a><span data-ttu-id="49c8f-160">Common scenarios related to permissions</span><span class="sxs-lookup"><span data-stu-id="49c8f-160">Common scenarios related to permissions</span></span>

<span data-ttu-id="49c8f-161">Following are some common scenarios to help you understand which permissions are needed to perform certain operations on a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="49c8f-161">Following are some common scenarios to help you understand which permissions are needed to perform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-to-read-a-file"></a><span data-ttu-id="49c8f-162">Permissions needed to read a file</span><span class="sxs-lookup"><span data-stu-id="49c8f-162">Permissions needed to read a file</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="49c8f-164">For the file to be read, the caller needs **Read** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-164">For the file to be read, the caller needs **Read** permissions.</span></span>
* <span data-ttu-id="49c8f-165">For all the folders in the folder structure that contain the file, the caller needs **Execute** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-165">For all the folders in the folder structure that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-append-to-a-file"></a><span data-ttu-id="49c8f-166">Permissions needed to append to a file</span><span class="sxs-lookup"><span data-stu-id="49c8f-166">Permissions needed to append to a file</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="49c8f-168">For the file to be appended to, the caller needs **Write** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-168">For the file to be appended to, the caller needs **Write** permissions.</span></span>
* <span data-ttu-id="49c8f-169">For all the folders that contain the file, the caller needs **Execute** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-169">For all the folders that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-delete-a-file"></a><span data-ttu-id="49c8f-170">Permissions needed to delete a file</span><span class="sxs-lookup"><span data-stu-id="49c8f-170">Permissions needed to delete a file</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="49c8f-172">For the parent folder, the caller needs **Write + Execute** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-172">For the parent folder, the caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="49c8f-173">For all the other folders in the file’s path, the caller needs **Execute** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-173">For all the other folders in the file’s path, the caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="49c8f-174">Write permissions on the file are not required to delete it as long as the previous two conditions are true.</span><span class="sxs-lookup"><span data-stu-id="49c8f-174">Write permissions on the file are not required to delete it as long as the previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-to-enumerate-a-folder"></a><span data-ttu-id="49c8f-175">Permissions needed to enumerate a folder</span><span class="sxs-lookup"><span data-stu-id="49c8f-175">Permissions needed to enumerate a folder</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="49c8f-177">For the folder to enumerate, the caller needs **Read + Execute** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-177">For the folder to enumerate, the caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="49c8f-178">For all the ancestor folders, the caller needs **Execute** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-178">For all the ancestor folders, the caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-the-azure-portal"></a><span data-ttu-id="49c8f-179">Viewing permissions in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="49c8f-179">Viewing permissions in the Azure portal</span></span>

<span data-ttu-id="49c8f-180">From the **Data Explorer** blade of the Data Lake Store account, click **Access** to see the ACLs for a file or a folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-180">From the **Data Explorer** blade of the Data Lake Store account, click **Access** to see the ACLs for a file or a folder.</span></span> <span data-ttu-id="49c8f-181">Click **Access** to see the ACLs for the **catalog** folder under the **mydatastore** account.</span><span class="sxs-lookup"><span data-stu-id="49c8f-181">Click **Access** to see the ACLs for the **catalog** folder under the **mydatastore** account.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="49c8f-183">On this blade, the top section shows an overview of the permissions that you have.</span><span class="sxs-lookup"><span data-stu-id="49c8f-183">On this blade, the top section shows an overview of the permissions that you have.</span></span> <span data-ttu-id="49c8f-184">(In the screenshot, the user is Bob.) Following that, the access permissions are shown.</span><span class="sxs-lookup"><span data-stu-id="49c8f-184">(In the screenshot, the user is Bob.) Following that, the access permissions are shown.</span></span> <span data-ttu-id="49c8f-185">After that, from the **Access** blade, click **Simple View** to see the simpler view.</span><span class="sxs-lookup"><span data-stu-id="49c8f-185">After that, from the **Access** blade, click **Simple View** to see the simpler view.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="49c8f-187">Click **Advanced View** to see the more advanced view, where the concepts of Default ACLs, mask, and super-user are shown.</span><span class="sxs-lookup"><span data-stu-id="49c8f-187">Click **Advanced View** to see the more advanced view, where the concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="the-super-user"></a><span data-ttu-id="49c8f-189">The super-user</span><span class="sxs-lookup"><span data-stu-id="49c8f-189">The super-user</span></span>

<span data-ttu-id="49c8f-190">A super-user has the most rights of all the users in the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49c8f-190">A super-user has the most rights of all the users in the Data Lake Store.</span></span> <span data-ttu-id="49c8f-191">A super-user:</span><span class="sxs-lookup"><span data-stu-id="49c8f-191">A super-user:</span></span>

* <span data-ttu-id="49c8f-192">Has RWX Permissions to **all** files and folders.</span><span class="sxs-lookup"><span data-stu-id="49c8f-192">Has RWX Permissions to **all** files and folders.</span></span>
* <span data-ttu-id="49c8f-193">Can change the permissions on any file or folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-193">Can change the permissions on any file or folder.</span></span>
* <span data-ttu-id="49c8f-194">Can change the owning user or owning group of any file or folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-194">Can change the owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="49c8f-195">In Azure, a Data Lake Store account has several Azure roles, including:</span><span class="sxs-lookup"><span data-stu-id="49c8f-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="49c8f-196">Owners</span><span class="sxs-lookup"><span data-stu-id="49c8f-196">Owners</span></span>
* <span data-ttu-id="49c8f-197">Contributors</span><span class="sxs-lookup"><span data-stu-id="49c8f-197">Contributors</span></span>
* <span data-ttu-id="49c8f-198">Readers</span><span class="sxs-lookup"><span data-stu-id="49c8f-198">Readers</span></span>

<span data-ttu-id="49c8f-199">Everyone in the **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span><span class="sxs-lookup"><span data-stu-id="49c8f-199">Everyone in the **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="49c8f-200">To learn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="49c8f-200">To learn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="49c8f-201">If you want to create a custom role-based-access control (RBAC) role that has super-user permissions, it needs to have the following permissions:</span><span class="sxs-lookup"><span data-stu-id="49c8f-201">If you want to create a custom role-based-access control (RBAC) role that has super-user permissions, it needs to have the following permissions:</span></span>
- <span data-ttu-id="49c8f-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="49c8f-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="49c8f-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="49c8f-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="the-owning-user"></a><span data-ttu-id="49c8f-204">The owning user</span><span class="sxs-lookup"><span data-stu-id="49c8f-204">The owning user</span></span>

<span data-ttu-id="49c8f-205">The user who created the item is automatically the owning user of the item.</span><span class="sxs-lookup"><span data-stu-id="49c8f-205">The user who created the item is automatically the owning user of the item.</span></span> <span data-ttu-id="49c8f-206">An owning user can:</span><span class="sxs-lookup"><span data-stu-id="49c8f-206">An owning user can:</span></span>

* <span data-ttu-id="49c8f-207">Change the permissions of a file that is owned.</span><span class="sxs-lookup"><span data-stu-id="49c8f-207">Change the permissions of a file that is owned.</span></span>
* <span data-ttu-id="49c8f-208">Change the owning group of a file that is owned, as long as the owning user is also a member of the target group.</span><span class="sxs-lookup"><span data-stu-id="49c8f-208">Change the owning group of a file that is owned, as long as the owning user is also a member of the target group.</span></span>

> [!NOTE]
> <span data-ttu-id="49c8f-209">The owning user *cannot* change the owning user of another owned file.</span><span class="sxs-lookup"><span data-stu-id="49c8f-209">The owning user *cannot* change the owning user of another owned file.</span></span> <span data-ttu-id="49c8f-210">Only super-users can change the owning user of a file or folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-210">Only super-users can change the owning user of a file or folder.</span></span>
>
>

## <a name="the-owning-group"></a><span data-ttu-id="49c8f-211">The owning group</span><span class="sxs-lookup"><span data-stu-id="49c8f-211">The owning group</span></span>

<span data-ttu-id="49c8f-212">In the POSIX ACLs, every user is associated with a "primary group."</span><span class="sxs-lookup"><span data-stu-id="49c8f-212">In the POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="49c8f-213">For example, user "alice" might belong to the "finance" group.</span><span class="sxs-lookup"><span data-stu-id="49c8f-213">For example, user "alice" might belong to the "finance" group.</span></span> <span data-ttu-id="49c8f-214">Alice might also belong to multiple groups, but one group is always designated as her primary group.</span><span class="sxs-lookup"><span data-stu-id="49c8f-214">Alice might also belong to multiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="49c8f-215">In POSIX, when Alice creates a file, the owning group of that file is set to her primary group, which in this case is "finance."</span><span class="sxs-lookup"><span data-stu-id="49c8f-215">In POSIX, when Alice creates a file, the owning group of that file is set to her primary group, which in this case is "finance."</span></span>

<span data-ttu-id="49c8f-216">When a new filesystem item is created, Data Lake Store assigns a value to the owning group.</span><span class="sxs-lookup"><span data-stu-id="49c8f-216">When a new filesystem item is created, Data Lake Store assigns a value to the owning group.</span></span>

* <span data-ttu-id="49c8f-217">**Case 1**: The root folder "/".</span><span class="sxs-lookup"><span data-stu-id="49c8f-217">**Case 1**: The root folder "/".</span></span> <span data-ttu-id="49c8f-218">This folder is created when a Data Lake Store account is created.</span><span class="sxs-lookup"><span data-stu-id="49c8f-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="49c8f-219">In this case, the owning group is set to the user who created the account.</span><span class="sxs-lookup"><span data-stu-id="49c8f-219">In this case, the owning group is set to the user who created the account.</span></span>
* <span data-ttu-id="49c8f-220">**Case 2** (Every other case): When a new item is created, the owning group is copied from the parent folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-220">**Case 2** (Every other case): When a new item is created, the owning group is copied from the parent folder.</span></span>

<span data-ttu-id="49c8f-221">The owning group can be changed by:</span><span class="sxs-lookup"><span data-stu-id="49c8f-221">The owning group can be changed by:</span></span>
* <span data-ttu-id="49c8f-222">Any super-users.</span><span class="sxs-lookup"><span data-stu-id="49c8f-222">Any super-users.</span></span>
* <span data-ttu-id="49c8f-223">The owning user, if the owning user is also a member of the target group.</span><span class="sxs-lookup"><span data-stu-id="49c8f-223">The owning user, if the owning user is also a member of the target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="49c8f-224">Access check algorithm</span><span class="sxs-lookup"><span data-stu-id="49c8f-224">Access check algorithm</span></span>

<span data-ttu-id="49c8f-225">The following illustration represents the access check algorithm for Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="49c8f-225">The following illustration represents the access check algorithm for Data Lake Store accounts.</span></span>

![Data Lake Store ACLs algorithm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="the-mask-and-effective-permissions"></a><span data-ttu-id="49c8f-227">The mask and "effective permissions"</span><span class="sxs-lookup"><span data-stu-id="49c8f-227">The mask and "effective permissions"</span></span>

<span data-ttu-id="49c8f-228">The **mask** is an RWX value that is used to limit access for **named users**, the **owning group**, and **named groups** when you're performing the access check algorithm.</span><span class="sxs-lookup"><span data-stu-id="49c8f-228">The **mask** is an RWX value that is used to limit access for **named users**, the **owning group**, and **named groups** when you're performing the access check algorithm.</span></span> <span data-ttu-id="49c8f-229">Here are the key concepts for the mask.</span><span class="sxs-lookup"><span data-stu-id="49c8f-229">Here are the key concepts for the mask.</span></span>

* <span data-ttu-id="49c8f-230">The mask creates "effective permissions."</span><span class="sxs-lookup"><span data-stu-id="49c8f-230">The mask creates "effective permissions."</span></span> <span data-ttu-id="49c8f-231">That is, it modifies the permissions at the time of access check.</span><span class="sxs-lookup"><span data-stu-id="49c8f-231">That is, it modifies the permissions at the time of access check.</span></span>
* <span data-ttu-id="49c8f-232">The mask can be directly edited by the file owner and any super-users.</span><span class="sxs-lookup"><span data-stu-id="49c8f-232">The mask can be directly edited by the file owner and any super-users.</span></span>
* <span data-ttu-id="49c8f-233">The mask can remove permissions to create the effective permission.</span><span class="sxs-lookup"><span data-stu-id="49c8f-233">The mask can remove permissions to create the effective permission.</span></span> <span data-ttu-id="49c8f-234">The mask *cannot* add permissions to the effective permission.</span><span class="sxs-lookup"><span data-stu-id="49c8f-234">The mask *cannot* add permissions to the effective permission.</span></span>

<span data-ttu-id="49c8f-235">Let's look at some examples.</span><span class="sxs-lookup"><span data-stu-id="49c8f-235">Let's look at some examples.</span></span> <span data-ttu-id="49c8f-236">In the following example, the mask is set to **RWX**, which means that the mask does not remove any permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-236">In the following example, the mask is set to **RWX**, which means that the mask does not remove any permissions.</span></span> <span data-ttu-id="49c8f-237">The effective permissions for the named user, owning group, and named group are not altered during the access check.</span><span class="sxs-lookup"><span data-stu-id="49c8f-237">The effective permissions for the named user, owning group, and named group are not altered during the access check.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="49c8f-239">In the following example, the mask is set to **R-X**.</span><span class="sxs-lookup"><span data-stu-id="49c8f-239">In the following example, the mask is set to **R-X**.</span></span> <span data-ttu-id="49c8f-240">This means that it **turns off the Write permissions** for **named user**, **owning group**, and **named group** at the time of access check.</span><span class="sxs-lookup"><span data-stu-id="49c8f-240">This means that it **turns off the Write permissions** for **named user**, **owning group**, and **named group** at the time of access check.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="49c8f-242">For reference, here is where the mask for a file or folder appears in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="49c8f-242">For reference, here is where the mask for a file or folder appears in the Azure portal.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="49c8f-244">For a new Data Lake Store account, the mask for the Access ACL and Default ACL of the root folder ("/") defaults to RWX.</span><span class="sxs-lookup"><span data-stu-id="49c8f-244">For a new Data Lake Store account, the mask for the Access ACL and Default ACL of the root folder ("/") defaults to RWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="49c8f-245">Permissions on new files and folders</span><span class="sxs-lookup"><span data-stu-id="49c8f-245">Permissions on new files and folders</span></span>

<span data-ttu-id="49c8f-246">When a new file or folder is created under an existing folder, the Default ACL on the parent folder determines:</span><span class="sxs-lookup"><span data-stu-id="49c8f-246">When a new file or folder is created under an existing folder, the Default ACL on the parent folder determines:</span></span>

- <span data-ttu-id="49c8f-247">A child folder’s Default ACL and Access ACL.</span><span class="sxs-lookup"><span data-stu-id="49c8f-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="49c8f-248">A child file's Access ACL (files do not have a Default ACL).</span><span class="sxs-lookup"><span data-stu-id="49c8f-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="the-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="49c8f-249">The Access ACL of a child file or folder</span><span class="sxs-lookup"><span data-stu-id="49c8f-249">The Access ACL of a child file or folder</span></span>

<span data-ttu-id="49c8f-250">When a child file or folder is created, the parent's Default ACL is copied as the Access ACL of the child file or folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-250">When a child file or folder is created, the parent's Default ACL is copied as the Access ACL of the child file or folder.</span></span> <span data-ttu-id="49c8f-251">Also, if **other** user has RWX permissions in the parent's default ACL, it is removed from the child item's Access ACL.</span><span class="sxs-lookup"><span data-stu-id="49c8f-251">Also, if **other** user has RWX permissions in the parent's default ACL, it is removed from the child item's Access ACL.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="49c8f-253">In most scenarios, the previous information is all you need to know about how a child item’s Access ACL is determined.</span><span class="sxs-lookup"><span data-stu-id="49c8f-253">In most scenarios, the previous information is all you need to know about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="49c8f-254">However, if you are familiar with POSIX systems and want to understand in-depth how this transformation is achieved, see the section [Umask’s role in creating the Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span><span class="sxs-lookup"><span data-stu-id="49c8f-254">However, if you are familiar with POSIX systems and want to understand in-depth how this transformation is achieved, see the section [Umask’s role in creating the Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="49c8f-255">A child folder's Default ACL</span><span class="sxs-lookup"><span data-stu-id="49c8f-255">A child folder's Default ACL</span></span>

<span data-ttu-id="49c8f-256">When a child folder is created under a parent folder, the parent folder's Default ACL is copied over as is to the child folder's Default ACL.</span><span class="sxs-lookup"><span data-stu-id="49c8f-256">When a child folder is created under a parent folder, the parent folder's Default ACL is copied over as is to the child folder's Default ACL.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="49c8f-258">Advanced topics for understanding ACLs in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49c8f-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="49c8f-259">Following are some advanced topics to help you understand how ACLs are determined for Data Lake Store files or folders.</span><span class="sxs-lookup"><span data-stu-id="49c8f-259">Following are some advanced topics to help you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-the-access-acl-for-new-files-and-folders"></a><span data-ttu-id="49c8f-260">Umask’s role in creating the Access ACL for new files and folders</span><span class="sxs-lookup"><span data-stu-id="49c8f-260">Umask’s role in creating the Access ACL for new files and folders</span></span>

<span data-ttu-id="49c8f-261">In a POSIX-compliant system, the general concept is that umask is a 9-bit value on the parent folder that's used to transform the permission for **owning user**, **owning group**, and **other** on the Access ACL of a new child file or folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-261">In a POSIX-compliant system, the general concept is that umask is a 9-bit value on the parent folder that's used to transform the permission for **owning user**, **owning group**, and **other** on the Access ACL of a new child file or folder.</span></span> <span data-ttu-id="49c8f-262">The bits of a umask identify which bits to turn off in the child item’s Access ACL.</span><span class="sxs-lookup"><span data-stu-id="49c8f-262">The bits of a umask identify which bits to turn off in the child item’s Access ACL.</span></span> <span data-ttu-id="49c8f-263">Thus it is used to selectively prevent the propagation of permissions for **owning user**, **owning group**, and **other**.</span><span class="sxs-lookup"><span data-stu-id="49c8f-263">Thus it is used to selectively prevent the propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="49c8f-264">In an HDFS system, the umask is typically a sitewide configuration option that is controlled by administrators.</span><span class="sxs-lookup"><span data-stu-id="49c8f-264">In an HDFS system, the umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="49c8f-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="49c8f-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="49c8f-266">The following table shows the unmask for Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49c8f-266">The following table shows the unmask for Data Lake Store.</span></span>

| <span data-ttu-id="49c8f-267">User group</span><span class="sxs-lookup"><span data-stu-id="49c8f-267">User group</span></span>  | <span data-ttu-id="49c8f-268">Setting</span><span class="sxs-lookup"><span data-stu-id="49c8f-268">Setting</span></span> | <span data-ttu-id="49c8f-269">Effect on new child item's Access ACL</span><span class="sxs-lookup"><span data-stu-id="49c8f-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="49c8f-270">Owning user</span><span class="sxs-lookup"><span data-stu-id="49c8f-270">Owning user</span></span> | ---     | <span data-ttu-id="49c8f-271">No effect</span><span class="sxs-lookup"><span data-stu-id="49c8f-271">No effect</span></span>                             |
| <span data-ttu-id="49c8f-272">Owning group</span><span class="sxs-lookup"><span data-stu-id="49c8f-272">Owning group</span></span>| ---     | <span data-ttu-id="49c8f-273">No effect</span><span class="sxs-lookup"><span data-stu-id="49c8f-273">No effect</span></span>                             |
| <span data-ttu-id="49c8f-274">Other</span><span class="sxs-lookup"><span data-stu-id="49c8f-274">Other</span></span>       | <span data-ttu-id="49c8f-275">RWX</span><span class="sxs-lookup"><span data-stu-id="49c8f-275">RWX</span></span>     | <span data-ttu-id="49c8f-276">Remove Read + Write + Execute</span><span class="sxs-lookup"><span data-stu-id="49c8f-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="49c8f-277">The following illustration shows this umask in action.</span><span class="sxs-lookup"><span data-stu-id="49c8f-277">The following illustration shows this umask in action.</span></span> <span data-ttu-id="49c8f-278">The net effect is to remove **Read + Write + Execute** for **other** user.</span><span class="sxs-lookup"><span data-stu-id="49c8f-278">The net effect is to remove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="49c8f-279">Because the umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span><span class="sxs-lookup"><span data-stu-id="49c8f-279">Because the umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Data Lake Store ACLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="the-sticky-bit"></a><span data-ttu-id="49c8f-281">The sticky bit</span><span class="sxs-lookup"><span data-stu-id="49c8f-281">The sticky bit</span></span>

<span data-ttu-id="49c8f-282">The sticky bit is a more advanced feature of a POSIX filesystem.</span><span class="sxs-lookup"><span data-stu-id="49c8f-282">The sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="49c8f-283">In the context of Data Lake Store, it is unlikely that the sticky bit will be needed.</span><span class="sxs-lookup"><span data-stu-id="49c8f-283">In the context of Data Lake Store, it is unlikely that the sticky bit will be needed.</span></span>

<span data-ttu-id="49c8f-284">The following table shows how the sticky bit works in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49c8f-284">The following table shows how the sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="49c8f-285">User group</span><span class="sxs-lookup"><span data-stu-id="49c8f-285">User group</span></span>         | <span data-ttu-id="49c8f-286">File</span><span class="sxs-lookup"><span data-stu-id="49c8f-286">File</span></span>    | <span data-ttu-id="49c8f-287">Folder</span><span class="sxs-lookup"><span data-stu-id="49c8f-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="49c8f-288">Sticky bit **OFF**</span><span class="sxs-lookup"><span data-stu-id="49c8f-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="49c8f-289">No effect</span><span class="sxs-lookup"><span data-stu-id="49c8f-289">No effect</span></span>   | <span data-ttu-id="49c8f-290">No effect.</span><span class="sxs-lookup"><span data-stu-id="49c8f-290">No effect.</span></span>           |
| <span data-ttu-id="49c8f-291">Sticky bit **ON**</span><span class="sxs-lookup"><span data-stu-id="49c8f-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="49c8f-292">No effect</span><span class="sxs-lookup"><span data-stu-id="49c8f-292">No effect</span></span>   | <span data-ttu-id="49c8f-293">Prevents anyone except **super-users** and the **owning user** of a child item from deleting or renaming that child item.</span><span class="sxs-lookup"><span data-stu-id="49c8f-293">Prevents anyone except **super-users** and the **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="49c8f-294">The sticky bit is not shown in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="49c8f-294">The sticky bit is not shown in the Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="49c8f-295">Common questions about ACLs in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49c8f-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="49c8f-296">Here are some questions that come up often about ACLs in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49c8f-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-to-enable-support-for-acls"></a><span data-ttu-id="49c8f-297">Do I have to enable support for ACLs?</span><span class="sxs-lookup"><span data-stu-id="49c8f-297">Do I have to enable support for ACLs?</span></span>

<span data-ttu-id="49c8f-298">No.</span><span class="sxs-lookup"><span data-stu-id="49c8f-298">No.</span></span> <span data-ttu-id="49c8f-299">Access control via ACLs is always on for a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="49c8f-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-to-recursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="49c8f-300">Which permissions are required to recursively delete a folder and its contents?</span><span class="sxs-lookup"><span data-stu-id="49c8f-300">Which permissions are required to recursively delete a folder and its contents?</span></span>

* <span data-ttu-id="49c8f-301">The parent folder must have **Write + Execute** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-301">The parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="49c8f-302">The folder to be deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span><span class="sxs-lookup"><span data-stu-id="49c8f-302">The folder to be deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="49c8f-303">You do not need Write permissions to delete files in folders.</span><span class="sxs-lookup"><span data-stu-id="49c8f-303">You do not need Write permissions to delete files in folders.</span></span> <span data-ttu-id="49c8f-304">Also, the root folder "/" can **never** be deleted.</span><span class="sxs-lookup"><span data-stu-id="49c8f-304">Also, the root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-the-owner-of-a-file-or-folder"></a><span data-ttu-id="49c8f-305">Who is the owner of a file or folder?</span><span class="sxs-lookup"><span data-stu-id="49c8f-305">Who is the owner of a file or folder?</span></span>

<span data-ttu-id="49c8f-306">The creator of a file or folder becomes the owner.</span><span class="sxs-lookup"><span data-stu-id="49c8f-306">The creator of a file or folder becomes the owner.</span></span>

### <a name="which-group-is-set-as-the-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="49c8f-307">Which group is set as the owning group of a file or folder at creation?</span><span class="sxs-lookup"><span data-stu-id="49c8f-307">Which group is set as the owning group of a file or folder at creation?</span></span>

<span data-ttu-id="49c8f-308">The owning group is copied from the owning group of the parent folder under which the new file or folder is created.</span><span class="sxs-lookup"><span data-stu-id="49c8f-308">The owning group is copied from the owning group of the parent folder under which the new file or folder is created.</span></span>

### <a name="i-am-the-owning-user-of-a-file-but-i-dont-have-the-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="49c8f-309">I am the owning user of a file but I don’t have the RWX permissions I need.</span><span class="sxs-lookup"><span data-stu-id="49c8f-309">I am the owning user of a file but I don’t have the RWX permissions I need.</span></span> <span data-ttu-id="49c8f-310">What do I do?</span><span class="sxs-lookup"><span data-stu-id="49c8f-310">What do I do?</span></span>

<span data-ttu-id="49c8f-311">The owning user can change the permissions of the file to give themselves any RWX permissions they need.</span><span class="sxs-lookup"><span data-stu-id="49c8f-311">The owning user can change the permissions of the file to give themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-the-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="49c8f-312">When I look at ACLs in the Azure portal I see user names but through APIs, I see GUIDs, why is that?</span><span class="sxs-lookup"><span data-stu-id="49c8f-312">When I look at ACLs in the Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="49c8f-313">Entries in the ACLs are stored as GUIDs that correspond to users in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49c8f-313">Entries in the ACLs are stored as GUIDs that correspond to users in Azure AD.</span></span> <span data-ttu-id="49c8f-314">The APIs return the GUIDs as is.</span><span class="sxs-lookup"><span data-stu-id="49c8f-314">The APIs return the GUIDs as is.</span></span> <span data-ttu-id="49c8f-315">The Azure portal tries to make ACLs easier to use by translating the GUIDs into friendly names when possible.</span><span class="sxs-lookup"><span data-stu-id="49c8f-315">The Azure portal tries to make ACLs easier to use by translating the GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-the-acls-when-im-using-the-azure-portal"></a><span data-ttu-id="49c8f-316">Why do I sometimes see GUIDs in the ACLs when I'm using the Azure portal?</span><span class="sxs-lookup"><span data-stu-id="49c8f-316">Why do I sometimes see GUIDs in the ACLs when I'm using the Azure portal?</span></span>

<span data-ttu-id="49c8f-317">A GUID is shown when the user doesn't exist in Azure AD anymore.</span><span class="sxs-lookup"><span data-stu-id="49c8f-317">A GUID is shown when the user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="49c8f-318">Usually this happens when the user has left the company or if their account has been deleted in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49c8f-318">Usually this happens when the user has left the company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="49c8f-319">Does Data Lake Store support inheritance of ACLs?</span><span class="sxs-lookup"><span data-stu-id="49c8f-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="49c8f-320">No.</span><span class="sxs-lookup"><span data-stu-id="49c8f-320">No.</span></span>

### <a name="what-is-the-difference-between-mask-and-umask"></a><span data-ttu-id="49c8f-321">What is the difference between mask and umask?</span><span class="sxs-lookup"><span data-stu-id="49c8f-321">What is the difference between mask and umask?</span></span>

| <span data-ttu-id="49c8f-322">mask</span><span class="sxs-lookup"><span data-stu-id="49c8f-322">mask</span></span> | <span data-ttu-id="49c8f-323">umask</span><span class="sxs-lookup"><span data-stu-id="49c8f-323">umask</span></span>|
|------|------|
| <span data-ttu-id="49c8f-324">The **mask** property is available on every file and folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-324">The **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="49c8f-325">The **umask** is a property of the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="49c8f-325">The **umask** is a property of the Data Lake Store account.</span></span> <span data-ttu-id="49c8f-326">So there is only a single umask in the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49c8f-326">So there is only a single umask in the Data Lake Store.</span></span>    |
| <span data-ttu-id="49c8f-327">The mask property on a file or folder can be altered by the owning user or owning group of a file or a super-user.</span><span class="sxs-lookup"><span data-stu-id="49c8f-327">The mask property on a file or folder can be altered by the owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="49c8f-328">The umask property cannot be modified by any user, even a super-user.</span><span class="sxs-lookup"><span data-stu-id="49c8f-328">The umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="49c8f-329">It is an unchangeable, constant value.</span><span class="sxs-lookup"><span data-stu-id="49c8f-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="49c8f-330">The mask property is used during the access check algorithm at runtime to determine whether a user has the right to perform on operation on a file or folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-330">The mask property is used during the access check algorithm at runtime to determine whether a user has the right to perform on operation on a file or folder.</span></span> <span data-ttu-id="49c8f-331">The role of the mask is to create "effective permissions" at the time of access check.</span><span class="sxs-lookup"><span data-stu-id="49c8f-331">The role of the mask is to create "effective permissions" at the time of access check.</span></span> | <span data-ttu-id="49c8f-332">The umask is not used during access check at all.</span><span class="sxs-lookup"><span data-stu-id="49c8f-332">The umask is not used during access check at all.</span></span> <span data-ttu-id="49c8f-333">The umask is used to determine the Access ACL of new child items of a folder.</span><span class="sxs-lookup"><span data-stu-id="49c8f-333">The umask is used to determine the Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="49c8f-334">The mask is a 3-bit RWX value that applies to named user, named group, and owning user at the time of access check.</span><span class="sxs-lookup"><span data-stu-id="49c8f-334">The mask is a 3-bit RWX value that applies to named user, named group, and owning user at the time of access check.</span></span>| <span data-ttu-id="49c8f-335">The umask is a 9-bit value that applies to the owning user, owning group, and **other** of a new child.</span><span class="sxs-lookup"><span data-stu-id="49c8f-335">The umask is a 9-bit value that applies to the owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="49c8f-336">Where can I learn more about POSIX access control model?</span><span class="sxs-lookup"><span data-stu-id="49c8f-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="49c8f-337">POSIX Access Control Lists on Linux</span><span class="sxs-lookup"><span data-stu-id="49c8f-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="49c8f-338">HDFS permission guide</span><span class="sxs-lookup"><span data-stu-id="49c8f-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="49c8f-339">POSIX FAQ</span><span class="sxs-lookup"><span data-stu-id="49c8f-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="49c8f-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="49c8f-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="49c8f-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="49c8f-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="49c8f-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="49c8f-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="49c8f-343">POSIX ACL on Ubuntu</span><span class="sxs-lookup"><span data-stu-id="49c8f-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="49c8f-344">ACL using access control lists on Linux</span><span class="sxs-lookup"><span data-stu-id="49c8f-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="49c8f-345">See also</span><span class="sxs-lookup"><span data-stu-id="49c8f-345">See also</span></span>

* [<span data-ttu-id="49c8f-346">Overview of Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49c8f-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
















