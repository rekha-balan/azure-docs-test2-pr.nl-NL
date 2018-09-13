---
title: Azure Kubernetes cluster for Windows | Microsoft Docs
description: Deploy and get started with a Kubernetes cluster for Windows containers in Azure Container Service
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service, kubernetes
keywords: ''
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/20/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 680e3f9aead02a7e143e9d66e895c9616505bef4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563892"
---
# <a name="get-started-with-kubernetes-and-windows-containers-in-container-service"></a><span data-ttu-id="dcfb5-103">Get started with Kubernetes and Windows containers in Container Service</span><span class="sxs-lookup"><span data-stu-id="dcfb5-103">Get started with Kubernetes and Windows containers in Container Service</span></span>


<span data-ttu-id="dcfb5-104">This article shows how to create a Kubernetes cluster in Azure Container Service that contains Windows nodes to run Windows containers.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-104">This article shows how to create a Kubernetes cluster in Azure Container Service that contains Windows nodes to run Windows containers.</span></span> 

> [!NOTE]
> <span data-ttu-id="dcfb5-105">Support for Windows containers with Kubernetes in Azure Container Service is in preview.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-105">Support for Windows containers with Kubernetes in Azure Container Service is in preview.</span></span> <span data-ttu-id="dcfb5-106">Use the Azure portal or a Resource Manager template to create a Kubernetes cluster with Windows nodes.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-106">Use the Azure portal or a Resource Manager template to create a Kubernetes cluster with Windows nodes.</span></span> <span data-ttu-id="dcfb5-107">This feature isn't currently supported with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-107">This feature isn't currently supported with the Azure CLI 2.0.</span></span>
>



<span data-ttu-id="dcfb5-108">The following image shows the architecture of a Kubernetes cluster in Azure Container Service with one Linux master node and two Windows agent nodes.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-108">The following image shows the architecture of a Kubernetes cluster in Azure Container Service with one Linux master node and two Windows agent nodes.</span></span> 

* <span data-ttu-id="dcfb5-109">The Linux master serves the Kubernetes REST API and is accessible by SSH on port 22 or `kubectl` on port 443.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-109">The Linux master serves the Kubernetes REST API and is accessible by SSH on port 22 or `kubectl` on port 443.</span></span> 
* <span data-ttu-id="dcfb5-110">The Windows agent nodes are grouped in an Azure availability set and run your containers.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-110">The Windows agent nodes are grouped in an Azure availability set and run your containers.</span></span> <span data-ttu-id="dcfb5-111">The Windows nodes can be accessed through an RDP SSH tunnel via the master node.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-111">The Windows nodes can be accessed through an RDP SSH tunnel via the master node.</span></span> <span data-ttu-id="dcfb5-112">Azure load balancer rules are dynamically added to the cluster depending on exposed services.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-112">Azure load balancer rules are dynamically added to the cluster depending on exposed services.</span></span>


![Image of Kubernetes cluster on Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-windows-walkthrough/kubernetes-windows.png)

<span data-ttu-id="dcfb5-114">All VMs are in the same private virtual network and are fully accessible to each other.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-114">All VMs are in the same private virtual network and are fully accessible to each other.</span></span> <span data-ttu-id="dcfb5-115">All VMs run a kubelet, Docker, and a proxy.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-115">All VMs run a kubelet, Docker, and a proxy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcfb5-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dcfb5-116">Prerequisites</span></span>


* <span data-ttu-id="dcfb5-117">**SSH RSA public key**: When deploying through the portal or one of the Azure quickstart templates, you need to provide an SSH RSA public key for authentication against Azure Container Service virtual machines.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-117">**SSH RSA public key**: When deploying through the portal or one of the Azure quickstart templates, you need to provide an SSH RSA public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="dcfb5-118">To create Secure Shell (SSH) RSA keys, see the [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md) guidance.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-118">To create Secure Shell (SSH) RSA keys, see the [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="dcfb5-119">**Service principal client ID and secret**: For more information and guidance, see [About the service principal for a Kubernetes cluster](container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="dcfb5-119">**Service principal client ID and secret**: For more information and guidance, see [About the service principal for a Kubernetes cluster](container-service-kubernetes-service-principal.md).</span></span>




## <a name="create-the-cluster"></a><span data-ttu-id="dcfb5-120">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="dcfb5-120">Create the cluster</span></span>

<span data-ttu-id="dcfb5-121">You can use the Azure portal to [create a Kubernetes cluster](container-service-deployment.md#create-a-cluster-by-using-the-azure-portal) with Windows agent nodes.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-121">You can use the Azure portal to [create a Kubernetes cluster](container-service-deployment.md#create-a-cluster-by-using-the-azure-portal) with Windows agent nodes.</span></span> <span data-ttu-id="dcfb5-122">Note the following settings when creating the cluster:</span><span class="sxs-lookup"><span data-stu-id="dcfb5-122">Note the following settings when creating the cluster:</span></span>

* <span data-ttu-id="dcfb5-123">On the **Basics** blade, in **Orchestrator**, select **Kubernetes**.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-123">On the **Basics** blade, in **Orchestrator**, select **Kubernetes**.</span></span> 

  ![Select Kubernetes orchestrator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-windows-walkthrough/portal-select-kubernetes.png)

* <span data-ttu-id="dcfb5-125">On the **Master configuration** blade, enter user credentials and service principal credentials for the Linux master nodes.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-125">On the **Master configuration** blade, enter user credentials and service principal credentials for the Linux master nodes.</span></span> <span data-ttu-id="dcfb5-126">Choose 1, 3, or 5 masters.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-126">Choose 1, 3, or 5 masters.</span></span>

* <span data-ttu-id="dcfb5-127">On the **Agent configuration** blade, in **Operating system**, select **Windows (preview)**.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-127">On the **Agent configuration** blade, in **Operating system**, select **Windows (preview)**.</span></span> <span data-ttu-id="dcfb5-128">Enter administrator credentials for the Windows agent nodes.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-128">Enter administrator credentials for the Windows agent nodes.</span></span>

  ![Select Windows agents](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-windows-walkthrough/portal-select-windows.png)

<span data-ttu-id="dcfb5-130">For more details, see [Deploy an Azure Container Service cluster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="dcfb5-130">For more details, see [Deploy an Azure Container Service cluster](container-service-deployment.md).</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="dcfb5-131">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="dcfb5-131">Connect to the cluster</span></span>

<span data-ttu-id="dcfb5-132">Use the `kubectl` command-line tool to connect from your local computer to the master node of the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-132">Use the `kubectl` command-line tool to connect from your local computer to the master node of the Kubernetes cluster.</span></span> <span data-ttu-id="dcfb5-133">For steps to install and set up `kubectl`, see [Connect to an Azure Container Service cluster](container-service-connect.md#connect-to-a-kubernetes-cluster).</span><span class="sxs-lookup"><span data-stu-id="dcfb5-133">For steps to install and set up `kubectl`, see [Connect to an Azure Container Service cluster](container-service-connect.md#connect-to-a-kubernetes-cluster).</span></span> <span data-ttu-id="dcfb5-134">You can use `kubectl` commands to access the Kubernetes web UI and to create and manage Windows container workloads.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-134">You can use `kubectl` commands to access the Kubernetes web UI and to create and manage Windows container workloads.</span></span>

## <a name="create-your-first-kubernetes-service"></a><span data-ttu-id="dcfb5-135">Create your first Kubernetes service</span><span class="sxs-lookup"><span data-stu-id="dcfb5-135">Create your first Kubernetes service</span></span>

<span data-ttu-id="dcfb5-136">After creating the cluster and connecting with `kubectl`, you can try starting a basic Windows web app and expose it to the internet.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-136">After creating the cluster and connecting with `kubectl`, you can try starting a basic Windows web app and expose it to the internet.</span></span> <span data-ttu-id="dcfb5-137">In this example, you specify the container resources using a YAML file, and then create it using `kubctl apply`.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-137">In this example, you specify the container resources using a YAML file, and then create it using `kubctl apply`.</span></span>

1. <span data-ttu-id="dcfb5-138">To see a list of your nodes, type `kubectl get nodes`.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-138">To see a list of your nodes, type `kubectl get nodes`.</span></span> <span data-ttu-id="dcfb5-139">If you want full details of the nodes, type:</span><span class="sxs-lookup"><span data-stu-id="dcfb5-139">If you want full details of the nodes, type:</span></span>  

    ```
    kubectl get nodes -o yaml
    ```

2. <span data-ttu-id="dcfb5-140">Create a file named `simpleweb.yaml` and copy the following.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-140">Create a file named `simpleweb.yaml` and copy the following.</span></span> <span data-ttu-id="dcfb5-141">This file sets up a web app using the Windows Server 2016 Server Core base OS image from [Docker Hub](https://hub.docker.com/r/microsoft/windowsservercore/).</span><span class="sxs-lookup"><span data-stu-id="dcfb5-141">This file sets up a web app using the Windows Server 2016 Server Core base OS image from [Docker Hub](https://hub.docker.com/r/microsoft/windowsservercore/).</span></span>  

```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: win-webserver
    labels:
      app: win-webserver
  spec:
    ports:
      # the port that this service should serve on
    - port: 80
      targetPort: 80
    selector:
      app: win-webserver
    type: LoadBalancer
  ---
  apiVersion: extensions/v1beta1
  kind: Deployment
  metadata:
    labels:
      app: win-webserver
    name: win-webserver
  spec:
    replicas: 1
    template:
      metadata:
        labels:
          app: win-webserver
        name: win-webserver
      spec:
        containers:
        - name: windowswebserver
          image: microsoft/windowsservercore
          command:
          - powershell.exe
          - -command
          - "<#code used from https://gist.github.com/wagnerandrade/5424431#> ; $$listener = New-Object System.Net.HttpListener ; $$listener.Prefixes.Add('http://*:80/') ; $$listener.Start() ; $$callerCounts = @{} ; Write-Host('Listening at http://*:80/') ; while ($$listener.IsListening) { ;$$context = $$listener.GetContext() ;$$requestUrl = $$context.Request.Url ;$$clientIP = $$context.Request.RemoteEndPoint.Address ;$$response = $$context.Response ;Write-Host '' ;Write-Host('> {0}' -f $$requestUrl) ;  ;$$count = 1 ;$$k=$$callerCounts.Get_Item($$clientIP) ;if ($$k -ne $$null) { $$count += $$k } ;$$callerCounts.Set_Item($$clientIP, $$count) ;$$header='<html><body><H1>Windows Container Web Server</H1>' ;$$callerCountsString='' ;$$callerCounts.Keys | % { $$callerCountsString+='<p>IP {0} callerCount {1} ' -f $$_,$$callerCounts.Item($$_) } ;$$footer='</body></html>' ;$$content='{0}{1}{2}' -f $$header,$$callerCountsString,$$footer ;Write-Output $$content ;$$buffer = [System.Text.Encoding]::UTF8.GetBytes($$content) ;$$response.ContentLength64 = $$buffer.Length ;$$response.OutputStream.Write($$buffer, 0, $$buffer.Length) ;$$response.Close() ;$$responseStatus = $$response.StatusCode ;Write-Host('< {0}' -f $$responseStatus)  } ; "
        nodeSelector:
          beta.kubernetes.io/os: windows
  ```

      
> [!NOTE] 
> <span data-ttu-id="dcfb5-142">The configuration includes `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-142">The configuration includes `type: LoadBalancer`.</span></span> <span data-ttu-id="dcfb5-143">This setting causes the service to be exposed to the internet through an Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-143">This setting causes the service to be exposed to the internet through an Azure load balancer.</span></span> <span data-ttu-id="dcfb5-144">For more information, see [Load balance containers in a Kubernetes cluster in Azure Container Service](container-service-kubernetes-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="dcfb5-144">For more information, see [Load balance containers in a Kubernetes cluster in Azure Container Service](container-service-kubernetes-load-balancing.md).</span></span>
>

## <a name="start-the-application"></a><span data-ttu-id="dcfb5-145">Start the application</span><span class="sxs-lookup"><span data-stu-id="dcfb5-145">Start the application</span></span>

1. <span data-ttu-id="dcfb5-146">To start the application, type:</span><span class="sxs-lookup"><span data-stu-id="dcfb5-146">To start the application, type:</span></span>  

    ```
    kubectl apply -f simpleweb.yaml
    ```  
  
  
2. <span data-ttu-id="dcfb5-147">To verify the deployment of the service (which takes about 30 seconds), type:</span><span class="sxs-lookup"><span data-stu-id="dcfb5-147">To verify the deployment of the service (which takes about 30 seconds), type:</span></span>  

    ```
    kubectl get pods
    ```

3. <span data-ttu-id="dcfb5-148">After the service is running, to see the internal and external IP addresses of the service, type:</span><span class="sxs-lookup"><span data-stu-id="dcfb5-148">After the service is running, to see the internal and external IP addresses of the service, type:</span></span>

    ```
    kubectl get svc
    ``` 
  
    ![IP addresses of Windows service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-windows-walkthrough/externalipa.png)

    <span data-ttu-id="dcfb5-150">The addition of the external IP address takes several minutes.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-150">The addition of the external IP address takes several minutes.</span></span> <span data-ttu-id="dcfb5-151">Before the load balancer configures the external address, it appears as `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-151">Before the load balancer configures the external address, it appears as `<pending>`.</span></span>

4. <span data-ttu-id="dcfb5-152">After the external IP address is available, you can reach the service in your web browser.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-152">After the external IP address is available, you can reach the service in your web browser.</span></span>

    ![Windows server app in browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-windows-walkthrough/wincontainerwebserver.png)


## <a name="access-the-windows-nodes"></a><span data-ttu-id="dcfb5-154">Access the Windows nodes</span><span class="sxs-lookup"><span data-stu-id="dcfb5-154">Access the Windows nodes</span></span>
<span data-ttu-id="dcfb5-155">Windows nodes can be accessed from a local Windows computer through Remote Desktop Connection.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-155">Windows nodes can be accessed from a local Windows computer through Remote Desktop Connection.</span></span> <span data-ttu-id="dcfb5-156">We recommend using an RDP SSH tunnel via the master node.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-156">We recommend using an RDP SSH tunnel via the master node.</span></span> 

<span data-ttu-id="dcfb5-157">There are multiple options for creating SSH tunnels on Windows.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-157">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="dcfb5-158">This section describes how to use PuTTY to create the tunnel.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-158">This section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="dcfb5-159">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-159">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="dcfb5-160">Run the application.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-160">Run the application.</span></span>

3. <span data-ttu-id="dcfb5-161">Enter a host name that is composed of the cluster admin user name and the public DNS name of the first master in the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-161">Enter a host name that is composed of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="dcfb5-162">The **Host Name** looks similar to `adminuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-162">The **Host Name** looks similar to `adminuser@PublicDNSName`.</span></span> <span data-ttu-id="dcfb5-163">Enter 22 for the **Port**.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-163">Enter 22 for the **Port**.</span></span>

  ![PuTTY configuration 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-windows-walkthrough/putty1.png)

4. <span data-ttu-id="dcfb5-165">Select **SSH > Auth**. Add a path to your private key file (.ppk format) for authentication.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-165">Select **SSH > Auth**. Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="dcfb5-166">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-166">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

  ![PuTTY configuration 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-windows-walkthrough/putty2.png)

5. <span data-ttu-id="dcfb5-168">Select **SSH > Tunnels** and configure the  forwarded ports.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-168">Select **SSH > Tunnels** and configure the  forwarded ports.</span></span> <span data-ttu-id="dcfb5-169">Since your local Windows machine is already using port 3389, it is recommended to use the following settings to reach Windows node 0 and Windows node 1.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-169">Since your local Windows machine is already using port 3389, it is recommended to use the following settings to reach Windows node 0 and Windows node 1.</span></span> <span data-ttu-id="dcfb5-170">(Continue this pattern for additional Windows nodes.)</span><span class="sxs-lookup"><span data-stu-id="dcfb5-170">(Continue this pattern for additional Windows nodes.)</span></span>

    <span data-ttu-id="dcfb5-171">**Windows Node 0**</span><span class="sxs-lookup"><span data-stu-id="dcfb5-171">**Windows Node 0**</span></span>

    * <span data-ttu-id="dcfb5-172">**Source Port:** 3390</span><span class="sxs-lookup"><span data-stu-id="dcfb5-172">**Source Port:** 3390</span></span>
    * <span data-ttu-id="dcfb5-173">**Destination:** 10.240.245.5:3389</span><span class="sxs-lookup"><span data-stu-id="dcfb5-173">**Destination:** 10.240.245.5:3389</span></span>

    <span data-ttu-id="dcfb5-174">**Windows Node 1**</span><span class="sxs-lookup"><span data-stu-id="dcfb5-174">**Windows Node 1**</span></span>

    * <span data-ttu-id="dcfb5-175">**Source Port:** 3391</span><span class="sxs-lookup"><span data-stu-id="dcfb5-175">**Source Port:** 3391</span></span>
    * <span data-ttu-id="dcfb5-176">**Destination:** 10.240.245.6:3389</span><span class="sxs-lookup"><span data-stu-id="dcfb5-176">**Destination:** 10.240.245.6:3389</span></span>

    ![Image of Windows RDP tunnels](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-windows-walkthrough/rdptunnels.png)

6. <span data-ttu-id="dcfb5-178">When you're finished, click **Session > Save** to save the connection configuration.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-178">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="dcfb5-179">To connect to the PuTTY session, click **Open**.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-179">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="dcfb5-180">Complete the connection to the master node.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-180">Complete the connection to the master node.</span></span>

8. <span data-ttu-id="dcfb5-181">Start Remote Desktop Connection.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-181">Start Remote Desktop Connection.</span></span> <span data-ttu-id="dcfb5-182">To connect to the first Windows node, for **Computer**, specify `localhost:3390`, and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-182">To connect to the first Windows node, for **Computer**, specify `localhost:3390`, and click **Connect**.</span></span> <span data-ttu-id="dcfb5-183">(To connect to the second, specify `localhost:3390`, and so on.) To complete your connection, provide the local Windows administrator password you configured during deployment.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-183">(To connect to the second, specify `localhost:3390`, and so on.) To complete your connection, provide the local Windows administrator password you configured during deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dcfb5-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="dcfb5-184">Next steps</span></span>

<span data-ttu-id="dcfb5-185">Here are recommended links to learn more about Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="dcfb5-185">Here are recommended links to learn more about Kubernetes:</span></span>

* <span data-ttu-id="dcfb5-186">[Kubernetes Bootcamp](https://kubernetesbootcamp.github.io/kubernetes-bootcamp/index.html) - shows you how to deploy, scale, update, and debug containerized applications.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-186">[Kubernetes Bootcamp](https://kubernetesbootcamp.github.io/kubernetes-bootcamp/index.html) - shows you how to deploy, scale, update, and debug containerized applications.</span></span>
* <span data-ttu-id="dcfb5-187">[Kubernetes User Guide](http://kubernetes.io/docs/user-guide/) - provides information on running programs in an existing Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-187">[Kubernetes User Guide](http://kubernetes.io/docs/user-guide/) - provides information on running programs in an existing Kubernetes cluster.</span></span>
* <span data-ttu-id="dcfb5-188">[Kubernetes Examples](https://github.com/kubernetes/kubernetes/tree/master/examples) - provides examples on how to run real applications with Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="dcfb5-188">[Kubernetes Examples](https://github.com/kubernetes/kubernetes/tree/master/examples) - provides examples on how to run real applications with Kubernetes.</span></span>







