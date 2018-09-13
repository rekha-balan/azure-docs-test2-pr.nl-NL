---
title: Remote Monitoring solution accelerator FAQ | Microsoft Docs
description: Frequently asked questions for Remote Monitoring solution accelerator
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 02/15/2018
ms.author: dobett
ms.openlocfilehash: ba0d81761904be74632f8f0025488b7f501bd715
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857486"
---
# <a name="frequently-asked-questions-for-remote-monitoring-solution-accelerator"></a><span data-ttu-id="6fabe-103">Frequently asked questions for Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="6fabe-103">Frequently asked questions for Remote Monitoring solution accelerator</span></span>

<span data-ttu-id="6fabe-104">See also, the general [FAQ](iot-accelerators-faq.md).</span><span class="sxs-lookup"><span data-stu-id="6fabe-104">See also, the general [FAQ](iot-accelerators-faq.md).</span></span>

### <a name="how-much-does-it-cost-to-provision-the-new-remote-monitoring-solution"></a><span data-ttu-id="6fabe-105">How much does it cost to provision the new Remote Monitoring solution?</span><span class="sxs-lookup"><span data-stu-id="6fabe-105">How much does it cost to provision the new Remote Monitoring solution?</span></span>

<span data-ttu-id="6fabe-106">The new solution accelerator offers two deployment options:</span><span class="sxs-lookup"><span data-stu-id="6fabe-106">The new solution accelerator offers two deployment options:</span></span>

* <span data-ttu-id="6fabe-107">A *basic* option designed for developers looking for lower development cost or customers looking to build a demo or proof of concept.</span><span class="sxs-lookup"><span data-stu-id="6fabe-107">A *basic* option designed for developers looking for lower development cost or customers looking to build a demo or proof of concept.</span></span>
* <span data-ttu-id="6fabe-108">A *standard* option designed for enterprises wanting to deploy a production-ready infrastructure.</span><span class="sxs-lookup"><span data-stu-id="6fabe-108">A *standard* option designed for enterprises wanting to deploy a production-ready infrastructure.</span></span>

### <a name="how-can-i-ensure-i-keep-my-costs-down-while-i-develop-my-solution"></a><span data-ttu-id="6fabe-109">How can I ensure I keep my costs down while I develop my solution?</span><span class="sxs-lookup"><span data-stu-id="6fabe-109">How can I ensure I keep my costs down while I develop my solution?</span></span>

<span data-ttu-id="6fabe-110">In addition to providing two differentiated deployments, the new Remote Monitoring solution has a setting to enable or disable all the simulated devices on demand.</span><span class="sxs-lookup"><span data-stu-id="6fabe-110">In addition to providing two differentiated deployments, the new Remote Monitoring solution has a setting to enable or disable all the simulated devices on demand.</span></span> <span data-ttu-id="6fabe-111">Disabling the simulation reduces the data ingested in the solution and, thus, the overall cost.</span><span class="sxs-lookup"><span data-stu-id="6fabe-111">Disabling the simulation reduces the data ingested in the solution and, thus, the overall cost.</span></span>

### <a name="what-is-the-difference-between-the-basic-and-standard-deployment-options-how-do-i-decide-between-the-two-deployment-options"></a><span data-ttu-id="6fabe-112">What is the difference between the basic and standard deployment options?</span><span class="sxs-lookup"><span data-stu-id="6fabe-112">What is the difference between the basic and standard deployment options?</span></span> <span data-ttu-id="6fabe-113">How do I decide between the two deployment options?</span><span class="sxs-lookup"><span data-stu-id="6fabe-113">How do I decide between the two deployment options?</span></span>

<span data-ttu-id="6fabe-114">Each deployment option responds to different needs.</span><span class="sxs-lookup"><span data-stu-id="6fabe-114">Each deployment option responds to different needs.</span></span> <span data-ttu-id="6fabe-115">The basic deployment is designed to get started and develop PoC and small pilots.</span><span class="sxs-lookup"><span data-stu-id="6fabe-115">The basic deployment is designed to get started and develop PoC and small pilots.</span></span> <span data-ttu-id="6fabe-116">It provides a streamlined architecture with the minimum necessary resources and a lower cost.</span><span class="sxs-lookup"><span data-stu-id="6fabe-116">It provides a streamlined architecture with the minimum necessary resources and a lower cost.</span></span> <span data-ttu-id="6fabe-117">The standard deployment is designed to build and customize a production-ready solution, and provides a deployment with the necessary elements to realize that.</span><span class="sxs-lookup"><span data-stu-id="6fabe-117">The standard deployment is designed to build and customize a production-ready solution, and provides a deployment with the necessary elements to realize that.</span></span> <span data-ttu-id="6fabe-118">For reliability and scale, application microservices are built as Docker containers and deployed using an orchestrator (Kubernetes by default).</span><span class="sxs-lookup"><span data-stu-id="6fabe-118">For reliability and scale, application microservices are built as Docker containers and deployed using an orchestrator (Kubernetes by default).</span></span> <span data-ttu-id="6fabe-119">The orchestrator is responsible for deployment, scaling, and management of the application.</span><span class="sxs-lookup"><span data-stu-id="6fabe-119">The orchestrator is responsible for deployment, scaling, and management of the application.</span></span> <span data-ttu-id="6fabe-120">You should choose an option based on your current needs.</span><span class="sxs-lookup"><span data-stu-id="6fabe-120">You should choose an option based on your current needs.</span></span> <span data-ttu-id="6fabe-121">You might use one, the other, or a combination of both depending on your project stage.</span><span class="sxs-lookup"><span data-stu-id="6fabe-121">You might use one, the other, or a combination of both depending on your project stage.</span></span>

### <a name="how-do-i-configure-a-dynamic-map-on-the-dashboard"></a><span data-ttu-id="6fabe-122">How do I configure a dynamic map on the dashboard?</span><span class="sxs-lookup"><span data-stu-id="6fabe-122">How do I configure a dynamic map on the dashboard?</span></span>

<span data-ttu-id="6fabe-123">For more information, see [Upgrade map key to see devices on a dynamic map](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide#upgrade-map-key-to-see-devices-on-a-dynamic-map).</span><span class="sxs-lookup"><span data-stu-id="6fabe-123">For more information, see [Upgrade map key to see devices on a dynamic map](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide#upgrade-map-key-to-see-devices-on-a-dynamic-map).</span></span>

### <a name="next-steps"></a><span data-ttu-id="6fabe-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="6fabe-124">Next steps</span></span>

<span data-ttu-id="6fabe-125">You can also explore some of the other features and capabilities of the IoT solution accelerators:</span><span class="sxs-lookup"><span data-stu-id="6fabe-125">You can also explore some of the other features and capabilities of the IoT solution accelerators:</span></span>

* [<span data-ttu-id="6fabe-126">Explore the capabilities of the Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="6fabe-126">Explore the capabilities of the Remote Monitoring solution accelerator</span></span>](quickstart-remote-monitoring-deploy.md)
* [<span data-ttu-id="6fabe-127">Predictive Maintenance solution accelerator overview</span><span class="sxs-lookup"><span data-stu-id="6fabe-127">Predictive Maintenance solution accelerator overview</span></span>](iot-accelerators-predictive-overview.md)
* [<span data-ttu-id="6fabe-128">Deploy Connected Factory solution accelerator</span><span class="sxs-lookup"><span data-stu-id="6fabe-128">Deploy Connected Factory solution accelerator</span></span>](quickstart-connected-factory-deploy.md)
* [<span data-ttu-id="6fabe-129">IoT security from the ground up</span><span class="sxs-lookup"><span data-stu-id="6fabe-129">IoT security from the ground up</span></span>](/azure/iot-fundamentals/iot-security-ground-up)
