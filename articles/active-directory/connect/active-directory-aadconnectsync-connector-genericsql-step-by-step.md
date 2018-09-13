---
title: Generic SQL Connector step-by step | Microsoft Docs
description: This article is walking you through a simple HR system step-by-step using the Generic SQL Connector.
services: active-directory
documentationcenter: ''
author: AndKjell
manager: femila
editor: ''
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: 70d74e0b6738785c4d2fc1e63f5bd1614eded67f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554530"
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="913c4-103">Generic SQL Connector step-by-step</span><span class="sxs-lookup"><span data-stu-id="913c4-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="913c4-104">This topic is a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="913c4-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="913c4-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span><span class="sxs-lookup"><span data-stu-id="913c4-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="913c4-106">Prepare the sample database</span><span class="sxs-lookup"><span data-stu-id="913c4-106">Prepare the sample database</span></span>
<span data-ttu-id="913c4-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="913c4-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="913c4-108">The object model for the created database looks like this picture:</span><span class="sxs-lookup"><span data-stu-id="913c4-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="913c4-109">![Object Model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-109">![Object Model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="913c4-110">Also create a user you want to use to connect to the database.</span><span class="sxs-lookup"><span data-stu-id="913c4-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="913c4-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span><span class="sxs-lookup"><span data-stu-id="913c4-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="913c4-112">Create the ODBC connection file</span><span class="sxs-lookup"><span data-stu-id="913c4-112">Create the ODBC connection file</span></span>
<span data-ttu-id="913c4-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span><span class="sxs-lookup"><span data-stu-id="913c4-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="913c4-114">First we need to create a file with the ODBC connection information.</span><span class="sxs-lookup"><span data-stu-id="913c4-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="913c4-115">Start the ODBC management utility on your server:</span><span class="sxs-lookup"><span data-stu-id="913c4-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="913c4-117">Select the tab **File DSN**.</span><span class="sxs-lookup"><span data-stu-id="913c4-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="913c4-118">Click **Add...**.</span><span class="sxs-lookup"><span data-stu-id="913c4-118">Click **Add...**.</span></span>  
   <span data-ttu-id="913c4-119">![ODBC1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-119">![ODBC1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="913c4-120">The out-of-box driver works fine, so select it and click **Next>**.</span><span class="sxs-lookup"><span data-stu-id="913c4-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="913c4-121">![ODBC2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-121">![ODBC2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="913c4-122">Give the file a name, such as **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="913c4-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="913c4-123">![ODBC3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-123">![ODBC3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="913c4-124">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="913c4-124">Click **Finish**.</span></span>  
   <span data-ttu-id="913c4-125">![ODBC4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-125">![ODBC4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="913c4-126">Time to configure the connection.</span><span class="sxs-lookup"><span data-stu-id="913c4-126">Time to configure the connection.</span></span> <span data-ttu-id="913c4-127">Give the data source a good description and provide the name of the server running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="913c4-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="913c4-129">Select how to authenticate with SQL.</span><span class="sxs-lookup"><span data-stu-id="913c4-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="913c4-130">In this case, we use Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="913c4-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="913c4-132">Provide the name of the sample database, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="913c4-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="913c4-133">![ODBC7](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-133">![ODBC7](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="913c4-134">Keep everything default on this screen.</span><span class="sxs-lookup"><span data-stu-id="913c4-134">Keep everything default on this screen.</span></span> <span data-ttu-id="913c4-135">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="913c4-135">Click **Finish**.</span></span>  
   <span data-ttu-id="913c4-136">![ODBC8](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-136">![ODBC8](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="913c4-137">To verify everything is working as expected, click **Test Data Source**.</span><span class="sxs-lookup"><span data-stu-id="913c4-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="913c4-138">![ODBC9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-138">![ODBC9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="913c4-139">Make sure the test is successful.</span><span class="sxs-lookup"><span data-stu-id="913c4-139">Make sure the test is successful.</span></span>  
    ![ODBC10](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="913c4-141">The ODBC configuration file should now be visible in File DSN.</span><span class="sxs-lookup"><span data-stu-id="913c4-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="913c4-143">We now have the file we need and can start creating the Connector.</span><span class="sxs-lookup"><span data-stu-id="913c4-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="913c4-144">Create the Generic SQL Connector</span><span class="sxs-lookup"><span data-stu-id="913c4-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="913c4-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span><span class="sxs-lookup"><span data-stu-id="913c4-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="913c4-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span><span class="sxs-lookup"><span data-stu-id="913c4-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="913c4-147">![Connector1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-147">![Connector1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="913c4-148">Find the DSN file you created in the previous section and upload it to the server.</span><span class="sxs-lookup"><span data-stu-id="913c4-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="913c4-149">Provide the credentials to connect to the database.</span><span class="sxs-lookup"><span data-stu-id="913c4-149">Provide the credentials to connect to the database.</span></span>  
   ![Connector2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="913c4-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span><span class="sxs-lookup"><span data-stu-id="913c4-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="913c4-152">![Connector3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-152">![Connector3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="913c4-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span><span class="sxs-lookup"><span data-stu-id="913c4-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="913c4-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span><span class="sxs-lookup"><span data-stu-id="913c4-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="913c4-155">![Connector4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-155">![Connector4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="913c4-156">Time to define the anchor attribute and the DN attribute.</span><span class="sxs-lookup"><span data-stu-id="913c4-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="913c4-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="913c4-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="913c4-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span><span class="sxs-lookup"><span data-stu-id="913c4-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="913c4-159">![Connector5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-159">![Connector5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="913c4-160">Not all attribute types can be detected in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="913c4-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="913c4-161">The reference attribute type in particular cannot.</span><span class="sxs-lookup"><span data-stu-id="913c4-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="913c4-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span><span class="sxs-lookup"><span data-stu-id="913c4-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connector6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="913c4-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span><span class="sxs-lookup"><span data-stu-id="913c4-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="913c4-165">In our case, the User object type.</span><span class="sxs-lookup"><span data-stu-id="913c4-165">In our case, the User object type.</span></span>  
   ![Connector7](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="913c4-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span><span class="sxs-lookup"><span data-stu-id="913c4-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="913c4-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span><span class="sxs-lookup"><span data-stu-id="913c4-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="913c4-169">![Connector8](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-169">![Connector8](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="913c4-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span><span class="sxs-lookup"><span data-stu-id="913c4-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="913c4-171">![Connector9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-171">![Connector9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="913c4-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span><span class="sxs-lookup"><span data-stu-id="913c4-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="913c4-173">On the **Configure Anchors** page, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="913c4-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="913c4-174">Create Run Profiles</span><span class="sxs-lookup"><span data-stu-id="913c4-174">Create Run Profiles</span></span>
1. <span data-ttu-id="913c4-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span><span class="sxs-lookup"><span data-stu-id="913c4-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="913c4-176">Click **New Profile**.</span><span class="sxs-lookup"><span data-stu-id="913c4-176">Click **New Profile**.</span></span> <span data-ttu-id="913c4-177">We start with **Full Import**.</span><span class="sxs-lookup"><span data-stu-id="913c4-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="913c4-178">![Runprofile1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-178">![Runprofile1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="913c4-179">Select the type **Full Import (Stage Only)**.</span><span class="sxs-lookup"><span data-stu-id="913c4-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="913c4-180">![Runprofile2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-180">![Runprofile2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="913c4-181">Select the partition **OBJECT=User**.</span><span class="sxs-lookup"><span data-stu-id="913c4-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="913c4-182">![Runprofile3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-182">![Runprofile3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="913c4-183">Select **Table** and type **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="913c4-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="913c4-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span><span class="sxs-lookup"><span data-stu-id="913c4-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="913c4-185">Select **Finish** to save the step.</span><span class="sxs-lookup"><span data-stu-id="913c4-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="913c4-186">![Runprofile4a](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-186">![Runprofile4a](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="913c4-187">![Runprofile4b](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-187">![Runprofile4b](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="913c4-188">Select **New Step**.</span><span class="sxs-lookup"><span data-stu-id="913c4-188">Select **New Step**.</span></span> <span data-ttu-id="913c4-189">This time, select **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="913c4-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="913c4-190">On the last page, use the configuration as in the following picture.</span><span class="sxs-lookup"><span data-stu-id="913c4-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="913c4-191">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="913c4-191">Click **Finish**.</span></span>  
   <span data-ttu-id="913c4-192">![Runprofile5a](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-192">![Runprofile5a](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="913c4-193">![Runprofile5b](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="913c4-193">![Runprofile5b](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="913c4-194">Optional: If you want to, you can configure additional run profiles.</span><span class="sxs-lookup"><span data-stu-id="913c4-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="913c4-195">For this walkthrough, only the Full Import is used.</span><span class="sxs-lookup"><span data-stu-id="913c4-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="913c4-196">Click **OK** to finish changing run profiles.</span><span class="sxs-lookup"><span data-stu-id="913c4-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="913c4-197">Add some test data and test the import</span><span class="sxs-lookup"><span data-stu-id="913c4-197">Add some test data and test the import</span></span>
<span data-ttu-id="913c4-198">Fill out some test data in your sample database.</span><span class="sxs-lookup"><span data-stu-id="913c4-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="913c4-199">When you are ready, select **Run** and **Full import**.</span><span class="sxs-lookup"><span data-stu-id="913c4-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="913c4-200">Here is a user with two phone numbers and a group with some members.</span><span class="sxs-lookup"><span data-stu-id="913c4-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="913c4-203">Appendix A</span><span class="sxs-lookup"><span data-stu-id="913c4-203">Appendix A</span></span>
<span data-ttu-id="913c4-204">**SQL script to create the sample database**</span><span class="sxs-lookup"><span data-stu-id="913c4-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```































