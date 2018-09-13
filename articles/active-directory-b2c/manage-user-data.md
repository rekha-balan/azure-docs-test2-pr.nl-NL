---
title: Manage user data in Azure Active Directory B2C | Microsoft Docs
description: Learn how to delete or export user data in Azure AD B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 05/06/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 49e9efa537ad1f2a1d7f06dd7f8a68a409c7d4e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869879"
---
# <a name="manage-user-data-in-azure-active-directory-b2c"></a><span data-ttu-id="6f81d-103">Manage user data in Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="6f81d-103">Manage user data in Azure Active Directory B2C</span></span>

 <span data-ttu-id="6f81d-104">This article discusses how you can manage the user data in Azure Active Directory (Azure AD) B2C by using the operations that are provided by the [Azure Active Directory Graph API](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="6f81d-104">This article discusses how you can manage the user data in Azure Active Directory (Azure AD) B2C by using the operations that are provided by the [Azure Active Directory Graph API](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span> <span data-ttu-id="6f81d-105">Managing user data includes deleting or exporting data from audit logs.</span><span class="sxs-lookup"><span data-stu-id="6f81d-105">Managing user data includes deleting or exporting data from audit logs.</span></span>

[!INCLUDE [gdpr-intro-sentence.md](../../includes/gdpr-intro-sentence.md)]

## <a name="delete-user-data"></a><span data-ttu-id="6f81d-106">Delete user data</span><span class="sxs-lookup"><span data-stu-id="6f81d-106">Delete user data</span></span>

<span data-ttu-id="6f81d-107">User data is stored in the Azure AD B2C directory and in the audit logs.</span><span class="sxs-lookup"><span data-stu-id="6f81d-107">User data is stored in the Azure AD B2C directory and in the audit logs.</span></span> <span data-ttu-id="6f81d-108">All user audit data is retained for 30 days in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6f81d-108">All user audit data is retained for 30 days in Azure AD B2C.</span></span> <span data-ttu-id="6f81d-109">If you want to delete user data within that 30-day period, you can use the [Delete a user](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#DeleteUser) operation.</span><span class="sxs-lookup"><span data-stu-id="6f81d-109">If you want to delete user data within that 30-day period, you can use the [Delete a user](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#DeleteUser) operation.</span></span> <span data-ttu-id="6f81d-110">A DELETE operation is required for each of the Azure AD B2C tenants where data might reside.</span><span class="sxs-lookup"><span data-stu-id="6f81d-110">A DELETE operation is required for each of the Azure AD B2C tenants where data might reside.</span></span> 

<span data-ttu-id="6f81d-111">Every user in Azure AD B2C is assigned an object ID.</span><span class="sxs-lookup"><span data-stu-id="6f81d-111">Every user in Azure AD B2C is assigned an object ID.</span></span> <span data-ttu-id="6f81d-112">The object ID provides an unambiguous identifier for you to use to delete user data in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6f81d-112">The object ID provides an unambiguous identifier for you to use to delete user data in Azure AD B2C.</span></span> <span data-ttu-id="6f81d-113">Depending on your architecture, the object ID can be a useful correlation identifier across other services, such as financial, marketing, and customer relationship management databases.</span><span class="sxs-lookup"><span data-stu-id="6f81d-113">Depending on your architecture, the object ID can be a useful correlation identifier across other services, such as financial, marketing, and customer relationship management databases.</span></span> 

<span data-ttu-id="6f81d-114">The most accurate way to get the object ID for a user is to obtain it as part of an authentication journey with Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6f81d-114">The most accurate way to get the object ID for a user is to obtain it as part of an authentication journey with Azure AD B2C.</span></span> <span data-ttu-id="6f81d-115">If you receive a valid request for data from a user by using other methods, an offline process, such as a search by a customer service support agent, might be necessary to find the user and note the associated object ID.</span><span class="sxs-lookup"><span data-stu-id="6f81d-115">If you receive a valid request for data from a user by using other methods, an offline process, such as a search by a customer service support agent, might be necessary to find the user and note the associated object ID.</span></span> 

<span data-ttu-id="6f81d-116">The following example shows a possible data-deletion flow:</span><span class="sxs-lookup"><span data-stu-id="6f81d-116">The following example shows a possible data-deletion flow:</span></span>

1. <span data-ttu-id="6f81d-117">The user signs in and selects **Delete my data**.</span><span class="sxs-lookup"><span data-stu-id="6f81d-117">The user signs in and selects **Delete my data**.</span></span>
2. <span data-ttu-id="6f81d-118">The application offers an option to delete the data within an administration section of the application.</span><span class="sxs-lookup"><span data-stu-id="6f81d-118">The application offers an option to delete the data within an administration section of the application.</span></span>
3. <span data-ttu-id="6f81d-119">The application forces an authentication to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6f81d-119">The application forces an authentication to Azure AD B2C.</span></span> <span data-ttu-id="6f81d-120">Azure AD B2C provides a token with the object ID of the user back to the application.</span><span class="sxs-lookup"><span data-stu-id="6f81d-120">Azure AD B2C provides a token with the object ID of the user back to the application.</span></span> 
4. <span data-ttu-id="6f81d-121">The token is received by the application, and the object ID is used to delete the user data through a call to the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="6f81d-121">The token is received by the application, and the object ID is used to delete the user data through a call to the Azure AD Graph API.</span></span> <span data-ttu-id="6f81d-122">The Azure AD Graph API deletes the user data and returns a status code of 200 OK.</span><span class="sxs-lookup"><span data-stu-id="6f81d-122">The Azure AD Graph API deletes the user data and returns a status code of 200 OK.</span></span>
5. <span data-ttu-id="6f81d-123">The application orchestrates the deletion of user data in other organizational systems as needed by using the object ID or other identifiers.</span><span class="sxs-lookup"><span data-stu-id="6f81d-123">The application orchestrates the deletion of user data in other organizational systems as needed by using the object ID or other identifiers.</span></span>
6. <span data-ttu-id="6f81d-124">The application confirms the deletion of data and provides next steps to the user.</span><span class="sxs-lookup"><span data-stu-id="6f81d-124">The application confirms the deletion of data and provides next steps to the user.</span></span>

## <a name="export-customer-data"></a><span data-ttu-id="6f81d-125">Export customer data</span><span class="sxs-lookup"><span data-stu-id="6f81d-125">Export customer data</span></span>

<span data-ttu-id="6f81d-126">The process of exporting customer data from Azure AD B2C is similar to the deletion process.</span><span class="sxs-lookup"><span data-stu-id="6f81d-126">The process of exporting customer data from Azure AD B2C is similar to the deletion process.</span></span>

<span data-ttu-id="6f81d-127">Azure AD B2C user data is limited to:</span><span class="sxs-lookup"><span data-stu-id="6f81d-127">Azure AD B2C user data is limited to:</span></span>

- <span data-ttu-id="6f81d-128">**Data stored in the Azure Active Directory**: You can retrieve data in an Azure AD B2C authentication user journey by using the object ID or any sign-in name, such as an email address or username.</span><span class="sxs-lookup"><span data-stu-id="6f81d-128">**Data stored in the Azure Active Directory**: You can retrieve data in an Azure AD B2C authentication user journey by using the object ID or any sign-in name, such as an email address or username.</span></span> 
- <span data-ttu-id="6f81d-129">**User-specific audit events report**: You can index data by using the object ID.</span><span class="sxs-lookup"><span data-stu-id="6f81d-129">**User-specific audit events report**: You can index data by using the object ID.</span></span>

<span data-ttu-id="6f81d-130">In the following example of an export data flow, the steps that are described as being performed by the application can also be performed by either a backend process or a user with an administrator role in the directory:</span><span class="sxs-lookup"><span data-stu-id="6f81d-130">In the following example of an export data flow, the steps that are described as being performed by the application can also be performed by either a backend process or a user with an administrator role in the directory:</span></span>

1. <span data-ttu-id="6f81d-131">The user signs in to the application.</span><span class="sxs-lookup"><span data-stu-id="6f81d-131">The user signs in to the application.</span></span> <span data-ttu-id="6f81d-132">Azure AD B2C enforces authentication with Azure Multi-Factor Authentication if needed.</span><span class="sxs-lookup"><span data-stu-id="6f81d-132">Azure AD B2C enforces authentication with Azure Multi-Factor Authentication if needed.</span></span>
2. <span data-ttu-id="6f81d-133">The application uses the user credentials to call an Azure AD Graph API operation to retrieve the user attributes.</span><span class="sxs-lookup"><span data-stu-id="6f81d-133">The application uses the user credentials to call an Azure AD Graph API operation to retrieve the user attributes.</span></span> <span data-ttu-id="6f81d-134">The Azure AD Graph API provides the attribute data in JSON format.</span><span class="sxs-lookup"><span data-stu-id="6f81d-134">The Azure AD Graph API provides the attribute data in JSON format.</span></span> <span data-ttu-id="6f81d-135">Depending on the schema, you can set the ID token contents to include all personal data about a user.</span><span class="sxs-lookup"><span data-stu-id="6f81d-135">Depending on the schema, you can set the ID token contents to include all personal data about a user.</span></span>
3. <span data-ttu-id="6f81d-136">The application retrieves the user audit activity.</span><span class="sxs-lookup"><span data-stu-id="6f81d-136">The application retrieves the user audit activity.</span></span> <span data-ttu-id="6f81d-137">The Azure AD Graph API provides the event data to the application.</span><span class="sxs-lookup"><span data-stu-id="6f81d-137">The Azure AD Graph API provides the event data to the application.</span></span>
4. <span data-ttu-id="6f81d-138">The application aggregates the data and makes it available to the user.</span><span class="sxs-lookup"><span data-stu-id="6f81d-138">The application aggregates the data and makes it available to the user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f81d-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f81d-139">Next steps</span></span>

- <span data-ttu-id="6f81d-140">To learn how to manage how users access your application, see [Manage user access](manage-user-access.md).</span><span class="sxs-lookup"><span data-stu-id="6f81d-140">To learn how to manage how users access your application, see [Manage user access](manage-user-access.md).</span></span>




