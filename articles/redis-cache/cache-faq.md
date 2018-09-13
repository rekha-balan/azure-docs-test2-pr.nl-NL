---
title: Azure Redis Cache FAQ | Microsoft Docs
description: Learn the answers to common questions, patterns and best practices for Azure Redis Cache
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: sdanie
ms.openlocfilehash: e214cef9b1f982a23e1e10f822b7ecde3d1e20c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540980"
---
# <a name="azure-redis-cache-faq"></a>Azure Redis Cache FAQ
Learn the answers to common questions, patterns, and best practices for Azure Redis Cache.

## <a name="what-if-my-question-isnt-answered-here"></a>What if my question isn't answered here?
If your question isn't listed here, let us know and we'll help you find an answer.

* You can post a question in the comments at the end of this FAQ and engage with the Azure Cache team and other community members about this article.
* To reach a wider audience, you can post a question on the [Azure Cache MSDN Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) and engage with the Azure Cache team and other members of the community.
* If you want to make a feature request, you can submit your requests and ideas to [Azure Redis Cache User Voice](https://feedback.azure.com/forums/169382-cache).
* You can also send an email to us at [Azure Cache External Feedback](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Azure Redis Cache basics
The FAQs in this section cover some of the basics of Azure Redis Cache.

* [What is Azure Redis Cache?](#what-is-azure-redis-cache)
* [How can I get started with Azure Redis Cache?](#how-can-i-get-started-with-azure-redis-cache)

The following FAQs cover basic concepts and questions about Azure Redis Cache and are answered in one of the other FAQ sections.

* [What Redis Cache offering and size should I use?](#what-redis-cache-offering-and-size-should-i-use)
* [What Redis cache clients can I use?](#what-redis-cache-clients-can-i-use)
* [Is there a local emulator for Azure Redis Cache?](#is-there-a-local-emulator-for-azure-redis-cache)
* [How do I monitor the health and performance of my cache?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Planning FAQs
* [What Redis Cache offering and size should I use?](#what-redis-cache-offering-and-size-should-i-use)
* [Azure Redis Cache performance](#azure-redis-cache-performance)
* [In what region should I locate my cache?](#in-what-region-should-i-locate-my-cache)
* [How am I billed for Azure Redis Cache?](#how-am-i-billed-for-azure-redis-cache)
* [Can I use Azure Redis Cache with Azure Government Cloud, Azure China Cloud, or Microsoft Azure Germany?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Development FAQs
* [What do the StackExchange.Redis configuration options do?](#what-do-the-stackexchangeredis-configuration-options-do)
* [What Redis cache clients can I use?](#what-redis-cache-clients-can-i-use)
* [Is there a local emulator for Azure Redis Cache?](#is-there-a-local-emulator-for-azure-redis-cache)
* [How can I run Redis commands?](#how-can-i-run-redis-commands)
* [Why doesn't Azure Redis Cache have an MSDN class library reference like some of the other Azure services?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Can I use Azure Redis Cache as a PHP session cache?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [What are Redis databases?](#what-are-redis-databases)

## <a name="security-faqs"></a>Security FAQs
* [When should I enable the non-SSL port for connecting to Redis?](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Production FAQs
* [What are some production best practices?](#what-are-some-production-best-practices)
* [What are some of the considerations when using common Redis commands?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [How can I benchmark and test the performance of my cache?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Important details about ThreadPool growth](#important-details-about-threadpool-growth)
* [Enable server GC to get more throughput on the client when using StackExchange.Redis](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)

## <a name="monitoring-and-troubleshooting-faqs"></a>Monitoring and troubleshooting FAQs
The FAQs in this section cover common monitoring and troubleshooting questions. For more information about monitoring and troubleshooting your Azure Redis Cache instances, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md) and [How to troubleshoot Azure Redis Cache](cache-how-to-troubleshoot.md).

* [How do I monitor the health and performance of my cache?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [My cache diagnostics storage account settings changed, what happened?](#my-cache-diagnostics-storage-account-settings-changed-what-happened)
* [Why are diagnostics enabled for some new caches but not others?](#why-are-diagnostics-enabled-for-some-new-caches-but-not-others)
* [Why am I seeing timeouts?](#why-am-i-seeing-timeouts)
* [Why was my client disconnected from the cache?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Prior Cache offering FAQs
* [Which Azure Cache offering is right for me?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>What is Azure Redis Cache?
Azure Redis Cache is based on the popular open-source [Redis cache](http://redis.io). It gives you access to a secure, dedicated Redis cache, managed by Microsoft, and accessible from any application within Azure. For a more detailed overview, see the [Azure Redis Cache](https://azure.microsoft.com/services/cache/) product page on Azure.com.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>How can I get started with Azure Redis Cache?
There are several ways you can get started with Azure Redis Cache.

* You can check out one of our tutorials available for [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md), and [Python](cache-python-get-started.md).
* You can watch [How to Build High-Performance Apps Using Microsoft Azure Redis Cache](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* You can check out the client documentation for the clients that match the development language of your project to see how to use Redis. There are many Redis clients that can be used with Azure Redis Cache. For a list of Redis clients, see [http://redis.io/clients](http://redis.io/clients).

If you don't already have an Azure account, you can:

* [Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). You get credits that can be used to try out paid Azure services. Even after the credits are used up, you can keep the account and use free Azure services and features.
* [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Your MSDN subscription gives you credits every month that you can use for paid Azure services.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>What Redis Cache offering and size should I use?
Each Azure Redis Cache offering provides different levels of **size**, **bandwidth**, **high availability**, and **SLA** options.

The following are considerations for choosing a Cache offering.

* **Memory**: The Basic and Standard tiers offer 250 MB – 53 GB. The Premium tier offers up to 530 GB with more available [on request](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). For more information, see [Azure Redis Cache Pricing](https://azure.microsoft.com/pricing/details/cache/).
* **Network Performance**: If you have a workload that requires high throughput, the Premium tier offers more bandwidth compared to Standard or Basic. Also within each tier, larger size caches have more bandwidth because of the underlying VM that hosts the cache. See the [following table](#cache-performance) for more information.
* **Throughput**: The Premium tier offers the maximum available throughput. If the cache server or client reaches the bandwidth limits, you may receive timeouts on the client side. For more information, see the following table.
* **High Availability/SLA**: Azure Redis Cache guarantees that a Standard/Premium cache is available at least 99.9% of the time. To learn more about our SLA, see [Azure Redis Cache Pricing](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). The SLA only covers connectivity to the Cache endpoints. The SLA does not cover protection from data loss. We recommend using the Redis data persistence feature in the Premium tier to increase resiliency against data loss.
* **Redis Data Persistence**: The Premium tier allows you to persist the cache data in an Azure Storage account. In a Basic/Standard cache, all the data is stored only in memory. If there are underlying infrastructure issues there can be potential data loss. We recommend using the Redis data persistence feature in the Premium tier to increase resiliency against data loss. Azure Redis Cache offers RDB and AOF (coming soon) options in Redis persistence. For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).
* **Redis Cluster**: To create caches larger than 53 GB, or to shard data across multiple Redis nodes, you can use Redis clustering, which is available in the Premium tier. Each node consists of a primary/replica cache pair for high availability. For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).
* **Enhanced security and network isolation**: Azure Virtual Network (VNET) deployment provides enhanced security and isolation for your Azure Redis Cache, as well as subnets, access control policies, and other features to further restrict access. For more information, see [How to configure Virtual Network support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).
* **Configure Redis**: In both the Standard and Premium tiers, you can configure Redis for Keyspace notifications.
* **Maximum number of client connections**: The Premium tier offers the maximum number of clients that can connect to Redis, with a higher number of connections for larger sized caches. For more information, see [Azure Redis Cache pricing](https://azure.microsoft.com/pricing/details/cache/).
* **Dedicated Core for Redis Server**: In the Premium tier, all cache sizes have a dedicated core for Redis. In the Basic/Standard tiers, the C1 size and above have a dedicated core for Redis server.
* **Redis is single-threaded** so having more than two cores does not provide additional benefit over having just two cores, but larger VM sizes typically have more bandwidth than smaller sizes. If the cache server or client reaches the bandwidth limits, then you receive timeouts on the client side.
* **Performance improvements**: Caches in the Premium tier are deployed on hardware that has faster processors, giving better performance compared to the Basic or Standard tier. Premium tier Caches have higher throughput and lower latencies.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Azure Redis Cache performance
The following table shows the maximum bandwidth values observed while testing various sizes of Standard and Premium caches using `redis-benchmark.exe` from an Iaas VM against the Azure Redis Cache endpoint. 

>[!NOTE] 
>These values are not guaranteed and there is no SLA for these numbers, but should be typical. You should load test your own application to determine the right cache size for your application.
>
>

From this table, we can draw the following conclusions:

* Throughput for the caches that are the same size is higher in the Premium tier as compared to the Standard tier. For example, with a 6 GB Cache, throughput of P1 is 140K RPS as compared to 49K for C3.
* With Redis clustering, throughput increases linearly as you increase the number of shards (nodes) in the cluster. For example, if you create a P4 cluster of 10 shards, then the available throughput is 250K *10 = 2.5 Million RPS.
* Throughput for bigger key sizes is higher in the Premium tier as compared to the Standard Tier.

| Pricing tier | Size | CPU cores | Available bandwidth | 1 KB value size |
| --- | --- | --- | --- | --- |
| **Standard cache sizes** | | |**Megabits per sec (Mb/s) / Megabytes per sec (MB/s)** |**Requests per second (RPS)** |
| C0 |250 MB |Shared |5 / 0.625 |600 |
| C1 |1 GB |1 |100 / 12.5 |12200 |
| C2 |2.5 GB |2 |200 / 25 |24000 |
| C3 |6 GB |4 |400 / 50 |49000 |
| C4 |13 GB |2 |500 / 62.5 |61000 |
| C5 |26 GB |4 |1000 / 125 |115000 |
| C6 |53 GB |8 |2000 / 250 |150000 |
| **Premium cache sizes** | |**CPU cores per shard** | |**Requests per second (RPS), per shard** |
| P1 |6 GB |2 |1000 / 125 |140000 |
| P2 |13 GB |4 |2000 / 250 |220000 |
| P3 |26 GB |4 |2000 / 250 |220000 |
| P4 |53 GB |8 |4000 / 500 |250000 |

For instructions on downloading the Redis tools such as `redis-benchmark.exe`, see the [How can I run Redis commands?](#cache-commands) section.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>In what region should I locate my cache?
For best performance and lowest latency, locate your Azure Redis Cache in the same region as your cache client application.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>How am I billed for Azure Redis Cache?
Azure Redis Cache pricing is [here](https://azure.microsoft.com/pricing/details/cache/). The pricing page lists pricing as an hourly rate. Caches are billed on a per-minute basis from the time that the cache is created until the time that a cache is deleted. There is no option for stopping or pausing the billing of a cache.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>Can I use Azure Redis Cache with Azure Government Cloud, Azure China Cloud, or Microsoft Azure Germany?
Yes, Azure Redis Cache is available in Azure Government Cloud, Azure China Cloud, and Microsoft Azure Germany. The URLs for accessing and managing Azure Redis Cache are different in these clouds compared with Azure Public Cloud. 

| Cloud   | Dns Suffix for Redis            |
|---------|---------------------------------|
| Public  | *.redis.cache.windows.net       |
| US Gov  | *.redis.cache.usgovcloudapi.net |
| Germany | *.redis.cache.cloudapi.de       |
| China   | *.redis.cache.chinacloudapi.cn  |

For more information on considerations when using Azure Redis Cache with other clouds, see the following links.

- [Azure Government Databases - Azure Redis Cache](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Azure China Cloud - Azure Redis Cache](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/)

For information on using Azure Redis Cache with PowerShell in Azure Government Cloud, Azure China Cloud, and Microsoft Azure Germany, see [How to connect to other clouds - Azure Redis Cache PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-the-stackexchangeredis-configuration-options-do"></a>What do the StackExchange.Redis configuration options do?
StackExchange.Redis has many options. This section talks about some of the common settings. For more detailed information about StackExchange.Redis options, see [StackExchange.Redis configuration](https://stackexchange.github.io/StackExchange.Redis/Configuration).

| ConfigurationOptions | Description | Recommendation |
| --- | --- | --- |
| AbortOnConnectFail |When set to true, the connection will not reconnect after a network failure. |Set to false and let StackExchange.Redis reconnect automatically. |
| ConnectRetry |The number of times to repeat connection attempts during initial connect. |See the following notes for guidance. |
| ConnectTimeout |Timeout in ms for connect operations. |See the following notes for guidance. |

Usually the default values of the client are sufficient. You can fine-tune the options based on your workload.

* **Retries**
  * For ConnectRetry and ConnectTimeout, the general guidance is to fail fast and retry again. This guidance is based on your workload and how much time on average it takes for your client to issue a Redis command and receive a response.
  * Let StackExchange.Redis automatically reconnect instead of checking connection status and reconnecting yourself. **Avoid using the ConnectionMultiplexer.IsConnected property**.
  * Snowballing - sometimes you may run into an issue where you are retrying and the retries snowball and never recovers. If snowballing occurs, you should consider using an exponential backoff retry algorithm as described in [Retry general guidance](../best-practices-retry-general.md) published by the Microsoft Patterns & Practices group.
* **Timeout values**
  * Consider your workload and set the values accordingly. If you are storing large values, set the timeout to a higher value.
  * Set `AbortOnConnectFail` to false and let StackExchange.Redis reconnect for you.
  * Use a single ConnectionMultiplexer instance for the application. You can use a LazyConnection to create a single instance that is returned by a Connection property, as shown in [Connect to the cache using the ConnectionMultiplexer class](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Set the `ConnectionMultiplexer.ClientName` property to an app instance unique name for diagnostic purposes.
  * Use multiple `ConnectionMultiplexer` instances for custom workloads.
      * You can follow this model if you have varying load in your application. For example:
      * You can have one multiplexer for dealing with large keys.
      * You can have one multiplexer for dealing with small keys.
      * You can set different values for connection timeouts and retry logic for each ConnectionMultiplexer that you use.
      * Set the `ClientName` property on each multiplexer to help with diagnostics.
      * This guidance may lead to more streamlined latency per `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>What Redis cache clients can I use?
One of the great things about Redis is that there are many clients supporting many different development languages. For a current list of clients, see [Redis clients](http://redis.io/clients). For tutorials that cover several different languages and clients, see [How to use Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md) and click the desired language from the language switcher at the top of the article.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Is there a local emulator for Azure Redis Cache?
There is no local emulator for Azure Redis Cache, but you can run the MSOpenTech version of redis-server.exe from the [Redis command-line tools](https://github.com/MSOpenTech/redis/releases/) on your local machine and connect to it to get a similar experience to a local cache emulator, as shown in the following example:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect to a locally running instance of Redis to simulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


You can optionally configure a [redis.conf](http://redis.io/topics/config) file to more closely match the [default cache settings](cache-configure.md#default-redis-server-configuration) for your online Azure Redis Cache if desired.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>How can I run Redis commands?
You can use any of the commands listed at [Redis commands](http://redis.io/commands#) except for the commands listed at [Redis commands not supported in Azure Redis Cache](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). You have several options to run Redis commands.

* If you have a Standard or Premium cache, you can run Redis commands using the [Redis Console](cache-configure.md#redis-console). The Redis console provides a secure way to run Redis commands in the Azure portal.
* You can also use the Redis command-line tools. To use them, perform the following steps:
* Download the [Redis command-line tools](https://github.com/MSOpenTech/redis/releases/).
* Connect to the cache using `redis-cli.exe`. Pass in the cache endpoint using the -h switch and the key using -a as shown in the following example:
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> The Redis command-line tools do not work with the SSL port, but you can use a utility such as `stunnel` to securely connect the tools to the SSL port by following the directions in the [Announcing ASP.NET Session State Provider for Redis Preview Release](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) blog post.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services"></a>Why doesn't Azure Redis Cache have an MSDN class library reference like some of the other Azure services?
Microsoft Azure Redis Cache is based on the popular open source Redis Cache and can be accessed by a wide variety of [Redis clients](http://redis.io/clients) for many programming languages. Each client has its own API that makes calls to the Redis cache instance using [Redis commands](http://redis.io/commands).

Because each client is different, there is not one centralized class reference on MSDN, and each client maintains its own reference documentation. In addition to the reference documentation, there are several tutorials showing how to get started with Azure Redis Cache using different languages and cache clients. To access these tutorials, see [How to use Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md) and click the desired language from the language switcher at the top of the article.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Can I use Azure Redis Cache as a PHP session cache?
Yes, to use Azure Redis Cache as a PHP session cache, specify the connection string to your Azure Redis Cache instance in `session.save_path`.

> [!IMPORTANT]
> When using Azure Redis Cache as a PHP session cache, you must URL encode the security key used to connect to the cache, as shown in the following example:
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> If the key is not URL encoded, you may receive an exception with a message like: `Failed to parse session.save_path`
>
>

For more information about using Redis Cache as a PHP session cache with the PhpRedis client, see [PHP Session handler](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>What are Redis databases?

Redis Databases are just a logical separation of data within the same Redis instance. The cache memory is shared between all the databases and actual memory consumption of a given database depends on the keys/values stored in that database. For example a C6 cache has 53 GB of memory. You can choose to put all 53 GB into one database or you can split it up between multiple databases. 

> [!NOTE]
> When using a Premium Azure Redis Cache with clustering enabled, only database 0 is available. This limitation is an intrinsic Redis limitation and is not specific to Azure Redis Cache. For more information, see [Do I need to make any changes to my client application to use clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-the-non-ssl-port-for-connecting-to-redis"></a>When should I enable the non-SSL port for connecting to Redis?
Redis server does not natively support SSL, but Azure Redis Cache does. If you are connecting to Azure Redis Cache and your client supports SSL, like StackExchange.Redis, then you should use SSL.

>[!NOTE]
>The non-SSL port is disabled by default for new Azure Redis Cache instances. If your client does not support SSL, then you must enable the non-SSL port by following the directions in the [Access ports](cache-configure.md#access-ports) section of the [Configure a cache in Azure Redis Cache](cache-configure.md) article.
>
>

Redis tools such as `redis-cli` do not work with the SSL port, but you can use a utility such as `stunnel` to securely connect the tools to the SSL port by following the directions in the [Announcing ASP.NET Session State Provider for Redis Preview Release](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) blog post.

For instructions on downloading the Redis tools, see the [How can I run Redis commands?](#cache-commands) section.

### <a name="what-are-some-production-best-practices"></a>What are some production best practices?
* [StackExchange.Redis best practices](#stackexchangeredis-best-practices)
* [Configuration and concepts](#configuration-and-concepts)
* [Performance testing](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>StackExchange.Redis best practices
* Set `AbortConnect` to false, then let the ConnectionMultiplexer reconnect automatically. [See here for details](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Reuse the ConnectionMultiplexer - do not create a new one for each request. The `Lazy<ConnectionMultiplexer>` pattern [shown here](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) is recommended.
* Redis works best with smaller values, so consider chopping up bigger data into multiple keys. In [this Redis discussion](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ), 100kb is considered large. Read [this article](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) for an example problem that can be caused by large values.
* Configure your [ThreadPool settings](#important-details-about-threadpool-growth) to avoid timeouts.
* Use at least the default connectTimeout of 5 seconds. This interval would give StackExchange.Redis sufficient time to re-establish the connection, in case of a network blip.
* Be aware of the performance costs associated with different operations you are running. For instance, the `KEYS` command is an O(n) operation and should be avoided. The [redis.io site](http://redis.io/commands/) has details around the time complexity for each operation that it supports. Click each command to see the complexity for each operation.

#### <a name="configuration-and-concepts"></a>Configuration and concepts
* Use Standard or Premium Tier for Production systems. The Basic Tier is a single node system with no data replication and no SLA. Also, use at least a C1 cache. C0 caches are typically used for simple dev/test scenarios.
* Remember that Redis is an **In-Memory** data store. Read [this article](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) so that you are aware of scenarios where data loss can occur.
* Develop your system such that it can handle connection blips [due to patching and failover](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Performance testing
* Start by using `redis-benchmark.exe` to get a feel for possible throughput before writing your own perf tests. Because `redis-benchmark` does not support SSL, you must [enable the Non-SSL port through the Azure portal](cache-configure.md#access-ports) before you run the test. For examples, see [How can I benchmark and test the performance of my cache?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* The client VM used for testing should be in the same region as your Redis cache instance.
* We recommend using Dv2 VM Series for your client as they have better hardware and should give the best results.
* Make sure your client VM you choose has at least as much computing and bandwidth capability as the cache you are testing.
* Enable VRSS on the client machine if you are on Windows. [See here for details](https://technet.microsoft.com/library/dn383582.aspx).
* Premium tier Redis instances have better network latency and throughput because they are running on better hardware for both CPU and Network.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-the-considerations-when-using-common-redis-commands"></a>What are some of the considerations when using common Redis commands?
* You should not run certain Redis commands which take a long time to complete, without understanding the impact of these commands.
  * For example, do not run the [KEYS](http://redis.io/commands/keys) command in production as it could take a long time to return depending on the number of keys. Redis is a single-threaded server and it processes commands one at a time. If you have other commands issued after KEYS, they will not be processed until Redis processes the KEYS command. The [redis.io site](http://redis.io/commands/) has details around the time complexity for each operation that it supports. Click each command to see the complexity for each operation.
* Key sizes - should I use small key/values or large key/values? In general, it depends on the scenario. If your scenario requires larger keys, you can adjust the ConnectionTimeout and retry values and adjust your retry logic. From a Redis server perspective, smaller values are observed to have better performance.
* These considerations don't mean that you can't store larger values in Redis; you must be aware of the following considerations. Latencies will be higher. If you have one set of data that is larger and one that is smaller, you can use multiple ConnectionMultiplexer instances, each configured with a different set of timeout and retry values, as described in the previous [What do the StackExchange.Redis configuration options do](#cache-configuration) section.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-the-performance-of-my-cache"></a>How can I benchmark and test the performance of my cache?
* [Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache. You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.
* You can use redis-benchmark.exe to load test your Redis server.
* Ensure that the load testing client and the Redis cache are in the same region.
* Use redis-cli.exe and monitor the cache using the INFO command.
* If your load is causing high memory fragmentation, you should scale up to a larger cache size.
* For instructions on downloading the Redis tools, see the [How can I run Redis commands?](#cache-commands) section.

The following commands provide an example of using redis-benchmark.exe. For accurate results, run these commands from a VM in the same region as your cache.

* Test Pipelined SET requests using a 1k payload

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Test Pipelined GET requests using a 1k payload.
  NOTE: Run the SET test shown above first to populate cache

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>Important details about ThreadPool growth
The CLR ThreadPool has two types of threads - "Worker" and "I/O Completion Port" (aka IOCP) threads.

* Worker threads are used when for things like processing `Task.Run(…)` or `ThreadPool.QueueUserWorkItem(…)` methods. These threads are also used by various components in the CLR when work needs to happen on a background thread.
* IOCP threads are used when asynchronous IO happens (e.g. reading from the network).

The thread pool provides new worker threads or I/O completion threads on demand (without any throttling) until it reaches the "Minimum" setting for each type of thread. By default, the minimum number of threads is set to the number of processors on a system.

Once the number of existing (busy) threads hits the "minimum" number of threads, the ThreadPool will throttle the rate at which it injects new threads to one thread per 500 milliseconds. Typically, if your system gets a burst of work needing an IOCP thread, it will process that work very quickly. However, if the burst of work is more than the configured "Minimum" setting, there will be some delay in processing some of the work as the ThreadPool waits for one of two things to happen.

1. An existing thread becomes free to process the work.
2. No existing thread becomes free for 500ms, so a new thread is created.

Basically, it means that when the number of Busy threads is greater than Min threads, you are likely paying a 500ms delay before network traffic is processed by the application. Also, it is important to note that when an existing thread stays idle for longer than 15 seconds (based on what I remember), it will be cleaned up and this cycle of growth and shrinkage can repeat.

If we look at an example error message from StackExchange.Redis (build 1.0.450 or later), you will see that it now prints ThreadPool statistics (see IOCP and WORKER details below).

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

In the previous example, you can see that for IOCP thread there are 6 busy threads and the system is configured to allow 4 minimum threads. In this case, the client would have likely seen two 500 ms delays because 6 > 4.

Note that StackExchange.Redis can hit timeouts if growth of either IOCP or WORKER threads gets throttled.

### <a name="recommendation"></a>Recommendation
Given this information, we strongly recommend that customers set the minimum configuration value for IOCP and WORKER threads to something larger than the default value. We can't give one-size-fits-all guidance on what this value should be because the right value for one application will be too high/low for another application. This setting can also impact the performance of other parts of complicated applications, so each customer needs to fine-tune this setting to their specific needs. A good starting place is 200 or 300, then test and tweak as needed.

How to configure this setting:

* In ASP.NET, use the ["minIoThreads" configuration setting]["minIoThreads" configuration setting] under the `<processModel>` configuration element in web.config. If you are running inside of Azure WebSites, this setting is not exposed through the configuration options. However, you should still be able to configure this setting programmatically (see below) from your Application_Start method in global.asax.cs.

  > [!NOTE] 
  > The value specified in this configuration element is a *per-core* setting. For example, if you have a 4 core machine and want your minIOThreads setting to be 200 at runtime, you would use `<processModel minIoThreads="50"/>`.
  >

* Outside of ASP.NET, use the [ThreadPool.SetMinThreads(…)](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API.

<a name="server-gc"></a>

### <a name="enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis"></a>Enable server GC to get more throughput on the client when using StackExchange.Redis
Enabling server GC can optimize the client and provide better performance and throughput when using StackExchange.Redis. For more information on server GC and how to enable it, see the following articles:

* [To enable server GC](https://msdn.microsoft.com/library/ms229357.aspx)
* [Fundamentals of Garbage Collection](https://msdn.microsoft.com/library/ee787088.aspx)
* [Garbage Collection and Performance](https://msdn.microsoft.com/library/ee851764.aspx)

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-the-health-and-performance-of-my-cache"></a>How do I monitor the health and performance of my cache?
Microsoft Azure Redis Cache instances can be monitored in the [Azure portal](https://portal.azure.com). You can view metrics, pin metrics charts to the Startboard, customize the date and time range of monitoring charts, add and remove metrics from the charts, and set alerts when certain conditions are met. For more information, see [Monitor Azure Redis Cache](cache-how-to-monitor.md).

The Redis Cache **Resource menu** also contains several tools for monitoring and troubleshooting your caches.

* **Diagnose and solve problems** provides information about common issues and strategies for resolving them.
* **Resource health** watches your resource and tells you if it's running as expected. For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).
* **New support request** provides options to open a support request for your cache.

These tools enable you to monitor the health of your Azure Redis Cache instances and help you manage your caching applications. For more information, see the "Support & troubleshooting settings" section of [How to configure Azure Redis Cache](cache-configure.md).

### <a name="my-cache-diagnostics-storage-account-settings-changed-what-happened"></a>My cache diagnostics storage account settings changed, what happened?
Caches in the same region and subscription share diagnostics storage settings, and if the configuration is changed (diagnostics enabled/disabled or changing the storage account) it applies to all caches in the subscription that are in that region. If the diagnostics settings for your cache have changed, check to see if the diagnostic settings for another cache in the same subscription and region have changed. One way to check is to view the audit logs for your cache for a `Write DiagnosticSettings` event. For more information on working with audit logs, see [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) and [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md). For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).

### <a name="why-are-diagnostics-enabled-for-some-new-caches-but-not-others"></a>Why are diagnostics enabled for some new caches but not others?
Caches in the same region and subscription share the same diagnostics storage settings. If you create a new cache in the same region and subscription as another cache that has diagnostics enabled, diagnostics is enabled on the new cache using the same settings.

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>Why am I seeing timeouts?
Timeouts happen in the client that you use to talk to Redis. When a command is sent to the Redis server, the command is queued up and Redis server eventually picks up the command and executes it. However the client can time out during this process and if it does an exception is raised on the calling side. For more information on troubleshooting timeout issues, see [Client-side troubleshooting](cache-how-to-troubleshoot.md#client-side-troubleshooting) and [StackExchange.Redis timeout exceptions](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-the-cache"></a>Why was my client disconnected from the cache?
The following are some common reason for a cache disconnect.

* Client-side causes
  * The client application was redeployed.
  * The client application performed a scaling operation.
    * In the case of Cloud Services or Web Apps, this may be due to auto-scaling.
  * The networking layer on the client side changed.
  * Transient errors occurred in the client or in the network nodes between the client and the server.
  * The bandwidth threshold limits were reached.
  * CPU bound operations took too long to complete.
* Server-side causes
  * On the standard cache offering, the Azure Redis Cache service initiated a fail-over from the primary node to the secondary node.
  * Azure was patching the instance where the cache was deployed
    * This can be for Redis server updates or general VM maintenance.

### <a name="which-azure-cache-offering-is-right-for-me"></a>Which Azure Cache offering is right for me?
> [!IMPORTANT]
> As per last year's [announcement](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/), Azure Managed Cache Service and Azure In-Role Cache service **have been retired** on November 30, 2016. Our recommendation is to use [Azure Redis Cache](https://azure.microsoft.com/services/cache/). For information on migrating, see [Migrate from Managed Cache Service to Azure Redis Cache](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>Azure Redis Cache
Azure Redis Cache is Generally Available in sizes up to 53 GB and has an availability SLA of 99.9%. The new [premium tier](cache-premium-tier-intro.md) offers sizes up to 530 GB and support for clustering, VNET, and persistence, with a 99.9% SLA.

Azure Redis Cache gives customers the ability to use a secure, dedicated Redis cache, managed by Microsoft. With this offer, you get to leverage the rich feature set and ecosystem provided by Redis, and reliable hosting and monitoring from Microsoft.

Unlike traditional caches which deal only with key-value pairs, Redis is popular for its highly performant data types. Redis also supports running atomic operations on these types, like appending to a string; incrementing the value in a hash; pushing to a list; computing set intersection, union and difference; or getting the member with highest ranking in a sorted set. Other features include support for transactions, pub/sub, Lua scripting, keys with a limited time-to-live, and configuration settings to make Redis behave more like a traditional cache.

Another key aspect to Redis success is the healthy, vibrant open source ecosystem built around it. This is reflected in the diverse set of Redis clients available across multiple languages. This ecosystem and wide range of clients allow Azure Redis Cache to be used by nearly any workload you would build inside of Azure.

For more information about getting started with Azure Redis Cache, see [How to Use Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md) and [Azure Redis Cache documentation](index.md).

### <a name="managed-cache-service"></a>Managed Cache service
[Managed Cache service has been retired November 30, 2016.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

### <a name="in-role-cache"></a>In-Role Cache
[In-Role Cache has been retired November 30, 2016.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
