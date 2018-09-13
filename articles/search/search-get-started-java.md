---
title: Get started with Azure Search in Java | Microsoft Docs
description: How to build a hosted cloud search application on Azure using Java as your programming language.
services: search
author: jj09
manager: jlembicz
ms.service: search
ms.topic: conceptual
ms.date: 08/26/2018
ms.author: jjed
ms.openlocfilehash: 6fed5a8afe6030038752d540bfabbc446c57db2c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808566"
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="42809-103">Get started with Azure Search in Java</span><span class="sxs-lookup"><span data-stu-id="42809-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="42809-106">Learn how to build a custom Java search application that uses Azure Search for its search experience.</span><span class="sxs-lookup"><span data-stu-id="42809-106">Learn how to build a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="42809-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span><span class="sxs-lookup"><span data-stu-id="42809-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="42809-108">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42809-108">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="42809-109">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="42809-109">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="42809-110">We used the following software to build and test this sample:</span><span class="sxs-lookup"><span data-stu-id="42809-110">We used the following software to build and test this sample:</span></span>

* <span data-ttu-id="42809-111">[Eclipse IDE for Java EE Developers](https://www.eclipse.org/downloads/packages/release/photon/r/eclipse-ide-java-ee-developers).</span><span class="sxs-lookup"><span data-stu-id="42809-111">[Eclipse IDE for Java EE Developers](https://www.eclipse.org/downloads/packages/release/photon/r/eclipse-ide-java-ee-developers).</span></span> <span data-ttu-id="42809-112">Be sure to download the EE version.</span><span class="sxs-lookup"><span data-stu-id="42809-112">Be sure to download the EE version.</span></span> <span data-ttu-id="42809-113">One of the verification steps requires a feature that is found only in this edition.</span><span class="sxs-lookup"><span data-stu-id="42809-113">One of the verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="42809-114">JDK 8u181</span><span class="sxs-lookup"><span data-stu-id="42809-114">JDK 8u181</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="42809-115">Apache Tomcat 8.5.33</span><span class="sxs-lookup"><span data-stu-id="42809-115">Apache Tomcat 8.5.33</span></span>](https://tomcat.apache.org/download-80.cgi#8.5.33)

## <a name="about-the-data"></a><span data-ttu-id="42809-116">About the data</span><span class="sxs-lookup"><span data-stu-id="42809-116">About the data</span></span>
<span data-ttu-id="42809-117">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span><span class="sxs-lookup"><span data-stu-id="42809-117">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="42809-118">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span><span class="sxs-lookup"><span data-stu-id="42809-118">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="42809-119">In this application, the **SearchServlet.java** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="42809-119">In this application, the **SearchServlet.java** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="42809-120">Predefined credentials and connection  information to the online data source are provided in the program code.</span><span class="sxs-lookup"><span data-stu-id="42809-120">Predefined credentials and connection  information to the online data source are provided in the program code.</span></span> <span data-ttu-id="42809-121">In terms of data access, no further configuration is necessary.</span><span class="sxs-lookup"><span data-stu-id="42809-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier. If you use the standard tier, this limit does not apply, and you can modify this code to use a bigger dataset. For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).
> 
> 

## <a name="about-the-program-files"></a><span data-ttu-id="42809-125">About the program files</span><span class="sxs-lookup"><span data-stu-id="42809-125">About the program files</span></span>
<span data-ttu-id="42809-126">The following list describes the files that are relevant to this sample.</span><span class="sxs-lookup"><span data-stu-id="42809-126">The following list describes the files that are relevant to this sample.</span></span>

* <span data-ttu-id="42809-127">Search.jsp: Provides the user interface</span><span class="sxs-lookup"><span data-stu-id="42809-127">Search.jsp: Provides the user interface</span></span>
* <span data-ttu-id="42809-128">SearchServlet.java: Provides methods (similar to a controller in MVC)</span><span class="sxs-lookup"><span data-stu-id="42809-128">SearchServlet.java: Provides methods (similar to a controller in MVC)</span></span>
* <span data-ttu-id="42809-129">SearchServiceClient.java: Handles HTTP requests</span><span class="sxs-lookup"><span data-stu-id="42809-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="42809-130">SearchServiceHelper.java: A helper class that provides static methods</span><span class="sxs-lookup"><span data-stu-id="42809-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="42809-131">Document.java: Provides the data model</span><span class="sxs-lookup"><span data-stu-id="42809-131">Document.java: Provides the data model</span></span>
* <span data-ttu-id="42809-132">config.properties: Sets the Search service URL and api-key</span><span class="sxs-lookup"><span data-stu-id="42809-132">config.properties: Sets the Search service URL and api-key</span></span>
* <span data-ttu-id="42809-133">pom.xml: A Maven dependency</span><span class="sxs-lookup"><span data-stu-id="42809-133">pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="42809-134">Find the service name and api-key of your Azure Search service</span><span class="sxs-lookup"><span data-stu-id="42809-134">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="42809-135">All REST API calls into Azure Search require that you provide the service URL and an api-key.</span><span class="sxs-lookup"><span data-stu-id="42809-135">All REST API calls into Azure Search require that you provide the service URL and an api-key.</span></span> 

1. <span data-ttu-id="42809-136">Sign in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42809-136">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="42809-137">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span><span class="sxs-lookup"><span data-stu-id="42809-137">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="42809-138">Select the service you want to use.</span><span class="sxs-lookup"><span data-stu-id="42809-138">Select the service you want to use.</span></span>
4. <span data-ttu-id="42809-139">On the service dashboard, you'll see tiles for essential information as well as the key icon for accessing the admin keys.</span><span class="sxs-lookup"><span data-stu-id="42809-139">On the service dashboard, you'll see tiles for essential information as well as the key icon for accessing the admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="42809-140">Copy the service URL and an admin key.</span><span class="sxs-lookup"><span data-stu-id="42809-140">Copy the service URL and an admin key.</span></span> <span data-ttu-id="42809-141">You will need them later, when you add them to the **config.properties** file.</span><span class="sxs-lookup"><span data-stu-id="42809-141">You will need them later, when you add them to the **config.properties** file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="42809-142">Download the sample files</span><span class="sxs-lookup"><span data-stu-id="42809-142">Download the sample files</span></span>
1. <span data-ttu-id="42809-143">Go to [search-java-indexer-demo](https://github.com/Azure-Samples/search-java-indexer-demo) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="42809-143">Go to [search-java-indexer-demo](https://github.com/Azure-Samples/search-java-indexer-demo) on GitHub.</span></span>
2. <span data-ttu-id="42809-144">Click **Download ZIP**, save the .zip file to disk, and then extract all the files it contains.</span><span class="sxs-lookup"><span data-stu-id="42809-144">Click **Download ZIP**, save the .zip file to disk, and then extract all the files it contains.</span></span> <span data-ttu-id="42809-145">Consider extracting the files into your Java workspace to make it easier to find the project later.</span><span class="sxs-lookup"><span data-stu-id="42809-145">Consider extracting the files into your Java workspace to make it easier to find the project later.</span></span>
3. <span data-ttu-id="42809-146">The sample files are read-only.</span><span class="sxs-lookup"><span data-stu-id="42809-146">The sample files are read-only.</span></span> <span data-ttu-id="42809-147">Right-click folder properties and clear the read-only attribute.</span><span class="sxs-lookup"><span data-stu-id="42809-147">Right-click folder properties and clear the read-only attribute.</span></span>

<span data-ttu-id="42809-148">All subsequent file modifications and run statements will be made against files in this folder.</span><span class="sxs-lookup"><span data-stu-id="42809-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="42809-149">Import project</span><span class="sxs-lookup"><span data-stu-id="42809-149">Import project</span></span>
1. <span data-ttu-id="42809-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span><span class="sxs-lookup"><span data-stu-id="42809-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="42809-151">In **Select root directory**, browse to the folder containing sample files.</span><span class="sxs-lookup"><span data-stu-id="42809-151">In **Select root directory**, browse to the folder containing sample files.</span></span> <span data-ttu-id="42809-152">Select the folder that contains the .project folder.</span><span class="sxs-lookup"><span data-stu-id="42809-152">Select the folder that contains the .project folder.</span></span> <span data-ttu-id="42809-153">The project should appear in the **Projects** list as a selected item.</span><span class="sxs-lookup"><span data-stu-id="42809-153">The project should appear in the **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="42809-154">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="42809-154">Click **Finish**.</span></span>
4. <span data-ttu-id="42809-155">Use **Project Explorer** to view and edit the files.</span><span class="sxs-lookup"><span data-stu-id="42809-155">Use **Project Explorer** to view and edit the files.</span></span> <span data-ttu-id="42809-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use the shortcut to open it.</span><span class="sxs-lookup"><span data-stu-id="42809-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use the shortcut to open it.</span></span>

## <a name="configure-the-service-url-and-api-key"></a><span data-ttu-id="42809-157">Configure the service URL and api-key</span><span class="sxs-lookup"><span data-stu-id="42809-157">Configure the service URL and api-key</span></span>
1. <span data-ttu-id="42809-158">In **Project Explorer**, double-click **config.properties** to edit the configuration settings containing the server name and api-key.</span><span class="sxs-lookup"><span data-stu-id="42809-158">In **Project Explorer**, double-click **config.properties** to edit the configuration settings containing the server name and api-key.</span></span>
2. <span data-ttu-id="42809-159">Refer to the steps earlier in this article, where you found the service URL and api-key in the [Azure Portal](https://portal.azure.com), to get the values you will now enter into **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="42809-159">Refer to the steps earlier in this article, where you found the service URL and api-key in the [Azure Portal](https://portal.azure.com), to get the values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="42809-160">In **config.properties**, replace "Api Key" with the api-key for your service.</span><span class="sxs-lookup"><span data-stu-id="42809-160">In **config.properties**, replace "Api Key" with the api-key for your service.</span></span> <span data-ttu-id="42809-161">Next, service name (the first component of the URL http://servicename.search.windows.net) replaces "service name" in the same file.</span><span class="sxs-lookup"><span data-stu-id="42809-161">Next, service name (the first component of the URL http://servicename.search.windows.net) replaces "service name" in the same file.</span></span>
   
    ![][5]

## <a name="configure-the-project-build-and-runtime-environments"></a><span data-ttu-id="42809-162">Configure the project, build and runtime environments</span><span class="sxs-lookup"><span data-stu-id="42809-162">Configure the project, build and runtime environments</span></span>
1. <span data-ttu-id="42809-163">In Eclipse, in Project Explorer, right-click the project > **Properties** > **Project Facets**.</span><span class="sxs-lookup"><span data-stu-id="42809-163">In Eclipse, in Project Explorer, right-click the project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="42809-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="42809-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="42809-165">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="42809-165">Click **Apply**.</span></span>
4. <span data-ttu-id="42809-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span><span class="sxs-lookup"><span data-stu-id="42809-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="42809-167">Expand Apache and select the version of the Apache Tomcat server you previously installed.</span><span class="sxs-lookup"><span data-stu-id="42809-167">Expand Apache and select the version of the Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="42809-168">On our system, we installed version 8.</span><span class="sxs-lookup"><span data-stu-id="42809-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="42809-169">On the next page, specify the Tomcat installation directory.</span><span class="sxs-lookup"><span data-stu-id="42809-169">On the next page, specify the Tomcat installation directory.</span></span> <span data-ttu-id="42809-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span><span class="sxs-lookup"><span data-stu-id="42809-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="42809-171">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="42809-171">Click **Finish**.</span></span>
8. <span data-ttu-id="42809-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="42809-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="42809-173">In **Add JRE**, select **Standard VM**.</span><span class="sxs-lookup"><span data-stu-id="42809-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="42809-174">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="42809-174">Click **Next**.</span></span>
11. <span data-ttu-id="42809-175">In JRE Definition, in JRE home, click **Directory**.</span><span class="sxs-lookup"><span data-stu-id="42809-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="42809-176">Navigate to **Program Files** > **Java** and select the JDK you previously installed.</span><span class="sxs-lookup"><span data-stu-id="42809-176">Navigate to **Program Files** > **Java** and select the JDK you previously installed.</span></span> <span data-ttu-id="42809-177">It's important to select the JDK as the JRE.</span><span class="sxs-lookup"><span data-stu-id="42809-177">It's important to select the JDK as the JRE.</span></span>
13. <span data-ttu-id="42809-178">In Installed JREs, choose the **JDK**.</span><span class="sxs-lookup"><span data-stu-id="42809-178">In Installed JREs, choose the **JDK**.</span></span> <span data-ttu-id="42809-179">Your settings should look similar to the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="42809-179">Your settings should look similar to the following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="42809-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** to open the application in an external browser window.</span><span class="sxs-lookup"><span data-stu-id="42809-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** to open the application in an external browser window.</span></span> <span data-ttu-id="42809-181">Using an external browser gives you a better Web application experience.</span><span class="sxs-lookup"><span data-stu-id="42809-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="42809-182">You have now completed the configuration tasks.</span><span class="sxs-lookup"><span data-stu-id="42809-182">You have now completed the configuration tasks.</span></span> <span data-ttu-id="42809-183">Next, you'll build and run the project.</span><span class="sxs-lookup"><span data-stu-id="42809-183">Next, you'll build and run the project.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="42809-184">Build the project</span><span class="sxs-lookup"><span data-stu-id="42809-184">Build the project</span></span>
1. <span data-ttu-id="42809-185">In Project Explorer, right-click the project name and choose **Run As** > **Maven build...** to configure the project.</span><span class="sxs-lookup"><span data-stu-id="42809-185">In Project Explorer, right-click the project name and choose **Run As** > **Maven build...** to configure the project.</span></span>
   
    ![][10]
2. <span data-ttu-id="42809-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="42809-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="42809-187">Status messages are output to the console window.</span><span class="sxs-lookup"><span data-stu-id="42809-187">Status messages are output to the console window.</span></span> <span data-ttu-id="42809-188">You should see BUILD SUCCESS indicating the project built without errors.</span><span class="sxs-lookup"><span data-stu-id="42809-188">You should see BUILD SUCCESS indicating the project built without errors.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="42809-189">Run the app</span><span class="sxs-lookup"><span data-stu-id="42809-189">Run the app</span></span>
<span data-ttu-id="42809-190">In this last step, you will run the application in a local server runtime environment.</span><span class="sxs-lookup"><span data-stu-id="42809-190">In this last step, you will run the application in a local server runtime environment.</span></span>

<span data-ttu-id="42809-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need to do that first.</span><span class="sxs-lookup"><span data-stu-id="42809-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need to do that first.</span></span>

1. <span data-ttu-id="42809-192">In Project Explorer, expand **WebContent**.</span><span class="sxs-lookup"><span data-stu-id="42809-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="42809-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span><span class="sxs-lookup"><span data-stu-id="42809-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="42809-194">Select the Apache Tomcat server, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="42809-194">Select the Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> If you used a non-default workspace to store your project, you'll need to modify **Run Configuration** to point to the project location to avoid a server start-up error. In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**. Select the Apache Tomcat server. Click **Arguments**. Click **Workspace** or **File System** to set the folder containing the project.
> 
> 

<span data-ttu-id="42809-200">When you run the application, you should see a browser window, providing a search box for entering terms.</span><span class="sxs-lookup"><span data-stu-id="42809-200">When you run the application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="42809-201">Wait about one minute before clicking **Search** to give the service time to create and load the index.</span><span class="sxs-lookup"><span data-stu-id="42809-201">Wait about one minute before clicking **Search** to give the service time to create and load the index.</span></span> <span data-ttu-id="42809-202">If you get an HTTP 404 error, you just need to wait a little bit longer before trying again.</span><span class="sxs-lookup"><span data-stu-id="42809-202">If you get an HTTP 404 error, you just need to wait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="42809-203">Search on USGS data</span><span class="sxs-lookup"><span data-stu-id="42809-203">Search on USGS data</span></span>
<span data-ttu-id="42809-204">The USGS data set includes records that are relevant to the state of Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="42809-204">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="42809-205">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span><span class="sxs-lookup"><span data-stu-id="42809-205">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="42809-206">Entering a search term will give the search engine something to go on.</span><span class="sxs-lookup"><span data-stu-id="42809-206">Entering a search term will give the search engine something to go on.</span></span> <span data-ttu-id="42809-207">Try entering a regional name.</span><span class="sxs-lookup"><span data-stu-id="42809-207">Try entering a regional name.</span></span> <span data-ttu-id="42809-208">"Roger Williams" was the first governor of Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="42809-208">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="42809-209">Numerous parks, buildings, and schools are named after him.</span><span class="sxs-lookup"><span data-stu-id="42809-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="42809-210">You could also try any of these terms:</span><span class="sxs-lookup"><span data-stu-id="42809-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="42809-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="42809-211">Pawtucket</span></span>
* <span data-ttu-id="42809-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="42809-212">Pembroke</span></span>
* <span data-ttu-id="42809-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="42809-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="42809-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="42809-214">Next steps</span></span>
<span data-ttu-id="42809-215">This is the first Azure Search tutorial based on Java and the USGS dataset.</span><span class="sxs-lookup"><span data-stu-id="42809-215">This is the first Azure Search tutorial based on Java and the USGS dataset.</span></span> <span data-ttu-id="42809-216">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span><span class="sxs-lookup"><span data-stu-id="42809-216">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="42809-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting the [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="42809-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting the [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="42809-218">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span><span class="sxs-lookup"><span data-stu-id="42809-218">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="42809-219">New to Azure Search?</span><span class="sxs-lookup"><span data-stu-id="42809-219">New to Azure Search?</span></span> <span data-ttu-id="42809-220">We recommend trying other tutorials to develop an understanding of what you can create.</span><span class="sxs-lookup"><span data-stu-id="42809-220">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="42809-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span><span class="sxs-lookup"><span data-stu-id="42809-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> 

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
