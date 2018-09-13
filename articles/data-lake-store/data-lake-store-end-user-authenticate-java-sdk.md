---
title: 'End-user authentication: Java with Data Lake Store using Azure Active Directory | Microsoft Docs'
description: Learn how to achieve end-user authentication with Data Lake Store using Azure Active Directory with Java
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
ms.openlocfilehash: 633bf87d1e02a1132cfc5cd151b1e58418de8152
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866894"
---
# <a name="end-user-authentication-with-data-lake-store-using-java"></a><span data-ttu-id="f1a3f-103">End-user authentication with Data Lake Store using Java</span><span class="sxs-lookup"><span data-stu-id="f1a3f-103">End-user authentication with Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-end-user-authenticate-java-sdk.md)
> * [Using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-end-user-authenticate-python.md)
> * [Using REST API](data-lake-store-end-user-authenticate-rest-api.md)
> 
>   

<span data-ttu-id="f1a3f-108">In this article, you learn about how to use the Java SDK to do end-user authentication with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-108">In this article, you learn about how to use the Java SDK to do end-user authentication with Azure Data Lake Store.</span></span> <span data-ttu-id="f1a3f-109">For service-to-service authentication with Data Lake Store using Java SDK, see [Service-to-service authentication with Data Lake Store using Java](data-lake-store-service-to-service-authenticate-java.md).</span><span class="sxs-lookup"><span data-stu-id="f1a3f-109">For service-to-service authentication with Data Lake Store using Java SDK, see [Service-to-service authentication with Data Lake Store using Java](data-lake-store-service-to-service-authenticate-java.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1a3f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f1a3f-110">Prerequisites</span></span>
* <span data-ttu-id="f1a3f-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-111">**An Azure subscription**.</span></span> <span data-ttu-id="f1a3f-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1a3f-112">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="f1a3f-113">**Create an Azure Active Directory "Native" Application**.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-113">**Create an Azure Active Directory "Native" Application**.</span></span> <span data-ttu-id="f1a3f-114">You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f1a3f-114">You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

* <span data-ttu-id="f1a3f-115">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="f1a3f-115">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="f1a3f-116">This tutorial uses Maven for build and project dependencies.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-116">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="f1a3f-117">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-117">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>

* <span data-ttu-id="f1a3f-118">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-118">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="end-user-authentication"></a><span data-ttu-id="f1a3f-119">End-user authentication</span><span class="sxs-lookup"><span data-stu-id="f1a3f-119">End-user authentication</span></span>
1. <span data-ttu-id="f1a3f-120">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command line or using an IDE.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-120">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command line or using an IDE.</span></span> <span data-ttu-id="f1a3f-121">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="f1a3f-121">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="f1a3f-122">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="f1a3f-122">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span>

2. <span data-ttu-id="f1a3f-123">Add the following dependencies to your Maven **pom.xml** file.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-123">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="f1a3f-124">Add the following snippet before the **\</project>** tag:</span><span class="sxs-lookup"><span data-stu-id="f1a3f-124">Add the following snippet before the **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="f1a3f-125">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-125">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="f1a3f-126">The second dependency is to specify the logging framework (`slf4j-nop`) to use for this application.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-126">The second dependency is to specify the logging framework (`slf4j-nop`) to use for this application.</span></span> <span data-ttu-id="f1a3f-127">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-127">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="f1a3f-128">For this example, we disable logging, hence we use the **slf4j-nop** binding.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-128">For this example, we disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="f1a3f-129">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="f1a3f-129">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

3. <span data-ttu-id="f1a3f-130">Add the following import statements to your application.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-130">Add the following import statements to your application.</span></span>

        import com.microsoft.azure.datalake.store.ADLException;
        import com.microsoft.azure.datalake.store.ADLStoreClient;
        import com.microsoft.azure.datalake.store.DirectoryEntry;
        import com.microsoft.azure.datalake.store.IfExists;
        import com.microsoft.azure.datalake.store.oauth2.AccessTokenProvider;
        import com.microsoft.azure.datalake.store.oauth2.DeviceCodeTokenProvider;

4. <span data-ttu-id="f1a3f-131">Use the following snippet in your Java application to obtain token for the Active Directory native application you created earlier using the `DeviceCodeTokenProvider`.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-131">Use the following snippet in your Java application to obtain token for the Active Directory native application you created earlier using the `DeviceCodeTokenProvider`.</span></span> <span data-ttu-id="f1a3f-132">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory native application.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-132">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory native application.</span></span>

        private static String nativeAppId = "FILL-IN-HERE";
            
        AccessTokenProvider provider = new DeviceCodeTokenProvider(nativeAppId);   

<span data-ttu-id="f1a3f-133">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-133">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="f1a3f-134">However, the SDK does not mandate that only these methods be used.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-134">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="f1a3f-135">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-135">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1a3f-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1a3f-136">Next steps</span></span>
<span data-ttu-id="f1a3f-137">In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using Java SDK.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-137">In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using Java SDK.</span></span> <span data-ttu-id="f1a3f-138">You can now look at the following articles that talk about how to use the Java SDK to work with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f1a3f-138">You can now look at the following articles that talk about how to use the Java SDK to work with Azure Data Lake Store.</span></span>

* [<span data-ttu-id="f1a3f-139">Data operations on Data Lake Store using Java SDK</span><span class="sxs-lookup"><span data-stu-id="f1a3f-139">Data operations on Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)


