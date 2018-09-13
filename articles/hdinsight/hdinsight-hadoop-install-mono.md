---
title: Install or update Mono on HDInsight - Azure
description: Learn how to use a specific version of Mono with HDInsight cluster. Mono is used to run .NET applications on Linux-based HDInsight clusters.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 04/10/2018
ms.author: jasonh
ms.custom: hdinsightactive
ms.openlocfilehash: db460c6ebe934fa9ca9b6b42d517f39acbecf0c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865944"
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="9ffae-104">Install or update Mono on HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ffae-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="9ffae-105">Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span><span class="sxs-lookup"><span data-stu-id="9ffae-105">Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="9ffae-106">Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications.</span><span class="sxs-lookup"><span data-stu-id="9ffae-106">Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications.</span></span> <span data-ttu-id="9ffae-107">For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9ffae-107">For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="9ffae-108">To install a different version on your cluster, use the script action in this document.</span><span class="sxs-lookup"><span data-stu-id="9ffae-108">To install a different version on your cluster, use the script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="9ffae-109">How it works</span><span class="sxs-lookup"><span data-stu-id="9ffae-109">How it works</span></span>

<span data-ttu-id="9ffae-110">This script accepts the following parameter:</span><span class="sxs-lookup"><span data-stu-id="9ffae-110">This script accepts the following parameter:</span></span>

* <span data-ttu-id="9ffae-111">__Mono version number__: The version of Mono to install.</span><span class="sxs-lookup"><span data-stu-id="9ffae-111">__Mono version number__: The version of Mono to install.</span></span> <span data-ttu-id="9ffae-112">The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="9ffae-112">The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="9ffae-113">The script installs the following Mono packages:</span><span class="sxs-lookup"><span data-stu-id="9ffae-113">The script installs the following Mono packages:</span></span>

* <span data-ttu-id="9ffae-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="9ffae-114">__mono-complete__</span></span>

* <span data-ttu-id="9ffae-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="9ffae-115">__ca-certificates-mono__</span></span>

## <a name="the-script"></a><span data-ttu-id="9ffae-116">The script</span><span class="sxs-lookup"><span data-stu-id="9ffae-116">The script</span></span>

<span data-ttu-id="9ffae-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="9ffae-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="9ffae-118">__Requirements__:</span><span class="sxs-lookup"><span data-stu-id="9ffae-118">__Requirements__:</span></span>

* <span data-ttu-id="9ffae-119">The script must be applied on the __head nodes__ and __worker nodes__.</span><span class="sxs-lookup"><span data-stu-id="9ffae-119">The script must be applied on the __head nodes__ and __worker nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="9ffae-120">To use the script</span><span class="sxs-lookup"><span data-stu-id="9ffae-120">To use the script</span></span>

<span data-ttu-id="9ffae-121">For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span><span class="sxs-lookup"><span data-stu-id="9ffae-121">For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="9ffae-122">You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9ffae-122">You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="9ffae-123">While following the script action document, use the following URI:</span><span class="sxs-lookup"><span data-stu-id="9ffae-123">While following the script action document, use the following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

<span data-ttu-id="9ffae-124">To specify the Mono version that is installed, use the version number in the __Parameters__ field.</span><span class="sxs-lookup"><span data-stu-id="9ffae-124">To specify the Mono version that is installed, use the version number in the __Parameters__ field.</span></span> <span data-ttu-id="9ffae-125">For example, enter `5.4` to install Mono 5.4.</span><span class="sxs-lookup"><span data-stu-id="9ffae-125">For example, enter `5.4` to install Mono 5.4.</span></span>

> [!NOTE]
> <span data-ttu-id="9ffae-126">When configuring HDInsight with this script, mark the script as __Persisted__.</span><span class="sxs-lookup"><span data-stu-id="9ffae-126">When configuring HDInsight with this script, mark the script as __Persisted__.</span></span> <span data-ttu-id="9ffae-127">This setting allows HDInsight to apply the script to worker nodes added through scaling operations.</span><span class="sxs-lookup"><span data-stu-id="9ffae-127">This setting allows HDInsight to apply the script to worker nodes added through scaling operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ffae-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ffae-128">Next steps</span></span>

<span data-ttu-id="9ffae-129">You have learned how to upgrade or install a specific version of Mono on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9ffae-129">You have learned how to upgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="9ffae-130">For more information on using .NET applications with Mono on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="9ffae-130">For more information on using .NET applications with Mono on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="9ffae-131">Use .NET for streaming MapReduce on HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ffae-131">Use .NET for streaming MapReduce on HDInsight</span></span>](hadoop/apache-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="9ffae-132">Use .NET with Hive and Pig on HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ffae-132">Use .NET with Hive and Pig on HDInsight</span></span>](hadoop/apache-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="9ffae-133">Develop C# solutions with Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ffae-133">Develop C# solutions with Storm on HDInsight</span></span>](storm/apache-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="9ffae-134">Migrate .NET solutions to Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ffae-134">Migrate .NET solutions to Linux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="9ffae-135">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="9ffae-135">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
