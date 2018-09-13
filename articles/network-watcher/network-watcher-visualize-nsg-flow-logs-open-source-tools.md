---
title: Visualize Azure Network Watcher NSG flow logs using open source tools | Microsoft Docs
description: This page describes how to use open source tools to visualize NSG flow logs.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 1c8535ed6c852dcffa912624ad82383f9dd3de9b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553892"
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Visualize Azure Network Watcher NSG flow logs using open source tools

Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups. These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.

These flow logs can be difficult to manually parse and gain insights from. However, there are several open source tools that can help visualize this data. This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.

## <a name="scenario"></a>Scenario

In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.  A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs. Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.

![scenario][scenario]

## <a name="steps"></a>Steps

### <a name="enable-network-security-group-flow-logging"></a>Enable Network Security Group flow logging
For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account. For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-the-elastic-stack"></a>Set up the Elastic Stack
By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.

#### <a name="install-elasticsearch"></a>Install Elasticsearch

1. The Elastic Stack from version 5.0 and above requires Java 8. Run the command `java -version` to check your version. If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Download the correct binary package for your system:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)

1. Verify that Elasticsearch is running with the command:

    ```
    curl http://127.0.0.1:9200
    ```

    You should see a response similar to this:

    ```
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

For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Install Logstash

1. To install Logstash run the following commands:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. Next we need to configure Logstash to access and parse the flow logs. Create a logstash.conf file using:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Add the following content to the file:

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
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

For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a>Install the Logstash input plugin for Azure blob storage

This Logstash plugin will allow you to directly access the flow logs from their designated storage account. To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:

```
logstash-plugin install logstash-input-azureblob
```

To start Logstash run the command:

```
sudo /etc/init.d/logstash start
```

For more information about this plugin, refer to documentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

### <a name="install-kibana"></a>Install Kibana

1. Run the following commands to install Kibana:

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. To run Kibana use the commands:

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. To view your Kibana web interface, navigate to `http://localhost:5601`
1. For this scenario, the index pattern used for the flow logs is "nsg-flow-logs". You may change the index pattern in the "output" section of your logstash.conf file.

1. If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.

### <a name="create-a-kibana-dashboard"></a>Create a Kibana dashboard

For this article, we have provided a sample dashboard for you to view trends and details in your alerts.

![figure 1][1]

1. Download the dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), the visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and the saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).

1. Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files. Then from the **Dashboard** tab you can open and load the sample dashboard.

You can also create your own visualizations and dashboards tailored towards metrics of your own interest. Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).

### <a name="visualize-nsg-flow-logs"></a>Visualize NSG flow logs

The sample dashboard provides several visualizations of the flow logs:

1. Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period. You can edit the unit of time and span of both these visualizations. Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic. With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.

  ![figure2][2]

1. Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports. With this view you can see your most commonly used ports. If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.

  ![figure3][3]

1. Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.

  ![figure4][4]

1. Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG. From here you can see which NSG and rules generated the most traffic.

  ![figure5][5]

1. Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs. You can adjust these charts to show more or less top IPs. From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.

  ![figure6][6]

1. Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.

  ![figure7][7]

Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest. For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Conclusion

By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic. These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies. Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.

## <a name="next-steps"></a>Next steps

Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png







