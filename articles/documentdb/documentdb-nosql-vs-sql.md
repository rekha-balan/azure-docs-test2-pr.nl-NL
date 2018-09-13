---
title: When to use NoSQL vs SQL | Microsoft Docs
description: Compare the benefits of using NoSQL non-relational solutions versus SQL solutions. Learn whether one of the Microsoft Azure NoSQL services or SQL Server best fits your scenario.
keywords: nosql vs sql, when to use NoSQL, sql vs nosql
services: documentdb
documentationcenter: ''
author: mimig1
manager: jhubbard
editor: ''
ms.assetid: 71ef1798-d709-4ccb-9f5c-57948fb96229
ms.service: documentdb
ms.custom: overview
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/14/2017
ms.author: mimig
ms.openlocfilehash: ccccf8db90857761dd2b2232c75cac3b0cb53a70
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552163"
---
# <a name="nosql-vs-sql"></a><span data-ttu-id="cf73c-105">NoSQL vs SQL</span><span class="sxs-lookup"><span data-stu-id="cf73c-105">NoSQL vs SQL</span></span>
<span data-ttu-id="cf73c-106">SQL Server and relational databases (RDBMS) have been the go-to databases for over 20 years.</span><span class="sxs-lookup"><span data-stu-id="cf73c-106">SQL Server and relational databases (RDBMS) have been the go-to databases for over 20 years.</span></span> <span data-ttu-id="cf73c-107">However, the increased need to process higher volumes, velocities, and varieties of data at a rapid rate has altered the nature of data storage needs for application developers.</span><span class="sxs-lookup"><span data-stu-id="cf73c-107">However, the increased need to process higher volumes, velocities, and varieties of data at a rapid rate has altered the nature of data storage needs for application developers.</span></span> <span data-ttu-id="cf73c-108">In order to enable this scenario, NoSQL databases that enable storing unstructured and heterogeneous data at scale have gained in popularity.</span><span class="sxs-lookup"><span data-stu-id="cf73c-108">In order to enable this scenario, NoSQL databases that enable storing unstructured and heterogeneous data at scale have gained in popularity.</span></span> <span data-ttu-id="cf73c-109">For most developers, relational databases are the default or go-to option because a table structure is easy to understand and is familiar, but there are many reasons to explore beyond relational databases.</span><span class="sxs-lookup"><span data-stu-id="cf73c-109">For most developers, relational databases are the default or go-to option because a table structure is easy to understand and is familiar, but there are many reasons to explore beyond relational databases.</span></span>

<span data-ttu-id="cf73c-110">NoSQL is a category of databases distinctly different from SQL databases.</span><span class="sxs-lookup"><span data-stu-id="cf73c-110">NoSQL is a category of databases distinctly different from SQL databases.</span></span> <span data-ttu-id="cf73c-111">NoSQL is often used to refer to data management systems that are “Not SQL” or an approach to data management that includes “Not only SQL".</span><span class="sxs-lookup"><span data-stu-id="cf73c-111">NoSQL is often used to refer to data management systems that are “Not SQL” or an approach to data management that includes “Not only SQL".</span></span> <span data-ttu-id="cf73c-112">There are a number of technologies in the NoSQL category, including document databases, key value stores, column family stores, and graph databases, which are popular with gaming, social, and IoT apps.</span><span class="sxs-lookup"><span data-stu-id="cf73c-112">There are a number of technologies in the NoSQL category, including document databases, key value stores, column family stores, and graph databases, which are popular with gaming, social, and IoT apps.</span></span>

![NoSQL vs SQL overview diagram demonstrating common scenarios and data models](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-vs-sql/nosql-vs-sql-overview.png)

<span data-ttu-id="cf73c-114">The goal of this article is to help you learn about the differences between NoSQL and SQL, and provide you with an introduction to the NoSQL and SQL offerings from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cf73c-114">The goal of this article is to help you learn about the differences between NoSQL and SQL, and provide you with an introduction to the NoSQL and SQL offerings from Microsoft.</span></span>  

## <a name="when-to-use-nosql"></a><span data-ttu-id="cf73c-115">When to use NoSQL?</span><span class="sxs-lookup"><span data-stu-id="cf73c-115">When to use NoSQL?</span></span>
<span data-ttu-id="cf73c-116">Let's imagine you're building a new social engagement site.</span><span class="sxs-lookup"><span data-stu-id="cf73c-116">Let's imagine you're building a new social engagement site.</span></span> <span data-ttu-id="cf73c-117">Users can create posts and add pictures, videos and music to them.</span><span class="sxs-lookup"><span data-stu-id="cf73c-117">Users can create posts and add pictures, videos and music to them.</span></span> <span data-ttu-id="cf73c-118">Other users can comment on the posts and give points (likes) to rate the posts.</span><span class="sxs-lookup"><span data-stu-id="cf73c-118">Other users can comment on the posts and give points (likes) to rate the posts.</span></span> <span data-ttu-id="cf73c-119">The landing page will have a feed of posts that users can share and interact with.</span><span class="sxs-lookup"><span data-stu-id="cf73c-119">The landing page will have a feed of posts that users can share and interact with.</span></span> 

<span data-ttu-id="cf73c-120">So how do you store this data?</span><span class="sxs-lookup"><span data-stu-id="cf73c-120">So how do you store this data?</span></span> <span data-ttu-id="cf73c-121">If you're familiar with SQL, you might start drawing something like this:</span><span class="sxs-lookup"><span data-stu-id="cf73c-121">If you're familiar with SQL, you might start drawing something like this:</span></span>

![NoSQL vs SQL diagram showing the relational data model for a social engagement site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-vs-sql/nosql-vs-sql-social.png)

<span data-ttu-id="cf73c-123">So far, so good, but now think about the structure of a single post and how to display it.</span><span class="sxs-lookup"><span data-stu-id="cf73c-123">So far, so good, but now think about the structure of a single post and how to display it.</span></span> <span data-ttu-id="cf73c-124">If you want to show the post and the associated images, audio, video, comments, points, and user info on a website or application, you'd have to perform a query with eight table joins just to retrieve the content.</span><span class="sxs-lookup"><span data-stu-id="cf73c-124">If you want to show the post and the associated images, audio, video, comments, points, and user info on a website or application, you'd have to perform a query with eight table joins just to retrieve the content.</span></span> <span data-ttu-id="cf73c-125">Now imagine a stream of posts that dynamically load and appear on the screen and you can easily predict that it's going to require thousands of queries and many joins to complete the task.</span><span class="sxs-lookup"><span data-stu-id="cf73c-125">Now imagine a stream of posts that dynamically load and appear on the screen and you can easily predict that it's going to require thousands of queries and many joins to complete the task.</span></span>

<span data-ttu-id="cf73c-126">Now you could use a relational solution like SQL Server to store the data and query it using joins, as SQL supports dynamic data [formatted as JSON](https://msdn.microsoft.com/library/dn921897.aspx) - but there's another option, a NoSQL option that simplifies the approach for this specific scenario.</span><span class="sxs-lookup"><span data-stu-id="cf73c-126">Now you could use a relational solution like SQL Server to store the data and query it using joins, as SQL supports dynamic data [formatted as JSON](https://msdn.microsoft.com/library/dn921897.aspx) - but there's another option, a NoSQL option that simplifies the approach for this specific scenario.</span></span> <span data-ttu-id="cf73c-127">By using a single document like the following and storing it in DocumentDB, an Azure NoSQL document database service, you can increase performance and retrieve the whole post with one query and no joins.</span><span class="sxs-lookup"><span data-stu-id="cf73c-127">By using a single document like the following and storing it in DocumentDB, an Azure NoSQL document database service, you can increase performance and retrieve the whole post with one query and no joins.</span></span> <span data-ttu-id="cf73c-128">It's a simpler, more straightforward, and more performant result.</span><span class="sxs-lookup"><span data-stu-id="cf73c-128">It's a simpler, more straightforward, and more performant result.</span></span>

    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"The first video"},
            {"url":"http://mysecondvideo.mp4", "title":"The second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"The first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"The second audio"}
        ]
    }

<span data-ttu-id="cf73c-129">In addition, this data can be partitioned by post id allowing the data to scale out naturally and take advantage of NoSQL scale characteristics.</span><span class="sxs-lookup"><span data-stu-id="cf73c-129">In addition, this data can be partitioned by post id allowing the data to scale out naturally and take advantage of NoSQL scale characteristics.</span></span> <span data-ttu-id="cf73c-130">Also NoSQL systems allow developers to loosen consistency and offer highly available apps with low-latency.</span><span class="sxs-lookup"><span data-stu-id="cf73c-130">Also NoSQL systems allow developers to loosen consistency and offer highly available apps with low-latency.</span></span>  <span data-ttu-id="cf73c-131">Finally, this solution does not require developers to define, manage and maintain schema in the data tier allowing for rapid iteration.</span><span class="sxs-lookup"><span data-stu-id="cf73c-131">Finally, this solution does not require developers to define, manage and maintain schema in the data tier allowing for rapid iteration.</span></span>

<span data-ttu-id="cf73c-132">You can then build on this solution using other Azure services:</span><span class="sxs-lookup"><span data-stu-id="cf73c-132">You can then build on this solution using other Azure services:</span></span>

* <span data-ttu-id="cf73c-133">[Azure Search](https://azure.microsoft.com/services/search/) can be used via the web app to enable users to search for posts.</span><span class="sxs-lookup"><span data-stu-id="cf73c-133">[Azure Search](https://azure.microsoft.com/services/search/) can be used via the web app to enable users to search for posts.</span></span>
* <span data-ttu-id="cf73c-134">[Azure App Services](https://azure.microsoft.com/services/app-service/) can be used to host applications and background processes.</span><span class="sxs-lookup"><span data-stu-id="cf73c-134">[Azure App Services](https://azure.microsoft.com/services/app-service/) can be used to host applications and background processes.</span></span>
* <span data-ttu-id="cf73c-135">[Azure Blob Storage](https://azure.microsoft.com/services/storage/) can be used to store full user profiles including images.</span><span class="sxs-lookup"><span data-stu-id="cf73c-135">[Azure Blob Storage](https://azure.microsoft.com/services/storage/) can be used to store full user profiles including images.</span></span>
* <span data-ttu-id="cf73c-136">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/) can be used to store massive amounts of data such as login information, and data for usage analytics.</span><span class="sxs-lookup"><span data-stu-id="cf73c-136">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/) can be used to store massive amounts of data such as login information, and data for usage analytics.</span></span>
* <span data-ttu-id="cf73c-137">[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)  can be used to build knowledge and intelligence that can provide feedback to the process and help deliver the right content to the right users.</span><span class="sxs-lookup"><span data-stu-id="cf73c-137">[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)  can be used to build knowledge and intelligence that can provide feedback to the process and help deliver the right content to the right users.</span></span>

<span data-ttu-id="cf73c-138">This social engagement site is just one one scenario in which a NoSQL database is the right data model for the job.</span><span class="sxs-lookup"><span data-stu-id="cf73c-138">This social engagement site is just one one scenario in which a NoSQL database is the right data model for the job.</span></span> <span data-ttu-id="cf73c-139">If you're interested in reading more about this scenario and how to model your data for DocumentDB in social media applications, see [Going social with DocumentDB](documentdb-social-media-apps.md).</span><span class="sxs-lookup"><span data-stu-id="cf73c-139">If you're interested in reading more about this scenario and how to model your data for DocumentDB in social media applications, see [Going social with DocumentDB](documentdb-social-media-apps.md).</span></span> 

## <a name="nosql-vs-sql-comparison"></a><span data-ttu-id="cf73c-140">NoSQL vs SQL comparison</span><span class="sxs-lookup"><span data-stu-id="cf73c-140">NoSQL vs SQL comparison</span></span>
<span data-ttu-id="cf73c-141">The following table compares the main differences between NoSQL and SQL.</span><span class="sxs-lookup"><span data-stu-id="cf73c-141">The following table compares the main differences between NoSQL and SQL.</span></span> 

![NoSQL vs SQL diagram showing when to use NoSQL and when to use SQL.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-vs-sql/nosql-vs-sql-comparison.png)

<span data-ttu-id="cf73c-144">If a NoSQL database best suits your requirements, continue to the next section to learn more about the NoSQL services available from Azure.</span><span class="sxs-lookup"><span data-stu-id="cf73c-144">If a NoSQL database best suits your requirements, continue to the next section to learn more about the NoSQL services available from Azure.</span></span> <span data-ttu-id="cf73c-145">Otherwise, if a SQL database best suits your needs, skip to [What are the Microsoft SQL offerings?](#what-are-the-microsoft-sql-offerings)</span><span class="sxs-lookup"><span data-stu-id="cf73c-145">Otherwise, if a SQL database best suits your needs, skip to [What are the Microsoft SQL offerings?](#what-are-the-microsoft-sql-offerings)</span></span>

## <a name="what-are-the-microsoft-azure-nosql-offerings"></a><span data-ttu-id="cf73c-146">What are the Microsoft Azure NoSQL offerings?</span><span class="sxs-lookup"><span data-stu-id="cf73c-146">What are the Microsoft Azure NoSQL offerings?</span></span>
<span data-ttu-id="cf73c-147">Azure has four fully-managed NoSQL services:</span><span class="sxs-lookup"><span data-stu-id="cf73c-147">Azure has four fully-managed NoSQL services:</span></span> 

* [<span data-ttu-id="cf73c-148">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="cf73c-148">Azure DocumentDB</span></span>](https://azure.microsoft.com/services/documentdb/)
* [<span data-ttu-id="cf73c-149">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="cf73c-149">Azure Table Storage</span></span>](https://azure.microsoft.com/services/storage/)
* [<span data-ttu-id="cf73c-150">Azure HBase as a part of HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf73c-150">Azure HBase as a part of HDInsight</span></span>](https://azure.microsoft.com/services/hdinsight/)
* [<span data-ttu-id="cf73c-151">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="cf73c-151">Azure Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)

<span data-ttu-id="cf73c-152">The following comparison chart maps out the key differentiators for each service.</span><span class="sxs-lookup"><span data-stu-id="cf73c-152">The following comparison chart maps out the key differentiators for each service.</span></span> <span data-ttu-id="cf73c-153">Which one most accurately describes the needs of your application?</span><span class="sxs-lookup"><span data-stu-id="cf73c-153">Which one most accurately describes the needs of your application?</span></span> 

![NoSQL vs SQL diagram showing when to use NoSQL offerings from Microsoft Azure, including DocumentDB, Table Storage, HBase as a part of HDInsight, and Redis Cache](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-nosql-vs-sql/nosql-vs-sql-documentdb-storage-hbase-hdinsight-redis-cache.png)

<span data-ttu-id="cf73c-155">If one or more of these services might meet the needs of your application, learn more with the following resources:</span><span class="sxs-lookup"><span data-stu-id="cf73c-155">If one or more of these services might meet the needs of your application, learn more with the following resources:</span></span> 

* <span data-ttu-id="cf73c-156">[DocumentDB learning path](https://azure.microsoft.com/documentation/learning-paths/documentdb/) and [DocumentDB use cases](documentdb-use-cases.md)</span><span class="sxs-lookup"><span data-stu-id="cf73c-156">[DocumentDB learning path](https://azure.microsoft.com/documentation/learning-paths/documentdb/) and [DocumentDB use cases](documentdb-use-cases.md)</span></span>
* [<span data-ttu-id="cf73c-157">Get started with Azure table storage</span><span class="sxs-lookup"><span data-stu-id="cf73c-157">Get started with Azure table storage</span></span>](../storage/storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="cf73c-158">What is HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf73c-158">What is HBase in HDInsight</span></span>](../hdinsight/hdinsight-hbase-overview.md)
* [<span data-ttu-id="cf73c-159">Redis Cache learning path</span><span class="sxs-lookup"><span data-stu-id="cf73c-159">Redis Cache learning path</span></span>](https://azure.microsoft.com/documentation/learning-paths/redis-cache/)

<span data-ttu-id="cf73c-160">Then go to [Next steps](#next-steps) for free trial information.</span><span class="sxs-lookup"><span data-stu-id="cf73c-160">Then go to [Next steps](#next-steps) for free trial information.</span></span>

## <a name="what-are-the-microsoft-sql-offerings"></a><span data-ttu-id="cf73c-161">What are the Microsoft SQL offerings?</span><span class="sxs-lookup"><span data-stu-id="cf73c-161">What are the Microsoft SQL offerings?</span></span>
<span data-ttu-id="cf73c-162">Microsoft has five SQL offerings:</span><span class="sxs-lookup"><span data-stu-id="cf73c-162">Microsoft has five SQL offerings:</span></span> 

* [<span data-ttu-id="cf73c-163">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cf73c-163">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/)
* [<span data-ttu-id="cf73c-164">SQL Server on Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="cf73c-164">SQL Server on Azure Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/sql-server/)
* [<span data-ttu-id="cf73c-165">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cf73c-165">SQL Server</span></span>](https://www.microsoft.com/server-cloud/products/sql-server-2016/)
* [<span data-ttu-id="cf73c-166">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cf73c-166">Azure SQL Data Warehouse</span></span>](https://azure.microsoft.com/services/sql-data-warehouse/)
* [<span data-ttu-id="cf73c-167">Analytics Platform System (on-premises appliance)</span><span class="sxs-lookup"><span data-stu-id="cf73c-167">Analytics Platform System (on-premises appliance)</span></span>](https://www.microsoft.com/en-us/server-cloud/products/analytics-platform-system/)

<span data-ttu-id="cf73c-168">If you're interested in SQL Server on a Virtual Machine or SQL Database, then read [Choose a cloud SQL Server option: Azure SQL (PaaS) Database or SQL Server on Azure VMs (IaaS)](../sql-database/sql-database-paas-vs-sql-server-iaas.md) to learn more about the differences between the two.</span><span class="sxs-lookup"><span data-stu-id="cf73c-168">If you're interested in SQL Server on a Virtual Machine or SQL Database, then read [Choose a cloud SQL Server option: Azure SQL (PaaS) Database or SQL Server on Azure VMs (IaaS)](../sql-database/sql-database-paas-vs-sql-server-iaas.md) to learn more about the differences between the two.</span></span>

<span data-ttu-id="cf73c-169">If SQL sounds like the best option, then go to [SQL Server](https://www.microsoft.com/server-cloud/products/) to learn more about what our Microsoft SQL products and services have to offer.</span><span class="sxs-lookup"><span data-stu-id="cf73c-169">If SQL sounds like the best option, then go to [SQL Server](https://www.microsoft.com/server-cloud/products/) to learn more about what our Microsoft SQL products and services have to offer.</span></span>

<span data-ttu-id="cf73c-170">Then go to [Next steps](#next-steps) for free trial and evaluation links.</span><span class="sxs-lookup"><span data-stu-id="cf73c-170">Then go to [Next steps](#next-steps) for free trial and evaluation links.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf73c-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf73c-171">Next steps</span></span>
<span data-ttu-id="cf73c-172">We invite you to learn more about our SQL and NoSQL products by trying them out for free.</span><span class="sxs-lookup"><span data-stu-id="cf73c-172">We invite you to learn more about our SQL and NoSQL products by trying them out for free.</span></span> 

* <span data-ttu-id="cf73c-173">For all Azure services, you can sign up for a [free one-month trial](https://azure.microsoft.com/pricing/free-trial/) and receive $200 to spend on any of the Azure services.</span><span class="sxs-lookup"><span data-stu-id="cf73c-173">For all Azure services, you can sign up for a [free one-month trial](https://azure.microsoft.com/pricing/free-trial/) and receive $200 to spend on any of the Azure services.</span></span>
  
  * [<span data-ttu-id="cf73c-174">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="cf73c-174">Azure DocumentDB</span></span>](https://azure.microsoft.com/services/documentdb/)
  * [<span data-ttu-id="cf73c-175">Azure HBase as a part of HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf73c-175">Azure HBase as a part of HDInsight</span></span>](https://azure.microsoft.com/services/hdinsight/)
  * [<span data-ttu-id="cf73c-176">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="cf73c-176">Azure Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)
  * [<span data-ttu-id="cf73c-177">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cf73c-177">Azure SQL Data Warehouse</span></span>](https://azure.microsoft.com/services/sql-data-warehouse/)
  * [<span data-ttu-id="cf73c-178">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cf73c-178">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/)
  * [<span data-ttu-id="cf73c-179">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="cf73c-179">Azure Table Storage</span></span>](https://azure.microsoft.com/services/storage/)
* <span data-ttu-id="cf73c-180">You can spin up an [evaluation version of SQL Server 2016 on a virtual machine](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016ctp33evaluationwindowsserver2012r2/) or download an [evaluation version of SQL Server](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016).</span><span class="sxs-lookup"><span data-stu-id="cf73c-180">You can spin up an [evaluation version of SQL Server 2016 on a virtual machine](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016ctp33evaluationwindowsserver2012r2/) or download an [evaluation version of SQL Server](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016).</span></span>
  
  * [<span data-ttu-id="cf73c-181">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cf73c-181">SQL Server</span></span>](https://www.microsoft.com/server-cloud/products/sql-server-2016/)
  * [<span data-ttu-id="cf73c-182">SQL Server on Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="cf73c-182">SQL Server on Azure Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/sql-server/)





