---
title: No working connector group found for an Application Proxy application | Microsoft Docs
description: Address problems you might encounter when there is no working Connector in a Connector Group for your application with the Azure AD Application Proxy
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: abcbce160205d52bcfadbfbaa1f3278b5f6c2a3e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554187"
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="9c655-103">No working connector group found for an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="9c655-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="9c655-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c655-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="9c655-105">Overview of steps</span><span class="sxs-lookup"><span data-stu-id="9c655-105">Overview of steps</span></span>
<span data-ttu-id="9c655-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span><span class="sxs-lookup"><span data-stu-id="9c655-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="9c655-107">If you have no connectors in the group, you can:</span><span class="sxs-lookup"><span data-stu-id="9c655-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="9c655-108">Download a new Connector on the right on-prem server, and assign it to this group</span><span class="sxs-lookup"><span data-stu-id="9c655-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="9c655-109">Move an active Connector into the group</span><span class="sxs-lookup"><span data-stu-id="9c655-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="9c655-110">If you have no active connectors in the group, you can:</span><span class="sxs-lookup"><span data-stu-id="9c655-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="9c655-111">Identify the reason your Connector is inactive and resolve</span><span class="sxs-lookup"><span data-stu-id="9c655-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="9c655-112">Move an active Connector into the group</span><span class="sxs-lookup"><span data-stu-id="9c655-112">Move an active Connector into the group</span></span>

<span data-ttu-id="9c655-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span><span class="sxs-lookup"><span data-stu-id="9c655-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="9c655-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span><span class="sxs-lookup"><span data-stu-id="9c655-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Connector group selection in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="9c655-116">For details on each of these options, see the corresponding section below.</span><span class="sxs-lookup"><span data-stu-id="9c655-116">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="9c655-117">Each of these assumes that you are starting from the Connector management page.</span><span class="sxs-lookup"><span data-stu-id="9c655-117">Each of these assumes that you are starting from the Connector management page.</span></span> <span data-ttu-id="9c655-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span><span class="sxs-lookup"><span data-stu-id="9c655-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="9c655-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span><span class="sxs-lookup"><span data-stu-id="9c655-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Connector group management in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="9c655-121">Download a new Connector</span><span class="sxs-lookup"><span data-stu-id="9c655-121">Download a new Connector</span></span>

<span data-ttu-id="9c655-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="9c655-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="9c655-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span><span class="sxs-lookup"><span data-stu-id="9c655-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="9c655-124">After downloading, the Connector should appear in this menu.</span><span class="sxs-lookup"><span data-stu-id="9c655-124">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="9c655-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span><span class="sxs-lookup"><span data-stu-id="9c655-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="9c655-126">Save the change.</span><span class="sxs-lookup"><span data-stu-id="9c655-126">Save the change.</span></span>

   ![Download the connector from the Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="9c655-128">Move an Active Connector</span><span class="sxs-lookup"><span data-stu-id="9c655-128">Move an Active Connector</span></span>

<span data-ttu-id="9c655-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span><span class="sxs-lookup"><span data-stu-id="9c655-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="9c655-130">To do so, click the Connector.</span><span class="sxs-lookup"><span data-stu-id="9c655-130">To do so, click the Connector.</span></span> <span data-ttu-id="9c655-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span><span class="sxs-lookup"><span data-stu-id="9c655-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="9c655-132">Resolve an inactive Connector</span><span class="sxs-lookup"><span data-stu-id="9c655-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="9c655-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span><span class="sxs-lookup"><span data-stu-id="9c655-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="9c655-134">see the ports Troubleshoot document for details on investigating this problem.</span><span class="sxs-lookup"><span data-stu-id="9c655-134">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c655-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c655-135">Next steps</span></span>
[<span data-ttu-id="9c655-136">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="9c655-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)





