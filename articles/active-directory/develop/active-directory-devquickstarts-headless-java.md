---
title: Azure AD Java command line getting started | Microsoft Docs
description: How to build a Java command line app that signs users in to access an API.
services: active-directory
documentationcenter: java
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: xerners
ms.openlocfilehash: a6df13209a0cf355dc9b0175d8a5916b0ad688be
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553889"
---
# <a name="using-java-command-line-app-to-access-an-api-with-azure-ad"></a><span data-ttu-id="5f4fd-103">Using Java Command Line App To Access An API with Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f4fd-103">Using Java Command Line App To Access An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="5f4fd-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="5f4fd-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span></span>

  <span data-ttu-id="5f4fd-106">Here we'll use ADAL4J to:</span><span class="sxs-lookup"><span data-stu-id="5f4fd-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="5f4fd-107">Sign the user into the app using Azure AD as the identity provider.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-107">Sign the user into the app using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="5f4fd-108">Display some information about the user.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-108">Display some information about the user.</span></span>
* <span data-ttu-id="5f4fd-109">Sign the user out of the app.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-109">Sign the user out of the app.</span></span>

<span data-ttu-id="5f4fd-110">In order to do this, you'll need to:</span><span class="sxs-lookup"><span data-stu-id="5f4fd-110">In order to do this, you'll need to:</span></span>

1. <span data-ttu-id="5f4fd-111">Register an application with Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f4fd-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="5f4fd-112">Set up your app to use the ADAL4J library.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-112">Set up your app to use the ADAL4J library.</span></span>
3. <span data-ttu-id="5f4fd-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="5f4fd-114">Print out data about the user.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-114">Print out data about the user.</span></span>

<span data-ttu-id="5f4fd-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="5f4fd-116">You'll also need an Azure AD tenant in which to register your application.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-116">You'll also need an Azure AD tenant in which to register your application.</span></span>  <span data-ttu-id="5f4fd-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="5f4fd-118">1.  Register an Application with Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f4fd-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="5f4fd-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span></span>

1. <span data-ttu-id="5f4fd-120">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5f4fd-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="5f4fd-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="5f4fd-123">Click on **App registrations** and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="5f4fd-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="5f4fd-125">The **name** of the application will describe your application to end-users</span><span class="sxs-lookup"><span data-stu-id="5f4fd-125">The **name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="5f4fd-126">The **Sign-On URL** is the base URL of your app.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-126">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="5f4fd-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="5f4fd-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="5f4fd-129">You'll need this value in the next sections, so copy it from the application tab.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-129">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="5f4fd-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="5f4fd-131">The **App ID URI** is a unique identifier for your application.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-131">The **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="5f4fd-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="5f4fd-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="5f4fd-134">You will need it shortly.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-to-use-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="5f4fd-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span><span class="sxs-lookup"><span data-stu-id="5f4fd-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="5f4fd-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="5f4fd-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="5f4fd-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span><span class="sxs-lookup"><span data-stu-id="5f4fd-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-the-java-publicclient-file"></a><span data-ttu-id="5f4fd-139">3. Create the Java PublicClient file</span><span class="sxs-lookup"><span data-stu-id="5f4fd-139">3. Create the Java PublicClient file</span></span>
<span data-ttu-id="5f4fd-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span></span> <span data-ttu-id="5f4fd-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span></span>

* <span data-ttu-id="5f4fd-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="5f4fd-143">You can cut/paste this from below:</span><span class="sxs-lookup"><span data-stu-id="5f4fd-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-the-sample"></a><span data-ttu-id="5f4fd-144">Compile and run the sample</span><span class="sxs-lookup"><span data-stu-id="5f4fd-144">Compile and run the sample</span></span>
<span data-ttu-id="5f4fd-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span></span> <span data-ttu-id="5f4fd-146">This will use the `pom.xml` file you wrote for dependencies.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-146">This will use the `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="5f4fd-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="5f4fd-148">You may deploy that in your Tomcat container and visit the URL</span><span class="sxs-lookup"><span data-stu-id="5f4fd-148">You may deploy that in your Tomcat container and visit the URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="5f4fd-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span></span> <span data-ttu-id="5f4fd-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your \`\`adal4jsample.war\` file.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your \`\`adal4jsample.war\` file.</span></span> <span data-ttu-id="5f4fd-151">It will autodeploy for you with the correct endpoint.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-151">It will autodeploy for you with the correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5f4fd-152">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5f4fd-152">Next Steps</span></span>
<span data-ttu-id="5f4fd-153">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="5f4fd-153">Congratulations!</span></span> <span data-ttu-id="5f4fd-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="5f4fd-155">If you haven't already, now is the time to populate your tenant with some users.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-155">If you haven't already, now is the time to populate your tenant with some users.</span></span>

<span data-ttu-id="5f4fd-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span><span class="sxs-lookup"><span data-stu-id="5f4fd-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

