---
title: Install MongoDB on a Windows VM in Azure | Microsoft Docs
description: Learn how to install MongoDB on an Azure VM running Windows Server 2012 R2 created with the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: cynthn
ms.openlocfilehash: 9fa6242910e912872184401d4cc345006cbac13b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44801013"
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="8a239-103">Install and configure MongoDB on a Windows VM in Azure</span><span class="sxs-lookup"><span data-stu-id="8a239-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="8a239-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span><span class="sxs-lookup"><span data-stu-id="8a239-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="8a239-105">This article guides you through installing and configuring MongoDB on a Windows Server 2016 virtual machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a239-105">This article guides you through installing and configuring MongoDB on a Windows Server 2016 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="8a239-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="8a239-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a239-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8a239-107">Prerequisites</span></span>
<span data-ttu-id="8a239-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span><span class="sxs-lookup"><span data-stu-id="8a239-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span></span> <span data-ttu-id="8a239-109">See the following articles to create a VM and add a data disk:</span><span class="sxs-lookup"><span data-stu-id="8a239-109">See the following articles to create a VM and add a data disk:</span></span>

* <span data-ttu-id="8a239-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8a239-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="8a239-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8a239-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="8a239-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="8a239-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="8a239-113">Install MongoDB</span><span class="sxs-lookup"><span data-stu-id="8a239-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8a239-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="8a239-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="8a239-115">Security features should be enabled before deploying MongoDB to a production environment.</span><span class="sxs-lookup"><span data-stu-id="8a239-115">Security features should be enabled before deploying MongoDB to a production environment.</span></span> <span data-ttu-id="8a239-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="8a239-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="8a239-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the taskbar.</span><span class="sxs-lookup"><span data-stu-id="8a239-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the taskbar.</span></span>
2. <span data-ttu-id="8a239-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a239-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="8a239-119">Internet Explorer enhanced security configuration is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="8a239-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="8a239-120">Add the MongoDB website to the list of allowed sites:</span><span class="sxs-lookup"><span data-stu-id="8a239-120">Add the MongoDB website to the list of allowed sites:</span></span>
   
   * <span data-ttu-id="8a239-121">Select the **Tools** icon in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="8a239-121">Select the **Tools** icon in the upper-right corner.</span></span>
   * <span data-ttu-id="8a239-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span><span class="sxs-lookup"><span data-stu-id="8a239-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="8a239-123">Click the **Sites** button.</span><span class="sxs-lookup"><span data-stu-id="8a239-123">Click the **Sites** button.</span></span> <span data-ttu-id="8a239-124">Add *https://\*.mongodb.com* to the list of trusted sites, and then close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="8a239-124">Add *https://\*.mongodb.com* to the list of trusted sites, and then close the dialog box.</span></span>
     
     ![Configure Internet Explorer security settings](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="8a239-126">Browse to the [MongoDB - Downloads](http://www.mongodb.com/downloads) page (http://www.mongodb.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="8a239-126">Browse to the [MongoDB - Downloads](http://www.mongodb.com/downloads) page (http://www.mongodb.com/downloads).</span></span>
5. <span data-ttu-id="8a239-127">If needed, select the **Community Server** edition and then select the latest current stable release for*Windows Server 2008 R2 64-bit and later*.</span><span class="sxs-lookup"><span data-stu-id="8a239-127">If needed, select the **Community Server** edition and then select the latest current stable release for*Windows Server 2008 R2 64-bit and later*.</span></span> <span data-ttu-id="8a239-128">To download the installer, click **DOWNLOAD (msi)**.</span><span class="sxs-lookup"><span data-stu-id="8a239-128">To download the installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Download MongoDB installer](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="8a239-130">Run the installer after the download is complete.</span><span class="sxs-lookup"><span data-stu-id="8a239-130">Run the installer after the download is complete.</span></span>
6. <span data-ttu-id="8a239-131">Read and accept the license agreement.</span><span class="sxs-lookup"><span data-stu-id="8a239-131">Read and accept the license agreement.</span></span> <span data-ttu-id="8a239-132">When you're prompted, select **Complete** install.</span><span class="sxs-lookup"><span data-stu-id="8a239-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="8a239-133">If desired, you can choose to also install Compass, a graphical interface for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8a239-133">If desired, you can choose to also install Compass, a graphical interface for MongoDB.</span></span>
8. <span data-ttu-id="8a239-134">On the final screen, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="8a239-134">On the final screen, click **Install**.</span></span>

## <a name="configure-the-vm-and-mongodb"></a><span data-ttu-id="8a239-135">Configure the VM and MongoDB</span><span class="sxs-lookup"><span data-stu-id="8a239-135">Configure the VM and MongoDB</span></span>
1. <span data-ttu-id="8a239-136">The path variables are not updated by the MongoDB installer.</span><span class="sxs-lookup"><span data-stu-id="8a239-136">The path variables are not updated by the MongoDB installer.</span></span> <span data-ttu-id="8a239-137">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span><span class="sxs-lookup"><span data-stu-id="8a239-137">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="8a239-138">To add the location to your path variable:</span><span class="sxs-lookup"><span data-stu-id="8a239-138">To add the location to your path variable:</span></span>
   
   * <span data-ttu-id="8a239-139">Right-click the **Start** menu, and select **System**.</span><span class="sxs-lookup"><span data-stu-id="8a239-139">Right-click the **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="8a239-140">Click **Advanced system settings**, and then click **Environment Variables**.</span><span class="sxs-lookup"><span data-stu-id="8a239-140">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="8a239-141">Under **System variables**, select **Path**, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="8a239-141">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configure PATH variables](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="8a239-143">Add the path to your MongoDB `bin` folder.</span><span class="sxs-lookup"><span data-stu-id="8a239-143">Add the path to your MongoDB `bin` folder.</span></span> <span data-ttu-id="8a239-144">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="8a239-144">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="8a239-145">Verify the installation path on your VM.</span><span class="sxs-lookup"><span data-stu-id="8a239-145">Verify the installation path on your VM.</span></span> <span data-ttu-id="8a239-146">The following example adds the default MongoDB install location to the `PATH` variable:</span><span class="sxs-lookup"><span data-stu-id="8a239-146">The following example adds the default MongoDB install location to the `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.6\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="8a239-147">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span><span class="sxs-lookup"><span data-stu-id="8a239-147">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span></span>

2. <span data-ttu-id="8a239-148">Create MongoDB data and log directories on your data disk.</span><span class="sxs-lookup"><span data-stu-id="8a239-148">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="8a239-149">From the **Start** menu, select **Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="8a239-149">From the **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="8a239-150">The following examples create the directories on drive F:</span><span class="sxs-lookup"><span data-stu-id="8a239-150">The following examples create the directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="8a239-151">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span><span class="sxs-lookup"><span data-stu-id="8a239-151">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="8a239-152">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span><span class="sxs-lookup"><span data-stu-id="8a239-152">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span></span> <span data-ttu-id="8a239-153">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span><span class="sxs-lookup"><span data-stu-id="8a239-153">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8a239-154">The command prompt stays focused on this task while your MongoDB instance is running.</span><span class="sxs-lookup"><span data-stu-id="8a239-154">The command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="8a239-155">Leave the command prompt window open to continue running MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8a239-155">Leave the command prompt window open to continue running MongoDB.</span></span> <span data-ttu-id="8a239-156">Or, install MongoDB as service, as detailed in the next step.</span><span class="sxs-lookup"><span data-stu-id="8a239-156">Or, install MongoDB as service, as detailed in the next step.</span></span>

4. <span data-ttu-id="8a239-157">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span><span class="sxs-lookup"><span data-stu-id="8a239-157">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span></span> <span data-ttu-id="8a239-158">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8a239-158">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span></span> <span data-ttu-id="8a239-159">Create the service as follows, adjusting the path to your data and log directories accordingly:</span><span class="sxs-lookup"><span data-stu-id="8a239-159">Create the service as follows, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install
    ```
   
    <span data-ttu-id="8a239-160">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="8a239-160">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="8a239-161">The following parameters are also specified:</span><span class="sxs-lookup"><span data-stu-id="8a239-161">The following parameters are also specified:</span></span>
   
   * <span data-ttu-id="8a239-162">The `--dbpath` option specifies the location of the data directory.</span><span class="sxs-lookup"><span data-stu-id="8a239-162">The `--dbpath` option specifies the location of the data directory.</span></span>
   * <span data-ttu-id="8a239-163">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span><span class="sxs-lookup"><span data-stu-id="8a239-163">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span></span>
   * <span data-ttu-id="8a239-164">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span><span class="sxs-lookup"><span data-stu-id="8a239-164">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>
   
   <span data-ttu-id="8a239-165">To start the MongoDB service, run the following command:</span><span class="sxs-lookup"><span data-stu-id="8a239-165">To start the MongoDB service, run the following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="8a239-166">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="8a239-166">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-the-mongodb-instance"></a><span data-ttu-id="8a239-167">Test the MongoDB instance</span><span class="sxs-lookup"><span data-stu-id="8a239-167">Test the MongoDB instance</span></span>
<span data-ttu-id="8a239-168">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span><span class="sxs-lookup"><span data-stu-id="8a239-168">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="8a239-169">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span><span class="sxs-lookup"><span data-stu-id="8a239-169">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span></span>

```
mongo  
```

<span data-ttu-id="8a239-170">You can list the databases with the `db` command.</span><span class="sxs-lookup"><span data-stu-id="8a239-170">You can list the databases with the `db` command.</span></span> <span data-ttu-id="8a239-171">Insert some data as follows:</span><span class="sxs-lookup"><span data-stu-id="8a239-171">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="8a239-172">Search for data as follows:</span><span class="sxs-lookup"><span data-stu-id="8a239-172">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="8a239-173">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="8a239-173">The output is similar to the following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="8a239-174">Exit the `mongo` console as follows:</span><span class="sxs-lookup"><span data-stu-id="8a239-174">Exit the `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="8a239-175">Configure firewall and Network Security Group rules</span><span class="sxs-lookup"><span data-stu-id="8a239-175">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="8a239-176">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8a239-176">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span> <span data-ttu-id="8a239-177">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span><span class="sxs-lookup"><span data-stu-id="8a239-177">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="8a239-178">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span><span class="sxs-lookup"><span data-stu-id="8a239-178">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="8a239-179">Create a new inbound rule to allow TCP port 27017.</span><span class="sxs-lookup"><span data-stu-id="8a239-179">Create a new inbound rule to allow TCP port 27017.</span></span>

<span data-ttu-id="8a239-180">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="8a239-180">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span></span> <span data-ttu-id="8a239-181">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8a239-181">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="8a239-182">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span><span class="sxs-lookup"><span data-stu-id="8a239-182">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="8a239-183">TCP port 27017 is the default port used by MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8a239-183">TCP port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="8a239-184">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span><span class="sxs-lookup"><span data-stu-id="8a239-184">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="8a239-185">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="8a239-185">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8a239-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a239-186">Next steps</span></span>
<span data-ttu-id="8a239-187">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span><span class="sxs-lookup"><span data-stu-id="8a239-187">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="8a239-188">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="8a239-188">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

