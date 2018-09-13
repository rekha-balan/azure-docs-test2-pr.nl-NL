---
title: Connect to an Azure Container Service cluster | Microsoft Docs
description: Connect to a Kubernetes, DC/OS, or Docker Swarm cluster in Azure Container Service from a remote computer
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: ff8d9e32-20d2-4658-829f-590dec89603d
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e4e3cff725cde2ca0b9f4e28a7604a2bf30a07d4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662499"
---
# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="276a9-104">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span><span class="sxs-lookup"><span data-stu-id="276a9-104">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="276a9-105">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span><span class="sxs-lookup"><span data-stu-id="276a9-105">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="276a9-106">This article describes how to connect to the master VM of the cluster from a remote computer.</span><span class="sxs-lookup"><span data-stu-id="276a9-106">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="276a9-107">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span><span class="sxs-lookup"><span data-stu-id="276a9-107">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="276a9-108">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span><span class="sxs-lookup"><span data-stu-id="276a9-108">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="276a9-109">For DC/OS and Docker Swarm, you must create a secure shell (SSH) tunnel to an internal system.</span><span class="sxs-lookup"><span data-stu-id="276a9-109">For DC/OS and Docker Swarm, you must create a secure shell (SSH) tunnel to an internal system.</span></span> <span data-ttu-id="276a9-110">After the tunnel is established, you can run commands which use the HTTP endpoints and view the cluster's web interface from your local system.</span><span class="sxs-lookup"><span data-stu-id="276a9-110">After the tunnel is established, you can run commands which use the HTTP endpoints and view the cluster's web interface from your local system.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="276a9-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="276a9-111">Prerequisites</span></span>

* <span data-ttu-id="276a9-112">A Kubernetes, DC/OS, or Swarm cluster [deployed in Azure Container Service](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="276a9-112">A Kubernetes, DC/OS, or Swarm cluster [deployed in Azure Container Service](container-service-deployment.md).</span></span>
* <span data-ttu-id="276a9-113">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span><span class="sxs-lookup"><span data-stu-id="276a9-113">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="276a9-114">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span><span class="sxs-lookup"><span data-stu-id="276a9-114">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="276a9-115">See these instructions for [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="276a9-115">See these instructions for [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="276a9-116">If the SSH connection isn't working, you may need to [reset your SSH keys](../virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="276a9-116">If the SSH connection isn't working, you may need to [reset your SSH keys](../virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="276a9-117">Connect to a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="276a9-117">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="276a9-118">Follow these steps to install and configure `kubectl` on your computer.</span><span class="sxs-lookup"><span data-stu-id="276a9-118">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="276a9-119">On Linux or OS X, you might need to run the commands in this section using `sudo`.</span><span class="sxs-lookup"><span data-stu-id="276a9-119">On Linux or OS X, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="276a9-120">Install kubectl</span><span class="sxs-lookup"><span data-stu-id="276a9-120">Install kubectl</span></span>
<span data-ttu-id="276a9-121">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span><span class="sxs-lookup"><span data-stu-id="276a9-121">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="276a9-122">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span><span class="sxs-lookup"><span data-stu-id="276a9-122">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or OS X
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="276a9-123">Alternatively, you can download the latest client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="276a9-123">Alternatively, you can download the latest client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="276a9-124">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/).</span><span class="sxs-lookup"><span data-stu-id="276a9-124">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="276a9-125">Download cluster credentials</span><span class="sxs-lookup"><span data-stu-id="276a9-125">Download cluster credentials</span></span>
<span data-ttu-id="276a9-126">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span><span class="sxs-lookup"><span data-stu-id="276a9-126">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="276a9-127">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span><span class="sxs-lookup"><span data-stu-id="276a9-127">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="276a9-128">Pass the name of the resource group and the name of the container service resource:</span><span class="sxs-lookup"><span data-stu-id="276a9-128">Pass the name of the resource group and the name of the container service resource:</span></span>


```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="276a9-129">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span><span class="sxs-lookup"><span data-stu-id="276a9-129">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="276a9-130">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span><span class="sxs-lookup"><span data-stu-id="276a9-130">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="276a9-131">For example:</span><span class="sxs-lookup"><span data-stu-id="276a9-131">For example:</span></span>

```console
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="276a9-132">If you are on Windows, you need to use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span><span class="sxs-lookup"><span data-stu-id="276a9-132">If you are on Windows, you need to use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>



### <a name="use-kubectl"></a><span data-ttu-id="276a9-133">Use kubectl</span><span class="sxs-lookup"><span data-stu-id="276a9-133">Use kubectl</span></span>

<span data-ttu-id="276a9-134">Once you have `kubectl` configured, you can test the connection by listing the nodes in your cluster:</span><span class="sxs-lookup"><span data-stu-id="276a9-134">Once you have `kubectl` configured, you can test the connection by listing the nodes in your cluster:</span></span>

```console
kubectl get nodes
```

<span data-ttu-id="276a9-135">You can try other `kubectl` commands.</span><span class="sxs-lookup"><span data-stu-id="276a9-135">You can try other `kubectl` commands.</span></span> <span data-ttu-id="276a9-136">For example, you can view the Kubernetes Dashboard.</span><span class="sxs-lookup"><span data-stu-id="276a9-136">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="276a9-137">First, run a proxy to the Kubernetes API server:</span><span class="sxs-lookup"><span data-stu-id="276a9-137">First, run a proxy to the Kubernetes API server:</span></span>

```console
kubectl proxy
```

<span data-ttu-id="276a9-138">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="276a9-138">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="276a9-139">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="276a9-139">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="276a9-140">Connect to a DC/OS or Swarm cluster</span><span class="sxs-lookup"><span data-stu-id="276a9-140">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="276a9-141">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a secure shell (SSH) tunnel from your local Linux, OS X, or Windows system.</span><span class="sxs-lookup"><span data-stu-id="276a9-141">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a secure shell (SSH) tunnel from your local Linux, OS X, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="276a9-142">These instructions focus on tunnelling TCP traffic over SSH.</span><span class="sxs-lookup"><span data-stu-id="276a9-142">These instructions focus on tunnelling TCP traffic over SSH.</span></span> <span data-ttu-id="276a9-143">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span><span class="sxs-lookup"><span data-stu-id="276a9-143">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="276a9-144">Working directly on an internal system risks inadvertent configuration changes.</span><span class="sxs-lookup"><span data-stu-id="276a9-144">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-os-x"></a><span data-ttu-id="276a9-145">Create an SSH tunnel on Linux or OS X</span><span class="sxs-lookup"><span data-stu-id="276a9-145">Create an SSH tunnel on Linux or OS X</span></span>
<span data-ttu-id="276a9-146">The first thing that you do when you create an SSH tunnel on Linux or OS X is to locate the public DNS name of load-balanced masters.</span><span class="sxs-lookup"><span data-stu-id="276a9-146">The first thing that you do when you create an SSH tunnel on Linux or OS X is to locate the public DNS name of load-balanced masters.</span></span> <span data-ttu-id="276a9-147">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="276a9-147">Follow these steps:</span></span>


1. <span data-ttu-id="276a9-148">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span><span class="sxs-lookup"><span data-stu-id="276a9-148">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="276a9-149">Expand the resource group so that each resource is displayed.</span><span class="sxs-lookup"><span data-stu-id="276a9-149">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="276a9-150">Click the container service resource, and click **Overview**.</span><span class="sxs-lookup"><span data-stu-id="276a9-150">Click the container service resource, and click **Overview**.</span></span> <span data-ttu-id="276a9-151">The **Master FQDN** of the cluster appears under **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="276a9-151">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="276a9-152">Save this name for later use.</span><span class="sxs-lookup"><span data-stu-id="276a9-152">Save this name for later use.</span></span> 

    ![Public DNS name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/pubdns.png)

    <span data-ttu-id="276a9-154">Alternatively, run the `az acs show` command on your container service.</span><span class="sxs-lookup"><span data-stu-id="276a9-154">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="276a9-155">Look for the **Master Profile:fqdn** property in the command output.</span><span class="sxs-lookup"><span data-stu-id="276a9-155">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="276a9-156">Now open a shell and run the `ssh` command by specifying the following values:</span><span class="sxs-lookup"><span data-stu-id="276a9-156">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="276a9-157">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span><span class="sxs-lookup"><span data-stu-id="276a9-157">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="276a9-158">For Swarm, set this to 2375.</span><span class="sxs-lookup"><span data-stu-id="276a9-158">For Swarm, set this to 2375.</span></span> <span data-ttu-id="276a9-159">For DC/OS, set this to 80.</span><span class="sxs-lookup"><span data-stu-id="276a9-159">For DC/OS, set this to 80.</span></span>  
    <span data-ttu-id="276a9-160">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span><span class="sxs-lookup"><span data-stu-id="276a9-160">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="276a9-161">For Swarm, use port 2375.</span><span class="sxs-lookup"><span data-stu-id="276a9-161">For Swarm, use port 2375.</span></span> <span data-ttu-id="276a9-162">For DC/OS, use port 80.</span><span class="sxs-lookup"><span data-stu-id="276a9-162">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="276a9-163">**USERNAME** is the user name that was provided when you deployed the cluster.</span><span class="sxs-lookup"><span data-stu-id="276a9-163">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="276a9-164">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span><span class="sxs-lookup"><span data-stu-id="276a9-164">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="276a9-165">**REGION** is the region in which your resource group is located.</span><span class="sxs-lookup"><span data-stu-id="276a9-165">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="276a9-166">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span><span class="sxs-lookup"><span data-stu-id="276a9-166">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="276a9-167">Use this option with the `-i` flag.</span><span class="sxs-lookup"><span data-stu-id="276a9-167">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com 
    ```
    > [!NOTE]
    > <span data-ttu-id="276a9-168">The SSH connection port is 2200 and not the standard port 22.</span><span class="sxs-lookup"><span data-stu-id="276a9-168">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="276a9-169">In a cluster with more than one master VM, this is the connection port to the first master VM.</span><span class="sxs-lookup"><span data-stu-id="276a9-169">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
    > 



<span data-ttu-id="276a9-170">See the examples for DC/OS and Swarm in the following sections.</span><span class="sxs-lookup"><span data-stu-id="276a9-170">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="276a9-171">DC/OS tunnel</span><span class="sxs-lookup"><span data-stu-id="276a9-171">DC/OS tunnel</span></span>
<span data-ttu-id="276a9-172">To open a tunnel for DC/OS endpoints, run a command like the following:</span><span class="sxs-lookup"><span data-stu-id="276a9-172">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="276a9-173">You can specify a local port other than port 80, such as port 8888.</span><span class="sxs-lookup"><span data-stu-id="276a9-173">You can specify a local port other than port 80, such as port 8888.</span></span> <span data-ttu-id="276a9-174">However, some web UI links might not work when you use this port.</span><span class="sxs-lookup"><span data-stu-id="276a9-174">However, some web UI links might not work when you use this port.</span></span>

<span data-ttu-id="276a9-175">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span><span class="sxs-lookup"><span data-stu-id="276a9-175">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="276a9-176">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="276a9-176">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="276a9-177">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="276a9-177">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="276a9-178">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="276a9-178">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="276a9-179">Similarly, you can reach the rest APIs for each application through this tunnel.</span><span class="sxs-lookup"><span data-stu-id="276a9-179">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="276a9-180">Swarm tunnel</span><span class="sxs-lookup"><span data-stu-id="276a9-180">Swarm tunnel</span></span>
<span data-ttu-id="276a9-181">To open a tunnel to the Swarm endpoint, run a command like the following:</span><span class="sxs-lookup"><span data-stu-id="276a9-181">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```

<span data-ttu-id="276a9-182">Now you can set your DOCKER_HOST environment variable as follows.</span><span class="sxs-lookup"><span data-stu-id="276a9-182">Now you can set your DOCKER_HOST environment variable as follows.</span></span> <span data-ttu-id="276a9-183">You can continue to use your Docker command-line interface (CLI) as normal.</span><span class="sxs-lookup"><span data-stu-id="276a9-183">You can continue to use your Docker command-line interface (CLI) as normal.</span></span>

```bash
export DOCKER_HOST=:2375
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="276a9-184">Create an SSH tunnel on Windows</span><span class="sxs-lookup"><span data-stu-id="276a9-184">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="276a9-185">There are multiple options for creating SSH tunnels on Windows.</span><span class="sxs-lookup"><span data-stu-id="276a9-185">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="276a9-186">This section describes how to use PuTTY to create the tunnel.</span><span class="sxs-lookup"><span data-stu-id="276a9-186">This section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="276a9-187">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span><span class="sxs-lookup"><span data-stu-id="276a9-187">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="276a9-188">Run the application.</span><span class="sxs-lookup"><span data-stu-id="276a9-188">Run the application.</span></span>

3. <span data-ttu-id="276a9-189">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span><span class="sxs-lookup"><span data-stu-id="276a9-189">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="276a9-190">The **Host Name** looks similar to `adminuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="276a9-190">The **Host Name** looks similar to `adminuser@PublicDNSName`.</span></span> <span data-ttu-id="276a9-191">Enter 2200 for the **Port**.</span><span class="sxs-lookup"><span data-stu-id="276a9-191">Enter 2200 for the **Port**.</span></span>

    ![PuTTY configuration 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/putty1.png)

4. <span data-ttu-id="276a9-193">Select **SSH > Auth**. Add a path to your private key file (.ppk format) for authentication.</span><span class="sxs-lookup"><span data-stu-id="276a9-193">Select **SSH > Auth**. Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="276a9-194">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="276a9-194">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![PuTTY configuration 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/putty2.png)

5. <span data-ttu-id="276a9-196">Select **SSH > Tunnels** and configure the following forwarded ports:</span><span class="sxs-lookup"><span data-stu-id="276a9-196">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="276a9-197">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span><span class="sxs-lookup"><span data-stu-id="276a9-197">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="276a9-198">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span><span class="sxs-lookup"><span data-stu-id="276a9-198">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="276a9-199">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="276a9-199">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="276a9-200">Port 80 must not be in use when you create this tunnel.</span><span class="sxs-lookup"><span data-stu-id="276a9-200">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY configuration 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/putty3.png)

6. <span data-ttu-id="276a9-202">When you're finished, click **Session > Save** to save the connection configuration.</span><span class="sxs-lookup"><span data-stu-id="276a9-202">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="276a9-203">To connect to the PuTTY session, click **Open**.</span><span class="sxs-lookup"><span data-stu-id="276a9-203">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="276a9-204">When you connect, you can see the port configuration in the PuTTY event log.</span><span class="sxs-lookup"><span data-stu-id="276a9-204">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![PuTTY event log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/putty4.png)

<span data-ttu-id="276a9-206">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span><span class="sxs-lookup"><span data-stu-id="276a9-206">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="276a9-207">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="276a9-207">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="276a9-208">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="276a9-208">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="276a9-209">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="276a9-209">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="276a9-210">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span><span class="sxs-lookup"><span data-stu-id="276a9-210">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="276a9-211">Then, you can access the Swarm cluster through the Docker CLI.</span><span class="sxs-lookup"><span data-stu-id="276a9-211">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="276a9-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="276a9-212">Next steps</span></span>
<span data-ttu-id="276a9-213">Deploy and manage containers in your cluster:</span><span class="sxs-lookup"><span data-stu-id="276a9-213">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="276a9-214">Work with Azure Container Service and Kubernetes</span><span class="sxs-lookup"><span data-stu-id="276a9-214">Work with Azure Container Service and Kubernetes</span></span>](container-service-kubernetes-ui.md)
* [<span data-ttu-id="276a9-215">Work with Azure Container Service and DC/OS</span><span class="sxs-lookup"><span data-stu-id="276a9-215">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="276a9-216">Work with the Azure Container Service and Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="276a9-216">Work with the Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)






