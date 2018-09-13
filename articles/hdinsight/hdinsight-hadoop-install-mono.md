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
# <a name="install-or-update-mono-on-hdinsight"></a>Install or update Mono on HDInsight

Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.

Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications. For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md). To install a different version on your cluster, use the script action in this document. 

## <a name="how-it-works"></a>How it works

This script accepts the following parameter:

* __Mono version number__: The version of Mono to install. The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

The script installs the following Mono packages:

* __mono-complete__

* __ca-certificates-mono__

## <a name="the-script"></a>The script

__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Requirements__:

* The script must be applied on the __head nodes__ and __worker nodes__.

## <a name="to-use-the-script"></a>To use the script

For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document. You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.

While following the script action document, use the following URI:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

To specify the Mono version that is installed, use the version number in the __Parameters__ field. For example, enter `5.4` to install Mono 5.4.

> [!NOTE]
> When configuring HDInsight with this script, mark the script as __Persisted__. This setting allows HDInsight to apply the script to worker nodes added through scaling operations.

## <a name="next-steps"></a>Next steps

You have learned how to upgrade or install a specific version of Mono on HDInsight. For more information on using .NET applications with Mono on HDInsight, see the following documents:

* [Use .NET for streaming MapReduce on HDInsight](hadoop/apache-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Use .NET with Hive and Pig on HDInsight](hadoop/apache-hadoop-hive-pig-udf-dotnet-csharp.md)
* [Develop C# solutions with Storm on HDInsight](storm/apache-storm-develop-csharp-visual-studio-topology.md)
* [Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)

For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)
