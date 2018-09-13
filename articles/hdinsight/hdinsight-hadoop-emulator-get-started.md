---
title: Use a Hadoop sandbox to learn about Hadoop | Microsoft Docs
description: 'To start learning about using the Hadoop ecosystem, you can set up a Hadoop sandbox from Hortonworks on an Azure virtual machine. '
keywords: hadoop emulator,hadoop sandbox
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: ''
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: nitinme
ms.openlocfilehash: 43618cd68a44678471d1d15275a507343110fc3f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552021"
---
# <a name="get-started-in-the-hadoop-ecosystem-with-a-hadoop-sandbox-on-a-virtual-machine"></a><span data-ttu-id="e8770-104">Get started in the Hadoop ecosystem with a Hadoop Sandbox on a virtual machine</span><span class="sxs-lookup"><span data-stu-id="e8770-104">Get started in the Hadoop ecosystem with a Hadoop Sandbox on a virtual machine</span></span>

<span data-ttu-id="e8770-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span><span class="sxs-lookup"><span data-stu-id="e8770-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="e8770-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span><span class="sxs-lookup"><span data-stu-id="e8770-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="e8770-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e8770-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="e8770-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8770-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8770-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e8770-109">Prerequisites</span></span>
* <span data-ttu-id="e8770-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="e8770-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="e8770-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="e8770-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="e8770-112">Download and install the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e8770-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="e8770-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="e8770-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>
2. <span data-ttu-id="e8770-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hrotonworks Sandbox on a VM.</span><span class="sxs-lookup"><span data-stu-id="e8770-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hrotonworks Sandbox on a VM.</span></span> <span data-ttu-id="e8770-115">You will be prompted to register with Hortonworks before the download begins.</span><span class="sxs-lookup"><span data-stu-id="e8770-115">You will be prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="e8770-116">It takes one to two hours to download depending on your network speed.</span><span class="sxs-lookup"><span data-stu-id="e8770-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Link image for download Hortonworks Sandbox for VirtualBox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="e8770-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8770-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="e8770-119">To download an older HDP version sandbox, expand the archive:</span><span class="sxs-lookup"><span data-stu-id="e8770-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Hortonworks Sandbox archive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="e8770-121">Start the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e8770-121">Start the virtual machine</span></span>

1. <span data-ttu-id="e8770-122">Open Oracle VM VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="e8770-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="e8770-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span><span class="sxs-lookup"><span data-stu-id="e8770-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="e8770-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span><span class="sxs-lookup"><span data-stu-id="e8770-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="e8770-125">Once the virtual machine has finished the boot process, it will display login instructions.</span><span class="sxs-lookup"><span data-stu-id="e8770-125">Once the virtual machine has finished the boot process, it will display login instructions.</span></span>
   
    ![Normal start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="e8770-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="e8770-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="e8770-128">Set Sandbox passwords</span><span class="sxs-lookup"><span data-stu-id="e8770-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="e8770-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span><span class="sxs-lookup"><span data-stu-id="e8770-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="e8770-130">Use the information on this page to login to the sandbox using SSH.</span><span class="sxs-lookup"><span data-stu-id="e8770-130">Use the information on this page to login to the sandbox using SSH.</span></span> <span data-ttu-id="e8770-131">Use the name and password provided.</span><span class="sxs-lookup"><span data-stu-id="e8770-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e8770-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span><span class="sxs-lookup"><span data-stu-id="e8770-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="e8770-133">The first time you connect using SSH, you will be prompted to change the password for the root account.</span><span class="sxs-lookup"><span data-stu-id="e8770-133">The first time you connect using SSH, you will be prompted to change the password for the root account.</span></span> <span data-ttu-id="e8770-134">Enter a new password, which will be used when you login using SSH in the future.</span><span class="sxs-lookup"><span data-stu-id="e8770-134">Enter a new password, which will be used when you login using SSH in the future.</span></span>
2. <span data-ttu-id="e8770-135">Once logged in, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="e8770-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="e8770-136">When prompted, provide a password for the Ambari admin account.</span><span class="sxs-lookup"><span data-stu-id="e8770-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="e8770-137">This will be used when you access the Ambari Web UI.</span><span class="sxs-lookup"><span data-stu-id="e8770-137">This will be used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="e8770-138">Use Hive commands</span><span class="sxs-lookup"><span data-stu-id="e8770-138">Use Hive commands</span></span>

1. <span data-ttu-id="e8770-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span><span class="sxs-lookup"><span data-stu-id="e8770-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="e8770-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span><span class="sxs-lookup"><span data-stu-id="e8770-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="e8770-141">Use the following to retrieve 10 rows from the `sample_07` table:</span><span class="sxs-lookup"><span data-stu-id="e8770-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="e8770-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8770-142">Next steps</span></span>
* [<span data-ttu-id="e8770-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="e8770-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="e8770-144">Learning the ropes of the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="e8770-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="e8770-145">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="e8770-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)




