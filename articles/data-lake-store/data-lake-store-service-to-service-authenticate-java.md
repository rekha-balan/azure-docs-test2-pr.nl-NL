---
title: 'Service-to-service authentication: Java with Data Lake Store using Azure Active Directory | Microsoft Docs'
description: Learn how to achieve service-to-service authentication with Data Lake Store using Azure Active Directory with Java
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: c8ef983871f3fb1ec47522571ce95843bdd2d313
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870588"
---
# <a name="service-to-service-authentication-with-data-lake-store-using-java"></a><span data-ttu-id="57a92-103">Service-to-service authentication with Data Lake Store using Java</span><span class="sxs-lookup"><span data-stu-id="57a92-103">Service-to-service authentication with Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-service-to-service-authenticate-java.md)
> * [Using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-service-to-service-authenticate-python.md)
> * [Using REST API](data-lake-store-service-to-service-authenticate-rest-api.md)
> 
>  

<span data-ttu-id="57a92-108">In this article, you learn about how to use the Java SDK to do service-to-service authentication with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="57a92-108">In this article, you learn about how to use the Java SDK to do service-to-service authentication with Azure Data Lake Store.</span></span> <span data-ttu-id="57a92-109">End-user authentication with Data Lake Store using Java SDK is not supported.</span><span class="sxs-lookup"><span data-stu-id="57a92-109">End-user authentication with Data Lake Store using Java SDK is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57a92-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="57a92-110">Prerequisites</span></span>
* <span data-ttu-id="57a92-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="57a92-111">**An Azure subscription**.</span></span> <span data-ttu-id="57a92-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57a92-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="57a92-113">**Create an Azure Active Directory "Web" Application**.</span><span class="sxs-lookup"><span data-stu-id="57a92-113">**Create an Azure Active Directory "Web" Application**.</span></span> <span data-ttu-id="57a92-114">You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="57a92-114">You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).</span></span>

* <span data-ttu-id="57a92-115">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="57a92-115">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="57a92-116">This tutorial uses Maven for build and project dependencies.</span><span class="sxs-lookup"><span data-stu-id="57a92-116">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="57a92-117">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span><span class="sxs-lookup"><span data-stu-id="57a92-117">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>

* <span data-ttu-id="57a92-118">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span><span class="sxs-lookup"><span data-stu-id="57a92-118">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="service-to-service-authentication"></a><span data-ttu-id="57a92-119">Service-to-service authentication</span><span class="sxs-lookup"><span data-stu-id="57a92-119">Service-to-service authentication</span></span>
1. <span data-ttu-id="57a92-120">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command line or using an IDE.</span><span class="sxs-lookup"><span data-stu-id="57a92-120">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command line or using an IDE.</span></span> <span data-ttu-id="57a92-121">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="57a92-121">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="57a92-122">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="57a92-122">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span>

2. <span data-ttu-id="57a92-123">Add the following dependencies to your Maven **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="57a92-123">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="57a92-124">Add the following snippet before the **\</project>** tag:</span><span class="sxs-lookup"><span data-stu-id="57a92-124">Add the following snippet before the **\</project>** tag:</span></span>
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.2.3</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    <span data-ttu-id="57a92-125">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span><span class="sxs-lookup"><span data-stu-id="57a92-125">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="57a92-126">The second dependency is to specify the logging framework (`slf4j-nop`) to use for this application.</span><span class="sxs-lookup"><span data-stu-id="57a92-126">The second dependency is to specify the logging framework (`slf4j-nop`) to use for this application.</span></span> <span data-ttu-id="57a92-127">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span><span class="sxs-lookup"><span data-stu-id="57a92-127">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="57a92-128">For this example, we disable logging, hence we use the **slf4j-nop** binding.</span><span class="sxs-lookup"><span data-stu-id="57a92-128">For this example, we disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="57a92-129">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="57a92-129">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

3. <span data-ttu-id="57a92-130">Add the following import statements to your application.</span><span class="sxs-lookup"><span data-stu-id="57a92-130">Add the following import statements to your application.</span></span>

        import com.microsoft.azure.datalake.store.ADLException;
        import com.microsoft.azure.datalake.store.ADLStoreClient;
        import com.microsoft.azure.datalake.store.DirectoryEntry;
        import com.microsoft.azure.datalake.store.IfExists;
        import com.microsoft.azure.datalake.store.oauth2.AccessTokenProvider;
        import com.microsoft.azure.datalake.store.oauth2.ClientCredsTokenProvider;

4. <span data-ttu-id="57a92-131">Use the following snippet in your Java application to obtain token for the Active Directory Web application you created earlier using one of the subclasses of `AccessTokenProvider` (the following example uses `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="57a92-131">Use the following snippet in your Java application to obtain token for the Active Directory Web application you created earlier using one of the subclasses of `AccessTokenProvider` (the following example uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="57a92-132">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span><span class="sxs-lookup"><span data-stu-id="57a92-132">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span></span> <span data-ttu-id="57a92-133">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code.</span><span class="sxs-lookup"><span data-stu-id="57a92-133">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code.</span></span> <span data-ttu-id="57a92-134">For now, let's just use the one provided in the SDK.</span><span class="sxs-lookup"><span data-stu-id="57a92-134">For now, let's just use the one provided in the SDK.</span></span>

    <span data-ttu-id="57a92-135">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span><span class="sxs-lookup"><span data-stu-id="57a92-135">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span></span>

        private static String clientId = "FILL-IN-HERE";
        private static String authTokenEndpoint = "FILL-IN-HERE";
        private static String clientKey = "FILL-IN-HERE";
    
        AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);   

<span data-ttu-id="57a92-136">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="57a92-136">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="57a92-137">However, the SDK does not mandate that only these methods be used.</span><span class="sxs-lookup"><span data-stu-id="57a92-137">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="57a92-138">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span><span class="sxs-lookup"><span data-stu-id="57a92-138">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57a92-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="57a92-139">Next steps</span></span>
<span data-ttu-id="57a92-140">In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using Java SDK.</span><span class="sxs-lookup"><span data-stu-id="57a92-140">In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using Java SDK.</span></span> <span data-ttu-id="57a92-141">You can now look at the following articles that talk about how to use the Java SDK to work with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="57a92-141">You can now look at the following articles that talk about how to use the Java SDK to work with Azure Data Lake Store.</span></span>

* [<span data-ttu-id="57a92-142">Data operations on Data Lake Store using Java SDK</span><span class="sxs-lookup"><span data-stu-id="57a92-142">Data operations on Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)


