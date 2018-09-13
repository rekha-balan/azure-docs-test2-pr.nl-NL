---
title: Collect Linux application performance in OMS Log Analytics | Microsoft Docs
description: This article provides details for configuring the OMS Agent for Linux to collect performance counters for MySQL and Apache HTTP Server.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 528274844908f9a1b2a604de42d8e84f4dc7d6f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864442"
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a><span data-ttu-id="4aa46-103">Collect performance counters for Linux applications in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4aa46-103">Collect performance counters for Linux applications in Log Analytics</span></span> 
<span data-ttu-id="4aa46-104">This article provides details for configuring the [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) to collect performance counters for specific applications.</span><span class="sxs-lookup"><span data-stu-id="4aa46-104">This article provides details for configuring the [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) to collect performance counters for specific applications.</span></span>  <span data-ttu-id="4aa46-105">The applications included in this article are:</span><span class="sxs-lookup"><span data-stu-id="4aa46-105">The applications included in this article are:</span></span>  

- [<span data-ttu-id="4aa46-106">MySQL</span><span class="sxs-lookup"><span data-stu-id="4aa46-106">MySQL</span></span>](#MySQL)
- [<span data-ttu-id="4aa46-107">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-107">Apache HTTP Server</span></span>](#apache-http-server)

## <a name="mysql"></a><span data-ttu-id="4aa46-108">MySQL</span><span class="sxs-lookup"><span data-stu-id="4aa46-108">MySQL</span></span>
<span data-ttu-id="4aa46-109">If MySQL Server or MariaDB Server is detected on the computer when the OMS agent is installed, a performance monitoring provider for MySQL Server will be automatically installed.</span><span class="sxs-lookup"><span data-stu-id="4aa46-109">If MySQL Server or MariaDB Server is detected on the computer when the OMS agent is installed, a performance monitoring provider for MySQL Server will be automatically installed.</span></span> <span data-ttu-id="4aa46-110">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span><span class="sxs-lookup"><span data-stu-id="4aa46-110">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="4aa46-111">MySQL user credentials must be configured so that the provider can access the MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="4aa46-111">MySQL user credentials must be configured so that the provider can access the MySQL Server.</span></span>

### <a name="configure-mysql-credentials"></a><span data-ttu-id="4aa46-112">Configure MySQL credentials</span><span class="sxs-lookup"><span data-stu-id="4aa46-112">Configure MySQL credentials</span></span>
<span data-ttu-id="4aa46-113">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance and health information from the MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="4aa46-113">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance and health information from the MySQL instance.</span></span>  <span data-ttu-id="4aa46-114">These credentials are stored in an authentication file that's stored on the Linux agent.</span><span class="sxs-lookup"><span data-stu-id="4aa46-114">These credentials are stored in an authentication file that's stored on the Linux agent.</span></span>  <span data-ttu-id="4aa46-115">The authentication file specifies what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span><span class="sxs-lookup"><span data-stu-id="4aa46-115">The authentication file specifies what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span>  

<span data-ttu-id="4aa46-116">During installation of the OMS Agent for Linux the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span><span class="sxs-lookup"><span data-stu-id="4aa46-116">During installation of the OMS Agent for Linux the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="4aa46-117">The MySQL authentication file is stored at `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span><span class="sxs-lookup"><span data-stu-id="4aa46-117">The MySQL authentication file is stored at `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span></span>


### <a name="authentication-file-format"></a><span data-ttu-id="4aa46-118">Authentication file format</span><span class="sxs-lookup"><span data-stu-id="4aa46-118">Authentication file format</span></span>
<span data-ttu-id="4aa46-119">Following is the format for the MySQL OMI authentication file</span><span class="sxs-lookup"><span data-stu-id="4aa46-119">Following is the format for the MySQL OMI authentication file</span></span>

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

<span data-ttu-id="4aa46-120">The entries in the authentication file are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4aa46-120">The entries in the authentication file are described in the following table.</span></span>

| <span data-ttu-id="4aa46-121">Property</span><span class="sxs-lookup"><span data-stu-id="4aa46-121">Property</span></span> | <span data-ttu-id="4aa46-122">Description</span><span class="sxs-lookup"><span data-stu-id="4aa46-122">Description</span></span> |
|:--|:--|
| <span data-ttu-id="4aa46-123">Port</span><span class="sxs-lookup"><span data-stu-id="4aa46-123">Port</span></span> | <span data-ttu-id="4aa46-124">Represents the current port the MySQL instance is listening on.</span><span class="sxs-lookup"><span data-stu-id="4aa46-124">Represents the current port the MySQL instance is listening on.</span></span> <span data-ttu-id="4aa46-125">Port 0 specifies that the properties following are used for default instance.</span><span class="sxs-lookup"><span data-stu-id="4aa46-125">Port 0 specifies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="4aa46-126">Bind-Address</span><span class="sxs-lookup"><span data-stu-id="4aa46-126">Bind-Address</span></span>| <span data-ttu-id="4aa46-127">Current MySQL bind-address.</span><span class="sxs-lookup"><span data-stu-id="4aa46-127">Current MySQL bind-address.</span></span> |
| <span data-ttu-id="4aa46-128">username</span><span class="sxs-lookup"><span data-stu-id="4aa46-128">username</span></span>| <span data-ttu-id="4aa46-129">MySQL user used to use to monitor the MySQL server instance.</span><span class="sxs-lookup"><span data-stu-id="4aa46-129">MySQL user used to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="4aa46-130">Base64 encoded Password</span><span class="sxs-lookup"><span data-stu-id="4aa46-130">Base64 encoded Password</span></span>| <span data-ttu-id="4aa46-131">Password of the MySQL monitoring user encoded in Base64.</span><span class="sxs-lookup"><span data-stu-id="4aa46-131">Password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="4aa46-132">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="4aa46-132">AutoUpdate</span></span>| <span data-ttu-id="4aa46-133">Specifies whether to rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file when the MySQL OMI Provider is upgraded.</span><span class="sxs-lookup"><span data-stu-id="4aa46-133">Specifies whether to rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file when the MySQL OMI Provider is upgraded.</span></span> |

### <a name="default-instance"></a><span data-ttu-id="4aa46-134">Default instance</span><span class="sxs-lookup"><span data-stu-id="4aa46-134">Default instance</span></span>
<span data-ttu-id="4aa46-135">The MySQL OMI authentication file can define a default instance and port number to make managing multiple MySQL instances on one Linux host easier.</span><span class="sxs-lookup"><span data-stu-id="4aa46-135">The MySQL OMI authentication file can define a default instance and port number to make managing multiple MySQL instances on one Linux host easier.</span></span>  <span data-ttu-id="4aa46-136">The default instance is denoted by an instance with port 0.</span><span class="sxs-lookup"><span data-stu-id="4aa46-136">The default instance is denoted by an instance with port 0.</span></span> <span data-ttu-id="4aa46-137">All additional instances will inherit properties set from the default instance unless they specify different values.</span><span class="sxs-lookup"><span data-stu-id="4aa46-137">All additional instances will inherit properties set from the default instance unless they specify different values.</span></span> <span data-ttu-id="4aa46-138">For example, if MySQL instance listening on port ‘3308’ is added, the default instance’s bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span><span class="sxs-lookup"><span data-stu-id="4aa46-138">For example, if MySQL instance listening on port ‘3308’ is added, the default instance’s bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="4aa46-139">If the instance on 3308 is bound to another address and uses the same MySQL username and password pair only the bind-address is needed, and the other properties will be inherited.</span><span class="sxs-lookup"><span data-stu-id="4aa46-139">If the instance on 3308 is bound to another address and uses the same MySQL username and password pair only the bind-address is needed, and the other properties will be inherited.</span></span>

<span data-ttu-id="4aa46-140">The following table has example instance settings</span><span class="sxs-lookup"><span data-stu-id="4aa46-140">The following table has example instance settings</span></span> 

| <span data-ttu-id="4aa46-141">Description</span><span class="sxs-lookup"><span data-stu-id="4aa46-141">Description</span></span> | <span data-ttu-id="4aa46-142">File</span><span class="sxs-lookup"><span data-stu-id="4aa46-142">File</span></span> |
|:--|:--|
| <span data-ttu-id="4aa46-143">Default instance and instance with port 3308.</span><span class="sxs-lookup"><span data-stu-id="4aa46-143">Default instance and instance with port 3308.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| <span data-ttu-id="4aa46-144">Default instance and instance with port 3308 and different user name and password.</span><span class="sxs-lookup"><span data-stu-id="4aa46-144">Default instance and instance with port 3308 and different user name and password.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a><span data-ttu-id="4aa46-145">MySQL OMI Authentication File Program</span><span class="sxs-lookup"><span data-stu-id="4aa46-145">MySQL OMI Authentication File Program</span></span>
<span data-ttu-id="4aa46-146">Included with the installation of the MySQL OMI provider is a MySQL OMI authentication file program which can be used to edit the MySQL OMI Authentication file.</span><span class="sxs-lookup"><span data-stu-id="4aa46-146">Included with the installation of the MySQL OMI provider is a MySQL OMI authentication file program which can be used to edit the MySQL OMI Authentication file.</span></span> <span data-ttu-id="4aa46-147">The authentication file program can be found at the following location.</span><span class="sxs-lookup"><span data-stu-id="4aa46-147">The authentication file program can be found at the following location.</span></span>

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> <span data-ttu-id="4aa46-148">The credentials file must be readable by the omsagent account.</span><span class="sxs-lookup"><span data-stu-id="4aa46-148">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="4aa46-149">Running the mycimprovauth command as omsgent is recommended.</span><span class="sxs-lookup"><span data-stu-id="4aa46-149">Running the mycimprovauth command as omsgent is recommended.</span></span>

<span data-ttu-id="4aa46-150">The following table provides details on the syntax for using mycimprovauth.</span><span class="sxs-lookup"><span data-stu-id="4aa46-150">The following table provides details on the syntax for using mycimprovauth.</span></span>

| <span data-ttu-id="4aa46-151">Operation</span><span class="sxs-lookup"><span data-stu-id="4aa46-151">Operation</span></span> | <span data-ttu-id="4aa46-152">Example</span><span class="sxs-lookup"><span data-stu-id="4aa46-152">Example</span></span> | <span data-ttu-id="4aa46-153">Description</span><span class="sxs-lookup"><span data-stu-id="4aa46-153">Description</span></span>
|:--|:--|:--|
| <span data-ttu-id="4aa46-154">autoupdate *false or true*</span><span class="sxs-lookup"><span data-stu-id="4aa46-154">autoupdate *false or true*</span></span> | <span data-ttu-id="4aa46-155">mycimprovauth autoupdate false</span><span class="sxs-lookup"><span data-stu-id="4aa46-155">mycimprovauth autoupdate false</span></span> | <span data-ttu-id="4aa46-156">Sets whether or not the authentication file will be automatically updated on restart or update.</span><span class="sxs-lookup"><span data-stu-id="4aa46-156">Sets whether or not the authentication file will be automatically updated on restart or update.</span></span> |
| <span data-ttu-id="4aa46-157">default *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="4aa46-157">default *bind-address username password*</span></span> | <span data-ttu-id="4aa46-158">mycimprovauth default 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="4aa46-158">mycimprovauth default 127.0.0.1 root pwd</span></span> | <span data-ttu-id="4aa46-159">Sets the default instance in the MySQL OMI authentication file.</span><span class="sxs-lookup"><span data-stu-id="4aa46-159">Sets the default instance in the MySQL OMI authentication file.</span></span><br><span data-ttu-id="4aa46-160">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded.</span><span class="sxs-lookup"><span data-stu-id="4aa46-160">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded.</span></span> |
| <span data-ttu-id="4aa46-161">delete *default or port_num*</span><span class="sxs-lookup"><span data-stu-id="4aa46-161">delete *default or port_num*</span></span> | <span data-ttu-id="4aa46-162">mycimprovauth 3308</span><span class="sxs-lookup"><span data-stu-id="4aa46-162">mycimprovauth 3308</span></span> | <span data-ttu-id="4aa46-163">Deletes the specified instance by either default or by port number.</span><span class="sxs-lookup"><span data-stu-id="4aa46-163">Deletes the specified instance by either default or by port number.</span></span> |
| <span data-ttu-id="4aa46-164">help</span><span class="sxs-lookup"><span data-stu-id="4aa46-164">help</span></span> | <span data-ttu-id="4aa46-165">mycimprov help</span><span class="sxs-lookup"><span data-stu-id="4aa46-165">mycimprov help</span></span> | <span data-ttu-id="4aa46-166">Prints out a list of commands to use.</span><span class="sxs-lookup"><span data-stu-id="4aa46-166">Prints out a list of commands to use.</span></span> |
| <span data-ttu-id="4aa46-167">print</span><span class="sxs-lookup"><span data-stu-id="4aa46-167">print</span></span> | <span data-ttu-id="4aa46-168">mycimprov print</span><span class="sxs-lookup"><span data-stu-id="4aa46-168">mycimprov print</span></span> | <span data-ttu-id="4aa46-169">Prints out an easy to read MySQL OMI authentication file.</span><span class="sxs-lookup"><span data-stu-id="4aa46-169">Prints out an easy to read MySQL OMI authentication file.</span></span> |
| <span data-ttu-id="4aa46-170">update port_num *bind-address username password*</span><span class="sxs-lookup"><span data-stu-id="4aa46-170">update port_num *bind-address username password*</span></span> | <span data-ttu-id="4aa46-171">mycimprov update 3307 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="4aa46-171">mycimprov update 3307 127.0.0.1 root pwd</span></span> | <span data-ttu-id="4aa46-172">Updates the specified instance or adds the instance if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="4aa46-172">Updates the specified instance or adds the instance if it does not exist.</span></span> |

<span data-ttu-id="4aa46-173">The following example commands define a default user account for the MySQL server on localhost.</span><span class="sxs-lookup"><span data-stu-id="4aa46-173">The following example commands define a default user account for the MySQL server on localhost.</span></span>  <span data-ttu-id="4aa46-174">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded</span><span class="sxs-lookup"><span data-stu-id="4aa46-174">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded</span></span>

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="4aa46-175">Database Permissions Required for MySQL Performance Counters</span><span class="sxs-lookup"><span data-stu-id="4aa46-175">Database Permissions Required for MySQL Performance Counters</span></span>
<span data-ttu-id="4aa46-176">The MySQL User requires access to the following queries to collect MySQL Server performance data.</span><span class="sxs-lookup"><span data-stu-id="4aa46-176">The MySQL User requires access to the following queries to collect MySQL Server performance data.</span></span> 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


<span data-ttu-id="4aa46-177">The MySQL user also requires SELECT access to the following default tables.</span><span class="sxs-lookup"><span data-stu-id="4aa46-177">The MySQL user also requires SELECT access to the following default tables.</span></span>

- <span data-ttu-id="4aa46-178">information_schema</span><span class="sxs-lookup"><span data-stu-id="4aa46-178">information_schema</span></span>
- <span data-ttu-id="4aa46-179">mysql.</span><span class="sxs-lookup"><span data-stu-id="4aa46-179">mysql.</span></span> 

<span data-ttu-id="4aa46-180">These privileges can be granted by running the following grant commands.</span><span class="sxs-lookup"><span data-stu-id="4aa46-180">These privileges can be granted by running the following grant commands.</span></span>

    GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;


> [!NOTE]
> <span data-ttu-id="4aa46-181">To grant permissions to a MySQL monitoring user the granting user must have the ‘GRANT option’ privilege as well as the privilege being granted.</span><span class="sxs-lookup"><span data-stu-id="4aa46-181">To grant permissions to a MySQL monitoring user the granting user must have the ‘GRANT option’ privilege as well as the privilege being granted.</span></span>

### <a name="define-performance-counters"></a><span data-ttu-id="4aa46-182">Define performance counters</span><span class="sxs-lookup"><span data-stu-id="4aa46-182">Define performance counters</span></span>

<span data-ttu-id="4aa46-183">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span><span class="sxs-lookup"><span data-stu-id="4aa46-183">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="4aa46-184">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span><span class="sxs-lookup"><span data-stu-id="4aa46-184">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="4aa46-185">Object Name</span><span class="sxs-lookup"><span data-stu-id="4aa46-185">Object Name</span></span> | <span data-ttu-id="4aa46-186">Counter Name</span><span class="sxs-lookup"><span data-stu-id="4aa46-186">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="4aa46-187">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="4aa46-187">MySQL Database</span></span> | <span data-ttu-id="4aa46-188">Disk Space in Bytes</span><span class="sxs-lookup"><span data-stu-id="4aa46-188">Disk Space in Bytes</span></span> |
| <span data-ttu-id="4aa46-189">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="4aa46-189">MySQL Database</span></span> | <span data-ttu-id="4aa46-190">Tables</span><span class="sxs-lookup"><span data-stu-id="4aa46-190">Tables</span></span> |
| <span data-ttu-id="4aa46-191">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-191">MySQL Server</span></span> | <span data-ttu-id="4aa46-192">Aborted Connection Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-192">Aborted Connection Pct</span></span> |
| <span data-ttu-id="4aa46-193">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-193">MySQL Server</span></span> | <span data-ttu-id="4aa46-194">Connection Use Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-194">Connection Use Pct</span></span> |
| <span data-ttu-id="4aa46-195">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-195">MySQL Server</span></span> | <span data-ttu-id="4aa46-196">Disk Space Use in Bytes</span><span class="sxs-lookup"><span data-stu-id="4aa46-196">Disk Space Use in Bytes</span></span> |
| <span data-ttu-id="4aa46-197">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-197">MySQL Server</span></span> | <span data-ttu-id="4aa46-198">Full Table Scan Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-198">Full Table Scan Pct</span></span> |
| <span data-ttu-id="4aa46-199">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-199">MySQL Server</span></span> | <span data-ttu-id="4aa46-200">InnoDB Buffer Pool Hit Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-200">InnoDB Buffer Pool Hit Pct</span></span> |
| <span data-ttu-id="4aa46-201">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-201">MySQL Server</span></span> | <span data-ttu-id="4aa46-202">InnoDB Buffer Pool Use Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-202">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="4aa46-203">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-203">MySQL Server</span></span> | <span data-ttu-id="4aa46-204">InnoDB Buffer Pool Use Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-204">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="4aa46-205">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-205">MySQL Server</span></span> | <span data-ttu-id="4aa46-206">Key Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-206">Key Cache Hit Pct</span></span> |
| <span data-ttu-id="4aa46-207">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-207">MySQL Server</span></span> | <span data-ttu-id="4aa46-208">Key Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-208">Key Cache Use Pct</span></span> |
| <span data-ttu-id="4aa46-209">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-209">MySQL Server</span></span> | <span data-ttu-id="4aa46-210">Key Cache Write Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-210">Key Cache Write Pct</span></span> |
| <span data-ttu-id="4aa46-211">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-211">MySQL Server</span></span> | <span data-ttu-id="4aa46-212">Query Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-212">Query Cache Hit Pct</span></span> |
| <span data-ttu-id="4aa46-213">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-213">MySQL Server</span></span> | <span data-ttu-id="4aa46-214">Query Cache Prunes Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-214">Query Cache Prunes Pct</span></span> |
| <span data-ttu-id="4aa46-215">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-215">MySQL Server</span></span> | <span data-ttu-id="4aa46-216">Query Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-216">Query Cache Use Pct</span></span> |
| <span data-ttu-id="4aa46-217">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-217">MySQL Server</span></span> | <span data-ttu-id="4aa46-218">Table Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-218">Table Cache Hit Pct</span></span> |
| <span data-ttu-id="4aa46-219">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-219">MySQL Server</span></span> | <span data-ttu-id="4aa46-220">Table Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-220">Table Cache Use Pct</span></span> |
| <span data-ttu-id="4aa46-221">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-221">MySQL Server</span></span> | <span data-ttu-id="4aa46-222">Table Lock Contention Pct</span><span class="sxs-lookup"><span data-stu-id="4aa46-222">Table Lock Contention Pct</span></span> |

## <a name="apache-http-server"></a><span data-ttu-id="4aa46-223">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-223">Apache HTTP Server</span></span> 
<span data-ttu-id="4aa46-224">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server will be automatically installed.</span><span class="sxs-lookup"><span data-stu-id="4aa46-224">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server will be automatically installed.</span></span> <span data-ttu-id="4aa46-225">This provider relies on an Apache module that must be loaded into the Apache HTTP Server in order to access performance data.</span><span class="sxs-lookup"><span data-stu-id="4aa46-225">This provider relies on an Apache module that must be loaded into the Apache HTTP Server in order to access performance data.</span></span> <span data-ttu-id="4aa46-226">The module can be loaded with the following command:</span><span class="sxs-lookup"><span data-stu-id="4aa46-226">The module can be loaded with the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="4aa46-227">To unload the Apache monitoring module, run the following command:</span><span class="sxs-lookup"><span data-stu-id="4aa46-227">To unload the Apache monitoring module, run the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a><span data-ttu-id="4aa46-228">Define performance counters</span><span class="sxs-lookup"><span data-stu-id="4aa46-228">Define performance counters</span></span>

<span data-ttu-id="4aa46-229">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span><span class="sxs-lookup"><span data-stu-id="4aa46-229">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="4aa46-230">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span><span class="sxs-lookup"><span data-stu-id="4aa46-230">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="4aa46-231">Object Name</span><span class="sxs-lookup"><span data-stu-id="4aa46-231">Object Name</span></span> | <span data-ttu-id="4aa46-232">Counter Name</span><span class="sxs-lookup"><span data-stu-id="4aa46-232">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="4aa46-233">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-233">Apache HTTP Server</span></span> | <span data-ttu-id="4aa46-234">Busy Workers</span><span class="sxs-lookup"><span data-stu-id="4aa46-234">Busy Workers</span></span> |
| <span data-ttu-id="4aa46-235">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-235">Apache HTTP Server</span></span> | <span data-ttu-id="4aa46-236">Idle Workers</span><span class="sxs-lookup"><span data-stu-id="4aa46-236">Idle Workers</span></span> |
| <span data-ttu-id="4aa46-237">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-237">Apache HTTP Server</span></span> | <span data-ttu-id="4aa46-238">Pct Busy Workers</span><span class="sxs-lookup"><span data-stu-id="4aa46-238">Pct Busy Workers</span></span> |
| <span data-ttu-id="4aa46-239">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-239">Apache HTTP Server</span></span> | <span data-ttu-id="4aa46-240">Total Pct CPU</span><span class="sxs-lookup"><span data-stu-id="4aa46-240">Total Pct CPU</span></span> |
| <span data-ttu-id="4aa46-241">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="4aa46-241">Apache Virtual Host</span></span> | <span data-ttu-id="4aa46-242">Errors per Minute - Client</span><span class="sxs-lookup"><span data-stu-id="4aa46-242">Errors per Minute - Client</span></span> |
| <span data-ttu-id="4aa46-243">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="4aa46-243">Apache Virtual Host</span></span> | <span data-ttu-id="4aa46-244">Errors per Minute - Server</span><span class="sxs-lookup"><span data-stu-id="4aa46-244">Errors per Minute - Server</span></span> |
| <span data-ttu-id="4aa46-245">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="4aa46-245">Apache Virtual Host</span></span> | <span data-ttu-id="4aa46-246">KB per Request</span><span class="sxs-lookup"><span data-stu-id="4aa46-246">KB per Request</span></span> |
| <span data-ttu-id="4aa46-247">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="4aa46-247">Apache Virtual Host</span></span> | <span data-ttu-id="4aa46-248">Requests KB per Second</span><span class="sxs-lookup"><span data-stu-id="4aa46-248">Requests KB per Second</span></span> |
| <span data-ttu-id="4aa46-249">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="4aa46-249">Apache Virtual Host</span></span> | <span data-ttu-id="4aa46-250">Requests per Second</span><span class="sxs-lookup"><span data-stu-id="4aa46-250">Requests per Second</span></span> |



## <a name="next-steps"></a><span data-ttu-id="4aa46-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="4aa46-251">Next steps</span></span>
* <span data-ttu-id="4aa46-252">[Collect performance counters](log-analytics-data-sources-performance-counters.md) from Linux agents.</span><span class="sxs-lookup"><span data-stu-id="4aa46-252">[Collect performance counters](log-analytics-data-sources-performance-counters.md) from Linux agents.</span></span>
* <span data-ttu-id="4aa46-253">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span><span class="sxs-lookup"><span data-stu-id="4aa46-253">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
