---
title: No working connector group found for an Application Proxy application | Microsoft Docs
description: Address problems you might encounter when there is no working Connector in a Connector Group for your application with the Azure AD Application Proxy
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: baaf7bbb83ff600045e95cd16206fbfff9fce1c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856677"
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="172fe-103">No working connector group found for an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="172fe-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="172fe-104">This article helps to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172fe-104">This article helps to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="172fe-105">Overview of steps</span><span class="sxs-lookup"><span data-stu-id="172fe-105">Overview of steps</span></span>
<span data-ttu-id="172fe-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span><span class="sxs-lookup"><span data-stu-id="172fe-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="172fe-107">If you have no connectors in the group, you can:</span><span class="sxs-lookup"><span data-stu-id="172fe-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="172fe-108">Download a new Connector on the right on-prem server, and assign it to this group</span><span class="sxs-lookup"><span data-stu-id="172fe-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="172fe-109">Move an active Connector into the group</span><span class="sxs-lookup"><span data-stu-id="172fe-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="172fe-110">If you have no active connectors in the group, you can:</span><span class="sxs-lookup"><span data-stu-id="172fe-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="172fe-111">Identify the reason your Connector is inactive and resolve</span><span class="sxs-lookup"><span data-stu-id="172fe-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="172fe-112">Move an active Connector into the group</span><span class="sxs-lookup"><span data-stu-id="172fe-112">Move an active Connector into the group</span></span>

<span data-ttu-id="172fe-113">To figure out the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span><span class="sxs-lookup"><span data-stu-id="172fe-113">To figure out the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="172fe-114">If there are no connectors in the group, the warning message specifies the group needs at least one Connector.</span><span class="sxs-lookup"><span data-stu-id="172fe-114">If there are no connectors in the group, the warning message specifies the group needs at least one Connector.</span></span> <span data-ttu-id="172fe-115">If you have no active Connectors, the warning message explains that.</span><span class="sxs-lookup"><span data-stu-id="172fe-115">If you have no active Connectors, the warning message explains that.</span></span> <span data-ttu-id="172fe-116">It is common to have inactive Connectors.</span><span class="sxs-lookup"><span data-stu-id="172fe-116">It is common to have inactive Connectors.</span></span> 

   ![Connector group selection in Azure portal](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="172fe-118">For details on each of these options, see the corresponding section below.</span><span class="sxs-lookup"><span data-stu-id="172fe-118">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="172fe-119">The instructions assume that you are starting from the Connector management page.</span><span class="sxs-lookup"><span data-stu-id="172fe-119">The instructions assume that you are starting from the Connector management page.</span></span> <span data-ttu-id="172fe-120">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span><span class="sxs-lookup"><span data-stu-id="172fe-120">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="172fe-121">You can also get to the page by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span><span class="sxs-lookup"><span data-stu-id="172fe-121">You can also get to the page by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Connector group management in Azure portal](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="172fe-123">Download a new Connector</span><span class="sxs-lookup"><span data-stu-id="172fe-123">Download a new Connector</span></span>

<span data-ttu-id="172fe-124">To download a new Connector, use the “Download Connector” button at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="172fe-124">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="172fe-125">Install the connector on a machine with direct line of sight to the backend application.</span><span class="sxs-lookup"><span data-stu-id="172fe-125">Install the connector on a machine with direct line of sight to the backend application.</span></span> <span data-ttu-id="172fe-126">Typically, the connector is installed on the same server as the application.</span><span class="sxs-lookup"><span data-stu-id="172fe-126">Typically, the connector is installed on the same server as the application.</span></span> <span data-ttu-id="172fe-127">After downloading, the Connector should appear in this menu.</span><span class="sxs-lookup"><span data-stu-id="172fe-127">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="172fe-128">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span><span class="sxs-lookup"><span data-stu-id="172fe-128">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="172fe-129">Save the change.</span><span class="sxs-lookup"><span data-stu-id="172fe-129">Save the change.</span></span>

   ![Download the connector from the Azure portal](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="172fe-131">Move an Active Connector</span><span class="sxs-lookup"><span data-stu-id="172fe-131">Move an Active Connector</span></span>

<span data-ttu-id="172fe-132">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span><span class="sxs-lookup"><span data-stu-id="172fe-132">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="172fe-133">To do so, click the Connector.</span><span class="sxs-lookup"><span data-stu-id="172fe-133">To do so, click the Connector.</span></span> <span data-ttu-id="172fe-134">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span><span class="sxs-lookup"><span data-stu-id="172fe-134">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="172fe-135">Resolve an inactive Connector</span><span class="sxs-lookup"><span data-stu-id="172fe-135">Resolve an inactive Connector</span></span>

<span data-ttu-id="172fe-136">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span><span class="sxs-lookup"><span data-stu-id="172fe-136">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="172fe-137">see the ports Troubleshoot document for details on investigating this problem.</span><span class="sxs-lookup"><span data-stu-id="172fe-137">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="172fe-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="172fe-138">Next steps</span></span>
[<span data-ttu-id="172fe-139">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="172fe-139">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-connectors.md)


