---
title: Create a Web App in Azure App Service using the Azure SDK for Java
description: Learn how to create a Web App on Azure App Service programmatically using the Azure SDK for Java.
tags: azure-classic-portal
services: app-service\web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 23f15617b587808acab9d5d3e42510c84a283af1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549105"
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="f82fd-103">Create a Web App in Azure App Service using the Azure SDK for Java</span><span class="sxs-lookup"><span data-stu-id="f82fd-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="f82fd-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f82fd-104">Overview</span></span>
<span data-ttu-id="f82fd-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span><span class="sxs-lookup"><span data-stu-id="f82fd-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="f82fd-106">It consists of two parts:</span><span class="sxs-lookup"><span data-stu-id="f82fd-106">It consists of two parts:</span></span>

* <span data-ttu-id="f82fd-107">Part 1 demonstrates how to build a Java application that creates a web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="f82fd-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span><span class="sxs-lookup"><span data-stu-id="f82fd-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f82fd-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f82fd-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="f82fd-110">Software Installations</span><span class="sxs-lookup"><span data-stu-id="f82fd-110">Software Installations</span></span>
<span data-ttu-id="f82fd-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="f82fd-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="f82fd-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="f82fd-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="f82fd-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span><span class="sxs-lookup"><span data-stu-id="f82fd-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="f82fd-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span><span class="sxs-lookup"><span data-stu-id="f82fd-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="f82fd-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="f82fd-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="f82fd-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="f82fd-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="f82fd-117">Create and Configure Cloud Resources in Azure</span><span class="sxs-lookup"><span data-stu-id="f82fd-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="f82fd-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span><span class="sxs-lookup"><span data-stu-id="f82fd-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="f82fd-119">Create an Active Directory (AD) in Azure</span><span class="sxs-lookup"><span data-stu-id="f82fd-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="f82fd-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="f82fd-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="f82fd-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span><span class="sxs-lookup"><span data-stu-id="f82fd-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="f82fd-122">Then click **Apply** to switch to that subscription view.</span><span class="sxs-lookup"><span data-stu-id="f82fd-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="f82fd-123">Select **Active Directory** from the menu at left.</span><span class="sxs-lookup"><span data-stu-id="f82fd-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="f82fd-124">**Click New > Directory > Custom Create**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="f82fd-125">In **Add Directory**, select **Create New Directory**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="f82fd-126">In **Name**, enter a directory name.</span><span class="sxs-lookup"><span data-stu-id="f82fd-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="f82fd-127">In **Domain**, enter a domain name.</span><span class="sxs-lookup"><span data-stu-id="f82fd-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="f82fd-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="f82fd-129">You can name it based on the directory name or another domain name that you own.</span><span class="sxs-lookup"><span data-stu-id="f82fd-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="f82fd-130">Later, you can add another domain name that your organization already uses.</span><span class="sxs-lookup"><span data-stu-id="f82fd-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="f82fd-131">In **Country or region**, select your locale.</span><span class="sxs-lookup"><span data-stu-id="f82fd-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="f82fd-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="f82fd-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="f82fd-133">Create a Management Certificate for Azure</span><span class="sxs-lookup"><span data-stu-id="f82fd-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="f82fd-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="f82fd-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="f82fd-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span><span class="sxs-lookup"><span data-stu-id="f82fd-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="f82fd-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span><span class="sxs-lookup"><span data-stu-id="f82fd-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="f82fd-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span><span class="sxs-lookup"><span data-stu-id="f82fd-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="f82fd-138">This involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="f82fd-138">This involves the following steps:</span></span>

* <span data-ttu-id="f82fd-139">Generate a PFX file representing your client certificate and save it locally.</span><span class="sxs-lookup"><span data-stu-id="f82fd-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="f82fd-140">Generate a management certificate (CER file) from the PFX file.</span><span class="sxs-lookup"><span data-stu-id="f82fd-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="f82fd-141">Upload the CER file to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f82fd-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="f82fd-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span><span class="sxs-lookup"><span data-stu-id="f82fd-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="f82fd-143">Write the application's authentication code, which refers to the local JKS file.</span><span class="sxs-lookup"><span data-stu-id="f82fd-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="f82fd-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span><span class="sxs-lookup"><span data-stu-id="f82fd-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="f82fd-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="f82fd-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="f82fd-146">Create a certificate</span><span class="sxs-lookup"><span data-stu-id="f82fd-146">Create a certificate</span></span>
<span data-ttu-id="f82fd-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span><span class="sxs-lookup"><span data-stu-id="f82fd-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="f82fd-148">**Note:**  The computer on which you run this command must have the JDK installed.</span><span class="sxs-lookup"><span data-stu-id="f82fd-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="f82fd-149">Also, the path to the keytool depends on the location in which you install the JDK.</span><span class="sxs-lookup"><span data-stu-id="f82fd-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="f82fd-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span><span class="sxs-lookup"><span data-stu-id="f82fd-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="f82fd-151">To create the .pfx file:</span><span class="sxs-lookup"><span data-stu-id="f82fd-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="f82fd-152">To create the .cer file:</span><span class="sxs-lookup"><span data-stu-id="f82fd-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="f82fd-153">where:</span><span class="sxs-lookup"><span data-stu-id="f82fd-153">where:</span></span>

* <span data-ttu-id="f82fd-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span><span class="sxs-lookup"><span data-stu-id="f82fd-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="f82fd-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="f82fd-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="f82fd-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="f82fd-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="f82fd-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="f82fd-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="f82fd-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span><span class="sxs-lookup"><span data-stu-id="f82fd-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="f82fd-159">You can enter no password, although this is not recommended.</span><span class="sxs-lookup"><span data-stu-id="f82fd-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="f82fd-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="f82fd-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="f82fd-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="f82fd-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="f82fd-162">Upload the certificate</span><span class="sxs-lookup"><span data-stu-id="f82fd-162">Upload the certificate</span></span>
<span data-ttu-id="f82fd-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span><span class="sxs-lookup"><span data-stu-id="f82fd-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="f82fd-164">Convert the PFX file into JKS</span><span class="sxs-lookup"><span data-stu-id="f82fd-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="f82fd-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span><span class="sxs-lookup"><span data-stu-id="f82fd-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="f82fd-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span><span class="sxs-lookup"><span data-stu-id="f82fd-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="f82fd-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span><span class="sxs-lookup"><span data-stu-id="f82fd-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="f82fd-168">The two passwords do not have to be the same.</span><span class="sxs-lookup"><span data-stu-id="f82fd-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="f82fd-169">You can enter no password, although this is not recommended.</span><span class="sxs-lookup"><span data-stu-id="f82fd-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="f82fd-170">Build a Web App creation application</span><span class="sxs-lookup"><span data-stu-id="f82fd-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="f82fd-171">Create the Eclipse Workspace and Maven Project</span><span class="sxs-lookup"><span data-stu-id="f82fd-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="f82fd-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="f82fd-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="f82fd-173">Create a new Maven project.</span><span class="sxs-lookup"><span data-stu-id="f82fd-173">Create a new Maven project.</span></span> <span data-ttu-id="f82fd-174">Click **File > New > Maven Project**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="f82fd-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="f82fd-176">On the second page of **New Maven Project**, specify the following:</span><span class="sxs-lookup"><span data-stu-id="f82fd-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="f82fd-177">Group ID: `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="f82fd-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="f82fd-178">Artifact ID: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="f82fd-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="f82fd-179">Version: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="f82fd-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="f82fd-180">Packaging: jar</span><span class="sxs-lookup"><span data-stu-id="f82fd-180">Packaging: jar</span></span>
   * <span data-ttu-id="f82fd-181">Name: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="f82fd-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="f82fd-182">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-182">Click **Finish**.</span></span>
3. <span data-ttu-id="f82fd-183">Open the new project's pom.xml file in Project Explorer.</span><span class="sxs-lookup"><span data-stu-id="f82fd-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="f82fd-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span><span class="sxs-lookup"><span data-stu-id="f82fd-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="f82fd-185">Open the Maven Repositories view.</span><span class="sxs-lookup"><span data-stu-id="f82fd-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="f82fd-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="f82fd-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span><span class="sxs-lookup"><span data-stu-id="f82fd-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="f82fd-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="f82fd-189">This step can take several minutes depending on the speed of your connection.</span><span class="sxs-lookup"><span data-stu-id="f82fd-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="f82fd-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span><span class="sxs-lookup"><span data-stu-id="f82fd-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="f82fd-191">In **Dependencies**, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="f82fd-192">In **Enter Group ID...** enter `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="f82fd-193">Select the packages for base management and App Service Web Apps management:</span><span class="sxs-lookup"><span data-stu-id="f82fd-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="f82fd-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span><span class="sxs-lookup"><span data-stu-id="f82fd-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="f82fd-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span><span class="sxs-lookup"><span data-stu-id="f82fd-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="f82fd-196">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-196">Click **OK**.</span></span> <span data-ttu-id="f82fd-197">The Azure packages then appear in the **Dependencies** list.</span><span class="sxs-lookup"><span data-stu-id="f82fd-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="f82fd-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span><span class="sxs-lookup"><span data-stu-id="f82fd-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="f82fd-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="f82fd-200">Create a Java class to contain the main entry point code.</span><span class="sxs-lookup"><span data-stu-id="f82fd-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="f82fd-201">In Project Explorer, right-click on the project node and select **New > Class**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="f82fd-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span><span class="sxs-lookup"><span data-stu-id="f82fd-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="f82fd-203">The selections should appear as follows:</span><span class="sxs-lookup"><span data-stu-id="f82fd-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="f82fd-204">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-204">Click **Finish**.</span></span> <span data-ttu-id="f82fd-205">The WebCreator.java file appears in Project Explorer.</span><span class="sxs-lookup"><span data-stu-id="f82fd-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="f82fd-206">Calling the Azure API to Create an App Service Web App</span><span class="sxs-lookup"><span data-stu-id="f82fd-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="f82fd-207">Add necessary imports</span><span class="sxs-lookup"><span data-stu-id="f82fd-207">Add necessary imports</span></span>
<span data-ttu-id="f82fd-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span><span class="sxs-lookup"><span data-stu-id="f82fd-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="f82fd-209">Define the main entry point class</span><span class="sxs-lookup"><span data-stu-id="f82fd-209">Define the main entry point class</span></span>
<span data-ttu-id="f82fd-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="f82fd-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="f82fd-212">Add the following parameter definitions for the web app and webspace.</span><span class="sxs-lookup"><span data-stu-id="f82fd-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="f82fd-213">You will need to provide your own Azure subscription ID and certificate information.</span><span class="sxs-lookup"><span data-stu-id="f82fd-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="f82fd-214">where:</span><span class="sxs-lookup"><span data-stu-id="f82fd-214">where:</span></span>

* <span data-ttu-id="f82fd-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span><span class="sxs-lookup"><span data-stu-id="f82fd-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="f82fd-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span><span class="sxs-lookup"><span data-stu-id="f82fd-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="f82fd-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span><span class="sxs-lookup"><span data-stu-id="f82fd-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="f82fd-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span><span class="sxs-lookup"><span data-stu-id="f82fd-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="f82fd-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="f82fd-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="f82fd-221">`domainName` should be specified as shown above.</span><span class="sxs-lookup"><span data-stu-id="f82fd-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="f82fd-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span><span class="sxs-lookup"><span data-stu-id="f82fd-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="f82fd-223">`appServicePlanName` should be specified as shown above.</span><span class="sxs-lookup"><span data-stu-id="f82fd-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="f82fd-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span><span class="sxs-lookup"><span data-stu-id="f82fd-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="f82fd-225">Otherwise, execution will fail because the same resource already exists on Azure.</span><span class="sxs-lookup"><span data-stu-id="f82fd-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="f82fd-226">Define the web creation method</span><span class="sxs-lookup"><span data-stu-id="f82fd-226">Define the web creation method</span></span>
<span data-ttu-id="f82fd-227">Next, define a method to create the web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="f82fd-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span><span class="sxs-lookup"><span data-stu-id="f82fd-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="f82fd-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span><span class="sxs-lookup"><span data-stu-id="f82fd-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="f82fd-230">The management client is key to creating Web Apps.</span><span class="sxs-lookup"><span data-stu-id="f82fd-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="f82fd-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span><span class="sxs-lookup"><span data-stu-id="f82fd-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="f82fd-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="f82fd-233">Define the main() method</span><span class="sxs-lookup"><span data-stu-id="f82fd-233">Define the main() method</span></span>
<span data-ttu-id="f82fd-234">Provide the main() method code that calls createWebApp() to create the web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="f82fd-235">Finally, call `createWebApp` from `main`:</span><span class="sxs-lookup"><span data-stu-id="f82fd-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="f82fd-236">Run the application and verify web app creation</span><span class="sxs-lookup"><span data-stu-id="f82fd-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="f82fd-237">To verify that your application runs, click **Run > Run**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="f82fd-238">When the application completes running, you should see the following output in the Eclipse console:</span><span class="sxs-lookup"><span data-stu-id="f82fd-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="f82fd-239">Log into the Azure classic portal and click **Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="f82fd-240">The new web app should appear in the Web Apps list within a few minutes.</span><span class="sxs-lookup"><span data-stu-id="f82fd-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="f82fd-241">Deploying an Application to the Web App</span><span class="sxs-lookup"><span data-stu-id="f82fd-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="f82fd-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span><span class="sxs-lookup"><span data-stu-id="f82fd-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="f82fd-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span><span class="sxs-lookup"><span data-stu-id="f82fd-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="f82fd-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span><span class="sxs-lookup"><span data-stu-id="f82fd-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="f82fd-245">Next you will create a "Hello World" application and deploy it to the web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="f82fd-246">Create a JSP Hello World application</span><span class="sxs-lookup"><span data-stu-id="f82fd-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="f82fd-247">Create the application</span><span class="sxs-lookup"><span data-stu-id="f82fd-247">Create the application</span></span>
<span data-ttu-id="f82fd-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span><span class="sxs-lookup"><span data-stu-id="f82fd-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="f82fd-249">Click **File > New > Dynamic Web Project**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="f82fd-250">Name it `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-250">Name it `JSPHello`.</span></span> <span data-ttu-id="f82fd-251">You do not need to change any other settings in this dialog.</span><span class="sxs-lookup"><span data-stu-id="f82fd-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="f82fd-252">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="f82fd-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="f82fd-254">In the New JSP File dialog, name the new file `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="f82fd-255">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-255">Click **Next**.</span></span>
3. <span data-ttu-id="f82fd-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="f82fd-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span><span class="sxs-lookup"><span data-stu-id="f82fd-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="f82fd-258">Run the Hello World application in localhost</span><span class="sxs-lookup"><span data-stu-id="f82fd-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="f82fd-259">Before you run this application, you need to configure a few properties.</span><span class="sxs-lookup"><span data-stu-id="f82fd-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="f82fd-260">Right-click the **JSPHello** project and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="f82fd-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span><span class="sxs-lookup"><span data-stu-id="f82fd-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="f82fd-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="f82fd-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="f82fd-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span><span class="sxs-lookup"><span data-stu-id="f82fd-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="f82fd-265">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-265">Click **Finish**.</span></span>
5. <span data-ttu-id="f82fd-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span><span class="sxs-lookup"><span data-stu-id="f82fd-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="f82fd-267">Select **Apache Tomcat v7.0**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="f82fd-268">In the Eclipse **Run** menu, click **Run**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="f82fd-269">In the **Run As** dialog, select **Run on Server**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="f82fd-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="f82fd-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="f82fd-271">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-271">Click **Finish**.</span></span>
7. <span data-ttu-id="f82fd-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span><span class="sxs-lookup"><span data-stu-id="f82fd-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="f82fd-273">Export the application as a WAR</span><span class="sxs-lookup"><span data-stu-id="f82fd-273">Export the application as a WAR</span></span>
<span data-ttu-id="f82fd-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="f82fd-275">The following web project files reside in the WebContent folder:</span><span class="sxs-lookup"><span data-stu-id="f82fd-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="f82fd-276">Right-click the WebContent folder and select **Export**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="f82fd-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="f82fd-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span><span class="sxs-lookup"><span data-stu-id="f82fd-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="f82fd-279">For example:</span><span class="sxs-lookup"><span data-stu-id="f82fd-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="f82fd-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="f82fd-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="f82fd-281">Deploying the Hello World Application Using FTP</span><span class="sxs-lookup"><span data-stu-id="f82fd-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="f82fd-282">Select a third-party FTP client to publish the application.</span><span class="sxs-lookup"><span data-stu-id="f82fd-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="f82fd-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span><span class="sxs-lookup"><span data-stu-id="f82fd-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="f82fd-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span><span class="sxs-lookup"><span data-stu-id="f82fd-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="f82fd-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span><span class="sxs-lookup"><span data-stu-id="f82fd-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="f82fd-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="f82fd-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span><span class="sxs-lookup"><span data-stu-id="f82fd-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="f82fd-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span><span class="sxs-lookup"><span data-stu-id="f82fd-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="f82fd-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span><span class="sxs-lookup"><span data-stu-id="f82fd-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="f82fd-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="f82fd-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="f82fd-291">Deploy using an FTP utility</span><span class="sxs-lookup"><span data-stu-id="f82fd-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="f82fd-292">Set up deployment credentials</span><span class="sxs-lookup"><span data-stu-id="f82fd-292">Set up deployment credentials</span></span>
<span data-ttu-id="f82fd-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="f82fd-294">You will transfer files to this location.</span><span class="sxs-lookup"><span data-stu-id="f82fd-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="f82fd-295">Log into the classic portal and click **Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="f82fd-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span><span class="sxs-lookup"><span data-stu-id="f82fd-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="f82fd-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span><span class="sxs-lookup"><span data-stu-id="f82fd-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="f82fd-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span><span class="sxs-lookup"><span data-stu-id="f82fd-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="f82fd-299">Deployment credentials are associated with a Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="f82fd-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="f82fd-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span><span class="sxs-lookup"><span data-stu-id="f82fd-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="f82fd-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="f82fd-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="f82fd-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span><span class="sxs-lookup"><span data-stu-id="f82fd-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="f82fd-303">Get FTP connection information</span><span class="sxs-lookup"><span data-stu-id="f82fd-303">Get FTP connection information</span></span>
<span data-ttu-id="f82fd-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span><span class="sxs-lookup"><span data-stu-id="f82fd-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="f82fd-305">There are two ways to obtain connection information.</span><span class="sxs-lookup"><span data-stu-id="f82fd-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="f82fd-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span><span class="sxs-lookup"><span data-stu-id="f82fd-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="f82fd-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f82fd-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="f82fd-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span><span class="sxs-lookup"><span data-stu-id="f82fd-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="f82fd-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="f82fd-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="f82fd-310">Under **Essentials**, find and copy the **FTP hostname**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="f82fd-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="f82fd-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="f82fd-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="f82fd-314">To obtain FTP connection information from the publish profile:</span><span class="sxs-lookup"><span data-stu-id="f82fd-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="f82fd-315">In the web app's blade, click **Get publish profile**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="f82fd-316">This will download a .publishsettings file to your local drive.</span><span class="sxs-lookup"><span data-stu-id="f82fd-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="f82fd-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="f82fd-318">It should look like the following:</span><span class="sxs-lookup"><span data-stu-id="f82fd-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="f82fd-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span><span class="sxs-lookup"><span data-stu-id="f82fd-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="f82fd-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="f82fd-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="f82fd-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span><span class="sxs-lookup"><span data-stu-id="f82fd-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="f82fd-323">`userName` is the same as **Deployment / FTP user**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="f82fd-324">They map to **User** and **Password** in FileZilla.</span><span class="sxs-lookup"><span data-stu-id="f82fd-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="f82fd-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="f82fd-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="f82fd-326">Configure the Web App to host a Java application</span><span class="sxs-lookup"><span data-stu-id="f82fd-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="f82fd-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span><span class="sxs-lookup"><span data-stu-id="f82fd-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="f82fd-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="f82fd-329">On the **Configure** page, specify the following settings.</span><span class="sxs-lookup"><span data-stu-id="f82fd-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="f82fd-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="f82fd-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="f82fd-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span><span class="sxs-lookup"><span data-stu-id="f82fd-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="f82fd-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span><span class="sxs-lookup"><span data-stu-id="f82fd-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="f82fd-333">(The default file for web apps is hostingstart.html.)</span><span class="sxs-lookup"><span data-stu-id="f82fd-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="f82fd-334">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="f82fd-335">Publish your application using Kudu</span><span class="sxs-lookup"><span data-stu-id="f82fd-335">Publish your application using Kudu</span></span>
<span data-ttu-id="f82fd-336">One way to publish the application is to use the Kudu debug console built into Azure.</span><span class="sxs-lookup"><span data-stu-id="f82fd-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="f82fd-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span><span class="sxs-lookup"><span data-stu-id="f82fd-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="f82fd-338">You access the console for the web app by browsing to a URL of the following form:</span><span class="sxs-lookup"><span data-stu-id="f82fd-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="f82fd-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span><span class="sxs-lookup"><span data-stu-id="f82fd-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="f82fd-340">From the top menu, select **Debug Console > CMD**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="f82fd-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span><span class="sxs-lookup"><span data-stu-id="f82fd-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="f82fd-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span><span class="sxs-lookup"><span data-stu-id="f82fd-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="f82fd-343">In the console command line, navigate to the webapps directory:</span><span class="sxs-lookup"><span data-stu-id="f82fd-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="f82fd-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="f82fd-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span><span class="sxs-lookup"><span data-stu-id="f82fd-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="f82fd-346">At first JSPHello.war appears in the directory area by itself:</span><span class="sxs-lookup"><span data-stu-id="f82fd-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="f82fd-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span><span class="sxs-lookup"><span data-stu-id="f82fd-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="f82fd-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span><span class="sxs-lookup"><span data-stu-id="f82fd-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="f82fd-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span><span class="sxs-lookup"><span data-stu-id="f82fd-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="f82fd-350">If you do not see these items, wait and repeat.</span><span class="sxs-lookup"><span data-stu-id="f82fd-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="f82fd-351">Publish your application using FileZilla (optional)</span><span class="sxs-lookup"><span data-stu-id="f82fd-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="f82fd-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span><span class="sxs-lookup"><span data-stu-id="f82fd-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="f82fd-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span><span class="sxs-lookup"><span data-stu-id="f82fd-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="f82fd-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="f82fd-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="f82fd-355">In FileZilla, click **File > Site Manager**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="f82fd-356">In the **Site Manager** dialog, click **New Site**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="f82fd-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span><span class="sxs-lookup"><span data-stu-id="f82fd-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="f82fd-358">For this procedure, name it `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="f82fd-359">On the **General** tab, specify the following settings:</span><span class="sxs-lookup"><span data-stu-id="f82fd-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="f82fd-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="f82fd-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="f82fd-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span><span class="sxs-lookup"><span data-stu-id="f82fd-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="f82fd-362">**Protocol:** FTP File Transfer Protocol</span><span class="sxs-lookup"><span data-stu-id="f82fd-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="f82fd-363">**Encryption:** Use plain FTP</span><span class="sxs-lookup"><span data-stu-id="f82fd-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="f82fd-364">**Logon Type:** Normal</span><span class="sxs-lookup"><span data-stu-id="f82fd-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="f82fd-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="f82fd-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="f82fd-366">This is the full FTP username, which has the form *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="f82fd-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="f82fd-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span><span class="sxs-lookup"><span data-stu-id="f82fd-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="f82fd-368">On the **Transfer Settings** tab, select **Passive**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="f82fd-369">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-369">Click **Connect**.</span></span> <span data-ttu-id="f82fd-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span><span class="sxs-lookup"><span data-stu-id="f82fd-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="f82fd-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f82fd-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="f82fd-372">In the **Remote** site panel, select the destination folder.</span><span class="sxs-lookup"><span data-stu-id="f82fd-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="f82fd-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span><span class="sxs-lookup"><span data-stu-id="f82fd-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="f82fd-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="f82fd-375">Name the directory `webapps` and enter that directory.</span><span class="sxs-lookup"><span data-stu-id="f82fd-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="f82fd-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="f82fd-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="f82fd-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="f82fd-378">You should see it appear in `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="f82fd-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="f82fd-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span><span class="sxs-lookup"><span data-stu-id="f82fd-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="f82fd-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span><span class="sxs-lookup"><span data-stu-id="f82fd-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="f82fd-381">Run the Hello World application on the Web App</span><span class="sxs-lookup"><span data-stu-id="f82fd-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="f82fd-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span><span class="sxs-lookup"><span data-stu-id="f82fd-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="f82fd-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span><span class="sxs-lookup"><span data-stu-id="f82fd-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="f82fd-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span><span class="sxs-lookup"><span data-stu-id="f82fd-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="f82fd-385">When the application runs, you should see a web page with the following output:</span><span class="sxs-lookup"><span data-stu-id="f82fd-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="f82fd-386">Clean up Azure resources</span><span class="sxs-lookup"><span data-stu-id="f82fd-386">Clean up Azure resources</span></span>
<span data-ttu-id="f82fd-387">This procedure creates an App Service web app.</span><span class="sxs-lookup"><span data-stu-id="f82fd-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="f82fd-388">You will be billed for the resource as long as it exists.</span><span class="sxs-lookup"><span data-stu-id="f82fd-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="f82fd-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span><span class="sxs-lookup"><span data-stu-id="f82fd-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="f82fd-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span><span class="sxs-lookup"><span data-stu-id="f82fd-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="f82fd-391">Deleting a web app erases all data you have uploaded to it.</span><span class="sxs-lookup"><span data-stu-id="f82fd-391">Deleting a web app erases all data you have uploaded to it.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com










