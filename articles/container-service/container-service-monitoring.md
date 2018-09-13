---
title: Monitor Azure DC/OS cluster - Datadog | Microsoft Docs
description: Monitor an Azure Container Service cluster with Datadog. Use the DC/OS web UI to deploy the Datadog agents to your cluster.
services: container-service
documentationcenter: ''
author: sauryadas
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Containers, DC/OS, Docker Swarm, Azure
ms.assetid: ed00635d-4569-4f87-ab63-e307b2690b42
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.openlocfilehash: 123e91aac99697271620133c40f3bcdcd4507a19
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563604"
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Monitor an Azure Container Service DC/OS cluster with Datadog
In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster. You will need an account with Datadog for this configuration. 

## <a name="prerequisites"></a>Prerequisites
[Deploy](container-service-deployment.md) and [connect](container-service-connect.md) a cluster configured by Azure Container Service. Explore the [Marathon UI](container-service-mesos-marathon-ui.md). Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account. 

## <a name="datadog"></a>Datadog
Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster. Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers. Metrics gathered from your containers are organized by CPU, Memory, Network and I/O. Datadog splits metrics into containers and images. An example of what the UI looks like for CPU usage is below.

![Datadog UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Configure a Datadog deployment with Marathon
These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon. 

Access your DC/OS UI via [http://localhost:80/](http://localhost:80/). Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."

![Datadog package within the DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring/datadog1.png)

Now to complete the configuration you will need a Datadog account or a free trial account. Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api). 

![Datadog API key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring/datadog2.png)

Next enter your API key into the Datadog configuration within the DC/OS Universe. 

![Datadog configuration in the DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring/datadog3.png) 

In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node. This is an interim solution. Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)." From there you will see Custom and Integration Dashboards. The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster. 





