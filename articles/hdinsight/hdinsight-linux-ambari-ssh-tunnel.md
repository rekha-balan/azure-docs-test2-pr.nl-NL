---
title: Use SSH tunneling to access Azure HDInsight services | Microsoft Docs
description: Learn how to use an SSH tunnel to securely browse web resources hosted on your Linux-based HDInsight nodes.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/06/2017
ms.author: larryfr
ms.openlocfilehash: d7c407d2696dd08d9d15b0d5268008ad0c66daf9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660835"
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="fcb91-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UI's</span><span class="sxs-lookup"><span data-stu-id="fcb91-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UI's</span></span>

<span data-ttu-id="fcb91-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span><span class="sxs-lookup"><span data-stu-id="fcb91-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="fcb91-105">For example, the web UI for other services that are surfaced through Ambari.</span><span class="sxs-lookup"><span data-stu-id="fcb91-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="fcb91-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span><span class="sxs-lookup"><span data-stu-id="fcb91-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="fcb91-107">Why use an SSH tunnel</span><span class="sxs-lookup"><span data-stu-id="fcb91-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="fcb91-108">Several of the menus in Ambari do not fully populate without an SSH tunnel, as they rely on web sites and services exposed by other Hadoop services running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="fcb91-108">Several of the menus in Ambari do not fully populate without an SSH tunnel, as they rely on web sites and services exposed by other Hadoop services running on the cluster.</span></span> <span data-ttu-id="fcb91-109">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span><span class="sxs-lookup"><span data-stu-id="fcb91-109">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span> <span data-ttu-id="fcb91-110">Sometimes the service runs the web site on another cluster node such as a Zookeeper node.</span><span class="sxs-lookup"><span data-stu-id="fcb91-110">Sometimes the service runs the web site on another cluster node such as a Zookeeper node.</span></span>

<span data-ttu-id="fcb91-111">The following are services that Ambari web UI uses, that cannot be accessed without an SSH tunnel:</span><span class="sxs-lookup"><span data-stu-id="fcb91-111">The following are services that Ambari web UI uses, that cannot be accessed without an SSH tunnel:</span></span>

* <span data-ttu-id="fcb91-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="fcb91-112">JobHistory</span></span>
* <span data-ttu-id="fcb91-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="fcb91-113">NameNode</span></span>
* <span data-ttu-id="fcb91-114">Thread Stacks</span><span class="sxs-lookup"><span data-stu-id="fcb91-114">Thread Stacks</span></span>
* <span data-ttu-id="fcb91-115">Oozie web UI</span><span class="sxs-lookup"><span data-stu-id="fcb91-115">Oozie web UI</span></span>
* <span data-ttu-id="fcb91-116">HBase Master and Logs UI</span><span class="sxs-lookup"><span data-stu-id="fcb91-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="fcb91-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="fcb91-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="fcb91-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span><span class="sxs-lookup"><span data-stu-id="fcb91-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="fcb91-119">What is an SSH tunnel</span><span class="sxs-lookup"><span data-stu-id="fcb91-119">What is an SSH tunnel</span></span>

<span data-ttu-id="fcb91-120">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation, through an SSH connection to your HDInsight cluster head node, where the request is then resolved as if it originated on the head node.</span><span class="sxs-lookup"><span data-stu-id="fcb91-120">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation, through an SSH connection to your HDInsight cluster head node, where the request is then resolved as if it originated on the head node.</span></span> <span data-ttu-id="fcb91-121">The response is then routed back through the tunnel to your workstation.</span><span class="sxs-lookup"><span data-stu-id="fcb91-121">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcb91-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fcb91-122">Prerequisites</span></span>

<span data-ttu-id="fcb91-123">When using an SSH tunnel for web traffic, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="fcb91-123">When using an SSH tunnel for web traffic, you must have the following:</span></span>

* <span data-ttu-id="fcb91-124">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="fcb91-124">An SSH client.</span></span> <span data-ttu-id="fcb91-125">For Linux and Unix distributions, Macintosh OS X, and Bash on Windows 10, the `ssh` command is provided with the operating system.</span><span class="sxs-lookup"><span data-stu-id="fcb91-125">For Linux and Unix distributions, Macintosh OS X, and Bash on Windows 10, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="fcb91-126">For Windows versions that do not include the `ssh` command, we recommend [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="fcb91-126">For Windows versions that do not include the `ssh` command, we recommend [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="fcb91-127">If you want to use an SSH client other than `ssh` or PuTTY, please consult the documentation for your client on how to establish an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="fcb91-127">If you want to use an SSH client other than `ssh` or PuTTY, please consult the documentation for your client on how to establish an SSH tunnel.</span></span>

* <span data-ttu-id="fcb91-128">A web browser that can be configured to use a SOCKS5 proxy.</span><span class="sxs-lookup"><span data-stu-id="fcb91-128">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="fcb91-129">The SOCKS proxy support built into Windows does not support SOCKS5, and will not work with the steps in this document.</span><span class="sxs-lookup"><span data-stu-id="fcb91-129">The SOCKS proxy support built into Windows does not support SOCKS5, and will not work with the steps in this document.</span></span> <span data-ttu-id="fcb91-130">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span><span class="sxs-lookup"><span data-stu-id="fcb91-130">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    > 
    > * <span data-ttu-id="fcb91-131">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="fcb91-131">Microsoft Edge</span></span>
    > * <span data-ttu-id="fcb91-132">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="fcb91-132">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="fcb91-133">Google Chrome also relies on the Windows proxy settings.</span><span class="sxs-lookup"><span data-stu-id="fcb91-133">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="fcb91-134">However, you can install extensions that support SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="fcb91-134">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="fcb91-135">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="fcb91-135">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <a name="usessh"></a><span data-ttu-id="fcb91-136">Create a tunnel using the SSH command</span><span class="sxs-lookup"><span data-stu-id="fcb91-136">Create a tunnel using the SSH command</span></span>

<span data-ttu-id="fcb91-137">Use the following command to create an SSH tunnel using the `ssh` command.</span><span class="sxs-lookup"><span data-stu-id="fcb91-137">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="fcb91-138">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="fcb91-138">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster</span></span>

```
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="fcb91-139">This creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span><span class="sxs-lookup"><span data-stu-id="fcb91-139">This creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="fcb91-140">The options are:</span><span class="sxs-lookup"><span data-stu-id="fcb91-140">The options are:</span></span>

* <span data-ttu-id="fcb91-141">**D 9876** - The local port that routes traffic through the tunnel.</span><span class="sxs-lookup"><span data-stu-id="fcb91-141">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="fcb91-142">**C** - Compress all data, because web traffic is mostly text.</span><span class="sxs-lookup"><span data-stu-id="fcb91-142">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="fcb91-143">**2** - Force SSH to try protocol version 2 only.</span><span class="sxs-lookup"><span data-stu-id="fcb91-143">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="fcb91-144">**q** - Quiet mode.</span><span class="sxs-lookup"><span data-stu-id="fcb91-144">**q** - Quiet mode.</span></span>
* <span data-ttu-id="fcb91-145">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span><span class="sxs-lookup"><span data-stu-id="fcb91-145">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="fcb91-146">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span><span class="sxs-lookup"><span data-stu-id="fcb91-146">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="fcb91-147">**N** - Do not execute a remote command, since we are just forwarding a port.</span><span class="sxs-lookup"><span data-stu-id="fcb91-147">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="fcb91-148">**f** - Run in the background.</span><span class="sxs-lookup"><span data-stu-id="fcb91-148">**f** - Run in the background.</span></span>

<span data-ttu-id="fcb91-149">If you configured the cluster with an SSH key, you may need use the `-i` parameter and specify the path to the private SSH key.</span><span class="sxs-lookup"><span data-stu-id="fcb91-149">If you configured the cluster with an SSH key, you may need use the `-i` parameter and specify the path to the private SSH key.</span></span>

<span data-ttu-id="fcb91-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed over Secure Sockets Layer (SSL) to the cluster head node and appear to originate there.</span><span class="sxs-lookup"><span data-stu-id="fcb91-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed over Secure Sockets Layer (SSL) to the cluster head node and appear to originate there.</span></span>

## <a name="useputty"></a><span data-ttu-id="fcb91-151">Create a tunnel using PuTTY</span><span class="sxs-lookup"><span data-stu-id="fcb91-151">Create a tunnel using PuTTY</span></span>

<span data-ttu-id="fcb91-152">Use the following steps to create an SSH tunnel using PuTTY.</span><span class="sxs-lookup"><span data-stu-id="fcb91-152">Use the following steps to create an SSH tunnel using PuTTY.</span></span>

1. <span data-ttu-id="fcb91-153">Open PuTTY, and enter your connection information.</span><span class="sxs-lookup"><span data-stu-id="fcb91-153">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="fcb91-154">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="fcb91-154">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="fcb91-155">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-155">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="fcb91-156">Provide the following information on the **Options controlling SSH port forwarding** form:</span><span class="sxs-lookup"><span data-stu-id="fcb91-156">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="fcb91-157">**Source port** - The port on the client that you wish to forward.</span><span class="sxs-lookup"><span data-stu-id="fcb91-157">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="fcb91-158">For example, **9876**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-158">For example, **9876**.</span></span>

   * <span data-ttu-id="fcb91-159">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="fcb91-159">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="fcb91-160">For example, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-160">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="fcb91-161">**Dynamic** - Enables dynamic SOCKS proxy routing.</span><span class="sxs-lookup"><span data-stu-id="fcb91-161">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![image of tunneling options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="fcb91-163">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span><span class="sxs-lookup"><span data-stu-id="fcb91-163">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="fcb91-164">When prompted, log in to the server.</span><span class="sxs-lookup"><span data-stu-id="fcb91-164">When prompted, log in to the server.</span></span> <span data-ttu-id="fcb91-165">This establishes an SSH session and enable the tunnel.</span><span class="sxs-lookup"><span data-stu-id="fcb91-165">This establishes an SSH session and enable the tunnel.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="fcb91-166">Use the tunnel from your browser</span><span class="sxs-lookup"><span data-stu-id="fcb91-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcb91-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span><span class="sxs-lookup"><span data-stu-id="fcb91-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="fcb91-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span><span class="sxs-lookup"><span data-stu-id="fcb91-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="fcb91-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="fcb91-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="fcb91-170">Here's what the Firefox settings look like.</span><span class="sxs-lookup"><span data-stu-id="fcb91-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="fcb91-171">If you used a different port than 9876, change the port to the one you used:</span><span class="sxs-lookup"><span data-stu-id="fcb91-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![image of Firefox settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="fcb91-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="fcb91-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="fcb91-174">If this is unselected, DNS is resolved locally.</span><span class="sxs-lookup"><span data-stu-id="fcb91-174">If this is unselected, DNS is resolved locally.</span></span>

2. <span data-ttu-id="fcb91-175">Verify that traffic is being routed through the tunnel by vising a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/) with the proxy settings enabled and disabled in Firefox.</span><span class="sxs-lookup"><span data-stu-id="fcb91-175">Verify that traffic is being routed through the tunnel by vising a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/) with the proxy settings enabled and disabled in Firefox.</span></span> <span data-ttu-id="fcb91-176">While the settings are enabled, the IP address returned is from a machine in the Microsoft Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="fcb91-176">While the settings are enabled, the IP address returned is from a machine in the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="fcb91-177">Verify with Ambari web UI</span><span class="sxs-lookup"><span data-stu-id="fcb91-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="fcb91-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span><span class="sxs-lookup"><span data-stu-id="fcb91-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="fcb91-179">In your browser, go to http://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="fcb91-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="fcb91-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span><span class="sxs-lookup"><span data-stu-id="fcb91-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="fcb91-181">When prompted, enter the admin user name (admin) and password for your cluster.</span><span class="sxs-lookup"><span data-stu-id="fcb91-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="fcb91-182">You may be prompted a second time by the Ambari web UI.</span><span class="sxs-lookup"><span data-stu-id="fcb91-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="fcb91-183">If so, re-enter the information.</span><span class="sxs-lookup"><span data-stu-id="fcb91-183">If so, re-enter the information.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fcb91-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting directly over the tunnel to the head node that Ambari is running on using HTTP and communication is secured using the SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="fcb91-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting directly over the tunnel to the head node that Ambari is running on using HTTP and communication is secured using the SSH tunnel.</span></span> <span data-ttu-id="fcb91-185">when connecting over the internet without the use of a tunnel, communication is secured using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fcb91-185">when connecting over the internet without the use of a tunnel, communication is secured using HTTPS.</span></span> <span data-ttu-id="fcb91-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="fcb91-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="fcb91-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span><span class="sxs-lookup"><span data-stu-id="fcb91-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>
   
    ![Image with HDFS selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)
3. <span data-ttu-id="fcb91-189">When the HDFS service information is displayed, select **Quick Links**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="fcb91-190">A list of the cluster head nodes appears.</span><span class="sxs-lookup"><span data-stu-id="fcb91-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="fcb91-191">Select one of the head nodes, and then select **NameNode UI**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>
   
    ![Image with the QuickLinks menu expanded](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)
   
   > [!NOTE]
   > <span data-ttu-id="fcb91-193">If you have a slow internet connection, or the head node is very busy, you may get a wait indicator instead of a menu when you select **Quick Links**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-193">If you have a slow internet connection, or the head node is very busy, you may get a wait indicator instead of a menu when you select **Quick Links**.</span></span> <span data-ttu-id="fcb91-194">If so, wait a minute or two for the data to be received from the server, then try the list again.</span><span class="sxs-lookup"><span data-stu-id="fcb91-194">If so, wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   > 
   > <span data-ttu-id="fcb91-195">If you have a lower resolution monitor, or your browser window is not maximized, some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span><span class="sxs-lookup"><span data-stu-id="fcb91-195">If you have a lower resolution monitor, or your browser window is not maximized, some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="fcb91-196">If so, expand the menu using your mouse, then use the right arrow key to scroll the screen to the right to see the rest of the menu.</span><span class="sxs-lookup"><span data-stu-id="fcb91-196">If so, expand the menu using your mouse, then use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>
   > 
   > 
4. <span data-ttu-id="fcb91-197">A page similar to the following should appear:</span><span class="sxs-lookup"><span data-stu-id="fcb91-197">A page similar to the following should appear:</span></span>
   
    ![Image of the NameNode UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)
   
   > [!NOTE]
   > <span data-ttu-id="fcb91-199">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-199">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="fcb91-200">This is using the internal fully qualified domain name (FQDN) of the node, and is not accessible without using an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="fcb91-200">This is using the internal fully qualified domain name (FQDN) of the node, and is not accessible without using an SSH tunnel.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="fcb91-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="fcb91-201">Next steps</span></span>

<span data-ttu-id="fcb91-202">Now that you have learned how to create and use an SSH tunnel, see the following for information on monitoring and managing your cluster using Ambari:</span><span class="sxs-lookup"><span data-stu-id="fcb91-202">Now that you have learned how to create and use an SSH tunnel, see the following for information on monitoring and managing your cluster using Ambari:</span></span>

* [<span data-ttu-id="fcb91-203">Manage HDInsight clusters by using Ambari</span><span class="sxs-lookup"><span data-stu-id="fcb91-203">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="fcb91-204">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fcb91-204">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>






