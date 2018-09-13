---
title: File share for Azure DC/OS cluster | Microsoft Docs
description: Create and mount a file share to a DC/OS cluster in Azure Container Service
services: container-service
documentationcenter: ''
author: julienstroheker
manager: dcaro
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, FileShare, cifs
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: juliens
ms.openlocfilehash: 62b97002697a014e37dacfcad6425642f14d2246
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554045"
---
# <a name="create-and-mount-a-file-share-to-a-dcos-cluster"></a><span data-ttu-id="815a1-104">Create and mount a file share to a DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="815a1-104">Create and mount a file share to a DC/OS cluster</span></span>
<span data-ttu-id="815a1-105">In this article, we'll explore how to create a file share on Azure and mount it on each agent and master of the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="815a1-105">In this article, we'll explore how to create a file share on Azure and mount it on each agent and master of the DC/OS cluster.</span></span> <span data-ttu-id="815a1-106">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span><span class="sxs-lookup"><span data-stu-id="815a1-106">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span></span>

<span data-ttu-id="815a1-107">Before working through this example, you need a DC/OS cluster that is configured in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="815a1-107">Before working through this example, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="815a1-108">See [Deploy an Azure Container Service cluster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="815a1-108">See [Deploy an Azure Container Service cluster](container-service-deployment.md).</span></span>

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="815a1-109">Create a file share on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="815a1-109">Create a file share on Microsoft Azure</span></span>
### <a name="using-the-portal"></a><span data-ttu-id="815a1-110">Using the portal</span><span class="sxs-lookup"><span data-stu-id="815a1-110">Using the portal</span></span>

1. <span data-ttu-id="815a1-111">Log in to the portal.</span><span class="sxs-lookup"><span data-stu-id="815a1-111">Log in to the portal.</span></span>
2. <span data-ttu-id="815a1-112">Create a storage account.</span><span class="sxs-lookup"><span data-stu-id="815a1-112">Create a storage account.</span></span>
   
  ![Azure container service create Storage Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-dcos-fileshare/createSA.png)

3. <span data-ttu-id="815a1-114">When it's created, click **Files** in the **Services** section.</span><span class="sxs-lookup"><span data-stu-id="815a1-114">When it's created, click **Files** in the **Services** section.</span></span>
   
  ![Azure container service Files section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-dcos-fileshare/filesServices.png)

4. <span data-ttu-id="815a1-116">Click **+ File share** and enter a name for this new share (**Quota** is not mandatory).</span><span class="sxs-lookup"><span data-stu-id="815a1-116">Click **+ File share** and enter a name for this new share (**Quota** is not mandatory).</span></span>
   
  ![Azure container service + File Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-dcos-fileshare/newFileShare.png)  

### <a name="using-azure-cli-20"></a><span data-ttu-id="815a1-118">Using Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="815a1-118">Using Azure CLI 2.0</span></span>

<span data-ttu-id="815a1-119">If you need to, [install and set up the Azure CLI](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="815a1-119">If you need to, [install and set up the Azure CLI](/cli/azure/install-azure-cli.md).</span></span>

```azurecli
################# Change these four parameters ##############
DCOS_PERS_STORAGE_ACCOUNT_NAME=anystorageaccountname
DCOS_PERS_RESOURCE_GROUP=AnyResourceGroupName
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=demoshare
#############################################################

# Create the storage account with the parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-the-share-in-your-cluster"></a><span data-ttu-id="815a1-120">Mount the share in your cluster</span><span class="sxs-lookup"><span data-stu-id="815a1-120">Mount the share in your cluster</span></span>

<span data-ttu-id="815a1-121">Next, we need to mount this share on every virtual machine inside your cluster using the cifs tool/protocol.</span><span class="sxs-lookup"><span data-stu-id="815a1-121">Next, we need to mount this share on every virtual machine inside your cluster using the cifs tool/protocol.</span></span> <span data-ttu-id="815a1-122">We do that with the following command line: `mount -t cifs`.</span><span class="sxs-lookup"><span data-stu-id="815a1-122">We do that with the following command line: `mount -t cifs`.</span></span>

<span data-ttu-id="815a1-123">Here is an example that uses:</span><span class="sxs-lookup"><span data-stu-id="815a1-123">Here is an example that uses:</span></span>
* <span data-ttu-id="815a1-124">Storage account name **`anystorageaccountname`**</span><span class="sxs-lookup"><span data-stu-id="815a1-124">Storage account name **`anystorageaccountname`**</span></span>
* <span data-ttu-id="815a1-125">The fictitious account key **`P/GuXXXuoRtIVsV+faSfLhuNyZDrTzPmZDm3RyCL4XS6ghyiHYriN12gl+w5JMN2gXGtOhCzxFf2JuGqXXXX1w==`**</span><span class="sxs-lookup"><span data-stu-id="815a1-125">The fictitious account key **`P/GuXXXuoRtIVsV+faSfLhuNyZDrTzPmZDm3RyCL4XS6ghyiHYriN12gl+w5JMN2gXGtOhCzxFf2JuGqXXXX1w==`**</span></span> 
* <span data-ttu-id="815a1-126">The mount point **`/mnt/share/demoshare`**</span><span class="sxs-lookup"><span data-stu-id="815a1-126">The mount point **`/mnt/share/demoshare`**</span></span>

```bash
sudo mount -t cifs //anystorageaccountname.file.core.windows.net/demoshare /mnt/share/demoshare -o vers=3.0,username=anystorageaccountname,password=P/GuXXXuoRtIVsV+faSfLhuNyZDrTzPmZDm3RyCL4XS6ghyiHYriN12gl+w5JMN2gXGtOhCzxFf2JuGqXXXX1w==,dir_mode=0777,file_mode=0777
```

<span data-ttu-id="815a1-127">We will run this command on each virtual machine of our cluster (master and agent nodes).</span><span class="sxs-lookup"><span data-stu-id="815a1-127">We will run this command on each virtual machine of our cluster (master and agent nodes).</span></span> <span data-ttu-id="815a1-128">If you have a large number of agents, we recommend automating this process by creating scripts.</span><span class="sxs-lookup"><span data-stu-id="815a1-128">If you have a large number of agents, we recommend automating this process by creating scripts.</span></span>  

### <a name="set-up-scripts"></a><span data-ttu-id="815a1-129">Set up scripts</span><span class="sxs-lookup"><span data-stu-id="815a1-129">Set up scripts</span></span>

1. <span data-ttu-id="815a1-130">First, SSH to the master (or the first master) of your DC/OS-based cluster.</span><span class="sxs-lookup"><span data-stu-id="815a1-130">First, SSH to the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="815a1-131">For example, `ssh userName@masterFQDN –A –p 22`, where the masterFQDN is the fully qualified domain name of the master VM.</span><span class="sxs-lookup"><span data-stu-id="815a1-131">For example, `ssh userName@masterFQDN –A –p 22`, where the masterFQDN is the fully qualified domain name of the master VM.</span></span>

2. <span data-ttu-id="815a1-132">Copy your private key to the working directory (~) on master.</span><span class="sxs-lookup"><span data-stu-id="815a1-132">Copy your private key to the working directory (~) on master.</span></span>

3. <span data-ttu-id="815a1-133">Change the permissions on it with the following command: `chmod 600 yourPrivateKeyFile`.</span><span class="sxs-lookup"><span data-stu-id="815a1-133">Change the permissions on it with the following command: `chmod 600 yourPrivateKeyFile`.</span></span>

4. <span data-ttu-id="815a1-134">Import your private key using the `ssh-add yourPrivateKeyFile` command.</span><span class="sxs-lookup"><span data-stu-id="815a1-134">Import your private key using the `ssh-add yourPrivateKeyFile` command.</span></span> <span data-ttu-id="815a1-135">You may have to run `eval ssh-agent -s` if it doesn't work the first time.</span><span class="sxs-lookup"><span data-stu-id="815a1-135">You may have to run `eval ssh-agent -s` if it doesn't work the first time.</span></span>

5. <span data-ttu-id="815a1-136">From the master, create two files, using your favorite editor such as vi, nano, or vim:</span><span class="sxs-lookup"><span data-stu-id="815a1-136">From the master, create two files, using your favorite editor such as vi, nano, or vim:</span></span> 
  
  * <span data-ttu-id="815a1-137">One with the script to execute on each VM, called **cifsMount.sh**</span><span class="sxs-lookup"><span data-stu-id="815a1-137">One with the script to execute on each VM, called **cifsMount.sh**</span></span> 
  * <span data-ttu-id="815a1-138">Another one to initiate all the ssh connections that will call the first script, called **mountShares.sh**</span><span class="sxs-lookup"><span data-stu-id="815a1-138">Another one to initiate all the ssh connections that will call the first script, called **mountShares.sh**</span></span>


```bash
# cifsMount.sh

# Install the cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create the local folder that will contain our share
if [ ! -d "/mnt/share/demoshare" ]; then sudo mkdir -p "/mnt/share/demoshare" ; fi

# Mount the share under the previous local folder created
sudo mount -t cifs //anystorageaccountname.file.core.windows.net/demoshare /mnt/share/demoshare -o vers=3.0,username=anystorageaccountname,password=P/GuXXXuoRtIVsV+faSfLhuNyZDrTzPmZDm3RyCL4XS6ghyiHYriN12gl+w5JMN2gXGtOhCzxFf2JuGqXXXX1w==,dir_mode=0777,file_mode=0777
```
  
```bash
# mountShares.sh

# Install jq used for the next command
sudo apt-get install jq

# Create the local folder that will contain our share
if [ ! -d "/mnt/share/demoshare" ]; then sudo mkdir -p "/mnt/share/demoshare" ; fi

# Mount the share on the current vm (master)
sudo mount -t cifs //anystorageaccountname.file.core.windows.net/demoshare /mnt/share/demoshare -o vers=3.0,username=anystorageaccountname,password=P/GuXXXuoRtIVsV+faSfLhuNyZDrTzPmZDm3RyCL4XS6ghyiHYriN12gl+w5JMN2gXGtOhCzxFf2JuGqXXXX1w==,dir_mode=0777,file_mode=0777

# Get the IP address of each node using the mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes
  
# From the previous file created, run our script to mount our share on each node
cat nodes | while read line
  do
    ssh `whoami`@$line -o StrictHostKeyChecking=no -i yourPrivateKeyFile < ./cifsMount.sh
    done
```  
> [!IMPORTANT]
> <span data-ttu-id="815a1-139">You have to change the **'mount'** command with your own settings such as the name of your storage account and the password.</span><span class="sxs-lookup"><span data-stu-id="815a1-139">You have to change the **'mount'** command with your own settings such as the name of your storage account and the password.</span></span>
>  

<span data-ttu-id="815a1-140">The folder where you created the previous scripts should now have 3 files:</span><span class="sxs-lookup"><span data-stu-id="815a1-140">The folder where you created the previous scripts should now have 3 files:</span></span>  

* <span data-ttu-id="815a1-141">**cifsMount.sh**</span><span class="sxs-lookup"><span data-stu-id="815a1-141">**cifsMount.sh**</span></span>
* <span data-ttu-id="815a1-142">**mountShares.sh**</span><span class="sxs-lookup"><span data-stu-id="815a1-142">**mountShares.sh**</span></span>
* <span data-ttu-id="815a1-143">**yourPrivateKeyFile**</span><span class="sxs-lookup"><span data-stu-id="815a1-143">**yourPrivateKeyFile**</span></span> 

### <a name="run-the-scripts"></a><span data-ttu-id="815a1-144">Run the scripts</span><span class="sxs-lookup"><span data-stu-id="815a1-144">Run the scripts</span></span>

<span data-ttu-id="815a1-145">Execute the **mountShares.sh** file with the following command: `sh mountShares.sh`.</span><span class="sxs-lookup"><span data-stu-id="815a1-145">Execute the **mountShares.sh** file with the following command: `sh mountShares.sh`.</span></span>

<span data-ttu-id="815a1-146">You should see the result printing in the terminal.</span><span class="sxs-lookup"><span data-stu-id="815a1-146">You should see the result printing in the terminal.</span></span> <span data-ttu-id="815a1-147">After the scripts complete, you can use the file share in your cluster.</span><span class="sxs-lookup"><span data-stu-id="815a1-147">After the scripts complete, you can use the file share in your cluster.</span></span>

<span data-ttu-id="815a1-148">You can optimize the scripts, but this example is straightforward and its purpose is to provide guidance.</span><span class="sxs-lookup"><span data-stu-id="815a1-148">You can optimize the scripts, but this example is straightforward and its purpose is to provide guidance.</span></span>

> [!NOTE] 
> <span data-ttu-id="815a1-149">This method is not recommended for scenarios that require high IOPS, but it is very useful to share documents and information across the cluster.</span><span class="sxs-lookup"><span data-stu-id="815a1-149">This method is not recommended for scenarios that require high IOPS, but it is very useful to share documents and information across the cluster.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="815a1-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="815a1-150">Next steps</span></span>
* <span data-ttu-id="815a1-151">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="815a1-151">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>
* <span data-ttu-id="815a1-152">DC/OS container management through the [Marathon REST API](container-service-mesos-marathon-rest.md).</span><span class="sxs-lookup"><span data-stu-id="815a1-152">DC/OS container management through the [Marathon REST API](container-service-mesos-marathon-rest.md).</span></span>


