---
title: Azure Quickstart - Create Batch AI cluster - Portal | Microsoft Docs
description: Quickstart - Create a Batch AI cluster for training machine learning and AI models - Azure portal
services: batch-ai
documentationcenter: na
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.custom: ''
ms.service: batch-ai
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/15/2018
ms.author: danlep
ms.openlocfilehash: 8b9daa0fbbf84e0f602498a0847c9e120f709b17
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856953"
---
# <a name="quickstart-create-a-cluster-for-batch-ai-training-jobs-using-the-azure-portal"></a><span data-ttu-id="7ff4e-103">Quickstart: Create a cluster for Batch AI training jobs using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7ff4e-103">Quickstart: Create a cluster for Batch AI training jobs using the Azure portal</span></span>

<span data-ttu-id="7ff4e-104">This quickstart shows how to use the Azure portal to create a Batch AI cluster you can use for training AI and machine learning models.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-104">This quickstart shows how to use the Azure portal to create a Batch AI cluster you can use for training AI and machine learning models.</span></span> <span data-ttu-id="7ff4e-105">Batch AI is a managed service for data scientists and AI researchers to train AI and machine learning models at scale on clusters of Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-105">Batch AI is a managed service for data scientists and AI researchers to train AI and machine learning models at scale on clusters of Azure virtual machines.</span></span>

<span data-ttu-id="7ff4e-106">The cluster initially has a single GPU node and an attached file server.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-106">The cluster initially has a single GPU node and an attached file server.</span></span> <span data-ttu-id="7ff4e-107">After completing this quickstart, you'll have a cluster you can scale up and use to train deep learning models.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-107">After completing this quickstart, you'll have a cluster you can scale up and use to train deep learning models.</span></span> <span data-ttu-id="7ff4e-108">Submit training jobs to the cluster using Batch AI, [Azure Machine Learning](../machine-learning/service/overview-what-is-azure-ml.md) tools, or the [Visual Studio Tools for AI](https://github.com/Microsoft/vs-tools-for-ai).</span><span class="sxs-lookup"><span data-stu-id="7ff4e-108">Submit training jobs to the cluster using Batch AI, [Azure Machine Learning](../machine-learning/service/overview-what-is-azure-ml.md) tools, or the [Visual Studio Tools for AI](https://github.com/Microsoft/vs-tools-for-ai).</span></span>

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-ssh-key-pair"></a><span data-ttu-id="7ff4e-109">Create SSH key pair</span><span class="sxs-lookup"><span data-stu-id="7ff4e-109">Create SSH key pair</span></span>

<span data-ttu-id="7ff4e-110">You need an SSH key pair to complete this quickstart.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-110">You need an SSH key pair to complete this quickstart.</span></span> <span data-ttu-id="7ff4e-111">If you have an existing SSH key pair, this step can be skipped.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-111">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="7ff4e-112">To create an SSH key pair, run the following command from a Bash shell and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-112">To create an SSH key pair, run the following command from a Bash shell and follow the on-screen directions.</span></span> <span data-ttu-id="7ff4e-113">For example, you can use the [Azure Cloud Shell](../cloud-shell/overview.md) or, on Windows, the [Windows Subsystem for Linux](/windows/wsl/install-win10).</span><span class="sxs-lookup"><span data-stu-id="7ff4e-113">For example, you can use the [Azure Cloud Shell](../cloud-shell/overview.md) or, on Windows, the [Windows Subsystem for Linux](/windows/wsl/install-win10).</span></span> <span data-ttu-id="7ff4e-114">The command output includes the file name of the public key file.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-114">The command output includes the file name of the public key file.</span></span> <span data-ttu-id="7ff4e-115">Copy the contents of the public key file (`cat ~/.ssh/id_rsa.pub`) to the clipboard or another location you can access in a later step.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-115">Copy the contents of the public key file (`cat ~/.ssh/id_rsa.pub`) to the clipboard or another location you can access in a later step.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

<span data-ttu-id="7ff4e-116">For more detailed information on how to create SSH key pairs, see [Create and use an SSH public-private key pair for Linux VMs in Azure](../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="7ff4e-116">For more detailed information on how to create SSH key pairs, see [Create and use an SSH public-private key pair for Linux VMs in Azure](../virtual-machines/linux/mac-create-ssh-keys.md).</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="7ff4e-117">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="7ff4e-117">Sign in to Azure</span></span>

<span data-ttu-id="7ff4e-118">Sign in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-118">Sign in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="create-a-batch-ai-workspace"></a><span data-ttu-id="7ff4e-119">Create a Batch AI workspace</span><span class="sxs-lookup"><span data-stu-id="7ff4e-119">Create a Batch AI workspace</span></span>

<span data-ttu-id="7ff4e-120">Start by creating a Batch AI workspace to organize your Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-120">Start by creating a Batch AI workspace to organize your Batch AI resources.</span></span> <span data-ttu-id="7ff4e-121">A workspace can contain one or more clusters or other Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-121">A workspace can contain one or more clusters or other Batch AI resources.</span></span>

1. <span data-ttu-id="7ff4e-122">Select **All services** and filter for **Batch AI**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-122">Select **All services** and filter for **Batch AI**.</span></span>

2. <span data-ttu-id="7ff4e-123">Select **Add Workspace**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-123">Select **Add Workspace**.</span></span>

3. <span data-ttu-id="7ff4e-124">Enter values for **Workspace name** and **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-124">Enter values for **Workspace name** and **Resource group**.</span></span> <span data-ttu-id="7ff4e-125">If you want to, select different options for the **Subscription** and **Location** for the workspace.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-125">If you want to, select different options for the **Subscription** and **Location** for the workspace.</span></span> <span data-ttu-id="7ff4e-126">Select **Create Workspace**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-126">Select **Create Workspace**.</span></span>

  ![Create Batch AI workspace](./media/quickstart-create-cluster-portal/create-workspace.png)

<span data-ttu-id="7ff4e-128">When the **Deployment succeeded** message appears, go the resource you created and select the workspace.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-128">When the **Deployment succeeded** message appears, go the resource you created and select the workspace.</span></span>

## <a name="create-a-file-server"></a><span data-ttu-id="7ff4e-129">Create a file server</span><span class="sxs-lookup"><span data-stu-id="7ff4e-129">Create a file server</span></span>

<span data-ttu-id="7ff4e-130">A Batch AI file server is a single-node NFS, which can be automatically mounted on cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-130">A Batch AI file server is a single-node NFS, which can be automatically mounted on cluster nodes.</span></span> <span data-ttu-id="7ff4e-131">It is one of several ways you can provide storage for input data and output from your training jobs.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-131">It is one of several ways you can provide storage for input data and output from your training jobs.</span></span>

1. <span data-ttu-id="7ff4e-132">In the workspace, select **File server** > **Add batch ai file server**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-132">In the workspace, select **File server** > **Add batch ai file server**.</span></span>

2. <span data-ttu-id="7ff4e-133">Enter values for **File server name** and **VM size**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-133">Enter values for **File server name** and **VM size**.</span></span> <span data-ttu-id="7ff4e-134">For this quickstart, a VM size of *Standard D1_v2* is suggested for the file server.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-134">For this quickstart, a VM size of *Standard D1_v2* is suggested for the file server.</span></span> <span data-ttu-id="7ff4e-135">Choose a different size if you need to store larger amounts of input or output data for training jobs.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-135">Choose a different size if you need to store larger amounts of input or output data for training jobs.</span></span>

3. <span data-ttu-id="7ff4e-136">Enter an **Admin username** and copy the contents of your SSH public key file to **SSH key**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-136">Enter an **Admin username** and copy the contents of your SSH public key file to **SSH key**.</span></span> <span data-ttu-id="7ff4e-137">Accept defaults for the remaining values and select **Create File server**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-137">Accept defaults for the remaining values and select **Create File server**.</span></span>

  ![Create Batch AI file server](./media/quickstart-create-cluster-portal/create-file-server.png)

<span data-ttu-id="7ff4e-139">It takes a few minutes to deploy the file server.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-139">It takes a few minutes to deploy the file server.</span></span>

<span data-ttu-id="7ff4e-140">After the server is created, click **Properties** and take note of the **Mount settings**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-140">After the server is created, click **Properties** and take note of the **Mount settings**.</span></span> <span data-ttu-id="7ff4e-141">You can SSH to the public IP address of the server to upload and download training data and output files at the indicated directory (*/data*).</span><span class="sxs-lookup"><span data-stu-id="7ff4e-141">You can SSH to the public IP address of the server to upload and download training data and output files at the indicated directory (*/data*).</span></span>

![File server properties](./media/quickstart-create-cluster-portal/file-server-properties.png)

## <a name="create-a-cluster"></a><span data-ttu-id="7ff4e-143">Create a cluster</span><span class="sxs-lookup"><span data-stu-id="7ff4e-143">Create a cluster</span></span>

<span data-ttu-id="7ff4e-144">The following steps create a cluster with a single GPU node.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-144">The following steps create a cluster with a single GPU node.</span></span> <span data-ttu-id="7ff4e-145">The cluster node runs a default Ubuntu Server image designed to host container-based applications, which you can use for most training workloads.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-145">The cluster node runs a default Ubuntu Server image designed to host container-based applications, which you can use for most training workloads.</span></span> <span data-ttu-id="7ff4e-146">The cluster node mounts the file server at its mount point.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-146">The cluster node mounts the file server at its mount point.</span></span> 

1. <span data-ttu-id="7ff4e-147">In your Batch AI workspace, select **Cluster** > **Add batch ai cluster**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-147">In your Batch AI workspace, select **Cluster** > **Add batch ai cluster**.</span></span>

2. <span data-ttu-id="7ff4e-148">Enter values for **Cluster name** and the following settings.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-148">Enter values for **Cluster name** and the following settings.</span></span> <span data-ttu-id="7ff4e-149">The suggested VM size has one NVIDIA Tesla K80 GPU.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-149">The suggested VM size has one NVIDIA Tesla K80 GPU.</span></span>
  
   |<span data-ttu-id="7ff4e-150">Setting</span><span class="sxs-lookup"><span data-stu-id="7ff4e-150">Setting</span></span>  |<span data-ttu-id="7ff4e-151">Value</span><span class="sxs-lookup"><span data-stu-id="7ff4e-151">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="7ff4e-152">**VM size**</span><span class="sxs-lookup"><span data-stu-id="7ff4e-152">**VM size**</span></span>     |<span data-ttu-id="7ff4e-153">Standard NC6</span><span class="sxs-lookup"><span data-stu-id="7ff4e-153">Standard NC6</span></span>|
   |<span data-ttu-id="7ff4e-154">**Target number of nodes**</span><span class="sxs-lookup"><span data-stu-id="7ff4e-154">**Target number of nodes**</span></span>     |<span data-ttu-id="7ff4e-155">1</span><span class="sxs-lookup"><span data-stu-id="7ff4e-155">1</span></span>|

3. <span data-ttu-id="7ff4e-156">Enter an **Admin username** and copy the contents of your SSH public key file to **SSH key**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-156">Enter an **Admin username** and copy the contents of your SSH public key file to **SSH key**.</span></span> <span data-ttu-id="7ff4e-157">Accept defaults for the remaining values on this page, and select **Next: Node setup**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-157">Accept defaults for the remaining values on this page, and select **Next: Node setup**.</span></span>

   ![Enter basic cluster information](./media/quickstart-create-cluster-portal/create-cluster.png)

4. <span data-ttu-id="7ff4e-159">Under **Mount Volumes**, select **File server references** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-159">Under **Mount Volumes**, select **File server references** > **Add**.</span></span> <span data-ttu-id="7ff4e-160">Select the file server you created previously.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-160">Select the file server you created previously.</span></span> <span data-ttu-id="7ff4e-161">Enter a **Relative mount path** where the file server is mounted on each cluster node.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-161">Enter a **Relative mount path** where the file server is mounted on each cluster node.</span></span> <span data-ttu-id="7ff4e-162">Select **Save and continue**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-162">Select **Save and continue**.</span></span>

   ![Add file server reference](./media/quickstart-create-cluster-portal/file-server-reference.png)

<span data-ttu-id="7ff4e-164">Save the node setup and select **Create Cluster**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-164">Save the node setup and select **Create Cluster**.</span></span>

<span data-ttu-id="7ff4e-165">Batch AI takes a few minutes to allocate the node.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-165">Batch AI takes a few minutes to allocate the node.</span></span> <span data-ttu-id="7ff4e-166">During this time, the cluster's **Allocation state** is **Resizing**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-166">During this time, the cluster's **Allocation state** is **Resizing**.</span></span> <span data-ttu-id="7ff4e-167">After a few minutes, the state of the cluster is **Steady**, and the node starts.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-167">After a few minutes, the state of the cluster is **Steady**, and the node starts.</span></span>

![Cluster starting](./media/quickstart-create-cluster-portal/cluster-resizing.png)

<span data-ttu-id="7ff4e-169">Select the cluster name to check the state of the node.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-169">Select the cluster name to check the state of the node.</span></span> <span data-ttu-id="7ff4e-170">When a node's state is **Idle**, it is ready to run training jobs.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-170">When a node's state is **Idle**, it is ready to run training jobs.</span></span>

### <a name="list-cluster-nodes"></a><span data-ttu-id="7ff4e-171">List cluster nodes</span><span class="sxs-lookup"><span data-stu-id="7ff4e-171">List cluster nodes</span></span>

<span data-ttu-id="7ff4e-172">If you need to connect to the cluster nodes (in this case, a single node) to install applications or perform maintenance, get connection information in the portal.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-172">If you need to connect to the cluster nodes (in this case, a single node) to install applications or perform maintenance, get connection information in the portal.</span></span> <span data-ttu-id="7ff4e-173">After the cluster is created, click **Nodes** and take note of the SSH **Connection** settings (IP address and port number).</span><span class="sxs-lookup"><span data-stu-id="7ff4e-173">After the cluster is created, click **Nodes** and take note of the SSH **Connection** settings (IP address and port number).</span></span>

![Cluster nodes](./media/quickstart-create-cluster-portal/cluster-nodes.png)

<span data-ttu-id="7ff4e-175">Use this information to make an SSH connection to the node.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-175">Use this information to make an SSH connection to the node.</span></span> <span data-ttu-id="7ff4e-176">For example, substitute the correct IP address and port number of your node in the following command:</span><span class="sxs-lookup"><span data-stu-id="7ff4e-176">For example, substitute the correct IP address and port number of your node in the following command:</span></span>

```bash
ssh myusername@137.135.82.15 -p 50000
``` 

### <a name="resize-the-cluster"></a><span data-ttu-id="7ff4e-177">Resize the cluster</span><span class="sxs-lookup"><span data-stu-id="7ff4e-177">Resize the cluster</span></span>

<span data-ttu-id="7ff4e-178">When you use your cluster to train a model, you might need more compute resources.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-178">When you use your cluster to train a model, you might need more compute resources.</span></span> <span data-ttu-id="7ff4e-179">For example, to increase the size to 2 nodes for a distributed training job, select **Scale** and set the **Target number of node** to 2.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-179">For example, to increase the size to 2 nodes for a distributed training job, select **Scale** and set the **Target number of node** to 2.</span></span> <span data-ttu-id="7ff4e-180">Save the configuration.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-180">Save the configuration.</span></span>

![Scale cluster](./media/quickstart-create-cluster-portal/scale-cluster.png)

<span data-ttu-id="7ff4e-182">It takes a few minutes for the cluster to resize.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-182">It takes a few minutes for the cluster to resize.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7ff4e-183">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7ff4e-183">Clean up resources</span></span>

<span data-ttu-id="7ff4e-184">If you want to continue with Batch AI tutorials and samples, use the Batch AI workspace, file server, and cluster created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-184">If you want to continue with Batch AI tutorials and samples, use the Batch AI workspace, file server, and cluster created in this quickstart.</span></span>

<span data-ttu-id="7ff4e-185">You're charged for the Batch AI cluster and file server while the underlying virtual machines are running, even if no jobs are scheduled.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-185">You're charged for the Batch AI cluster and file server while the underlying virtual machines are running, even if no jobs are scheduled.</span></span> <span data-ttu-id="7ff4e-186">If you want to maintain the cluster configuration when you have no jobs to run, resize the cluster to 0 nodes.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-186">If you want to maintain the cluster configuration when you have no jobs to run, resize the cluster to 0 nodes.</span></span> <span data-ttu-id="7ff4e-187">Later, resize it to 1 or more nodes to run your jobs.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-187">Later, resize it to 1 or more nodes to run your jobs.</span></span> 

<span data-ttu-id="7ff4e-188">When no longer needed, delete the Batch AI workspace containing the cluster and file server.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-188">When no longer needed, delete the Batch AI workspace containing the cluster and file server.</span></span> <span data-ttu-id="7ff4e-189">To do so, select the Batch AI workspace and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-189">To do so, select the Batch AI workspace and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ff4e-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ff4e-190">Next steps</span></span>

<span data-ttu-id="7ff4e-191">In this quickstart, you learned how to create a Batch AI cluster and an attached file server, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-191">In this quickstart, you learned how to create a Batch AI cluster and an attached file server, using the Azure portal.</span></span> <span data-ttu-id="7ff4e-192">To learn about how to use a Batch AI cluster to train a model, continue to the quickstart for training a deep learning model.</span><span class="sxs-lookup"><span data-stu-id="7ff4e-192">To learn about how to use a Batch AI cluster to train a model, continue to the quickstart for training a deep learning model.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ff4e-193">Train a deep learning model</span><span class="sxs-lookup"><span data-stu-id="7ff4e-193">Train a deep learning model</span></span>](./quickstart-tensorflow-training-cli.md)
