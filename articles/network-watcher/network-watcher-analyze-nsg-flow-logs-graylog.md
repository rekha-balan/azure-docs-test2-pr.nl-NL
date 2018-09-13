---
title: Analyze Azure network security group flow logs - Graylog | Microsoft Docs
description: Learn how to manage and analyze network security group flow logs in Azure using Network Watcher and Graylog.
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
ms.date: 09/19/2017
ms.author: mareat
ms.openlocfilehash: db3b08ae8092661e6ffa0f2dd7e460f341a8d013
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868437"
---
# <a name="manage-and-analyze-network-security-group-flow-logs-in-azure-using-network-watcher-and-graylog"></a><span data-ttu-id="25136-103">Manage and analyze network security group flow logs in Azure using Network Watcher and Graylog</span><span class="sxs-lookup"><span data-stu-id="25136-103">Manage and analyze network security group flow logs in Azure using Network Watcher and Graylog</span></span>

<span data-ttu-id="25136-104">[Network security group flow logs](network-watcher-nsg-flow-logging-overview.md) provide information that you can use to understand ingress and egress IP traffic for Azure network interfaces.</span><span class="sxs-lookup"><span data-stu-id="25136-104">[Network security group flow logs](network-watcher-nsg-flow-logging-overview.md) provide information that you can use to understand ingress and egress IP traffic for Azure network interfaces.</span></span> <span data-ttu-id="25136-105">Flow logs show outbound and inbound flows on a per network security group rule basis, the network interface the flow applies to, 5-tuple information (Source/Destination IP, Source/Destination Port, Protocol) about the flow, and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="25136-105">Flow logs show outbound and inbound flows on a per network security group rule basis, the network interface the flow applies to, 5-tuple information (Source/Destination IP, Source/Destination Port, Protocol) about the flow, and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="25136-106">You can have many network security groups in your network with flow logging enabled.</span><span class="sxs-lookup"><span data-stu-id="25136-106">You can have many network security groups in your network with flow logging enabled.</span></span> <span data-ttu-id="25136-107">Several network security groups with flow logging enabled can make it cumbersome to parse and gain insights from your logs.</span><span class="sxs-lookup"><span data-stu-id="25136-107">Several network security groups with flow logging enabled can make it cumbersome to parse and gain insights from your logs.</span></span> <span data-ttu-id="25136-108">This article provides a solution to centrally manage these network security group flow logs using Graylog, an open source log management and analysis tool, and Logstash, an open source server-side data processing pipeline.</span><span class="sxs-lookup"><span data-stu-id="25136-108">This article provides a solution to centrally manage these network security group flow logs using Graylog, an open source log management and analysis tool, and Logstash, an open source server-side data processing pipeline.</span></span>

## <a name="scenario"></a><span data-ttu-id="25136-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="25136-109">Scenario</span></span>

<span data-ttu-id="25136-110">Network security group flow logs are enabled using Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="25136-110">Network security group flow logs are enabled using Network Watcher.</span></span> <span data-ttu-id="25136-111">Flow logs flow in to Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="25136-111">Flow logs flow in to Azure blob storage.</span></span> <span data-ttu-id="25136-112">A Logstash plugin is used to connect and process flow logs from blob storage and send them to Graylog.</span><span class="sxs-lookup"><span data-stu-id="25136-112">A Logstash plugin is used to connect and process flow logs from blob storage and send them to Graylog.</span></span> <span data-ttu-id="25136-113">Once the flow logs are stored in Graylog, they can be analyzed and visualized into customized dashboards.</span><span class="sxs-lookup"><span data-stu-id="25136-113">Once the flow logs are stored in Graylog, they can be analyzed and visualized into customized dashboards.</span></span>

![Graylog workflow](./media/network-watcher-analyze-nsg-flow-logs-graylog/workflow.png)

## <a name="installation-steps"></a><span data-ttu-id="25136-115">Installation Steps</span><span class="sxs-lookup"><span data-stu-id="25136-115">Installation Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="25136-116">Enable network security group flow logging</span><span class="sxs-lookup"><span data-stu-id="25136-116">Enable network security group flow logging</span></span>

<span data-ttu-id="25136-117">For this scenario, you must have network security group flow logging enabled on at least one network security group in your account.</span><span class="sxs-lookup"><span data-stu-id="25136-117">For this scenario, you must have network security group flow logging enabled on at least one network security group in your account.</span></span> <span data-ttu-id="25136-118">For instructions on enabling network security group flow logs, refer to the following article [Introduction to flow logging for network security groups](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25136-118">For instructions on enabling network security group flow logs, refer to the following article [Introduction to flow logging for network security groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

### <a name="setting-up-graylog"></a><span data-ttu-id="25136-119">Setting up Graylog</span><span class="sxs-lookup"><span data-stu-id="25136-119">Setting up Graylog</span></span>

<span data-ttu-id="25136-120">In this example, both Graylog and Logstash are configured on an Ubuntu 14.04 Server, deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="25136-120">In this example, both Graylog and Logstash are configured on an Ubuntu 14.04 Server, deployed in Azure.</span></span>

- <span data-ttu-id="25136-121">Refer to the [documentation](http://docs.graylog.org/en/2.2/pages/installation/os/ubuntu.html) from Graylog, for step by step instructions on how install onto Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="25136-121">Refer to the [documentation](http://docs.graylog.org/en/2.2/pages/installation/os/ubuntu.html) from Graylog, for step by step instructions on how install onto Ubuntu.</span></span>
- <span data-ttu-id="25136-122">Make sure to also configure the Graylog web interface by following the [documentation](http://docs.graylog.org/en/2.2/pages/configuration/web_interface.html#configuring-webif).</span><span class="sxs-lookup"><span data-stu-id="25136-122">Make sure to also configure the Graylog web interface by following the [documentation](http://docs.graylog.org/en/2.2/pages/configuration/web_interface.html#configuring-webif).</span></span>

<span data-ttu-id="25136-123">This example uses the minimum Graylog setup (i.e</span><span class="sxs-lookup"><span data-stu-id="25136-123">This example uses the minimum Graylog setup (i.e</span></span> <span data-ttu-id="25136-124">a single instance of a Graylog), but Graylog can be architected to scale across resources depending on your system and production needs.</span><span class="sxs-lookup"><span data-stu-id="25136-124">a single instance of a Graylog), but Graylog can be architected to scale across resources depending on your system and production needs.</span></span> <span data-ttu-id="25136-125">For more information on architectural considerations or a deep architectural guide, see Graylog’s [documentation](http://docs.graylog.org/en/2.2/pages/architecture.html) and [architectural guide](https://www.slideshare.net/Graylog/graylog-engineering-design-your-architecture).</span><span class="sxs-lookup"><span data-stu-id="25136-125">For more information on architectural considerations or a deep architectural guide, see Graylog’s [documentation](http://docs.graylog.org/en/2.2/pages/architecture.html) and [architectural guide](https://www.slideshare.net/Graylog/graylog-engineering-design-your-architecture).</span></span>

<span data-ttu-id="25136-126">Graylog can be installed in many ways, depending on your platform and preferences.</span><span class="sxs-lookup"><span data-stu-id="25136-126">Graylog can be installed in many ways, depending on your platform and preferences.</span></span> <span data-ttu-id="25136-127">For a full list of possible installation methods, refer to Graylog's official [documentation](http://docs.graylog.org/en/2.2/pages/installation.html).</span><span class="sxs-lookup"><span data-stu-id="25136-127">For a full list of possible installation methods, refer to Graylog's official [documentation](http://docs.graylog.org/en/2.2/pages/installation.html).</span></span> <span data-ttu-id="25136-128">The Graylog server application runs on Linux distributions and has the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="25136-128">The Graylog server application runs on Linux distributions and has the following prerequisites:</span></span>

-  <span data-ttu-id="25136-129">Oracle Java SE 8 or later – [Oracle’s installation documentation](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="25136-129">Oracle Java SE 8 or later – [Oracle’s installation documentation](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
-  <span data-ttu-id="25136-130">Elastic Search 2.x (2.1.0 or later) - [Elasticsearch installation documentation](https://www.elastic.co/guide/en/elasticsearch/reference/2.4/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="25136-130">Elastic Search 2.x (2.1.0 or later) - [Elasticsearch installation documentation](https://www.elastic.co/guide/en/elasticsearch/reference/2.4/_installation.html)</span></span>
-  <span data-ttu-id="25136-131">MongoDB 2.4 or later – [MongoDB installation documentation](https://docs.mongodb.com/manual/administration/install-on-linux/)</span><span class="sxs-lookup"><span data-stu-id="25136-131">MongoDB 2.4 or later – [MongoDB installation documentation](https://docs.mongodb.com/manual/administration/install-on-linux/)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="25136-132">Install Logstash</span><span class="sxs-lookup"><span data-stu-id="25136-132">Install Logstash</span></span>

<span data-ttu-id="25136-133">Logstash is used to flatten the JSON formatted flow logs to a flow tuple level.</span><span class="sxs-lookup"><span data-stu-id="25136-133">Logstash is used to flatten the JSON formatted flow logs to a flow tuple level.</span></span> <span data-ttu-id="25136-134">Flattening the flow logs makes the logs easier to organize and search in Graylog.</span><span class="sxs-lookup"><span data-stu-id="25136-134">Flattening the flow logs makes the logs easier to organize and search in Graylog.</span></span>

1. <span data-ttu-id="25136-135">To install Logstash, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="25136-135">To install Logstash, run the following commands:</span></span>

   ```bash
   curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
   sudo dpkg -i logstash-5.2.0.deb
   ```

2. <span data-ttu-id="25136-136">Configure Logstash to parse the flow logs and send them to Graylog.</span><span class="sxs-lookup"><span data-stu-id="25136-136">Configure Logstash to parse the flow logs and send them to Graylog.</span></span> <span data-ttu-id="25136-137">Create a Logstash.conf file:</span><span class="sxs-lookup"><span data-stu-id="25136-137">Create a Logstash.conf file:</span></span>

   ```bash
   sudo touch /etc/logstash/conf.d/logstash.conf
   ```

3. <span data-ttu-id="25136-138">Add the following content to the file.</span><span class="sxs-lookup"><span data-stu-id="25136-138">Add the following content to the file.</span></span> <span data-ttu-id="25136-139">Change the highlighted values to reflect your storage account details:</span><span class="sxs-lookup"><span data-stu-id="25136-139">Change the highlighted values to reflect your storage account details:</span></span>

   ```
    input {
        azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "NrUZmx7pJSKaRJzvQbeiZWi5nBRWOTr7Wwr9DrvK7YtDBrADYxT1y0oEExtSlkDnGRt7qcRiZzEBCCyRYND8SxSt"
            container => "insights-logs-networksecuritygroupflowevent"
            registry_create_policy => "start_over"
            codec => "json"
            file_head_bytes => 21
            file_tail_bytes => 9
            # Possible options: `do_not_break`, `with_head_tail`, `without_head_tail`
            break_json_down_policy  => 'with_head_tail'
            break_json_batch_count => 2
            interval => 5
        }
    }
    
    filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"
    }
    
     mutate {
        split => { "[records][resourceId]" => "/"}
        add_field =>{
                    "Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"
        }
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
        udp {
            host => "127.0.0.1"
            port => 12201
        }
    }
    ```
<span data-ttu-id="25136-140">The Logstash config file provided is composed of three parts: the input, filter, and output.</span><span class="sxs-lookup"><span data-stu-id="25136-140">The Logstash config file provided is composed of three parts: the input, filter, and output.</span></span> <span data-ttu-id="25136-141">The input section designates the input source of the logs that Logstash will process – in this case, you are going to use an Azure blog input plugin (installed in the next steps) that allows us to access the network security group flow log JSON files stored in blob storage.</span><span class="sxs-lookup"><span data-stu-id="25136-141">The input section designates the input source of the logs that Logstash will process – in this case, you are going to use an Azure blog input plugin (installed in the next steps) that allows us to access the network security group flow log JSON files stored in blob storage.</span></span>

<span data-ttu-id="25136-142">The filter section then flattens each flow log file so that each individual flow tuple and its associated properties becomes a separate Logstash event.</span><span class="sxs-lookup"><span data-stu-id="25136-142">The filter section then flattens each flow log file so that each individual flow tuple and its associated properties becomes a separate Logstash event.</span></span>

<span data-ttu-id="25136-143">Finally, the output section forwards each Logstash event to the Graylog server.</span><span class="sxs-lookup"><span data-stu-id="25136-143">Finally, the output section forwards each Logstash event to the Graylog server.</span></span> <span data-ttu-id="25136-144">To suit your specific needs, modify the Logstash config file, as required.</span><span class="sxs-lookup"><span data-stu-id="25136-144">To suit your specific needs, modify the Logstash config file, as required.</span></span>

   > [!NOTE]
   > <span data-ttu-id="25136-145">The previous config file assumes that the Graylog server has been configured on the local host loopback IP address 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="25136-145">The previous config file assumes that the Graylog server has been configured on the local host loopback IP address 127.0.0.1.</span></span> <span data-ttu-id="25136-146">If not, be sure to change the host parameter in the output section to the correct IP address.</span><span class="sxs-lookup"><span data-stu-id="25136-146">If not, be sure to change the host parameter in the output section to the correct IP address.</span></span>

<span data-ttu-id="25136-147">For further instructions on installing Logstash, see the Logstash [documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html).</span><span class="sxs-lookup"><span data-stu-id="25136-147">For further instructions on installing Logstash, see the Logstash [documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html).</span></span>

### <a name="install-the-logstash-input-plug-in-for-azure-blob-storage"></a><span data-ttu-id="25136-148">Install the Logstash input plug-in for Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="25136-148">Install the Logstash input plug-in for Azure blob storage</span></span>

<span data-ttu-id="25136-149">The Logstash plugin allows you to directly access the flow logs from their designated blob storage account.</span><span class="sxs-lookup"><span data-stu-id="25136-149">The Logstash plugin allows you to directly access the flow logs from their designated blob storage account.</span></span> <span data-ttu-id="25136-150">To install the plug-in, from the default Logstash installation directory (in this case /usr/share/logstash/bin), run the following command:</span><span class="sxs-lookup"><span data-stu-id="25136-150">To install the plug-in, from the default Logstash installation directory (in this case /usr/share/logstash/bin), run the following command:</span></span>

```bash
cd /usr/share/logstash/bin
sudo ./logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="25136-151">For more information about this plug in, see the [documentation](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob).</span><span class="sxs-lookup"><span data-stu-id="25136-151">For more information about this plug in, see the [documentation](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob).</span></span>

### <a name="set-up-connection-from-logstash-to-graylog"></a><span data-ttu-id="25136-152">Set up connection from Logstash to Graylog</span><span class="sxs-lookup"><span data-stu-id="25136-152">Set up connection from Logstash to Graylog</span></span>

<span data-ttu-id="25136-153">Now that you have established a connection to the flow logs using Logstash and set up the Graylog server, you need to configure Graylog to accept the incoming log files.</span><span class="sxs-lookup"><span data-stu-id="25136-153">Now that you have established a connection to the flow logs using Logstash and set up the Graylog server, you need to configure Graylog to accept the incoming log files.</span></span>

1. <span data-ttu-id="25136-154">Navigate to your Graylog Server web interface using the URL you configured for it.</span><span class="sxs-lookup"><span data-stu-id="25136-154">Navigate to your Graylog Server web interface using the URL you configured for it.</span></span> <span data-ttu-id="25136-155">You can access the interface by directing your browser to `http://<graylog-server-ip>:9000/`</span><span class="sxs-lookup"><span data-stu-id="25136-155">You can access the interface by directing your browser to `http://<graylog-server-ip>:9000/`</span></span>

2. <span data-ttu-id="25136-156">To navigate to the configuration page, select the **System** drop-down menu in the top navigation bar to the right, and then click **Inputs**.</span><span class="sxs-lookup"><span data-stu-id="25136-156">To navigate to the configuration page, select the **System** drop-down menu in the top navigation bar to the right, and then click **Inputs**.</span></span>
   <span data-ttu-id="25136-157">Alternatively, navigate to `http://<graylog-server-ip>:9000/system/inputs`</span><span class="sxs-lookup"><span data-stu-id="25136-157">Alternatively, navigate to `http://<graylog-server-ip>:9000/system/inputs`</span></span>

   ![Getting started](./media/network-watcher-analyze-nsg-flow-logs-graylog/getting-started.png)

3. <span data-ttu-id="25136-159">To launch the new input, select *GELF UDP* in the **Select input** drop-down, and then fill out the form.</span><span class="sxs-lookup"><span data-stu-id="25136-159">To launch the new input, select *GELF UDP* in the **Select input** drop-down, and then fill out the form.</span></span> <span data-ttu-id="25136-160">GELF stands for Graylog Extended Log Format.</span><span class="sxs-lookup"><span data-stu-id="25136-160">GELF stands for Graylog Extended Log Format.</span></span> <span data-ttu-id="25136-161">The GELF format is developed by Graylog.</span><span class="sxs-lookup"><span data-stu-id="25136-161">The GELF format is developed by Graylog.</span></span> <span data-ttu-id="25136-162">To learn more about its advantages, see the Graylog [documentation](http://docs.graylog.org/en/2.2/pages/gelf.html).</span><span class="sxs-lookup"><span data-stu-id="25136-162">To learn more about its advantages, see the Graylog [documentation](http://docs.graylog.org/en/2.2/pages/gelf.html).</span></span>

   <span data-ttu-id="25136-163">Make sure to bind the input to the IP you configured your Graylog server on.</span><span class="sxs-lookup"><span data-stu-id="25136-163">Make sure to bind the input to the IP you configured your Graylog server on.</span></span> <span data-ttu-id="25136-164">The IP address should match the **host** field of the UDP output of the Logstash configuration file.</span><span class="sxs-lookup"><span data-stu-id="25136-164">The IP address should match the **host** field of the UDP output of the Logstash configuration file.</span></span> <span data-ttu-id="25136-165">The default port should be *12201*.</span><span class="sxs-lookup"><span data-stu-id="25136-165">The default port should be *12201*.</span></span> <span data-ttu-id="25136-166">Ensure the port matches the **port** field in the UDP output designated in the Logstash config file.</span><span class="sxs-lookup"><span data-stu-id="25136-166">Ensure the port matches the **port** field in the UDP output designated in the Logstash config file.</span></span>

   ![Inputs](./media/network-watcher-analyze-nsg-flow-logs-graylog/inputs.png)

   <span data-ttu-id="25136-168">Once you launch the input, you should see it appear under the **Local inputs** section, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="25136-168">Once you launch the input, you should see it appear under the **Local inputs** section, as shown in the following picture:</span></span>

   ![](./media/network-watcher-analyze-nsg-flow-logs-graylog/local-inputs.png)

   <span data-ttu-id="25136-169">To learn more about Graylog message inputs, refer to the [documentation](http://docs.graylog.org/en/2.2/pages/sending_data.html#what-are-graylog-message-inputs).</span><span class="sxs-lookup"><span data-stu-id="25136-169">To learn more about Graylog message inputs, refer to the [documentation](http://docs.graylog.org/en/2.2/pages/sending_data.html#what-are-graylog-message-inputs).</span></span>

4. <span data-ttu-id="25136-170">Once these configurations have been made, you can start Logstash to begin reading in flow logs with the following command: `sudo systemctl start logstash.service`.</span><span class="sxs-lookup"><span data-stu-id="25136-170">Once these configurations have been made, you can start Logstash to begin reading in flow logs with the following command: `sudo systemctl start logstash.service`.</span></span>

### <a name="search-through-graylog-messages"></a><span data-ttu-id="25136-171">Search through Graylog messages</span><span class="sxs-lookup"><span data-stu-id="25136-171">Search through Graylog messages</span></span>

<span data-ttu-id="25136-172">After allowing some time for your Graylog server to collect messages, you are able to search through the messages.</span><span class="sxs-lookup"><span data-stu-id="25136-172">After allowing some time for your Graylog server to collect messages, you are able to search through the messages.</span></span> <span data-ttu-id="25136-173">To check the messages being sent to your Graylog server, from the **Inputs** configuration page click the “**Show received messages**” button of the GELF UDP input you created.</span><span class="sxs-lookup"><span data-stu-id="25136-173">To check the messages being sent to your Graylog server, from the **Inputs** configuration page click the “**Show received messages**” button of the GELF UDP input you created.</span></span> <span data-ttu-id="25136-174">You are directed to a screen that looks similar to the following picture:</span><span class="sxs-lookup"><span data-stu-id="25136-174">You are directed to a screen that looks similar to the following picture:</span></span> 

![Histogram](./media/network-watcher-analyze-nsg-flow-logs-graylog/histogram.png)

<span data-ttu-id="25136-176">Clicking on the blue “%{Message}” link expands each message to show the parameters of each flow tuple, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="25136-176">Clicking on the blue “%{Message}” link expands each message to show the parameters of each flow tuple, as shown in the following picture:</span></span>

![Messages](./media/network-watcher-analyze-nsg-flow-logs-graylog/messages.png)

<span data-ttu-id="25136-178">By default, all message fields are included in the search if you don’t select a specific message field to search for.</span><span class="sxs-lookup"><span data-stu-id="25136-178">By default, all message fields are included in the search if you don’t select a specific message field to search for.</span></span> <span data-ttu-id="25136-179">If you want to search for specific messages (i.e</span><span class="sxs-lookup"><span data-stu-id="25136-179">If you want to search for specific messages (i.e</span></span> <span data-ttu-id="25136-180">– flow tuples from a specific source IP) you can use the Graylog search query language as [documented](http://docs.graylog.org/en/2.2/pages/queries.html)</span><span class="sxs-lookup"><span data-stu-id="25136-180">– flow tuples from a specific source IP) you can use the Graylog search query language as [documented](http://docs.graylog.org/en/2.2/pages/queries.html)</span></span>

## <a name="analyze-network-security-group-flow-logs-using-graylog"></a><span data-ttu-id="25136-181">Analyze network security group flow logs using Graylog</span><span class="sxs-lookup"><span data-stu-id="25136-181">Analyze network security group flow logs using Graylog</span></span>

<span data-ttu-id="25136-182">Now that Graylog it set up running, you can use some of its functionality to better understand your flow log data.</span><span class="sxs-lookup"><span data-stu-id="25136-182">Now that Graylog it set up running, you can use some of its functionality to better understand your flow log data.</span></span> <span data-ttu-id="25136-183">One such way is by using dashboards to create specific views of your data.</span><span class="sxs-lookup"><span data-stu-id="25136-183">One such way is by using dashboards to create specific views of your data.</span></span>

### <a name="create-a-dashboard"></a><span data-ttu-id="25136-184">Create a dashboard</span><span class="sxs-lookup"><span data-stu-id="25136-184">Create a dashboard</span></span>

1. <span data-ttu-id="25136-185">In the top navigation bar, select **Dashboards** or navigate to `http://<graylog-server-ip>:9000/dashboards/`</span><span class="sxs-lookup"><span data-stu-id="25136-185">In the top navigation bar, select **Dashboards** or navigate to `http://<graylog-server-ip>:9000/dashboards/`</span></span>

2. <span data-ttu-id="25136-186">From there, click the green **Create dashboard** button and fill out the short form with the title and description of your dashboard.</span><span class="sxs-lookup"><span data-stu-id="25136-186">From there, click the green **Create dashboard** button and fill out the short form with the title and description of your dashboard.</span></span> <span data-ttu-id="25136-187">Hit the **Save** button to create the new dashboard.</span><span class="sxs-lookup"><span data-stu-id="25136-187">Hit the **Save** button to create the new dashboard.</span></span> <span data-ttu-id="25136-188">You see a dashboard similar to the following picture:</span><span class="sxs-lookup"><span data-stu-id="25136-188">You see a dashboard similar to the following picture:</span></span>

    ![Dashboards](./media/network-watcher-analyze-nsg-flow-logs-graylog/dashboards.png)

### <a name="add-widgets"></a><span data-ttu-id="25136-190">Add widgets</span><span class="sxs-lookup"><span data-stu-id="25136-190">Add widgets</span></span>

<span data-ttu-id="25136-191">You can click the title of the dashboard to see it, but right now it's empty, since we haven’t added any widgets.</span><span class="sxs-lookup"><span data-stu-id="25136-191">You can click the title of the dashboard to see it, but right now it's empty, since we haven’t added any widgets.</span></span> <span data-ttu-id="25136-192">An easy and useful type widget to add to the dashboard are **Quick Values** charts, which display a list of values of the selected field, and their distribution.</span><span class="sxs-lookup"><span data-stu-id="25136-192">An easy and useful type widget to add to the dashboard are **Quick Values** charts, which display a list of values of the selected field, and their distribution.</span></span>

1. <span data-ttu-id="25136-193">Navigate back to the search results of the UDP input that’s receiving flow logs by selecting **Search** from the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="25136-193">Navigate back to the search results of the UDP input that’s receiving flow logs by selecting **Search** from the top navigation bar.</span></span>

2. <span data-ttu-id="25136-194">Under the **Search result** panel to the left side of the screen, find the **Fields** tab, which lists the various fields of each incoming flow tuple  message.</span><span class="sxs-lookup"><span data-stu-id="25136-194">Under the **Search result** panel to the left side of the screen, find the **Fields** tab, which lists the various fields of each incoming flow tuple  message.</span></span>

3. <span data-ttu-id="25136-195">Select any desired parameter in which to visualize (in this example, the IP source is selected).</span><span class="sxs-lookup"><span data-stu-id="25136-195">Select any desired parameter in which to visualize (in this example, the IP source is selected).</span></span> <span data-ttu-id="25136-196">To show the list of possible widgets, click the blue drop-down arrow to the left of the field, then select **Quick values** to generate the widget.</span><span class="sxs-lookup"><span data-stu-id="25136-196">To show the list of possible widgets, click the blue drop-down arrow to the left of the field, then select **Quick values** to generate the widget.</span></span> <span data-ttu-id="25136-197">You should see something similar to the following picture:</span><span class="sxs-lookup"><span data-stu-id="25136-197">You should see something similar to the following picture:</span></span>

   ![Source IP](./media/network-watcher-analyze-nsg-flow-logs-graylog/srcip.png)

4. <span data-ttu-id="25136-199">From there, you can select the **Add to dashboard** button at the top right corner of the widget and select the corresponding dashboard to add.</span><span class="sxs-lookup"><span data-stu-id="25136-199">From there, you can select the **Add to dashboard** button at the top right corner of the widget and select the corresponding dashboard to add.</span></span>

5. <span data-ttu-id="25136-200">Navigate back to the dashboard to see the widget you just added.</span><span class="sxs-lookup"><span data-stu-id="25136-200">Navigate back to the dashboard to see the widget you just added.</span></span>

   <span data-ttu-id="25136-201">You can add a variety of other widgets such as histograms and counts to your dashboard to keep track of important metrics, such as the sample dashboard shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="25136-201">You can add a variety of other widgets such as histograms and counts to your dashboard to keep track of important metrics, such as the sample dashboard shown in the following picture:</span></span>

   ![Flowlogs dashboard](./media/network-watcher-analyze-nsg-flow-logs-graylog/flowlogs-dashboard.png)

    <span data-ttu-id="25136-203">For further explanation on dashboards and the other types of widgets, refer to Graylog’s [documentation](http://docs.graylog.org/en/2.2/pages/dashboards.html).</span><span class="sxs-lookup"><span data-stu-id="25136-203">For further explanation on dashboards and the other types of widgets, refer to Graylog’s [documentation](http://docs.graylog.org/en/2.2/pages/dashboards.html).</span></span>

<span data-ttu-id="25136-204">By integrating Network Watcher with Graylog, you now have a convenient and centralized way to manage and visualize network security group flow logs.</span><span class="sxs-lookup"><span data-stu-id="25136-204">By integrating Network Watcher with Graylog, you now have a convenient and centralized way to manage and visualize network security group flow logs.</span></span> <span data-ttu-id="25136-205">Graylog has a number of other powerful features such as streams and alerts that can also be used to further manage flow logs and better understand your network traffic.</span><span class="sxs-lookup"><span data-stu-id="25136-205">Graylog has a number of other powerful features such as streams and alerts that can also be used to further manage flow logs and better understand your network traffic.</span></span> <span data-ttu-id="25136-206">Now that you have Graylog set up and connected to Azure, feel free to continue to explore the other functionality that it offers.</span><span class="sxs-lookup"><span data-stu-id="25136-206">Now that you have Graylog set up and connected to Azure, feel free to continue to explore the other functionality that it offers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25136-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="25136-207">Next steps</span></span>

<span data-ttu-id="25136-208">Learn how to visualize your network security group flow logs with Power BI by visiting [Visualize network security group flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="25136-208">Learn how to visualize your network security group flow logs with Power BI by visiting [Visualize network security group flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>
