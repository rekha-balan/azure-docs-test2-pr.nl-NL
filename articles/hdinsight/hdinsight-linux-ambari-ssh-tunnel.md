---
title: Use SSH tunneling to access Azure HDInsight
description: Learn how to use an SSH tunnel to securely browse web resources hosted on your Linux-based HDInsight nodes.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/30/2018
ms.author: jasonh
ms.openlocfilehash: 0722a366c374bd69fd9cf97279416a60d7133428
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44770412"
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="436c8-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span><span class="sxs-lookup"><span data-stu-id="436c8-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="436c8-104">HDInsight clusters provide access to the Ambari web UI over the Internet, but some features require an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="436c8-104">HDInsight clusters provide access to the Ambari web UI over the Internet, but some features require an SSH tunnel.</span></span> <span data-ttu-id="436c8-105">For example, the web UI for the Oozie service cannot be accessed over the internet without an SSh tunnel.</span><span class="sxs-lookup"><span data-stu-id="436c8-105">For example, the web UI for the Oozie service cannot be accessed over the internet without an SSh tunnel.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="436c8-106">Why use an SSH tunnel</span><span class="sxs-lookup"><span data-stu-id="436c8-106">Why use an SSH tunnel</span></span>

<span data-ttu-id="436c8-107">Several of the menus in Ambari only work through an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="436c8-107">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="436c8-108">These menus rely on web sites and services running on other node types, such as worker nodes.</span><span class="sxs-lookup"><span data-stu-id="436c8-108">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span>

<span data-ttu-id="436c8-109">The following Web UIs require an SSH tunnel:</span><span class="sxs-lookup"><span data-stu-id="436c8-109">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="436c8-110">JobHistory</span><span class="sxs-lookup"><span data-stu-id="436c8-110">JobHistory</span></span>
* <span data-ttu-id="436c8-111">NameNode</span><span class="sxs-lookup"><span data-stu-id="436c8-111">NameNode</span></span>
* <span data-ttu-id="436c8-112">Thread Stacks</span><span class="sxs-lookup"><span data-stu-id="436c8-112">Thread Stacks</span></span>
* <span data-ttu-id="436c8-113">Oozie web UI</span><span class="sxs-lookup"><span data-stu-id="436c8-113">Oozie web UI</span></span>
* <span data-ttu-id="436c8-114">HBase Master and Logs UI</span><span class="sxs-lookup"><span data-stu-id="436c8-114">HBase Master and Logs UI</span></span>

<span data-ttu-id="436c8-115">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web service require an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="436c8-115">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web service require an SSH tunnel.</span></span> <span data-ttu-id="436c8-116">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span><span class="sxs-lookup"><span data-stu-id="436c8-116">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="436c8-117">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span><span class="sxs-lookup"><span data-stu-id="436c8-117">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="436c8-118">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="436c8-118">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="436c8-119">What is an SSH tunnel</span><span class="sxs-lookup"><span data-stu-id="436c8-119">What is an SSH tunnel</span></span>

<span data-ttu-id="436c8-120">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) connects a port on your local machine to a head node on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="436c8-120">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) connects a port on your local machine to a head node on HDInsight.</span></span> <span data-ttu-id="436c8-121">Traffic sent to the local port is routed through an SSH connection to the head node.</span><span class="sxs-lookup"><span data-stu-id="436c8-121">Traffic sent to the local port is routed through an SSH connection to the head node.</span></span> <span data-ttu-id="436c8-122">The request is resolved as if it originated on the head node.</span><span class="sxs-lookup"><span data-stu-id="436c8-122">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="436c8-123">The response is then routed back through the tunnel to your workstation.</span><span class="sxs-lookup"><span data-stu-id="436c8-123">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="436c8-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="436c8-124">Prerequisites</span></span>

* <span data-ttu-id="436c8-125">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="436c8-125">An SSH client.</span></span> <span data-ttu-id="436c8-126">Most operating systems provide an SSH client through the `ssh` command.</span><span class="sxs-lookup"><span data-stu-id="436c8-126">Most operating systems provide an SSH client through the `ssh` command.</span></span> <span data-ttu-id="436c8-127">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="436c8-127">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="436c8-128">A web browser that can be configured to use a SOCKS5 proxy.</span><span class="sxs-lookup"><span data-stu-id="436c8-128">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="436c8-129">The SOCKS proxy support built into Windows Internet settings does not support SOCKS5, and does not work with the steps in this document.</span><span class="sxs-lookup"><span data-stu-id="436c8-129">The SOCKS proxy support built into Windows Internet settings does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="436c8-130">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span><span class="sxs-lookup"><span data-stu-id="436c8-130">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="436c8-131">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="436c8-131">Microsoft Edge</span></span>
    > * <span data-ttu-id="436c8-132">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="436c8-132">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="436c8-133">Google Chrome also relies on the Windows proxy settings.</span><span class="sxs-lookup"><span data-stu-id="436c8-133">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="436c8-134">However, you can install extensions that support SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="436c8-134">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="436c8-135">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="436c8-135">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <a name="usessh"></a><span data-ttu-id="436c8-136">Create a tunnel using the SSH command</span><span class="sxs-lookup"><span data-stu-id="436c8-136">Create a tunnel using the SSH command</span></span>

<span data-ttu-id="436c8-137">Use the following command to create an SSH tunnel using the `ssh` command.</span><span class="sxs-lookup"><span data-stu-id="436c8-137">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="436c8-138">Replace **sshuser** with an SSH user for your HDInsight cluster, and replace **clustername** with the name of your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="436c8-138">Replace **sshuser** with an SSH user for your HDInsight cluster, and replace **clustername** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 sshuser@clustername-ssh.azurehdinsight.net
```

<span data-ttu-id="436c8-139">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span><span class="sxs-lookup"><span data-stu-id="436c8-139">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="436c8-140">The options are:</span><span class="sxs-lookup"><span data-stu-id="436c8-140">The options are:</span></span>

* <span data-ttu-id="436c8-141">**D 9876** - The local port that routes traffic through the tunnel.</span><span class="sxs-lookup"><span data-stu-id="436c8-141">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="436c8-142">**C** - Compress all data, because web traffic is mostly text.</span><span class="sxs-lookup"><span data-stu-id="436c8-142">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="436c8-143">**2** - Force SSH to try protocol version 2 only.</span><span class="sxs-lookup"><span data-stu-id="436c8-143">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="436c8-144">**q** - Quiet mode.</span><span class="sxs-lookup"><span data-stu-id="436c8-144">**q** - Quiet mode.</span></span>
* <span data-ttu-id="436c8-145">**T** - Disable pseudo-tty allocation, since you are just forwarding a port.</span><span class="sxs-lookup"><span data-stu-id="436c8-145">**T** - Disable pseudo-tty allocation, since you are just forwarding a port.</span></span>
* <span data-ttu-id="436c8-146">**n** - Prevent reading of STDIN, since you are just forwarding a port.</span><span class="sxs-lookup"><span data-stu-id="436c8-146">**n** - Prevent reading of STDIN, since you are just forwarding a port.</span></span>
* <span data-ttu-id="436c8-147">**N** - Do not execute a remote command, since you are just forwarding a port.</span><span class="sxs-lookup"><span data-stu-id="436c8-147">**N** - Do not execute a remote command, since you are just forwarding a port.</span></span>
* <span data-ttu-id="436c8-148">**f** - Run in the background.</span><span class="sxs-lookup"><span data-stu-id="436c8-148">**f** - Run in the background.</span></span>

<span data-ttu-id="436c8-149">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="436c8-149">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <a name="useputty"></a><span data-ttu-id="436c8-150">Create a tunnel using PuTTY</span><span class="sxs-lookup"><span data-stu-id="436c8-150">Create a tunnel using PuTTY</span></span>

<span data-ttu-id="436c8-151">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span><span class="sxs-lookup"><span data-stu-id="436c8-151">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="436c8-152">Use the following steps to create an SSH tunnel using PuTTY:</span><span class="sxs-lookup"><span data-stu-id="436c8-152">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="436c8-153">Open PuTTY, and enter your connection information.</span><span class="sxs-lookup"><span data-stu-id="436c8-153">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="436c8-154">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="436c8-154">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="436c8-155">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="436c8-155">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="436c8-156">Provide the following information on the **Options controlling SSH port forwarding** form:</span><span class="sxs-lookup"><span data-stu-id="436c8-156">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="436c8-157">**Source port** - The port on the client that you wish to forward.</span><span class="sxs-lookup"><span data-stu-id="436c8-157">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="436c8-158">For example, **9876**.</span><span class="sxs-lookup"><span data-stu-id="436c8-158">For example, **9876**.</span></span>

   * <span data-ttu-id="436c8-159">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="436c8-159">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="436c8-160">For example, **mycluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="436c8-160">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="436c8-161">**Dynamic** - Enables dynamic SOCKS proxy routing.</span><span class="sxs-lookup"><span data-stu-id="436c8-161">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![image of tunneling options](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="436c8-163">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span><span class="sxs-lookup"><span data-stu-id="436c8-163">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="436c8-164">When prompted, log in to the server.</span><span class="sxs-lookup"><span data-stu-id="436c8-164">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="436c8-165">Use the tunnel from your browser</span><span class="sxs-lookup"><span data-stu-id="436c8-165">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="436c8-166">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span><span class="sxs-lookup"><span data-stu-id="436c8-166">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="436c8-167">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span><span class="sxs-lookup"><span data-stu-id="436c8-167">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="436c8-168">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="436c8-168">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="436c8-169">Here's what the Firefox settings look like.</span><span class="sxs-lookup"><span data-stu-id="436c8-169">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="436c8-170">If you used a different port than 9876, change the port to the one you used:</span><span class="sxs-lookup"><span data-stu-id="436c8-170">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![image of Firefox settings](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="436c8-172">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="436c8-172">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="436c8-173">This setting resolves DNS using the head node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="436c8-173">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="436c8-174">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="436c8-174">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="436c8-175">The IP returned should be one used by the Microsoft Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="436c8-175">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="436c8-176">Verify with Ambari web UI</span><span class="sxs-lookup"><span data-stu-id="436c8-176">Verify with Ambari web UI</span></span>

<span data-ttu-id="436c8-177">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span><span class="sxs-lookup"><span data-stu-id="436c8-177">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="436c8-178">In your browser, go to http://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="436c8-178">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="436c8-179">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the head node that Ambari is running on.</span><span class="sxs-lookup"><span data-stu-id="436c8-179">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the head node that Ambari is running on.</span></span> <span data-ttu-id="436c8-180">When prompted, enter the admin user name (admin) and password for your cluster.</span><span class="sxs-lookup"><span data-stu-id="436c8-180">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="436c8-181">You may be prompted a second time by the Ambari web UI.</span><span class="sxs-lookup"><span data-stu-id="436c8-181">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="436c8-182">If so, reenter the information.</span><span class="sxs-lookup"><span data-stu-id="436c8-182">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="436c8-183">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span><span class="sxs-lookup"><span data-stu-id="436c8-183">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="436c8-184">Communication is secured using the SSH tunnel instead of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="436c8-184">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="436c8-185">To connect over the internet using HTTPS, use https://clustername.azurehdinsight.net, where **clustername** is the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="436c8-185">To connect over the internet using HTTPS, use https://clustername.azurehdinsight.net, where **clustername** is the name of the cluster.</span></span>

2. <span data-ttu-id="436c8-186">From the Ambari Web UI, select HDFS from the list on the left of the page.</span><span class="sxs-lookup"><span data-stu-id="436c8-186">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Image with HDFS selected](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="436c8-188">When the HDFS service information is displayed, select **Quick Links**.</span><span class="sxs-lookup"><span data-stu-id="436c8-188">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="436c8-189">A list of the cluster head nodes appears.</span><span class="sxs-lookup"><span data-stu-id="436c8-189">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="436c8-190">Select one of the head nodes, and then select **NameNode UI**.</span><span class="sxs-lookup"><span data-stu-id="436c8-190">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Image with the QuickLinks menu expanded](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="436c8-192">When you select __Quick Links__, you may get a wait indicator.</span><span class="sxs-lookup"><span data-stu-id="436c8-192">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="436c8-193">This condition can occur if you have a slow internet connection.</span><span class="sxs-lookup"><span data-stu-id="436c8-193">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="436c8-194">Wait a minute or two for the data to be received from the server, then try the list again.</span><span class="sxs-lookup"><span data-stu-id="436c8-194">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="436c8-195">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span><span class="sxs-lookup"><span data-stu-id="436c8-195">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="436c8-196">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span><span class="sxs-lookup"><span data-stu-id="436c8-196">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="436c8-197">A page similar to the following image is displayed:</span><span class="sxs-lookup"><span data-stu-id="436c8-197">A page similar to the following image is displayed:</span></span>

    ![Image of the NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="436c8-199">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="436c8-199">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="436c8-200">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="436c8-200">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="436c8-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="436c8-201">Next steps</span></span>

<span data-ttu-id="436c8-202">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span><span class="sxs-lookup"><span data-stu-id="436c8-202">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="436c8-203">Manage HDInsight clusters by using Ambari</span><span class="sxs-lookup"><span data-stu-id="436c8-203">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="436c8-204">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="436c8-204">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

