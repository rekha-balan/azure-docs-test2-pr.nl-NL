---
title: Twitter trending topics with Apache Storm on HDInsight | Microsoft Docs
description: Learn how to use Trident to create an Apache Storm topology that determines trending topics on Twitter based on hashtags.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: b2d9653665352a7e553c8546cfde86d2cbfb0304
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556712"
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="b7e9a-103">Determine Twitter trending topics with Apache Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7e9a-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="b7e9a-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="b7e9a-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="b7e9a-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="b7e9a-107">The example used in this document is a Trident topology with a custom spout and function.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="b7e9a-108">It also uses several built-in functions provided by Trident.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="b7e9a-109">Requirements</span><span class="sxs-lookup"><span data-stu-id="b7e9a-109">Requirements</span></span>

* <span data-ttu-id="b7e9a-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="b7e9a-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="b7e9a-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="b7e9a-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="b7e9a-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="b7e9a-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="b7e9a-113">A Twitter developer account</span><span class="sxs-lookup"><span data-stu-id="b7e9a-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="b7e9a-114">Download the project</span><span class="sxs-lookup"><span data-stu-id="b7e9a-114">Download the project</span></span>

<span data-ttu-id="b7e9a-115">Use the following code to clone the project locally.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="b7e9a-116">Understanding the topology</span><span class="sxs-lookup"><span data-stu-id="b7e9a-116">Understanding the topology</span></span>

<span data-ttu-id="b7e9a-117">The following diagram shows of how data flows through this topology:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-117">The following diagram shows of how data flows through this topology:</span></span>

![topology](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="b7e9a-119">This diagram is a simplified view of the topology.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="b7e9a-120">Multiple instances of the components are distributed across the nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="b7e9a-121">The Trident code that implements the topology is as follows:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="b7e9a-122">This code performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="b7e9a-123">Creates a stream from the spout.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-123">Creates a stream from the spout.</span></span> <span data-ttu-id="b7e9a-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span><span class="sxs-lookup"><span data-stu-id="b7e9a-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="b7e9a-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="b7e9a-126">The hash tags are emitted to the stream.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="b7e9a-127">The stream is grouped by hash tag, and passed to an aggregator.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="b7e9a-128">This aggregator creates a count of how many times each hash tag has occurred.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="b7e9a-129">This data is persisted in memory.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-129">This data is persisted in memory.</span></span> <span data-ttu-id="b7e9a-130">Finally, a new stream is emitted that contains the hash tag and the count.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="b7e9a-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="b7e9a-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="b7e9a-133">The spout</span><span class="sxs-lookup"><span data-stu-id="b7e9a-133">The spout</span></span>

<span data-ttu-id="b7e9a-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="b7e9a-135">A filter is created for the words __love__, **music**, and **coffee**.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="b7e9a-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="b7e9a-137">Finally, items are pulled off the queue and emitted to the topology.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="b7e9a-138">The HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="b7e9a-138">The HashtagExtractor</span></span>

<span data-ttu-id="b7e9a-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="b7e9a-140">These are then emitted to the stream.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="b7e9a-141">Configure Twitter</span><span class="sxs-lookup"><span data-stu-id="b7e9a-141">Configure Twitter</span></span>

<span data-ttu-id="b7e9a-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="b7e9a-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="b7e9a-144">When filling in the form, leave the **Callback URL** field empty.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="b7e9a-145">When the app is created, click the **Keys and Access Tokens** tab.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="b7e9a-146">Copy the **Consumer Key** and **Consumer Secret** information.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="b7e9a-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="b7e9a-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="b7e9a-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="b7e9a-150">Build the topology</span><span class="sxs-lookup"><span data-stu-id="b7e9a-150">Build the topology</span></span>

<span data-ttu-id="b7e9a-151">Use the following code to build the project:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="b7e9a-152">Test the topology</span><span class="sxs-lookup"><span data-stu-id="b7e9a-152">Test the topology</span></span>

<span data-ttu-id="b7e9a-153">Use the following command to test the topology locally:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="b7e9a-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span><span class="sxs-lookup"><span data-stu-id="b7e9a-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="b7e9a-155">The output should appear similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="b7e9a-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7e9a-156">Next steps</span></span>

<span data-ttu-id="b7e9a-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b7e9a-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="b7e9a-158">You may also be interested in the following Storm topics:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="b7e9a-159">Develop Java topologies for Storm on HDInsight using Maven</span><span class="sxs-lookup"><span data-stu-id="b7e9a-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="b7e9a-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b7e9a-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="b7e9a-161">For more Storm examples for HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b7e9a-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="b7e9a-162">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7e9a-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)


