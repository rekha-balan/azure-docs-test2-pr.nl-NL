---
title: Create a function app from the Azure Portal | Microsoft Docs
description: Create a new function app in Azure App Service from the portal.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
ms.assetid: ''
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.openlocfilehash: 60c387331f0d47ddcc0dd2da8831911618c002b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661246"
---
# <a name="create-a-function-app-from-the-azure-portal"></a><span data-ttu-id="1a531-103">Create a function app from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1a531-103">Create a function app from the Azure portal</span></span>

<span data-ttu-id="1a531-104">Azure Function Apps uses the Azure App Service infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1a531-104">Azure Function Apps uses the Azure App Service infrastructure.</span></span> <span data-ttu-id="1a531-105">This topic shows you how to create a function app in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1a531-105">This topic shows you how to create a function app in the Azure portal.</span></span> <span data-ttu-id="1a531-106">A function app is the container that hosts the execution of individual functions.</span><span class="sxs-lookup"><span data-stu-id="1a531-106">A function app is the container that hosts the execution of individual functions.</span></span> <span data-ttu-id="1a531-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span><span class="sxs-lookup"><span data-stu-id="1a531-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="1a531-108">Create a function app</span><span class="sxs-lookup"><span data-stu-id="1a531-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="1a531-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="1a531-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="1a531-110">Underscore (**_**) is not an allowed character.</span><span class="sxs-lookup"><span data-stu-id="1a531-110">Underscore (**_**) is not an allowed character.</span></span> 

<span data-ttu-id="1a531-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span><span class="sxs-lookup"><span data-stu-id="1a531-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="1a531-112">Your storage account name must be unique within Azure.</span><span class="sxs-lookup"><span data-stu-id="1a531-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="1a531-113">After the function app is created, you can create individual functions in one or more different languages.</span><span class="sxs-lookup"><span data-stu-id="1a531-113">After the function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="1a531-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-a-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="1a531-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-a-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>  

## <a name="service-plans"></a><span data-ttu-id="1a531-115">Service plans</span><span class="sxs-lookup"><span data-stu-id="1a531-115">Service plans</span></span>

<span data-ttu-id="1a531-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span><span class="sxs-lookup"><span data-stu-id="1a531-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="1a531-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span><span class="sxs-lookup"><span data-stu-id="1a531-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="1a531-118">The App Service plan gives your function app access to all the facilities of App Service.</span><span class="sxs-lookup"><span data-stu-id="1a531-118">The App Service plan gives your function app access to all the facilities of App Service.</span></span> <span data-ttu-id="1a531-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span><span class="sxs-lookup"><span data-stu-id="1a531-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="1a531-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="1a531-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="1a531-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span><span class="sxs-lookup"><span data-stu-id="1a531-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="1a531-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="1a531-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span> 

## <a name="storage-account-requirements"></a><span data-ttu-id="1a531-123">Storage account requirements</span><span class="sxs-lookup"><span data-stu-id="1a531-123">Storage account requirements</span></span>

<span data-ttu-id="1a531-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span><span class="sxs-lookup"><span data-stu-id="1a531-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="1a531-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span><span class="sxs-lookup"><span data-stu-id="1a531-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="1a531-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span><span class="sxs-lookup"><span data-stu-id="1a531-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="1a531-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span><span class="sxs-lookup"><span data-stu-id="1a531-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="1a531-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span><span class="sxs-lookup"><span data-stu-id="1a531-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span></span> <span data-ttu-id="1a531-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span><span class="sxs-lookup"><span data-stu-id="1a531-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="1a531-130">To learn more about storage account types, see [Introducing the Azure Storage Services] (../storage/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="1a531-130">To learn more about storage account types, see [Introducing the Azure Storage Services] (../storage/storage-introduction.md#introducing-the-azure-storage-services).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a531-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a531-131">Next steps</span></span>
[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]

[!INCLUDE [Getting Started Note](../../includes/functions-get-help.md)]

