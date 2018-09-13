---
title: Application or user-specific Marathon service | Microsoft Docs
description: Create an application or user-specific Marathon service
services: container-service
documentationcenter: ''
author: rgardler
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Containers, Marathon, Micro-services, DC/OS, Azure
ms.assetid: 16ecc16e-e504-480e-8dc3-cac14e9e1561
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.openlocfilehash: 1ea024d83c1d8881467be1556675a47c605fee66
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550077"
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="cc96c-104">Create an application or user-specific Marathon service</span><span class="sxs-lookup"><span data-stu-id="cc96c-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="cc96c-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span><span class="sxs-lookup"><span data-stu-id="cc96c-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="cc96c-106">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span><span class="sxs-lookup"><span data-stu-id="cc96c-106">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span></span> <span data-ttu-id="cc96c-107">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span><span class="sxs-lookup"><span data-stu-id="cc96c-107">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span></span> <span data-ttu-id="cc96c-108">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span><span class="sxs-lookup"><span data-stu-id="cc96c-108">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span></span>

<span data-ttu-id="cc96c-109">In this article, we'll explain how to add an application or user-specific Marathon service.</span><span class="sxs-lookup"><span data-stu-id="cc96c-109">In this article, we'll explain how to add an application or user-specific Marathon service.</span></span>

<span data-ttu-id="cc96c-110">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span><span class="sxs-lookup"><span data-stu-id="cc96c-110">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span></span> <span data-ttu-id="cc96c-111">Also, Azure Container Service will ensure that the service continues to run.</span><span class="sxs-lookup"><span data-stu-id="cc96c-111">Also, Azure Container Service will ensure that the service continues to run.</span></span> <span data-ttu-id="cc96c-112">If the service fails, Azure Container Service will restart it for you.</span><span class="sxs-lookup"><span data-stu-id="cc96c-112">If the service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="cc96c-113">Most of the time you won't even notice it had downtime.</span><span class="sxs-lookup"><span data-stu-id="cc96c-113">Most of the time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc96c-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc96c-114">Prerequisites</span></span>
<span data-ttu-id="cc96c-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="cc96c-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](container-service-connect.md).</span></span> <span data-ttu-id="cc96c-116">Also, do the following steps.</span><span class="sxs-lookup"><span data-stu-id="cc96c-116">Also, do the following steps.</span></span>

[!INCLUDE [install the DC/OS CLI](../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="cc96c-117">Create an application or user-specific Marathon service</span><span class="sxs-lookup"><span data-stu-id="cc96c-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="cc96c-118">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span><span class="sxs-lookup"><span data-stu-id="cc96c-118">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span></span> <span data-ttu-id="cc96c-119">Here we use `marathon-alice` as the framework name.</span><span class="sxs-lookup"><span data-stu-id="cc96c-119">Here we use `marathon-alice` as the framework name.</span></span> <span data-ttu-id="cc96c-120">Save the file as something like `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="cc96c-120">Save the file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="cc96c-121">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span><span class="sxs-lookup"><span data-stu-id="cc96c-121">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="cc96c-122">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span><span class="sxs-lookup"><span data-stu-id="cc96c-122">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span></span> <span data-ttu-id="cc96c-123">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span><span class="sxs-lookup"><span data-stu-id="cc96c-123">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span></span>

## <a name="set-the-dcos-cli-to-access-the-service"></a><span data-ttu-id="cc96c-124">Set the DC/OS CLI to access the service</span><span class="sxs-lookup"><span data-stu-id="cc96c-124">Set the DC/OS CLI to access the service</span></span>
<span data-ttu-id="cc96c-125">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span><span class="sxs-lookup"><span data-stu-id="cc96c-125">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="cc96c-126">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span><span class="sxs-lookup"><span data-stu-id="cc96c-126">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span></span> <span data-ttu-id="cc96c-127">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="cc96c-127">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span></span>

