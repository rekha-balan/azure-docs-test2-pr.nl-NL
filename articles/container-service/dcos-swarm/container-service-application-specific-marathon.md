---
title: Application or user-specific Marathon service
description: Create an application or user-specific Marathon service
services: container-service
author: rgardler
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 4ff263fe0ca4f435199127ed64faadee1c2527f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857386"
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="b7aa6-103">Create an application or user-specific Marathon service</span><span class="sxs-lookup"><span data-stu-id="b7aa6-103">Create an application or user-specific Marathon service</span></span>

<span data-ttu-id="b7aa6-104">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-104">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="b7aa6-105">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-105">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span></span> <span data-ttu-id="b7aa6-106">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-106">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span></span> <span data-ttu-id="b7aa6-107">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-107">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span></span>

<span data-ttu-id="b7aa6-108">In this article, we'll explain how to add an application or user-specific Marathon service.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-108">In this article, we'll explain how to add an application or user-specific Marathon service.</span></span>

<span data-ttu-id="b7aa6-109">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-109">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span></span> <span data-ttu-id="b7aa6-110">Also, Azure Container Service will ensure that the service continues to run.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-110">Also, Azure Container Service will ensure that the service continues to run.</span></span> <span data-ttu-id="b7aa6-111">If the service fails, Azure Container Service will restart it for you.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-111">If the service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="b7aa6-112">Most of the time you won't even notice it had downtime.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-112">Most of the time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7aa6-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7aa6-113">Prerequisites</span></span>
<span data-ttu-id="b7aa6-114">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b7aa6-114">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](../container-service-connect.md).</span></span> <span data-ttu-id="b7aa6-115">Also, do the following steps.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-115">Also, do the following steps.</span></span>

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="b7aa6-116">Create an application or user-specific Marathon service</span><span class="sxs-lookup"><span data-stu-id="b7aa6-116">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="b7aa6-117">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-117">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span></span> <span data-ttu-id="b7aa6-118">Here we use `marathon-alice` as the framework name.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-118">Here we use `marathon-alice` as the framework name.</span></span> <span data-ttu-id="b7aa6-119">Save the file as something like `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="b7aa6-119">Save the file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="b7aa6-120">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span><span class="sxs-lookup"><span data-stu-id="b7aa6-120">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="b7aa6-121">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-121">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span></span> <span data-ttu-id="b7aa6-122">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-122">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span></span>

## <a name="set-the-dcos-cli-to-access-the-service"></a><span data-ttu-id="b7aa6-123">Set the DC/OS CLI to access the service</span><span class="sxs-lookup"><span data-stu-id="b7aa6-123">Set the DC/OS CLI to access the service</span></span>
<span data-ttu-id="b7aa6-124">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span><span class="sxs-lookup"><span data-stu-id="b7aa6-124">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="b7aa6-125">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-125">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span></span> <span data-ttu-id="b7aa6-126">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="b7aa6-126">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span></span>

