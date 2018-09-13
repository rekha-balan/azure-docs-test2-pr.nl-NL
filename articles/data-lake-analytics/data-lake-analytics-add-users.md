---
title: Add users to an Azure Data Lake Analytics account
description: Learn how to correctly add users to your Data Lake Analytics account
services: data-lake-analytics
ms.service: data-lake-analytics
author: saveenr
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: db35f16e-1565-4873-a851-bd987accdc58
ms.topic: conceptual
ms.date: 05/24/2018
ms.openlocfilehash: 0386406f5fc81a007d55bd5358e7a6b333f63b04
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856716"
---
# <a name="adding-a-user-in-the-azure-portal"></a><span data-ttu-id="b52ea-103">Adding a user in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b52ea-103">Adding a user in the Azure portal</span></span>

## <a name="start-the-add-user-wizard"></a><span data-ttu-id="b52ea-104">Start the Add User Wizard</span><span class="sxs-lookup"><span data-stu-id="b52ea-104">Start the Add User Wizard</span></span>
1. <span data-ttu-id="b52ea-105">Open your Azure Data Lake Analytics via https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b52ea-105">Open your Azure Data Lake Analytics via https://portal.azure.com.</span></span>
2. <span data-ttu-id="b52ea-106">Click **Add User Wizard**.</span><span class="sxs-lookup"><span data-stu-id="b52ea-106">Click **Add User Wizard**.</span></span>
3. <span data-ttu-id="b52ea-107">In the **Select user** step, find the user you want to add.</span><span class="sxs-lookup"><span data-stu-id="b52ea-107">In the **Select user** step, find the user you want to add.</span></span> <span data-ttu-id="b52ea-108">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b52ea-108">Click **Select**.</span></span>
4. <span data-ttu-id="b52ea-109">the **Select role** step, pick **Data Lake Analytics Developer**.</span><span class="sxs-lookup"><span data-stu-id="b52ea-109">the **Select role** step, pick **Data Lake Analytics Developer**.</span></span> <span data-ttu-id="b52ea-110">This role has the minimum set of permissions required to submit/monitor/manage U-SQL jobs.</span><span class="sxs-lookup"><span data-stu-id="b52ea-110">This role has the minimum set of permissions required to submit/monitor/manage U-SQL jobs.</span></span> <span data-ttu-id="b52ea-111">Assign to this role if the group is not intended for managing Azure services.</span><span class="sxs-lookup"><span data-stu-id="b52ea-111">Assign to this role if the group is not intended for managing Azure services.</span></span>
5. <span data-ttu-id="b52ea-112">In the **Select catalog permissions** step, select any additional databases that user will need access to.</span><span class="sxs-lookup"><span data-stu-id="b52ea-112">In the **Select catalog permissions** step, select any additional databases that user will need access to.</span></span> <span data-ttu-id="b52ea-113">Read and Write Access to the master database is required to submit jobs.</span><span class="sxs-lookup"><span data-stu-id="b52ea-113">Read and Write Access to the master database is required to submit jobs.</span></span> <span data-ttu-id="b52ea-114">When you are done, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b52ea-114">When you are done, click **OK**.</span></span>
6. <span data-ttu-id="b52ea-115">In the final step called **Assign selected permissions** review the changes the wizard will make.</span><span class="sxs-lookup"><span data-stu-id="b52ea-115">In the final step called **Assign selected permissions** review the changes the wizard will make.</span></span> <span data-ttu-id="b52ea-116">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b52ea-116">Click **OK**.</span></span>


## <a name="configure-acls-for-data-folders"></a><span data-ttu-id="b52ea-117">Configure ACLs for data folders</span><span class="sxs-lookup"><span data-stu-id="b52ea-117">Configure ACLs for data folders</span></span>
<span data-ttu-id="b52ea-118">Grant "R-X" or "RWX", as needed, on folders containing input data and output data.</span><span class="sxs-lookup"><span data-stu-id="b52ea-118">Grant "R-X" or "RWX", as needed, on folders containing input data and output data.</span></span>


## <a name="optionally-add-the-user-to-the-azure-data-lake-store-role-reader-role"></a><span data-ttu-id="b52ea-119">Optionally, add the user to the Azure Data Lake Store role **Reader** role.</span><span class="sxs-lookup"><span data-stu-id="b52ea-119">Optionally, add the user to the Azure Data Lake Store role **Reader** role.</span></span>
1.  <span data-ttu-id="b52ea-120">Find your Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="b52ea-120">Find your Azure Data Lake Store account.</span></span>
2.  <span data-ttu-id="b52ea-121">Click on **Users**.</span><span class="sxs-lookup"><span data-stu-id="b52ea-121">Click on **Users**.</span></span>
3. <span data-ttu-id="b52ea-122">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b52ea-122">Click **Add**.</span></span>
4.  <span data-ttu-id="b52ea-123">Select an Azure RBAC Role to assign this group.</span><span class="sxs-lookup"><span data-stu-id="b52ea-123">Select an Azure RBAC Role to assign this group.</span></span>
5.  <span data-ttu-id="b52ea-124">Assign to Reader role.</span><span class="sxs-lookup"><span data-stu-id="b52ea-124">Assign to Reader role.</span></span> <span data-ttu-id="b52ea-125">This role has the minimum set of permissions required to browse/manage data stored in ADLS.</span><span class="sxs-lookup"><span data-stu-id="b52ea-125">This role has the minimum set of permissions required to browse/manage data stored in ADLS.</span></span> <span data-ttu-id="b52ea-126">Assign to this role if the Group is not intended for managing Azure services.</span><span class="sxs-lookup"><span data-stu-id="b52ea-126">Assign to this role if the Group is not intended for managing Azure services.</span></span>
6.  <span data-ttu-id="b52ea-127">Type in the name of the Group.</span><span class="sxs-lookup"><span data-stu-id="b52ea-127">Type in the name of the Group.</span></span>
7.  <span data-ttu-id="b52ea-128">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b52ea-128">Click **OK**.</span></span>

## <a name="adding-a-user-using-powershell"></a><span data-ttu-id="b52ea-129">Adding a user using PowerShell</span><span class="sxs-lookup"><span data-stu-id="b52ea-129">Adding a user using PowerShell</span></span>

1. <span data-ttu-id="b52ea-130">Follow the instructions in this guide: [How to install and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="b52ea-130">Follow the instructions in this guide: [How to install and configure Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="b52ea-131">Download the [Add-AdlaJobUser.ps1](https://github.com/Azure/AzureDataLake/blob/master/Samples/PowerShell/ADLAUsers/Add-AdlaJobUser.ps1) PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="b52ea-131">Download the [Add-AdlaJobUser.ps1](https://github.com/Azure/AzureDataLake/blob/master/Samples/PowerShell/ADLAUsers/Add-AdlaJobUser.ps1) PowerShell script.</span></span>
3. <span data-ttu-id="b52ea-132">Run the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="b52ea-132">Run the PowerShell script.</span></span> 

<span data-ttu-id="b52ea-133">The sample command to give user access to submit jobs, view new job metadata, and view old metadata is:</span><span class="sxs-lookup"><span data-stu-id="b52ea-133">The sample command to give user access to submit jobs, view new job metadata, and view old metadata is:</span></span>

`Add-AdlaJobUser.ps1 -Account myadlsaccount -EntityToAdd 546e153e-0ecf-417b-ab7f-aa01ce4a7bff -EntityType User -FullReplication`


## <a name="next-steps"></a><span data-ttu-id="b52ea-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="b52ea-134">Next steps</span></span>

* [<span data-ttu-id="b52ea-135">Overview of Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b52ea-135">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="b52ea-136">Get started with Data Lake Analytics by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b52ea-136">Get started with Data Lake Analytics by using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="b52ea-137">Manage Azure Data Lake Analytics by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b52ea-137">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

