---
title: Change feed for HL7 FHIR resources - Azure Cosmos DB | Microsoft Docs
description: Learn how to set up change notifications for HL7 FHIR patient health care records using Azure Logic Apps, Azure Cosmos DB, and Service Bus.
keywords: hl7 fhir
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 02/08/2017
ms.author: sngun
ms.openlocfilehash: 910e38f61cd0f8dc9633c4dca74fee8213234bf0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870706"
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="33e9e-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="33e9e-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="33e9e-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span><span class="sxs-lookup"><span data-stu-id="33e9e-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="33e9e-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span><span class="sxs-lookup"><span data-stu-id="33e9e-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="33e9e-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span><span class="sxs-lookup"><span data-stu-id="33e9e-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="33e9e-108">Project requirements</span><span class="sxs-lookup"><span data-stu-id="33e9e-108">Project requirements</span></span>
- <span data-ttu-id="33e9e-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span><span class="sxs-lookup"><span data-stu-id="33e9e-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="33e9e-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span><span class="sxs-lookup"><span data-stu-id="33e9e-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="33e9e-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span><span class="sxs-lookup"><span data-stu-id="33e9e-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="33e9e-112">Modified FHIR resource documents are sent by email in JSON format.</span><span class="sxs-lookup"><span data-stu-id="33e9e-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="33e9e-113">Solution workflow</span><span class="sxs-lookup"><span data-stu-id="33e9e-113">Solution workflow</span></span> 

<span data-ttu-id="33e9e-114">At a high level, the project required the following workflow steps:</span><span class="sxs-lookup"><span data-stu-id="33e9e-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="33e9e-115">Convert C-CDA documents to FHIR resources.</span><span class="sxs-lookup"><span data-stu-id="33e9e-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="33e9e-116">Perform recurring trigger polling for modified FHIR resources.</span><span class="sxs-lookup"><span data-stu-id="33e9e-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="33e9e-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span><span class="sxs-lookup"><span data-stu-id="33e9e-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="33e9e-118">Save the response to the Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="33e9e-118">Save the response to the Service Bus queue.</span></span>
4. <span data-ttu-id="33e9e-119">Poll for new messages in the Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="33e9e-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="33e9e-120">Send email notifications to patients.</span><span class="sxs-lookup"><span data-stu-id="33e9e-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="33e9e-121">Solution architecture</span><span class="sxs-lookup"><span data-stu-id="33e9e-121">Solution architecture</span></span>
<span data-ttu-id="33e9e-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span><span class="sxs-lookup"><span data-stu-id="33e9e-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="33e9e-123">The three logic apps are:</span><span class="sxs-lookup"><span data-stu-id="33e9e-123">The three logic apps are:</span></span>
1. <span data-ttu-id="33e9e-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="33e9e-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="33e9e-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="33e9e-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="33e9e-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span><span class="sxs-lookup"><span data-stu-id="33e9e-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="33e9e-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span><span class="sxs-lookup"><span data-stu-id="33e9e-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![The three Logic Apps used in this HL7 FHIR healthcare solution](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="33e9e-129">Azure services used in the solution</span><span class="sxs-lookup"><span data-stu-id="33e9e-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-sql-api"></a><span data-ttu-id="33e9e-130">Azure Cosmos DB SQL API</span><span class="sxs-lookup"><span data-stu-id="33e9e-130">Azure Cosmos DB SQL API</span></span>
<span data-ttu-id="33e9e-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="33e9e-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![The Azure Cosmos DB account used in this HL7 FHIR healthcare tutorial](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="33e9e-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="33e9e-133">Logic Apps</span></span>
<span data-ttu-id="33e9e-134">Logic Apps handle the workflow process.</span><span class="sxs-lookup"><span data-stu-id="33e9e-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="33e9e-135">The following screenshots show the Logic apps created for this solution.</span><span class="sxs-lookup"><span data-stu-id="33e9e-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="33e9e-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="33e9e-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="33e9e-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span><span class="sxs-lookup"><span data-stu-id="33e9e-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![The Logic App used to receive HL7 FHIR healthcare records](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="33e9e-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="33e9e-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="33e9e-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span><span class="sxs-lookup"><span data-stu-id="33e9e-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![The Logic App used to query Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="33e9e-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span><span class="sxs-lookup"><span data-stu-id="33e9e-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![The Logic App that sends patient email with the HL7 FHIR resource in the body](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="33e9e-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="33e9e-144">Service Bus</span></span>
<span data-ttu-id="33e9e-145">The following figure shows the patients queue.</span><span class="sxs-lookup"><span data-stu-id="33e9e-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="33e9e-146">The Tag property value is used for the email subject.</span><span class="sxs-lookup"><span data-stu-id="33e9e-146">The Tag property value is used for the email subject.</span></span>

![The Service Bus Queue used in this HL7 FHIR tutorial](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="33e9e-148">API app</span><span class="sxs-lookup"><span data-stu-id="33e9e-148">API app</span></span>
<span data-ttu-id="33e9e-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span><span class="sxs-lookup"><span data-stu-id="33e9e-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="33e9e-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="33e9e-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="33e9e-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB SQL .NET API.</span><span class="sxs-lookup"><span data-stu-id="33e9e-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB SQL .NET API.</span></span> <span data-ttu-id="33e9e-152">For more information, see the [change feed article](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="33e9e-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="33e9e-153">GetNewOrModifiedFhirDocuments operation</span><span class="sxs-lookup"><span data-stu-id="33e9e-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="33e9e-154">**Inputs**</span><span class="sxs-lookup"><span data-stu-id="33e9e-154">**Inputs**</span></span>
- <span data-ttu-id="33e9e-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="33e9e-155">DatabaseId</span></span>
- <span data-ttu-id="33e9e-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="33e9e-156">CollectionId</span></span>
- <span data-ttu-id="33e9e-157">HL7 FHIR Resource Type name</span><span class="sxs-lookup"><span data-stu-id="33e9e-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="33e9e-158">Boolean: Start from Beginning</span><span class="sxs-lookup"><span data-stu-id="33e9e-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="33e9e-159">Int: Number of documents returned</span><span class="sxs-lookup"><span data-stu-id="33e9e-159">Int: Number of documents returned</span></span>

<span data-ttu-id="33e9e-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="33e9e-160">**Outputs**</span></span>
- <span data-ttu-id="33e9e-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span><span class="sxs-lookup"><span data-stu-id="33e9e-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="33e9e-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span><span class="sxs-lookup"><span data-stu-id="33e9e-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="33e9e-163">**Source for the API app**</span><span class="sxs-lookup"><span data-stu-id="33e9e-163">**Source for the API app**</span></span>

```csharp

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="33e9e-164">Testing the FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="33e9e-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="33e9e-165">The following image demonstrates how swagger was used to test the [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="33e9e-165">The following image demonstrates how swagger was used to test the [FhirNotificationApi](#api-app-source).</span></span>

![The Swagger file used to test the API app](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="33e9e-167">Azure portal dashboard</span><span class="sxs-lookup"><span data-stu-id="33e9e-167">Azure portal dashboard</span></span>

<span data-ttu-id="33e9e-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33e9e-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![The Azure portal showing all the services used in this HL7 FHIR tutorial](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="33e9e-170">Summary</span><span class="sxs-lookup"><span data-stu-id="33e9e-170">Summary</span></span>

- <span data-ttu-id="33e9e-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span><span class="sxs-lookup"><span data-stu-id="33e9e-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="33e9e-172">By leveraging Logic Apps, you can create workflows without writing any code.</span><span class="sxs-lookup"><span data-stu-id="33e9e-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="33e9e-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span><span class="sxs-lookup"><span data-stu-id="33e9e-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33e9e-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="33e9e-174">Next steps</span></span>
<span data-ttu-id="33e9e-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="33e9e-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="33e9e-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="33e9e-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


