---
title: Manage server admins in Azure Analysis Services | Microsoft Docs
description: Learn how to manage server admins for an Analysis Services server in Azure.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 06/20/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 9d8f74bd66fc7c980c4fc5f83492aad7d8a4aa5c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866803"
---
# <a name="manage-server-administrators"></a><span data-ttu-id="454d4-103">Manage server administrators</span><span class="sxs-lookup"><span data-stu-id="454d4-103">Manage server administrators</span></span>
<span data-ttu-id="454d4-104">Server administrators must be a valid user or security group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span><span class="sxs-lookup"><span data-stu-id="454d4-104">Server administrators must be a valid user or security group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="454d4-105">You can use **Analysis Services Admins** for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span><span class="sxs-lookup"><span data-stu-id="454d4-105">You can use **Analysis Services Admins** for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

> [!NOTE]
> <span data-ttu-id="454d4-106">Security groups must have the `MailEnabled` property set to `True`.</span><span class="sxs-lookup"><span data-stu-id="454d4-106">Security groups must have the `MailEnabled` property set to `True`.</span></span>

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="454d4-107">To add server administrators by using Azure portal</span><span class="sxs-lookup"><span data-stu-id="454d4-107">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="454d4-108">In the portal, for your server, click **Analysis Services Admins**.</span><span class="sxs-lookup"><span data-stu-id="454d4-108">In the portal, for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="454d4-109">In **\<servername> - Analysis Services Admins**, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="454d4-109">In **\<servername> - Analysis Services Admins**, click **Add**.</span></span>
3. <span data-ttu-id="454d4-110">In **Add Server Administrators**, select user accounts from your Azure AD or invite external users by email address.</span><span class="sxs-lookup"><span data-stu-id="454d4-110">In **Add Server Administrators**, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Server Admins in Azure portal](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="454d4-112">To add server administrators by using SSMS</span><span class="sxs-lookup"><span data-stu-id="454d4-112">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="454d4-113">Right-click the server > **Properties**.</span><span class="sxs-lookup"><span data-stu-id="454d4-113">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="454d4-114">In **Analysis Server Properties**, click **Security**.</span><span class="sxs-lookup"><span data-stu-id="454d4-114">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="454d4-115">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="454d4-115">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![Add server administrators in SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="454d4-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="454d4-117">Next steps</span></span> 
[<span data-ttu-id="454d4-118">Authentication and user permissions</span><span class="sxs-lookup"><span data-stu-id="454d4-118">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="454d4-119">Manage database roles and users</span><span class="sxs-lookup"><span data-stu-id="454d4-119">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="454d4-120">Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="454d4-120">Role-Based Access Control</span></span>](../role-based-access-control/overview.md)  

