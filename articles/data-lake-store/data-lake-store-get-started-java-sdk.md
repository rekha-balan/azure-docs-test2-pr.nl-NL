---
title: Use the Java SDK to develop applications in Azure Data Lake Store | Microsoft Docs
description: Use Azure Data Lake Store Java SDK to create a Data Lake Store account and perform basic operations in the Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/03/2017
ms.author: nitinme
ms.openlocfilehash: 7e1d596739e6c548349827ff79b76cc0312bc4df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556220"
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="2f214-103">Get started with Azure Data Lake Store using Java</span><span class="sxs-lookup"><span data-stu-id="2f214-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI](data-lake-store-get-started-cli.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="2f214-113">Learn how to use the Azure Data Lake Store Java SDK to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f214-113">Learn how to use the Azure Data Lake Store Java SDK to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="2f214-114">You can access the Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="2f214-114">You can access the Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f214-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f214-115">Prerequisites</span></span>
* <span data-ttu-id="2f214-116">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span><span class="sxs-lookup"><span data-stu-id="2f214-116">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="2f214-117">Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2f214-117">Azure Data Lake Store account.</span></span> <span data-ttu-id="2f214-118">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2f214-118">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="2f214-119">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="2f214-119">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="2f214-120">This tutorial uses Maven for build and project dependencies.</span><span class="sxs-lookup"><span data-stu-id="2f214-120">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="2f214-121">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span><span class="sxs-lookup"><span data-stu-id="2f214-121">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>
* <span data-ttu-id="2f214-122">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span><span class="sxs-lookup"><span data-stu-id="2f214-122">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="2f214-123">How do I authenticate using Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f214-123">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="2f214-124">In this tutorial we use a Azure AD application client secret to retrieve an Azure Active Directory token (service-to-service authentication).</span><span class="sxs-lookup"><span data-stu-id="2f214-124">In this tutorial we use a Azure AD application client secret to retrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="2f214-125">We use this token to create an Data Lake Store client object to perform operations file and directory operations.</span><span class="sxs-lookup"><span data-stu-id="2f214-125">We use this token to create an Data Lake Store client object to perform operations file and directory operations.</span></span> <span data-ttu-id="2f214-126">For instructions on how to authenticate with Azure Data Lake Store using the client secret, we perform the following high-level steps:</span><span class="sxs-lookup"><span data-stu-id="2f214-126">For instructions on how to authenticate with Azure Data Lake Store using the client secret, we perform the following high-level steps:</span></span>

1. <span data-ttu-id="2f214-127">Create an Azure AD web application</span><span class="sxs-lookup"><span data-stu-id="2f214-127">Create an Azure AD web application</span></span>
2. <span data-ttu-id="2f214-128">Retrieve the client ID, client secret, and token endpoint for the Azure AD web application.</span><span class="sxs-lookup"><span data-stu-id="2f214-128">Retrieve the client ID, client secret, and token endpoint for the Azure AD web application.</span></span>
3. <span data-ttu-id="2f214-129">Configure access for the Azure AD web application on the Data Lake Store file/folder that you want to access from the Java application you are creating.</span><span class="sxs-lookup"><span data-stu-id="2f214-129">Configure access for the Azure AD web application on the Data Lake Store file/folder that you want to access from the Java application you are creating.</span></span>

<span data-ttu-id="2f214-130">For instructions on how to perform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="2f214-130">For instructions on how to perform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="2f214-131">Azure Active Directory provides other options as well to retrieve a token.</span><span class="sxs-lookup"><span data-stu-id="2f214-131">Azure Active Directory provides other options as well to retrieve a token.</span></span> <span data-ttu-id="2f214-132">You can pick from a number of different authentication mechanisms to suit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f214-132">You can pick from a number of different authentication mechanisms to suit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="2f214-133">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you to synchronize your on-premises Active Directory users with the cloud.</span><span class="sxs-lookup"><span data-stu-id="2f214-133">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you to synchronize your on-premises Active Directory users with the cloud.</span></span> <span data-ttu-id="2f214-134">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="2f214-134">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="2f214-135">Create a Java application</span><span class="sxs-lookup"><span data-stu-id="2f214-135">Create a Java application</span></span>
<span data-ttu-id="2f214-136">The code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span><span class="sxs-lookup"><span data-stu-id="2f214-136">The code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span></span> <span data-ttu-id="2f214-137">This section of the article walk you through the main parts of the code.</span><span class="sxs-lookup"><span data-stu-id="2f214-137">This section of the article walk you through the main parts of the code.</span></span>

1. <span data-ttu-id="2f214-138">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command-line or using an IDE.</span><span class="sxs-lookup"><span data-stu-id="2f214-138">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command-line or using an IDE.</span></span> <span data-ttu-id="2f214-139">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="2f214-139">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="2f214-140">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="2f214-140">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="2f214-141">Add the following dependencies to your Maven **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="2f214-141">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="2f214-142">Add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span><span class="sxs-lookup"><span data-stu-id="2f214-142">Add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.4</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    <span data-ttu-id="2f214-143">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span><span class="sxs-lookup"><span data-stu-id="2f214-143">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="2f214-144">The second dependency (`slf4j-nop`) is to specify which logging framework to use for this application.</span><span class="sxs-lookup"><span data-stu-id="2f214-144">The second dependency (`slf4j-nop`) is to specify which logging framework to use for this application.</span></span> <span data-ttu-id="2f214-145">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span><span class="sxs-lookup"><span data-stu-id="2f214-145">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="2f214-146">For this example, we will disable logging, hence we use the **slf4j-nop** binding.</span><span class="sxs-lookup"><span data-stu-id="2f214-146">For this example, we will disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="2f214-147">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="2f214-147">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-the-application-code"></a><span data-ttu-id="2f214-148">Add the application code</span><span class="sxs-lookup"><span data-stu-id="2f214-148">Add the application code</span></span>
<span data-ttu-id="2f214-149">There are three main parts to the code.</span><span class="sxs-lookup"><span data-stu-id="2f214-149">There are three main parts to the code.</span></span>

1. <span data-ttu-id="2f214-150">Obtain the Azure Active Directory token</span><span class="sxs-lookup"><span data-stu-id="2f214-150">Obtain the Azure Active Directory token</span></span>
2. <span data-ttu-id="2f214-151">Use the token to create a Data Lake Store client.</span><span class="sxs-lookup"><span data-stu-id="2f214-151">Use the token to create a Data Lake Store client.</span></span>
3. <span data-ttu-id="2f214-152">Use the Data Lake Store client to perform operations.</span><span class="sxs-lookup"><span data-stu-id="2f214-152">Use the Data Lake Store client to perform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="2f214-153">Step 1: Obtain an Azure Active Directory token.</span><span class="sxs-lookup"><span data-stu-id="2f214-153">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="2f214-154">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="2f214-154">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="2f214-155">However, the SDK does not mandate that only these methods be used.</span><span class="sxs-lookup"><span data-stu-id="2f214-155">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="2f214-156">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span><span class="sxs-lookup"><span data-stu-id="2f214-156">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="2f214-157">To use the Data Lake Store SDK to obtain token for the Active Directory Web application you created earlier, use one of the subclasses of `AccessTokenProvider` (the example below uses `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="2f214-157">To use the Data Lake Store SDK to obtain token for the Active Directory Web application you created earlier, use one of the subclasses of `AccessTokenProvider` (the example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="2f214-158">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span><span class="sxs-lookup"><span data-stu-id="2f214-158">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span></span> <span data-ttu-id="2f214-159">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use the one provided in the SDK.</span><span class="sxs-lookup"><span data-stu-id="2f214-159">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use the one provided in the SDK.</span></span>

<span data-ttu-id="2f214-160">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span><span class="sxs-lookup"><span data-stu-id="2f214-160">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="2f214-161">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span><span class="sxs-lookup"><span data-stu-id="2f214-161">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="2f214-162">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you to specify the Data Lake Store account name and the token provider you generated in the last step.</span><span class="sxs-lookup"><span data-stu-id="2f214-162">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you to specify the Data Lake Store account name and the token provider you generated in the last step.</span></span> <span data-ttu-id="2f214-163">Note that the Data Lake Store account name needs to be a fully qualified domain name.</span><span class="sxs-lookup"><span data-stu-id="2f214-163">Note that the Data Lake Store account name needs to be a fully qualified domain name.</span></span> <span data-ttu-id="2f214-164">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="2f214-164">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just the account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-the-adlstoreclient-to-perform-file-and-directory-operations"></a><span data-ttu-id="2f214-165">Step 3: Use the ADLStoreClient to perform file and directory operations</span><span class="sxs-lookup"><span data-stu-id="2f214-165">Step 3: Use the ADLStoreClient to perform file and directory operations</span></span>
<span data-ttu-id="2f214-166">The code below contains example snippets of some common operations.</span><span class="sxs-lookup"><span data-stu-id="2f214-166">The code below contains example snippets of some common operations.</span></span> <span data-ttu-id="2f214-167">You can look at the full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of the **ADLStoreClient** object to see other operations.</span><span class="sxs-lookup"><span data-stu-id="2f214-167">You can look at the full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of the **ADLStoreClient** object to see other operations.</span></span>

<span data-ttu-id="2f214-168">Note that files are read from and written into using standard Java streams.</span><span class="sxs-lookup"><span data-stu-id="2f214-168">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="2f214-169">This means that you can layer any of the Java streams on top of the Data Lake Store streams to benefit from standard Java functionality (e.g., Print streams for formatted output, or any of the compression or encryption streams for additional functionality on top, etc.).</span><span class="sxs-lookup"><span data-stu-id="2f214-169">This means that you can layer any of the Java streams on top of the Data Lake Store streams to benefit from standard Java functionality (e.g., Print streams for formatted output, or any of the compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is the same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append to file
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate the two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename the file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all the subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-the-application"></a><span data-ttu-id="2f214-170">Step 4: Build and run the application</span><span class="sxs-lookup"><span data-stu-id="2f214-170">Step 4: Build and run the application</span></span>
1. <span data-ttu-id="2f214-171">To run from within an IDE, locate and press the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="2f214-171">To run from within an IDE, locate and press the **Run** button.</span></span> <span data-ttu-id="2f214-172">To run from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="2f214-172">To run from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="2f214-173">To produce a standalone jar that you can run from command-line build the jar with all dependencies included, using the [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="2f214-173">To produce a standalone jar that you can run from command-line build the jar with all dependencies included, using the [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="2f214-174">The pom.xml in the [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how to do this.</span><span class="sxs-lookup"><span data-stu-id="2f214-174">The pom.xml in the [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how to do this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f214-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f214-175">Next steps</span></span>
* [<span data-ttu-id="2f214-176">Explore JavaDoc for the Java SDK</span><span class="sxs-lookup"><span data-stu-id="2f214-176">Explore JavaDoc for the Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="2f214-177">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2f214-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="2f214-178">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2f214-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2f214-179">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2f214-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

