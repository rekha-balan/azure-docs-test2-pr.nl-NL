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
# <a name="get-started-in-the-hadoop-ecosystem-with-a-hadoop-sandbox-on-a-virtual-machine"></a>Get started in the Hadoop ecosystem with a Hadoop Sandbox on a virtual machine

Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem. The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission. Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster. For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Prerequisites
* [Oracle VirtualBox](https://www.virtualbox.org/). Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-the-virtual-machine"></a>Download and install the virtual machine
1. Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).
2. Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hrotonworks Sandbox on a VM. You will be prompted to register with Hortonworks before the download begins. It takes one to two hours to download depending on your network speed.
   
    ![Link image for download Hortonworks Sandbox for VirtualBox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.

To download an older HDP version sandbox, expand the archive:

![Hortonworks Sandbox archive](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a>Start the virtual machine

1. Open Oracle VM VirtualBox.
2. From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.
1. Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**. Once the virtual machine has finished the boot process, it will display login instructions.
   
    ![Normal start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).

## <a name="set-sandbox-passwords"></a>Set Sandbox passwords

1. From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**. Use the information on this page to login to the sandbox using SSH. Use the name and password provided.
   
   > [!NOTE]
   > If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.
   > 
   
    The first time you connect using SSH, you will be prompted to change the password for the root account. Enter a new password, which will be used when you login using SSH in the future.
2. Once logged in, enter the following command:
   
        ambari-admin-password-reset
   
    When prompted, provide a password for the Ambari admin account. This will be used when you access the Ambari Web UI.

## <a name="use-hive-commands"></a>Use Hive commands

1. From an SSH connection to the sandbox, use the following command to start the Hive shell:
   
        hive
2. Once the shell has started, use the following to view the tables that are provided with the sandbox:
   
        show tables;
3. Use the following to retrieve 10 rows from the `sample_07` table:
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Next steps
* [Learn how to use Visual Studio with the Hortonworks Sandbox](hdinsight-hadoop-emulator-visual-studio.md)
* [Learning the ropes of the Hortonworks Sandbox](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)




