---
title: Secure Azure Data Lake Analytics for multiple users
description: Learn how to configure multiple users to run jobs in Azure Data Lake Analytics.
ms.service: data-lake-analytics
services: data-lake-analytics
author: matt1883
ms.author: mahi
ms.reviewer: jasonwhowell
ms.topic: conceptual
ms.date: 05/30/2018
ms.openlocfilehash: c6b86e25602f36896855d2593952609904396879
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870757"
---
# <a name="configure-user-access-to-job-information-to-job-information-in-azure-data-lake-analytics"></a><span data-ttu-id="99985-103">Configure user access to job information to job information in Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="99985-103">Configure user access to job information to job information in Azure Data Lake Analytics</span></span> 

<span data-ttu-id="99985-104">In Azure Data Lake Analytics, you can use multiple user accounts or service principals to run jobs.</span><span class="sxs-lookup"><span data-stu-id="99985-104">In Azure Data Lake Analytics, you can use multiple user accounts or service principals to run jobs.</span></span> 

<span data-ttu-id="99985-105">In order for those same users to see the detailed job information, the users need to be able to read the contents of the job folders.</span><span class="sxs-lookup"><span data-stu-id="99985-105">In order for those same users to see the detailed job information, the users need to be able to read the contents of the job folders.</span></span> <span data-ttu-id="99985-106">The job folders are located in `/system/` directory.</span><span class="sxs-lookup"><span data-stu-id="99985-106">The job folders are located in `/system/` directory.</span></span> 

<span data-ttu-id="99985-107">If the necessary permissions are not configured, the user may see an error: `Graph data not available - You don't have permissions to access the graph data.`</span><span class="sxs-lookup"><span data-stu-id="99985-107">If the necessary permissions are not configured, the user may see an error: `Graph data not available - You don't have permissions to access the graph data.`</span></span> 

## <a name="configure-user-access-to-job-information"></a><span data-ttu-id="99985-108">Configure user access to job information</span><span class="sxs-lookup"><span data-stu-id="99985-108">Configure user access to job information</span></span>

<span data-ttu-id="99985-109">You can use the **Add User Wizard** to configure the ACLs on the folders.</span><span class="sxs-lookup"><span data-stu-id="99985-109">You can use the **Add User Wizard** to configure the ACLs on the folders.</span></span> <span data-ttu-id="99985-110">For more information, see [Add a new user](data-lake-analytics-manage-use-portal.md#add-a-new-user).</span><span class="sxs-lookup"><span data-stu-id="99985-110">For more information, see [Add a new user](data-lake-analytics-manage-use-portal.md#add-a-new-user).</span></span>

<span data-ttu-id="99985-111">If you need more granular control, or need to script the permissions, then secure the folders as follows:</span><span class="sxs-lookup"><span data-stu-id="99985-111">If you need more granular control, or need to script the permissions, then secure the folders as follows:</span></span>

1. <span data-ttu-id="99985-112">Grant **execute** permissions (via an access ACL) on the root folder:</span><span class="sxs-lookup"><span data-stu-id="99985-112">Grant **execute** permissions (via an access ACL) on the root folder:</span></span>
   - /
   
2. <span data-ttu-id="99985-113">Grant **execute** and **read** permissions (via an access ACL and a default ACL) on the folders that contain the job folders.</span><span class="sxs-lookup"><span data-stu-id="99985-113">Grant **execute** and **read** permissions (via an access ACL and a default ACL) on the folders that contain the job folders.</span></span> <span data-ttu-id="99985-114">For example, for a specific job that ran on May 25, 2018, these folders need to be accessed:</span><span class="sxs-lookup"><span data-stu-id="99985-114">For example, for a specific job that ran on May 25, 2018, these folders need to be accessed:</span></span>
   - <span data-ttu-id="99985-115">/system</span><span class="sxs-lookup"><span data-stu-id="99985-115">/system</span></span>
   - <span data-ttu-id="99985-116">/system/jobservice</span><span class="sxs-lookup"><span data-stu-id="99985-116">/system/jobservice</span></span>
   - <span data-ttu-id="99985-117">/system/jobservice/jobs</span><span class="sxs-lookup"><span data-stu-id="99985-117">/system/jobservice/jobs</span></span>
   - <span data-ttu-id="99985-118">/system/jobservice/jobs/Usql</span><span class="sxs-lookup"><span data-stu-id="99985-118">/system/jobservice/jobs/Usql</span></span>
   - <span data-ttu-id="99985-119">/system/jobservice/jobs/Usql/2018</span><span class="sxs-lookup"><span data-stu-id="99985-119">/system/jobservice/jobs/Usql/2018</span></span>
   - <span data-ttu-id="99985-120">/system/jobservice/jobs/Usql/2018/05</span><span class="sxs-lookup"><span data-stu-id="99985-120">/system/jobservice/jobs/Usql/2018/05</span></span>
   - <span data-ttu-id="99985-121">/system/jobservice/jobs/Usql/2018/05/25</span><span class="sxs-lookup"><span data-stu-id="99985-121">/system/jobservice/jobs/Usql/2018/05/25</span></span>
   - <span data-ttu-id="99985-122">/system/jobservice/jobs/Usql/2018/05/25/11</span><span class="sxs-lookup"><span data-stu-id="99985-122">/system/jobservice/jobs/Usql/2018/05/25/11</span></span>
   - <span data-ttu-id="99985-123">/system/jobservice/jobs/Usql/2018/05/25/11/01</span><span class="sxs-lookup"><span data-stu-id="99985-123">/system/jobservice/jobs/Usql/2018/05/25/11/01</span></span>
   - <span data-ttu-id="99985-124">/system/jobservice/jobs/Usql/2018/05/25/11/01/b074bd7a-1448-d879-9d75-f562b101bd3d</span><span class="sxs-lookup"><span data-stu-id="99985-124">/system/jobservice/jobs/Usql/2018/05/25/11/01/b074bd7a-1448-d879-9d75-f562b101bd3d</span></span>

## <a name="next-steps"></a><span data-ttu-id="99985-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="99985-125">Next steps</span></span>
[<span data-ttu-id="99985-126">Add a new user</span><span class="sxs-lookup"><span data-stu-id="99985-126">Add a new user</span></span>](data-lake-analytics-manage-use-portal.md#add-a-new-user)
