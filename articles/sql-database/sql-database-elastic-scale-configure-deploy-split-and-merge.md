---
title: Deploy a split-merge service | Microsoft Docs
description: Use the split-merge too to move data between sharded databases.
services: sql-database
author: stevestein
manager: craigg
ms.service: sql-database
ms.custom: scale out apps
ms.topic: conceptual
ms.date: 04/01/2018
ms.author: sstein
ms.openlocfilehash: c7682b63689d9b47fce5fa65a3c0a2301d53502a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803327"
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="826a7-103">Deploy a split-merge service</span><span class="sxs-lookup"><span data-stu-id="826a7-103">Deploy a split-merge service</span></span>
<span data-ttu-id="826a7-104">The split-merge tool lets you move data between sharded databases.</span><span class="sxs-lookup"><span data-stu-id="826a7-104">The split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="826a7-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="826a7-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-the-split-merge-packages"></a><span data-ttu-id="826a7-106">Download the Split-Merge packages</span><span class="sxs-lookup"><span data-stu-id="826a7-106">Download the Split-Merge packages</span></span>
1. <span data-ttu-id="826a7-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="826a7-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="826a7-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="826a7-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="826a7-109">The download includes PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="826a7-109">The download includes PowerShell commands.</span></span>
3. <span data-ttu-id="826a7-110">Download the latest Split-Merge package into the current directory with the below command:</span><span class="sxs-lookup"><span data-stu-id="826a7-110">Download the latest Split-Merge package into the current directory with the below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="826a7-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span><span class="sxs-lookup"><span data-stu-id="826a7-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span></span> <span data-ttu-id="826a7-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client dlls) in the **content\splitmerge\powershell** sub-directory.</span><span class="sxs-lookup"><span data-stu-id="826a7-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client dlls) in the **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="826a7-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="826a7-113">Prerequisites</span></span>
1. <span data-ttu-id="826a7-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span><span class="sxs-lookup"><span data-stu-id="826a7-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span></span> <span data-ttu-id="826a7-115">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="826a7-115">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="826a7-116">Create a new **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="826a7-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="826a7-117">Give the database a name and create a new administrator and password.</span><span class="sxs-lookup"><span data-stu-id="826a7-117">Give the database a name and create a new administrator and password.</span></span> <span data-ttu-id="826a7-118">Be sure to record the name and password for later use.</span><span class="sxs-lookup"><span data-stu-id="826a7-118">Be sure to record the name and password for later use.</span></span>
2. <span data-ttu-id="826a7-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span><span class="sxs-lookup"><span data-stu-id="826a7-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="826a7-120">In the portal, in the **Firewall Settings**, ensure the **Allow access to Azure Services** setting is set to **On**.</span><span class="sxs-lookup"><span data-stu-id="826a7-120">In the portal, in the **Firewall Settings**, ensure the **Allow access to Azure Services** setting is set to **On**.</span></span> <span data-ttu-id="826a7-121">Click the "save" icon.</span><span class="sxs-lookup"><span data-stu-id="826a7-121">Click the "save" icon.</span></span>
3. <span data-ttu-id="826a7-122">Create an Azure Storage account for diagnostics output.</span><span class="sxs-lookup"><span data-stu-id="826a7-122">Create an Azure Storage account for diagnostics output.</span></span>
4. <span data-ttu-id="826a7-123">Create an Azure Cloud Service for your Split-Merge service.</span><span class="sxs-lookup"><span data-stu-id="826a7-123">Create an Azure Cloud Service for your Split-Merge service.</span></span>

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="826a7-124">Configure your Split-Merge service</span><span class="sxs-lookup"><span data-stu-id="826a7-124">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="826a7-125">Split-Merge service configuration</span><span class="sxs-lookup"><span data-stu-id="826a7-125">Split-Merge service configuration</span></span>
1. <span data-ttu-id="826a7-126">In the folder into which you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="826a7-126">In the folder into which you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="826a7-127">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span><span class="sxs-lookup"><span data-stu-id="826a7-127">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span></span>
3. <span data-ttu-id="826a7-128">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span><span class="sxs-lookup"><span data-stu-id="826a7-128">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="826a7-129">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="826a7-129">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="826a7-130">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="826a7-130">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="826a7-131">With Azure SQL DB, the connection string typically is of the form:</span><span class="sxs-lookup"><span data-stu-id="826a7-131">With Azure SQL DB, the connection string typically is of the form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="826a7-132">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span><span class="sxs-lookup"><span data-stu-id="826a7-132">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="826a7-133">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span><span class="sxs-lookup"><span data-stu-id="826a7-133">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="826a7-134">Configure security</span><span class="sxs-lookup"><span data-stu-id="826a7-134">Configure security</span></span>
<span data-ttu-id="826a7-135">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="826a7-135">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="826a7-136">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span><span class="sxs-lookup"><span data-stu-id="826a7-136">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span></span> <span data-ttu-id="826a7-137">These steps enable only the one machine/account executing them to communicate with the service.</span><span class="sxs-lookup"><span data-stu-id="826a7-137">These steps enable only the one machine/account executing them to communicate with the service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="826a7-138">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="826a7-138">Create a self-signed certificate</span></span>
<span data-ttu-id="826a7-139">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span><span class="sxs-lookup"><span data-stu-id="826a7-139">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="826a7-140">You are asked for a password to protect the private key.</span><span class="sxs-lookup"><span data-stu-id="826a7-140">You are asked for a password to protect the private key.</span></span> <span data-ttu-id="826a7-141">Enter a strong password and confirm it.</span><span class="sxs-lookup"><span data-stu-id="826a7-141">Enter a strong password and confirm it.</span></span> <span data-ttu-id="826a7-142">You are then prompted for the password to be used once more after that.</span><span class="sxs-lookup"><span data-stu-id="826a7-142">You are then prompted for the password to be used once more after that.</span></span> <span data-ttu-id="826a7-143">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span><span class="sxs-lookup"><span data-stu-id="826a7-143">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="826a7-144">Create a PFX file</span><span class="sxs-lookup"><span data-stu-id="826a7-144">Create a PFX file</span></span>
<span data-ttu-id="826a7-145">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span><span class="sxs-lookup"><span data-stu-id="826a7-145">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-the-client-certificate-into-the-personal-store"></a><span data-ttu-id="826a7-146">Import the client certificate into the personal store</span><span class="sxs-lookup"><span data-stu-id="826a7-146">Import the client certificate into the personal store</span></span>
1. <span data-ttu-id="826a7-147">In Windows Explorer, double-click **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="826a7-147">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="826a7-148">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="826a7-148">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="826a7-149">Confirm the file path and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="826a7-149">Confirm the file path and click **Next**.</span></span>
4. <span data-ttu-id="826a7-150">Type the password, leave **Include all extended properties** checked and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="826a7-150">Type the password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="826a7-151">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="826a7-151">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="826a7-152">Click **Finish** and **OK**.</span><span class="sxs-lookup"><span data-stu-id="826a7-152">Click **Finish** and **OK**.</span></span>

### <a name="upload-the-pfx-file-to-the-cloud-service"></a><span data-ttu-id="826a7-153">Upload the PFX file to the cloud service</span><span class="sxs-lookup"><span data-stu-id="826a7-153">Upload the PFX file to the cloud service</span></span>
1. <span data-ttu-id="826a7-154">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="826a7-154">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="826a7-155">Select **Cloud Services**.</span><span class="sxs-lookup"><span data-stu-id="826a7-155">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="826a7-156">Select the cloud service you created above for the Split/Merge service.</span><span class="sxs-lookup"><span data-stu-id="826a7-156">Select the cloud service you created above for the Split/Merge service.</span></span>
4. <span data-ttu-id="826a7-157">Click **Certificates** on the top menu.</span><span class="sxs-lookup"><span data-stu-id="826a7-157">Click **Certificates** on the top menu.</span></span>
5. <span data-ttu-id="826a7-158">Click **Upload** in the bottom bar.</span><span class="sxs-lookup"><span data-stu-id="826a7-158">Click **Upload** in the bottom bar.</span></span>
6. <span data-ttu-id="826a7-159">Select the PFX file and enter the same password as above.</span><span class="sxs-lookup"><span data-stu-id="826a7-159">Select the PFX file and enter the same password as above.</span></span>
7. <span data-ttu-id="826a7-160">Once completed, copy the certificate thumbprint from the new entry in the list.</span><span class="sxs-lookup"><span data-stu-id="826a7-160">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

### <a name="update-the-service-configuration-file"></a><span data-ttu-id="826a7-161">Update the service configuration file</span><span class="sxs-lookup"><span data-stu-id="826a7-161">Update the service configuration file</span></span>
<span data-ttu-id="826a7-162">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span><span class="sxs-lookup"><span data-stu-id="826a7-162">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="826a7-163">For the worker role:</span><span class="sxs-lookup"><span data-stu-id="826a7-163">For the worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="826a7-164">For the web role:</span><span class="sxs-lookup"><span data-stu-id="826a7-164">For the web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="826a7-165">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span><span class="sxs-lookup"><span data-stu-id="826a7-165">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span></span> <span data-ttu-id="826a7-166">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="826a7-166">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="826a7-167">Deploy your service</span><span class="sxs-lookup"><span data-stu-id="826a7-167">Deploy your service</span></span>
1. <span data-ttu-id="826a7-168">Go to the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="826a7-168">Go to the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="826a7-169">Select the cloud service that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="826a7-169">Select the cloud service that you created earlier.</span></span>
3. <span data-ttu-id="826a7-170">Click **Overview**.</span><span class="sxs-lookup"><span data-stu-id="826a7-170">Click **Overview**.</span></span>
4. <span data-ttu-id="826a7-171">Choose the staging environment, then click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="826a7-171">Choose the staging environment, then click **Upload**.</span></span>
5. <span data-ttu-id="826a7-172">In the dialog box, enter a deployment label.</span><span class="sxs-lookup"><span data-stu-id="826a7-172">In the dialog box, enter a deployment label.</span></span> <span data-ttu-id="826a7-173">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your cscfg file that you configured earlier.</span><span class="sxs-lookup"><span data-stu-id="826a7-173">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="826a7-174">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span><span class="sxs-lookup"><span data-stu-id="826a7-174">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="826a7-175">Hit the tick button in the bottom right to begin the deployment.</span><span class="sxs-lookup"><span data-stu-id="826a7-175">Hit the tick button in the bottom right to begin the deployment.</span></span> <span data-ttu-id="826a7-176">Expect it to take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="826a7-176">Expect it to take a few minutes to complete.</span></span>


## <a name="troubleshoot-the-deployment"></a><span data-ttu-id="826a7-177">Troubleshoot the deployment</span><span class="sxs-lookup"><span data-stu-id="826a7-177">Troubleshoot the deployment</span></span>
<span data-ttu-id="826a7-178">If your web role fails to come online, it is likely a problem with the security configuration.</span><span class="sxs-lookup"><span data-stu-id="826a7-178">If your web role fails to come online, it is likely a problem with the security configuration.</span></span> <span data-ttu-id="826a7-179">Check that the SSL is configured as described above.</span><span class="sxs-lookup"><span data-stu-id="826a7-179">Check that the SSL is configured as described above.</span></span>

<span data-ttu-id="826a7-180">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="826a7-180">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span></span>

* <span data-ttu-id="826a7-181">Make sure that the connection string in your cscfg is accurate.</span><span class="sxs-lookup"><span data-stu-id="826a7-181">Make sure that the connection string in your cscfg is accurate.</span></span>
* <span data-ttu-id="826a7-182">Check that the server and database exist, and that the user id and password are correct.</span><span class="sxs-lookup"><span data-stu-id="826a7-182">Check that the server and database exist, and that the user id and password are correct.</span></span>
* <span data-ttu-id="826a7-183">For Azure SQL DB, the connection string should be of the form:</span><span class="sxs-lookup"><span data-stu-id="826a7-183">For Azure SQL DB, the connection string should be of the form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="826a7-184">Ensure that the server name does not begin with **https://**.</span><span class="sxs-lookup"><span data-stu-id="826a7-184">Ensure that the server name does not begin with **https://**.</span></span>
* <span data-ttu-id="826a7-185">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span><span class="sxs-lookup"><span data-stu-id="826a7-185">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="826a7-186">To do this, open your database in the portal and ensure that the **Allow access to Azure Services** setting is set to \*\*On\*\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="826a7-186">To do this, open your database in the portal and ensure that the **Allow access to Azure Services** setting is set to \*\*On\*\*\*\*.</span></span>

## <a name="test-the-service-deployment"></a><span data-ttu-id="826a7-187">Test the service deployment</span><span class="sxs-lookup"><span data-stu-id="826a7-187">Test the service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="826a7-188">Connect with a web browser</span><span class="sxs-lookup"><span data-stu-id="826a7-188">Connect with a web browser</span></span>
<span data-ttu-id="826a7-189">Determine the web endpoint of your Split-Merge service.</span><span class="sxs-lookup"><span data-stu-id="826a7-189">Determine the web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="826a7-190">You can find this in the portal by going to the **Overview** of your cloud service and looking under **Site URL** on the right side.</span><span class="sxs-lookup"><span data-stu-id="826a7-190">You can find this in the portal by going to the **Overview** of your cloud service and looking under **Site URL** on the right side.</span></span> <span data-ttu-id="826a7-191">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="826a7-191">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span></span> <span data-ttu-id="826a7-192">Load the page for this URL into your browser.</span><span class="sxs-lookup"><span data-stu-id="826a7-192">Load the page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="826a7-193">Test with PowerShell scripts</span><span class="sxs-lookup"><span data-stu-id="826a7-193">Test with PowerShell scripts</span></span>
<span data-ttu-id="826a7-194">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="826a7-194">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span></span>

<span data-ttu-id="826a7-195">The script files included are:</span><span class="sxs-lookup"><span data-stu-id="826a7-195">The script files included are:</span></span>

1. <span data-ttu-id="826a7-196">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span><span class="sxs-lookup"><span data-stu-id="826a7-196">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="826a7-197">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span><span class="sxs-lookup"><span data-stu-id="826a7-197">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="826a7-198">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span><span class="sxs-lookup"><span data-stu-id="826a7-198">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span></span>
4. <span data-ttu-id="826a7-199">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="826a7-199">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span></span>
5. <span data-ttu-id="826a7-200">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span><span class="sxs-lookup"><span data-stu-id="826a7-200">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="826a7-201">PowerShell file</span><span class="sxs-lookup"><span data-stu-id="826a7-201">PowerShell file</span></span></th>
       <th><span data-ttu-id="826a7-202">Steps</span><span class="sxs-lookup"><span data-stu-id="826a7-202">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="826a7-203">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="826a7-203">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="826a7-204">Creates a shard map manager database</span><span class="sxs-lookup"><span data-stu-id="826a7-204">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="826a7-205">Creates 2 shard databases.</span><span class="sxs-lookup"><span data-stu-id="826a7-205">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="826a7-206">Creates a shard map for those databases (deletes any existing shard maps on those databases).</span><span class="sxs-lookup"><span data-stu-id="826a7-206">Creates a shard map for those databases (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="826a7-207">Creates a small sample table in both the shards, and populates the table in one of the shards.</span><span class="sxs-lookup"><span data-stu-id="826a7-207">Creates a small sample table in both the shards, and populates the table in one of the shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="826a7-208">Declares the SchemaInfo for the sharded table.</span><span class="sxs-lookup"><span data-stu-id="826a7-208">Declares the SchemaInfo for the sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="826a7-209">PowerShell file</span><span class="sxs-lookup"><span data-stu-id="826a7-209">PowerShell file</span></span></th>
       <th><span data-ttu-id="826a7-210">Steps</span><span class="sxs-lookup"><span data-stu-id="826a7-210">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="826a7-211">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="826a7-211">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="826a7-212">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span><span class="sxs-lookup"><span data-stu-id="826a7-212">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="826a7-213">Polls the web frontend for the split request status and waits until the request completes.</span><span class="sxs-lookup"><span data-stu-id="826a7-213">Polls the web frontend for the split request status and waits until the request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="826a7-214">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span><span class="sxs-lookup"><span data-stu-id="826a7-214">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="826a7-215">Polls the web frontend for the merge request status and waits until the request completes.</span><span class="sxs-lookup"><span data-stu-id="826a7-215">Polls the web frontend for the merge request status and waits until the request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-to-verify-your-deployment"></a><span data-ttu-id="826a7-216">Use PowerShell to verify your deployment</span><span class="sxs-lookup"><span data-stu-id="826a7-216">Use PowerShell to verify your deployment</span></span>
1. <span data-ttu-id="826a7-217">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span><span class="sxs-lookup"><span data-stu-id="826a7-217">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span></span>
2. <span data-ttu-id="826a7-218">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span><span class="sxs-lookup"><span data-stu-id="826a7-218">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="826a7-219">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span><span class="sxs-lookup"><span data-stu-id="826a7-219">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span></span> <span data-ttu-id="826a7-220">This is not a restriction of the Split-Merge Service itself.</span><span class="sxs-lookup"><span data-stu-id="826a7-220">This is not a restriction of the Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="826a7-221">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span><span class="sxs-lookup"><span data-stu-id="826a7-221">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span></span> <span data-ttu-id="826a7-222">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span><span class="sxs-lookup"><span data-stu-id="826a7-222">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="826a7-223">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span><span class="sxs-lookup"><span data-stu-id="826a7-223">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span></span> <span data-ttu-id="826a7-224">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span><span class="sxs-lookup"><span data-stu-id="826a7-224">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="826a7-225">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span><span class="sxs-lookup"><span data-stu-id="826a7-225">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span></span>
   
   <span data-ttu-id="826a7-226">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span><span class="sxs-lookup"><span data-stu-id="826a7-226">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span></span> <span data-ttu-id="826a7-227">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span><span class="sxs-lookup"><span data-stu-id="826a7-227">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span></span>
   
   <span data-ttu-id="826a7-228">Sample command line:</span><span class="sxs-lookup"><span data-stu-id="826a7-228">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="826a7-229">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span><span class="sxs-lookup"><span data-stu-id="826a7-229">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="826a7-230">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span><span class="sxs-lookup"><span data-stu-id="826a7-230">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span></span> <span data-ttu-id="826a7-231">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span><span class="sxs-lookup"><span data-stu-id="826a7-231">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span></span>
   
   <span data-ttu-id="826a7-232">Sample command line:</span><span class="sxs-lookup"><span data-stu-id="826a7-232">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="826a7-233">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span><span class="sxs-lookup"><span data-stu-id="826a7-233">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="826a7-234">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span><span class="sxs-lookup"><span data-stu-id="826a7-234">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="826a7-235">If it succeeded, the output should look like the below:</span><span class="sxs-lookup"><span data-stu-id="826a7-235">If it succeeded, the output should look like the below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="826a7-236">Experiment with other data types!</span><span class="sxs-lookup"><span data-stu-id="826a7-236">Experiment with other data types!</span></span> <span data-ttu-id="826a7-237">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span><span class="sxs-lookup"><span data-stu-id="826a7-237">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span></span> <span data-ttu-id="826a7-238">The default is Int32, but you can also specify Int64, Guid, or Binary.</span><span class="sxs-lookup"><span data-stu-id="826a7-238">The default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="826a7-239">Create requests</span><span class="sxs-lookup"><span data-stu-id="826a7-239">Create requests</span></span>
<span data-ttu-id="826a7-240">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span><span class="sxs-lookup"><span data-stu-id="826a7-240">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span></span>

<span data-ttu-id="826a7-241">The service can move data in both sharded tables and reference tables.</span><span class="sxs-lookup"><span data-stu-id="826a7-241">The service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="826a7-242">A sharded table has a sharding key column and has different row data on each shard.</span><span class="sxs-lookup"><span data-stu-id="826a7-242">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="826a7-243">A reference table is not sharded so it contains the same row data on every shard.</span><span class="sxs-lookup"><span data-stu-id="826a7-243">A reference table is not sharded so it contains the same row data on every shard.</span></span> <span data-ttu-id="826a7-244">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span><span class="sxs-lookup"><span data-stu-id="826a7-244">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span></span>

<span data-ttu-id="826a7-245">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span><span class="sxs-lookup"><span data-stu-id="826a7-245">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span></span> <span data-ttu-id="826a7-246">This is accomplished with the **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="826a7-246">This is accomplished with the **SchemaInfo** API.</span></span> <span data-ttu-id="826a7-247">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span><span class="sxs-lookup"><span data-stu-id="826a7-247">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="826a7-248">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span><span class="sxs-lookup"><span data-stu-id="826a7-248">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span></span>
2. <span data-ttu-id="826a7-249">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span><span class="sxs-lookup"><span data-stu-id="826a7-249">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span></span>
3. <span data-ttu-id="826a7-250">Add the above TableInfo objects to a new **SchemaInfo** object.</span><span class="sxs-lookup"><span data-stu-id="826a7-250">Add the above TableInfo objects to a new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="826a7-251">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="826a7-251">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="826a7-252">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span><span class="sxs-lookup"><span data-stu-id="826a7-252">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span></span>

<span data-ttu-id="826a7-253">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="826a7-253">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="826a7-254">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span><span class="sxs-lookup"><span data-stu-id="826a7-254">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span></span> <span data-ttu-id="826a7-255">They must be pre-created before sending a request to the service.</span><span class="sxs-lookup"><span data-stu-id="826a7-255">They must be pre-created before sending a request to the service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="826a7-256">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="826a7-256">Troubleshooting</span></span>
<span data-ttu-id="826a7-257">You may see the below message when running the sample powershell scripts:</span><span class="sxs-lookup"><span data-stu-id="826a7-257">You may see the below message when running the sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.
   ```

<span data-ttu-id="826a7-258">This error means that your SSL certificate is not configured correctly.</span><span class="sxs-lookup"><span data-stu-id="826a7-258">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="826a7-259">Please follow the instructions in section 'Connecting with a web browser'.</span><span class="sxs-lookup"><span data-stu-id="826a7-259">Please follow the instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="826a7-260">If you cannot submit requests you may see this:</span><span class="sxs-lookup"><span data-stu-id="826a7-260">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="826a7-261">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="826a7-261">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="826a7-262">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span><span class="sxs-lookup"><span data-stu-id="826a7-262">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

