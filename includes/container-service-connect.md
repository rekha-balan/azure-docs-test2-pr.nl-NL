# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="5a3e1-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span><span class="sxs-lookup"><span data-stu-id="5a3e1-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="5a3e1-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="5a3e1-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="5a3e1-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="5a3e1-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="5a3e1-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="5a3e1-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5a3e1-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5a3e1-108">Prerequisites</span></span>

* <span data-ttu-id="5a3e1-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e1-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="5a3e1-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="5a3e1-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="5a3e1-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="5a3e1-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e1-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="5a3e1-114">Connect to a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="5a3e1-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="5a3e1-115">Follow these steps to install and configure `kubectl` on your computer.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="5a3e1-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="5a3e1-117">Install kubectl</span><span class="sxs-lookup"><span data-stu-id="5a3e1-117">Install kubectl</span></span>
<span data-ttu-id="5a3e1-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="5a3e1-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and signed in to an Azure account (`az login`).</span><span class="sxs-lookup"><span data-stu-id="5a3e1-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and signed in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="5a3e1-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e1-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="5a3e1-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="5a3e1-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="5a3e1-122">Download cluster credentials</span><span class="sxs-lookup"><span data-stu-id="5a3e1-122">Download cluster credentials</span></span>
<span data-ttu-id="5a3e1-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="5a3e1-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="5a3e1-125">Pass the name of the resource group and the name of the container service resource:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="5a3e1-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="5a3e1-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="5a3e1-128">For example:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="5a3e1-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="5a3e1-130">Use kubectl</span><span class="sxs-lookup"><span data-stu-id="5a3e1-130">Use kubectl</span></span>

<span data-ttu-id="5a3e1-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="5a3e1-132">You can try other `kubectl` commands.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="5a3e1-133">For example, you can view the Kubernetes Dashboard.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="5a3e1-134">First, run a proxy to the Kubernetes API server:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="5a3e1-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="5a3e1-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="5a3e1-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="5a3e1-137">Connect to a DC/OS or Swarm cluster</span><span class="sxs-lookup"><span data-stu-id="5a3e1-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="5a3e1-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="5a3e1-139">These instructions focus on tunneling TCP traffic over SSH.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="5a3e1-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="5a3e1-141">Working directly on an internal system risks inadvertent configuration changes.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="5a3e1-142">Create an SSH tunnel on Linux or macOS</span><span class="sxs-lookup"><span data-stu-id="5a3e1-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="5a3e1-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="5a3e1-144">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-144">Follow these steps:</span></span>


1. <span data-ttu-id="5a3e1-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="5a3e1-146">Expand the resource group so that each resource is displayed.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="5a3e1-147">Click the **Container service** resource, and click **Overview**.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="5a3e1-148">The **Master FQDN** of the cluster appears under **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="5a3e1-149">Save this name for later use.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-149">Save this name for later use.</span></span> 

    ![Public DNS name](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="5a3e1-151">Alternatively, run the `az acs show` command on your container service.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="5a3e1-152">Look for the **Master Profile:fqdn** property in the command output.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="5a3e1-153">Now open a shell and run the `ssh` command by specifying the following values:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="5a3e1-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="5a3e1-155">For Swarm, set this to 2375.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="5a3e1-156">For DC/OS, set this to 80.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="5a3e1-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="5a3e1-158">For Swarm, use port 2375.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="5a3e1-159">For DC/OS, use port 80.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="5a3e1-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="5a3e1-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="5a3e1-162">**REGION** is the region in which your resource group is located.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="5a3e1-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="5a3e1-164">Use this option with the `-i` flag.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="5a3e1-165">The SSH connection port is 2200 and not the standard port 22.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="5a3e1-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="5a3e1-167">The command returns without output.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-167">The command returns without output.</span></span>

<span data-ttu-id="5a3e1-168">See the examples for DC/OS and Swarm in the following sections.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="5a3e1-169">DC/OS tunnel</span><span class="sxs-lookup"><span data-stu-id="5a3e1-169">DC/OS tunnel</span></span>
<span data-ttu-id="5a3e1-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="5a3e1-171">Ensure that you do not have another local process that binds port 80.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="5a3e1-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="5a3e1-173">However, some web UI links might not work when you use this port.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="5a3e1-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span><span class="sxs-lookup"><span data-stu-id="5a3e1-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="5a3e1-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="5a3e1-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="5a3e1-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="5a3e1-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="5a3e1-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="5a3e1-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="5a3e1-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="5a3e1-179">Swarm tunnel</span><span class="sxs-lookup"><span data-stu-id="5a3e1-179">Swarm tunnel</span></span>
<span data-ttu-id="5a3e1-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="5a3e1-181">Ensure that you do not have another local process that binds port 2375.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="5a3e1-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="5a3e1-183">If necessary, you can specify a local port other than port 2375.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="5a3e1-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="5a3e1-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="5a3e1-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="5a3e1-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="5a3e1-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="5a3e1-188">For example:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="5a3e1-189">Create an SSH tunnel on Windows</span><span class="sxs-lookup"><span data-stu-id="5a3e1-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="5a3e1-190">There are multiple options for creating SSH tunnels on Windows.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="5a3e1-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="5a3e1-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="5a3e1-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="5a3e1-194">Run the application.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-194">Run the application.</span></span>

3. <span data-ttu-id="5a3e1-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="5a3e1-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="5a3e1-197">Enter 2200 for the **Port**.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-197">Enter 2200 for the **Port**.</span></span>

    ![PuTTY configuration 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="5a3e1-199">Select **SSH > Auth**. Add a path to your private key file (.ppk format) for authentication.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-199">Select **SSH > Auth**. Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="5a3e1-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![PuTTY configuration 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="5a3e1-202">Select **SSH > Tunnels** and configure the following forwarded ports:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-202">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="5a3e1-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="5a3e1-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="5a3e1-205">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-205">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5a3e1-206">Port 80 must not be in use when you create this tunnel.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY configuration 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="5a3e1-208">When you're finished, click **Session > Save** to save the connection configuration.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-208">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="5a3e1-209">To connect to the PuTTY session, click **Open**.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-209">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="5a3e1-210">When you connect, you can see the port configuration in the PuTTY event log.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-210">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![PuTTY event log](./media/container-service-connect/putty4.png)

<span data-ttu-id="5a3e1-212">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-212">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="5a3e1-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="5a3e1-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="5a3e1-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="5a3e1-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="5a3e1-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="5a3e1-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="5a3e1-216">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-216">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="5a3e1-217">Then, you can access the Swarm cluster through the Docker CLI.</span><span class="sxs-lookup"><span data-stu-id="5a3e1-217">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a3e1-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a3e1-218">Next steps</span></span>
<span data-ttu-id="5a3e1-219">Deploy and manage containers in your cluster:</span><span class="sxs-lookup"><span data-stu-id="5a3e1-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="5a3e1-220">Work with Azure Container Service and Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5a3e1-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="5a3e1-221">Work with Azure Container Service and DC/OS</span><span class="sxs-lookup"><span data-stu-id="5a3e1-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="5a3e1-222">Work with the Azure Container Service and Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5a3e1-222">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

