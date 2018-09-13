---
title: Learn using a Hadoop sandbox - emulator - Azure HDInsight
description: 'To start learning about using the Hadoop ecosystem, you can set up a Hadoop sandbox from Hortonworks on an Azure virtual machine. '
keywords: hadoop emulator,hadoop sandbox
ms.reviewer: jasonh
services: hdinsight
author: jasonwhowell
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 12/11/2017
ms.author: jasonh
ms.openlocfilehash: 66450077de4748bcd8703080d33f37169671ebe3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966573"
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="129d6-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span><span class="sxs-lookup"><span data-stu-id="129d6-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="129d6-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span><span class="sxs-lookup"><span data-stu-id="129d6-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="129d6-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span><span class="sxs-lookup"><span data-stu-id="129d6-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="129d6-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="129d6-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="129d6-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](apache-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="129d6-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](apache-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="129d6-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="129d6-109">Prerequisites</span></span>
* <span data-ttu-id="129d6-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="129d6-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="129d6-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="129d6-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="129d6-112">Download and install the virtual machine</span><span class="sxs-lookup"><span data-stu-id="129d6-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="129d6-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="129d6-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="129d6-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span><span class="sxs-lookup"><span data-stu-id="129d6-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="129d6-115">You are prompted to register with Hortonworks before the download begins.</span><span class="sxs-lookup"><span data-stu-id="129d6-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="129d6-116">It takes one to two hours to download depending on your network speed.</span><span class="sxs-lookup"><span data-stu-id="129d6-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Link image for download Hortonworks Sandbox for VirtualBox](./media/apache-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="129d6-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="129d6-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="129d6-119">To download an older HDP version sandbox, expand the archive:</span><span class="sxs-lookup"><span data-stu-id="129d6-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Hortonworks Sandbox archive](./media/apache-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="129d6-121">Start the virtual machine</span><span class="sxs-lookup"><span data-stu-id="129d6-121">Start the virtual machine</span></span>

1. <span data-ttu-id="129d6-122">Open Oracle VM VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="129d6-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="129d6-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span><span class="sxs-lookup"><span data-stu-id="129d6-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="129d6-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span><span class="sxs-lookup"><span data-stu-id="129d6-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="129d6-125">Once the virtual machine has finished the boot process, it displays login instructions.</span><span class="sxs-lookup"><span data-stu-id="129d6-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![Normal start](./media/apache-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="129d6-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="129d6-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="129d6-128">Set Sandbox passwords</span><span class="sxs-lookup"><span data-stu-id="129d6-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="129d6-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span><span class="sxs-lookup"><span data-stu-id="129d6-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="129d6-130">Use the information on this page to log in to the sandbox using SSH.</span><span class="sxs-lookup"><span data-stu-id="129d6-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="129d6-131">Use the name and password provided.</span><span class="sxs-lookup"><span data-stu-id="129d6-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="129d6-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span><span class="sxs-lookup"><span data-stu-id="129d6-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="129d6-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span><span class="sxs-lookup"><span data-stu-id="129d6-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="129d6-134">Enter a new password, which you use when you log in using SSH.</span><span class="sxs-lookup"><span data-stu-id="129d6-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="129d6-135">Once logged in, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="129d6-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="129d6-136">When prompted, provide a password for the Ambari admin account.</span><span class="sxs-lookup"><span data-stu-id="129d6-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="129d6-137">This is used when you access the Ambari Web UI.</span><span class="sxs-lookup"><span data-stu-id="129d6-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="129d6-138">Use Hive commands</span><span class="sxs-lookup"><span data-stu-id="129d6-138">Use Hive commands</span></span>

1. <span data-ttu-id="129d6-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span><span class="sxs-lookup"><span data-stu-id="129d6-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="129d6-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span><span class="sxs-lookup"><span data-stu-id="129d6-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="129d6-141">Use the following to retrieve 10 rows from the `sample_07` table:</span><span class="sxs-lookup"><span data-stu-id="129d6-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="129d6-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="129d6-142">Next steps</span></span>
* [<span data-ttu-id="129d6-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="129d6-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](../hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="129d6-144">Learning the ropes of the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="129d6-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="129d6-145">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="129d6-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

