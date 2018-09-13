---
title: Use Apache Phoenix and SQuirreL with Windows-based Azure HDInsight | Microsoft Docs
description: Learn how to use Apache Phoenix in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/09/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 5367edf90b4e13ce506bae0d2bc6264537bcbf49
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551288"
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="e979f-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e979f-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="e979f-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e979f-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span></span> <span data-ttu-id="e979f-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="e979f-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="e979f-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="e979f-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="e979f-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e979f-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="e979f-108">The steps in this document only work for Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="e979f-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="e979f-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="e979f-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="e979f-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="e979f-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e979f-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="e979f-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span> <span data-ttu-id="e979f-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e979f-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="e979f-113">Use SQLLine</span><span class="sxs-lookup"><span data-stu-id="e979f-113">Use SQLLine</span></span>
<span data-ttu-id="e979f-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span><span class="sxs-lookup"><span data-stu-id="e979f-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e979f-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e979f-115">Prerequisites</span></span>
<span data-ttu-id="e979f-116">Before you can use SQLLine, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="e979f-116">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="e979f-117">**A HBase cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e979f-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="e979f-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="e979f-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="e979f-119">**Connect to the HBase cluster via the remote desktop protocol**.</span><span class="sxs-lookup"><span data-stu-id="e979f-119">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="e979f-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="e979f-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="e979f-121">**To find out the host name**</span><span class="sxs-lookup"><span data-stu-id="e979f-121">**To find out the host name**</span></span>

1. <span data-ttu-id="e979f-122">Open **Hadoop Command Line** from the desktop.</span><span class="sxs-lookup"><span data-stu-id="e979f-122">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="e979f-123">Run the following command to get the DNS suffix:</span><span class="sxs-lookup"><span data-stu-id="e979f-123">Run the following command to get the DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="e979f-124">Write down **Connection-specific DNS Suffix**.</span><span class="sxs-lookup"><span data-stu-id="e979f-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="e979f-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="e979f-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="e979f-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span><span class="sxs-lookup"><span data-stu-id="e979f-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span></span> <span data-ttu-id="e979f-127">Each HDInsight cluster has 3 Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="e979f-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="e979f-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="e979f-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="e979f-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="e979f-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="e979f-130">**To use SQLLine**</span><span class="sxs-lookup"><span data-stu-id="e979f-130">**To use SQLLine**</span></span>

1. <span data-ttu-id="e979f-131">Open **Hadoop Command Line** from the desktop.</span><span class="sxs-lookup"><span data-stu-id="e979f-131">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="e979f-132">Run the following commands to open SQLLine:</span><span class="sxs-lookup"><span data-stu-id="e979f-132">Run the following commands to open SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [The FQDN of one of the Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="e979f-134">The commands used in the sample:</span><span class="sxs-lookup"><span data-stu-id="e979f-134">The commands used in the sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="e979f-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="e979f-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="e979f-136">Use SQuirreL</span><span class="sxs-lookup"><span data-stu-id="e979f-136">Use SQuirreL</span></span>
<span data-ttu-id="e979f-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e979f-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span></span>

<span data-ttu-id="e979f-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span><span class="sxs-lookup"><span data-stu-id="e979f-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e979f-139">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e979f-139">Prerequisites</span></span>
<span data-ttu-id="e979f-140">Before following the procedures, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="e979f-140">Before following the procedures, you must have the following:</span></span>

* <span data-ttu-id="e979f-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e979f-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="e979f-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="e979f-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="e979f-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span><span class="sxs-lookup"><span data-stu-id="e979f-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="e979f-144">To get it, RDP into the cluster, and then run IPConfig.</span><span class="sxs-lookup"><span data-stu-id="e979f-144">To get it, RDP into the cluster, and then run IPConfig.</span></span>  <span data-ttu-id="e979f-145">The DNS suffix is similar to:</span><span class="sxs-lookup"><span data-stu-id="e979f-145">The DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="e979f-146">Download and install [Microsoft Visual Studio Express 2013 for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span><span class="sxs-lookup"><span data-stu-id="e979f-146">Download and install [Microsoft Visual Studio Express 2013 for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="e979f-147">You will need makecert from the package to create your certificate.</span><span class="sxs-lookup"><span data-stu-id="e979f-147">You will need makecert from the package to create your certificate.</span></span>  
* <span data-ttu-id="e979f-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span><span class="sxs-lookup"><span data-stu-id="e979f-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="e979f-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span><span class="sxs-lookup"><span data-stu-id="e979f-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-to-the-azure-virtual-network"></a><span data-ttu-id="e979f-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="e979f-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span></span>
<span data-ttu-id="e979f-151">There are 3 steps involved configuring a point-to-site VPN connection:</span><span class="sxs-lookup"><span data-stu-id="e979f-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="e979f-152">Configure a virtual network and a dynamic routing gateway</span><span class="sxs-lookup"><span data-stu-id="e979f-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="e979f-153">Create your certificates</span><span class="sxs-lookup"><span data-stu-id="e979f-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="e979f-154">Configure your VPN client</span><span class="sxs-lookup"><span data-stu-id="e979f-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="e979f-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="e979f-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="e979f-156">Configure a virtual network and a dynamic routing gateway</span><span class="sxs-lookup"><span data-stu-id="e979f-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="e979f-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span><span class="sxs-lookup"><span data-stu-id="e979f-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span></span> <span data-ttu-id="e979f-158">The next step is to configure a point-to-site connection.</span><span class="sxs-lookup"><span data-stu-id="e979f-158">The next step is to configure a point-to-site connection.</span></span>

<span data-ttu-id="e979f-159">**To configure the point-to-site connectivity**</span><span class="sxs-lookup"><span data-stu-id="e979f-159">**To configure the point-to-site connectivity**</span></span>

1. <span data-ttu-id="e979f-160">Sign in to the [Azure Classic Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="e979f-160">Sign in to the [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="e979f-161">On the left, click **NETWORKS**.</span><span class="sxs-lookup"><span data-stu-id="e979f-161">On the left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="e979f-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="e979f-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="e979f-163">Click **CONFIGURE** from the top.</span><span class="sxs-lookup"><span data-stu-id="e979f-163">Click **CONFIGURE** from the top.</span></span>
5. <span data-ttu-id="e979f-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span><span class="sxs-lookup"><span data-stu-id="e979f-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="e979f-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span><span class="sxs-lookup"><span data-stu-id="e979f-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="e979f-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span><span class="sxs-lookup"><span data-stu-id="e979f-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="e979f-167">For example.</span><span class="sxs-lookup"><span data-stu-id="e979f-167">For example.</span></span> <span data-ttu-id="e979f-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span><span class="sxs-lookup"><span data-stu-id="e979f-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span></span> <span data-ttu-id="e979f-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span><span class="sxs-lookup"><span data-stu-id="e979f-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="e979f-170">In the virtual network address spaces section, click **add gateway subnet**.</span><span class="sxs-lookup"><span data-stu-id="e979f-170">In the virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="e979f-171">Click **SAVE** on the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e979f-171">Click **SAVE** on the bottom of the page.</span></span>
9. <span data-ttu-id="e979f-172">Click **YES** to confirm the change.</span><span class="sxs-lookup"><span data-stu-id="e979f-172">Click **YES** to confirm the change.</span></span> <span data-ttu-id="e979f-173">Wait until the system has finished making the change before you proceed to the next procedure.</span><span class="sxs-lookup"><span data-stu-id="e979f-173">Wait until the system has finished making the change before you proceed to the next procedure.</span></span>

<span data-ttu-id="e979f-174">**To create a dynamic routing gateway**</span><span class="sxs-lookup"><span data-stu-id="e979f-174">**To create a dynamic routing gateway**</span></span>

1. <span data-ttu-id="e979f-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span><span class="sxs-lookup"><span data-stu-id="e979f-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span></span>
2. <span data-ttu-id="e979f-176">Click **CREATE GATEWAY** from the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e979f-176">Click **CREATE GATEWAY** from the bottom of the page.</span></span>
3. <span data-ttu-id="e979f-177">Click **YES** to confirm.</span><span class="sxs-lookup"><span data-stu-id="e979f-177">Click **YES** to confirm.</span></span> <span data-ttu-id="e979f-178">Wait until the gateway is created.</span><span class="sxs-lookup"><span data-stu-id="e979f-178">Wait until the gateway is created.</span></span>
4. <span data-ttu-id="e979f-179">Click **DASHBOARD** from the top.</span><span class="sxs-lookup"><span data-stu-id="e979f-179">Click **DASHBOARD** from the top.</span></span>  <span data-ttu-id="e979f-180">You will see a visual diagram of the virtual network:</span><span class="sxs-lookup"><span data-stu-id="e979f-180">You will see a visual diagram of the virtual network:</span></span>

    ![Azure virtual network point-to-site virtual diagram][img-vnet-diagram]

    <span data-ttu-id="e979f-182">The diagram shows 0 client connections.</span><span class="sxs-lookup"><span data-stu-id="e979f-182">The diagram shows 0 client connections.</span></span> <span data-ttu-id="e979f-183">After you make a connection to the virtual network, the number will be updated to one.</span><span class="sxs-lookup"><span data-stu-id="e979f-183">After you make a connection to the virtual network, the number will be updated to one.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="e979f-184">Create your certificates</span><span class="sxs-lookup"><span data-stu-id="e979f-184">Create your certificates</span></span>
<span data-ttu-id="e979f-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express 2013 for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="e979f-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express 2013 for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="e979f-186">**To create a self-signed root certificate**</span><span class="sxs-lookup"><span data-stu-id="e979f-186">**To create a self-signed root certificate**</span></span>

1. <span data-ttu-id="e979f-187">From your workstation, open a command prompt window.</span><span class="sxs-lookup"><span data-stu-id="e979f-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="e979f-188">Navigate to the Visual Studio tools folder.</span><span class="sxs-lookup"><span data-stu-id="e979f-188">Navigate to the Visual Studio tools folder.</span></span>
3. <span data-ttu-id="e979f-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="e979f-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="e979f-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span><span class="sxs-lookup"><span data-stu-id="e979f-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span></span>

    <span data-ttu-id="e979f-191">Don't close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="e979f-191">Don't close the command prompt.</span></span>  <span data-ttu-id="e979f-192">You will need it in the next procedure.</span><span class="sxs-lookup"><span data-stu-id="e979f-192">You will need it in the next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e979f-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span><span class="sxs-lookup"><span data-stu-id="e979f-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="e979f-194">**To create a client certificate**</span><span class="sxs-lookup"><span data-stu-id="e979f-194">**To create a client certificate**</span></span>

* <span data-ttu-id="e979f-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span><span class="sxs-lookup"><span data-stu-id="e979f-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span></span> <span data-ttu-id="e979f-196">The client certificate must be generated from the root certificate), run the following command:</span><span class="sxs-lookup"><span data-stu-id="e979f-196">The client certificate must be generated from the root certificate), run the following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="e979f-197">HBaseVnetVPNRootCertificate is the root certificate name.</span><span class="sxs-lookup"><span data-stu-id="e979f-197">HBaseVnetVPNRootCertificate is the root certificate name.</span></span>  <span data-ttu-id="e979f-198">It has to match the root certificate name.</span><span class="sxs-lookup"><span data-stu-id="e979f-198">It has to match the root certificate name.</span></span>  

    <span data-ttu-id="e979f-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span><span class="sxs-lookup"><span data-stu-id="e979f-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="e979f-200">Use certmgr.msc to verify.</span><span class="sxs-lookup"><span data-stu-id="e979f-200">Use certmgr.msc to verify.</span></span>

    ![Azure virtual network point-to-site VPN certificate][img-certificate]

    <span data-ttu-id="e979f-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="e979f-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="e979f-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="e979f-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="e979f-204">To export the client certificates, use certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="e979f-204">To export the client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="e979f-205">**To upload the root certificate to the Azure Classic Portal**</span><span class="sxs-lookup"><span data-stu-id="e979f-205">**To upload the root certificate to the Azure Classic Portal**</span></span>

1. <span data-ttu-id="e979f-206">From the Azure Classic Portal, click **NETWORK** on the left.</span><span class="sxs-lookup"><span data-stu-id="e979f-206">From the Azure Classic Portal, click **NETWORK** on the left.</span></span>
2. <span data-ttu-id="e979f-207">Click the virtual network where your HBase cluster is deployed to.</span><span class="sxs-lookup"><span data-stu-id="e979f-207">Click the virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="e979f-208">Click **CERTIFICATES** from the top.</span><span class="sxs-lookup"><span data-stu-id="e979f-208">Click **CERTIFICATES** from the top.</span></span>
4. <span data-ttu-id="e979f-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span><span class="sxs-lookup"><span data-stu-id="e979f-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span></span> <span data-ttu-id="e979f-210">Wait until the certificate got imported.</span><span class="sxs-lookup"><span data-stu-id="e979f-210">Wait until the certificate got imported.</span></span>
5. <span data-ttu-id="e979f-211">Click **DASHBOARD** on the top.</span><span class="sxs-lookup"><span data-stu-id="e979f-211">Click **DASHBOARD** on the top.</span></span>  <span data-ttu-id="e979f-212">The virtual diagram shows the status.</span><span class="sxs-lookup"><span data-stu-id="e979f-212">The virtual diagram shows the status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="e979f-213">Configure your VPN client</span><span class="sxs-lookup"><span data-stu-id="e979f-213">Configure your VPN client</span></span>
<span data-ttu-id="e979f-214">**To download and install the client VPN package**</span><span class="sxs-lookup"><span data-stu-id="e979f-214">**To download and install the client VPN package**</span></span>

1. <span data-ttu-id="e979f-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span><span class="sxs-lookup"><span data-stu-id="e979f-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="e979f-216">Click **Run** to install the package.</span><span class="sxs-lookup"><span data-stu-id="e979f-216">Click **Run** to install the package.</span></span>
3. <span data-ttu-id="e979f-217">At the security prompt, click **More info**, and then click **Run anyway**.</span><span class="sxs-lookup"><span data-stu-id="e979f-217">At the security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="e979f-218">Click **Yes** twice.</span><span class="sxs-lookup"><span data-stu-id="e979f-218">Click **Yes** twice.</span></span>

<span data-ttu-id="e979f-219">**To connect to VPN**</span><span class="sxs-lookup"><span data-stu-id="e979f-219">**To connect to VPN**</span></span>

1. <span data-ttu-id="e979f-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span><span class="sxs-lookup"><span data-stu-id="e979f-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span></span> <span data-ttu-id="e979f-221">You shall see a VPN connection with your virtual network name.</span><span class="sxs-lookup"><span data-stu-id="e979f-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="e979f-222">Click the VPN connection name.</span><span class="sxs-lookup"><span data-stu-id="e979f-222">Click the VPN connection name.</span></span>
3. <span data-ttu-id="e979f-223">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="e979f-223">Click **Connect**.</span></span>

<span data-ttu-id="e979f-224">**To test the VPN connection and domain name resolution**</span><span class="sxs-lookup"><span data-stu-id="e979f-224">**To test the VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="e979f-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="e979f-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="e979f-226">Install and configure SQuirreL on your workstation</span><span class="sxs-lookup"><span data-stu-id="e979f-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="e979f-227">**To install SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="e979f-227">**To install SQuirreL**</span></span>

1. <span data-ttu-id="e979f-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="e979f-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="e979f-229">Open/run the jar file.</span><span class="sxs-lookup"><span data-stu-id="e979f-229">Open/run the jar file.</span></span> <span data-ttu-id="e979f-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="e979f-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="e979f-231">Click **Next** twice.</span><span class="sxs-lookup"><span data-stu-id="e979f-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="e979f-232">Specify a path where you have the write permission, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e979f-232">Specify a path where you have the write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e979f-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span><span class="sxs-lookup"><span data-stu-id="e979f-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="e979f-234">In order to write to this path, the installer must be granted the administrator privilege.</span><span class="sxs-lookup"><span data-stu-id="e979f-234">In order to write to this path, the installer must be granted the administrator privilege.</span></span> <span data-ttu-id="e979f-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span><span class="sxs-lookup"><span data-stu-id="e979f-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="e979f-236">java.exe -jar [the path of the SQuirreL jar file]</span><span class="sxs-lookup"><span data-stu-id="e979f-236">java.exe -jar [the path of the SQuirreL jar file]</span></span>
5. <span data-ttu-id="e979f-237">Click **OK** to confirm creating the target directory.</span><span class="sxs-lookup"><span data-stu-id="e979f-237">Click **OK** to confirm creating the target directory.</span></span>
6. <span data-ttu-id="e979f-238">The default setting is to install the Base and Standard packages.</span><span class="sxs-lookup"><span data-stu-id="e979f-238">The default setting is to install the Base and Standard packages.</span></span>  <span data-ttu-id="e979f-239">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e979f-239">Click **Next**.</span></span>
7. <span data-ttu-id="e979f-240">Click **Next** twice, and then click **Done**.</span><span class="sxs-lookup"><span data-stu-id="e979f-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="e979f-241">**To install the Phoenix driver**</span><span class="sxs-lookup"><span data-stu-id="e979f-241">**To install the Phoenix driver**</span></span>

<span data-ttu-id="e979f-242">The phoenix driver jar file is located on the HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="e979f-242">The phoenix driver jar file is located on the HBase cluster.</span></span> <span data-ttu-id="e979f-243">The path is similar to the following based on the versions:</span><span class="sxs-lookup"><span data-stu-id="e979f-243">The path is similar to the following based on the versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="e979f-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span><span class="sxs-lookup"><span data-stu-id="e979f-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="e979f-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span><span class="sxs-lookup"><span data-stu-id="e979f-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span></span>

<span data-ttu-id="e979f-246">**To add a Phoenix driver to SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="e979f-246">**To add a Phoenix driver to SQuirreL**</span></span>

1. <span data-ttu-id="e979f-247">Open SQuirreL SQL Client from your workstation.</span><span class="sxs-lookup"><span data-stu-id="e979f-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="e979f-248">Click the **Driver** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="e979f-248">Click the **Driver** tab on the left.</span></span>
3. <span data-ttu-id="e979f-249">From the **Drivers** menu, click **New Driver**.</span><span class="sxs-lookup"><span data-stu-id="e979f-249">From the **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="e979f-250">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="e979f-250">Enter the following information:</span></span>

   * <span data-ttu-id="e979f-251">**Name**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="e979f-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="e979f-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e979f-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="e979f-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="e979f-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="e979f-254">User all lower case in the Example URL.</span><span class="sxs-lookup"><span data-stu-id="e979f-254">User all lower case in the Example URL.</span></span> <span data-ttu-id="e979f-255">You can use they full zookeeper quorum in case one of them is down.</span><span class="sxs-lookup"><span data-stu-id="e979f-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="e979f-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="e979f-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL driver][img-squirrel-driver]
5. <span data-ttu-id="e979f-258">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e979f-258">Click **OK**.</span></span>

<span data-ttu-id="e979f-259">**To create an alias to the HBase cluster**</span><span class="sxs-lookup"><span data-stu-id="e979f-259">**To create an alias to the HBase cluster**</span></span>

1. <span data-ttu-id="e979f-260">From SQuirreL, Click the **Aliases** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="e979f-260">From SQuirreL, Click the **Aliases** tab on the left.</span></span>
2. <span data-ttu-id="e979f-261">From the **Aliases** menu, click **New Alias**.</span><span class="sxs-lookup"><span data-stu-id="e979f-261">From the **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="e979f-262">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="e979f-262">Enter the following information:</span></span>

   * <span data-ttu-id="e979f-263">**Name**: The name of the HBase cluster or any name you prefer.</span><span class="sxs-lookup"><span data-stu-id="e979f-263">**Name**: The name of the HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="e979f-264">**Driver**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="e979f-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="e979f-265">This must match the driver name you created in the last procedure.</span><span class="sxs-lookup"><span data-stu-id="e979f-265">This must match the driver name you created in the last procedure.</span></span>
   * <span data-ttu-id="e979f-266">**URL**: The URL is copied from your driver configuration.</span><span class="sxs-lookup"><span data-stu-id="e979f-266">**URL**: The URL is copied from your driver configuration.</span></span> <span data-ttu-id="e979f-267">Make sure to user all lower case.</span><span class="sxs-lookup"><span data-stu-id="e979f-267">Make sure to user all lower case.</span></span>
   * <span data-ttu-id="e979f-268">**User name**: It can be any text.</span><span class="sxs-lookup"><span data-stu-id="e979f-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="e979f-269">Because you use VPN connectivity here, the user name is not used at all.</span><span class="sxs-lookup"><span data-stu-id="e979f-269">Because you use VPN connectivity here, the user name is not used at all.</span></span>
   * <span data-ttu-id="e979f-270">**Password**: It can be any text.</span><span class="sxs-lookup"><span data-stu-id="e979f-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL driver][img-squirrel-alias]
4. <span data-ttu-id="e979f-272">Click **Test**.</span><span class="sxs-lookup"><span data-stu-id="e979f-272">Click **Test**.</span></span>
5. <span data-ttu-id="e979f-273">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="e979f-273">Click **Connect**.</span></span> <span data-ttu-id="e979f-274">When it makes the connection, SQuirreL looks like:</span><span class="sxs-lookup"><span data-stu-id="e979f-274">When it makes the connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="e979f-276">**To run a test**</span><span class="sxs-lookup"><span data-stu-id="e979f-276">**To run a test**</span></span>

1. <span data-ttu-id="e979f-277">Click the **SQL** tab right next to the **Objects** tab.</span><span class="sxs-lookup"><span data-stu-id="e979f-277">Click the **SQL** tab right next to the **Objects** tab.</span></span>
2. <span data-ttu-id="e979f-278">Copy and paste the following code:</span><span class="sxs-lookup"><span data-stu-id="e979f-278">Copy and paste the following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="e979f-279">Click the run button.</span><span class="sxs-lookup"><span data-stu-id="e979f-279">Click the run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="e979f-281">Switch back to the **Objects** tab.</span><span class="sxs-lookup"><span data-stu-id="e979f-281">Switch back to the **Objects** tab.</span></span>
5. <span data-ttu-id="e979f-282">Expand the alias name, and then expand **TABLE**.</span><span class="sxs-lookup"><span data-stu-id="e979f-282">Expand the alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="e979f-283">You shall see the new table listed under.</span><span class="sxs-lookup"><span data-stu-id="e979f-283">You shall see the new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e979f-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="e979f-284">Next steps</span></span>
<span data-ttu-id="e979f-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e979f-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="e979f-286">To learn more, see</span><span class="sxs-lookup"><span data-stu-id="e979f-286">To learn more, see</span></span>

* <span data-ttu-id="e979f-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span><span class="sxs-lookup"><span data-stu-id="e979f-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="e979f-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span><span class="sxs-lookup"><span data-stu-id="e979f-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="e979f-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span><span class="sxs-lookup"><span data-stu-id="e979f-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="e979f-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e979f-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png







