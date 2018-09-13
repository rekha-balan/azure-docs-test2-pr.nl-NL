---
title: Manage Azure DC/OS cluster with Marathon UI | Microsoft Docs
description: Deploy containers to an Azure Container Service cluster service by using the Marathon web UI.
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.assetid: d148ed1e-b582-4d51-944f-1ac7ae3c4fd6
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.openlocfilehash: add77a5d053d3236f27ba8c75470b8a206b775c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555220"
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-the-marathon-web-ui"></a>Manage an Azure Container Service DC/OS cluster through the Marathon web UI
DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware. On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.

While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon. 


## <a name="prerequisites"></a>Prerequisites
Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service. You also need to have remote connectivity to this cluster. For more information on these items, see the following articles:

* [Deploy an Azure Container Service cluster](container-service-deployment.md)
* [Connect to an Azure Container Service cluster](container-service-connect.md)

> [!NOTE]
> This article assumes you are tunneling to the DC/OS cluster through your local port 80.
>

## <a name="explore-the-dcos-ui"></a>Explore the DC/OS UI
With a Secure Shell (SSH) tunnel [established](container-service-connect.md), browse to http://localhost/. This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.

![DC/OS UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-the-marathon-ui"></a>Explore the Marathon UI
To see the Marathon UI, browse to http://localhost/marathon. From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster. You can also see information about running containers and applications.  

![Marathon UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Deploy a Docker-formatted container
To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:

| Field | Value |
| --- | --- |
| ID |nginx |
| Memory | 32 |
| Image |nginx |
| Network |Bridged |
| Host Port |80 |
| Protocol |TCP |

![New Application UI--General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos4.png)

![New Application UI--Docker Container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos5.png)

![New Application UI--Ports and Service Discovery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos6.png)

If you want to statically map the container port to a port on the agent, you need to use JSON Mode. To do so, switch the New Application wizard to **JSON Mode** by using the toggle. Then enter the following setting under the `portMappings` section of the application definition. This example binds port 80 of the container to port 80 of the DC/OS agent. You can switch this wizard out of JSON Mode after you make this change.

```none
"hostPort": 80,
```

![New Application UI--port 80 example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos13.png)

If you want to enable health checks, set a path on the **Health Checks** tab.

![New Application UI--health checks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

The DC/OS cluster is deployed with set of private and public agents. For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent. To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.

Then click **Create Application**.

![New Application UI--public agent setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos14.png)

Back on the Marathon main page, you can see the deployment status for the container. Initially you see a status of **Deploying**. After a successful deployment, the status changes to **Running**.

![Marathon main page UI--container deployment status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos7.png)

When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.

![DC/OS web UI--task running on the cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos8.png)

To see the cluster node that the task is running on, click the **Nodes** tab.

![DC/OS web UI--task cluster node](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-the-container"></a>Reach the container

In this example, the application is running on a public agent node. You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:

* **DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.
* **REGION** is the region in which your resource group is located.

    ![Nginx from Internet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Next steps
* [Work with DC/OS and the Marathon API](container-service-mesos-marathon-rest.md)

* Deep dive on the Azure Container Service with Mesos

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 












