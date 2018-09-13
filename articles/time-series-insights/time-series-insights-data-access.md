---
title: Data access policies in Azure Time Series Insights | Microsoft Docs
description: In this tutorial, you learn to manage data access policies in Time Series Insights
keywords: ''
services: time-series-insights
documentationcenter: ''
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: ''
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/20/2017
ms.author: omravi
ms.openlocfilehash: 77fa5f809077207b11bdcb5e54db495882210e4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553585"
---
# <a name="grant-data-access-to-a-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="459f7-103">Grant data access to a Time Series Insights environment using Azure portal</span><span class="sxs-lookup"><span data-stu-id="459f7-103">Grant data access to a Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="459f7-104">Time Series Insights environments have two independent kinds of access policies:</span><span class="sxs-lookup"><span data-stu-id="459f7-104">Time Series Insights environments have two independent kinds of access policies:</span></span>

* <span data-ttu-id="459f7-105">Management access policies (“Access control (IAM)” tab on the environment blade)</span><span class="sxs-lookup"><span data-stu-id="459f7-105">Management access policies (“Access control (IAM)” tab on the environment blade)</span></span>
* <span data-ttu-id="459f7-106">Data access policies</span><span class="sxs-lookup"><span data-stu-id="459f7-106">Data access policies</span></span>

## <a name="management-of-the-time-series-insights-environment"></a><span data-ttu-id="459f7-107">Management of the Time Series Insights environment</span><span class="sxs-lookup"><span data-stu-id="459f7-107">Management of the Time Series Insights environment</span></span>

<span data-ttu-id="459f7-108">Both kinds of policies grant Azure Active Directory principals (users and apps) various permissions.</span><span class="sxs-lookup"><span data-stu-id="459f7-108">Both kinds of policies grant Azure Active Directory principals (users and apps) various permissions.</span></span> <span data-ttu-id="459f7-109">Management access policies grant permissions related to the configuration of the environment (creation and deletion of the environment, event sources, reference data sets, etc.).</span><span class="sxs-lookup"><span data-stu-id="459f7-109">Management access policies grant permissions related to the configuration of the environment (creation and deletion of the environment, event sources, reference data sets, etc.).</span></span> <span data-ttu-id="459f7-110">Data access polies grant permissions to issue data queries and manipulate reference data rows.</span><span class="sxs-lookup"><span data-stu-id="459f7-110">Data access polies grant permissions to issue data queries and manipulate reference data rows.</span></span> <span data-ttu-id="459f7-111">The two kinds of the policies allow clear separation between access to the management of an environment access to the data inside the environment.</span><span class="sxs-lookup"><span data-stu-id="459f7-111">The two kinds of the policies allow clear separation between access to the management of an environment access to the data inside the environment.</span></span> <span data-ttu-id="459f7-112">For example, it is possible to setup an environment such that even the owner/creator of the environment is removed from the data access.</span><span class="sxs-lookup"><span data-stu-id="459f7-112">For example, it is possible to setup an environment such that even the owner/creator of the environment is removed from the data access.</span></span> <span data-ttu-id="459f7-113">As well as users and service that are allowed to read data may have absolutely no access to the configuration of the environment.</span><span class="sxs-lookup"><span data-stu-id="459f7-113">As well as users and service that are allowed to read data may have absolutely no access to the configuration of the environment.</span></span>

<span data-ttu-id="459f7-114">Both kinds of policies operate over principals (users and apps) defined in the Active Directory (or “Azure tenant”) associated with the subscription containing the environment.</span><span class="sxs-lookup"><span data-stu-id="459f7-114">Both kinds of policies operate over principals (users and apps) defined in the Active Directory (or “Azure tenant”) associated with the subscription containing the environment.</span></span>

<span data-ttu-id="459f7-115">The following steps show how to grant data access for a user principal:</span><span class="sxs-lookup"><span data-stu-id="459f7-115">The following steps show how to grant data access for a user principal:</span></span>

1.  <span data-ttu-id="459f7-116">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="459f7-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="459f7-117">Click “All resources” in the menu on the left side of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="459f7-117">Click “All resources” in the menu on the left side of the Azure portal.</span></span>
3.  <span data-ttu-id="459f7-118">Select your Time Series Insights environment.</span><span class="sxs-lookup"><span data-stu-id="459f7-118">Select your Time Series Insights environment.</span></span>
  
  ![Manage the Time Series Insights source - environment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="459f7-120">Select “Data Plane Access”, click “Add”</span><span class="sxs-lookup"><span data-stu-id="459f7-120">Select “Data Plane Access”, click “Add”</span></span>
  
  ![Manage the Time Series Insights source - add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/data-access/getstarted-grant-data-access2.png)
  
5.  <span data-ttu-id="459f7-122">Click “Select user”.</span><span class="sxs-lookup"><span data-stu-id="459f7-122">Click “Select user”.</span></span>
6.  <span data-ttu-id="459f7-123">Search and select user by the email.</span><span class="sxs-lookup"><span data-stu-id="459f7-123">Search and select user by the email.</span></span>
7.  <span data-ttu-id="459f7-124">Click “Select” in “Select User” blade.</span><span class="sxs-lookup"><span data-stu-id="459f7-124">Click “Select” in “Select User” blade.</span></span>
  
  ![Manage the Time Series Insights source - select user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/data-access/getstarted-grant-data-access3.png)
  
8.  <span data-ttu-id="459f7-126">Click “Select role”.</span><span class="sxs-lookup"><span data-stu-id="459f7-126">Click “Select role”.</span></span>
9.  <span data-ttu-id="459f7-127">Select “Contributor” if you want to allow user to change reference data and share saved queries and perspectives with other users of the environment.</span><span class="sxs-lookup"><span data-stu-id="459f7-127">Select “Contributor” if you want to allow user to change reference data and share saved queries and perspectives with other users of the environment.</span></span> <span data-ttu-id="459f7-128">Otherwise select “Reader” to allow user query data in the environment and save personal (not shared) queries in the environment.</span><span class="sxs-lookup"><span data-stu-id="459f7-128">Otherwise select “Reader” to allow user query data in the environment and save personal (not shared) queries in the environment.</span></span>
10. <span data-ttu-id="459f7-129">Click “Ok” in the “Select Role” blade.</span><span class="sxs-lookup"><span data-stu-id="459f7-129">Click “Ok” in the “Select Role” blade.</span></span>
  
  ![Manage the Time Series Insights source - select role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/data-access/getstarted-grant-data-access4.png)
  
11. <span data-ttu-id="459f7-131">Click “Ok” in the “Select User Role” blade.</span><span class="sxs-lookup"><span data-stu-id="459f7-131">Click “Ok” in the “Select User Role” blade.</span></span>
12. <span data-ttu-id="459f7-132">You should see:</span><span class="sxs-lookup"><span data-stu-id="459f7-132">You should see:</span></span>
  
  ![Manage the Time Series Insights source - results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/data-access/getstarted-grant-data-access5.png)
  





