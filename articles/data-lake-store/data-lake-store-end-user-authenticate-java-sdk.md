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
# <a name="end-user-authentication-with-data-lake-store-using-java"></a>End-user authentication with Data Lake Store using Java
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-end-user-authenticate-java-sdk.md)
> * [Using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-end-user-authenticate-python.md)
> * [Using REST API](data-lake-store-end-user-authenticate-rest-api.md)
> 
>   

In this article, you learn about how to use the Java SDK to do end-user authentication with Azure Data Lake Store. For service-to-service authentication with Data Lake Store using Java SDK, see [Service-to-service authentication with Data Lake Store using Java](data-lake-store-service-to-service-authenticate-java.md).

## <a name="prerequisites"></a>Prerequisites
* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

* **Create an Azure Active Directory "Native" Application**. You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

* [Maven](https://maven.apache.org/install.html). This tutorial uses Maven for build and project dependencies. Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.

* (Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.

## <a name="end-user-authentication"></a>End-user authentication
1. Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command line or using an IDE. For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).

2. Add the following dependencies to your Maven **pom.xml** file. Add the following snippet before the **\</project>** tag:
   
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
   
    The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository. The second dependency is to specify the logging framework (`slf4j-nop`) to use for this application. The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging. For this example, we disable logging, hence we use the **slf4j-nop** binding. To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).

3. Add the following import statements to your application.

        import com.microsoft.azure.datalake.store.ADLException;
        import com.microsoft.azure.datalake.store.ADLStoreClient;
        import com.microsoft.azure.datalake.store.DirectoryEntry;
        import com.microsoft.azure.datalake.store.IfExists;
        import com.microsoft.azure.datalake.store.oauth2.AccessTokenProvider;
        import com.microsoft.azure.datalake.store.oauth2.DeviceCodeTokenProvider;

4. Use the following snippet in your Java application to obtain token for the Active Directory native application you created earlier using the `DeviceCodeTokenProvider`. Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory native application.

        private static String nativeAppId = "FILL-IN-HERE";
            
        AccessTokenProvider provider = new DeviceCodeTokenProvider(nativeAppId);   

The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account. However, the SDK does not mandate that only these methods be used. You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.

## <a name="next-steps"></a>Next steps
In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using Java SDK. You can now look at the following articles that talk about how to use the Java SDK to work with Azure Data Lake Store.

* [Data operations on Data Lake Store using Java SDK](data-lake-store-get-started-java-sdk.md)

