---
title: Azure Functions Runtime Overview | Microsoft Docs
description: Overview of the Azure Functions Runtime Preview
services: functions
author: apwestgarth
manager: stefsch
ms.assetid: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 11/28/2017
ms.author: anwestg
ms.openlocfilehash: 4d11af1edc13fa675bef5cf9067dbe95646abff1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869872"
---
# <a name="azure-functions-runtime-overview-preview"></a><span data-ttu-id="8d34b-103">Azure Functions Runtime Overview (preview)</span><span class="sxs-lookup"><span data-stu-id="8d34b-103">Azure Functions Runtime Overview (preview)</span></span>

<span data-ttu-id="8d34b-104">The Azure Functions Runtime (preview) provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span><span class="sxs-lookup"><span data-stu-id="8d34b-104">The Azure Functions Runtime (preview) provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="8d34b-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span><span class="sxs-lookup"><span data-stu-id="8d34b-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Azure Functions Runtime Preview Portal][1]

<span data-ttu-id="8d34b-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span><span class="sxs-lookup"><span data-stu-id="8d34b-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="8d34b-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span><span class="sxs-lookup"><span data-stu-id="8d34b-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="8d34b-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span><span class="sxs-lookup"><span data-stu-id="8d34b-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="8d34b-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span><span class="sxs-lookup"><span data-stu-id="8d34b-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="8d34b-111">The Azure Functions Runtime consists of two pieces:</span><span class="sxs-lookup"><span data-stu-id="8d34b-111">The Azure Functions Runtime consists of two pieces:</span></span>

* <span data-ttu-id="8d34b-112">Azure Functions Runtime Management Role</span><span class="sxs-lookup"><span data-stu-id="8d34b-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="8d34b-113">Azure Functions Runtime Worker Role</span><span class="sxs-lookup"><span data-stu-id="8d34b-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="8d34b-114">Azure Functions Management Role</span><span class="sxs-lookup"><span data-stu-id="8d34b-114">Azure Functions Management Role</span></span>

<span data-ttu-id="8d34b-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span><span class="sxs-lookup"><span data-stu-id="8d34b-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="8d34b-116">This role performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8d34b-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="8d34b-117">Hosting of the Azure Functions Management Portal, which is the same one you see in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8d34b-117">Hosting of the Azure Functions Management Portal, which is the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8d34b-118">The portal provides a consistent experience that lets you develop your functions in the same way as you would in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8d34b-118">The portal provides a consistent experience that lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="8d34b-119">Distributing functions across multiple Functions workers.</span><span class="sxs-lookup"><span data-stu-id="8d34b-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="8d34b-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio by downloading and importing the publishing profile.</span><span class="sxs-lookup"><span data-stu-id="8d34b-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio by downloading and importing the publishing profile.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="8d34b-121">Azure Functions Worker Role</span><span class="sxs-lookup"><span data-stu-id="8d34b-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="8d34b-122">The Azure Functions Worker Roles are deployed in Windows Containers and are where your function code executes.</span><span class="sxs-lookup"><span data-stu-id="8d34b-122">The Azure Functions Worker Roles are deployed in Windows Containers and are where your function code executes.</span></span>  <span data-ttu-id="8d34b-123">You can deploy multiple Worker Roles throughout your organization and this option is a key way in which customers can make use of spare compute power.</span><span class="sxs-lookup"><span data-stu-id="8d34b-123">You can deploy multiple Worker Roles throughout your organization and this option is a key way in which customers can make use of spare compute power.</span></span>  <span data-ttu-id="8d34b-124">One example of where spare compute exists in many organizations is machines powered on constantly but not being used for large periods of time.</span><span class="sxs-lookup"><span data-stu-id="8d34b-124">One example of where spare compute exists in many organizations is machines powered on constantly but not being used for large periods of time.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="8d34b-125">Minimum Requirements</span><span class="sxs-lookup"><span data-stu-id="8d34b-125">Minimum Requirements</span></span>

<span data-ttu-id="8d34b-126">To get started with the Azure Functions Runtime, you must have a machine with Windows Server 2016 or Windows 10 Creators Update with access to a SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="8d34b-126">To get started with the Azure Functions Runtime, you must have a machine with Windows Server 2016 or Windows 10 Creators Update with access to a SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d34b-127">Next Steps</span><span class="sxs-lookup"><span data-stu-id="8d34b-127">Next Steps</span></span>

<span data-ttu-id="8d34b-128">Install the [Azure Functions Runtime preview](https://aka.ms/azafrdoc)</span><span class="sxs-lookup"><span data-stu-id="8d34b-128">Install the [Azure Functions Runtime preview](https://aka.ms/azafrdoc)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
