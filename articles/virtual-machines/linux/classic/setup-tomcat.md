---
title: Set up Apache Tomcat on a Linux virtual machine | Microsoft Docs
description: Learn how to set up Apache Tomcat7 by using Azure Virtual Machines running Linux.
services: virtual-machines-linux
documentationcenter: ''
author: NingKuang
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: 5f12258e527ed789a9ce177230b19ad361b630db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553231"
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="78fde-103">Set up Tomcat7 on a Linux virtual machine with Azure</span><span class="sxs-lookup"><span data-stu-id="78fde-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="78fde-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by the Apache Software Foundation (ASF).</span><span class="sxs-lookup"><span data-stu-id="78fde-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by the Apache Software Foundation (ASF).</span></span> <span data-ttu-id="78fde-105">Tomcat implements the Java Servlet and the JavaServer Pages (JSP) specifications from Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="78fde-105">Tomcat implements the Java Servlet and the JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="78fde-106">Tomcat provides a pure Java HTTP web server environment in which to run Java code.</span><span class="sxs-lookup"><span data-stu-id="78fde-106">Tomcat provides a pure Java HTTP web server environment in which to run Java code.</span></span> <span data-ttu-id="78fde-107">In the simplest configuration, Tomcat runs in a single operating system process.</span><span class="sxs-lookup"><span data-stu-id="78fde-107">In the simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="78fde-108">This process runs a Java virtual machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="78fde-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="78fde-109">Every HTTP request from a browser to Tomcat is processed as a separate thread in the Tomcat process.</span><span class="sxs-lookup"><span data-stu-id="78fde-109">Every HTTP request from a browser to Tomcat is processed as a separate thread in the Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="78fde-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="78fde-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="78fde-111">This article covers how to use the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="78fde-111">This article covers how to use the classic deployment model.</span></span> <span data-ttu-id="78fde-112">We recommend that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="78fde-112">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="78fde-113">To use a Resource Manager template to deploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="78fde-113">To use a Resource Manager template to deploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="78fde-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span><span class="sxs-lookup"><span data-stu-id="78fde-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="78fde-115">You will learn:</span><span class="sxs-lookup"><span data-stu-id="78fde-115">You will learn:</span></span>  

* <span data-ttu-id="78fde-116">How to create a virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="78fde-116">How to create a virtual machine in Azure.</span></span>
* <span data-ttu-id="78fde-117">How to prepare the virtual machine for Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="78fde-117">How to prepare the virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="78fde-118">How to install Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="78fde-118">How to install Tomcat7.</span></span>

<span data-ttu-id="78fde-119">It is assumed that you already have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="78fde-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="78fde-120">If not, you can sign up for a free trial at [the Azure website](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="78fde-120">If not, you can sign up for a free trial at [the Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="78fde-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="78fde-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="78fde-122">To learn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="78fde-122">To learn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="78fde-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span><span class="sxs-lookup"><span data-stu-id="78fde-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="78fde-124">Phase 1: Create an image</span><span class="sxs-lookup"><span data-stu-id="78fde-124">Phase 1: Create an image</span></span>
<span data-ttu-id="78fde-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span><span class="sxs-lookup"><span data-stu-id="78fde-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="78fde-126">Step 1: Generate an SSH authentication key</span><span class="sxs-lookup"><span data-stu-id="78fde-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="78fde-127">SSH is an important tool for system administrators.</span><span class="sxs-lookup"><span data-stu-id="78fde-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="78fde-128">However, configuring access security based on a human-determined password is not recommended.</span><span class="sxs-lookup"><span data-stu-id="78fde-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="78fde-129">Malicious users can break into your system based on a username and a weak password.</span><span class="sxs-lookup"><span data-stu-id="78fde-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="78fde-130">The good news is that there is a way to leave remote access open and not worry about passwords.</span><span class="sxs-lookup"><span data-stu-id="78fde-130">The good news is that there is a way to leave remote access open and not worry about passwords.</span></span> <span data-ttu-id="78fde-131">This method consists of authentication with asymmetric cryptography.</span><span class="sxs-lookup"><span data-stu-id="78fde-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="78fde-132">The user’s private key is the one that grants the authentication.</span><span class="sxs-lookup"><span data-stu-id="78fde-132">The user’s private key is the one that grants the authentication.</span></span> <span data-ttu-id="78fde-133">You can even lock the user’s account to not allow password authentication.</span><span class="sxs-lookup"><span data-stu-id="78fde-133">You can even lock the user’s account to not allow password authentication.</span></span>

<span data-ttu-id="78fde-134">Another advantage of this method is that you do not need different passwords to sign in to different servers.</span><span class="sxs-lookup"><span data-stu-id="78fde-134">Another advantage of this method is that you do not need different passwords to sign in to different servers.</span></span> <span data-ttu-id="78fde-135">You can authenticate by using the personal private key on all servers, which prevents you from having to remember several passwords.</span><span class="sxs-lookup"><span data-stu-id="78fde-135">You can authenticate by using the personal private key on all servers, which prevents you from having to remember several passwords.</span></span>



<span data-ttu-id="78fde-136">Follow these steps to generate the SSH authentication key.</span><span class="sxs-lookup"><span data-stu-id="78fde-136">Follow these steps to generate the SSH authentication key.</span></span>

1. <span data-ttu-id="78fde-137">Download and install PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="78fde-137">Download and install PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="78fde-138">Run Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="78fde-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="78fde-139">Click **Generate** to generate the keys.</span><span class="sxs-lookup"><span data-stu-id="78fde-139">Click **Generate** to generate the keys.</span></span> <span data-ttu-id="78fde-140">In the process, you can increase randomness by moving the mouse over the blank area in the window.</span><span class="sxs-lookup"><span data-stu-id="78fde-140">In the process, you can increase randomness by moving the mouse over the blank area in the window.</span></span>  
   <span data-ttu-id="78fde-141">![PuTTY Key Generator screenshot that shows the generate new key button][1]</span><span class="sxs-lookup"><span data-stu-id="78fde-141">![PuTTY Key Generator screenshot that shows the generate new key button][1]</span></span>
4. <span data-ttu-id="78fde-142">After the generate process, Puttygen.exe will show your new public key.</span><span class="sxs-lookup"><span data-stu-id="78fde-142">After the generate process, Puttygen.exe will show your new public key.</span></span>  
   ![PuTTY Key Generator screenshot that shows the new public key and the save private key button][2]
5. <span data-ttu-id="78fde-144">Select and copy the public key, and save it in a file named publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="78fde-144">Select and copy the public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="78fde-145">Don’t click **Save public key**, because the saved public key’s file format is different from the public key we want.</span><span class="sxs-lookup"><span data-stu-id="78fde-145">Don’t click **Save public key**, because the saved public key’s file format is different from the public key we want.</span></span>
6. <span data-ttu-id="78fde-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="78fde-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-the-image-in-the-azure-portal"></a><span data-ttu-id="78fde-147">Step 2: Create the image in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="78fde-147">Step 2: Create the image in the Azure portal</span></span>
1. <span data-ttu-id="78fde-148">In the [portal](https://portal.azure.com/), click **New** in the task bar to create an image.</span><span class="sxs-lookup"><span data-stu-id="78fde-148">In the [portal](https://portal.azure.com/), click **New** in the task bar to create an image.</span></span> <span data-ttu-id="78fde-149">Then choose the Linux image that is based on your needs.</span><span class="sxs-lookup"><span data-stu-id="78fde-149">Then choose the Linux image that is based on your needs.</span></span> <span data-ttu-id="78fde-150">The following example uses the Ubuntu 14.04 image.</span><span class="sxs-lookup"><span data-stu-id="78fde-150">The following example uses the Ubuntu 14.04 image.</span></span>
<span data-ttu-id="78fde-151">![Screenshot of the portal that shows the New button][3]</span><span class="sxs-lookup"><span data-stu-id="78fde-151">![Screenshot of the portal that shows the New button][3]</span></span>

2. <span data-ttu-id="78fde-152">For **Host Name**, specify the name for the URL that you and Internet clients will use to access this virtual machine.</span><span class="sxs-lookup"><span data-stu-id="78fde-152">For **Host Name**, specify the name for the URL that you and Internet clients will use to access this virtual machine.</span></span> <span data-ttu-id="78fde-153">Define the last part of the DNS name, for example, tomcatdemo.</span><span class="sxs-lookup"><span data-stu-id="78fde-153">Define the last part of the DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="78fde-154">Azure will then generate the URL as tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="78fde-154">Azure will then generate the URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="78fde-155">For **SSH Authentication Key**, copy the key value from the publicKey.pem file, which contains the public key generated by PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="78fde-155">For **SSH Authentication Key**, copy the key value from the publicKey.pem file, which contains the public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="78fde-156">![SSH Authentication Key box in the portal][4]</span><span class="sxs-lookup"><span data-stu-id="78fde-156">![SSH Authentication Key box in the portal][4]</span></span>

4. <span data-ttu-id="78fde-157">Configure other settings as needed, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="78fde-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="78fde-158">Phase 2: Prepare your virtual machine for Tomcat7</span><span class="sxs-lookup"><span data-stu-id="78fde-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="78fde-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect to your new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="78fde-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect to your new virtual machine.</span></span>

### <a name="step-1-open-the-http-port-to-allow-web-access"></a><span data-ttu-id="78fde-160">Step 1: Open the HTTP port to allow web access</span><span class="sxs-lookup"><span data-stu-id="78fde-160">Step 1: Open the HTTP port to allow web access</span></span>
<span data-ttu-id="78fde-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span><span class="sxs-lookup"><span data-stu-id="78fde-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="78fde-162">The private port is the port that the service is listening to on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="78fde-162">The private port is the port that the service is listening to on the virtual machine.</span></span> <span data-ttu-id="78fde-163">The public port is the port that the Azure cloud service listens to externally for incoming, Internet-based traffic.</span><span class="sxs-lookup"><span data-stu-id="78fde-163">The public port is the port that the Azure cloud service listens to externally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="78fde-164">TCP port 8080 is the default port number that Tomcat uses to listen.</span><span class="sxs-lookup"><span data-stu-id="78fde-164">TCP port 8080 is the default port number that Tomcat uses to listen.</span></span> <span data-ttu-id="78fde-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span><span class="sxs-lookup"><span data-stu-id="78fde-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="78fde-166">In the portal, click **Browse** > **Virtual machines**, and then click the virtual machine that you created.</span><span class="sxs-lookup"><span data-stu-id="78fde-166">In the portal, click **Browse** > **Virtual machines**, and then click the virtual machine that you created.</span></span>  
   <span data-ttu-id="78fde-167">![Screenshot of the Virtual machines directory][5]</span><span class="sxs-lookup"><span data-stu-id="78fde-167">![Screenshot of the Virtual machines directory][5]</span></span>
2. <span data-ttu-id="78fde-168">To add an endpoint to your virtual machine, click the **Endpoints** box.</span><span class="sxs-lookup"><span data-stu-id="78fde-168">To add an endpoint to your virtual machine, click the **Endpoints** box.</span></span>
   <span data-ttu-id="78fde-169">![Screenshot that shows the Endpoints box][6]</span><span class="sxs-lookup"><span data-stu-id="78fde-169">![Screenshot that shows the Endpoints box][6]</span></span>
3. <span data-ttu-id="78fde-170">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="78fde-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="78fde-171">For the endpoint, enter a name for the endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span><span class="sxs-lookup"><span data-stu-id="78fde-171">For the endpoint, enter a name for the endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="78fde-172">If you set it to 80, you don’t need to include the port number in the URL that is used to access Tomcat.</span><span class="sxs-lookup"><span data-stu-id="78fde-172">If you set it to 80, you don’t need to include the port number in the URL that is used to access Tomcat.</span></span> <span data-ttu-id="78fde-173">For example, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="78fde-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="78fde-174">If you set it to another value, such as 81, you need to add the port number to the URL to access Tomcat.</span><span class="sxs-lookup"><span data-stu-id="78fde-174">If you set it to another value, such as 81, you need to add the port number to the URL to access Tomcat.</span></span> <span data-ttu-id="78fde-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="78fde-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="78fde-176">Enter 8080 in **Private Port**.</span><span class="sxs-lookup"><span data-stu-id="78fde-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="78fde-177">By default, Tomcat listens on TCP port 8080.</span><span class="sxs-lookup"><span data-stu-id="78fde-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="78fde-178">If you changed the default listen port of Tomcat, you should update **Private Port** to be the same as the Tomcat listen port.</span><span class="sxs-lookup"><span data-stu-id="78fde-178">If you changed the default listen port of Tomcat, you should update **Private Port** to be the same as the Tomcat listen port.</span></span>  
      <span data-ttu-id="78fde-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span><span class="sxs-lookup"><span data-stu-id="78fde-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="78fde-180">Click **OK** to add the endpoint to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="78fde-180">Click **OK** to add the endpoint to your virtual machine.</span></span>

### <a name="step-2-connect-to-the-image-you-created"></a><span data-ttu-id="78fde-181">Step 2: Connect to the image you created</span><span class="sxs-lookup"><span data-stu-id="78fde-181">Step 2: Connect to the image you created</span></span>
<span data-ttu-id="78fde-182">You can choose any SSH tool to connect to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="78fde-182">You can choose any SSH tool to connect to your virtual machine.</span></span> <span data-ttu-id="78fde-183">In this example, we use PuTTY.</span><span class="sxs-lookup"><span data-stu-id="78fde-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="78fde-184">Get the DNS name of your virtual machine from the portal.</span><span class="sxs-lookup"><span data-stu-id="78fde-184">Get the DNS name of your virtual machine from the portal.</span></span>
    1. <span data-ttu-id="78fde-185">Click **Browse** > **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="78fde-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="78fde-186">Select the name of your virtual machine, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="78fde-186">Select the name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="78fde-187">In the **Properties** tile, look in the **Domain Name** box to get the DNS name.</span><span class="sxs-lookup"><span data-stu-id="78fde-187">In the **Properties** tile, look in the **Domain Name** box to get the DNS name.</span></span>  

2. <span data-ttu-id="78fde-188">Get the port number for SSH connections from the **SSH** box.</span><span class="sxs-lookup"><span data-stu-id="78fde-188">Get the port number for SSH connections from the **SSH** box.</span></span>  
<span data-ttu-id="78fde-189">![Screenshot that shows the SSH connection port number][8]</span><span class="sxs-lookup"><span data-stu-id="78fde-189">![Screenshot that shows the SSH connection port number][8]</span></span>

3. <span data-ttu-id="78fde-190">Download [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="78fde-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="78fde-191">After downloading, click the executable file Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="78fde-191">After downloading, click the executable file Putty.exe.</span></span> <span data-ttu-id="78fde-192">In PuTTY configuration, configure the basic options with the host name and port number that is obtained from the properties of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="78fde-192">In PuTTY configuration, configure the basic options with the host name and port number that is obtained from the properties of your virtual machine.</span></span>   
![Screenshot that shows the PuTTY configuration host name and port options][9]

5. <span data-ttu-id="78fde-194">In the left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** to specify the location of the privateKey.ppk file.</span><span class="sxs-lookup"><span data-stu-id="78fde-194">In the left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** to specify the location of the privateKey.ppk file.</span></span> <span data-ttu-id="78fde-195">The privateKey.ppk file contains the private key that is generated by PuTTYgen earlier in the "Phase 1: Create an image" section of this article.</span><span class="sxs-lookup"><span data-stu-id="78fde-195">The privateKey.ppk file contains the private key that is generated by PuTTYgen earlier in the "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="78fde-196">![Screenshot that shows the Connection directory hierarchy and Browse button][10]</span><span class="sxs-lookup"><span data-stu-id="78fde-196">![Screenshot that shows the Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="78fde-197">Click **Open**.</span><span class="sxs-lookup"><span data-stu-id="78fde-197">Click **Open**.</span></span> <span data-ttu-id="78fde-198">You might be alerted by a message box.</span><span class="sxs-lookup"><span data-stu-id="78fde-198">You might be alerted by a message box.</span></span> <span data-ttu-id="78fde-199">If you have configured the DNS name and port number correctly, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="78fde-199">If you have configured the DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="78fde-200">![Screenshot that shows the notification][11]</span><span class="sxs-lookup"><span data-stu-id="78fde-200">![Screenshot that shows the notification][11]</span></span>

7. <span data-ttu-id="78fde-201">You are prompted to enter your username.</span><span class="sxs-lookup"><span data-stu-id="78fde-201">You are prompted to enter your username.</span></span>  
![Screenshot that shows where to enter username][12]

8. <span data-ttu-id="78fde-203">Enter the username that you used to create the virtual machine in the "Phase 1: Create an image" section earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="78fde-203">Enter the username that you used to create the virtual machine in the "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="78fde-204">You will see something like the following:</span><span class="sxs-lookup"><span data-stu-id="78fde-204">You will see something like the following:</span></span>  
![Screenshot that shows the authentication confirmation][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="78fde-206">Phase 3: Install software</span><span class="sxs-lookup"><span data-stu-id="78fde-206">Phase 3: Install software</span></span>
<span data-ttu-id="78fde-207">In this phase, you install the Java runtime environment, Tomcat7, and other Tomcat7 components.</span><span class="sxs-lookup"><span data-stu-id="78fde-207">In this phase, you install the Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="78fde-208">Java runtime environment</span><span class="sxs-lookup"><span data-stu-id="78fde-208">Java runtime environment</span></span>
<span data-ttu-id="78fde-209">Tomcat is written in Java.</span><span class="sxs-lookup"><span data-stu-id="78fde-209">Tomcat is written in Java.</span></span> <span data-ttu-id="78fde-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="78fde-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="78fde-211">You can choose the one you want.</span><span class="sxs-lookup"><span data-stu-id="78fde-211">You can choose the one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="78fde-212">Both JDKs have almost the same code for the classes in the Java API, but the code for the virtual machine is different.</span><span class="sxs-lookup"><span data-stu-id="78fde-212">Both JDKs have almost the same code for the classes in the Java API, but the code for the virtual machine is different.</span></span> <span data-ttu-id="78fde-213">OpenJDK tends to use open libraries, while Oracle JDK tends to use closed ones.</span><span class="sxs-lookup"><span data-stu-id="78fde-213">OpenJDK tends to use open libraries, while Oracle JDK tends to use closed ones.</span></span> <span data-ttu-id="78fde-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="78fde-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="78fde-215">Install OpenJDK</span><span class="sxs-lookup"><span data-stu-id="78fde-215">Install OpenJDK</span></span>  

<span data-ttu-id="78fde-216">Use the following command to download OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="78fde-216">Use the following command to download OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="78fde-217">To create a directory to contain the JDK files:</span><span class="sxs-lookup"><span data-stu-id="78fde-217">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="78fde-218">To extract the JDK files into the /usr/lib/jvm/ directory:</span><span class="sxs-lookup"><span data-stu-id="78fde-218">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="78fde-219">Install Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="78fde-219">Install Oracle JDK</span></span>


<span data-ttu-id="78fde-220">Use the following command to download Oracle JDK from the Oracle website.</span><span class="sxs-lookup"><span data-stu-id="78fde-220">Use the following command to download Oracle JDK from the Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="78fde-221">To create a directory to contain the JDK files:</span><span class="sxs-lookup"><span data-stu-id="78fde-221">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="78fde-222">To extract the JDK files into the /usr/lib/jvm/ directory:</span><span class="sxs-lookup"><span data-stu-id="78fde-222">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="78fde-223">To set Oracle JDK as the default Java virtual machine:</span><span class="sxs-lookup"><span data-stu-id="78fde-223">To set Oracle JDK as the default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="78fde-224">Confirm that Java installation is successful</span><span class="sxs-lookup"><span data-stu-id="78fde-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="78fde-225">You can use a command like the following to test if the Java runtime environment is installed correctly:</span><span class="sxs-lookup"><span data-stu-id="78fde-225">You can use a command like the following to test if the Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="78fde-226">If you installed OpenJDK, you should see a message like the following: ![Successful OpenJDK installation message][14]</span><span class="sxs-lookup"><span data-stu-id="78fde-226">If you installed OpenJDK, you should see a message like the following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="78fde-227">If you installed Oracle JDK, you should see a message like the following: ![Successful Oracle JDK installation message][15]</span><span class="sxs-lookup"><span data-stu-id="78fde-227">If you installed Oracle JDK, you should see a message like the following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="78fde-228">Install Tomcat7</span><span class="sxs-lookup"><span data-stu-id="78fde-228">Install Tomcat7</span></span>
<span data-ttu-id="78fde-229">Use the following command to install Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="78fde-229">Use the following command to install Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="78fde-230">If you are not using Tomcat7, use the appropriate variation of this command.</span><span class="sxs-lookup"><span data-stu-id="78fde-230">If you are not using Tomcat7, use the appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="78fde-231">Confirm that Tomcat7 installation is successful</span><span class="sxs-lookup"><span data-stu-id="78fde-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="78fde-232">To check if Tomcat7 is successfully installed, browse to your Tomcat server’s DNS name.</span><span class="sxs-lookup"><span data-stu-id="78fde-232">To check if Tomcat7 is successfully installed, browse to your Tomcat server’s DNS name.</span></span> <span data-ttu-id="78fde-233">In this article, the example URL is http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="78fde-233">In this article, the example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="78fde-234">If you see a message like the following, Tomcat7 is installed correctly.</span><span class="sxs-lookup"><span data-stu-id="78fde-234">If you see a message like the following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="78fde-235">![Successful Tomcat7 installation message][16]</span><span class="sxs-lookup"><span data-stu-id="78fde-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="78fde-236">Install other Tomcat7 components</span><span class="sxs-lookup"><span data-stu-id="78fde-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="78fde-237">There are other optional Tomcat components that you can install.</span><span class="sxs-lookup"><span data-stu-id="78fde-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="78fde-238">Use the **sudo apt-cache search tomcat7** command to see all of the available components.</span><span class="sxs-lookup"><span data-stu-id="78fde-238">Use the **sudo apt-cache search tomcat7** command to see all of the available components.</span></span> <span data-ttu-id="78fde-239">Use the following commands to install some useful components.</span><span class="sxs-lookup"><span data-stu-id="78fde-239">Use the following commands to install some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools to create user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="78fde-240">Phase 4: Configure Tomcat7</span><span class="sxs-lookup"><span data-stu-id="78fde-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="78fde-241">In this phase, you administer Tomcat.</span><span class="sxs-lookup"><span data-stu-id="78fde-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="78fde-242">Start and stop Tomcat7</span><span class="sxs-lookup"><span data-stu-id="78fde-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="78fde-243">The Tomcat7 server automatically starts when you install it.</span><span class="sxs-lookup"><span data-stu-id="78fde-243">The Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="78fde-244">You can also start it with the following command:</span><span class="sxs-lookup"><span data-stu-id="78fde-244">You can also start it with the following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="78fde-245">To stop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="78fde-245">To stop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="78fde-246">To view the status of Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="78fde-246">To view the status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="78fde-247">To restart Tomcat services:</span><span class="sxs-lookup"><span data-stu-id="78fde-247">To restart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="78fde-248">Tomcat7 administration</span><span class="sxs-lookup"><span data-stu-id="78fde-248">Tomcat7 administration</span></span>
<span data-ttu-id="78fde-249">You can edit the Tomcat user configuration file to set up your admin credentials.</span><span class="sxs-lookup"><span data-stu-id="78fde-249">You can edit the Tomcat user configuration file to set up your admin credentials.</span></span> <span data-ttu-id="78fde-250">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="78fde-250">Use the following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="78fde-251">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="78fde-251">Here is an example:</span></span>  
![Screenshot that shows the sudo vi command output][17]  

> [!NOTE]
> <span data-ttu-id="78fde-253">Create a strong password for the admin username.</span><span class="sxs-lookup"><span data-stu-id="78fde-253">Create a strong password for the admin username.</span></span>  

<span data-ttu-id="78fde-254">After editing this file, you should restart Tomcat7 services with the following command to ensure that the changes take effect:</span><span class="sxs-lookup"><span data-stu-id="78fde-254">After editing this file, you should restart Tomcat7 services with the following command to ensure that the changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="78fde-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as the URL.</span><span class="sxs-lookup"><span data-stu-id="78fde-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as the URL.</span></span> <span data-ttu-id="78fde-256">For the example in this article, the URL is http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="78fde-256">For the example in this article, the URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="78fde-257">After connecting, you should see something similar to the following:</span><span class="sxs-lookup"><span data-stu-id="78fde-257">After connecting, you should see something similar to the following:</span></span>  
![Screenshot of the Tomcat Web Application Manager][18]

## <a name="common-issues"></a><span data-ttu-id="78fde-259">Common issues</span><span class="sxs-lookup"><span data-stu-id="78fde-259">Common issues</span></span>
### <a name="cant-access-the-virtual-machine-with-tomcat-and-moodle-from-the-internet"></a><span data-ttu-id="78fde-260">Can't access the virtual machine with Tomcat and Moodle from the Internet</span><span class="sxs-lookup"><span data-stu-id="78fde-260">Can't access the virtual machine with Tomcat and Moodle from the Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="78fde-261">Symptom</span><span class="sxs-lookup"><span data-stu-id="78fde-261">Symptom</span></span>  
  <span data-ttu-id="78fde-262">Tomcat is running but you can’t see the Tomcat default page with your browser.</span><span class="sxs-lookup"><span data-stu-id="78fde-262">Tomcat is running but you can’t see the Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="78fde-263">Possible root cause</span><span class="sxs-lookup"><span data-stu-id="78fde-263">Possible root cause</span></span>   

  * <span data-ttu-id="78fde-264">The Tomcat listen port is not the same as the private port of your virtual machine's endpoint for Tomcat traffic.</span><span class="sxs-lookup"><span data-stu-id="78fde-264">The Tomcat listen port is not the same as the private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="78fde-265">Check your public port and private port endpoint settings and make sure the private port is the same as the Tomcat listen port.</span><span class="sxs-lookup"><span data-stu-id="78fde-265">Check your public port and private port endpoint settings and make sure the private port is the same as the Tomcat listen port.</span></span> <span data-ttu-id="78fde-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="78fde-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="78fde-267">To determine the Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span><span class="sxs-lookup"><span data-stu-id="78fde-267">To determine the Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="78fde-268">By default, the Tomcat listen port is 8080.</span><span class="sxs-lookup"><span data-stu-id="78fde-268">By default, the Tomcat listen port is 8080.</span></span> <span data-ttu-id="78fde-269">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="78fde-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="78fde-270">If you are using a virtual machine like Debian or Ubuntu and you want to change the default port of Tomcat Listen (for example 8081), you should also open the port for the operating system.</span><span class="sxs-lookup"><span data-stu-id="78fde-270">If you are using a virtual machine like Debian or Ubuntu and you want to change the default port of Tomcat Listen (for example 8081), you should also open the port for the operating system.</span></span> <span data-ttu-id="78fde-271">First, open the profile:</span><span class="sxs-lookup"><span data-stu-id="78fde-271">First, open the profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="78fde-272">Then uncomment the last line and change “no” to “yes”.</span><span class="sxs-lookup"><span data-stu-id="78fde-272">Then uncomment the last line and change “no” to “yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="78fde-273">The firewall has disabled the listen port of Tomcat.</span><span class="sxs-lookup"><span data-stu-id="78fde-273">The firewall has disabled the listen port of Tomcat.</span></span>

     <span data-ttu-id="78fde-274">You can only see the Tomcat default page from the local host.</span><span class="sxs-lookup"><span data-stu-id="78fde-274">You can only see the Tomcat default page from the local host.</span></span> <span data-ttu-id="78fde-275">The problem is most likely that the port, which is listened to by Tomcat, is blocked by the firewall.</span><span class="sxs-lookup"><span data-stu-id="78fde-275">The problem is most likely that the port, which is listened to by Tomcat, is blocked by the firewall.</span></span> <span data-ttu-id="78fde-276">You can use the w3m tool to browse the webpage.</span><span class="sxs-lookup"><span data-stu-id="78fde-276">You can use the w3m tool to browse the webpage.</span></span> <span data-ttu-id="78fde-277">The following commands install w3m and browse to the Tomcat default page:</span><span class="sxs-lookup"><span data-stu-id="78fde-277">The following commands install w3m and browse to the Tomcat default page:</span></span>  


        <span data-ttu-id="78fde-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="78fde-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="78fde-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="78fde-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="78fde-280">Solution</span><span class="sxs-lookup"><span data-stu-id="78fde-280">Solution</span></span>

  * <span data-ttu-id="78fde-281">If the Tomcat listen port is not the same as the private port of the endpoint for traffic to the virtual machine, you need change the private port to be the same as the Tomcat listen port.</span><span class="sxs-lookup"><span data-stu-id="78fde-281">If the Tomcat listen port is not the same as the private port of the endpoint for traffic to the virtual machine, you need change the private port to be the same as the Tomcat listen port.</span></span>   
  2. <span data-ttu-id="78fde-282">If the issue is caused by firewall/iptables, add the following lines to /etc/sysconfig/iptables.</span><span class="sxs-lookup"><span data-stu-id="78fde-282">If the issue is caused by firewall/iptables, add the following lines to /etc/sysconfig/iptables.</span></span> <span data-ttu-id="78fde-283">The second line is only needed for https traffic:</span><span class="sxs-lookup"><span data-stu-id="78fde-283">The second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="78fde-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="78fde-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="78fde-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="78fde-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="78fde-286">Make sure the previous lines are positioned above any lines that would globally restrict access, such as the following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span><span class="sxs-lookup"><span data-stu-id="78fde-286">Make sure the previous lines are positioned above any lines that would globally restrict access, such as the following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="78fde-287">To reload the iptables, run the following command:</span><span class="sxs-lookup"><span data-stu-id="78fde-287">To reload the iptables, run the following command:</span></span>

    service iptables restart

<span data-ttu-id="78fde-288">This has been tested on CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="78fde-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-to-varlibtomcat7webapps"></a><span data-ttu-id="78fde-289">Permission denied when you upload project files to /var/lib/tomcat7/webapps/</span><span class="sxs-lookup"><span data-stu-id="78fde-289">Permission denied when you upload project files to /var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="78fde-290">Symptom</span><span class="sxs-lookup"><span data-stu-id="78fde-290">Symptom</span></span>
  <span data-ttu-id="78fde-291">When you use an SFTP client (such as FileZilla) to connect to your virtual machine and navigate to /var/lib/tomcat7/webapps/ to publish your site, you get an error message similar to the following:</span><span class="sxs-lookup"><span data-stu-id="78fde-291">When you use an SFTP client (such as FileZilla) to connect to your virtual machine and navigate to /var/lib/tomcat7/webapps/ to publish your site, you get an error message similar to the following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="78fde-292">Possible root cause</span><span class="sxs-lookup"><span data-stu-id="78fde-292">Possible root cause</span></span>
  <span data-ttu-id="78fde-293">You have no permissions to access the /var/lib/tomcat7/webapps folder.</span><span class="sxs-lookup"><span data-stu-id="78fde-293">You have no permissions to access the /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="78fde-294">Solution</span><span class="sxs-lookup"><span data-stu-id="78fde-294">Solution</span></span>  
  <span data-ttu-id="78fde-295">You need to get permission from the root account.</span><span class="sxs-lookup"><span data-stu-id="78fde-295">You need to get permission from the root account.</span></span> <span data-ttu-id="78fde-296">You can change the ownership of that folder from root to the username you used when you provisioned the machine.</span><span class="sxs-lookup"><span data-stu-id="78fde-296">You can change the ownership of that folder from root to the username you used when you provisioned the machine.</span></span> <span data-ttu-id="78fde-297">Here is an example with the azureuser account name:</span><span class="sxs-lookup"><span data-stu-id="78fde-297">Here is an example with the azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="78fde-298">Use the -R option to apply the permissions for all files inside of a directory too.</span><span class="sxs-lookup"><span data-stu-id="78fde-298">Use the -R option to apply the permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="78fde-299">This command also works for directories.</span><span class="sxs-lookup"><span data-stu-id="78fde-299">This command also works for directories.</span></span> <span data-ttu-id="78fde-300">The -R option changes the permissions for all files and directories inside the directory.</span><span class="sxs-lookup"><span data-stu-id="78fde-300">The -R option changes the permissions for all files and directories inside the directory.</span></span> <span data-ttu-id="78fde-301">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="78fde-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="78fde-302">This command changes ownership (both user and group) for all files and directories that are inside the directory.</span><span class="sxs-lookup"><span data-stu-id="78fde-302">This command changes ownership (both user and group) for all files and directories that are inside the directory.</span></span>  

  <span data-ttu-id="78fde-303">The following command only changes the permission of the folder directory.</span><span class="sxs-lookup"><span data-stu-id="78fde-303">The following command only changes the permission of the folder directory.</span></span> <span data-ttu-id="78fde-304">The files and folders inside the directory are not changed.</span><span class="sxs-lookup"><span data-stu-id="78fde-304">The files and folders inside the directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png


















