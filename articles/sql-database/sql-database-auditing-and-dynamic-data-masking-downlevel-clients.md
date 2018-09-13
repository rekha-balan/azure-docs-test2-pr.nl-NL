---
title: Auditing, TDS redirection, and IP endpoints for Azure SQL Database | Microsoft Docs
description: Learn about auditing, TDS redirctioni and IP endpoint changes when implementing table auditing in Azure SQL Database.
services: sql-database
documentationcenter: ''
author: ronitr
manager: jhubbard
editor: ''
ms.assetid: 4ef19ed1-e798-43a2-ad99-0e563f93ab53
ms.service: sql-database
ms.custom: security-protect
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: ronitr
ms.openlocfilehash: 7fc79af9b9cdbed8cd90aa85bf297d6d96729121
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555521"
---
# <a name="sql-database----downlevel-clients-support-and-ip-endpoint-changes-for-auditing"></a><span data-ttu-id="f3e90-103">SQL Database -  Downlevel clients support and IP endpoint changes for Auditing</span><span class="sxs-lookup"><span data-stu-id="f3e90-103">SQL Database -  Downlevel clients support and IP endpoint changes for Auditing</span></span>
<span data-ttu-id="f3e90-104">[Database Auditing](sql-database-auditing.md) works automatically with SQL clients that support TDS redirection.</span><span class="sxs-lookup"><span data-stu-id="f3e90-104">[Database Auditing](sql-database-auditing.md) works automatically with SQL clients that support TDS redirection.</span></span> <span data-ttu-id="f3e90-105">Note that redirection does not apply when using the Blob Auditing method.</span><span class="sxs-lookup"><span data-stu-id="f3e90-105">Note that redirection does not apply when using the Blob Auditing method.</span></span>

## <a id="subheading-1"></a><span data-ttu-id="f3e90-106">Downlevel clients support</span><span class="sxs-lookup"><span data-stu-id="f3e90-106">Downlevel clients support</span></span>
<span data-ttu-id="f3e90-107">Any client which implements TDS 7.4 should also support redirection.</span><span class="sxs-lookup"><span data-stu-id="f3e90-107">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="f3e90-108">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span><span class="sxs-lookup"><span data-stu-id="f3e90-108">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="f3e90-109">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span><span class="sxs-lookup"><span data-stu-id="f3e90-109">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="f3e90-110">Original server FQDN in the connection string: <*server name*>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="f3e90-110">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="f3e90-111">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="f3e90-111">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="f3e90-112">A partial list of "Downlevel clients" includes:</span><span class="sxs-lookup"><span data-stu-id="f3e90-112">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="f3e90-113">.NET 4.0 and below,</span><span class="sxs-lookup"><span data-stu-id="f3e90-113">.NET 4.0 and below,</span></span>
* <span data-ttu-id="f3e90-114">ODBC 10.0 and below.</span><span class="sxs-lookup"><span data-stu-id="f3e90-114">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="f3e90-115">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span><span class="sxs-lookup"><span data-stu-id="f3e90-115">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="f3e90-116">Tedious (for Node.JS)</span><span class="sxs-lookup"><span data-stu-id="f3e90-116">Tedious (for Node.JS)</span></span>

<span data-ttu-id="f3e90-117">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span><span class="sxs-lookup"><span data-stu-id="f3e90-117">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>

## <a id="subheading-2"></a><span data-ttu-id="f3e90-118">IP endpoint changes when enabling Auditing</span><span class="sxs-lookup"><span data-stu-id="f3e90-118">IP endpoint changes when enabling Auditing</span></span>
<span data-ttu-id="f3e90-119">Please note that when you enable Table Auditing, the IP endpoint of your database will change.</span><span class="sxs-lookup"><span data-stu-id="f3e90-119">Please note that when you enable Table Auditing, the IP endpoint of your database will change.</span></span> <span data-ttu-id="f3e90-120">If you have strict firewall settings, please update those firewall settings accordingly.</span><span class="sxs-lookup"><span data-stu-id="f3e90-120">If you have strict firewall settings, please update those firewall settings accordingly.</span></span>

<span data-ttu-id="f3e90-121">The new database IP endpoint will depend on the database region:</span><span class="sxs-lookup"><span data-stu-id="f3e90-121">The new database IP endpoint will depend on the database region:</span></span>

| <span data-ttu-id="f3e90-122">Database Region</span><span class="sxs-lookup"><span data-stu-id="f3e90-122">Database Region</span></span> | <span data-ttu-id="f3e90-123">Possible IP endpoints</span><span class="sxs-lookup"><span data-stu-id="f3e90-123">Possible IP endpoints</span></span> |
| --- | --- |
| <span data-ttu-id="f3e90-124">China North</span><span class="sxs-lookup"><span data-stu-id="f3e90-124">China North</span></span> |<span data-ttu-id="f3e90-125">139.217.29.176, 139.217.28.254</span><span class="sxs-lookup"><span data-stu-id="f3e90-125">139.217.29.176, 139.217.28.254</span></span> |
| <span data-ttu-id="f3e90-126">China East</span><span class="sxs-lookup"><span data-stu-id="f3e90-126">China East</span></span> |<span data-ttu-id="f3e90-127">42.159.245.65, 42.159.246.245</span><span class="sxs-lookup"><span data-stu-id="f3e90-127">42.159.245.65, 42.159.246.245</span></span> |
| <span data-ttu-id="f3e90-128">Australia East</span><span class="sxs-lookup"><span data-stu-id="f3e90-128">Australia East</span></span> |<span data-ttu-id="f3e90-129">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span><span class="sxs-lookup"><span data-stu-id="f3e90-129">104.210.91.32, 40.126.244.159, 191.239.64.60, 40.126.255.94</span></span> |
| <span data-ttu-id="f3e90-130">Australia Southeast</span><span class="sxs-lookup"><span data-stu-id="f3e90-130">Australia Southeast</span></span> |<span data-ttu-id="f3e90-131">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span><span class="sxs-lookup"><span data-stu-id="f3e90-131">191.239.184.223, 40.127.85.81, 191.239.161.83, 40.127.81.130</span></span> |
| <span data-ttu-id="f3e90-132">Brazil South</span><span class="sxs-lookup"><span data-stu-id="f3e90-132">Brazil South</span></span> |<span data-ttu-id="f3e90-133">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span><span class="sxs-lookup"><span data-stu-id="f3e90-133">104.41.44.161, 104.41.62.230, 23.97.99.54, 104.41.59.191</span></span> |
| <span data-ttu-id="f3e90-134">Central US</span><span class="sxs-lookup"><span data-stu-id="f3e90-134">Central US</span></span> |<span data-ttu-id="f3e90-135">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span><span class="sxs-lookup"><span data-stu-id="f3e90-135">104.43.255.70, 40.83.14.7, 23.99.128.244, 40.83.15.176</span></span> |
| <span data-ttu-id="f3e90-136">Central US EUAP</span><span class="sxs-lookup"><span data-stu-id="f3e90-136">Central US EUAP</span></span> |<span data-ttu-id="f3e90-137">52.180.178.16, 52.180.176.190</span><span class="sxs-lookup"><span data-stu-id="f3e90-137">52.180.178.16, 52.180.176.190</span></span> |
| <span data-ttu-id="f3e90-138">East Asia</span><span class="sxs-lookup"><span data-stu-id="f3e90-138">East Asia</span></span> |<span data-ttu-id="f3e90-139">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span><span class="sxs-lookup"><span data-stu-id="f3e90-139">23.99.125.133, 13.75.40.42, 23.97.71.138, 13.94.43.245</span></span> |
| <span data-ttu-id="f3e90-140">East US 2</span><span class="sxs-lookup"><span data-stu-id="f3e90-140">East US 2</span></span> |<span data-ttu-id="f3e90-141">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span><span class="sxs-lookup"><span data-stu-id="f3e90-141">104.209.141.31, 104.208.238.177, 191.237.131.51, 104.208.235.50</span></span> |
| <span data-ttu-id="f3e90-142">East US</span><span class="sxs-lookup"><span data-stu-id="f3e90-142">East US</span></span> |<span data-ttu-id="f3e90-143">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span><span class="sxs-lookup"><span data-stu-id="f3e90-143">23.96.107.223, 104.41.150.122, 23.96.38.170, 104.41.146.44</span></span> |
| <span data-ttu-id="f3e90-144">East US EUAP</span><span class="sxs-lookup"><span data-stu-id="f3e90-144">East US EUAP</span></span> |<span data-ttu-id="f3e90-145">52.225.190.86, 52.225.191.187</span><span class="sxs-lookup"><span data-stu-id="f3e90-145">52.225.190.86, 52.225.191.187</span></span> |
| <span data-ttu-id="f3e90-146">Central India</span><span class="sxs-lookup"><span data-stu-id="f3e90-146">Central India</span></span> |<span data-ttu-id="f3e90-147">104.211.98.219, 104.211.103.71</span><span class="sxs-lookup"><span data-stu-id="f3e90-147">104.211.98.219, 104.211.103.71</span></span> |
| <span data-ttu-id="f3e90-148">South India</span><span class="sxs-lookup"><span data-stu-id="f3e90-148">South India</span></span> |<span data-ttu-id="f3e90-149">104.211.227.102, 104.211.225.157</span><span class="sxs-lookup"><span data-stu-id="f3e90-149">104.211.227.102, 104.211.225.157</span></span> |
| <span data-ttu-id="f3e90-150">West India</span><span class="sxs-lookup"><span data-stu-id="f3e90-150">West India</span></span> |<span data-ttu-id="f3e90-151">104.211.161.152, 104.211.162.21</span><span class="sxs-lookup"><span data-stu-id="f3e90-151">104.211.161.152, 104.211.162.21</span></span> |
| <span data-ttu-id="f3e90-152">Japan East</span><span class="sxs-lookup"><span data-stu-id="f3e90-152">Japan East</span></span> |<span data-ttu-id="f3e90-153">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span><span class="sxs-lookup"><span data-stu-id="f3e90-153">104.41.179.1, 40.115.253.81, 23.102.64.207, 40.115.250.196</span></span> |
| <span data-ttu-id="f3e90-154">Japan West</span><span class="sxs-lookup"><span data-stu-id="f3e90-154">Japan West</span></span> |<span data-ttu-id="f3e90-155">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span><span class="sxs-lookup"><span data-stu-id="f3e90-155">104.214.140.140, 104.214.146.31, 191.233.32.34, 104.214.146.198</span></span> |
| <span data-ttu-id="f3e90-156">North Central US</span><span class="sxs-lookup"><span data-stu-id="f3e90-156">North Central US</span></span> |<span data-ttu-id="f3e90-157">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span><span class="sxs-lookup"><span data-stu-id="f3e90-157">191.236.155.178, 23.96.192.130, 23.96.177.169, 23.96.193.231</span></span> |
| <span data-ttu-id="f3e90-158">North Europe</span><span class="sxs-lookup"><span data-stu-id="f3e90-158">North Europe</span></span> |<span data-ttu-id="f3e90-159">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span><span class="sxs-lookup"><span data-stu-id="f3e90-159">104.41.209.221, 40.85.139.245, 137.116.251.66, 40.85.142.176</span></span> |
| <span data-ttu-id="f3e90-160">South Central US</span><span class="sxs-lookup"><span data-stu-id="f3e90-160">South Central US</span></span> |<span data-ttu-id="f3e90-161">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span><span class="sxs-lookup"><span data-stu-id="f3e90-161">191.238.184.128, 40.84.190.84, 23.102.160.153, 40.84.186.66</span></span> |
| <span data-ttu-id="f3e90-162">Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="f3e90-162">Southeast Asia</span></span> |<span data-ttu-id="f3e90-163">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span><span class="sxs-lookup"><span data-stu-id="f3e90-163">104.215.198.156, 13.76.252.200, 23.97.51.109, 13.76.252.113</span></span> |
| <span data-ttu-id="f3e90-164">West Europe</span><span class="sxs-lookup"><span data-stu-id="f3e90-164">West Europe</span></span> |<span data-ttu-id="f3e90-165">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span><span class="sxs-lookup"><span data-stu-id="f3e90-165">104.40.230.120, 13.80.23.64, 137.117.171.161, 13.80.8.37, 104.47.167.215, 40.118.56.193, 104.40.176.73, 40.118.56.20</span></span> |
| <span data-ttu-id="f3e90-166">West US</span><span class="sxs-lookup"><span data-stu-id="f3e90-166">West US</span></span> |<span data-ttu-id="f3e90-167">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span><span class="sxs-lookup"><span data-stu-id="f3e90-167">191.236.123.146, 138.91.163.240, 168.62.194.148, 23.99.6.91</span></span> |
| <span data-ttu-id="f3e90-168">West US 2</span><span class="sxs-lookup"><span data-stu-id="f3e90-168">West US 2</span></span> |<span data-ttu-id="f3e90-169">13.66.224.156, 13.66.227.8</span><span class="sxs-lookup"><span data-stu-id="f3e90-169">13.66.224.156, 13.66.227.8</span></span> |
| <span data-ttu-id="f3e90-170">West Central US</span><span class="sxs-lookup"><span data-stu-id="f3e90-170">West Central US</span></span> |<span data-ttu-id="f3e90-171">52.161.29.186, 52.161.27.213</span><span class="sxs-lookup"><span data-stu-id="f3e90-171">52.161.29.186, 52.161.27.213</span></span> |
| <span data-ttu-id="f3e90-172">Canada Central</span><span class="sxs-lookup"><span data-stu-id="f3e90-172">Canada Central</span></span> |<span data-ttu-id="f3e90-173">13.88.248.106, 13.88.248.110</span><span class="sxs-lookup"><span data-stu-id="f3e90-173">13.88.248.106, 13.88.248.110</span></span> |
| <span data-ttu-id="f3e90-174">Canada East</span><span class="sxs-lookup"><span data-stu-id="f3e90-174">Canada East</span></span> |<span data-ttu-id="f3e90-175">40.86.227.82, 40.86.225.194</span><span class="sxs-lookup"><span data-stu-id="f3e90-175">40.86.227.82, 40.86.225.194</span></span> |
| <span data-ttu-id="f3e90-176">UK North</span><span class="sxs-lookup"><span data-stu-id="f3e90-176">UK North</span></span> |<span data-ttu-id="f3e90-177">13.87.101.18, 13.87.100.232</span><span class="sxs-lookup"><span data-stu-id="f3e90-177">13.87.101.18, 13.87.100.232</span></span> |
| <span data-ttu-id="f3e90-178">UK South 2</span><span class="sxs-lookup"><span data-stu-id="f3e90-178">UK South 2</span></span> |<span data-ttu-id="f3e90-179">13.87.32.202, 13.87.32.226</span><span class="sxs-lookup"><span data-stu-id="f3e90-179">13.87.32.202, 13.87.32.226</span></span> |
