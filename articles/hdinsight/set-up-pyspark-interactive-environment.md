---
title: Azure HDInsight Tools - Set Up PySpark Interactive Environment for Visual Studio Code
description: Learn how to use the Azure HDInsight Tools for Visual Studio Code to create and submit queries and scripts.
keywords: VScode,Azure HDInsight Tools,Hive,Python,PySpark,Spark,HDInsight,Hadoop,LLAP,Interactive Hive,Interactive Query
services: hdinsight
ms.service: hdinsight
author: jejiang
ms.author: jejiang
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 10/27/2017
ms.openlocfilehash: 74ac93821ba724ccad602a338cda1fe543495e8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856027"
---
# <a name="set-up-the-pyspark-interactive-environment-for-visual-studio-code"></a><span data-ttu-id="7a6e6-104">Set up the PySpark interactive environment for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7a6e6-104">Set up the PySpark interactive environment for Visual Studio Code</span></span>

<span data-ttu-id="7a6e6-105">The following steps show you how to install Python packages by running **HDInsight: PySpark Interactive**.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-105">The following steps show you how to install Python packages by running **HDInsight: PySpark Interactive**.</span></span>


## <a name="set-up-the-pyspark-interactive-environment-on-macos-and-linux"></a><span data-ttu-id="7a6e6-106">Set up the PySpark interactive environment on macOS and Linux</span><span class="sxs-lookup"><span data-stu-id="7a6e6-106">Set up the PySpark interactive environment on macOS and Linux</span></span>
<span data-ttu-id="7a6e6-107">If you're using **python 3.x**, you need to use the command **pip3** for the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a6e6-107">If you're using **python 3.x**, you need to use the command **pip3** for the following steps:</span></span>

1. <span data-ttu-id="7a6e6-108">Make sure **Python** and **pip** are installed.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-108">Make sure **Python** and **pip** are installed.</span></span>
 
    ![Python pip version](./media/set-up-pyspark-interactive-environment/check-python-pip-version.png)

2.  <span data-ttu-id="7a6e6-110">Install Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-110">Install Jupyter.</span></span>
    ```
    sudo pip install jupyter
    ```
   <span data-ttu-id="7a6e6-111">You might see the following error message on Linux and macOS:</span><span class="sxs-lookup"><span data-stu-id="7a6e6-111">You might see the following error message on Linux and macOS:</span></span>

   ![Error 1](./media/set-up-pyspark-interactive-environment/error1.png)

   ```Resolve:
    sudo pip uninstall asyncio
    sudo pip install trollies
    ```

3. <span data-ttu-id="7a6e6-113">Install **libkrb5-dev** (for Linux only).</span><span class="sxs-lookup"><span data-stu-id="7a6e6-113">Install **libkrb5-dev** (for Linux only).</span></span> <span data-ttu-id="7a6e6-114">You might see the following error message:</span><span class="sxs-lookup"><span data-stu-id="7a6e6-114">You might see the following error message:</span></span>

   ![Error 2](./media/set-up-pyspark-interactive-environment/error2.png)
       
   ```Resolve:
   sudo apt-get install libkrb5-dev 
   ```

3. <span data-ttu-id="7a6e6-116">Install **sparkmagic**.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-116">Install **sparkmagic**.</span></span>
   ```
   sudo pip install sparkmagic
   ```

4. <span data-ttu-id="7a6e6-117">Make sure that **ipywidgets** is properly installed by running the following:</span><span class="sxs-lookup"><span data-stu-id="7a6e6-117">Make sure that **ipywidgets** is properly installed by running the following:</span></span>
   ```
   sudo jupyter nbextension enable --py --sys-prefix widgetsnbextension
   ```
   ![Install the wrapper kernels](./media/set-up-pyspark-interactive-environment/ipywidget-enable.png)
 

5. <span data-ttu-id="7a6e6-119">Install the wrapper kernels.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-119">Install the wrapper kernels.</span></span> <span data-ttu-id="7a6e6-120">Run **pip show sparkmagic**.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-120">Run **pip show sparkmagic**.</span></span> <span data-ttu-id="7a6e6-121">The output shows the path for the **sparkmagic** installation.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-121">The output shows the path for the **sparkmagic** installation.</span></span> 

    ![sparkmagic location](./media/set-up-pyspark-interactive-environment/sparkmagic-location.png)
   
6. <span data-ttu-id="7a6e6-123">Go to the location, and then run:</span><span class="sxs-lookup"><span data-stu-id="7a6e6-123">Go to the location, and then run:</span></span>

   ```Python2
   sudo jupyter-kernelspec install sparkmagic/kernels/pysparkkernel   
   ```
   ```Python3
   sudo jupyter-kernelspec install sparkmagic/kernels/pyspark3kernel
   ```

   ![jupyter kernelspec install](./media/set-up-pyspark-interactive-environment/jupyter-kernelspec-install.png)
7. <span data-ttu-id="7a6e6-125">Check the installation status.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-125">Check the installation status.</span></span>

    ```
    jupyter-kernelspec list
    ```
    ![jupyter kernelspec list](./media/set-up-pyspark-interactive-environment/jupyter-kernelspec-list.png)

    <span data-ttu-id="7a6e6-127">For available kernels:</span><span class="sxs-lookup"><span data-stu-id="7a6e6-127">For available kernels:</span></span> 
    - <span data-ttu-id="7a6e6-128">**python2** and **pysparkkernel** correspond to **python 2.x**.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-128">**python2** and **pysparkkernel** correspond to **python 2.x**.</span></span> 
    - <span data-ttu-id="7a6e6-129">**python3** and **pyspark3kernel** correspond to **python 3.x**.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-129">**python3** and **pyspark3kernel** correspond to **python 3.x**.</span></span> 

8. <span data-ttu-id="7a6e6-130">Restart VS Code, and then go back to the script editor that's running **HDInsight: PySpark Interactive**.</span><span class="sxs-lookup"><span data-stu-id="7a6e6-130">Restart VS Code, and then go back to the script editor that's running **HDInsight: PySpark Interactive**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a6e6-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a6e6-131">Next steps</span></span>

### <a name="demo"></a><span data-ttu-id="7a6e6-132">Demo</span><span class="sxs-lookup"><span data-stu-id="7a6e6-132">Demo</span></span>
* <span data-ttu-id="7a6e6-133">HDInsight for VS Code: [Video](https://go.microsoft.com/fwlink/?linkid=858706)</span><span class="sxs-lookup"><span data-stu-id="7a6e6-133">HDInsight for VS Code: [Video](https://go.microsoft.com/fwlink/?linkid=858706)</span></span>

### <a name="tools-and-extensions"></a><span data-ttu-id="7a6e6-134">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="7a6e6-134">Tools and extensions</span></span>
* [<span data-ttu-id="7a6e6-135">Use Azure HDInsight Tool for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7a6e6-135">Use Azure HDInsight Tool for Visual Studio Code</span></span>](hdinsight-for-vscode.md)
* [<span data-ttu-id="7a6e6-136">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span><span class="sxs-lookup"><span data-stu-id="7a6e6-136">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span></span>](spark/apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7a6e6-137">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span><span class="sxs-lookup"><span data-stu-id="7a6e6-137">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](spark/apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="7a6e6-138">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span><span class="sxs-lookup"><span data-stu-id="7a6e6-138">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](spark/apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7a6e6-139">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span><span class="sxs-lookup"><span data-stu-id="7a6e6-139">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](spark/apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="7a6e6-140">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="7a6e6-140">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hadoop/hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="7a6e6-141">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6e6-141">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](spark/apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="7a6e6-142">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6e6-142">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](spark/apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7a6e6-143">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="7a6e6-143">Use external packages with Jupyter notebooks</span></span>](spark/apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="7a6e6-144">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="7a6e6-144">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](spark/apache-spark-jupyter-notebook-install-locally.md)
* [<span data-ttu-id="7a6e6-145">Visualize Hive data with Microsoft Power BI in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6e6-145">Visualize Hive data with Microsoft Power BI in Azure HDInsight</span></span>](hadoop/apache-hadoop-connect-hive-power-bi.md)
* [<span data-ttu-id="7a6e6-146">Use Zeppelin to run Hive queries in Azure HDInsight </span><span class="sxs-lookup"><span data-stu-id="7a6e6-146">Use Zeppelin to run Hive queries in Azure HDInsight </span></span>](hdinsight-connect-hive-zeppelin.md)
