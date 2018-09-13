---
title: Visualize Azure Network Watcher NSG flow logs using open source tools | Microsoft Docs
description: This page describes how to use open source tools to visualize NSG flow logs.
services: network-watcher
documentationcenter: na
author: mattreatMSFT
manager: vitinnan
editor: ''
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: mareat
ms.openlocfilehash: aa83ba1f428e70cd78cba2af6d39989179d5b30f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44789274"
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="7ed3d-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span><span class="sxs-lookup"><span data-stu-id="7ed3d-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="7ed3d-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="7ed3d-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="7ed3d-106">These flow logs can be difficult to manually parse and gain insights from.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-106">These flow logs can be difficult to manually parse and gain insights from.</span></span> <span data-ttu-id="7ed3d-107">However, there are several open source tools that can help visualize this data.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="7ed3d-108">This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-108">This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="7ed3d-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="7ed3d-109">Scenario</span></span>

<span data-ttu-id="7ed3d-110">In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-110">In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.</span></span>  <span data-ttu-id="7ed3d-111">A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-111">A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs.</span></span> <span data-ttu-id="7ed3d-112">Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-112">Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.</span></span>

![scenario][scenario]

## <a name="steps"></a><span data-ttu-id="7ed3d-114">Steps</span><span class="sxs-lookup"><span data-stu-id="7ed3d-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="7ed3d-115">Enable Network Security Group flow logging</span><span class="sxs-lookup"><span data-stu-id="7ed3d-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="7ed3d-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="7ed3d-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7ed3d-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="7ed3d-118">Set up the Elastic Stack</span><span class="sxs-lookup"><span data-stu-id="7ed3d-118">Set up the Elastic Stack</span></span>
<span data-ttu-id="7ed3d-119">By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-119">By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="7ed3d-120">Install Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="7ed3d-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="7ed3d-121">The Elastic Stack from version 5.0 and above requires Java 8.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-121">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="7ed3d-122">Run the command `java -version` to check your version.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-122">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="7ed3d-123">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html).</span><span class="sxs-lookup"><span data-stu-id="7ed3d-123">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html).</span></span>
2. <span data-ttu-id="7ed3d-124">Download the correct binary package for your system:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-124">Download the correct binary package for your system:</span></span>

   ```bash
   curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
   sudo dpkg -i elasticsearch-5.2.0.deb
   sudo /etc/init.d/elasticsearch start
   ```

   <span data-ttu-id="7ed3d-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="7ed3d-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

3. <span data-ttu-id="7ed3d-126">Verify that Elasticsearch is running with the command:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-126">Verify that Elasticsearch is running with the command:</span></span>

    ```bash
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="7ed3d-127">You should see a response similar to this:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-127">You should see a response similar to this:</span></span>

    ```json
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

<span data-ttu-id="7ed3d-128">For further instructions on installing Elastic search, refer to [Installation instructions](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html).</span><span class="sxs-lookup"><span data-stu-id="7ed3d-128">For further instructions on installing Elastic search, refer to [Installation instructions](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html).</span></span>

### <a name="install-logstash"></a><span data-ttu-id="7ed3d-129">Install Logstash</span><span class="sxs-lookup"><span data-stu-id="7ed3d-129">Install Logstash</span></span>

1. <span data-ttu-id="7ed3d-130">To install Logstash run the following commands:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-130">To install Logstash run the following commands:</span></span>

    ```bash
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
2. <span data-ttu-id="7ed3d-131">Next we need to configure Logstash to access and parse the flow logs.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-131">Next we need to configure Logstash to access and parse the flow logs.</span></span> <span data-ttu-id="7ed3d-132">Create a logstash.conf file using:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-132">Create a logstash.conf file using:</span></span>

    ```bash
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

3. <span data-ttu-id="7ed3d-133">Add the following content to the file:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-133">Add the following content to the file:</span></span>

   ```
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

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
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
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
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

<span data-ttu-id="7ed3d-134">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html).</span><span class="sxs-lookup"><span data-stu-id="7ed3d-134">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html).</span></span>

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="7ed3d-135">Install the Logstash input plugin for Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="7ed3d-135">Install the Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="7ed3d-136">This Logstash plugin will allow you to directly access the flow logs from their designated storage account.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-136">This Logstash plugin will allow you to directly access the flow logs from their designated storage account.</span></span> <span data-ttu-id="7ed3d-137">To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-137">To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span></span>

```bash
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="7ed3d-138">To start Logstash run the command:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-138">To start Logstash run the command:</span></span>

```bash
sudo /etc/init.d/logstash start
```

<span data-ttu-id="7ed3d-139">For more information about this plugin, refer to the [documentation](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob).</span><span class="sxs-lookup"><span data-stu-id="7ed3d-139">For more information about this plugin, refer to the [documentation](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob).</span></span>

### <a name="install-kibana"></a><span data-ttu-id="7ed3d-140">Install Kibana</span><span class="sxs-lookup"><span data-stu-id="7ed3d-140">Install Kibana</span></span>

1. <span data-ttu-id="7ed3d-141">Run the following commands to install Kibana:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-141">Run the following commands to install Kibana:</span></span>

   ```bash
   curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
   tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
   ```

2. <span data-ttu-id="7ed3d-142">To run Kibana use the commands:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-142">To run Kibana use the commands:</span></span>

   ```bash
   cd kibana-5.2.0-linux-x86_64/
   ./bin/kibana
   ```

3. <span data-ttu-id="7ed3d-143">To view your Kibana web interface, navigate to `http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="7ed3d-143">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
4. <span data-ttu-id="7ed3d-144">For this scenario, the index pattern used for the flow logs is "nsg-flow-logs".</span><span class="sxs-lookup"><span data-stu-id="7ed3d-144">For this scenario, the index pattern used for the flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="7ed3d-145">You may change the index pattern in the "output" section of your logstash.conf file.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-145">You may change the index pattern in the "output" section of your logstash.conf file.</span></span>
5. <span data-ttu-id="7ed3d-146">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-146">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="7ed3d-147">Create a Kibana dashboard</span><span class="sxs-lookup"><span data-stu-id="7ed3d-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="7ed3d-148">A sample dashboard to view trends and details in your alerts is shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-148">A sample dashboard to view trends and details in your alerts is shown in the following picture:</span></span>

![figure 1][1]

<span data-ttu-id="7ed3d-150">Download the [dashboard file](https://aka.ms/networkwatchernsgflowlogdashboard), the [visualization file](https://aka.ms/networkwatchernsgflowlogvisualizations), and the [saved search file](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="7ed3d-150">Download the [dashboard file](https://aka.ms/networkwatchernsgflowlogdashboard), the [visualization file](https://aka.ms/networkwatchernsgflowlogvisualizations), and the [saved search file](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

<span data-ttu-id="7ed3d-151">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-151">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="7ed3d-152">Then from the **Dashboard** tab you can open and load the sample dashboard.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-152">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="7ed3d-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="7ed3d-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="7ed3d-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="7ed3d-155">Visualize NSG flow logs</span><span class="sxs-lookup"><span data-stu-id="7ed3d-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="7ed3d-156">The sample dashboard provides several visualizations of the flow logs:</span><span class="sxs-lookup"><span data-stu-id="7ed3d-156">The sample dashboard provides several visualizations of the flow logs:</span></span>

1. <span data-ttu-id="7ed3d-157">Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-157">Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period.</span></span> <span data-ttu-id="7ed3d-158">You can edit the unit of time and span of both these visualizations.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-158">You can edit the unit of time and span of both these visualizations.</span></span> <span data-ttu-id="7ed3d-159">Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-159">Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="7ed3d-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

   ![figure2][2]

2. <span data-ttu-id="7ed3d-162">Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-162">Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports.</span></span> <span data-ttu-id="7ed3d-163">With this view you can see your most commonly used ports.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="7ed3d-164">If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-164">If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.</span></span>

   ![figure3][3]

3. <span data-ttu-id="7ed3d-166">Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-166">Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.</span></span>

   ![figure4][4]

4. <span data-ttu-id="7ed3d-168">Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-168">Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG.</span></span> <span data-ttu-id="7ed3d-169">From here you can see which NSG and rules generated the most traffic.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-169">From here you can see which NSG and rules generated the most traffic.</span></span>

   ![figure5][5]

5. <span data-ttu-id="7ed3d-171">Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-171">Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs.</span></span> <span data-ttu-id="7ed3d-172">You can adjust these charts to show more or less top IPs.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-172">You can adjust these charts to show more or less top IPs.</span></span> <span data-ttu-id="7ed3d-173">From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-173">From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.</span></span>

   ![figure6][6]

6. <span data-ttu-id="7ed3d-175">Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-175">Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

   ![figure7][7]

<span data-ttu-id="7ed3d-177">Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-177">Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="7ed3d-178">For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="7ed3d-178">For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="7ed3d-179">Conclusion</span><span class="sxs-lookup"><span data-stu-id="7ed3d-179">Conclusion</span></span>

<span data-ttu-id="7ed3d-180">By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-180">By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic.</span></span> <span data-ttu-id="7ed3d-181">These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-181">These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="7ed3d-182">Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.</span><span class="sxs-lookup"><span data-stu-id="7ed3d-182">Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ed3d-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ed3d-183">Next steps</span></span>

<span data-ttu-id="7ed3d-184">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="7ed3d-184">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
