---
title: DocumentDB Database Questions - Frequently Asked Questions | Microsoft Docs
description: Get answers to frequently asked questions about Azure DocumentDB a NoSQL document database service for JSON. Answer database questions about capacity, performance levels, and scaling.
keywords: Database questions, frequently asked questions, documentdb, azure, Microsoft azure
services: documentdb
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: ''
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: mimig
ms.openlocfilehash: 8ebc1aa663f298d1f3f495523d85bda8777d5d29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552916"
---
# <a name="frequently-asked-questions-about-documentdb"></a>Frequently asked questions about DocumentDB
## <a name="database-questions-about-microsoft-azure-documentdb-fundamentals"></a>Database questions about Microsoft Azure DocumentDB fundamentals
### <a name="what-is-microsoft-azure-documentdb"></a>What is Microsoft Azure DocumentDB?
Microsoft Azure DocumentDB is a blazing fast, planet-scale NoSQL document database-as-a-service that offers rich querying over schema-free data, helps deliver configurable and reliable performance, and enables rapid development, all through a managed platform backed by the power and reach of Microsoft Azure. DocumentDB is the right solution for web, mobile, gaming, and IoT applications when predictable throughput, high availability, low latency, and a schema-free data model are key requirements. DocumentDB delivers schema flexibility and rich indexing via a native JSON data model, and includes multi-document transactional support with integrated JavaScript.  

For more database questions, answers, and instructions on deploying and using this service, see the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).

### <a name="what-kind-of-database-is-documentdb"></a>What kind of database is DocumentDB?
DocumentDB is a NoSQL document oriented database that stores data in JSON format.  DocumentDB supports nested, self-contained-data structures that can be queried through a rich DocumentDB [SQL query grammar](documentdb-sql-query.md). DocumentDB provides high-performance transactional processing of server-side JavaScript through [stored procedures, triggers, and user defined functions](documentdb-programming.md). The database also supports developer tunable consistency levels with associated [performance levels](documentdb-performance-levels.md).

### <a name="do-documentdb-databases-have-tables-like-a-relational-database-rdbms"></a>Do DocumentDB databases have tables like a relational database (RDBMS)?
No, DocumentDB  stores data in collections of JSON documents.  For information on DocumentDB resources, see [DocumentDB resource model and concepts](documentdb-resources.md). For more information about how NoSQL solutions such as DocumentDB differ from relational solutions, see [NoSQL vs SQL](documentdb-nosql-vs-sql.md).

### <a name="do-documentdb-databases-support-schema-free-data"></a>Do DocumentDB databases support schema-free data?
Yes, DocumentDB allows applications to store arbitrary JSON documents without schema definition or hints. Data is immediately available for query through the DocumentDB SQL query interface.   

### <a name="does-documentdb-support-acid-transactions"></a>Does DocumentDB support ACID transactions?
Yes, DocumentDB supports cross-document transactions expressed as JavaScript stored procedures and triggers. Transactions are scoped to a single partition within each collection and executed with ACID semantics as all or nothing isolated from other concurrently executing code and user requests.  If exceptions are thrown through the server-side execution of JavaScript application code, the entire transaction is rolled back. For more information about transactions, see [Database program transactions](documentdb-programming.md#database-program-transactions).

### <a name="what-are-the-typical-use-cases-for-documentdb"></a>What are the typical use cases for DocumentDB?
DocumentDB is a good choice for new web, mobile, gaming and IoT applications where automatic scale, predictable performance, fast order of millisecond response times, and the ability to query over schema-free data is important. DocumentDB lends itself to rapid development and supporting the continuous iteration of application data models. Applications that manage user generated content and data are [common use cases for DocumentDB](documentdb-use-cases.md).  

### <a name="how-does-documentdb-offer-predictable-performance"></a>How does DocumentDB offer predictable performance?
A [request unit](documentdb-request-units.md) is the measure of throughput in DocumentDB. 1 RU corresponds to the throughput of the GET of a 1KB document. Every operation in DocumentDB, including reads, writes, SQL queries, and stored procedure executions has a deterministic RU value based on the throughput required to complete the operation. Instead of thinking about CPU, IO and memory and how they each impact your application throughput, you can think in terms of a single RU measure.

Each DocumentDB collection can be reserved with provisioned throughput in terms of RUs of throughput per second. For applications of any scale, you can benchmark individual requests to measure their RU values, and provision collections to handle the sum total of request units across all requests. You can also scale up or scale down your collection’s throughput as the needs of your application evolve. For more information about request units and for help determining your collection needs, read [Estimating throughput needs](documentdb-request-units.md#estimating-throughput-needs) and try the [throughput calculator](https://www.documentdb.com/capacityplanner).

### <a name="is-documentdb-hipaa-compliant"></a>Is DocumentDB HIPAA compliant?
Yes, DocumentDB is HIPAA-compliant. HIPAA establishes requirements for the use, disclosure, and safeguarding of individually identifiable health information. For more information, see the [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-the-storage-limits-of-documentdb"></a>What are the storage limits of DocumentDB?
There is no limit to the total amount of data that a collection can store in DocumentDB.

### <a name="what-are-the-throughput-limits-of-documentdb"></a>What are the throughput limits of DocumentDB?
There is no limit to the total amount of throughput that a collection can support in DocumentDB, if your workload can be distributed roughly evenly among a sufficiently large number of partition keys.

### <a name="how-much-does-microsoft-azure-documentdb-cost"></a>How much does Microsoft Azure DocumentDB cost?
Refer to the [DocumentDB pricing details](https://azure.microsoft.com/pricing/details/documentdb/) page for details. DocumentDB usage charges are determined by the number of collections provisioned, the number of hours the collections were online, and the provisioned throughput for each collection.

### <a name="is-there-a-free-account-available"></a>Is there a free account available?
If you are new to Azure, you can sign up for an [Azure free account](https://azure.microsoft.com/free/), which gives you 30 days and $200 to try all the Azure services. Or, if you have a Visual Studio subscription, you are eligible for [$150 in free Azure credits per month](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) to use on any Azure service.  

You can also use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to develop and test your application locally for free, without creating an Azure subscription. When you're satisfied with how your application is working in the DocumentDB Emulator, you can switch to using an Azure DocumentDB account in the cloud.

### <a name="how-can-i-get-additional-help-with-documentdb"></a>How can I get additional help with DocumentDB?
If you need any help, reach out to us on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or schedule a 1:1 chat with the DocumentDB engineering team by sending mail to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com). To stay up to date on the latest DocumentDB news and features, follow us on [Twitter](https://twitter.com/DocumentDB).

## <a name="set-up-microsoft-azure-documentdb"></a>Set up Microsoft Azure DocumentDB
### <a name="how-do-i-sign-up-for-microsoft-azure-documentdb"></a>How do I sign up for Microsoft Azure DocumentDB?
Microsoft Azure DocumentDB is available in the [Azure Portal][azure-portal].  First you must sign up for a Microsoft Azure subscription.  Once you sign up for a Microsoft Azure subscription, you can add a DocumentDB account to your Azure subscription. For instructions on adding a DocumentDB account, see [Create a DocumentDB database account](documentdb-create-account.md).   

### <a name="what-is-a-master-key"></a>What is a master key?
A master key is a security token to access all resources for an account. Individuals with the key have read and write access to the all resources in the database account. Use caution when distributing master keys. The primary master key and secondary master key are available in the **Keys **blade of the [Azure Portal][azure-portal]. For more information about keys, see [View, copy, and regenerate access keys](documentdb-manage-account.md#keys).

### <a name="how-do-i-create-a-database"></a>How do I create a database?
You can create databases using the [Azure Portal]() as described in [Create a DocumentDB collection and database](documentdb-create-collection.md), one of the [DocumentDB SDKs](documentdb-sdk-dotnet.md), or through the [REST APIs](https://msdn.microsoft.com/library/azure/dn781481.aspx).  

### <a name="what-is-a-collection"></a>What is a collection?
A collection is a container of JSON documents and the associated JavaScript application logic. A collection is a billable entity, where the [cost](documentdb-performance-levels.md) is determined by the throughput and storage used. Collections can span one or more partitions/servers and can scale to handle practically unlimited volumes of storage or throughput.

Collections are also the billing entities for DocumentDB. Each collection is billed hourly based on the provisioned throughput and the storage space used. For more information, see [DocumentDB pricing](https://azure.microsoft.com/pricing/details/documentdb/).  

### <a name="how-do-i-set-up-users-and-permissions"></a>How do I set up users and permissions?
You can create users and permissions using one of the [DocumentDB SDKs](documentdb-sdk-dotnet.md) or through the [REST APIs](https://msdn.microsoft.com/library/azure/dn781481.aspx).   

## <a name="database-questions-about-developing-against-microsoft-azure-documentdb"></a>Database questions about developing against Microsoft Azure DocumentDB
### <a name="how-to-do-i-start-developing-against-documentdb"></a>How to do I start developing against DocumentDB?
[SDKs](documentdb-sdk-dotnet.md) are available for .NET, Python, Node.js, JavaScript, and Java.  Developers can also use the [RESTful HTTP APIs](https://msdn.microsoft.com/library/azure/dn781481.aspx) to interact with DocumentDB resources from various platforms and languages.

Samples for the DocumentDB [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), and [Python](documentdb-python-samples.md) SDKs are available on GitHub.

### <a name="does-documentdb-support-sql"></a>Does DocumentDB support SQL?
The DocumentDB SQL query language is an enhanced subset of the query functionality supported by SQL. The DocumentDB SQL query language provides rich hierarchical and relational operators and extensibility via JavaScript based user-defined functions (UDFs). JSON grammar allows for modeling JSON documents as trees with labels as the tree nodes, which is used by both the DocumentDB automatic indexing techniques and the SQL query dialect of DocumentDB.  For details on how to use the SQL grammar, see the [Query DocumentDB][query] article.

### <a name="does-documentdb-support-sql-aggregation-functions"></a>Does DocumentDB support SQL aggregation functions?
DocumentDB supports low latency aggregation at any scale via aggregate functions `COUNT`, `MIN`, `MAX`, `AVG`, and `SUM` via the SQL grammar. For more information, see [Aggregate functions](documentdb-sql-query.md#Aggregates).

### <a name="what-are-the-data-types-supported-by-documentdb"></a>What are the data types supported by DocumentDB?
The primitive data types supported in DocumentDB are the same as JSON. JSON has a simple type system that consists of Strings, Numbers (IEEE754 double precision), and Booleans - true, false, and Nulls. DocumentDB natively supports spatial types Point, Polygon, and LineString expressed as GeoJSON. More complex data types like DateTime, Guid, Int64, and Geometry can be represented both in JSON and DocumentDB through the creation of nested objects using the { } operator and arrays using the [ ] operator.

### <a name="how-does-documentdb-provide-concurrency"></a>How does DocumentDB provide concurrency?
DocumentDB supports optimistic concurrency control (OCC) through HTTP entity tags or etags. Every DocumentDB resource has an etag, and the etag is set on the server every time a document is updated. The etag header and the current value are included in all response messages. Etags can be used with the If-Match header to allow the server to decide if a resource should be updated. The If-Match value is the etag value to be checked against. If the etag value matches the server etag value, the resource will be updated. If the etag is no longer current, the server rejects the operation with an "HTTP 412 Precondition failure" response code. The client will then have to refetch the resource to acquire the current etag value for the resource. In addition, etags can be used with If-None-Match header to determine if a re-fetch of a resource is needed.

To use optimistic concurrency in .NET, use the [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) class. For a .NET sample, see [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) in the DocumentManagement sample on github.

### <a name="how-do-i-perform-transactions-in-documentdb"></a>How do I perform transactions in DocumentDB?
DocumentDB supports language-integrated transactions via JavaScript stored procedures and triggers. All database operations inside scripts are executed under snapshot isolation scoped to the collection if it is a single-partition collection, or documents with the same partition key value within a collection, if the collection is partitioned. A snapshot of the document versions (ETags) is taken at the start of the transaction and committed only if the script succeeds. If the JavaScript throws an error, the transaction is rolled back. See [DocumentDB server-side programming](documentdb-programming.md) for more details.

### <a name="how-can-i-bulk-insert-documents-into-documentdb"></a>How can I bulk insert documents into DocumentDB?
There are three ways to bulk insert documents into DocumentDB:

* The data migration tool, as described in [Import data to DocumentDB](documentdb-import-data.md).
* Document Explorer in the Azure Portal, as described in [Bulk add documents with Document Explorer](documentdb-view-json-document-explorer.md#bulk-add-documents).
* Stored procedures, as described in [DocumentDB server-side programming](documentdb-programming.md).

### <a name="does-documentdb-support-resource-link-caching"></a>Does DocumentDB support resource link caching?
Yes, because DocumentDB is a RESTful service, resource links are immutable and can be cached. DocumentDB clients can specify an "If-None-Match" header for reads against any resource like document or collection and update their local copies only when the server version has change.

### <a name="is-a-local-instance-of-documentdb-available"></a>Is a local instance of DocumentDB available?
Yes. The [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) provides a high-fidelity emulation of the DocumentDB service. It supports identical functionality as Azure DocumentDB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers. You can develop and test applications using the DocumentDB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for DocumentDB.

## <a name="database-questions-about-developing-against-api-for-mongodb"></a>Database questions about developing against API for MongoDB
### <a name="what-is-documentdbs-api-for-mongodb"></a>What is DocumentDB's API for MongoDB?
Microsoft Azure DocumentDB's API for MongoDB is a compatability layer that allows applications to easily and transparently communicate with the native DocumentDB database engine using existing, community supported Apache MongoDB APIs and drivers. Developers can now use existing MongoDB tool chains and skills to build applications that leverage DocumentDB, benefitting from DocumentDB's unique capabilities, which include auto-indexing, backup maintenance, financially backed service level agreements (SLAs), etc.

### <a name="how-to-do-i-connect-to-my-api-for-mongodb-database"></a>How to do I connect to my API for MongoDB database?
The quickest way to connect to DocumentDB's API for MongoDB is to head over to the [Azure portal](https://portal.azure.com). Navigate your way to your account. In the account's *Left Navigation*, click on *Quick Start*. *Quick Start* is the best way to get code snippets to connect to your database. 

DocumentDB enforces strict security requirements and standards. DocumentDB accounts require authentication and secure communication via *SSL*, so make sure to use TLSv1.2.

For more details, see [Connect to your API for MongoDB database](documentdb-connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>Are there additional error codes for an API for MongoDB database?
API for MongoDB has its own specific error codes in addition to the common MongoDB error codes.


| Error               | Code  | Description  | Solution  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | The total number of request units consumed has exceeded the provisioned request unit rate for the collection and has been throttled. | Consider scaling the throughput of the collection from the Azure Portal or retrying again. |
| ExceededMemoryLimit | 16501 | As a multi-tenant service, the operation has exceeded the client's memory allotment. | Reduce the scope of the operation through a more restrictive query criteria or contact support from the [Azure portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>*Ex:  &nbsp;&nbsp;&nbsp;&nbsp;db.getCollection('users').aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
