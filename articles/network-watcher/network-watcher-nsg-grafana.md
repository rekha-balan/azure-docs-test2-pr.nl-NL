---
title: Manage Network Security Group Flow Logs using Network Watcher and Grafana | Microsoft Docs
description: Manage and analyze Network Security Group Flow Logs in Azure using Network Watcher and Grafana.
services: network-watcher
documentationcenter: na
author: mattreatMSFT
manager: vitinnan
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/15/2017
ms.author: mareat
ms.openlocfilehash: e375476536e7fe150e3aabcae7cee942deac02d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867673"
---
# <a name="manage-and-analyze-network-security-group-flow-logs-using-network-watcher-and-grafana"></a><span data-ttu-id="f7535-103">Manage and analyze Network Security Group flow logs using Network Watcher and Grafana</span><span class="sxs-lookup"><span data-stu-id="f7535-103">Manage and analyze Network Security Group flow logs using Network Watcher and Grafana</span></span>

<span data-ttu-id="f7535-104">[Network Security Group (NSG) flow logs](network-watcher-nsg-flow-logging-overview.md) provide information that can be used to understand ingress and egress IP traffic on network interfaces.</span><span class="sxs-lookup"><span data-stu-id="f7535-104">[Network Security Group (NSG) flow logs](network-watcher-nsg-flow-logging-overview.md) provide information that can be used to understand ingress and egress IP traffic on network interfaces.</span></span> <span data-ttu-id="f7535-105">These flow logs show outbound and inbound flows on a per NSG rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="f7535-105">These flow logs show outbound and inbound flows on a per NSG rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="f7535-106">You can have many NSGs in your network with flow logging enabled.</span><span class="sxs-lookup"><span data-stu-id="f7535-106">You can have many NSGs in your network with flow logging enabled.</span></span> <span data-ttu-id="f7535-107">This amount of logging data makes it cumbersome to parse and gain insights from your logs.</span><span class="sxs-lookup"><span data-stu-id="f7535-107">This amount of logging data makes it cumbersome to parse and gain insights from your logs.</span></span> <span data-ttu-id="f7535-108">This article provides a solution to centrally manage these NSG flow logs using Grafana, an open source graphing tool, ElasticSearch, a distributed search and analytics engine, and Logstash, which is an open source server-side data processing pipeline.</span><span class="sxs-lookup"><span data-stu-id="f7535-108">This article provides a solution to centrally manage these NSG flow logs using Grafana, an open source graphing tool, ElasticSearch, a distributed search and analytics engine, and Logstash, which is an open source server-side data processing pipeline.</span></span>  

## <a name="scenario"></a><span data-ttu-id="f7535-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="f7535-109">Scenario</span></span>

<span data-ttu-id="f7535-110">NSG flow logs are enabled using Network Watcher and are stored in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="f7535-110">NSG flow logs are enabled using Network Watcher and are stored in Azure blob storage.</span></span> <span data-ttu-id="f7535-111">A Logstash plugin is used to connect and process flow logs from blob storage and send them to ElasticSearch.</span><span class="sxs-lookup"><span data-stu-id="f7535-111">A Logstash plugin is used to connect and process flow logs from blob storage and send them to ElasticSearch.</span></span>  <span data-ttu-id="f7535-112">Once the flow logs are stored in ElasticSearch, they can be analyzed and visualized into customized dashboards in Grafana.</span><span class="sxs-lookup"><span data-stu-id="f7535-112">Once the flow logs are stored in ElasticSearch, they can be analyzed and visualized into customized dashboards in Grafana.</span></span>

![NSG Network Watcher Grafana](./media/network-watcher-nsg-grafana/network-watcher-nsg-grafana-fig1.png)

## <a name="installation-steps"></a><span data-ttu-id="f7535-114">Installation steps</span><span class="sxs-lookup"><span data-stu-id="f7535-114">Installation steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="f7535-115">Enable Network Security Group flow logging</span><span class="sxs-lookup"><span data-stu-id="f7535-115">Enable Network Security Group flow logging</span></span>

<span data-ttu-id="f7535-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span><span class="sxs-lookup"><span data-stu-id="f7535-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="f7535-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7535-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

### <a name="setup-considerations"></a><span data-ttu-id="f7535-118">Setup considerations</span><span class="sxs-lookup"><span data-stu-id="f7535-118">Setup considerations</span></span>

<span data-ttu-id="f7535-119">In this example Grafana, ElasticSearch, and Logstash are configured on an Ubuntu 16.04 LTS Server deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7535-119">In this example Grafana, ElasticSearch, and Logstash are configured on an Ubuntu 16.04 LTS Server deployed in Azure.</span></span> <span data-ttu-id="f7535-120">This minimal setup is used for running all three components – they are all running on the same VM.</span><span class="sxs-lookup"><span data-stu-id="f7535-120">This minimal setup is used for running all three components – they are all running on the same VM.</span></span> <span data-ttu-id="f7535-121">This setup should only be used for testing and non-critical workloads.</span><span class="sxs-lookup"><span data-stu-id="f7535-121">This setup should only be used for testing and non-critical workloads.</span></span> <span data-ttu-id="f7535-122">Logstash, Elasticsearch, and Grafana can all be architected to scale independently across many instances.</span><span class="sxs-lookup"><span data-stu-id="f7535-122">Logstash, Elasticsearch, and Grafana can all be architected to scale independently across many instances.</span></span> <span data-ttu-id="f7535-123">For more information, see the documentation for each of these components.</span><span class="sxs-lookup"><span data-stu-id="f7535-123">For more information, see the documentation for each of these components.</span></span>

### <a name="install-logstash"></a><span data-ttu-id="f7535-124">Install Logstash</span><span class="sxs-lookup"><span data-stu-id="f7535-124">Install Logstash</span></span>

<span data-ttu-id="f7535-125">You use Logstash to flatten the JSON formatted flow logs to a flow tuple level.</span><span class="sxs-lookup"><span data-stu-id="f7535-125">You use Logstash to flatten the JSON formatted flow logs to a flow tuple level.</span></span>

1. <span data-ttu-id="f7535-126">To install Logstash, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="f7535-126">To install Logstash, run the following commands:</span></span>

    ```bash
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```

2. <span data-ttu-id="f7535-127">Configure Logstash to parse the flow logs and send them to ElasticSearch.</span><span class="sxs-lookup"><span data-stu-id="f7535-127">Configure Logstash to parse the flow logs and send them to ElasticSearch.</span></span> <span data-ttu-id="f7535-128">Create a Logstash.conf file using:</span><span class="sxs-lookup"><span data-stu-id="f7535-128">Create a Logstash.conf file using:</span></span>

    ```bash
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

3. <span data-ttu-id="f7535-129">Add the following content to the file.</span><span class="sxs-lookup"><span data-stu-id="f7535-129">Add the following content to the file.</span></span> <span data-ttu-id="f7535-130">Change the storage account name and access key to reflect your storage account details:</span><span class="sxs-lookup"><span data-stu-id="f7535-130">Change the storage account name and access key to reflect your storage account details:</span></span>

   ```bash
    input {
      azureblob
      {
        storage_account_name => "mystorageaccount"
        storage_access_key => "VGhpcyBpcyBhIGZha2Uga2V5Lg=="
        container => "insights-logs-networksecuritygroupflowevent"
        codec => "json"
        # Refer https://docs.microsoft.com/azure/network-watcher/network-watcher-read-nsg-flow-logs
        # Typical numbers could be 21/9 or 12/2 depends on the nsg log file types
        file_head_bytes => 12
        file_tail_bytes => 2
        # Enable / tweak these settings when event is too big for codec to handle.
        # break_json_down_policy => "with_head_tail"
        # break_json_batch_count => 2
      }
    }
    filter {
      split { field => "[records]" }
      split { field => "[records][properties][flows]"}
      split { field => "[records][properties][flows][flows]"}
      split { field => "[records][properties][flows][flows][flowTuples]"}

      mutate {
        split => { "[records][resourceId]" => "/"}
        add_field => { "Subscription" => "%{[records][resourceId][2]}"
          "ResourceGroup" => "%{[records][resourceId][4]}"
          "NetworkSecurityGroup" => "%{[records][resourceId][8]}" 
        }
        convert => {"Subscription" => "string"}
        convert => {"ResourceGroup" => "string"}
        convert => {"NetworkSecurityGroup" => "string"}
        split => { "[records][properties][flows][flows][flowTuples]" => "," }
        add_field => {
          "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
          "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
          "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
          "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
          "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
          "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
          "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
          "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
        }
        add_field => {
          "time" => "%{[records][time]}"
          "systemId" => "%{[records][systemId]}"
          "category" => "%{[records][category]}"
          "resourceId" => "%{[records][resourceId]}"
          "operationName" => "%{[records][operationName}}"
          "Version" => "%{[records][properties][Version}}"
          "rule" => "%{[records][properties][flows][rule]}"
          "mac" => "%{[records][properties][flows][flows][mac]}"
        }
        convert => {"unixtimestamp" => "integer"}
        convert => {"srcPort" => "integer"}
        convert => {"destPort" => "integer"}
        add_field => { "message" => "%{Message}" }        
      }
 
      date {
        match => ["unixtimestamp" , "UNIX"]
      }
    }
    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }
   ```

<span data-ttu-id="f7535-131">The Logstash config file provided is composed of three parts: the input, filter, and output.</span><span class="sxs-lookup"><span data-stu-id="f7535-131">The Logstash config file provided is composed of three parts: the input, filter, and output.</span></span>
<span data-ttu-id="f7535-132">The input section designates the input source of the logs that Logstash will process – in this case we are going to use an “azureblob” input plugin (installed in the next steps) that will allow us to access the NSG flow log JSON files stored in blob storage.</span><span class="sxs-lookup"><span data-stu-id="f7535-132">The input section designates the input source of the logs that Logstash will process – in this case we are going to use an “azureblob” input plugin (installed in the next steps) that will allow us to access the NSG flow log JSON files stored in blob storage.</span></span> 

<span data-ttu-id="f7535-133">The filter section then flattens each flow log file so that each individual flow tuple and its associated properties becomes a separate Logstash event.</span><span class="sxs-lookup"><span data-stu-id="f7535-133">The filter section then flattens each flow log file so that each individual flow tuple and its associated properties becomes a separate Logstash event.</span></span>

<span data-ttu-id="f7535-134">Finally, the output section forwards each Logstash event to the ElasticSearch server.</span><span class="sxs-lookup"><span data-stu-id="f7535-134">Finally, the output section forwards each Logstash event to the ElasticSearch server.</span></span> <span data-ttu-id="f7535-135">Feel free to modify the Logstash config file to suit your specific needs.</span><span class="sxs-lookup"><span data-stu-id="f7535-135">Feel free to modify the Logstash config file to suit your specific needs.</span></span>

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="f7535-136">Install the Logstash input plugin for Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="f7535-136">Install the Logstash input plugin for Azure Blob storage</span></span>

<span data-ttu-id="f7535-137">This Logstash plugin enables you to directly access the flow logs from their designated blob storage account.</span><span class="sxs-lookup"><span data-stu-id="f7535-137">This Logstash plugin enables you to directly access the flow logs from their designated blob storage account.</span></span> <span data-ttu-id="f7535-138">To install this plug in, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span><span class="sxs-lookup"><span data-stu-id="f7535-138">To install this plug in, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span></span>

```bash
cd /usr/share/logstash/bin
sudo ./logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="f7535-139">For more information about this plug in, see [Logstash input plugin for Azure Storage Blobs](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob).</span><span class="sxs-lookup"><span data-stu-id="f7535-139">For more information about this plug in, see [Logstash input plugin for Azure Storage Blobs](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob).</span></span>

### <a name="install-elasticsearch"></a><span data-ttu-id="f7535-140">Install ElasticSearch</span><span class="sxs-lookup"><span data-stu-id="f7535-140">Install ElasticSearch</span></span>

<span data-ttu-id="f7535-141">You can use the following script to install ElasticSearch.</span><span class="sxs-lookup"><span data-stu-id="f7535-141">You can use the following script to install ElasticSearch.</span></span> <span data-ttu-id="f7535-142">For information about installing ElasticSearch, see [Elastic Stack](https://www.elastic.co/guide/en/elastic-stack/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="f7535-142">For information about installing ElasticSearch, see [Elastic Stack](https://www.elastic.co/guide/en/elastic-stack/current/index.html).</span></span>

```bash
apt-get install apt-transport-https openjdk-8-jre-headless uuid-runtime pwgen -y
wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | apt-key add -
echo "deb https://packages.elastic.co/elasticsearch/5.x/debian stable main" | tee -a /etc/apt/sources.list.d/elasticsearch-5.x.list
apt-get update && apt-get install elasticsearch
sed -i s/#cluster.name:.*/cluster.name:\ grafana/ /etc/elasticsearch/elasticsearch.yml
systemctl daemon-reload
systemctl enable elasticsearch.service
systemctl start elasticsearch.service
```

### <a name="install-grafana"></a><span data-ttu-id="f7535-143">Install Grafana</span><span class="sxs-lookup"><span data-stu-id="f7535-143">Install Grafana</span></span>

<span data-ttu-id="f7535-144">To install and run Grafana, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="f7535-144">To install and run Grafana, run the following commands:</span></span>

```bash
wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana_4.5.1_amd64.deb
sudo apt-get install -y adduser libfontconfig
sudo dpkg -i grafana_4.5.1_amd64.deb
sudo service grafana-server start
```

<span data-ttu-id="f7535-145">For additional installation information, see [Installing on Debian / Ubuntu](http://docs.grafana.org/installation/debian/).</span><span class="sxs-lookup"><span data-stu-id="f7535-145">For additional installation information, see [Installing on Debian / Ubuntu](http://docs.grafana.org/installation/debian/).</span></span>

#### <a name="add-the-elasticsearch-server-as-a-data-source"></a><span data-ttu-id="f7535-146">Add the ElasticSearch server as a data source</span><span class="sxs-lookup"><span data-stu-id="f7535-146">Add the ElasticSearch server as a data source</span></span>

<span data-ttu-id="f7535-147">Next, you need to add the ElasticSearch index containing flow logs as a data source.</span><span class="sxs-lookup"><span data-stu-id="f7535-147">Next, you need to add the ElasticSearch index containing flow logs as a data source.</span></span> <span data-ttu-id="f7535-148">You can add a data source by selecting **Add data source** and completing the form with the relevant information.</span><span class="sxs-lookup"><span data-stu-id="f7535-148">You can add a data source by selecting **Add data source** and completing the form with the relevant information.</span></span> <span data-ttu-id="f7535-149">A sample of this configuration can be found in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="f7535-149">A sample of this configuration can be found in the following screenshot:</span></span>

![Add data source](./media/network-watcher-nsg-grafana/network-watcher-nsg-grafana-fig2.png)

#### <a name="create-a-dashboard"></a><span data-ttu-id="f7535-151">Create a dashboard</span><span class="sxs-lookup"><span data-stu-id="f7535-151">Create a dashboard</span></span>

<span data-ttu-id="f7535-152">Now that you have successfully configured Grafana to read from the ElasticSearch index containing NSG flow logs, you can create and personalize dashboards.</span><span class="sxs-lookup"><span data-stu-id="f7535-152">Now that you have successfully configured Grafana to read from the ElasticSearch index containing NSG flow logs, you can create and personalize dashboards.</span></span> <span data-ttu-id="f7535-153">To create a new dashboard, select **Create your first dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f7535-153">To create a new dashboard, select **Create your first dashboard**.</span></span> <span data-ttu-id="f7535-154">The following sample graph configuration shows flows segmented by NSG rule:</span><span class="sxs-lookup"><span data-stu-id="f7535-154">The following sample graph configuration shows flows segmented by NSG rule:</span></span>

![Dashboard graph](./media/network-watcher-nsg-grafana/network-watcher-nsg-grafana-fig3.png)

<span data-ttu-id="f7535-156">The following screenshot depicts a graph and chart showing the top flows and their frequency.</span><span class="sxs-lookup"><span data-stu-id="f7535-156">The following screenshot depicts a graph and chart showing the top flows and their frequency.</span></span> <span data-ttu-id="f7535-157">Flows are also shown by NSG rule and flows by decision.</span><span class="sxs-lookup"><span data-stu-id="f7535-157">Flows are also shown by NSG rule and flows by decision.</span></span> <span data-ttu-id="f7535-158">Grafana is highly customizable so it's advisable that you create dashboards to suit your specific monitoring needs.</span><span class="sxs-lookup"><span data-stu-id="f7535-158">Grafana is highly customizable so it's advisable that you create dashboards to suit your specific monitoring needs.</span></span> <span data-ttu-id="f7535-159">The following example shows a typical dashboard:</span><span class="sxs-lookup"><span data-stu-id="f7535-159">The following example shows a typical dashboard:</span></span>

![Dashboard graph](./media/network-watcher-nsg-grafana/network-watcher-nsg-grafana-fig4.png)

## <a name="conclusion"></a><span data-ttu-id="f7535-161">Conclusion</span><span class="sxs-lookup"><span data-stu-id="f7535-161">Conclusion</span></span>

<span data-ttu-id="f7535-162">By integrating Network Watcher with ElasticSearch and Grafana, you now have a convenient and centralized way to manage and visualize NSG flow logs as well as other data.</span><span class="sxs-lookup"><span data-stu-id="f7535-162">By integrating Network Watcher with ElasticSearch and Grafana, you now have a convenient and centralized way to manage and visualize NSG flow logs as well as other data.</span></span> <span data-ttu-id="f7535-163">Grafana has a number of other powerful graphing features that can also be used to further manage flow logs and better understand your network traffic.</span><span class="sxs-lookup"><span data-stu-id="f7535-163">Grafana has a number of other powerful graphing features that can also be used to further manage flow logs and better understand your network traffic.</span></span> <span data-ttu-id="f7535-164">Now that you have a Grafana instance set up and connected to Azure, feel free to continue to explore the other functionality that it offers.</span><span class="sxs-lookup"><span data-stu-id="f7535-164">Now that you have a Grafana instance set up and connected to Azure, feel free to continue to explore the other functionality that it offers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7535-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7535-165">Next steps</span></span>

- <span data-ttu-id="f7535-166">Learn more about using [Network Watcher](network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7535-166">Learn more about using [Network Watcher](network-watcher-monitoring-overview.md).</span></span>

