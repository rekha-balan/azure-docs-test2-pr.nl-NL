---
title: SCP.NET programming guide | Microsoft Docs
description: Learn how to use SCP.NET to create .NET-based Storm topologies for use with Storm on HDInsight.
services: hdinsight
documentationcenter: ''
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: cb87adc4b5b6d3f06015bafc6a5ffa708e3a1727
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552341"
---
# <a name="scp-programming-guide"></a><span data-ttu-id="87f6a-103">SCP programming guide</span><span class="sxs-lookup"><span data-stu-id="87f6a-103">SCP programming guide</span></span>
<span data-ttu-id="87f6a-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span><span class="sxs-lookup"><span data-stu-id="87f6a-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="87f6a-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span><span class="sxs-lookup"><span data-stu-id="87f6a-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="87f6a-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span><span class="sxs-lookup"><span data-stu-id="87f6a-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="87f6a-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span><span class="sxs-lookup"><span data-stu-id="87f6a-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="87f6a-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span><span class="sxs-lookup"><span data-stu-id="87f6a-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="87f6a-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span><span class="sxs-lookup"><span data-stu-id="87f6a-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="87f6a-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span><span class="sxs-lookup"><span data-stu-id="87f6a-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="87f6a-111">Processing model</span><span class="sxs-lookup"><span data-stu-id="87f6a-111">Processing model</span></span>
<span data-ttu-id="87f6a-112">The data in SCP is modeled as continuous streams of tuples.</span><span class="sxs-lookup"><span data-stu-id="87f6a-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="87f6a-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span><span class="sxs-lookup"><span data-stu-id="87f6a-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![A diagram of a queue feeding data to processing, which feeds a data store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="87f6a-115">In Storm, an application topology defines a graph of computation.</span><span class="sxs-lookup"><span data-stu-id="87f6a-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="87f6a-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span><span class="sxs-lookup"><span data-stu-id="87f6a-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="87f6a-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span><span class="sxs-lookup"><span data-stu-id="87f6a-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="87f6a-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span><span class="sxs-lookup"><span data-stu-id="87f6a-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="87f6a-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span><span class="sxs-lookup"><span data-stu-id="87f6a-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="87f6a-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span><span class="sxs-lookup"><span data-stu-id="87f6a-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="87f6a-121">At-least-once processing is simple and reliable and suits well in many applications.</span><span class="sxs-lookup"><span data-stu-id="87f6a-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="87f6a-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span><span class="sxs-lookup"><span data-stu-id="87f6a-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="87f6a-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span><span class="sxs-lookup"><span data-stu-id="87f6a-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="87f6a-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span><span class="sxs-lookup"><span data-stu-id="87f6a-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="87f6a-125">The .NET and JVM communicate via TCP local socket.</span><span class="sxs-lookup"><span data-stu-id="87f6a-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="87f6a-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span><span class="sxs-lookup"><span data-stu-id="87f6a-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="87f6a-127">To build a data processing application on top of SCP, several steps are needed:</span><span class="sxs-lookup"><span data-stu-id="87f6a-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="87f6a-128">Design and implement the Spouts to pull in data from queue.</span><span class="sxs-lookup"><span data-stu-id="87f6a-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="87f6a-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span><span class="sxs-lookup"><span data-stu-id="87f6a-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="87f6a-130">Design the topology, then submit and run the topology.</span><span class="sxs-lookup"><span data-stu-id="87f6a-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="87f6a-131">The topology defines vertexes and the data flows between the vertexes.</span><span class="sxs-lookup"><span data-stu-id="87f6a-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="87f6a-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span><span class="sxs-lookup"><span data-stu-id="87f6a-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="87f6a-133">The failover and scaling will be taken care of by the Storm task scheduler.</span><span class="sxs-lookup"><span data-stu-id="87f6a-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="87f6a-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span><span class="sxs-lookup"><span data-stu-id="87f6a-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="87f6a-135">SCP Plugin Interface</span><span class="sxs-lookup"><span data-stu-id="87f6a-135">SCP Plugin Interface</span></span>
<span data-ttu-id="87f6a-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span><span class="sxs-lookup"><span data-stu-id="87f6a-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="87f6a-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span><span class="sxs-lookup"><span data-stu-id="87f6a-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="87f6a-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span><span class="sxs-lookup"><span data-stu-id="87f6a-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="87f6a-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span><span class="sxs-lookup"><span data-stu-id="87f6a-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="87f6a-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="87f6a-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="87f6a-141">ISCPSpout</span></span>
* <span data-ttu-id="87f6a-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="87f6a-142">ISCPBolt</span></span>
* <span data-ttu-id="87f6a-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="87f6a-143">ISCPTxSpout</span></span>
* <span data-ttu-id="87f6a-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="87f6a-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="87f6a-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="87f6a-145">ISCPPlugin</span></span>
<span data-ttu-id="87f6a-146">ISCPPlugin is the common interface for all kinds of plugins.</span><span class="sxs-lookup"><span data-stu-id="87f6a-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="87f6a-147">Currently, it is a dummy interface.</span><span class="sxs-lookup"><span data-stu-id="87f6a-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="87f6a-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="87f6a-148">ISCPSpout</span></span>
<span data-ttu-id="87f6a-149">ISCPSpout is the interface for non-transactional spout.</span><span class="sxs-lookup"><span data-stu-id="87f6a-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="87f6a-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span><span class="sxs-lookup"><span data-stu-id="87f6a-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="87f6a-151">If there is nothing to emit, this method should return without emitting anything.</span><span class="sxs-lookup"><span data-stu-id="87f6a-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="87f6a-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span><span class="sxs-lookup"><span data-stu-id="87f6a-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="87f6a-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span><span class="sxs-lookup"><span data-stu-id="87f6a-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="87f6a-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span><span class="sxs-lookup"><span data-stu-id="87f6a-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="87f6a-155">The `seqId` is used to identify the tuple which is acked or failed.</span><span class="sxs-lookup"><span data-stu-id="87f6a-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="87f6a-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span><span class="sxs-lookup"><span data-stu-id="87f6a-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="87f6a-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span><span class="sxs-lookup"><span data-stu-id="87f6a-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="87f6a-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span><span class="sxs-lookup"><span data-stu-id="87f6a-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="87f6a-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="87f6a-159">ISCPBolt</span></span>
<span data-ttu-id="87f6a-160">ISCPBolt is the interface for non-transactional bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="87f6a-161">When new tuple is available, the `Execute()` function will be called to process it.</span><span class="sxs-lookup"><span data-stu-id="87f6a-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="87f6a-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="87f6a-162">ISCPTxSpout</span></span>
<span data-ttu-id="87f6a-163">ISCPTxSpout is the interface for transactional spout.</span><span class="sxs-lookup"><span data-stu-id="87f6a-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="87f6a-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span><span class="sxs-lookup"><span data-stu-id="87f6a-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="87f6a-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span><span class="sxs-lookup"><span data-stu-id="87f6a-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="87f6a-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="87f6a-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="87f6a-167">In `NextTx()`, user can emit data to Java side.</span><span class="sxs-lookup"><span data-stu-id="87f6a-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="87f6a-168">The data will be stored in ZooKeeper to support replay.</span><span class="sxs-lookup"><span data-stu-id="87f6a-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="87f6a-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span><span class="sxs-lookup"><span data-stu-id="87f6a-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="87f6a-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span><span class="sxs-lookup"><span data-stu-id="87f6a-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="87f6a-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span><span class="sxs-lookup"><span data-stu-id="87f6a-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="87f6a-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span><span class="sxs-lookup"><span data-stu-id="87f6a-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="87f6a-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="87f6a-173">ISCPBatchBolt</span></span>
<span data-ttu-id="87f6a-174">ISCPBatchBolt is the interface for transactional bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="87f6a-175">`Execute()` is called when there is new tuple arriving at the bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="87f6a-176">`FinishBatch()` is called when this transaction is ended.</span><span class="sxs-lookup"><span data-stu-id="87f6a-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="87f6a-177">The `parms` input parameter is reserved for future use.</span><span class="sxs-lookup"><span data-stu-id="87f6a-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="87f6a-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="87f6a-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="87f6a-179">It has two fields, `TxId` and `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="87f6a-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="87f6a-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span><span class="sxs-lookup"><span data-stu-id="87f6a-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="87f6a-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span><span class="sxs-lookup"><span data-stu-id="87f6a-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="87f6a-182">The purpose of this design is to support parallel transactions processing.</span><span class="sxs-lookup"><span data-stu-id="87f6a-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="87f6a-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span><span class="sxs-lookup"><span data-stu-id="87f6a-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="87f6a-184">Object Model</span><span class="sxs-lookup"><span data-stu-id="87f6a-184">Object Model</span></span>
<span data-ttu-id="87f6a-185">SCP.NET also provides a simple set of key objects for developers to program with.</span><span class="sxs-lookup"><span data-stu-id="87f6a-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="87f6a-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="87f6a-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="87f6a-187">They will be discussed in the rest part of this section.</span><span class="sxs-lookup"><span data-stu-id="87f6a-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="87f6a-188">Context</span><span class="sxs-lookup"><span data-stu-id="87f6a-188">Context</span></span>
<span data-ttu-id="87f6a-189">Context provides a running environment to the application.</span><span class="sxs-lookup"><span data-stu-id="87f6a-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="87f6a-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span><span class="sxs-lookup"><span data-stu-id="87f6a-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="87f6a-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span><span class="sxs-lookup"><span data-stu-id="87f6a-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="87f6a-192">Static Part</span><span class="sxs-lookup"><span data-stu-id="87f6a-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="87f6a-193">`Logger` is provided for log purpose.</span><span class="sxs-lookup"><span data-stu-id="87f6a-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="87f6a-194">`pluginType` is used to indicate the plugin type of the C\# process.</span><span class="sxs-lookup"><span data-stu-id="87f6a-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="87f6a-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="87f6a-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="87f6a-196">`Config` is provided to get configuration parameters from Java side.</span><span class="sxs-lookup"><span data-stu-id="87f6a-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="87f6a-197">The parameters are passed from Java side when C\# plugin is initialized.</span><span class="sxs-lookup"><span data-stu-id="87f6a-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="87f6a-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="87f6a-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="87f6a-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span><span class="sxs-lookup"><span data-stu-id="87f6a-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="87f6a-200">For example:</span><span class="sxs-lookup"><span data-stu-id="87f6a-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="87f6a-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span><span class="sxs-lookup"><span data-stu-id="87f6a-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="87f6a-202">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="87f6a-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a><span data-ttu-id="87f6a-203">Dynamic Part</span><span class="sxs-lookup"><span data-stu-id="87f6a-203">Dynamic Part</span></span>
<span data-ttu-id="87f6a-204">The following interfaces are pertinent to a certain Context instance.</span><span class="sxs-lookup"><span data-stu-id="87f6a-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="87f6a-205">The Context instance is created by SCP.NET platform and passed to the user code:</span><span class="sxs-lookup"><span data-stu-id="87f6a-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="87f6a-206">For non-transactional spout supporting ack, the following method is provided:</span><span class="sxs-lookup"><span data-stu-id="87f6a-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="87f6a-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span><span class="sxs-lookup"><span data-stu-id="87f6a-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="87f6a-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span><span class="sxs-lookup"><span data-stu-id="87f6a-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="87f6a-209">The following methods are provided.</span><span class="sxs-lookup"><span data-stu-id="87f6a-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="87f6a-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="87f6a-210">StateStore</span></span>
<span data-ttu-id="87f6a-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span><span class="sxs-lookup"><span data-stu-id="87f6a-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="87f6a-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span><span class="sxs-lookup"><span data-stu-id="87f6a-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="87f6a-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span><span class="sxs-lookup"><span data-stu-id="87f6a-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="87f6a-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span><span class="sxs-lookup"><span data-stu-id="87f6a-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="87f6a-215">The `StateStore` object mainly has these methods:</span><span class="sxs-lookup"><span data-stu-id="87f6a-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="87f6a-216">The `State` object mainly has these methods:</span><span class="sxs-lookup"><span data-stu-id="87f6a-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="87f6a-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="87f6a-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="87f6a-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span><span class="sxs-lookup"><span data-stu-id="87f6a-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="87f6a-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="87f6a-219">SCPRuntime</span></span>
<span data-ttu-id="87f6a-220">SCPRuntime provides the following two methods.</span><span class="sxs-lookup"><span data-stu-id="87f6a-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="87f6a-221">`Initialize()` is used to initialize the SCP runtime environment.</span><span class="sxs-lookup"><span data-stu-id="87f6a-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="87f6a-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span><span class="sxs-lookup"><span data-stu-id="87f6a-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="87f6a-223">`LaunchPlugin()` is used to kick off the message processing loop.</span><span class="sxs-lookup"><span data-stu-id="87f6a-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="87f6a-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span><span class="sxs-lookup"><span data-stu-id="87f6a-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="87f6a-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span><span class="sxs-lookup"><span data-stu-id="87f6a-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="87f6a-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="87f6a-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span><span class="sxs-lookup"><span data-stu-id="87f6a-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="87f6a-228">Generally speaking, the SCP plugins may run in two modes here:</span><span class="sxs-lookup"><span data-stu-id="87f6a-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="87f6a-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span><span class="sxs-lookup"><span data-stu-id="87f6a-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="87f6a-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span><span class="sxs-lookup"><span data-stu-id="87f6a-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="87f6a-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span><span class="sxs-lookup"><span data-stu-id="87f6a-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="87f6a-232">Here is an example of launching SCP plugin:</span><span class="sxs-lookup"><span data-stu-id="87f6a-232">Here is an example of launching SCP plugin:</span></span>
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="87f6a-233">Topology Specification Language</span><span class="sxs-lookup"><span data-stu-id="87f6a-233">Topology Specification Language</span></span>
<span data-ttu-id="87f6a-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span><span class="sxs-lookup"><span data-stu-id="87f6a-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="87f6a-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span><span class="sxs-lookup"><span data-stu-id="87f6a-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="87f6a-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span><span class="sxs-lookup"><span data-stu-id="87f6a-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="87f6a-237">SCP.NET has add follow functions to define the Transactional Topology:</span><span class="sxs-lookup"><span data-stu-id="87f6a-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="87f6a-238">**New Functions**</span><span class="sxs-lookup"><span data-stu-id="87f6a-238">**New Functions**</span></span> | <span data-ttu-id="87f6a-239">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="87f6a-239">**Parameters**</span></span> | <span data-ttu-id="87f6a-240">**Description**</span><span class="sxs-lookup"><span data-stu-id="87f6a-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87f6a-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="87f6a-241">**tx-topolopy**</span></span> |<span data-ttu-id="87f6a-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="87f6a-242">topology-name</span></span><br /><span data-ttu-id="87f6a-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="87f6a-243">spout-map</span></span><br /><span data-ttu-id="87f6a-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="87f6a-244">bolt-map</span></span> |<span data-ttu-id="87f6a-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span><span class="sxs-lookup"><span data-stu-id="87f6a-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="87f6a-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="87f6a-246">**scp-tx-spout**</span></span> |<span data-ttu-id="87f6a-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="87f6a-247">exec-name</span></span><br /><span data-ttu-id="87f6a-248">args</span><span class="sxs-lookup"><span data-stu-id="87f6a-248">args</span></span><br /><span data-ttu-id="87f6a-249">fields</span><span class="sxs-lookup"><span data-stu-id="87f6a-249">fields</span></span> |<span data-ttu-id="87f6a-250">Define a transactional spout.</span><span class="sxs-lookup"><span data-stu-id="87f6a-250">Define a transactional spout.</span></span> <span data-ttu-id="87f6a-251">It will run the application with ***exec-name*** using ***args***.</span><span class="sxs-lookup"><span data-stu-id="87f6a-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="87f6a-252">The ***fields*** is the Output Fields for spout</span><span class="sxs-lookup"><span data-stu-id="87f6a-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="87f6a-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="87f6a-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="87f6a-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="87f6a-254">exec-name</span></span><br /><span data-ttu-id="87f6a-255">args</span><span class="sxs-lookup"><span data-stu-id="87f6a-255">args</span></span><br /><span data-ttu-id="87f6a-256">fields</span><span class="sxs-lookup"><span data-stu-id="87f6a-256">fields</span></span> |<span data-ttu-id="87f6a-257">Define a transactional Batch Bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="87f6a-258">It will run the application with ***exec-name*** using ***args.***</span><span class="sxs-lookup"><span data-stu-id="87f6a-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="87f6a-259">The Fields is the Output Fields for bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="87f6a-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="87f6a-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="87f6a-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="87f6a-261">exec-name</span></span><br /><span data-ttu-id="87f6a-262">args</span><span class="sxs-lookup"><span data-stu-id="87f6a-262">args</span></span><br /><span data-ttu-id="87f6a-263">fields</span><span class="sxs-lookup"><span data-stu-id="87f6a-263">fields</span></span> |<span data-ttu-id="87f6a-264">Define a transactional Committer Bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="87f6a-265">It will run the application with ***exec-name*** using ***args***.</span><span class="sxs-lookup"><span data-stu-id="87f6a-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="87f6a-266">The ***fields*** is the Output Fields for bolt</span><span class="sxs-lookup"><span data-stu-id="87f6a-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="87f6a-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="87f6a-267">**nontx-topolopy**</span></span> |<span data-ttu-id="87f6a-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="87f6a-268">topology-name</span></span><br /><span data-ttu-id="87f6a-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="87f6a-269">spout-map</span></span><br /><span data-ttu-id="87f6a-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="87f6a-270">bolt-map</span></span> |<span data-ttu-id="87f6a-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span><span class="sxs-lookup"><span data-stu-id="87f6a-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="87f6a-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="87f6a-272">**scp-spout**</span></span> |<span data-ttu-id="87f6a-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="87f6a-273">exec-name</span></span><br /><span data-ttu-id="87f6a-274">args</span><span class="sxs-lookup"><span data-stu-id="87f6a-274">args</span></span><br /><span data-ttu-id="87f6a-275">fields</span><span class="sxs-lookup"><span data-stu-id="87f6a-275">fields</span></span><br /><span data-ttu-id="87f6a-276">parameters</span><span class="sxs-lookup"><span data-stu-id="87f6a-276">parameters</span></span> |<span data-ttu-id="87f6a-277">Define a nontransactional spout.</span><span class="sxs-lookup"><span data-stu-id="87f6a-277">Define a nontransactional spout.</span></span> <span data-ttu-id="87f6a-278">It will run the application with ***exec-name*** using ***args***.</span><span class="sxs-lookup"><span data-stu-id="87f6a-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="87f6a-279">The ***fields*** is the Output Fields for spout</span><span class="sxs-lookup"><span data-stu-id="87f6a-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="87f6a-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="87f6a-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="87f6a-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="87f6a-281">**scp-bolt**</span></span> |<span data-ttu-id="87f6a-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="87f6a-282">exec-name</span></span><br /><span data-ttu-id="87f6a-283">args</span><span class="sxs-lookup"><span data-stu-id="87f6a-283">args</span></span><br /><span data-ttu-id="87f6a-284">fields</span><span class="sxs-lookup"><span data-stu-id="87f6a-284">fields</span></span><br /><span data-ttu-id="87f6a-285">parameters</span><span class="sxs-lookup"><span data-stu-id="87f6a-285">parameters</span></span> |<span data-ttu-id="87f6a-286">Define a nontransactional Bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="87f6a-287">It will run the application with ***exec-name*** using ***args***.</span><span class="sxs-lookup"><span data-stu-id="87f6a-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="87f6a-288">The ***fields*** is the Output Fields for bolt</span><span class="sxs-lookup"><span data-stu-id="87f6a-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="87f6a-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="87f6a-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="87f6a-290">SCP.NET has follow keys words defined:</span><span class="sxs-lookup"><span data-stu-id="87f6a-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="87f6a-291">**Key Words**</span><span class="sxs-lookup"><span data-stu-id="87f6a-291">**Key Words**</span></span> | <span data-ttu-id="87f6a-292">**Description**</span><span class="sxs-lookup"><span data-stu-id="87f6a-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="87f6a-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="87f6a-293">**:name**</span></span> |<span data-ttu-id="87f6a-294">Define the Topology Name</span><span class="sxs-lookup"><span data-stu-id="87f6a-294">Define the Topology Name</span></span> |
| <span data-ttu-id="87f6a-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="87f6a-295">**:topology**</span></span> |<span data-ttu-id="87f6a-296">Define the Topology using the above functions and build in ones.</span><span class="sxs-lookup"><span data-stu-id="87f6a-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="87f6a-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="87f6a-297">**:p**</span></span> |<span data-ttu-id="87f6a-298">Define the parallelism hint for each spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="87f6a-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="87f6a-299">**:config**</span></span> |<span data-ttu-id="87f6a-300">Define configure parameter or update the existing ones</span><span class="sxs-lookup"><span data-stu-id="87f6a-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="87f6a-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="87f6a-301">**:schema**</span></span> |<span data-ttu-id="87f6a-302">Define the Schema of Stream.</span><span class="sxs-lookup"><span data-stu-id="87f6a-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="87f6a-303">And frequently-used parameters:</span><span class="sxs-lookup"><span data-stu-id="87f6a-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="87f6a-304">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="87f6a-304">**Parameter**</span></span> | <span data-ttu-id="87f6a-305">**Description**</span><span class="sxs-lookup"><span data-stu-id="87f6a-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="87f6a-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="87f6a-306">**"plugin.name"**</span></span> |<span data-ttu-id="87f6a-307">exe file name of the C# plugin</span><span class="sxs-lookup"><span data-stu-id="87f6a-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="87f6a-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="87f6a-308">**"plugin.args"**</span></span> |<span data-ttu-id="87f6a-309">plugin args</span><span class="sxs-lookup"><span data-stu-id="87f6a-309">plugin args</span></span> |
| <span data-ttu-id="87f6a-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="87f6a-310">**"output.schema"**</span></span> |<span data-ttu-id="87f6a-311">Output schema</span><span class="sxs-lookup"><span data-stu-id="87f6a-311">Output schema</span></span> |
| <span data-ttu-id="87f6a-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="87f6a-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="87f6a-313">Whether ack is enabled for nontransactional topology</span><span class="sxs-lookup"><span data-stu-id="87f6a-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="87f6a-314">The runspec command will be deployed together with the bits, the usage is like:</span><span class="sxs-lookup"><span data-stu-id="87f6a-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="87f6a-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span><span class="sxs-lookup"><span data-stu-id="87f6a-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="87f6a-316">The ***classpath*** parameter is also optional.</span><span class="sxs-lookup"><span data-stu-id="87f6a-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="87f6a-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="87f6a-318">Miscellaneous Features</span><span class="sxs-lookup"><span data-stu-id="87f6a-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="87f6a-319">Input and Output Schema Declaration</span><span class="sxs-lookup"><span data-stu-id="87f6a-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="87f6a-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span><span class="sxs-lookup"><span data-stu-id="87f6a-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="87f6a-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span><span class="sxs-lookup"><span data-stu-id="87f6a-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="87f6a-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="87f6a-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="87f6a-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span><span class="sxs-lookup"><span data-stu-id="87f6a-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="87f6a-324">The component can have multi-streams declared.</span><span class="sxs-lookup"><span data-stu-id="87f6a-324">The component can have multi-streams declared.</span></span>

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


<span data-ttu-id="87f6a-325">In Context object, we have the following API added:</span><span class="sxs-lookup"><span data-stu-id="87f6a-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="87f6a-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span><span class="sxs-lookup"><span data-stu-id="87f6a-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="87f6a-327">Multi-Stream Support</span><span class="sxs-lookup"><span data-stu-id="87f6a-327">Multi-Stream Support</span></span>
<span data-ttu-id="87f6a-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span><span class="sxs-lookup"><span data-stu-id="87f6a-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="87f6a-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span><span class="sxs-lookup"><span data-stu-id="87f6a-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="87f6a-330">Two methods in the SCP.NET Context object have been added.</span><span class="sxs-lookup"><span data-stu-id="87f6a-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="87f6a-331">They are used to emit Tuple or Tuples to specify StreamId.</span><span class="sxs-lookup"><span data-stu-id="87f6a-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="87f6a-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span><span class="sxs-lookup"><span data-stu-id="87f6a-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="87f6a-333">The emitting to a non-existing stream will cause runtime exceptions.</span><span class="sxs-lookup"><span data-stu-id="87f6a-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="87f6a-334">Fields Grouping</span><span class="sxs-lookup"><span data-stu-id="87f6a-334">Fields Grouping</span></span>
<span data-ttu-id="87f6a-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="87f6a-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="87f6a-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span><span class="sxs-lookup"><span data-stu-id="87f6a-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="87f6a-337">The byte[] object hash code is the address of this object in memory.</span><span class="sxs-lookup"><span data-stu-id="87f6a-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="87f6a-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span><span class="sxs-lookup"><span data-stu-id="87f6a-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="87f6a-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span><span class="sxs-lookup"><span data-stu-id="87f6a-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="87f6a-340">In **SPEC** file, the syntax is like:</span><span class="sxs-lookup"><span data-stu-id="87f6a-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="87f6a-341">Here,</span><span class="sxs-lookup"><span data-stu-id="87f6a-341">Here,</span></span>

1. <span data-ttu-id="87f6a-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span><span class="sxs-lookup"><span data-stu-id="87f6a-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="87f6a-343">":tx" or ":non-tx" means if it’s transactional topology.</span><span class="sxs-lookup"><span data-stu-id="87f6a-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="87f6a-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span><span class="sxs-lookup"><span data-stu-id="87f6a-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="87f6a-345">[0,1] means a hashset of field Ids, starting from 0.</span><span class="sxs-lookup"><span data-stu-id="87f6a-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="87f6a-346">Hybrid topology</span><span class="sxs-lookup"><span data-stu-id="87f6a-346">Hybrid topology</span></span>
<span data-ttu-id="87f6a-347">The native Storm is written in Java.</span><span class="sxs-lookup"><span data-stu-id="87f6a-347">The native Storm is written in Java.</span></span> <span data-ttu-id="87f6a-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span><span class="sxs-lookup"><span data-stu-id="87f6a-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="87f6a-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span><span class="sxs-lookup"><span data-stu-id="87f6a-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="87f6a-350">Specify Java Spout/Bolt in spec file</span><span class="sxs-lookup"><span data-stu-id="87f6a-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="87f6a-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span><span class="sxs-lookup"><span data-stu-id="87f6a-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="87f6a-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span><span class="sxs-lookup"><span data-stu-id="87f6a-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="87f6a-353">Specify Java Classpath in runSpec Command</span><span class="sxs-lookup"><span data-stu-id="87f6a-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="87f6a-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span><span class="sxs-lookup"><span data-stu-id="87f6a-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="87f6a-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span><span class="sxs-lookup"><span data-stu-id="87f6a-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="87f6a-356">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="87f6a-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="87f6a-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span><span class="sxs-lookup"><span data-stu-id="87f6a-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="87f6a-358">Serialization and Deserialization between Java and C\\</span><span class="sxs-lookup"><span data-stu-id="87f6a-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="87f6a-359">Our SCP component includes Java side and C\# side.</span><span class="sxs-lookup"><span data-stu-id="87f6a-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="87f6a-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span><span class="sxs-lookup"><span data-stu-id="87f6a-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![diagram of java component sending to SCP component sending to Java component](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="87f6a-362">**Serialization in Java side and Deserialization in C\# side**</span><span class="sxs-lookup"><span data-stu-id="87f6a-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="87f6a-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span><span class="sxs-lookup"><span data-stu-id="87f6a-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="87f6a-364">The serialization method in Java side can be specified in SPEC file:</span><span class="sxs-lookup"><span data-stu-id="87f6a-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="87f6a-365">The deserialization method in C\# side should be specified in C\# user code:</span><span class="sxs-lookup"><span data-stu-id="87f6a-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="87f6a-366">This default implementation should handle most cases if the data type is not too complex.</span><span class="sxs-lookup"><span data-stu-id="87f6a-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="87f6a-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span><span class="sxs-lookup"><span data-stu-id="87f6a-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="87f6a-368">The serialize interface in java side is defined as:</span><span class="sxs-lookup"><span data-stu-id="87f6a-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="87f6a-369">The deserialize interface in C\# side is defined as:</span><span class="sxs-lookup"><span data-stu-id="87f6a-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="87f6a-370">public interface ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="87f6a-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="87f6a-371">**Serialization in C\# side and Deserialization in Java side side**</span><span class="sxs-lookup"><span data-stu-id="87f6a-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="87f6a-372">The serialization method in C\# side should be specified in C\# user code:</span><span class="sxs-lookup"><span data-stu-id="87f6a-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="87f6a-373">The Deserialization method in Java side should be specified in SPEC file:</span><span class="sxs-lookup"><span data-stu-id="87f6a-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="87f6a-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="87f6a-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="87f6a-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span><span class="sxs-lookup"><span data-stu-id="87f6a-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="87f6a-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span><span class="sxs-lookup"><span data-stu-id="87f6a-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="87f6a-377">This is the interface for C\# serializer:</span><span class="sxs-lookup"><span data-stu-id="87f6a-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="87f6a-378">This is the interface for Java Deserializer:</span><span class="sxs-lookup"><span data-stu-id="87f6a-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="87f6a-379">SCP Host Mode</span><span class="sxs-lookup"><span data-stu-id="87f6a-379">SCP Host Mode</span></span>
<span data-ttu-id="87f6a-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span><span class="sxs-lookup"><span data-stu-id="87f6a-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="87f6a-381">The spec file looks like this:</span><span class="sxs-lookup"><span data-stu-id="87f6a-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="87f6a-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span><span class="sxs-lookup"><span data-stu-id="87f6a-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="87f6a-383">SCPHost.exe which accepts exactly three parameters:</span><span class="sxs-lookup"><span data-stu-id="87f6a-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="87f6a-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span><span class="sxs-lookup"><span data-stu-id="87f6a-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="87f6a-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span><span class="sxs-lookup"><span data-stu-id="87f6a-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="87f6a-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="87f6a-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="87f6a-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span><span class="sxs-lookup"><span data-stu-id="87f6a-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="87f6a-388">So SCP platform can get full control of the whole processing logic.</span><span class="sxs-lookup"><span data-stu-id="87f6a-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="87f6a-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span><span class="sxs-lookup"><span data-stu-id="87f6a-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="87f6a-390">SCP Programming Examples</span><span class="sxs-lookup"><span data-stu-id="87f6a-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="87f6a-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="87f6a-391">HelloWorld</span></span>
<span data-ttu-id="87f6a-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="87f6a-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="87f6a-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span><span class="sxs-lookup"><span data-stu-id="87f6a-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="87f6a-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span><span class="sxs-lookup"><span data-stu-id="87f6a-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="87f6a-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="87f6a-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span><span class="sxs-lookup"><span data-stu-id="87f6a-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="87f6a-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span><span class="sxs-lookup"><span data-stu-id="87f6a-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="87f6a-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span><span class="sxs-lookup"><span data-stu-id="87f6a-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="87f6a-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span><span class="sxs-lookup"><span data-stu-id="87f6a-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="87f6a-400">If Fail() is called, the failed tuple will be replayed:</span><span class="sxs-lookup"><span data-stu-id="87f6a-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="87f6a-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="87f6a-401">HelloWorldTx</span></span>
<span data-ttu-id="87f6a-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span><span class="sxs-lookup"><span data-stu-id="87f6a-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="87f6a-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="87f6a-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="87f6a-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="87f6a-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="87f6a-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="87f6a-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="87f6a-407">The **count-sum** bolt will summarize the total count.</span><span class="sxs-lookup"><span data-stu-id="87f6a-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="87f6a-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span><span class="sxs-lookup"><span data-stu-id="87f6a-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="87f6a-409">In this example, it has a static member variable:</span><span class="sxs-lookup"><span data-stu-id="87f6a-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="87f6a-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span><span class="sxs-lookup"><span data-stu-id="87f6a-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

<span data-ttu-id="87f6a-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span><span class="sxs-lookup"><span data-stu-id="87f6a-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="87f6a-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="87f6a-412">HybridTopology</span></span>
<span data-ttu-id="87f6a-413">This topology contains a Java Spout and a C\# Bolt.</span><span class="sxs-lookup"><span data-stu-id="87f6a-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="87f6a-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span><span class="sxs-lookup"><span data-stu-id="87f6a-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="87f6a-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span><span class="sxs-lookup"><span data-stu-id="87f6a-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="87f6a-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="87f6a-416">SCPHostDemo</span></span>
<span data-ttu-id="87f6a-417">This example is the same as HelloWorld in essence.</span><span class="sxs-lookup"><span data-stu-id="87f6a-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="87f6a-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="87f6a-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="87f6a-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span><span class="sxs-lookup"><span data-stu-id="87f6a-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87f6a-420">Next Steps</span><span class="sxs-lookup"><span data-stu-id="87f6a-420">Next Steps</span></span>
<span data-ttu-id="87f6a-421">For examples of Storm topologies created using SCP, see the following:</span><span class="sxs-lookup"><span data-stu-id="87f6a-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="87f6a-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87f6a-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="87f6a-423">Process events from Azure Event Hubs with Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="87f6a-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="87f6a-424">Create multiple data streams in a C# Storm topology</span><span class="sxs-lookup"><span data-stu-id="87f6a-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="87f6a-425">Use Power Bi to visualize data from a Storm topology</span><span class="sxs-lookup"><span data-stu-id="87f6a-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="87f6a-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="87f6a-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="87f6a-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span><span class="sxs-lookup"><span data-stu-id="87f6a-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="87f6a-428">Correlate events using Storm and HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="87f6a-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)



