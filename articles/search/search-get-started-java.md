---
title: Get started with Azure Search in Java | Microsoft Docs
description: How to build a hosted cloud search application on Azure using Java as your programming language.
services: search
documentationcenter: ''
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 1c6139fab18cf82bccc188a201ced1ac4a14463c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562909"
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="8c7dc-103">Get started with Azure Search in Java</span><span class="sxs-lookup"><span data-stu-id="8c7dc-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="8c7dc-106">Learn how to build a custom Java search application that uses Azure Search for its search experience.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-106">Learn how to build a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="8c7dc-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="8c7dc-108">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c7dc-108">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="8c7dc-109">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-109">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="8c7dc-110">We used the following software to build and test this sample:</span><span class="sxs-lookup"><span data-stu-id="8c7dc-110">We used the following software to build and test this sample:</span></span>

* <span data-ttu-id="8c7dc-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="8c7dc-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="8c7dc-112">Be sure to download the EE version.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-112">Be sure to download the EE version.</span></span> <span data-ttu-id="8c7dc-113">One of the verification steps requires a feature that is found only in this edition.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-113">One of the verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="8c7dc-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="8c7dc-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="8c7dc-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="8c7dc-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-the-data"></a><span data-ttu-id="8c7dc-116">About the data</span><span class="sxs-lookup"><span data-stu-id="8c7dc-116">About the data</span></span>
<span data-ttu-id="8c7dc-117">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-117">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="8c7dc-118">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-118">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="8c7dc-119">In this application, the **SearchServlet.java** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-119">In this application, the **SearchServlet.java** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="8c7dc-120">Predefined credentials and connection  information to the online data source are provided in the program code.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-120">Predefined credentials and connection  information to the online data source are provided in the program code.</span></span> <span data-ttu-id="8c7dc-121">In terms of data access, no further configuration is necessary.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier. If you use the standard tier, this limit does not apply, and you can modify this code to use a bigger dataset. For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).
> 
> 

## <a name="about-the-program-files"></a><span data-ttu-id="8c7dc-125">About the program files</span><span class="sxs-lookup"><span data-stu-id="8c7dc-125">About the program files</span></span>
<span data-ttu-id="8c7dc-126">The following list describes the files that are relevant to this sample.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-126">The following list describes the files that are relevant to this sample.</span></span>

* <span data-ttu-id="8c7dc-127">Search.jsp: Provides the user interface</span><span class="sxs-lookup"><span data-stu-id="8c7dc-127">Search.jsp: Provides the user interface</span></span>
* <span data-ttu-id="8c7dc-128">SearchServlet.java: Provides methods (similar to a controller in MVC)</span><span class="sxs-lookup"><span data-stu-id="8c7dc-128">SearchServlet.java: Provides methods (similar to a controller in MVC)</span></span>
* <span data-ttu-id="8c7dc-129">SearchServiceClient.java: Handles HTTP requests</span><span class="sxs-lookup"><span data-stu-id="8c7dc-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="8c7dc-130">SearchServiceHelper.java: A helper class that provides static methods</span><span class="sxs-lookup"><span data-stu-id="8c7dc-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="8c7dc-131">Document.java: Provides the data model</span><span class="sxs-lookup"><span data-stu-id="8c7dc-131">Document.java: Provides the data model</span></span>
* <span data-ttu-id="8c7dc-132">config.properties: Sets the Search service URL and api-key</span><span class="sxs-lookup"><span data-stu-id="8c7dc-132">config.properties: Sets the Search service URL and api-key</span></span>
* <span data-ttu-id="8c7dc-133">Pom.xml: A Maven dependency</span><span class="sxs-lookup"><span data-stu-id="8c7dc-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="8c7dc-134">Find the service name and api-key of your Azure Search service</span><span class="sxs-lookup"><span data-stu-id="8c7dc-134">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="8c7dc-135">All REST API calls into Azure Search require that you provide the service URL and an api-key.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-135">All REST API calls into Azure Search require that you provide the service URL and an api-key.</span></span> 

1. <span data-ttu-id="8c7dc-136">Sign in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c7dc-136">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8c7dc-137">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-137">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="8c7dc-138">Select the service you want to use.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-138">Select the service you want to use.</span></span>
4. <span data-ttu-id="8c7dc-139">On the service dashboard, you'll see tiles for essential information as well as the key icon for accessing the admin keys.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-139">On the service dashboard, you'll see tiles for essential information as well as the key icon for accessing the admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="8c7dc-140">Copy the service URL and an admin key.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-140">Copy the service URL and an admin key.</span></span> <span data-ttu-id="8c7dc-141">You will need them later, when you add them to the **config.properties** file.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-141">You will need them later, when you add them to the **config.properties** file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="8c7dc-142">Download the sample files</span><span class="sxs-lookup"><span data-stu-id="8c7dc-142">Download the sample files</span></span>
1. <span data-ttu-id="8c7dc-143">Go to [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-143">Go to [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="8c7dc-144">Click **Download ZIP**, save the .zip file to disk, and then extract all the files it contains.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-144">Click **Download ZIP**, save the .zip file to disk, and then extract all the files it contains.</span></span> <span data-ttu-id="8c7dc-145">Consider extracting the files into your Java workspace to make it easier to find the project later.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-145">Consider extracting the files into your Java workspace to make it easier to find the project later.</span></span>
3. <span data-ttu-id="8c7dc-146">The sample files are read-only.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-146">The sample files are read-only.</span></span> <span data-ttu-id="8c7dc-147">Right-click folder properties and clear the read-only attribute.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-147">Right-click folder properties and clear the read-only attribute.</span></span>

<span data-ttu-id="8c7dc-148">All subsequent file modifications and run statements will be made against files in this folder.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="8c7dc-149">Import project</span><span class="sxs-lookup"><span data-stu-id="8c7dc-149">Import project</span></span>
1. <span data-ttu-id="8c7dc-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="8c7dc-151">In **Select root directory**, browse to the folder containing sample files.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-151">In **Select root directory**, browse to the folder containing sample files.</span></span> <span data-ttu-id="8c7dc-152">Select the folder that contains the .project folder.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-152">Select the folder that contains the .project folder.</span></span> <span data-ttu-id="8c7dc-153">The project should appear in the **Projects** list as a selected item.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-153">The project should appear in the **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="8c7dc-154">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-154">Click **Finish**.</span></span>
4. <span data-ttu-id="8c7dc-155">Use **Project Explorer** to view and edit the files.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-155">Use **Project Explorer** to view and edit the files.</span></span> <span data-ttu-id="8c7dc-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use the shortcut to open it.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use the shortcut to open it.</span></span>

## <a name="configure-the-service-url-and-api-key"></a><span data-ttu-id="8c7dc-157">Configure the service URL and api-key</span><span class="sxs-lookup"><span data-stu-id="8c7dc-157">Configure the service URL and api-key</span></span>
1. <span data-ttu-id="8c7dc-158">In **Project Explorer**, double-click **config.properties** to edit the configuration settings containing the server name and api-key.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-158">In **Project Explorer**, double-click **config.properties** to edit the configuration settings containing the server name and api-key.</span></span>
2. <span data-ttu-id="8c7dc-159">Refer to the steps earlier in this article, where you found the service URL and api-key in the [Azure Portal](https://portal.azure.com), to get the values you will now enter into **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-159">Refer to the steps earlier in this article, where you found the service URL and api-key in the [Azure Portal](https://portal.azure.com), to get the values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="8c7dc-160">In **config.properties**, replace "Api Key" with the api-key for your service.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-160">In **config.properties**, replace "Api Key" with the api-key for your service.</span></span> <span data-ttu-id="8c7dc-161">Next, service name (the first component of the URL http://servicename.search.windows.net) replaces "service name" in the same file.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-161">Next, service name (the first component of the URL http://servicename.search.windows.net) replaces "service name" in the same file.</span></span>
   
    ![][5]

## <a name="configure-the-project-build-and-runtime-environments"></a><span data-ttu-id="8c7dc-162">Configure the project, build and runtime environments</span><span class="sxs-lookup"><span data-stu-id="8c7dc-162">Configure the project, build and runtime environments</span></span>
1. <span data-ttu-id="8c7dc-163">In Eclipse, in Project Explorer, right-click the project > **Properties** > **Project Facets**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-163">In Eclipse, in Project Explorer, right-click the project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="8c7dc-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="8c7dc-165">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-165">Click **Apply**.</span></span>
4. <span data-ttu-id="8c7dc-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="8c7dc-167">Expand Apache and select the version of the Apache Tomcat server you previously installed.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-167">Expand Apache and select the version of the Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="8c7dc-168">On our system, we installed version 8.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="8c7dc-169">On the next page, specify the Tomcat installation directory.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-169">On the next page, specify the Tomcat installation directory.</span></span> <span data-ttu-id="8c7dc-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="8c7dc-171">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-171">Click **Finish**.</span></span>
8. <span data-ttu-id="8c7dc-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="8c7dc-173">In **Add JRE**, select **Standard VM**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="8c7dc-174">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-174">Click **Next**.</span></span>
11. <span data-ttu-id="8c7dc-175">In JRE Definition, in JRE home, click **Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="8c7dc-176">Navigate to **Program Files** > **Java** and select the JDK you previously installed.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-176">Navigate to **Program Files** > **Java** and select the JDK you previously installed.</span></span> <span data-ttu-id="8c7dc-177">It's important to select the JDK as the JRE.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-177">It's important to select the JDK as the JRE.</span></span>
13. <span data-ttu-id="8c7dc-178">In Installed JREs, choose the **JDK**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-178">In Installed JREs, choose the **JDK**.</span></span> <span data-ttu-id="8c7dc-179">Your settings should look similar to the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-179">Your settings should look similar to the following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="8c7dc-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** to open the application in an external browser window.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** to open the application in an external browser window.</span></span> <span data-ttu-id="8c7dc-181">Using an external browser gives you a better Web application experience.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="8c7dc-182">You have now completed the configuration tasks.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-182">You have now completed the configuration tasks.</span></span> <span data-ttu-id="8c7dc-183">Next, you'll build and run the project.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-183">Next, you'll build and run the project.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="8c7dc-184">Build the project</span><span class="sxs-lookup"><span data-stu-id="8c7dc-184">Build the project</span></span>
1. <span data-ttu-id="8c7dc-185">In Project Explorer, right-click the project name and choose **Run As** > **Maven build...** to configure the project.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-185">In Project Explorer, right-click the project name and choose **Run As** > **Maven build...** to configure the project.</span></span>
   
    ![][10]
2. <span data-ttu-id="8c7dc-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="8c7dc-187">Status messages are output to the console window.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-187">Status messages are output to the console window.</span></span> <span data-ttu-id="8c7dc-188">You should see BUILD SUCCESS indicating the project built without errors.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-188">You should see BUILD SUCCESS indicating the project built without errors.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="8c7dc-189">Run the app</span><span class="sxs-lookup"><span data-stu-id="8c7dc-189">Run the app</span></span>
<span data-ttu-id="8c7dc-190">In this last step, you will run the application in a local server runtime environment.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-190">In this last step, you will run the application in a local server runtime environment.</span></span>

<span data-ttu-id="8c7dc-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need to do that first.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need to do that first.</span></span>

1. <span data-ttu-id="8c7dc-192">In Project Explorer, expand **WebContent**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="8c7dc-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="8c7dc-194">Select the Apache Tomcat server, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-194">Select the Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> If you used a non-default workspace to store your project, you'll need to modify **Run Configuration** to point to the project location to avoid a server start-up error. In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**. Select the Apache Tomcat server. Click **Arguments**. Click **Workspace** or **File System** to set the folder containing the project.
> 
> 

<span data-ttu-id="8c7dc-200">When you run the application, you should see a browser window, providing a search box for entering terms.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-200">When you run the application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="8c7dc-201">Wait about one minute before clicking **Search** to give the service time to create and load the index.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-201">Wait about one minute before clicking **Search** to give the service time to create and load the index.</span></span> <span data-ttu-id="8c7dc-202">If you get an HTTP 404 error, you just need to wait a little bit longer before trying again.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-202">If you get an HTTP 404 error, you just need to wait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="8c7dc-203">Search on USGS data</span><span class="sxs-lookup"><span data-stu-id="8c7dc-203">Search on USGS data</span></span>
<span data-ttu-id="8c7dc-204">The USGS data set includes records that are relevant to the state of Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-204">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="8c7dc-205">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-205">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="8c7dc-206">Entering a search term will give the search engine something to go on.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-206">Entering a search term will give the search engine something to go on.</span></span> <span data-ttu-id="8c7dc-207">Try entering a regional name.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-207">Try entering a regional name.</span></span> <span data-ttu-id="8c7dc-208">"Roger Williams" was the first governor of Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-208">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="8c7dc-209">Numerous parks, buildings, and schools are named after him.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="8c7dc-210">You could also try any of these terms:</span><span class="sxs-lookup"><span data-stu-id="8c7dc-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="8c7dc-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="8c7dc-211">Pawtucket</span></span>
* <span data-ttu-id="8c7dc-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="8c7dc-212">Pembroke</span></span>
* <span data-ttu-id="8c7dc-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="8c7dc-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c7dc-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c7dc-214">Next steps</span></span>
<span data-ttu-id="8c7dc-215">This is the first Azure Search tutorial based on Java and the USGS dataset.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-215">This is the first Azure Search tutorial based on Java and the USGS dataset.</span></span> <span data-ttu-id="8c7dc-216">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-216">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="8c7dc-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting the [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="8c7dc-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting the [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="8c7dc-218">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-218">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="8c7dc-219">New to Azure Search?</span><span class="sxs-lookup"><span data-stu-id="8c7dc-219">New to Azure Search?</span></span> <span data-ttu-id="8c7dc-220">We recommend trying other tutorials to develop an understanding of what you can create.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-220">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="8c7dc-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="8c7dc-222">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span><span class="sxs-lookup"><span data-stu-id="8c7dc-222">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/create-search-portal-1.PNG
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/create-search-portal-21.PNG
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/create-search-portal-31.PNG
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-java/AzSearch-Java-SelectProject.png












