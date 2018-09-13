---
title: NoSQL C++ tutorial for DocumentDB | Microsoft Docs
description: A NoSQL C++ tutorial that creates a C++ database and console application using a DocumentDB endorsed SDK for C++. DocumentDB is a planet-scale NoSQL database service.
services: documentdb
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: ''
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: hero-article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: fee792a61022e257399b3007b296180d225987bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552205"
---
# <a name="nosql-c-tutorial-documentdb-c-console-application"></a><span data-ttu-id="6eae7-104">NoSQL C++ tutorial: DocumentDB C++ console application</span><span class="sxs-lookup"><span data-stu-id="6eae7-104">NoSQL C++ tutorial: DocumentDB C++ console application</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](documentdb-mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="6eae7-111">Welcome to the C++ tutorial for the Azure DocumentDB endorsed SDK for C++!</span><span class="sxs-lookup"><span data-stu-id="6eae7-111">Welcome to the C++ tutorial for the Azure DocumentDB endorsed SDK for C++!</span></span> <span data-ttu-id="6eae7-112">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources, including a C++ database.</span><span class="sxs-lookup"><span data-stu-id="6eae7-112">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources, including a C++ database.</span></span>

<span data-ttu-id="6eae7-113">We'll cover:</span><span class="sxs-lookup"><span data-stu-id="6eae7-113">We'll cover:</span></span>

* <span data-ttu-id="6eae7-114">Creating and connecting to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="6eae7-114">Creating and connecting to a DocumentDB account</span></span>
* <span data-ttu-id="6eae7-115">Setting up your application</span><span class="sxs-lookup"><span data-stu-id="6eae7-115">Setting up your application</span></span>
* <span data-ttu-id="6eae7-116">Creating a C++ DocumentDB database</span><span class="sxs-lookup"><span data-stu-id="6eae7-116">Creating a C++ DocumentDB database</span></span>
* <span data-ttu-id="6eae7-117">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="6eae7-117">Creating a collection</span></span>
* <span data-ttu-id="6eae7-118">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="6eae7-118">Creating JSON documents</span></span>
* <span data-ttu-id="6eae7-119">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="6eae7-119">Querying the collection</span></span>
* <span data-ttu-id="6eae7-120">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="6eae7-120">Replacing a document</span></span>
* <span data-ttu-id="6eae7-121">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="6eae7-121">Deleting a document</span></span>
* <span data-ttu-id="6eae7-122">Deleting the C++ DocumentDB database</span><span class="sxs-lookup"><span data-stu-id="6eae7-122">Deleting the C++ DocumentDB database</span></span>

<span data-ttu-id="6eae7-123">Don't have time?</span><span class="sxs-lookup"><span data-stu-id="6eae7-123">Don't have time?</span></span> <span data-ttu-id="6eae7-124">Don't worry!</span><span class="sxs-lookup"><span data-stu-id="6eae7-124">Don't worry!</span></span> <span data-ttu-id="6eae7-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="6eae7-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="6eae7-126">See [Get the complete solution](#GetSolution) for quick instructions.</span><span class="sxs-lookup"><span data-stu-id="6eae7-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="6eae7-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span><span class="sxs-lookup"><span data-stu-id="6eae7-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="6eae7-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="6eae7-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="6eae7-129">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="6eae7-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="6eae7-130">Prerequisites for the C++ tutorial</span><span class="sxs-lookup"><span data-stu-id="6eae7-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="6eae7-131">Please make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="6eae7-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="6eae7-132">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="6eae7-132">An active Azure account.</span></span> <span data-ttu-id="6eae7-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6eae7-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6eae7-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span><span class="sxs-lookup"><span data-stu-id="6eae7-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-a-documentdb-account"></a><span data-ttu-id="6eae7-135">Step 1: Create a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="6eae7-135">Step 1: Create a DocumentDB account</span></span>
<span data-ttu-id="6eae7-136">Let's create a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="6eae7-136">Let's create a DocumentDB account.</span></span> <span data-ttu-id="6eae7-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="6eae7-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

## <a id="SetupC++"></a><span data-ttu-id="6eae7-138">Step 2: Set up your C++ application</span><span class="sxs-lookup"><span data-stu-id="6eae7-138">Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="6eae7-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="6eae7-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="6eae7-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span><span class="sxs-lookup"><span data-stu-id="6eae7-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="6eae7-141">Name the project hellodocumentdb and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eae7-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Screenshot of the New project wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-cpp-get-started/hellodocumentdb.png)
3. <span data-ttu-id="6eae7-143">When the Win32 Application Wizard starts, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="6eae7-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="6eae7-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="6eae7-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Screenshot showing Manage NuGet Package on the project menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="6eae7-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="6eae7-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="6eae7-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="6eae7-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="6eae7-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="6eae7-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![Screenshot showing the DocumentDbCpp package highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-cpp-get-started/documentdbcpp.png)
   
    <span data-ttu-id="6eae7-150">Once the packages have been added to your project, we are all set to start writing some code.</span><span class="sxs-lookup"><span data-stu-id="6eae7-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <a id="Config"></a><span data-ttu-id="6eae7-151">Step 3: Copy connection details from Azure portal for your DocumentDB database</span><span class="sxs-lookup"><span data-stu-id="6eae7-151">Step 3: Copy connection details from Azure portal for your DocumentDB database</span></span>
<span data-ttu-id="6eae7-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the NoSQL (DocumentDB) database account you created.</span><span class="sxs-lookup"><span data-stu-id="6eae7-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the NoSQL (DocumentDB) database account you created.</span></span> <span data-ttu-id="6eae7-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span><span class="sxs-lookup"><span data-stu-id="6eae7-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![DocumentDB URI and keys in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a><span data-ttu-id="6eae7-155">Step 4: Connect to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="6eae7-155">Step 4: Connect to a DocumentDB account</span></span>
1. <span data-ttu-id="6eae7-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="6eae7-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="6eae7-157">Next add the following code to your main function and replace the account configuration and primary key to match your DocumentDB settings from step 3.</span><span class="sxs-lookup"><span data-stu-id="6eae7-157">Next add the following code to your main function and replace the account configuration and primary key to match your DocumentDB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="6eae7-158">Now that you have the code to initialize the documentdb client, let's take a look at working with DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="6eae7-158">Now that you have the code to initialize the documentdb client, let's take a look at working with DocumentDB resources.</span></span>

## <a id="CreateDBColl"></a><span data-ttu-id="6eae7-159">Step 5: Create a C++ database and collection</span><span class="sxs-lookup"><span data-stu-id="6eae7-159">Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="6eae7-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6eae7-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to DocumentDB.</span></span> <span data-ttu-id="6eae7-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span><span class="sxs-lookup"><span data-stu-id="6eae7-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="6eae7-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="6eae7-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="6eae7-163">You can learn more about the DocumentDB hierarchical resource model and concepts in [DocumentDB hierarchical resource model and concepts](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6eae7-163">You can learn more about the DocumentDB hierarchical resource model and concepts in [DocumentDB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="6eae7-164">To create a database and a corresponding collection add the following code to the end of your main function.</span><span class="sxs-lookup"><span data-stu-id="6eae7-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="6eae7-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span><span class="sxs-lookup"><span data-stu-id="6eae7-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a><span data-ttu-id="6eae7-166">Step 6: Create a document</span><span class="sxs-lookup"><span data-stu-id="6eae7-166">Step 6: Create a document</span></span>
<span data-ttu-id="6eae7-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="6eae7-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="6eae7-168">You can now insert a document into DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6eae7-168">You can now insert a document into DocumentDB.</span></span> <span data-ttu-id="6eae7-169">You can create a document by copying the following code into the end of the main function.</span><span class="sxs-lookup"><span data-stu-id="6eae7-169">You can create a document by copying the following code into the end of the main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="6eae7-170">To summarize, this code creates a DocumentDB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6eae7-170">To summarize, this code creates a DocumentDB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![C++ tutorial - Diagram illustrating the hierarchical relationship between the account, the database, the collection, and the documents](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-cpp-get-started/documentdbdocs.png)

## <a id="QueryDB"></a><span data-ttu-id="6eae7-172">Step 7: Query DocumentDB resources</span><span class="sxs-lookup"><span data-stu-id="6eae7-172">Step 7: Query DocumentDB resources</span></span>
<span data-ttu-id="6eae7-173">DocumentDB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="6eae7-173">DocumentDB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="6eae7-174">The following sample code shows a query made using DocumentDB SQL syntax that you can run against the documents we created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="6eae7-174">The following sample code shows a query made using DocumentDB SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="6eae7-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span><span class="sxs-lookup"><span data-stu-id="6eae7-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="6eae7-176">Add this code before main function.</span><span class="sxs-lookup"><span data-stu-id="6eae7-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Replace"></a><span data-ttu-id="6eae7-177">Step 8: Replace a document</span><span class="sxs-lookup"><span data-stu-id="6eae7-177">Step 8: Replace a document</span></span>
<span data-ttu-id="6eae7-178">DocumentDB supports replacing JSON documents, as demonstrated in the following code.</span><span class="sxs-lookup"><span data-stu-id="6eae7-178">DocumentDB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="6eae7-179">Add this code after the executesimplequery function.</span><span class="sxs-lookup"><span data-stu-id="6eae7-179">Add this code after the executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <a id="Delete"></a><span data-ttu-id="6eae7-180">Step 9: Delete a document</span><span class="sxs-lookup"><span data-stu-id="6eae7-180">Step 9: Delete a document</span></span>
<span data-ttu-id="6eae7-181">DocumentDB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span><span class="sxs-lookup"><span data-stu-id="6eae7-181">DocumentDB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="DeleteDB"></a><span data-ttu-id="6eae7-182">Step 10: Delete a database</span><span class="sxs-lookup"><span data-stu-id="6eae7-182">Step 10: Delete a database</span></span>
<span data-ttu-id="6eae7-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="6eae7-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="6eae7-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span><span class="sxs-lookup"><span data-stu-id="6eae7-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a><span data-ttu-id="6eae7-185">Step 11: Run your C++ application all together!</span><span class="sxs-lookup"><span data-stu-id="6eae7-185">Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="6eae7-186">We have now added code to create, query, modify, and delete different DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="6eae7-186">We have now added code to create, query, modify, and delete different DocumentDB resources.</span></span>  <span data-ttu-id="6eae7-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span><span class="sxs-lookup"><span data-stu-id="6eae7-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="6eae7-188">You can do so by replacing the main function of your application with the following code.</span><span class="sxs-lookup"><span data-stu-id="6eae7-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="6eae7-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span><span class="sxs-lookup"><span data-stu-id="6eae7-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="6eae7-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span><span class="sxs-lookup"><span data-stu-id="6eae7-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="6eae7-191">You should see the output of your get started app.</span><span class="sxs-lookup"><span data-stu-id="6eae7-191">You should see the output of your get started app.</span></span> <span data-ttu-id="6eae7-192">The output should match the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="6eae7-192">The output should match the following screenshot.</span></span>

![DocumentDB C++ application output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-cpp-get-started/docdbconsole.png)

<span data-ttu-id="6eae7-194">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="6eae7-194">Congratulations!</span></span> <span data-ttu-id="6eae7-195">You've completed the C++ tutorial and have your first DocumentDB console application!</span><span class="sxs-lookup"><span data-stu-id="6eae7-195">You've completed the C++ tutorial and have your first DocumentDB console application!</span></span>

## <a id="GetSolution"></a><span data-ttu-id="6eae7-196">Get the complete C++ tutorial solution</span><span class="sxs-lookup"><span data-stu-id="6eae7-196">Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="6eae7-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="6eae7-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="6eae7-198">[DocumentDB account][documentdb-create-account].</span><span class="sxs-lookup"><span data-stu-id="6eae7-198">[DocumentDB account][documentdb-create-account].</span></span>
* <span data-ttu-id="6eae7-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="6eae7-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eae7-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="6eae7-200">Next steps</span></span>
* <span data-ttu-id="6eae7-201">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="6eae7-201">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span></span>
* <span data-ttu-id="6eae7-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="6eae7-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="6eae7-203">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="6eae7-203">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[documentdb-create-account]: documentdb-create-account.md








