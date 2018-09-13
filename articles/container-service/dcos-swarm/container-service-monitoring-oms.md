---
title: Monitor Azure DC/OS cluster - Operations Management
description: Monitor an Azure Container Service DC/OS cluster with Log Analytics.
services: container-service
author: keikhara
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: b326e5b686e14cefac4e6376bd3f26787ea1d10d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869792"
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-log-analytics"></a>Monitor an Azure Container Service DC/OS cluster with Log Analytics

Log Analytics is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure. Container Solution is a solution in Log Analytics, which helps you view the container inventory, performance, and logs in a single location. You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.

![](media/container-service-monitoring-oms/image1.png)

For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-log-analytics-from-the-dcos-universe"></a>Setting up Log Analytics from the DC/OS universe


This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.

### <a name="pre-requisite"></a>Pre-requisite
- [Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.  
- Log Analytics Workspace Setup - see "Step 3" below
- [DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.

1. In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.

![](media/container-service-monitoring-oms/image2.png)

2. Click **Install**. You will see a pop up with the version information and an **Install Package** or **Advanced Installation** button. When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. Here, you will be asked to enter the `wsid` (the Log Analytics workspace ID) and `wskey` (the primary key for the workspace id). To get both `wsid` and `wskey` you need to create an account at <https://mms.microsoft.com>.
Please follow the steps to create an account. Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.

 ![](media/container-service-monitoring-oms/image5.png)

4. Select the number of instances that you want and click the ‘Review and Install’ button. Typically, you will want to have the number of instances equal to the number of VM’s you have in your agent cluster. OMS Agent for Linux installs as individual containers on each VM that it wants to collect information for monitoring and logging information.

## <a name="setting-up-a-simple-oms-dashboard"></a>Setting up a simple OMS dashboard

Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard. There are two ways to do this: OMS Portal or Azure Portal.

### <a name="oms-portal"></a>OMS Portal 

Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.

![](media/container-service-monitoring-oms/image6.png)

Once you are in the **Solution Gallery**, select **Containers**.

![](media/container-service-monitoring-oms/image7.png)

Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page. Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Azure Portal 

Login to Azure portal at <https://portal.microsoft.com/>. Go to **Marketplace**, select **Monitoring + management** and click **See All**. Then Type `containers` in search. You will see "containers" in the search results. Select **Containers** and click **Create**.

![](media/container-service-monitoring-oms/image9.png)

Once you click **Create**, it will ask you for your workspace. Select your workspace or if you do not have one, create a new workspace.

![](media/container-service-monitoring-oms/image10.PNG)

Once you’ve selected your workspace, click **Create**.

![](media/container-service-monitoring-oms/image11.png)

For more information about the Log Analytics Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).

### <a name="how-to-scale-oms-agent-with-acs-dcos"></a>How to scale OMS Agent with ACS DC/OS 

In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.

You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.

![](media/container-service-monitoring-oms/image12.PNG)

This will deploy to other nodes which have not yet deployed the OMS agent.

## <a name="uninstall-ms-oms"></a>Uninstall MS OMS

To uninstall MS OMS enter the following command:

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>Let us know!!!
What works? What is missing? What else do you need for this to be useful for you? Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Next steps

 Now that you have set up Log Analytics to monitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).