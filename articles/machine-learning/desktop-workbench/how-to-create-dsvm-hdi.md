---
title: How to create DSVM and HDI as compute targets for Azure ML
description: Create DSVM and HDI Spark cluster as compute targets for Azure ML experimentation.
services: machine-learning
author: hning86
ms.author: haining
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 09/26/2017
ms.openlocfilehash: 211f60b9c25b4bd20769f6a4840afaecf8373b9f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865165"
---
# <a name="create-dsvm-and-hdi-spark-cluster-as-compute-targets"></a><span data-ttu-id="d03c0-103">Create DSVM and HDI Spark cluster as compute targets</span><span class="sxs-lookup"><span data-stu-id="d03c0-103">Create DSVM and HDI Spark cluster as compute targets</span></span>

<span data-ttu-id="d03c0-104">You can easily scale up or scale out your machine learning experiment by adding additional compute targets such as Ubuntu-based DSVM (Data Science Virtual Machine), and Apache Spark for Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d03c0-104">You can easily scale up or scale out your machine learning experiment by adding additional compute targets such as Ubuntu-based DSVM (Data Science Virtual Machine), and Apache Spark for Azure HDInsight cluster.</span></span> <span data-ttu-id="d03c0-105">This article walks you through the steps of creating these compute targets in Azure.</span><span class="sxs-lookup"><span data-stu-id="d03c0-105">This article walks you through the steps of creating these compute targets in Azure.</span></span> <span data-ttu-id="d03c0-106">For more information on Azure ML compute targets, refer to [overview of Azure Machine Learning experimentation service](experimentation-service-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="d03c0-106">For more information on Azure ML compute targets, refer to [overview of Azure Machine Learning experimentation service](experimentation-service-configuration.md).</span></span>

>[!NOTE]
><span data-ttu-id="d03c0-107">You need to ensure you have proper permissions to create resources such as VM and HDI clusters in Azure before you proceed.</span><span class="sxs-lookup"><span data-stu-id="d03c0-107">You need to ensure you have proper permissions to create resources such as VM and HDI clusters in Azure before you proceed.</span></span> <span data-ttu-id="d03c0-108">Also both of these resources can consume many compute cores depending on your configuration.</span><span class="sxs-lookup"><span data-stu-id="d03c0-108">Also both of these resources can consume many compute cores depending on your configuration.</span></span> <span data-ttu-id="d03c0-109">Make sure your subscription has enough capacity for the virtual CPU cores.</span><span class="sxs-lookup"><span data-stu-id="d03c0-109">Make sure your subscription has enough capacity for the virtual CPU cores.</span></span> <span data-ttu-id="d03c0-110">You can always get in touch with Azure support to increase the maximum number of cores allowed in your subscription.</span><span class="sxs-lookup"><span data-stu-id="d03c0-110">You can always get in touch with Azure support to increase the maximum number of cores allowed in your subscription.</span></span>

## <a name="create-an-ubuntu-dsvm-in-azure-portal"></a><span data-ttu-id="d03c0-111">Create an Ubuntu DSVM in Azure portal</span><span class="sxs-lookup"><span data-stu-id="d03c0-111">Create an Ubuntu DSVM in Azure portal</span></span>

<span data-ttu-id="d03c0-112">You can create a DSVM from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d03c0-112">You can create a DSVM from Azure portal.</span></span> 

1. <span data-ttu-id="d03c0-113">Log on to Azure portal from https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="d03c0-113">Log on to Azure portal from https://portal.azure.com</span></span>
2. <span data-ttu-id="d03c0-114">Click on the **+NEW** link, and search for "data science virtual machine for Linux".</span><span class="sxs-lookup"><span data-stu-id="d03c0-114">Click on the **+NEW** link, and search for "data science virtual machine for Linux".</span></span>
    <span data-ttu-id="d03c0-115">![Ubuntu](media/how-to-create-dsvm-hdi/ubuntu_dsvm.png)</span><span class="sxs-lookup"><span data-stu-id="d03c0-115">![Ubuntu](media/how-to-create-dsvm-hdi/ubuntu_dsvm.png)</span></span>
4. <span data-ttu-id="d03c0-116">Choose **Data Science Virtual Machine for Linux (Ubuntu)** in the list, and follow the on-screen instructions to create the DSVM.</span><span class="sxs-lookup"><span data-stu-id="d03c0-116">Choose **Data Science Virtual Machine for Linux (Ubuntu)** in the list, and follow the on-screen instructions to create the DSVM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d03c0-117">Make sure you choose **Password** as the _Authentication type_.</span><span class="sxs-lookup"><span data-stu-id="d03c0-117">Make sure you choose **Password** as the _Authentication type_.</span></span>

![use pwd](media/how-to-create-dsvm-hdi/use_pwd.png)

## <a name="create-an-ubuntu-dsvm-using-azure-cli"></a><span data-ttu-id="d03c0-119">Create an Ubuntu DSVM using azure-cli</span><span class="sxs-lookup"><span data-stu-id="d03c0-119">Create an Ubuntu DSVM using azure-cli</span></span>

<span data-ttu-id="d03c0-120">You can also use an Azure resource management template to deploy a DSVM.</span><span class="sxs-lookup"><span data-stu-id="d03c0-120">You can also use an Azure resource management template to deploy a DSVM.</span></span>

>[!NOTE]
><span data-ttu-id="d03c0-121">All following commands are assumed to be issued from the root folder of an Azure ML project.</span><span class="sxs-lookup"><span data-stu-id="d03c0-121">All following commands are assumed to be issued from the root folder of an Azure ML project.</span></span>

<span data-ttu-id="d03c0-122">First, create a `mydsvm.json` file using your favorite text editor in the `docs` folder.</span><span class="sxs-lookup"><span data-stu-id="d03c0-122">First, create a `mydsvm.json` file using your favorite text editor in the `docs` folder.</span></span> <span data-ttu-id="d03c0-123">(If you don't have a `docs` folder in the project root folder, create one.) We use this file to configure some basic parameters for the Azure resource management template.</span><span class="sxs-lookup"><span data-stu-id="d03c0-123">(If you don't have a `docs` folder in the project root folder, create one.) We use this file to configure some basic parameters for the Azure resource management template.</span></span> 

<span data-ttu-id="d03c0-124">Copy and paste the following JSON snippet into the `mydsvm.json` file, and fill in the appropriate values:</span><span class="sxs-lookup"><span data-stu-id="d03c0-124">Copy and paste the following JSON snippet into the `mydsvm.json` file, and fill in the appropriate values:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "adminUsername": { "value" : "<admin username>"},
     "adminPassword": { "value" : "<admin password>"},
     "vmName": { "value" : "<vm name>"},
     "vmSize": { "value" : "<vm size>"}
  }
}
```

<span data-ttu-id="d03c0-125">For the _vmSize_ field, you can use any suppported VM size listed in the [Ubuntu DSVM Azure resource management template](https://github.com/Azure/DataScienceVM/blob/master/Scripts/CreateDSVM/Ubuntu/multiazuredeploywithext.json).</span><span class="sxs-lookup"><span data-stu-id="d03c0-125">For the _vmSize_ field, you can use any suppported VM size listed in the [Ubuntu DSVM Azure resource management template](https://github.com/Azure/DataScienceVM/blob/master/Scripts/CreateDSVM/Ubuntu/multiazuredeploywithext.json).</span></span> <span data-ttu-id="d03c0-126">We recommend you use one of the below sizes as compute targets for Azure ML.</span><span class="sxs-lookup"><span data-stu-id="d03c0-126">We recommend you use one of the below sizes as compute targets for Azure ML.</span></span> 


>[!TIP]
> <span data-ttu-id="d03c0-127">For [deep learning workloads](how-to-use-gpu.md) you can deploy to GPU powered VMs.</span><span class="sxs-lookup"><span data-stu-id="d03c0-127">For [deep learning workloads](how-to-use-gpu.md) you can deploy to GPU powered VMs.</span></span>

- [<span data-ttu-id="d03c0-128">General Purpose VMs</span><span class="sxs-lookup"><span data-stu-id="d03c0-128">General Purpose VMs</span></span>](../../virtual-machines/linux/sizes-general.md)
  - <span data-ttu-id="d03c0-129">Standard_DS2_v2</span><span class="sxs-lookup"><span data-stu-id="d03c0-129">Standard_DS2_v2</span></span> 
  - <span data-ttu-id="d03c0-130">Standard_DS3_v2</span><span class="sxs-lookup"><span data-stu-id="d03c0-130">Standard_DS3_v2</span></span> 
  - <span data-ttu-id="d03c0-131">Standard_DS4_v2</span><span class="sxs-lookup"><span data-stu-id="d03c0-131">Standard_DS4_v2</span></span> 
  - <span data-ttu-id="d03c0-132">Standard_DS12_v2</span><span class="sxs-lookup"><span data-stu-id="d03c0-132">Standard_DS12_v2</span></span> 
  - <span data-ttu-id="d03c0-133">Standard_DS13_v2</span><span class="sxs-lookup"><span data-stu-id="d03c0-133">Standard_DS13_v2</span></span> 
  - <span data-ttu-id="d03c0-134">Standard_DS14_v2</span><span class="sxs-lookup"><span data-stu-id="d03c0-134">Standard_DS14_v2</span></span> 
- [<span data-ttu-id="d03c0-135">GPU powered VMs</span><span class="sxs-lookup"><span data-stu-id="d03c0-135">GPU powered VMs</span></span>](../../virtual-machines/linux/sizes-gpu.md)
  - <span data-ttu-id="d03c0-136">Standard_NC6</span><span class="sxs-lookup"><span data-stu-id="d03c0-136">Standard_NC6</span></span> 
  - <span data-ttu-id="d03c0-137">Standard_NC12</span><span class="sxs-lookup"><span data-stu-id="d03c0-137">Standard_NC12</span></span> 
  - <span data-ttu-id="d03c0-138">Standard_NC24</span><span class="sxs-lookup"><span data-stu-id="d03c0-138">Standard_NC24</span></span> 
 

<span data-ttu-id="d03c0-139">Read more about these [sizes for Linux virtual machines in Azure](../../virtual-machines/linux/sizes.md) and their [pricing information](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).</span><span class="sxs-lookup"><span data-stu-id="d03c0-139">Read more about these [sizes for Linux virtual machines in Azure](../../virtual-machines/linux/sizes.md) and their [pricing information](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).</span></span>

<span data-ttu-id="d03c0-140">Launch CLI Window from the Azure ML Workbench app by clicking on **File** --> **Open Command Prompt**, or **Open PowerShell** menu item.</span><span class="sxs-lookup"><span data-stu-id="d03c0-140">Launch CLI Window from the Azure ML Workbench app by clicking on **File** --> **Open Command Prompt**, or **Open PowerShell** menu item.</span></span> 

>[!NOTE]
><span data-ttu-id="d03c0-141">You can also do this in any command-line environment where you have az-cli installed.</span><span class="sxs-lookup"><span data-stu-id="d03c0-141">You can also do this in any command-line environment where you have az-cli installed.</span></span>

<span data-ttu-id="d03c0-142">In the command-line window, enter the below commands:</span><span class="sxs-lookup"><span data-stu-id="d03c0-142">In the command-line window, enter the below commands:</span></span>

```azurecli
# first make sure you have a valid Azure authentication token
$ az account get-access-token

# if you don't have a valid token, please log in to Azure first. 
# if you already do, you can skip this step.
$ az login

# list all subscriptions you have access to
$ az account list -o table

# make sure you set the subscription you want to use to create DSVM as the current subscription
$ az account set -s <subscription name or Id>

# it is always a good idea to create a resource group for the VM and associated resources to live in.
# you can use any Azure region, but it is best to create them in the region where your Azure ML Experimentation account is, e.g. eastus2, westcentralus or australiaeast.
# also, only certain Azure regions has GPU-equipped VMs available.
$ az group create -n <resource group name> -l <azure region>

# now let's create the DSVM based on the JSON configuration file you created earlier.
# note we assume the mydsvm.json config file is placed in the "docs" sub-folder.
$ az group deployment create -g <resource group name> --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json --parameters @docs/mydsvm.json

# find the FQDN (fully qualified domain name) of the VM just created. 
# you can also use IP address from the next command if FQDN is not set.
$ az vm show -g <resource group name> -n <vm name> --query "fqdns"

# find the IP address of the VM just created
$ az vm show -g <resource group name> -n <vm name> --query "publicIps"
```
## <a name="attach-a-dsvm-compute-target"></a><span data-ttu-id="d03c0-143">Attach a DSVM compute target</span><span class="sxs-lookup"><span data-stu-id="d03c0-143">Attach a DSVM compute target</span></span>
<span data-ttu-id="d03c0-144">Once the DSVM is created, you can now attach it to your Azure ML project.</span><span class="sxs-lookup"><span data-stu-id="d03c0-144">Once the DSVM is created, you can now attach it to your Azure ML project.</span></span>

```azurecli
# attach the DSVM compute target
# it is a good idea to use FQDN in case the IP address changes after you deallocate the VM and restart it
$ az ml computetarget attach remotedocker --name <compute target name> --address <ip address or FQDN> --username <admin username> --password <admin password> 

# prepare the Docker image on the DSVM 
$ az ml experiment prepare -c <compute target name>
```
<span data-ttu-id="d03c0-145">Now you should be ready to run experiments on this DSVM.</span><span class="sxs-lookup"><span data-stu-id="d03c0-145">Now you should be ready to run experiments on this DSVM.</span></span>

## <a name="deallocate-a-dsvm-and-restart-it-later"></a><span data-ttu-id="d03c0-146">Deallocate a DSVM and restart it later</span><span class="sxs-lookup"><span data-stu-id="d03c0-146">Deallocate a DSVM and restart it later</span></span>
<span data-ttu-id="d03c0-147">When you finish the compute tasks from Azure ML, you can deallocate the DSVM.</span><span class="sxs-lookup"><span data-stu-id="d03c0-147">When you finish the compute tasks from Azure ML, you can deallocate the DSVM.</span></span> <span data-ttu-id="d03c0-148">This action shuts down the VM, releases the compute resources, but it preserves the virtual disks.</span><span class="sxs-lookup"><span data-stu-id="d03c0-148">This action shuts down the VM, releases the compute resources, but it preserves the virtual disks.</span></span> <span data-ttu-id="d03c0-149">You are not charged for the compute cost when the VM is deallocated.</span><span class="sxs-lookup"><span data-stu-id="d03c0-149">You are not charged for the compute cost when the VM is deallocated.</span></span>

<span data-ttu-id="d03c0-150">To deallocate a VM:</span><span class="sxs-lookup"><span data-stu-id="d03c0-150">To deallocate a VM:</span></span>

```azurecli
$ az vm deallocate -g <resource group name> -n <vm name>
```

<span data-ttu-id="d03c0-151">To bring the VM back to life, use the `az ml start` command:</span><span class="sxs-lookup"><span data-stu-id="d03c0-151">To bring the VM back to life, use the `az ml start` command:</span></span>

```azurecli
$ az vm start -g <resource group name> -n <vm name>
```

## <a name="expand-the-dsvm-os-disk"></a><span data-ttu-id="d03c0-152">Expand the DSVM OS disk</span><span class="sxs-lookup"><span data-stu-id="d03c0-152">Expand the DSVM OS disk</span></span>
<span data-ttu-id="d03c0-153">The Ubuntu DSVM comes with a 50GB OS disk and 100GB data disk.</span><span class="sxs-lookup"><span data-stu-id="d03c0-153">The Ubuntu DSVM comes with a 50GB OS disk and 100GB data disk.</span></span> <span data-ttu-id="d03c0-154">Docker stores its images on the data disk, as more space is available there.</span><span class="sxs-lookup"><span data-stu-id="d03c0-154">Docker stores its images on the data disk, as more space is available there.</span></span> <span data-ttu-id="d03c0-155">When used as compute target for Azure ML, this disk can be used up by Docker engine pulling down Docker images and building conda layers on top of it.</span><span class="sxs-lookup"><span data-stu-id="d03c0-155">When used as compute target for Azure ML, this disk can be used up by Docker engine pulling down Docker images and building conda layers on top of it.</span></span> <span data-ttu-id="d03c0-156">You might need to expand the disk to a larger size (such as 200 GB) to avoid the "disk full" error while you are in the middle of an execution.</span><span class="sxs-lookup"><span data-stu-id="d03c0-156">You might need to expand the disk to a larger size (such as 200 GB) to avoid the "disk full" error while you are in the middle of an execution.</span></span> <span data-ttu-id="d03c0-157">Reference [How to expand virtual hard disks on a Linux VM with the Azure CLI](../../virtual-machines/linux/expand-disks.md) to learn how to do this easily from azure-cli.</span><span class="sxs-lookup"><span data-stu-id="d03c0-157">Reference [How to expand virtual hard disks on a Linux VM with the Azure CLI](../../virtual-machines/linux/expand-disks.md) to learn how to do this easily from azure-cli.</span></span> 

## <a name="create-an-apache-spark-for-azure-hdinsight-cluster-in-azure-portal"></a><span data-ttu-id="d03c0-158">Create an Apache Spark for Azure HDInsight cluster in Azure portal</span><span class="sxs-lookup"><span data-stu-id="d03c0-158">Create an Apache Spark for Azure HDInsight cluster in Azure portal</span></span>

<span data-ttu-id="d03c0-159">To run scale-out Spark jobs, you need to create an Apache Spark for Azure HDInsight cluster in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d03c0-159">To run scale-out Spark jobs, you need to create an Apache Spark for Azure HDInsight cluster in Azure portal.</span></span>

1. <span data-ttu-id="d03c0-160">Log on to Azure portal from https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="d03c0-160">Log on to Azure portal from https://portal.azure.com</span></span>
2. <span data-ttu-id="d03c0-161">Click on the **+NEW** link, and search for "HDInsight".</span><span class="sxs-lookup"><span data-stu-id="d03c0-161">Click on the **+NEW** link, and search for "HDInsight".</span></span>

    ![find hdi](media/how-to-create-dsvm-hdi/hdi.png)
    
3. <span data-ttu-id="d03c0-163">Choose **HDInsight** in the list, and then click on the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="d03c0-163">Choose **HDInsight** in the list, and then click on the **Create** button.</span></span>
4. <span data-ttu-id="d03c0-164">In the **Basics** configuration screen, **Cluster type** settings, make sure you choose **Spark** as the _Cluster type_, **Linux** as the _Operating system_, and **Spark 2.1.0 (HDI 3.6)** as the _Version.</span><span class="sxs-lookup"><span data-stu-id="d03c0-164">In the **Basics** configuration screen, **Cluster type** settings, make sure you choose **Spark** as the _Cluster type_, **Linux** as the _Operating system_, and **Spark 2.1.0 (HDI 3.6)** as the _Version.</span></span>

    ![configure hdi](media/how-to-create-dsvm-hdi/configure_hdi.png)

    >[!IMPORTANT]
    ><span data-ttu-id="d03c0-166">Notice in the above screen the cluster has a _Cluster login username_ field and a _Secure Shell (SSH) username_ field.</span><span class="sxs-lookup"><span data-stu-id="d03c0-166">Notice in the above screen the cluster has a _Cluster login username_ field and a _Secure Shell (SSH) username_ field.</span></span> <span data-ttu-id="d03c0-167">These are two different user identities, even though for convenience you can specify the same password for both logins.</span><span class="sxs-lookup"><span data-stu-id="d03c0-167">These are two different user identities, even though for convenience you can specify the same password for both logins.</span></span> <span data-ttu-id="d03c0-168">The _Cluster login username_ is used to log in to the management web UI of the HDI cluster.</span><span class="sxs-lookup"><span data-stu-id="d03c0-168">The _Cluster login username_ is used to log in to the management web UI of the HDI cluster.</span></span> <span data-ttu-id="d03c0-169">The _SSH login username_ is used to log in to the head node of the cluster, and this is what's needed for Azure ML to dispatch Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="d03c0-169">The _SSH login username_ is used to log in to the head node of the cluster, and this is what's needed for Azure ML to dispatch Spark jobs.</span></span>

5. <span data-ttu-id="d03c0-170">Choose the cluster size and node size you need and finish the creation wizard.</span><span class="sxs-lookup"><span data-stu-id="d03c0-170">Choose the cluster size and node size you need and finish the creation wizard.</span></span> <span data-ttu-id="d03c0-171">It can take up to 30 minutes for the cluster to finish provisioning.</span><span class="sxs-lookup"><span data-stu-id="d03c0-171">It can take up to 30 minutes for the cluster to finish provisioning.</span></span> 

## <a name="attach-an-hdi-spark-cluster-compute-target"></a><span data-ttu-id="d03c0-172">Attach an HDI Spark cluster compute target</span><span class="sxs-lookup"><span data-stu-id="d03c0-172">Attach an HDI Spark cluster compute target</span></span>

<span data-ttu-id="d03c0-173">Once the Spark HDI cluster is created, you can now attach it to your Azure ML project.</span><span class="sxs-lookup"><span data-stu-id="d03c0-173">Once the Spark HDI cluster is created, you can now attach it to your Azure ML project.</span></span>

```azurecli
# attach the HDI compute target
$ az ml computetarget attach cluster --name <compute target name> --address <cluster name, such as myhdicluster123.azurehdinsight.net> --username <ssh username> --password <ssh password> 

# prepare the conda environment on HDI
$ az ml experiment prepare -c <compute target name>
```
<span data-ttu-id="d03c0-174">Now you should be ready to run experiments on this Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="d03c0-174">Now you should be ready to run experiments on this Spark cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d03c0-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="d03c0-175">Next steps</span></span>

<span data-ttu-id="d03c0-176">Learn more about:</span><span class="sxs-lookup"><span data-stu-id="d03c0-176">Learn more about:</span></span>
- [<span data-ttu-id="d03c0-177">Overview of Azure Machine Learning experimentation service</span><span class="sxs-lookup"><span data-stu-id="d03c0-177">Overview of Azure Machine Learning experimentation service</span></span>](experimentation-service-configuration.md)
- [<span data-ttu-id="d03c0-178">Azure Machine Learning Workbench experimentation service configuration files</span><span class="sxs-lookup"><span data-stu-id="d03c0-178">Azure Machine Learning Workbench experimentation service configuration files</span></span>](experimentation-service-configuration-reference.md)
- [<span data-ttu-id="d03c0-179">Apache Spark for Azure HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="d03c0-179">Apache Spark for Azure HDInsight cluster</span></span>](https://azure.microsoft.com/services/hdinsight/apache-spark/)
- [<span data-ttu-id="d03c0-180">Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="d03c0-180">Data Science Virtual Machine</span></span>](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)
