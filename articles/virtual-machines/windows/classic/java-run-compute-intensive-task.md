---
title: Compute-intensive Java application on a VM | Microsoft Docs
description: Learn how to create an Azure virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 392e941d36a50307bfb13af255c29c85cb9c7e72
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553783"
---
# <a name="how-to-run-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="17e3b-103">How to run a compute-intensive task in Java on a virtual machine</span><span class="sxs-lookup"><span data-stu-id="17e3b-103">How to run a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="17e3b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="17e3b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="17e3b-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="17e3b-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="17e3b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="17e3b-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="17e3b-107">With Azure, you can use a virtual machine to handle compute-intensive tasks.</span><span class="sxs-lookup"><span data-stu-id="17e3b-107">With Azure, you can use a virtual machine to handle compute-intensive tasks.</span></span> <span data-ttu-id="17e3b-108">For example, a virtual machine can handle tasks and deliver results to client machines or mobile applications.</span><span class="sxs-lookup"><span data-stu-id="17e3b-108">For example, a virtual machine can handle tasks and deliver results to client machines or mobile applications.</span></span> <span data-ttu-id="17e3b-109">After reading this article, you will have an understanding of how to create a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span><span class="sxs-lookup"><span data-stu-id="17e3b-109">After reading this article, you will have an understanding of how to create a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="17e3b-110">This tutorial assumes you know how to create Java console applications, can import libraries to your Java application, and can generate a Java archive (JAR).</span><span class="sxs-lookup"><span data-stu-id="17e3b-110">This tutorial assumes you know how to create Java console applications, can import libraries to your Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="17e3b-111">No knowledge of Microsoft Azure is assumed.</span><span class="sxs-lookup"><span data-stu-id="17e3b-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="17e3b-112">You will learn:</span><span class="sxs-lookup"><span data-stu-id="17e3b-112">You will learn:</span></span>

* <span data-ttu-id="17e3b-113">How to create a virtual machine with a Java Development Kit (JDK) already installed.</span><span class="sxs-lookup"><span data-stu-id="17e3b-113">How to create a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="17e3b-114">How to remotely log in to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17e3b-114">How to remotely log in to your virtual machine.</span></span>
* <span data-ttu-id="17e3b-115">How to create a service bus namespace.</span><span class="sxs-lookup"><span data-stu-id="17e3b-115">How to create a service bus namespace.</span></span>
* <span data-ttu-id="17e3b-116">How to create a Java application that performs a compute-intensive task.</span><span class="sxs-lookup"><span data-stu-id="17e3b-116">How to create a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="17e3b-117">How to create a Java application that monitors the progress of the compute-intensive task.</span><span class="sxs-lookup"><span data-stu-id="17e3b-117">How to create a Java application that monitors the progress of the compute-intensive task.</span></span>
* <span data-ttu-id="17e3b-118">How to run the Java applications.</span><span class="sxs-lookup"><span data-stu-id="17e3b-118">How to run the Java applications.</span></span>
* <span data-ttu-id="17e3b-119">How to stop the Java applications.</span><span class="sxs-lookup"><span data-stu-id="17e3b-119">How to stop the Java applications.</span></span>

<span data-ttu-id="17e3b-120">This tutorial will use the Traveling Salesman Problem for the compute-intensive task.</span><span class="sxs-lookup"><span data-stu-id="17e3b-120">This tutorial will use the Traveling Salesman Problem for the compute-intensive task.</span></span> <span data-ttu-id="17e3b-121">The following is an example of the Java application running the compute-intensive task.</span><span class="sxs-lookup"><span data-stu-id="17e3b-121">The following is an example of the Java application running the compute-intensive task.</span></span>

![Traveling Salesman Problem solver][solver_output]

<span data-ttu-id="17e3b-123">The following is an example of the Java application monitoring the compute-intensive task.</span><span class="sxs-lookup"><span data-stu-id="17e3b-123">The following is an example of the Java application monitoring the compute-intensive task.</span></span>

![Traveling Salesman Problem client][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="17e3b-125">To create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="17e3b-125">To create a virtual machine</span></span>
1. <span data-ttu-id="17e3b-126">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="17e3b-126">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="17e3b-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="17e3b-128">In the **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-128">In the **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="17e3b-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready to run in JDK 7.</span><span class="sxs-lookup"><span data-stu-id="17e3b-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready to run in JDK 7.</span></span>
4. <span data-ttu-id="17e3b-130">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-130">Click **Next**.</span></span>
5. <span data-ttu-id="17e3b-131">In the **Virtual machine configuration** dialog box:</span><span class="sxs-lookup"><span data-stu-id="17e3b-131">In the **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="17e3b-132">Specify a name for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17e3b-132">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="17e3b-133">Specify the size to use for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17e3b-133">Specify the size to use for the virtual machine.</span></span>
   3. <span data-ttu-id="17e3b-134">Enter a name for the administrator in the **User Name** field.</span><span class="sxs-lookup"><span data-stu-id="17e3b-134">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="17e3b-135">Remember this name and the password you will enter next, you will use them when you remotely log in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17e3b-135">Remember this name and the password you will enter next, you will use them when you remotely log in to the virtual machine.</span></span>
   4. <span data-ttu-id="17e3b-136">Enter a password in the **New password** field, and re-enter it in the **Confirm** field.</span><span class="sxs-lookup"><span data-stu-id="17e3b-136">Enter a password in the **New password** field, and re-enter it in the **Confirm** field.</span></span> <span data-ttu-id="17e3b-137">This is the Administrator account password.</span><span class="sxs-lookup"><span data-stu-id="17e3b-137">This is the Administrator account password.</span></span>
   5. <span data-ttu-id="17e3b-138">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-138">Click **Next**.</span></span>
6. <span data-ttu-id="17e3b-139">In the next **Virtual machine configuration** dialog box:</span><span class="sxs-lookup"><span data-stu-id="17e3b-139">In the next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="17e3b-140">For **Cloud service**, use the default **Create a new cloud service**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-140">For **Cloud service**, use the default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="17e3b-141">The value for **Cloud service DNS name** must be unique across cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="17e3b-141">The value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="17e3b-142">If needed, modify this value so that Azure indicates it is unique.</span><span class="sxs-lookup"><span data-stu-id="17e3b-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="17e3b-143">Specify a region, affinity group, or virtual network.</span><span class="sxs-lookup"><span data-stu-id="17e3b-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="17e3b-144">For purposes of this tutorial, specify a region such as **West US**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="17e3b-145">For **Storage Account**, select **Use an automatically generated storage account**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="17e3b-146">For **Availability Set**, select **(None)**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="17e3b-147">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-147">Click **Next**.</span></span>
7. <span data-ttu-id="17e3b-148">In the final **Virtual machine configuration** dialog box:</span><span class="sxs-lookup"><span data-stu-id="17e3b-148">In the final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="17e3b-149">Accept the default endpoint entries.</span><span class="sxs-lookup"><span data-stu-id="17e3b-149">Accept the default endpoint entries.</span></span>
   2. <span data-ttu-id="17e3b-150">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-150">Click **Complete**.</span></span>

## <a name="to-remotely-log-in-to-your-virtual-machine"></a><span data-ttu-id="17e3b-151">To remotely log in to your virtual machine</span><span class="sxs-lookup"><span data-stu-id="17e3b-151">To remotely log in to your virtual machine</span></span>
1. <span data-ttu-id="17e3b-152">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="17e3b-152">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="17e3b-153">Click **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="17e3b-154">Click the name of the virtual machine that you want to log in to.</span><span class="sxs-lookup"><span data-stu-id="17e3b-154">Click the name of the virtual machine that you want to log in to.</span></span>
4. <span data-ttu-id="17e3b-155">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-155">Click **Connect**.</span></span>
5. <span data-ttu-id="17e3b-156">Respond to the prompts as needed to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17e3b-156">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="17e3b-157">When prompted for the administrator name and password, use the values that you provided when you created the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17e3b-157">When prompted for the administrator name and password, use the values that you provided when you created the virtual machine.</span></span>

<span data-ttu-id="17e3b-158">Note that the Azure Service Bus functionality requires the Baltimore CyberTrust Root certificate to be installed as part of your JRE's **cacerts** store.</span><span class="sxs-lookup"><span data-stu-id="17e3b-158">Note that the Azure Service Bus functionality requires the Baltimore CyberTrust Root certificate to be installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="17e3b-159">This certificate is automatically included in the Java Runtime Environment (JRE) used by this tutorial.</span><span class="sxs-lookup"><span data-stu-id="17e3b-159">This certificate is automatically included in the Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="17e3b-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing the certificates in your cacerts store).</span><span class="sxs-lookup"><span data-stu-id="17e3b-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing the certificates in your cacerts store).</span></span>

## <a name="how-to-create-a-service-bus-namespace"></a><span data-ttu-id="17e3b-161">How to create a service bus namespace</span><span class="sxs-lookup"><span data-stu-id="17e3b-161">How to create a service bus namespace</span></span>
<span data-ttu-id="17e3b-162">To begin using Service Bus queues in Azure, you must first create a service namespace.</span><span class="sxs-lookup"><span data-stu-id="17e3b-162">To begin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="17e3b-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span><span class="sxs-lookup"><span data-stu-id="17e3b-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="17e3b-164">To create a service namespace:</span><span class="sxs-lookup"><span data-stu-id="17e3b-164">To create a service namespace:</span></span>

1. <span data-ttu-id="17e3b-165">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="17e3b-165">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="17e3b-166">In the lower-left navigation pane of the Azure classic portal, click **Service Bus, Access Control & Caching**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-166">In the lower-left navigation pane of the Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="17e3b-167">In the upper-left pane of the Azure classic portal, click the **Service Bus** node, and then click the **New** button.</span><span class="sxs-lookup"><span data-stu-id="17e3b-167">In the upper-left pane of the Azure classic portal, click the **Service Bus** node, and then click the **New** button.</span></span>  
   <span data-ttu-id="17e3b-168">![Service Bus Node screenshot][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="17e3b-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="17e3b-169">In the **Create a new Service Namespace** dialog box, enter a **Namespace**, and then to make sure that it is unique, click the **Check Availability** button.</span><span class="sxs-lookup"><span data-stu-id="17e3b-169">In the **Create a new Service Namespace** dialog box, enter a **Namespace**, and then to make sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="17e3b-170">![Create a New Namespace screenshot][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="17e3b-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="17e3b-171">After making sure the namespace name is available, choose the country or region in which your namespace should be hosted, and then click the **Create Namespace** button.</span><span class="sxs-lookup"><span data-stu-id="17e3b-171">After making sure the namespace name is available, choose the country or region in which your namespace should be hosted, and then click the **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="17e3b-172">The namespace you created will then appear in the Azure classic portal and takes a moment to activate.</span><span class="sxs-lookup"><span data-stu-id="17e3b-172">The namespace you created will then appear in the Azure classic portal and takes a moment to activate.</span></span> <span data-ttu-id="17e3b-173">Wait until the status is **Active** before continuing with the next step.</span><span class="sxs-lookup"><span data-stu-id="17e3b-173">Wait until the status is **Active** before continuing with the next step.</span></span>

## <a name="obtain-the-default-management-credentials-for-the-namespace"></a><span data-ttu-id="17e3b-174">Obtain the Default Management Credentials for the namespace</span><span class="sxs-lookup"><span data-stu-id="17e3b-174">Obtain the Default Management Credentials for the namespace</span></span>
<span data-ttu-id="17e3b-175">In order to perform management operations, such as creating a queue, on the new namespace, you need to obtain the management credentials for the namespace.</span><span class="sxs-lookup"><span data-stu-id="17e3b-175">In order to perform management operations, such as creating a queue, on the new namespace, you need to obtain the management credentials for the namespace.</span></span>

1. <span data-ttu-id="17e3b-176">In the left navigation pane, click the **Service Bus** node to display the list of available namespaces.</span><span class="sxs-lookup"><span data-stu-id="17e3b-176">In the left navigation pane, click the **Service Bus** node to display the list of available namespaces.</span></span>
   <span data-ttu-id="17e3b-177">![Available Namespaces screenshot][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="17e3b-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="17e3b-178">Select the namespace you just created from the list shown.</span><span class="sxs-lookup"><span data-stu-id="17e3b-178">Select the namespace you just created from the list shown.</span></span>
   <span data-ttu-id="17e3b-179">![Namespace List screenshot][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="17e3b-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="17e3b-180">The right-hand **Properties** pane lists the properties for the new namespace.</span><span class="sxs-lookup"><span data-stu-id="17e3b-180">The right-hand **Properties** pane lists the properties for the new namespace.</span></span>
   <span data-ttu-id="17e3b-181">![Properties Pane screenshot][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="17e3b-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="17e3b-182">The **Default Key** is hidden.</span><span class="sxs-lookup"><span data-stu-id="17e3b-182">The **Default Key** is hidden.</span></span> <span data-ttu-id="17e3b-183">Click the **View** button to display the security credentials.</span><span class="sxs-lookup"><span data-stu-id="17e3b-183">Click the **View** button to display the security credentials.</span></span>
   <span data-ttu-id="17e3b-184">![Default Key screenshot][default_key]</span><span class="sxs-lookup"><span data-stu-id="17e3b-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="17e3b-185">Make a note of the **Default Issuer** and the **Default Key** as you will use this information below to perform operations with the namespace.</span><span class="sxs-lookup"><span data-stu-id="17e3b-185">Make a note of the **Default Issuer** and the **Default Key** as you will use this information below to perform operations with the namespace.</span></span>

## <a name="how-to-create-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="17e3b-186">How to create a Java application that performs a compute-intensive task</span><span class="sxs-lookup"><span data-stu-id="17e3b-186">How to create a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="17e3b-187">On your development machine (which does not have to be the virtual machine that you created), download the [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="17e3b-187">On your development machine (which does not have to be the virtual machine that you created), download the [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="17e3b-188">Create a Java console application using the example code at the end of this section.</span><span class="sxs-lookup"><span data-stu-id="17e3b-188">Create a Java console application using the example code at the end of this section.</span></span> <span data-ttu-id="17e3b-189">In this tutorial, we'll use **TSPSolver.java** as the Java file name.</span><span class="sxs-lookup"><span data-stu-id="17e3b-189">In this tutorial, we'll use **TSPSolver.java** as the Java file name.</span></span> <span data-ttu-id="17e3b-190">Modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span><span class="sxs-lookup"><span data-stu-id="17e3b-190">Modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="17e3b-191">After coding, export the application to a runnable Java archive (JAR), and package the required libraries into the generated JAR.</span><span class="sxs-lookup"><span data-stu-id="17e3b-191">After coding, export the application to a runnable Java archive (JAR), and package the required libraries into the generated JAR.</span></span> <span data-ttu-id="17e3b-192">In this tutorial, we'll use **TSPSolver.jar** as the generated JAR name.</span><span class="sxs-lookup"><span data-stu-id="17e3b-192">In this tutorial, we'll use **TSPSolver.jar** as the generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often to provide an update to the console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as the default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing to occur other than creating the queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing to occur other than deleting the queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume the value passed in is the number of cities to solve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-to-create-a-java-application-that-monitors-the-progress-of-the-compute-intensive-task"></a><span data-ttu-id="17e3b-193">How to create a Java application that monitors the progress of the compute-intensive task</span><span class="sxs-lookup"><span data-stu-id="17e3b-193">How to create a Java application that monitors the progress of the compute-intensive task</span></span>
1. <span data-ttu-id="17e3b-194">On your development machine, create a Java console application using the example code at the end of this section.</span><span class="sxs-lookup"><span data-stu-id="17e3b-194">On your development machine, create a Java console application using the example code at the end of this section.</span></span> <span data-ttu-id="17e3b-195">In this tutorial, we'll use **TSPClient.java** as the Java file name.</span><span class="sxs-lookup"><span data-stu-id="17e3b-195">In this tutorial, we'll use **TSPClient.java** as the Java file name.</span></span> <span data-ttu-id="17e3b-196">As shown earlier, modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span><span class="sxs-lookup"><span data-stu-id="17e3b-196">As shown earlier, modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="17e3b-197">Export the application to a runnable JAR, and package the required libraries into the generated JAR.</span><span class="sxs-lookup"><span data-stu-id="17e3b-197">Export the application to a runnable JAR, and package the required libraries into the generated JAR.</span></span> <span data-ttu-id="17e3b-198">In this tutorial, we'll use **TSPClient.jar** as the generated JAR name.</span><span class="sxs-lookup"><span data-stu-id="17e3b-198">In this tutorial, we'll use **TSPClient.jar** as the generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as the default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display the queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing to occur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // The queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-to-run-the-java-applications"></a><span data-ttu-id="17e3b-199">How to run the Java applications</span><span class="sxs-lookup"><span data-stu-id="17e3b-199">How to run the Java applications</span></span>
<span data-ttu-id="17e3b-200">Run the compute-intensive application, first to create the queue, then to solve the Traveling Saleseman Problem, which will add the current best route to the service bus queue.</span><span class="sxs-lookup"><span data-stu-id="17e3b-200">Run the compute-intensive application, first to create the queue, then to solve the Traveling Saleseman Problem, which will add the current best route to the service bus queue.</span></span> <span data-ttu-id="17e3b-201">While the compute-intensive application is running (or afterwards), run the client to display results from the service bus queue.</span><span class="sxs-lookup"><span data-stu-id="17e3b-201">While the compute-intensive application is running (or afterwards), run the client to display results from the service bus queue.</span></span>

### <a name="to-run-the-compute-intensive-application"></a><span data-ttu-id="17e3b-202">To run the compute-intensive application</span><span class="sxs-lookup"><span data-stu-id="17e3b-202">To run the compute-intensive application</span></span>
1. <span data-ttu-id="17e3b-203">Log on to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17e3b-203">Log on to your virtual machine.</span></span>
2. <span data-ttu-id="17e3b-204">Create a folder where you will run your application.</span><span class="sxs-lookup"><span data-stu-id="17e3b-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="17e3b-205">For example, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="17e3b-206">Copy **TSPSolver.jar** to **c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="17e3b-206">Copy **TSPSolver.jar** to **c:\TSP**,</span></span>
4. <span data-ttu-id="17e3b-207">Create a file named **c:\TSP\cities.txt** with the following contents.</span><span class="sxs-lookup"><span data-stu-id="17e3b-207">Create a file named **c:\TSP\cities.txt** with the following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="17e3b-208">At a command prompt, change directories to c:\TSP.</span><span class="sxs-lookup"><span data-stu-id="17e3b-208">At a command prompt, change directories to c:\TSP.</span></span>
6. <span data-ttu-id="17e3b-209">Ensure the JRE's bin folder is in the PATH environment variable.</span><span class="sxs-lookup"><span data-stu-id="17e3b-209">Ensure the JRE's bin folder is in the PATH environment variable.</span></span>
7. <span data-ttu-id="17e3b-210">You'll need to create the service bus queue before you run the TSP solver permutations.</span><span class="sxs-lookup"><span data-stu-id="17e3b-210">You'll need to create the service bus queue before you run the TSP solver permutations.</span></span> <span data-ttu-id="17e3b-211">Run the following command to create the service bus queue.</span><span class="sxs-lookup"><span data-stu-id="17e3b-211">Run the following command to create the service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="17e3b-212">Now that the queue is created, you can run the TSP solver permutations.</span><span class="sxs-lookup"><span data-stu-id="17e3b-212">Now that the queue is created, you can run the TSP solver permutations.</span></span> <span data-ttu-id="17e3b-213">For example, run the following command to run the solver for 8 cities.</span><span class="sxs-lookup"><span data-stu-id="17e3b-213">For example, run the following command to run the solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="17e3b-214">If you don't specify a number, it will run for 10 cities.</span><span class="sxs-lookup"><span data-stu-id="17e3b-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="17e3b-215">As the solver finds current shortest routes, it will add them to the queue.</span><span class="sxs-lookup"><span data-stu-id="17e3b-215">As the solver finds current shortest routes, it will add them to the queue.</span></span>

> [!NOTE]
> <span data-ttu-id="17e3b-216">The larger the number that you specify, the longer the solver will run.</span><span class="sxs-lookup"><span data-stu-id="17e3b-216">The larger the number that you specify, the longer the solver will run.</span></span> <span data-ttu-id="17e3b-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span><span class="sxs-lookup"><span data-stu-id="17e3b-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="17e3b-218">Increasing to 16 or more cities could result in days of runtime (eventually weeks, months, and years).</span><span class="sxs-lookup"><span data-stu-id="17e3b-218">Increasing to 16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="17e3b-219">This is due to the rapid increase in the number of permutations evaluated by the solver as the number of cities increases.</span><span class="sxs-lookup"><span data-stu-id="17e3b-219">This is due to the rapid increase in the number of permutations evaluated by the solver as the number of cities increases.</span></span>
> 
> 

### <a name="how-to-run-the-monitoring-client-application"></a><span data-ttu-id="17e3b-220">How to run the monitoring client application</span><span class="sxs-lookup"><span data-stu-id="17e3b-220">How to run the monitoring client application</span></span>
1. <span data-ttu-id="17e3b-221">Log on to your machine where you will run the client application.</span><span class="sxs-lookup"><span data-stu-id="17e3b-221">Log on to your machine where you will run the client application.</span></span> <span data-ttu-id="17e3b-222">This does not need to be the same machine running the **TSPSolver** application, although it can be.</span><span class="sxs-lookup"><span data-stu-id="17e3b-222">This does not need to be the same machine running the **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="17e3b-223">Create a folder where you will run your application.</span><span class="sxs-lookup"><span data-stu-id="17e3b-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="17e3b-224">For example, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="17e3b-225">Copy **TSPClient.jar** to **c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="17e3b-225">Copy **TSPClient.jar** to **c:\TSP**,</span></span>
4. <span data-ttu-id="17e3b-226">Ensure the JRE's bin folder is in the PATH environment variable.</span><span class="sxs-lookup"><span data-stu-id="17e3b-226">Ensure the JRE's bin folder is in the PATH environment variable.</span></span>
5. <span data-ttu-id="17e3b-227">At a command prompt, change directories to c:\TSP.</span><span class="sxs-lookup"><span data-stu-id="17e3b-227">At a command prompt, change directories to c:\TSP.</span></span>
6. <span data-ttu-id="17e3b-228">Run the following command.</span><span class="sxs-lookup"><span data-stu-id="17e3b-228">Run the following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="17e3b-229">Optionally, specify the number of minutes to sleep in between checking the queue, by passing in a command-line argument.</span><span class="sxs-lookup"><span data-stu-id="17e3b-229">Optionally, specify the number of minutes to sleep in between checking the queue, by passing in a command-line argument.</span></span> <span data-ttu-id="17e3b-230">The default sleep period for checking the queue is 3 minutes, which is used if no command-line argument is passed to **TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="17e3b-230">The default sleep period for checking the queue is 3 minutes, which is used if no command-line argument is passed to **TSPClient**.</span></span> <span data-ttu-id="17e3b-231">If you want to use a different value for the sleep interval, for example, one minute, run the following command.</span><span class="sxs-lookup"><span data-stu-id="17e3b-231">If you want to use a different value for the sleep interval, for example, one minute, run the following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="17e3b-232">The client will run until it sees a queue message of "Complete".</span><span class="sxs-lookup"><span data-stu-id="17e3b-232">The client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="17e3b-233">Note that if you run multiple occurrences of the solver without running the client, you may need to run the client multiple times to completely empty the queue.</span><span class="sxs-lookup"><span data-stu-id="17e3b-233">Note that if you run multiple occurrences of the solver without running the client, you may need to run the client multiple times to completely empty the queue.</span></span> <span data-ttu-id="17e3b-234">Alternatively, you can delete the queue and then create it again.</span><span class="sxs-lookup"><span data-stu-id="17e3b-234">Alternatively, you can delete the queue and then create it again.</span></span> <span data-ttu-id="17e3b-235">To delete the queue, run the following **TSPSolver** (not **TSPClient**)  command.</span><span class="sxs-lookup"><span data-stu-id="17e3b-235">To delete the queue, run the following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="17e3b-236">The solver will run until it finishes examining all routes.</span><span class="sxs-lookup"><span data-stu-id="17e3b-236">The solver will run until it finishes examining all routes.</span></span>

## <a name="how-to-stop-the-java-applications"></a><span data-ttu-id="17e3b-237">How to stop the Java applications</span><span class="sxs-lookup"><span data-stu-id="17e3b-237">How to stop the Java applications</span></span>
<span data-ttu-id="17e3b-238">For both the solver and client applications, you can press **Ctrl+C** to exit if you want to end prior to normal completion.</span><span class="sxs-lookup"><span data-stu-id="17e3b-238">For both the solver and client applications, you can press **Ctrl+C** to exit if you want to end prior to normal completion.</span></span>

[solver_output]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md








