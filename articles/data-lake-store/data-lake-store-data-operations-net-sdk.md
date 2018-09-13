---
title: '.NET SDK: Filesystem operations on Azure Data Lake Storage Gen1 | Microsoft Docs'
description: Use Azure Data Lake Storage Gen1 .NET SDK to perform filesystem operations on Data Lake Storage Gen1 such as create folders, etc.
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
ms.openlocfilehash: 71ddbc2363075b721bfbd418bd29e5154baba866
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865153"
---
# <a name="filesystem-operations-on-azure-data-lake-storage-gen1-using-net-sdk"></a><span data-ttu-id="b7a4f-103">Filesystem operations on Azure Data Lake Storage Gen1 using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b7a4f-103">Filesystem operations on Azure Data Lake Storage Gen1 using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [.NET SDK](data-lake-store-data-operations-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-data-operations-rest-api.md)
> * [Python](data-lake-store-data-operations-python.md)
>
>

<span data-ttu-id="b7a4f-108">In this article, you learn how to perform filesytem operations on Data Lake Storage Gen1 using .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-108">In this article, you learn how to perform filesytem operations on Data Lake Storage Gen1 using .NET SDK.</span></span> <span data-ttu-id="b7a4f-109">Filesystem operations include creating folders in a Data Lake Storage Gen1 account, uploading files, downloading files, etc.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-109">Filesystem operations include creating folders in a Data Lake Storage Gen1 account, uploading files, downloading files, etc.</span></span>

<span data-ttu-id="b7a4f-110">For instructions on how to perform account management operations on Data Lake Storage Gen1 using .NET SDK, see [Account management operations on Data Lake Storage Gen1 using .NET SDK](data-lake-store-get-started-net-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b7a4f-110">For instructions on how to perform account management operations on Data Lake Storage Gen1 using .NET SDK, see [Account management operations on Data Lake Storage Gen1 using .NET SDK](data-lake-store-get-started-net-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7a4f-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7a4f-111">Prerequisites</span></span>
* <span data-ttu-id="b7a4f-112">**Visual Studio 2013, 2015, or 2017**.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-112">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="b7a4f-113">The instructions below use Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-113">The instructions below use Visual Studio 2017.</span></span>

* <span data-ttu-id="b7a4f-114">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-114">**An Azure subscription**.</span></span> <span data-ttu-id="b7a4f-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7a4f-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="b7a4f-116">**Azure Data Lake Storage Gen1 account**.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-116">**Azure Data Lake Storage Gen1 account**.</span></span> <span data-ttu-id="b7a4f-117">For instructions on how to create an account, see [Get started with Azure Data Lake Storage Gen1](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b7a4f-117">For instructions on how to create an account, see [Get started with Azure Data Lake Storage Gen1](data-lake-store-get-started-portal.md)</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="b7a4f-118">Create a .NET application</span><span class="sxs-lookup"><span data-stu-id="b7a4f-118">Create a .NET application</span></span>
<span data-ttu-id="b7a4f-119">The code sample available [on GitHub](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-119">The code sample available [on GitHub](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span></span> <span data-ttu-id="b7a4f-120">This section of the article walks you through the main parts of the code.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-120">This section of the article walks you through the main parts of the code.</span></span>

1. <span data-ttu-id="b7a4f-121">Open Visual Studio and create a console application.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-121">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="b7a4f-122">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-122">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="b7a4f-123">From **New Project**, type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="b7a4f-123">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="b7a4f-124">Property</span><span class="sxs-lookup"><span data-stu-id="b7a4f-124">Property</span></span> | <span data-ttu-id="b7a4f-125">Value</span><span class="sxs-lookup"><span data-stu-id="b7a4f-125">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="b7a4f-126">Category</span><span class="sxs-lookup"><span data-stu-id="b7a4f-126">Category</span></span> |<span data-ttu-id="b7a4f-127">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="b7a4f-127">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="b7a4f-128">Template</span><span class="sxs-lookup"><span data-stu-id="b7a4f-128">Template</span></span> |<span data-ttu-id="b7a4f-129">Console Application</span><span class="sxs-lookup"><span data-stu-id="b7a4f-129">Console Application</span></span> |
   | <span data-ttu-id="b7a4f-130">Name</span><span class="sxs-lookup"><span data-stu-id="b7a4f-130">Name</span></span> |<span data-ttu-id="b7a4f-131">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="b7a4f-131">CreateADLApplication</span></span> |

4. <span data-ttu-id="b7a4f-132">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-132">Click **OK** to create the project.</span></span>

5. <span data-ttu-id="b7a4f-133">Add the NuGet packages to your project.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-133">Add the NuGet packages to your project.</span></span>

   1. <span data-ttu-id="b7a4f-134">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-134">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b7a4f-135">In the **NuGet Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-135">In the **NuGet Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="b7a4f-136">Search for and install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="b7a4f-136">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="b7a4f-137">`Microsoft.Azure.DataLake.Store` - This tutorial uses v1.0.0.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-137">`Microsoft.Azure.DataLake.Store` - This tutorial uses v1.0.0.</span></span>
      * <span data-ttu-id="b7a4f-138">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.3.1.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-138">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.3.1.</span></span>
    
    <span data-ttu-id="b7a4f-139">Close the **NuGet Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-139">Close the **NuGet Package Manager**.</span></span>

6. <span data-ttu-id="b7a4f-140">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-140">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span></span>

        using System;
        using System.IO;using System.Threading;
        using System.Linq;
        using System.Text;
        using System.Collections.Generic;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
                
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.DataLake.Store;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

7. <span data-ttu-id="b7a4f-141">Declare the variables as shown below, and provide the values for the placeholders.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-141">Declare the variables as shown below, and provide the values for the placeholders.</span></span> <span data-ttu-id="b7a4f-142">Also, make sure the local path and file name you provide here exist on the computer.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-142">Also, make sure the local path and file name you provide here exist on the computer.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static string _adlsg1AccountName = "<DATA-LAKE-STORAGE-GEN1-NAME>.azuredatalakestore.net";        
            }
        }

<span data-ttu-id="b7a4f-143">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-143">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="b7a4f-144">Authentication</span><span class="sxs-lookup"><span data-stu-id="b7a4f-144">Authentication</span></span>

* <span data-ttu-id="b7a4f-145">For end-user authentication for your application, see [End-user authentication with Data Lake Storage Gen1 using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b7a4f-145">For end-user authentication for your application, see [End-user authentication with Data Lake Storage Gen1 using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md).</span></span>
* <span data-ttu-id="b7a4f-146">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Storage Gen1 using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b7a4f-146">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Storage Gen1 using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md).</span></span>


## <a name="create-client-object"></a><span data-ttu-id="b7a4f-147">Create client object</span><span class="sxs-lookup"><span data-stu-id="b7a4f-147">Create client object</span></span>
<span data-ttu-id="b7a4f-148">The following snippet creates the Data Lake Storage Gen1 filesystem client object, which is used to issue requests to the service.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-148">The following snippet creates the Data Lake Storage Gen1 filesystem client object, which is used to issue requests to the service.</span></span>

    // Create client objects
    AdlsClient client = AdlsClient.CreateClient(_adlsg1AccountName, adlCreds);

## <a name="create-a-file-and-directory"></a><span data-ttu-id="b7a4f-149">Create a file and directory</span><span class="sxs-lookup"><span data-stu-id="b7a4f-149">Create a file and directory</span></span>
<span data-ttu-id="b7a4f-150">Add the following snippet to your application.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-150">Add the following snippet to your application.</span></span> <span data-ttu-id="b7a4f-151">This snippet adds a file as well as any parent directory that do not exist.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-151">This snippet adds a file as well as any parent directory that do not exist.</span></span>

    // Create a file - automatically creates any parent directories that don't exist
    // The AdlsOutputStream preserves record boundaries - it does not break records while writing to the store
    using (var stream = client.CreateFile(fileName, IfExists.Overwrite))
    {
        byte[] textByteArray = Encoding.UTF8.GetBytes("This is test data to write.\r\n");
        stream.Write(textByteArray, 0, textByteArray.Length);

        textByteArray = Encoding.UTF8.GetBytes("This is the second line.\r\n");
        stream.Write(textByteArray, 0, textByteArray.Length);
    }

## <a name="append-to-a-file"></a><span data-ttu-id="b7a4f-152">Append to a file</span><span class="sxs-lookup"><span data-stu-id="b7a4f-152">Append to a file</span></span>
<span data-ttu-id="b7a4f-153">The following snippet appends data to an existing file in Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-153">The following snippet appends data to an existing file in Data Lake Storage Gen1 account.</span></span>

    // Append to existing file
    using (var stream = client.GetAppendStream(fileName))
    {
        byte[] textByteArray = Encoding.UTF8.GetBytes("This is the added line.\r\n");
        stream.Write(textByteArray, 0, textByteArray.Length);
    }

## <a name="read-a-file"></a><span data-ttu-id="b7a4f-154">Read a file</span><span class="sxs-lookup"><span data-stu-id="b7a4f-154">Read a file</span></span>
<span data-ttu-id="b7a4f-155">The following snippet reads the contents of a file in Data Lake Storage Gen1.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-155">The following snippet reads the contents of a file in Data Lake Storage Gen1.</span></span>

    //Read file contents
    using (var readStream = new StreamReader(client.GetReadStream(fileName)))
    {
        string line;
        while ((line = readStream.ReadLine()) != null)
        {
            Console.WriteLine(line);
        }
    }

## <a name="get-file-properties"></a><span data-ttu-id="b7a4f-156">Get file properties</span><span class="sxs-lookup"><span data-stu-id="b7a4f-156">Get file properties</span></span>
<span data-ttu-id="b7a4f-157">The following snippet returns the properties associated with a file or a directory.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-157">The following snippet returns the properties associated with a file or a directory.</span></span>

    // Get file properties
    var directoryEntry = client.GetDirectoryEntry(fileName);
    PrintDirectoryEntry(directoryEntry);

<span data-ttu-id="b7a4f-158">The definition of the `PrintDirectoryEntry` method is available as part of the sample [on Github](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted).</span><span class="sxs-lookup"><span data-stu-id="b7a4f-158">The definition of the `PrintDirectoryEntry` method is available as part of the sample [on Github](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted).</span></span> 

## <a name="rename-a-file"></a><span data-ttu-id="b7a4f-159">Rename a file</span><span class="sxs-lookup"><span data-stu-id="b7a4f-159">Rename a file</span></span>
<span data-ttu-id="b7a4f-160">The following snippet renames an existing file in a Data Lake Storage Gen1 account.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-160">The following snippet renames an existing file in a Data Lake Storage Gen1 account.</span></span>

    // Rename a file
    string destFilePath = "/Test/testRenameDest3.txt";
    client.Rename(fileName, destFilePath, true);

## <a name="enumerate-a-directory"></a><span data-ttu-id="b7a4f-161">Enumerate a directory</span><span class="sxs-lookup"><span data-stu-id="b7a4f-161">Enumerate a directory</span></span>
<span data-ttu-id="b7a4f-162">The following snippet enumerates directories in a Data Lake Storage Gen1 account</span><span class="sxs-lookup"><span data-stu-id="b7a4f-162">The following snippet enumerates directories in a Data Lake Storage Gen1 account</span></span>

    // Enumerate directory
    foreach (var entry in client.EnumerateDirectory("/Test"))
    {
        PrintDirectoryEntry(entry);
    }

<span data-ttu-id="b7a4f-163">The definition of the `PrintDirectoryEntry` method is available as part of the sample [on Github](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted).</span><span class="sxs-lookup"><span data-stu-id="b7a4f-163">The definition of the `PrintDirectoryEntry` method is available as part of the sample [on Github](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted).</span></span>

## <a name="delete-directories-recursively"></a><span data-ttu-id="b7a4f-164">Delete directories recursively</span><span class="sxs-lookup"><span data-stu-id="b7a4f-164">Delete directories recursively</span></span>
<span data-ttu-id="b7a4f-165">The following snippet deletes a directory, and all its sub-directories, recursively.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-165">The following snippet deletes a directory, and all its sub-directories, recursively.</span></span>

    // Delete a directory and all its subdirectories and files
    client.DeleteRecursive("/Test");

## <a name="samples"></a><span data-ttu-id="b7a4f-166">Samples</span><span class="sxs-lookup"><span data-stu-id="b7a4f-166">Samples</span></span>
<span data-ttu-id="b7a4f-167">Here are a couple of samples on how to use the Data Lake Storage Gen1 Filesystem SDK.</span><span class="sxs-lookup"><span data-stu-id="b7a4f-167">Here are a couple of samples on how to use the Data Lake Storage Gen1 Filesystem SDK.</span></span>
* [<span data-ttu-id="b7a4f-168">Basic sample on Github</span><span class="sxs-lookup"><span data-stu-id="b7a4f-168">Basic sample on Github</span></span>](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-get-started/tree/master/AdlsSDKGettingStarted)
* [<span data-ttu-id="b7a4f-169">Advanced sample on Github</span><span class="sxs-lookup"><span data-stu-id="b7a4f-169">Advanced sample on Github</span></span>](https://github.com/Azure-Samples/data-lake-store-adls-dot-net-samples)

## <a name="see-also"></a><span data-ttu-id="b7a4f-170">See also</span><span class="sxs-lookup"><span data-stu-id="b7a4f-170">See also</span></span>
* [<span data-ttu-id="b7a4f-171">Account management operations on Data Lake Storage Gen1 using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b7a4f-171">Account management operations on Data Lake Storage Gen1 using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="b7a4f-172">Data Lake Storage Gen1 .NET SDK Reference</span><span class="sxs-lookup"><span data-stu-id="b7a4f-172">Data Lake Storage Gen1 .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet)

## <a name="next-steps"></a><span data-ttu-id="b7a4f-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7a4f-173">Next steps</span></span>
* [<span data-ttu-id="b7a4f-174">Secure data in Data Lake Storage Gen1</span><span class="sxs-lookup"><span data-stu-id="b7a4f-174">Secure data in Data Lake Storage Gen1</span></span>](data-lake-store-secure-data.md)
