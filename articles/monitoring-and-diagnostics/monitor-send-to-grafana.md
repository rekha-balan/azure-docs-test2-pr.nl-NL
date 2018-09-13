---
title: Monitor Azure services and applications using Grafana
description: Route Azure Monitor and Application Insights data so you can view them in Grafana.
services: azure-monitor
keywords: ''
author: rboucher
ms.author: robb
ms.date: 11/06/2017
ms.topic: conceptual
ms.service: azure-monitor
ms.component: ''
ms.openlocfilehash: de2c57949cb2087e41b79a225963225d340f12af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871707"
---
# <a name="monitor-your-azure-services-in-grafana"></a><span data-ttu-id="128ba-103">Monitor your Azure services in Grafana</span><span class="sxs-lookup"><span data-stu-id="128ba-103">Monitor your Azure services in Grafana</span></span>
<span data-ttu-id="128ba-104">You can now also monitor Azure services and applications from [Grafana](https://grafana.com/) using the [Azure Monitor data source plugin](https://grafana.com/plugins/grafana-azure-monitor-datasource).</span><span class="sxs-lookup"><span data-stu-id="128ba-104">You can now also monitor Azure services and applications from [Grafana](https://grafana.com/) using the [Azure Monitor data source plugin](https://grafana.com/plugins/grafana-azure-monitor-datasource).</span></span> <span data-ttu-id="128ba-105">The plugin gathers application performance data collected by the Application Insights SDK as well as infrastructure data provided by Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="128ba-105">The plugin gathers application performance data collected by the Application Insights SDK as well as infrastructure data provided by Azure Monitor.</span></span> <span data-ttu-id="128ba-106">You can then display this data on your Grafana dashboard.</span><span class="sxs-lookup"><span data-stu-id="128ba-106">You can then display this data on your Grafana dashboard.</span></span>

<span data-ttu-id="128ba-107">The plugin is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="128ba-107">The plugin is currently in preview.</span></span>

<span data-ttu-id="128ba-108">Use the following steps to set up a Grafana server from Azure Marketplace and build dashboards for metrics from Azure Monitor and Application Insights.</span><span class="sxs-lookup"><span data-stu-id="128ba-108">Use the following steps to set up a Grafana server from Azure Marketplace and build dashboards for metrics from Azure Monitor and Application Insights.</span></span>

## <a name="set-up-a-grafana-instance"></a><span data-ttu-id="128ba-109">Set up a Grafana instance</span><span class="sxs-lookup"><span data-stu-id="128ba-109">Set up a Grafana instance</span></span>
1. <span data-ttu-id="128ba-110">Go to Azure Marketplace and pick Grafana by Grafana Labs.</span><span class="sxs-lookup"><span data-stu-id="128ba-110">Go to Azure Marketplace and pick Grafana by Grafana Labs.</span></span>

2. <span data-ttu-id="128ba-111">Fill in the names and details.</span><span class="sxs-lookup"><span data-stu-id="128ba-111">Fill in the names and details.</span></span> <span data-ttu-id="128ba-112">Create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="128ba-112">Create a new resource group.</span></span> <span data-ttu-id="128ba-113">Keep track of the values you choose for the VM username, VM password, and Grafana server admin password.</span><span class="sxs-lookup"><span data-stu-id="128ba-113">Keep track of the values you choose for the VM username, VM password, and Grafana server admin password.</span></span>  

3. <span data-ttu-id="128ba-114">Choose VM size and a storage account.</span><span class="sxs-lookup"><span data-stu-id="128ba-114">Choose VM size and a storage account.</span></span>

4. <span data-ttu-id="128ba-115">Configure the network configuration settings.</span><span class="sxs-lookup"><span data-stu-id="128ba-115">Configure the network configuration settings.</span></span>

5. <span data-ttu-id="128ba-116">View the summary and select **Create** after accepting the terms of use.</span><span class="sxs-lookup"><span data-stu-id="128ba-116">View the summary and select **Create** after accepting the terms of use.</span></span>

## <a name="log-in-to-grafana"></a><span data-ttu-id="128ba-117">Log in to Grafana</span><span class="sxs-lookup"><span data-stu-id="128ba-117">Log in to Grafana</span></span>
1. <span data-ttu-id="128ba-118">After the deployment completes, select **Go to Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="128ba-118">After the deployment completes, select **Go to Resource Group**.</span></span> <span data-ttu-id="128ba-119">You see a list of newly created resources.</span><span class="sxs-lookup"><span data-stu-id="128ba-119">You see a list of newly created resources.</span></span>

    ![Grafana resource group objects](.\media\monitor-how-to-grafana\grafana1.png)

    <span data-ttu-id="128ba-121">If you select the network security group (*grafana-nsg* in this case), you can see that port 3000 is used to access Grafana server.</span><span class="sxs-lookup"><span data-stu-id="128ba-121">If you select the network security group (*grafana-nsg* in this case), you can see that port 3000 is used to access Grafana server.</span></span>

2. <span data-ttu-id="128ba-122">Go back to the list of resources and select **Public IP address**.</span><span class="sxs-lookup"><span data-stu-id="128ba-122">Go back to the list of resources and select **Public IP address**.</span></span> <span data-ttu-id="128ba-123">Using the values found on this screen, type *http://<IP address>:3000*  or the *<DNSName>:3000* in your browser.</span><span class="sxs-lookup"><span data-stu-id="128ba-123">Using the values found on this screen, type *http://<IP address>:3000*  or the *<DNSName>:3000* in your browser.</span></span> <span data-ttu-id="128ba-124">You should see a login page for the Grafana server you just built.</span><span class="sxs-lookup"><span data-stu-id="128ba-124">You should see a login page for the Grafana server you just built.</span></span>

    ![Grafana login screen](.\media\monitor-how-to-grafana\grafana2.png)

3. <span data-ttu-id="128ba-126">Log in with the user name as *admin* and the Grafana server admin password you created earlier.</span><span class="sxs-lookup"><span data-stu-id="128ba-126">Log in with the user name as *admin* and the Grafana server admin password you created earlier.</span></span>

## <a name="configure-data-source-plugin"></a><span data-ttu-id="128ba-127">Configure data source plugin</span><span class="sxs-lookup"><span data-stu-id="128ba-127">Configure data source plugin</span></span>

<span data-ttu-id="128ba-128">Once successfully logged in, you should see that the Azure Monitor data source plugin is already included.</span><span class="sxs-lookup"><span data-stu-id="128ba-128">Once successfully logged in, you should see that the Azure Monitor data source plugin is already included.</span></span>

![Grafana shows Azure Monitor plugin](.\media\monitor-how-to-grafana\grafana3.png)

1. <span data-ttu-id="128ba-130">Select **Add data source** to configure Azure Monitor and Application Insights.</span><span class="sxs-lookup"><span data-stu-id="128ba-130">Select **Add data source** to configure Azure Monitor and Application Insights.</span></span>

2. <span data-ttu-id="128ba-131">Pick a name for the data source and select **Azure Monitor** as the data source from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="128ba-131">Pick a name for the data source and select **Azure Monitor** as the data source from the dropdown.</span></span>


## <a name="create-a-service-principal"></a><span data-ttu-id="128ba-132">Create a service principal</span><span class="sxs-lookup"><span data-stu-id="128ba-132">Create a service principal</span></span>

<span data-ttu-id="128ba-133">Grafana uses an Azure Active Directory service principal to connect to Azure Monitor APIs and collect metrics data.</span><span class="sxs-lookup"><span data-stu-id="128ba-133">Grafana uses an Azure Active Directory service principal to connect to Azure Monitor APIs and collect metrics data.</span></span> <span data-ttu-id="128ba-134">You must create a service principal to manage access to your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="128ba-134">You must create a service principal to manage access to your Azure resources.</span></span>

1. <span data-ttu-id="128ba-135">See [these instructions](../azure-resource-manager/resource-group-create-service-principal-portal.md) to create a service principal.</span><span class="sxs-lookup"><span data-stu-id="128ba-135">See [these instructions](../azure-resource-manager/resource-group-create-service-principal-portal.md) to create a service principal.</span></span> <span data-ttu-id="128ba-136">Copy and save your tenant ID, client ID, and a client secret.</span><span class="sxs-lookup"><span data-stu-id="128ba-136">Copy and save your tenant ID, client ID, and a client secret.</span></span>

2. <span data-ttu-id="128ba-137">See [Assign application to role](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#assign-application-to-role) to assign the reader role to the Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="128ba-137">See [Assign application to role](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#assign-application-to-role) to assign the reader role to the Azure Active Directory application.</span></span>     

3. <span data-ttu-id="128ba-138">If you use Application Insights, you can also include your Application Insights API and application ID to collect Application Insights based metrics.</span><span class="sxs-lookup"><span data-stu-id="128ba-138">If you use Application Insights, you can also include your Application Insights API and application ID to collect Application Insights based metrics.</span></span> <span data-ttu-id="128ba-139">For more information, see [Getting your API key and Application ID](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).</span><span class="sxs-lookup"><span data-stu-id="128ba-139">For more information, see [Getting your API key and Application ID](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).</span></span>

4. <span data-ttu-id="128ba-140">After you have entered all of this info, select **Save** and Grafana tests the API.</span><span class="sxs-lookup"><span data-stu-id="128ba-140">After you have entered all of this info, select **Save** and Grafana tests the API.</span></span> <span data-ttu-id="128ba-141">You should see a message similar to the following one.</span><span class="sxs-lookup"><span data-stu-id="128ba-141">You should see a message similar to the following one.</span></span>  

    ![Grafana shows Azure Monitor plugin](.\media\monitor-how-to-grafana\grafana4-1.png)

> [!NOTE]
> <span data-ttu-id="128ba-143">While configuring the plugin you can indicate which Azure Cloud (Public, Azure US Government, Azure Germany, or Azure China) you would like the plugin to be configured against.</span><span class="sxs-lookup"><span data-stu-id="128ba-143">While configuring the plugin you can indicate which Azure Cloud (Public, Azure US Government, Azure Germany, or Azure China) you would like the plugin to be configured against.</span></span>
>
>

## <a name="build-a-grafana-dashboard"></a><span data-ttu-id="128ba-144">Build a Grafana dashboard</span><span class="sxs-lookup"><span data-stu-id="128ba-144">Build a Grafana dashboard</span></span>

1. <span data-ttu-id="128ba-145">Go to Home and select **New Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="128ba-145">Go to Home and select **New Dashboard**.</span></span>

2. <span data-ttu-id="128ba-146">In the new dashboard, select the **Graph**.</span><span class="sxs-lookup"><span data-stu-id="128ba-146">In the new dashboard, select the **Graph**.</span></span> <span data-ttu-id="128ba-147">You can try other charting options but this article uses *Graph* as an example.</span><span class="sxs-lookup"><span data-stu-id="128ba-147">You can try other charting options but this article uses *Graph* as an example.</span></span>

    ![Grafana New Dashboard](.\media\monitor-how-to-grafana\grafana5.png)

3. <span data-ttu-id="128ba-149">A blank graph shows up on your dashboard.</span><span class="sxs-lookup"><span data-stu-id="128ba-149">A blank graph shows up on your dashboard.</span></span>

4. <span data-ttu-id="128ba-150">Click on the panel title and select **Edit** to enter the details of the data you want to plot in this graph chart.</span><span class="sxs-lookup"><span data-stu-id="128ba-150">Click on the panel title and select **Edit** to enter the details of the data you want to plot in this graph chart.</span></span>

5. <span data-ttu-id="128ba-151">Once you have selected all the right VMs, you can start viewing the metrics in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="128ba-151">Once you have selected all the right VMs, you can start viewing the metrics in the dashboard.</span></span>

<span data-ttu-id="128ba-152">Following is a simple dashboard with two charts.</span><span class="sxs-lookup"><span data-stu-id="128ba-152">Following is a simple dashboard with two charts.</span></span> <span data-ttu-id="128ba-153">The one on left shows the CPU percentage of two VMs.</span><span class="sxs-lookup"><span data-stu-id="128ba-153">The one on left shows the CPU percentage of two VMs.</span></span> <span data-ttu-id="128ba-154">The chart on the right shows the transactions in an Azure Storage account broken down by the Transaction API type.</span><span class="sxs-lookup"><span data-stu-id="128ba-154">The chart on the right shows the transactions in an Azure Storage account broken down by the Transaction API type.</span></span>

![Grafana Two Charts Example](.\media\monitor-how-to-grafana\grafana6.png)


## <a name="optional-create-dashboard-playlists"></a><span data-ttu-id="128ba-156">Optional: Create dashboard playlists</span><span class="sxs-lookup"><span data-stu-id="128ba-156">Optional: Create dashboard playlists</span></span>

<span data-ttu-id="128ba-157">One of the many useful features of Grafana is the dashboard playlist.</span><span class="sxs-lookup"><span data-stu-id="128ba-157">One of the many useful features of Grafana is the dashboard playlist.</span></span> <span data-ttu-id="128ba-158">You can create multiple dashboards and add them to a playlist configuring an interval for each dashboard to show.</span><span class="sxs-lookup"><span data-stu-id="128ba-158">You can create multiple dashboards and add them to a playlist configuring an interval for each dashboard to show.</span></span> <span data-ttu-id="128ba-159">Select **Play** to see the dashboards cycle through.</span><span class="sxs-lookup"><span data-stu-id="128ba-159">Select **Play** to see the dashboards cycle through.</span></span> <span data-ttu-id="128ba-160">You may want to display them on a large wall monitor to provide a "status board" for your group.</span><span class="sxs-lookup"><span data-stu-id="128ba-160">You may want to display them on a large wall monitor to provide a "status board" for your group.</span></span>

![Grafana Playlist Example](.\media\monitor-how-to-grafana\grafana7.png)


## <a name="optional-monitor-your-custom-metrics-in-the-same-grafana-server"></a><span data-ttu-id="128ba-162">Optional: Monitor your custom metrics in the same Grafana server</span><span class="sxs-lookup"><span data-stu-id="128ba-162">Optional: Monitor your custom metrics in the same Grafana server</span></span>

<span data-ttu-id="128ba-163">You can also install Telegraf and InfluxDB to collect and plot both custom and agent-based metrics in the same Grafana instance.</span><span class="sxs-lookup"><span data-stu-id="128ba-163">You can also install Telegraf and InfluxDB to collect and plot both custom and agent-based metrics in the same Grafana instance.</span></span> <span data-ttu-id="128ba-164">There are many data source plugins that you can use to bring these metrics together in a dashboard.</span><span class="sxs-lookup"><span data-stu-id="128ba-164">There are many data source plugins that you can use to bring these metrics together in a dashboard.</span></span>

<span data-ttu-id="128ba-165">You can also reuse this set up to include metrics from your Prometheus server.</span><span class="sxs-lookup"><span data-stu-id="128ba-165">You can also reuse this set up to include metrics from your Prometheus server.</span></span> <span data-ttu-id="128ba-166">Use the Prometheus data source plugin in Grafana's plugin gallery.</span><span class="sxs-lookup"><span data-stu-id="128ba-166">Use the Prometheus data source plugin in Grafana's plugin gallery.</span></span>

<span data-ttu-id="128ba-167">Here are good reference articles on how to use Telegraf, InfluxDB, Prometheus, and Docker</span><span class="sxs-lookup"><span data-stu-id="128ba-167">Here are good reference articles on how to use Telegraf, InfluxDB, Prometheus, and Docker</span></span>
 - [<span data-ttu-id="128ba-168">How To Monitor System Metrics with the TICK Stack on Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="128ba-168">How To Monitor System Metrics with the TICK Stack on Ubuntu 16.04</span></span>](https://www.digitalocean.com/community/tutorials/how-to-monitor-system-metrics-with-the-tick-stack-on-ubuntu-16-04)

 - [<span data-ttu-id="128ba-169">Monitor Docker resource metrics with Grafana, InfluxDB, and Telegraf</span><span class="sxs-lookup"><span data-stu-id="128ba-169">Monitor Docker resource metrics with Grafana, InfluxDB, and Telegraf</span></span>](https://blog.vpetkov.net/2016/08/04/monitor-docker-resource-metrics-with-grafana-influxdb-and-telegraf/)

 - [<span data-ttu-id="128ba-170">A monitoring solution for Docker hosts, containers, and containerized services</span><span class="sxs-lookup"><span data-stu-id="128ba-170">A monitoring solution for Docker hosts, containers, and containerized services</span></span>](https://stefanprodan.com/2016/a-monitoring-solution-for-docker-hosts-containers-and-containerized-services/)

<span data-ttu-id="128ba-171">Here is an image of a full Grafana dashboard that has metrics from Azure Monitor and Application Insights.</span><span class="sxs-lookup"><span data-stu-id="128ba-171">Here is an image of a full Grafana dashboard that has metrics from Azure Monitor and Application Insights.</span></span>
<span data-ttu-id="128ba-172">![Grafana Example Metrics](.\media\monitor-how-to-grafana\grafana8.png)</span><span class="sxs-lookup"><span data-stu-id="128ba-172">![Grafana Example Metrics](.\media\monitor-how-to-grafana\grafana8.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="128ba-173">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="128ba-173">Clean up resources</span></span>

<span data-ttu-id="128ba-174">You are charged when VMs are running whether you are using them or not.</span><span class="sxs-lookup"><span data-stu-id="128ba-174">You are charged when VMs are running whether you are using them or not.</span></span> <span data-ttu-id="128ba-175">To avoid incurring additional charges, clean up the resource group created in this article.</span><span class="sxs-lookup"><span data-stu-id="128ba-175">To avoid incurring additional charges, clean up the resource group created in this article.</span></span>

1. <span data-ttu-id="128ba-176">From the left-hand menu in the Azure portal, click **Resource groups** and then click **Grafana**.</span><span class="sxs-lookup"><span data-stu-id="128ba-176">From the left-hand menu in the Azure portal, click **Resource groups** and then click **Grafana**.</span></span>
2. <span data-ttu-id="128ba-177">On your resource group page, click **Delete**, type **Grafana** in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="128ba-177">On your resource group page, click **Delete**, type **Grafana** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="128ba-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="128ba-178">Next steps</span></span>
* [<span data-ttu-id="128ba-179">Overview of Azure Monitor Metrics</span><span class="sxs-lookup"><span data-stu-id="128ba-179">Overview of Azure Monitor Metrics</span></span>](monitoring-overview-metrics.md)
