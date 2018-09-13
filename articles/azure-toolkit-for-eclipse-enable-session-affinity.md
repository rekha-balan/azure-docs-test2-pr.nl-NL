---
title: Enable Session Affinity using the Azure Toolkit for Eclipse
description: Learn how to enable session affinity using the Azure Toolkit for Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2016
ms.author: robmcm
ms.openlocfilehash: 5a821a0f4ce55d4d6156e934e75b3fdb5b131024
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662463"
---
# <a name="enable-session-affinity"></a><span data-ttu-id="73017-103">Enable Session Affinity</span><span class="sxs-lookup"><span data-stu-id="73017-103">Enable Session Affinity</span></span>
<span data-ttu-id="73017-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span><span class="sxs-lookup"><span data-stu-id="73017-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="73017-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span><span class="sxs-lookup"><span data-stu-id="73017-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="73017-106">To enable session affinity for your role</span><span class="sxs-lookup"><span data-stu-id="73017-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="73017-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span><span class="sxs-lookup"><span data-stu-id="73017-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>
2. <span data-ttu-id="73017-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span><span class="sxs-lookup"><span data-stu-id="73017-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>
   1. <span data-ttu-id="73017-109">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span><span class="sxs-lookup"><span data-stu-id="73017-109">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>
   2. <span data-ttu-id="73017-110">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span><span class="sxs-lookup"><span data-stu-id="73017-110">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="73017-111">Your application must use this endpoint as its HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="73017-111">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="73017-112">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span><span class="sxs-lookup"><span data-stu-id="73017-112">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>
   3. <span data-ttu-id="73017-113">Rebuild your application.</span><span class="sxs-lookup"><span data-stu-id="73017-113">Rebuild your application.</span></span>

<span data-ttu-id="73017-114">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span><span class="sxs-lookup"><span data-stu-id="73017-114">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="73017-115">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span><span class="sxs-lookup"><span data-stu-id="73017-115">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="73017-116">ARR reroutes HTTP requests to the appropriate role instance.</span><span class="sxs-lookup"><span data-stu-id="73017-116">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="73017-117">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span><span class="sxs-lookup"><span data-stu-id="73017-117">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="73017-118">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span><span class="sxs-lookup"><span data-stu-id="73017-118">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="73017-119">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span><span class="sxs-lookup"><span data-stu-id="73017-119">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="73017-120">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span><span class="sxs-lookup"><span data-stu-id="73017-120">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="73017-121">Notes about session affinity</span><span class="sxs-lookup"><span data-stu-id="73017-121">Notes about session affinity</span></span>
* <span data-ttu-id="73017-122">Session affinity does not work in the compute emulator.</span><span class="sxs-lookup"><span data-stu-id="73017-122">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="73017-123">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span><span class="sxs-lookup"><span data-stu-id="73017-123">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>
* <span data-ttu-id="73017-124">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="73017-124">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>
* <span data-ttu-id="73017-125">The time to initialize each role will take longer.</span><span class="sxs-lookup"><span data-stu-id="73017-125">The time to initialize each role will take longer.</span></span>
* <span data-ttu-id="73017-126">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span><span class="sxs-lookup"><span data-stu-id="73017-126">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="73017-127">See Also</span><span class="sxs-lookup"><span data-stu-id="73017-127">See Also</span></span>
<span data-ttu-id="73017-128">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="73017-128">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="73017-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="73017-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="73017-130">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="73017-130">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="73017-131">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="73017-131">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->

