---
title: Monitor an Azure Container Service cluster with Sysdig | Microsoft Docs
description: Monitor an Azure Container Service cluster with Sysdig.
services: container-service
documentationcenter: ''
author: sauryadas
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Containers, DC/OS, Azure
ms.assetid: 91d9a28a-3a52-4194-879e-30f2fa3d946b
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.openlocfilehash: 34e9f538c85bc55fc71d83342cae53beda341a3a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553180"
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Monitor an Azure Container Service cluster with Sysdig
In this article, we will deploy Sysdig agents to all the agent nodes in your Azure Container Service cluster. You need an account with Sysdig for this configuration. 

## <a name="prerequisites"></a>Prerequisites
[Deploy](container-service-deployment.md) and [connect](container-service-connect.md) a cluster configured by Azure Container Service. Explore the [Marathon UI](container-service-mesos-marathon-ui.md). Go to [http://app.sysdigcloud.com](http://app.sysdigcloud.com) to set up a Sysdig cloud account. 

## <a name="sysdig"></a>Sysdig
Sysdig is a monitoring service that allows you to monitor your containers within your cluster. Sysdig is known to help with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O. Sysdig makes it easy to see which containers are working the hardest or essentially using the most memory and CPU. This view is in the “Overview” section, which is currently in beta. 

![Sysdig UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Configure a Sysdig deployment with Marathon
These steps will show you how to configure and deploy Sysdig applications to your cluster with Marathon. 

Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to the "Universe", which is on the bottom left and then search for "Sysdig."

![Sysdig in DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig1.png)

Now to complete the configuration you need a Sysdig cloud account or a free trial account. Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key." 

![Sysdig API key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig2.png) 

Next enter your Access Key into the Sysdig configuration within the DC/OS Universe. 

![Sysdig configuration in the DC/OS Universe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig3.png)

Now set the instances to 10000000 so whenever a new node is added to the cluster Sysdig will automatically deploy an agent to that new node. This is an interim solution to make sure Sysdig will deploy to all new agents within the cluster. 

![Sysdig configuration in the DC/OS Universe-instances](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig4.png)

Once you've installed the package navigate back to the Sysdig UI and you'll be able to explore the different usage metrics for the containers within your cluster. 

You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).





