---
title: Add a service principal to Azure Analysis Services server admin role | Microsoft Docs
description: Learn how to add an automation service principal to the server admin role
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 779a202fccd3ff56c174ebc1ebbf3c4adfdd8c7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857021"
---
# <a name="add-a-service-principal-to-the-server-administrator-role"></a><span data-ttu-id="3491f-103">Add a service principal to the server administrator role</span><span class="sxs-lookup"><span data-stu-id="3491f-103">Add a service principal to the server administrator role</span></span> 

 <span data-ttu-id="3491f-104">To automate unattended PowerShell tasks, a service principal must have **server administrator** privileges on the Analysis Services server being managed.</span><span class="sxs-lookup"><span data-stu-id="3491f-104">To automate unattended PowerShell tasks, a service principal must have **server administrator** privileges on the Analysis Services server being managed.</span></span> <span data-ttu-id="3491f-105">This article describes how to add a service principal to the server administrators role on an Azure AS server.</span><span class="sxs-lookup"><span data-stu-id="3491f-105">This article describes how to add a service principal to the server administrators role on an Azure AS server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3491f-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="3491f-106">Before you begin</span></span>
<span data-ttu-id="3491f-107">Before completing this task, you must have a service principal registered in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3491f-107">Before completing this task, you must have a service principal registered in Azure Active Directory.</span></span>

<span data-ttu-id="3491f-108">[Create service principal - Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) </span><span class="sxs-lookup"><span data-stu-id="3491f-108">[Create service principal - Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) </span></span>  
[<span data-ttu-id="3491f-109">Create service principal - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3491f-109">Create service principal - PowerShell</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="required-permissions"></a><span data-ttu-id="3491f-110">Required permissions</span><span class="sxs-lookup"><span data-stu-id="3491f-110">Required permissions</span></span>
<span data-ttu-id="3491f-111">To complete this task, you must have [server administrator](analysis-services-server-admins.md) permissions on the Azure AS server.</span><span class="sxs-lookup"><span data-stu-id="3491f-111">To complete this task, you must have [server administrator](analysis-services-server-admins.md) permissions on the Azure AS server.</span></span> 

## <a name="add-service-principal-to-server-administrators-role"></a><span data-ttu-id="3491f-112">Add service principal to server administrators role</span><span class="sxs-lookup"><span data-stu-id="3491f-112">Add service principal to server administrators role</span></span>

1. <span data-ttu-id="3491f-113">In SSMS, connect to your Azure AS server.</span><span class="sxs-lookup"><span data-stu-id="3491f-113">In SSMS, connect to your Azure AS server.</span></span>
2. <span data-ttu-id="3491f-114">In **Server Properties** > **Security**, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3491f-114">In **Server Properties** > **Security**, click **Add**.</span></span>
3. <span data-ttu-id="3491f-115">In **Select a User or Group**, search for your registered app by name, select, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3491f-115">In **Select a User or Group**, search for your registered app by name, select, and then click **Add**.</span></span>

    ![Search for service principal account](./media/analysis-services-addservprinc-admins/aas-add-sp-ssms-picker.png)

4. <span data-ttu-id="3491f-117">Verify the service principal account ID, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3491f-117">Verify the service principal account ID, and then click **OK**.</span></span>
    
    ![Search for service principal account](./media/analysis-services-addservprinc-admins/aas-add-sp-ssms-add.png)


> [!NOTE]
> <span data-ttu-id="3491f-119">For server operations using AzureRm cmdlets, service principal running scheduler must also belong to the **Owner** role for the resource in [Azure Role-Based Access Control (RBAC)](../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="3491f-119">For server operations using AzureRm cmdlets, service principal running scheduler must also belong to the **Owner** role for the resource in [Azure Role-Based Access Control (RBAC)](../role-based-access-control/overview.md).</span></span> 

## <a name="related-information"></a><span data-ttu-id="3491f-120">Related information</span><span class="sxs-lookup"><span data-stu-id="3491f-120">Related information</span></span>

* [<span data-ttu-id="3491f-121">Download SQL Server PowerShell Module</span><span class="sxs-lookup"><span data-stu-id="3491f-121">Download SQL Server PowerShell Module</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [<span data-ttu-id="3491f-122">Download SSMS</span><span class="sxs-lookup"><span data-stu-id="3491f-122">Download SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   


