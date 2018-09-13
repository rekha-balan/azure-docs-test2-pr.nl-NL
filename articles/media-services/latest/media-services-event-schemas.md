---
title: Azure Event Grid schemas for Media Services events
description: Describes the properties that are provided for Media Services events with Azure Event Grid
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: reference
ms.date: 08/17/2018
ms.author: juliako
ms.openlocfilehash: a6a6c459e170627d26aa1445f4f4dd193965fe70
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871535"
---
# <a name="azure-event-grid-schemas-for-media-services-events"></a><span data-ttu-id="43d82-103">Azure Event Grid schemas for Media Services events</span><span class="sxs-lookup"><span data-stu-id="43d82-103">Azure Event Grid schemas for Media Services events</span></span>

<span data-ttu-id="43d82-104">This article provides the schemas and properties for Media Services events.</span><span class="sxs-lookup"><span data-stu-id="43d82-104">This article provides the schemas and properties for Media Services events.</span></span>

<span data-ttu-id="43d82-105">For a list of sample scripts and tutorials, see [Media Services event source](../../event-grid/event-sources.md#azure-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="43d82-105">For a list of sample scripts and tutorials, see [Media Services event source](../../event-grid/event-sources.md#azure-subscriptions).</span></span>

## <a name="available-event-types"></a><span data-ttu-id="43d82-106">Available event types</span><span class="sxs-lookup"><span data-stu-id="43d82-106">Available event types</span></span>

<span data-ttu-id="43d82-107">Media Services emits the following event types:</span><span class="sxs-lookup"><span data-stu-id="43d82-107">Media Services emits the following event types:</span></span>

| <span data-ttu-id="43d82-108">Event type</span><span class="sxs-lookup"><span data-stu-id="43d82-108">Event type</span></span> | <span data-ttu-id="43d82-109">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-109">Description</span></span> |
| ---------- | ----------- |
| <span data-ttu-id="43d82-110">Microsoft.Media.JobStateChange</span><span class="sxs-lookup"><span data-stu-id="43d82-110">Microsoft.Media.JobStateChange</span></span>| <span data-ttu-id="43d82-111">State of the Job changes.</span><span class="sxs-lookup"><span data-stu-id="43d82-111">State of the Job changes.</span></span> |
| <span data-ttu-id="43d82-112">Microsoft.Media.LiveEventConnectionRejected</span><span class="sxs-lookup"><span data-stu-id="43d82-112">Microsoft.Media.LiveEventConnectionRejected</span></span> | <span data-ttu-id="43d82-113">Encoder's connection attempt is rejected.</span><span class="sxs-lookup"><span data-stu-id="43d82-113">Encoder's connection attempt is rejected.</span></span> |
| <span data-ttu-id="43d82-114">Microsoft.Media.LiveEventEncoderConnected</span><span class="sxs-lookup"><span data-stu-id="43d82-114">Microsoft.Media.LiveEventEncoderConnected</span></span> | <span data-ttu-id="43d82-115">Encoder establishes connection with live event.</span><span class="sxs-lookup"><span data-stu-id="43d82-115">Encoder establishes connection with live event.</span></span> |
| <span data-ttu-id="43d82-116">Microsoft.Media.LiveEventEncoderDisconnected</span><span class="sxs-lookup"><span data-stu-id="43d82-116">Microsoft.Media.LiveEventEncoderDisconnected</span></span> | <span data-ttu-id="43d82-117">Encoder disconnects.</span><span class="sxs-lookup"><span data-stu-id="43d82-117">Encoder disconnects.</span></span> |
| <span data-ttu-id="43d82-118">Microsoft.Media.LiveEventIncomingDataChunkDropped</span><span class="sxs-lookup"><span data-stu-id="43d82-118">Microsoft.Media.LiveEventIncomingDataChunkDropped</span></span> | <span data-ttu-id="43d82-119">Media server drops data chunk because it's too late or has an overlapping timestamp (timestamp of new data chunk is less than the end time of the previous data chunk).</span><span class="sxs-lookup"><span data-stu-id="43d82-119">Media server drops data chunk because it's too late or has an overlapping timestamp (timestamp of new data chunk is less than the end time of the previous data chunk).</span></span> |
| <span data-ttu-id="43d82-120">Microsoft.Media.LiveEventIncomingStreamReceived</span><span class="sxs-lookup"><span data-stu-id="43d82-120">Microsoft.Media.LiveEventIncomingStreamReceived</span></span> | <span data-ttu-id="43d82-121">Media server receives first data chunk for each track in the stream or connection.</span><span class="sxs-lookup"><span data-stu-id="43d82-121">Media server receives first data chunk for each track in the stream or connection.</span></span> |
| <span data-ttu-id="43d82-122">Microsoft.Media.LiveEventIncomingStreamsOutOfSync</span><span class="sxs-lookup"><span data-stu-id="43d82-122">Microsoft.Media.LiveEventIncomingStreamsOutOfSync</span></span> | <span data-ttu-id="43d82-123">Media server detects audio and video streams are out of sync. Use as a warning because user experience may not be impacted.</span><span class="sxs-lookup"><span data-stu-id="43d82-123">Media server detects audio and video streams are out of sync. Use as a warning because user experience may not be impacted.</span></span> |
| <span data-ttu-id="43d82-124">Microsoft.Media.LiveEventIncomingVideoStreamsOutOfSync</span><span class="sxs-lookup"><span data-stu-id="43d82-124">Microsoft.Media.LiveEventIncomingVideoStreamsOutOfSync</span></span> | <span data-ttu-id="43d82-125">Media server detects any of the two video streams coming from external encoder are out of sync. Use as a warning because user experience may not be impacted.</span><span class="sxs-lookup"><span data-stu-id="43d82-125">Media server detects any of the two video streams coming from external encoder are out of sync. Use as a warning because user experience may not be impacted.</span></span> |
| <span data-ttu-id="43d82-126">Microsoft.Media.LiveEventIngestHeartbeat</span><span class="sxs-lookup"><span data-stu-id="43d82-126">Microsoft.Media.LiveEventIngestHeartbeat</span></span> | <span data-ttu-id="43d82-127">Published every 20 seconds for each track when live event is running.</span><span class="sxs-lookup"><span data-stu-id="43d82-127">Published every 20 seconds for each track when live event is running.</span></span> <span data-ttu-id="43d82-128">Provides ingest health summary.</span><span class="sxs-lookup"><span data-stu-id="43d82-128">Provides ingest health summary.</span></span> |
| <span data-ttu-id="43d82-129">Microsoft.Media.LiveEventTrackDiscontinuityDetected</span><span class="sxs-lookup"><span data-stu-id="43d82-129">Microsoft.Media.LiveEventTrackDiscontinuityDetected</span></span> | <span data-ttu-id="43d82-130">Media server detects discontinuity in the incoming track.</span><span class="sxs-lookup"><span data-stu-id="43d82-130">Media server detects discontinuity in the incoming track.</span></span> |

<span data-ttu-id="43d82-131">There are two categories for the **Live** events: stream-level events and track-level events.</span><span class="sxs-lookup"><span data-stu-id="43d82-131">There are two categories for the **Live** events: stream-level events and track-level events.</span></span> 

<span data-ttu-id="43d82-132">Stream-level events are raised per stream or connection.</span><span class="sxs-lookup"><span data-stu-id="43d82-132">Stream-level events are raised per stream or connection.</span></span> <span data-ttu-id="43d82-133">Each event has a `StreamId` parameter that identifies the connection or stream.</span><span class="sxs-lookup"><span data-stu-id="43d82-133">Each event has a `StreamId` parameter that identifies the connection or stream.</span></span> <span data-ttu-id="43d82-134">Each stream or connection has one or more tracks of different types.</span><span class="sxs-lookup"><span data-stu-id="43d82-134">Each stream or connection has one or more tracks of different types.</span></span> <span data-ttu-id="43d82-135">For example, one connection from an encoder may have one audio track and four video tracks.</span><span class="sxs-lookup"><span data-stu-id="43d82-135">For example, one connection from an encoder may have one audio track and four video tracks.</span></span> <span data-ttu-id="43d82-136">The stream event types are:</span><span class="sxs-lookup"><span data-stu-id="43d82-136">The stream event types are:</span></span>

* <span data-ttu-id="43d82-137">LiveEventConnectionRejected</span><span class="sxs-lookup"><span data-stu-id="43d82-137">LiveEventConnectionRejected</span></span>
* <span data-ttu-id="43d82-138">LiveEventEncoderConnected</span><span class="sxs-lookup"><span data-stu-id="43d82-138">LiveEventEncoderConnected</span></span>
* <span data-ttu-id="43d82-139">LiveEventEncoderDisconnected</span><span class="sxs-lookup"><span data-stu-id="43d82-139">LiveEventEncoderDisconnected</span></span>

<span data-ttu-id="43d82-140">Track-level events are raised per track. The track event types are:</span><span class="sxs-lookup"><span data-stu-id="43d82-140">Track-level events are raised per track. The track event types are:</span></span>

* <span data-ttu-id="43d82-141">LiveEventIncomingDataChunkDropped</span><span class="sxs-lookup"><span data-stu-id="43d82-141">LiveEventIncomingDataChunkDropped</span></span>
* <span data-ttu-id="43d82-142">LiveEventIncomingStreamReceived</span><span class="sxs-lookup"><span data-stu-id="43d82-142">LiveEventIncomingStreamReceived</span></span>
* <span data-ttu-id="43d82-143">LiveEventIncomingStreamsOutOfSync</span><span class="sxs-lookup"><span data-stu-id="43d82-143">LiveEventIncomingStreamsOutOfSync</span></span>
* <span data-ttu-id="43d82-144">LiveEventIncomingVideoStreamsOutOfSync</span><span class="sxs-lookup"><span data-stu-id="43d82-144">LiveEventIncomingVideoStreamsOutOfSync</span></span>
* <span data-ttu-id="43d82-145">LiveEventIngestHeartbeat</span><span class="sxs-lookup"><span data-stu-id="43d82-145">LiveEventIngestHeartbeat</span></span>
* <span data-ttu-id="43d82-146">LiveEventTrackDiscontinuityDetected</span><span class="sxs-lookup"><span data-stu-id="43d82-146">LiveEventTrackDiscontinuityDetected</span></span>

## <a name="jobstatechange"></a><span data-ttu-id="43d82-147">JobStateChange</span><span class="sxs-lookup"><span data-stu-id="43d82-147">JobStateChange</span></span>

<span data-ttu-id="43d82-148">The following example shows the schema of the **JobStateChange** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-148">The following example shows the schema of the **JobStateChange** event:</span></span> 

```json
[
  {
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaservices/<account-name>",
    "subject": "transforms/VideoAnalyzerTransform/jobs/<job-id>",
    "eventType": "Microsoft.Media.JobStateChange",
    "eventTime": "2018-04-20T21:26:13.8978772",
    "id": "b9d38923-9210-4c2b-958f-0054467d4dd7",
    "data": {
      "previousState": "Processing",
      "state": "Finished"
    },
    "dataVersion": "1.0",
    "metadataVersion": "1"
  }
]
```

<span data-ttu-id="43d82-149">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-149">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-150">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-150">Property</span></span> | <span data-ttu-id="43d82-151">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-151">Type</span></span> | <span data-ttu-id="43d82-152">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-152">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-153">previousState</span><span class="sxs-lookup"><span data-stu-id="43d82-153">previousState</span></span> | <span data-ttu-id="43d82-154">string</span><span class="sxs-lookup"><span data-stu-id="43d82-154">string</span></span> | <span data-ttu-id="43d82-155">The state of the job before the event.</span><span class="sxs-lookup"><span data-stu-id="43d82-155">The state of the job before the event.</span></span> |
| <span data-ttu-id="43d82-156">state</span><span class="sxs-lookup"><span data-stu-id="43d82-156">state</span></span> | <span data-ttu-id="43d82-157">string</span><span class="sxs-lookup"><span data-stu-id="43d82-157">string</span></span> | <span data-ttu-id="43d82-158">The new state of the job being notified in this event.</span><span class="sxs-lookup"><span data-stu-id="43d82-158">The new state of the job being notified in this event.</span></span> <span data-ttu-id="43d82-159">For example, "Queued: The Job is awaiting resources" or "Scheduled: The job is ready to start".</span><span class="sxs-lookup"><span data-stu-id="43d82-159">For example, "Queued: The Job is awaiting resources" or "Scheduled: The job is ready to start".</span></span>|

<span data-ttu-id="43d82-160">Where the Job state can be one of the values: *Queued*, *Scheduled*, *Processing*, *Finished*, *Error*, *Canceled*, *Canceling*</span><span class="sxs-lookup"><span data-stu-id="43d82-160">Where the Job state can be one of the values: *Queued*, *Scheduled*, *Processing*, *Finished*, *Error*, *Canceled*, *Canceling*</span></span>

## <a name="liveeventconnectionrejected"></a><span data-ttu-id="43d82-161">LiveEventConnectionRejected</span><span class="sxs-lookup"><span data-stu-id="43d82-161">LiveEventConnectionRejected</span></span>

<span data-ttu-id="43d82-162">The following example shows the schema of the **LiveEventConnectionRejected** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-162">The following example shows the schema of the **LiveEventConnectionRejected** event:</span></span> 

```json
[
  {
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaServices/<account-name>",
    "subject": "/LiveEvents/MyLiveEvent1",
    "eventType": "Microsoft.Media.LiveEventConnectionRejected",
    "eventTime": "2018-01-16T01:57:26.005121Z",
    "id": "b303db59-d5c1-47eb-927a-3650875fded1",
    "data": { 
      "StreamId":"Mystream1",
      "IngestUrl": "http://abc.ingest.isml",
      "EncoderIp": "118.238.251.xxx",
      "EncoderPort": 52859,
      "ResultCode": "MPE_INGEST_CODEC_NOT_SUPPORTED"
    },
    "dataVersion": "1.0"
  }
]
```

<span data-ttu-id="43d82-163">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-163">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-164">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-164">Property</span></span> | <span data-ttu-id="43d82-165">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-165">Type</span></span> | <span data-ttu-id="43d82-166">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-166">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-167">StreamId</span><span class="sxs-lookup"><span data-stu-id="43d82-167">StreamId</span></span> | <span data-ttu-id="43d82-168">string</span><span class="sxs-lookup"><span data-stu-id="43d82-168">string</span></span> | <span data-ttu-id="43d82-169">Identifier of the stream or connection.</span><span class="sxs-lookup"><span data-stu-id="43d82-169">Identifier of the stream or connection.</span></span> <span data-ttu-id="43d82-170">Encoder or customer is responsible to add this ID in the ingest URL.</span><span class="sxs-lookup"><span data-stu-id="43d82-170">Encoder or customer is responsible to add this ID in the ingest URL.</span></span> |  
| <span data-ttu-id="43d82-171">IngestUrl</span><span class="sxs-lookup"><span data-stu-id="43d82-171">IngestUrl</span></span> | <span data-ttu-id="43d82-172">string</span><span class="sxs-lookup"><span data-stu-id="43d82-172">string</span></span> | <span data-ttu-id="43d82-173">Ingest URL provided by the live event.</span><span class="sxs-lookup"><span data-stu-id="43d82-173">Ingest URL provided by the live event.</span></span> |  
| <span data-ttu-id="43d82-174">EncoderIp</span><span class="sxs-lookup"><span data-stu-id="43d82-174">EncoderIp</span></span> | <span data-ttu-id="43d82-175">string</span><span class="sxs-lookup"><span data-stu-id="43d82-175">string</span></span> | <span data-ttu-id="43d82-176">IP of the encoder.</span><span class="sxs-lookup"><span data-stu-id="43d82-176">IP of the encoder.</span></span> |
| <span data-ttu-id="43d82-177">EncoderPort</span><span class="sxs-lookup"><span data-stu-id="43d82-177">EncoderPort</span></span> | <span data-ttu-id="43d82-178">string</span><span class="sxs-lookup"><span data-stu-id="43d82-178">string</span></span> | <span data-ttu-id="43d82-179">Port of the encoder from where this stream is coming.</span><span class="sxs-lookup"><span data-stu-id="43d82-179">Port of the encoder from where this stream is coming.</span></span> |
| <span data-ttu-id="43d82-180">ResultCode</span><span class="sxs-lookup"><span data-stu-id="43d82-180">ResultCode</span></span> | <span data-ttu-id="43d82-181">string</span><span class="sxs-lookup"><span data-stu-id="43d82-181">string</span></span> | <span data-ttu-id="43d82-182">The reason the connection was rejected.</span><span class="sxs-lookup"><span data-stu-id="43d82-182">The reason the connection was rejected.</span></span> <span data-ttu-id="43d82-183">The result codes are listed in the following table.</span><span class="sxs-lookup"><span data-stu-id="43d82-183">The result codes are listed in the following table.</span></span> |

<span data-ttu-id="43d82-184">The result codes are:</span><span class="sxs-lookup"><span data-stu-id="43d82-184">The result codes are:</span></span>

| <span data-ttu-id="43d82-185">Result code</span><span class="sxs-lookup"><span data-stu-id="43d82-185">Result code</span></span> | <span data-ttu-id="43d82-186">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-186">Description</span></span> |
| ----------- | ----------- |
| <span data-ttu-id="43d82-187">MPE_RTMP_APPID_AUTH_FAILURE</span><span class="sxs-lookup"><span data-stu-id="43d82-187">MPE_RTMP_APPID_AUTH_FAILURE</span></span> | <span data-ttu-id="43d82-188">Incorrect ingest URL</span><span class="sxs-lookup"><span data-stu-id="43d82-188">Incorrect ingest URL</span></span> |
| <span data-ttu-id="43d82-189">MPE_INGEST_ENCODER_CONNECTION_DENIED</span><span class="sxs-lookup"><span data-stu-id="43d82-189">MPE_INGEST_ENCODER_CONNECTION_DENIED</span></span> | <span data-ttu-id="43d82-190">Encoder IP isn't present in IP allow list configured</span><span class="sxs-lookup"><span data-stu-id="43d82-190">Encoder IP isn't present in IP allow list configured</span></span> |
| <span data-ttu-id="43d82-191">MPE_INGEST_RTMP_SETDATAFRAME_NOT_RECEIVED</span><span class="sxs-lookup"><span data-stu-id="43d82-191">MPE_INGEST_RTMP_SETDATAFRAME_NOT_RECEIVED</span></span> | <span data-ttu-id="43d82-192">Encoder didn't send metadata about the stream.</span><span class="sxs-lookup"><span data-stu-id="43d82-192">Encoder didn't send metadata about the stream.</span></span> |
| <span data-ttu-id="43d82-193">MPE_INGEST_CODEC_NOT_SUPPORTED</span><span class="sxs-lookup"><span data-stu-id="43d82-193">MPE_INGEST_CODEC_NOT_SUPPORTED</span></span> | <span data-ttu-id="43d82-194">Codec specified isn't supported.</span><span class="sxs-lookup"><span data-stu-id="43d82-194">Codec specified isn't supported.</span></span> |
| <span data-ttu-id="43d82-195">MPE_INGEST_DESCRIPTION_INFO_NOT_RECEIVED</span><span class="sxs-lookup"><span data-stu-id="43d82-195">MPE_INGEST_DESCRIPTION_INFO_NOT_RECEIVED</span></span> | <span data-ttu-id="43d82-196">Received a fragment before receiving and header for that stream.</span><span class="sxs-lookup"><span data-stu-id="43d82-196">Received a fragment before receiving and header for that stream.</span></span> |
| <span data-ttu-id="43d82-197">MPE_INGEST_MEDIA_QUALITIES_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="43d82-197">MPE_INGEST_MEDIA_QUALITIES_EXCEEDED</span></span> | <span data-ttu-id="43d82-198">Number of qualities specified exceeds allowed max limit.</span><span class="sxs-lookup"><span data-stu-id="43d82-198">Number of qualities specified exceeds allowed max limit.</span></span> |
| <span data-ttu-id="43d82-199">MPE_INGEST_BITRATE_AGGREGATED_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="43d82-199">MPE_INGEST_BITRATE_AGGREGATED_EXCEEDED</span></span> | <span data-ttu-id="43d82-200">Aggregated bitrate exceeds max allowed limit.</span><span class="sxs-lookup"><span data-stu-id="43d82-200">Aggregated bitrate exceeds max allowed limit.</span></span> |
| <span data-ttu-id="43d82-201">MPE_RTMP_FLV_TAG_TIMESTAMP_INVALID</span><span class="sxs-lookup"><span data-stu-id="43d82-201">MPE_RTMP_FLV_TAG_TIMESTAMP_INVALID</span></span> | <span data-ttu-id="43d82-202">The timestamp for video or audio FLVTag is invalid from RTMP encoder.</span><span class="sxs-lookup"><span data-stu-id="43d82-202">The timestamp for video or audio FLVTag is invalid from RTMP encoder.</span></span> |

## <a name="liveeventencoderconnected"></a><span data-ttu-id="43d82-203">LiveEventEncoderConnected</span><span class="sxs-lookup"><span data-stu-id="43d82-203">LiveEventEncoderConnected</span></span>

<span data-ttu-id="43d82-204">The following example shows the schema of the **LiveEventEncoderConnected** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-204">The following example shows the schema of the **LiveEventEncoderConnected** event:</span></span> 

```json
[
  { 
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaservices/<account-name>",
    "subject": "liveEvent/mle1",
    "eventType": "Microsoft.Media.LiveEventEncoderConnected",
    "eventTime": "2018-08-07T23:08:09.1710643",
    "id": "<id>",
    "data": {
      "ingestUrl": "http://mle1-amsts03mediaacctgndos-ts031.channel.media.azure-test.net:80/ingest.isml",
      "streamId": "15864-stream0",
      "encoderIp": "131.107.147.xxx",
      "encoderPort": "27485"
    },
    "dataVersion": "1.0",
    "metadataVersion": "1"
  }
]
```

<span data-ttu-id="43d82-205">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-205">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-206">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-206">Property</span></span> | <span data-ttu-id="43d82-207">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-207">Type</span></span> | <span data-ttu-id="43d82-208">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-208">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-209">StreamId</span><span class="sxs-lookup"><span data-stu-id="43d82-209">StreamId</span></span> | <span data-ttu-id="43d82-210">string</span><span class="sxs-lookup"><span data-stu-id="43d82-210">string</span></span> | <span data-ttu-id="43d82-211">Identifier of the stream or connection.</span><span class="sxs-lookup"><span data-stu-id="43d82-211">Identifier of the stream or connection.</span></span> <span data-ttu-id="43d82-212">Encoder or customer is responsible for providing this ID in the ingest URL.</span><span class="sxs-lookup"><span data-stu-id="43d82-212">Encoder or customer is responsible for providing this ID in the ingest URL.</span></span> |
| <span data-ttu-id="43d82-213">IngestUrl</span><span class="sxs-lookup"><span data-stu-id="43d82-213">IngestUrl</span></span> | <span data-ttu-id="43d82-214">string</span><span class="sxs-lookup"><span data-stu-id="43d82-214">string</span></span> | <span data-ttu-id="43d82-215">Ingest URL provided by the live event.</span><span class="sxs-lookup"><span data-stu-id="43d82-215">Ingest URL provided by the live event.</span></span> |
| <span data-ttu-id="43d82-216">EncoderIp</span><span class="sxs-lookup"><span data-stu-id="43d82-216">EncoderIp</span></span> | <span data-ttu-id="43d82-217">string</span><span class="sxs-lookup"><span data-stu-id="43d82-217">string</span></span> | <span data-ttu-id="43d82-218">IP of the encoder.</span><span class="sxs-lookup"><span data-stu-id="43d82-218">IP of the encoder.</span></span> |
| <span data-ttu-id="43d82-219">EncoderPort</span><span class="sxs-lookup"><span data-stu-id="43d82-219">EncoderPort</span></span> | <span data-ttu-id="43d82-220">string</span><span class="sxs-lookup"><span data-stu-id="43d82-220">string</span></span> | <span data-ttu-id="43d82-221">Port of the encoder from where this stream is coming.</span><span class="sxs-lookup"><span data-stu-id="43d82-221">Port of the encoder from where this stream is coming.</span></span> |

## <a name="liveeventencoderdisconnected"></a><span data-ttu-id="43d82-222">LiveEventEncoderDisconnected</span><span class="sxs-lookup"><span data-stu-id="43d82-222">LiveEventEncoderDisconnected</span></span>

<span data-ttu-id="43d82-223">The following example shows the schema of the **LiveEventEncoderDisconnected** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-223">The following example shows the schema of the **LiveEventEncoderDisconnected** event:</span></span> 

```json
[
  { 
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaservices/<account-name>",
    "subject": "liveEvent/mle1",
    "eventType": "Microsoft.Media.LiveEventEncoderDisconnected",
    "eventTime": "2018-08-07T23:08:09.1710872",
    "id": "<id>",
    "data": {
      "ingestUrl": "http://mle1-amsts03mediaacctgndos-ts031.channel.media.azure-test.net:80/ingest.isml",
      "streamId": "15864-stream0",
      "encoderIp": "131.107.147.xxx",
      "encoderPort": "27485",
      "resultCode": "S_OK"
    },
    "dataVersion": "1.0",
    "metadataVersion": "1"
  }
]
```

<span data-ttu-id="43d82-224">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-224">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-225">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-225">Property</span></span> | <span data-ttu-id="43d82-226">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-226">Type</span></span> | <span data-ttu-id="43d82-227">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-227">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-228">StreamId</span><span class="sxs-lookup"><span data-stu-id="43d82-228">StreamId</span></span> | <span data-ttu-id="43d82-229">string</span><span class="sxs-lookup"><span data-stu-id="43d82-229">string</span></span> | <span data-ttu-id="43d82-230">Identifier of the stream or connection.</span><span class="sxs-lookup"><span data-stu-id="43d82-230">Identifier of the stream or connection.</span></span> <span data-ttu-id="43d82-231">Encoder or customer is responsible to add this ID in the ingest URL.</span><span class="sxs-lookup"><span data-stu-id="43d82-231">Encoder or customer is responsible to add this ID in the ingest URL.</span></span> |  
| <span data-ttu-id="43d82-232">IngestUrl</span><span class="sxs-lookup"><span data-stu-id="43d82-232">IngestUrl</span></span> | <span data-ttu-id="43d82-233">string</span><span class="sxs-lookup"><span data-stu-id="43d82-233">string</span></span> | <span data-ttu-id="43d82-234">Ingest URL provided by the live event.</span><span class="sxs-lookup"><span data-stu-id="43d82-234">Ingest URL provided by the live event.</span></span> |  
| <span data-ttu-id="43d82-235">EncoderIp</span><span class="sxs-lookup"><span data-stu-id="43d82-235">EncoderIp</span></span> | <span data-ttu-id="43d82-236">string</span><span class="sxs-lookup"><span data-stu-id="43d82-236">string</span></span> | <span data-ttu-id="43d82-237">IP of the encoder.</span><span class="sxs-lookup"><span data-stu-id="43d82-237">IP of the encoder.</span></span> |
| <span data-ttu-id="43d82-238">EncoderPort</span><span class="sxs-lookup"><span data-stu-id="43d82-238">EncoderPort</span></span> | <span data-ttu-id="43d82-239">string</span><span class="sxs-lookup"><span data-stu-id="43d82-239">string</span></span> | <span data-ttu-id="43d82-240">Port of the encoder from where this stream is coming.</span><span class="sxs-lookup"><span data-stu-id="43d82-240">Port of the encoder from where this stream is coming.</span></span> |
| <span data-ttu-id="43d82-241">ResultCode</span><span class="sxs-lookup"><span data-stu-id="43d82-241">ResultCode</span></span> | <span data-ttu-id="43d82-242">string</span><span class="sxs-lookup"><span data-stu-id="43d82-242">string</span></span> | <span data-ttu-id="43d82-243">The reason for the encoder disconnecting.</span><span class="sxs-lookup"><span data-stu-id="43d82-243">The reason for the encoder disconnecting.</span></span> <span data-ttu-id="43d82-244">It could be graceful disconnect or from an error.</span><span class="sxs-lookup"><span data-stu-id="43d82-244">It could be graceful disconnect or from an error.</span></span> <span data-ttu-id="43d82-245">The result codes are listed in the following table.</span><span class="sxs-lookup"><span data-stu-id="43d82-245">The result codes are listed in the following table.</span></span> |

<span data-ttu-id="43d82-246">The error result codes are:</span><span class="sxs-lookup"><span data-stu-id="43d82-246">The error result codes are:</span></span>

| <span data-ttu-id="43d82-247">Result code</span><span class="sxs-lookup"><span data-stu-id="43d82-247">Result code</span></span> | <span data-ttu-id="43d82-248">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-248">Description</span></span> |
| ----------- | ----------- |
| <span data-ttu-id="43d82-249">MPE_RTMP_SESSION_IDLE_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="43d82-249">MPE_RTMP_SESSION_IDLE_TIMEOUT</span></span> | <span data-ttu-id="43d82-250">RTMP session timed out after being idle for allowed time limit.</span><span class="sxs-lookup"><span data-stu-id="43d82-250">RTMP session timed out after being idle for allowed time limit.</span></span> |
| <span data-ttu-id="43d82-251">MPE_RTMP_FLV_TAG_TIMESTAMP_INVALID</span><span class="sxs-lookup"><span data-stu-id="43d82-251">MPE_RTMP_FLV_TAG_TIMESTAMP_INVALID</span></span> | <span data-ttu-id="43d82-252">The timestamp for video or audio FLVTag is invalid from RTMP encoder.</span><span class="sxs-lookup"><span data-stu-id="43d82-252">The timestamp for video or audio FLVTag is invalid from RTMP encoder.</span></span> |
| <span data-ttu-id="43d82-253">MPE_CAPACITY_LIMIT_REACHED</span><span class="sxs-lookup"><span data-stu-id="43d82-253">MPE_CAPACITY_LIMIT_REACHED</span></span> | <span data-ttu-id="43d82-254">Encoder sending data too fast.</span><span class="sxs-lookup"><span data-stu-id="43d82-254">Encoder sending data too fast.</span></span> |
| <span data-ttu-id="43d82-255">Unknown Error Codes</span><span class="sxs-lookup"><span data-stu-id="43d82-255">Unknown Error Codes</span></span> | <span data-ttu-id="43d82-256">These error codes can range from memory error to duplicate entries in hash map.</span><span class="sxs-lookup"><span data-stu-id="43d82-256">These error codes can range from memory error to duplicate entries in hash map.</span></span> |

<span data-ttu-id="43d82-257">The graceful disconnect result codes are:</span><span class="sxs-lookup"><span data-stu-id="43d82-257">The graceful disconnect result codes are:</span></span>

| <span data-ttu-id="43d82-258">Result code</span><span class="sxs-lookup"><span data-stu-id="43d82-258">Result code</span></span> | <span data-ttu-id="43d82-259">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-259">Description</span></span> |
| ----------- | ----------- |
| <span data-ttu-id="43d82-260">S_OK</span><span class="sxs-lookup"><span data-stu-id="43d82-260">S_OK</span></span> | <span data-ttu-id="43d82-261">Encoder disconnected successfully.</span><span class="sxs-lookup"><span data-stu-id="43d82-261">Encoder disconnected successfully.</span></span> |
| <span data-ttu-id="43d82-262">MPE_CLIENT_TERMINATED_SESSION</span><span class="sxs-lookup"><span data-stu-id="43d82-262">MPE_CLIENT_TERMINATED_SESSION</span></span> | <span data-ttu-id="43d82-263">Encoder disconnected (RTMP).</span><span class="sxs-lookup"><span data-stu-id="43d82-263">Encoder disconnected (RTMP).</span></span> |
| <span data-ttu-id="43d82-264">MPE_CLIENT_DISCONNECTED</span><span class="sxs-lookup"><span data-stu-id="43d82-264">MPE_CLIENT_DISCONNECTED</span></span> | <span data-ttu-id="43d82-265">Encoder disconnected (FMP4).</span><span class="sxs-lookup"><span data-stu-id="43d82-265">Encoder disconnected (FMP4).</span></span> |
| <span data-ttu-id="43d82-266">MPI_REST_API_CHANNEL_RESET</span><span class="sxs-lookup"><span data-stu-id="43d82-266">MPI_REST_API_CHANNEL_RESET</span></span> | <span data-ttu-id="43d82-267">Channel reset command is received.</span><span class="sxs-lookup"><span data-stu-id="43d82-267">Channel reset command is received.</span></span> |
| <span data-ttu-id="43d82-268">MPI_REST_API_CHANNEL_STOP</span><span class="sxs-lookup"><span data-stu-id="43d82-268">MPI_REST_API_CHANNEL_STOP</span></span> | <span data-ttu-id="43d82-269">Channel stop command received.</span><span class="sxs-lookup"><span data-stu-id="43d82-269">Channel stop command received.</span></span> |
| <span data-ttu-id="43d82-270">MPI_REST_API_CHANNEL_STOP</span><span class="sxs-lookup"><span data-stu-id="43d82-270">MPI_REST_API_CHANNEL_STOP</span></span> | <span data-ttu-id="43d82-271">Channel undergoing maintenance.</span><span class="sxs-lookup"><span data-stu-id="43d82-271">Channel undergoing maintenance.</span></span> |
| <span data-ttu-id="43d82-272">MPI_STREAM_HIT_EOF</span><span class="sxs-lookup"><span data-stu-id="43d82-272">MPI_STREAM_HIT_EOF</span></span> | <span data-ttu-id="43d82-273">EOF stream is sent by the encoder.</span><span class="sxs-lookup"><span data-stu-id="43d82-273">EOF stream is sent by the encoder.</span></span> |

## <a name="liveeventincomingdatachunkdropped"></a><span data-ttu-id="43d82-274">LiveEventIncomingDataChunkDropped</span><span class="sxs-lookup"><span data-stu-id="43d82-274">LiveEventIncomingDataChunkDropped</span></span>

<span data-ttu-id="43d82-275">The following example shows the schema of the **LiveEventIncomingDataChunkDropped** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-275">The following example shows the schema of the **LiveEventIncomingDataChunkDropped** event:</span></span> 

```json
[
  {
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaServices/<account-name>",
    "subject": "/LiveEvents/MyLiveEvent1",
    "eventType": "Microsoft.Media.LiveEventIncomingDataChunkDropped",
    "eventTime": "2018-01-16T01:57:26.005121Z",
    "id": "03da9c10-fde7-48e1-80d8-49936f2c3e7d",
    "data": { 
      "TrackType": "Video",
      "TrackName": "Video",
      "Bitrate": 300000,
      "Timestamp": 36656620000,
      "Timescale": 10000000,
      "ResultCode": "FragmentDrop_OverlapTimestamp"
    },
    "dataVersion": "1.0"
  }
]
```

<span data-ttu-id="43d82-276">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-276">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-277">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-277">Property</span></span> | <span data-ttu-id="43d82-278">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-278">Type</span></span> | <span data-ttu-id="43d82-279">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-279">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-280">TrackType</span><span class="sxs-lookup"><span data-stu-id="43d82-280">TrackType</span></span> | <span data-ttu-id="43d82-281">string</span><span class="sxs-lookup"><span data-stu-id="43d82-281">string</span></span> | <span data-ttu-id="43d82-282">Type of the track (Audio / Video).</span><span class="sxs-lookup"><span data-stu-id="43d82-282">Type of the track (Audio / Video).</span></span> |
| <span data-ttu-id="43d82-283">TrackName</span><span class="sxs-lookup"><span data-stu-id="43d82-283">TrackName</span></span> | <span data-ttu-id="43d82-284">string</span><span class="sxs-lookup"><span data-stu-id="43d82-284">string</span></span> | <span data-ttu-id="43d82-285">Name of the track.</span><span class="sxs-lookup"><span data-stu-id="43d82-285">Name of the track.</span></span> |
| <span data-ttu-id="43d82-286">Bitrate</span><span class="sxs-lookup"><span data-stu-id="43d82-286">Bitrate</span></span> | <span data-ttu-id="43d82-287">integer</span><span class="sxs-lookup"><span data-stu-id="43d82-287">integer</span></span> | <span data-ttu-id="43d82-288">Bitrate of the track.</span><span class="sxs-lookup"><span data-stu-id="43d82-288">Bitrate of the track.</span></span> |
| <span data-ttu-id="43d82-289">Timestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-289">Timestamp</span></span> | <span data-ttu-id="43d82-290">string</span><span class="sxs-lookup"><span data-stu-id="43d82-290">string</span></span> | <span data-ttu-id="43d82-291">Timestamp of the data chunk dropped.</span><span class="sxs-lookup"><span data-stu-id="43d82-291">Timestamp of the data chunk dropped.</span></span> |
| <span data-ttu-id="43d82-292">Timescale</span><span class="sxs-lookup"><span data-stu-id="43d82-292">Timescale</span></span> | <span data-ttu-id="43d82-293">string</span><span class="sxs-lookup"><span data-stu-id="43d82-293">string</span></span> | <span data-ttu-id="43d82-294">Timescale of the timestamp.</span><span class="sxs-lookup"><span data-stu-id="43d82-294">Timescale of the timestamp.</span></span> |
| <span data-ttu-id="43d82-295">ResultCode</span><span class="sxs-lookup"><span data-stu-id="43d82-295">ResultCode</span></span> | <span data-ttu-id="43d82-296">string</span><span class="sxs-lookup"><span data-stu-id="43d82-296">string</span></span> | <span data-ttu-id="43d82-297">Reason of the data chunk drop.</span><span class="sxs-lookup"><span data-stu-id="43d82-297">Reason of the data chunk drop.</span></span> <span data-ttu-id="43d82-298">**FragmentDrop_OverlapTimestamp** or **FragmentDrop_NonIncreasingTimestamp**.</span><span class="sxs-lookup"><span data-stu-id="43d82-298">**FragmentDrop_OverlapTimestamp** or **FragmentDrop_NonIncreasingTimestamp**.</span></span> |

## <a name="liveeventincomingstreamreceived"></a><span data-ttu-id="43d82-299">LiveEventIncomingStreamReceived</span><span class="sxs-lookup"><span data-stu-id="43d82-299">LiveEventIncomingStreamReceived</span></span>

<span data-ttu-id="43d82-300">The following example shows the schema of the **LiveEventIncomingStreamReceived** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-300">The following example shows the schema of the **LiveEventIncomingStreamReceived** event:</span></span> 

```json
[
  {
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaservices/<account-name>",
    "subject": "liveEvent/mle1",
    "eventType": "Microsoft.Media.LiveEventIncomingStreamReceived",
    "eventTime": "2018-08-07T23:08:10.5069288Z",
    "id": "7f939a08-320c-47e7-8250-43dcfc04ab4d",
    "data": {
      "ingestUrl": "http://mle1-amsts03mediaacctgndos-ts031.channel.media.azure-test.net:80/ingest.isml/Streams(15864-stream0)15864-stream0",
      "trackType": "video",
      "trackName": "video",
      "bitrate": 2962000,
      "encoderIp": "131.107.147.xxx",
      "encoderPort": "27485",
      "timestamp": "15336831655032322",
      "duration": "20000000",
      "timescale": "10000000"
    },
    "dataVersion": "1.0",
    "metadataVersion": "1"
  }
]
```

<span data-ttu-id="43d82-301">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-301">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-302">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-302">Property</span></span> | <span data-ttu-id="43d82-303">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-303">Type</span></span> | <span data-ttu-id="43d82-304">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-304">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-305">TrackType</span><span class="sxs-lookup"><span data-stu-id="43d82-305">TrackType</span></span> | <span data-ttu-id="43d82-306">string</span><span class="sxs-lookup"><span data-stu-id="43d82-306">string</span></span> | <span data-ttu-id="43d82-307">Type of the track (Audio / Video).</span><span class="sxs-lookup"><span data-stu-id="43d82-307">Type of the track (Audio / Video).</span></span> |
| <span data-ttu-id="43d82-308">TrackName</span><span class="sxs-lookup"><span data-stu-id="43d82-308">TrackName</span></span> | <span data-ttu-id="43d82-309">string</span><span class="sxs-lookup"><span data-stu-id="43d82-309">string</span></span> | <span data-ttu-id="43d82-310">Name of the track (either provided by the encoder or, in case of RTMP, server generates in *TrackType_Bitrate* format).</span><span class="sxs-lookup"><span data-stu-id="43d82-310">Name of the track (either provided by the encoder or, in case of RTMP, server generates in *TrackType_Bitrate* format).</span></span> |
| <span data-ttu-id="43d82-311">Bitrate</span><span class="sxs-lookup"><span data-stu-id="43d82-311">Bitrate</span></span> | <span data-ttu-id="43d82-312">integer</span><span class="sxs-lookup"><span data-stu-id="43d82-312">integer</span></span> | <span data-ttu-id="43d82-313">Bitrate of the track.</span><span class="sxs-lookup"><span data-stu-id="43d82-313">Bitrate of the track.</span></span> |
| <span data-ttu-id="43d82-314">IngestUrl</span><span class="sxs-lookup"><span data-stu-id="43d82-314">IngestUrl</span></span> | <span data-ttu-id="43d82-315">string</span><span class="sxs-lookup"><span data-stu-id="43d82-315">string</span></span> | <span data-ttu-id="43d82-316">Ingest URL provided by the live event.</span><span class="sxs-lookup"><span data-stu-id="43d82-316">Ingest URL provided by the live event.</span></span> |
| <span data-ttu-id="43d82-317">EncoderIp</span><span class="sxs-lookup"><span data-stu-id="43d82-317">EncoderIp</span></span> | <span data-ttu-id="43d82-318">string</span><span class="sxs-lookup"><span data-stu-id="43d82-318">string</span></span>  | <span data-ttu-id="43d82-319">IP of the encoder.</span><span class="sxs-lookup"><span data-stu-id="43d82-319">IP of the encoder.</span></span> |
| <span data-ttu-id="43d82-320">EncoderPort</span><span class="sxs-lookup"><span data-stu-id="43d82-320">EncoderPort</span></span> | <span data-ttu-id="43d82-321">string</span><span class="sxs-lookup"><span data-stu-id="43d82-321">string</span></span> | <span data-ttu-id="43d82-322">Port of the encoder from where this stream is coming.</span><span class="sxs-lookup"><span data-stu-id="43d82-322">Port of the encoder from where this stream is coming.</span></span> |
| <span data-ttu-id="43d82-323">Timestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-323">Timestamp</span></span> | <span data-ttu-id="43d82-324">string</span><span class="sxs-lookup"><span data-stu-id="43d82-324">string</span></span> | <span data-ttu-id="43d82-325">First timestamp of the data chunk received.</span><span class="sxs-lookup"><span data-stu-id="43d82-325">First timestamp of the data chunk received.</span></span> |
| <span data-ttu-id="43d82-326">Timescale</span><span class="sxs-lookup"><span data-stu-id="43d82-326">Timescale</span></span> | <span data-ttu-id="43d82-327">string</span><span class="sxs-lookup"><span data-stu-id="43d82-327">string</span></span> | <span data-ttu-id="43d82-328">Timescale in which timestamp is represented.</span><span class="sxs-lookup"><span data-stu-id="43d82-328">Timescale in which timestamp is represented.</span></span> |

## <a name="liveeventincomingstreamsoutofsync"></a><span data-ttu-id="43d82-329">LiveEventIncomingStreamsOutOfSync</span><span class="sxs-lookup"><span data-stu-id="43d82-329">LiveEventIncomingStreamsOutOfSync</span></span>

<span data-ttu-id="43d82-330">The following example shows the schema of the **LiveEventIncomingStreamsOutOfSync** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-330">The following example shows the schema of the **LiveEventIncomingStreamsOutOfSync** event:</span></span> 

```json
[
  {
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaservices/<account-name>",
    "subject": "liveEvent/mle1",
    "eventType": "Microsoft.Media.LiveEventIncomingStreamsOutOfSync",
    "eventTime": "2018-08-10T02:26:20.6269183Z",
    "id": "b9d38923-9210-4c2b-958f-0054467d4dd7",
    "data": {
      "minLastTimestamp": "319996",
      "typeOfStreamWithMinLastTimestamp": "Audio",
      "maxLastTimestamp": "366000",
      "typeOfStreamWithMaxLastTimestamp": "Video"
    },
    "dataVersion": "1.0",
    "metadataVersion": "1"
  }
]
```

<span data-ttu-id="43d82-331">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-331">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-332">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-332">Property</span></span> | <span data-ttu-id="43d82-333">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-333">Type</span></span> | <span data-ttu-id="43d82-334">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-334">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-335">MinLastTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-335">MinLastTimestamp</span></span> | <span data-ttu-id="43d82-336">string</span><span class="sxs-lookup"><span data-stu-id="43d82-336">string</span></span> | <span data-ttu-id="43d82-337">Minimum of last timestamps among all the tracks (audio or video).</span><span class="sxs-lookup"><span data-stu-id="43d82-337">Minimum of last timestamps among all the tracks (audio or video).</span></span> |
| <span data-ttu-id="43d82-338">TypeOfTrackWithMinLastTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-338">TypeOfTrackWithMinLastTimestamp</span></span> | <span data-ttu-id="43d82-339">string</span><span class="sxs-lookup"><span data-stu-id="43d82-339">string</span></span> | <span data-ttu-id="43d82-340">Type of the track (audio or video) with minimum last timestamp.</span><span class="sxs-lookup"><span data-stu-id="43d82-340">Type of the track (audio or video) with minimum last timestamp.</span></span> |
| <span data-ttu-id="43d82-341">MaxLastTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-341">MaxLastTimestamp</span></span> | <span data-ttu-id="43d82-342">string</span><span class="sxs-lookup"><span data-stu-id="43d82-342">string</span></span> | <span data-ttu-id="43d82-343">Maximum of all the timestamps among all the tracks (audio or video).</span><span class="sxs-lookup"><span data-stu-id="43d82-343">Maximum of all the timestamps among all the tracks (audio or video).</span></span> |
| <span data-ttu-id="43d82-344">TypeOfTrackWithMaxLastTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-344">TypeOfTrackWithMaxLastTimestamp</span></span> | <span data-ttu-id="43d82-345">string</span><span class="sxs-lookup"><span data-stu-id="43d82-345">string</span></span> | <span data-ttu-id="43d82-346">Type of the track (audio or video) with maximum last timestamp.</span><span class="sxs-lookup"><span data-stu-id="43d82-346">Type of the track (audio or video) with maximum last timestamp.</span></span> |

## <a name="liveeventincomingvideostreamsoutofsync"></a><span data-ttu-id="43d82-347">LiveEventIncomingVideoStreamsOutOfSync</span><span class="sxs-lookup"><span data-stu-id="43d82-347">LiveEventIncomingVideoStreamsOutOfSync</span></span>

<span data-ttu-id="43d82-348">The following example shows the schema of the **LiveEventIncomingVideoStreamsOutOfSync** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-348">The following example shows the schema of the **LiveEventIncomingVideoStreamsOutOfSync** event:</span></span> 

```json
[
  {
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaServices/<account-name>",
    "subject": "/LiveEvents/LiveEvent1",
    "eventType": "Microsoft.Media.LiveEventIncomingVideoStreamsOutOfSync",
    "eventTime": "2018-01-16T01:57:26.005121Z",
    "id": "6dd4d862-d442-40a0-b9f3-fc14bcf6d750",
    "data": {
      "FirstTimestamp": "2162058216",
      "FirstDuration": "2000",
      "SecondTimestamp": "2162057216",
      "SecondDuration": "2000"
    },
    "dataVersion": "1.0"
  }
]
```

<span data-ttu-id="43d82-349">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-349">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-350">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-350">Property</span></span> | <span data-ttu-id="43d82-351">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-351">Type</span></span> | <span data-ttu-id="43d82-352">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-352">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-353">FirstTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-353">FirstTimestamp</span></span> | <span data-ttu-id="43d82-354">string</span><span class="sxs-lookup"><span data-stu-id="43d82-354">string</span></span> | <span data-ttu-id="43d82-355">Timestamp received for one of the tracks/quality levels of type video.</span><span class="sxs-lookup"><span data-stu-id="43d82-355">Timestamp received for one of the tracks/quality levels of type video.</span></span> |
| <span data-ttu-id="43d82-356">FirstDuration</span><span class="sxs-lookup"><span data-stu-id="43d82-356">FirstDuration</span></span> | <span data-ttu-id="43d82-357">string</span><span class="sxs-lookup"><span data-stu-id="43d82-357">string</span></span> | <span data-ttu-id="43d82-358">Duration of the data chunk with first timestamp.</span><span class="sxs-lookup"><span data-stu-id="43d82-358">Duration of the data chunk with first timestamp.</span></span> |
| <span data-ttu-id="43d82-359">SecondTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-359">SecondTimestamp</span></span> | <span data-ttu-id="43d82-360">string</span><span class="sxs-lookup"><span data-stu-id="43d82-360">string</span></span>  | <span data-ttu-id="43d82-361">Timestamp received for some other track/quality level of the type video.</span><span class="sxs-lookup"><span data-stu-id="43d82-361">Timestamp received for some other track/quality level of the type video.</span></span> |
| <span data-ttu-id="43d82-362">SecondDuration</span><span class="sxs-lookup"><span data-stu-id="43d82-362">SecondDuration</span></span> | <span data-ttu-id="43d82-363">string</span><span class="sxs-lookup"><span data-stu-id="43d82-363">string</span></span> | <span data-ttu-id="43d82-364">Duration of the data chunk with second timestamp.</span><span class="sxs-lookup"><span data-stu-id="43d82-364">Duration of the data chunk with second timestamp.</span></span> |

## <a name="liveeventingestheartbeat"></a><span data-ttu-id="43d82-365">LiveEventIngestHeartbeat</span><span class="sxs-lookup"><span data-stu-id="43d82-365">LiveEventIngestHeartbeat</span></span>

<span data-ttu-id="43d82-366">The following example shows the schema of the **LiveEventIngestHeartbeat** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-366">The following example shows the schema of the **LiveEventIngestHeartbeat** event:</span></span> 

```json
[
  {
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaservices/<account-name>",
    "subject": "liveEvent/mle1",
    "eventType": "Microsoft.Media.LiveEventIngestHeartbeat",
    "eventTime": "2018-08-07T23:17:57.4610506",
    "id": "7f450938-491f-41e1-b06f-c6cd3965d786",
    "data": {
      "trackType": "audio",
      "trackName": "audio",
      "bitrate": 160000,
      "incomingBitrate": 155903,
      "lastTimestamp": "15336837535253637",
      "timescale": "10000000",
      "overlapCount": 0,
      "discontinuityCount": 0,
      "nonincreasingCount": 0,
      "unexpectedBitrate": false,
      "state": "Running",
      "healthy": true
    },
    "dataVersion": "1.0",
    "metadataVersion": "1"
  }
]
```

<span data-ttu-id="43d82-367">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-367">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-368">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-368">Property</span></span> | <span data-ttu-id="43d82-369">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-369">Type</span></span> | <span data-ttu-id="43d82-370">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-370">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-371">TrackType</span><span class="sxs-lookup"><span data-stu-id="43d82-371">TrackType</span></span> | <span data-ttu-id="43d82-372">string</span><span class="sxs-lookup"><span data-stu-id="43d82-372">string</span></span> | <span data-ttu-id="43d82-373">Type of the track (Audio / Video).</span><span class="sxs-lookup"><span data-stu-id="43d82-373">Type of the track (Audio / Video).</span></span> |
| <span data-ttu-id="43d82-374">TrackName</span><span class="sxs-lookup"><span data-stu-id="43d82-374">TrackName</span></span> | <span data-ttu-id="43d82-375">string</span><span class="sxs-lookup"><span data-stu-id="43d82-375">string</span></span> | <span data-ttu-id="43d82-376">Name of the track (either provided by the encoder or, in case of RTMP, server generates in *TrackType_Bitrate* format).</span><span class="sxs-lookup"><span data-stu-id="43d82-376">Name of the track (either provided by the encoder or, in case of RTMP, server generates in *TrackType_Bitrate* format).</span></span> |
| <span data-ttu-id="43d82-377">Bitrate</span><span class="sxs-lookup"><span data-stu-id="43d82-377">Bitrate</span></span> | <span data-ttu-id="43d82-378">integer</span><span class="sxs-lookup"><span data-stu-id="43d82-378">integer</span></span> | <span data-ttu-id="43d82-379">Bitrate of the track.</span><span class="sxs-lookup"><span data-stu-id="43d82-379">Bitrate of the track.</span></span> |
| <span data-ttu-id="43d82-380">IncomingBitrate</span><span class="sxs-lookup"><span data-stu-id="43d82-380">IncomingBitrate</span></span> | <span data-ttu-id="43d82-381">integer</span><span class="sxs-lookup"><span data-stu-id="43d82-381">integer</span></span> | <span data-ttu-id="43d82-382">Calculated bitrate based on data chunks coming from encoder.</span><span class="sxs-lookup"><span data-stu-id="43d82-382">Calculated bitrate based on data chunks coming from encoder.</span></span> |
| <span data-ttu-id="43d82-383">LastTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-383">LastTimestamp</span></span> | <span data-ttu-id="43d82-384">string</span><span class="sxs-lookup"><span data-stu-id="43d82-384">string</span></span> | <span data-ttu-id="43d82-385">Latest timestamp received for a track in last 20 seconds.</span><span class="sxs-lookup"><span data-stu-id="43d82-385">Latest timestamp received for a track in last 20 seconds.</span></span> |
| <span data-ttu-id="43d82-386">Timescale</span><span class="sxs-lookup"><span data-stu-id="43d82-386">Timescale</span></span> | <span data-ttu-id="43d82-387">string</span><span class="sxs-lookup"><span data-stu-id="43d82-387">string</span></span> | <span data-ttu-id="43d82-388">Timescale in which timestamps are expressed.</span><span class="sxs-lookup"><span data-stu-id="43d82-388">Timescale in which timestamps are expressed.</span></span> |
| <span data-ttu-id="43d82-389">OverlapCount</span><span class="sxs-lookup"><span data-stu-id="43d82-389">OverlapCount</span></span> | <span data-ttu-id="43d82-390">integer</span><span class="sxs-lookup"><span data-stu-id="43d82-390">integer</span></span> | <span data-ttu-id="43d82-391">Number of data chunks had overlapped timestamps in last 20 seconds.</span><span class="sxs-lookup"><span data-stu-id="43d82-391">Number of data chunks had overlapped timestamps in last 20 seconds.</span></span> |
| <span data-ttu-id="43d82-392">DiscontinuityCount</span><span class="sxs-lookup"><span data-stu-id="43d82-392">DiscontinuityCount</span></span> | <span data-ttu-id="43d82-393">integer</span><span class="sxs-lookup"><span data-stu-id="43d82-393">integer</span></span> | <span data-ttu-id="43d82-394">Number of discontinuities observed in last 20 seconds.</span><span class="sxs-lookup"><span data-stu-id="43d82-394">Number of discontinuities observed in last 20 seconds.</span></span> |
| <span data-ttu-id="43d82-395">NonIncreasingCount</span><span class="sxs-lookup"><span data-stu-id="43d82-395">NonIncreasingCount</span></span> | <span data-ttu-id="43d82-396">integer</span><span class="sxs-lookup"><span data-stu-id="43d82-396">integer</span></span> | <span data-ttu-id="43d82-397">Number of data chunks with timestamps in the past were received in last 20 seconds.</span><span class="sxs-lookup"><span data-stu-id="43d82-397">Number of data chunks with timestamps in the past were received in last 20 seconds.</span></span> |
| <span data-ttu-id="43d82-398">UnexpectedBitrate</span><span class="sxs-lookup"><span data-stu-id="43d82-398">UnexpectedBitrate</span></span> | <span data-ttu-id="43d82-399">bool</span><span class="sxs-lookup"><span data-stu-id="43d82-399">bool</span></span> | <span data-ttu-id="43d82-400">If expected and actual bitrates differ by more than allowed limit in last 20 seconds.</span><span class="sxs-lookup"><span data-stu-id="43d82-400">If expected and actual bitrates differ by more than allowed limit in last 20 seconds.</span></span> <span data-ttu-id="43d82-401">It's true if and only if, IncomingBitrate >= 2\* bitrate OR IncomingBitrate <= bitrate/2 OR IncomingBitrate = 0.</span><span class="sxs-lookup"><span data-stu-id="43d82-401">It's true if and only if, IncomingBitrate >= 2\* bitrate OR IncomingBitrate <= bitrate/2 OR IncomingBitrate = 0.</span></span> |
| <span data-ttu-id="43d82-402">State</span><span class="sxs-lookup"><span data-stu-id="43d82-402">State</span></span> | <span data-ttu-id="43d82-403">string</span><span class="sxs-lookup"><span data-stu-id="43d82-403">string</span></span> | <span data-ttu-id="43d82-404">State of the live event.</span><span class="sxs-lookup"><span data-stu-id="43d82-404">State of the live event.</span></span> |
| <span data-ttu-id="43d82-405">Healthy</span><span class="sxs-lookup"><span data-stu-id="43d82-405">Healthy</span></span> | <span data-ttu-id="43d82-406">bool</span><span class="sxs-lookup"><span data-stu-id="43d82-406">bool</span></span> | <span data-ttu-id="43d82-407">Indicates whether ingest is healthy based on the counts and flags.</span><span class="sxs-lookup"><span data-stu-id="43d82-407">Indicates whether ingest is healthy based on the counts and flags.</span></span> <span data-ttu-id="43d82-408">Healthy is true if OverlapCount = 0 && DiscontinuityCount = 0 && NonIncreasingCount = 0 && UnexpectedBitrate = false.</span><span class="sxs-lookup"><span data-stu-id="43d82-408">Healthy is true if OverlapCount = 0 && DiscontinuityCount = 0 && NonIncreasingCount = 0 && UnexpectedBitrate = false.</span></span> |

## <a name="liveeventtrackdiscontinuitydetected"></a><span data-ttu-id="43d82-409">LiveEventTrackDiscontinuityDetected</span><span class="sxs-lookup"><span data-stu-id="43d82-409">LiveEventTrackDiscontinuityDetected</span></span>

<span data-ttu-id="43d82-410">The following example shows the schema of the **LiveEventTrackDiscontinuityDetected** event:</span><span class="sxs-lookup"><span data-stu-id="43d82-410">The following example shows the schema of the **LiveEventTrackDiscontinuityDetected** event:</span></span> 

```json
[
  {
    "topic": "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Media/mediaservices/<account-name>",
    "subject": "liveEvent/mle1",
    "eventType": "Microsoft.Media.LiveEventTrackDiscontinuityDetected",
    "eventTime": "2018-08-07T23:18:06.1270405Z",
    "id": "5f4c510d-5be7-4bef-baf0-64b828be9c9b",
    "data": {
      "trackName": "video",
      "previousTimestamp": "15336837615032322",
      "trackType": "video",
      "bitrate": 2962000,
      "newTimestamp": "15336837619774273",
      "discontinuityGap": "575284",
      "timescale": "10000000"
    },
    "dataVersion": "1.0",
    "metadataVersion": "1"
  }
]
```

<span data-ttu-id="43d82-411">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="43d82-411">The data object has the following properties:</span></span>

| <span data-ttu-id="43d82-412">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-412">Property</span></span> | <span data-ttu-id="43d82-413">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-413">Type</span></span> | <span data-ttu-id="43d82-414">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-414">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-415">TrackType</span><span class="sxs-lookup"><span data-stu-id="43d82-415">TrackType</span></span> | <span data-ttu-id="43d82-416">string</span><span class="sxs-lookup"><span data-stu-id="43d82-416">string</span></span> | <span data-ttu-id="43d82-417">Type of the track (Audio / Video).</span><span class="sxs-lookup"><span data-stu-id="43d82-417">Type of the track (Audio / Video).</span></span> |
| <span data-ttu-id="43d82-418">TrackName</span><span class="sxs-lookup"><span data-stu-id="43d82-418">TrackName</span></span> | <span data-ttu-id="43d82-419">string</span><span class="sxs-lookup"><span data-stu-id="43d82-419">string</span></span> | <span data-ttu-id="43d82-420">Name of the track (either provided by the encoder or, in case of RTMP, server generates in *TrackType_Bitrate* format).</span><span class="sxs-lookup"><span data-stu-id="43d82-420">Name of the track (either provided by the encoder or, in case of RTMP, server generates in *TrackType_Bitrate* format).</span></span> |
| <span data-ttu-id="43d82-421">Bitrate</span><span class="sxs-lookup"><span data-stu-id="43d82-421">Bitrate</span></span> | <span data-ttu-id="43d82-422">integer</span><span class="sxs-lookup"><span data-stu-id="43d82-422">integer</span></span> | <span data-ttu-id="43d82-423">Bitrate of the track.</span><span class="sxs-lookup"><span data-stu-id="43d82-423">Bitrate of the track.</span></span> |
| <span data-ttu-id="43d82-424">PreviousTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-424">PreviousTimestamp</span></span> | <span data-ttu-id="43d82-425">string</span><span class="sxs-lookup"><span data-stu-id="43d82-425">string</span></span> | <span data-ttu-id="43d82-426">Timestamp of the previous fragment.</span><span class="sxs-lookup"><span data-stu-id="43d82-426">Timestamp of the previous fragment.</span></span> |
| <span data-ttu-id="43d82-427">NewTimestamp</span><span class="sxs-lookup"><span data-stu-id="43d82-427">NewTimestamp</span></span> | <span data-ttu-id="43d82-428">string</span><span class="sxs-lookup"><span data-stu-id="43d82-428">string</span></span> | <span data-ttu-id="43d82-429">Timestamp of the current fragment.</span><span class="sxs-lookup"><span data-stu-id="43d82-429">Timestamp of the current fragment.</span></span> |
| <span data-ttu-id="43d82-430">DiscontinuityGap</span><span class="sxs-lookup"><span data-stu-id="43d82-430">DiscontinuityGap</span></span> | <span data-ttu-id="43d82-431">string</span><span class="sxs-lookup"><span data-stu-id="43d82-431">string</span></span> | <span data-ttu-id="43d82-432">Gap between above two timestamps.</span><span class="sxs-lookup"><span data-stu-id="43d82-432">Gap between above two timestamps.</span></span> |
| <span data-ttu-id="43d82-433">Timescale</span><span class="sxs-lookup"><span data-stu-id="43d82-433">Timescale</span></span> | <span data-ttu-id="43d82-434">string</span><span class="sxs-lookup"><span data-stu-id="43d82-434">string</span></span> | <span data-ttu-id="43d82-435">Timescale in which both timestamp and discontinuity gap are represented.</span><span class="sxs-lookup"><span data-stu-id="43d82-435">Timescale in which both timestamp and discontinuity gap are represented.</span></span> |

## <a name="common-event-properties"></a><span data-ttu-id="43d82-436">Common event properties</span><span class="sxs-lookup"><span data-stu-id="43d82-436">Common event properties</span></span>

<span data-ttu-id="43d82-437">An event has the following top-level data:</span><span class="sxs-lookup"><span data-stu-id="43d82-437">An event has the following top-level data:</span></span>

| <span data-ttu-id="43d82-438">Property</span><span class="sxs-lookup"><span data-stu-id="43d82-438">Property</span></span> | <span data-ttu-id="43d82-439">Type</span><span class="sxs-lookup"><span data-stu-id="43d82-439">Type</span></span> | <span data-ttu-id="43d82-440">Description</span><span class="sxs-lookup"><span data-stu-id="43d82-440">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="43d82-441">topic</span><span class="sxs-lookup"><span data-stu-id="43d82-441">topic</span></span> | <span data-ttu-id="43d82-442">string</span><span class="sxs-lookup"><span data-stu-id="43d82-442">string</span></span> | <span data-ttu-id="43d82-443">The EventGrid topic.</span><span class="sxs-lookup"><span data-stu-id="43d82-443">The EventGrid topic.</span></span> <span data-ttu-id="43d82-444">This property has the resource ID for the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="43d82-444">This property has the resource ID for the Media Services account.</span></span> |
| <span data-ttu-id="43d82-445">subject</span><span class="sxs-lookup"><span data-stu-id="43d82-445">subject</span></span> | <span data-ttu-id="43d82-446">string</span><span class="sxs-lookup"><span data-stu-id="43d82-446">string</span></span> | <span data-ttu-id="43d82-447">The resource path for the Media Services channel under the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="43d82-447">The resource path for the Media Services channel under the Media Services account.</span></span> <span data-ttu-id="43d82-448">Concatenating the topic and subject give you the resource ID for the job.</span><span class="sxs-lookup"><span data-stu-id="43d82-448">Concatenating the topic and subject give you the resource ID for the job.</span></span> |
| <span data-ttu-id="43d82-449">eventType</span><span class="sxs-lookup"><span data-stu-id="43d82-449">eventType</span></span> | <span data-ttu-id="43d82-450">string</span><span class="sxs-lookup"><span data-stu-id="43d82-450">string</span></span> | <span data-ttu-id="43d82-451">One of the registered event types for this event source.</span><span class="sxs-lookup"><span data-stu-id="43d82-451">One of the registered event types for this event source.</span></span> <span data-ttu-id="43d82-452">For example, "Microsoft.Media.JobStateChange".</span><span class="sxs-lookup"><span data-stu-id="43d82-452">For example, "Microsoft.Media.JobStateChange".</span></span> |
| <span data-ttu-id="43d82-453">eventTime</span><span class="sxs-lookup"><span data-stu-id="43d82-453">eventTime</span></span> | <span data-ttu-id="43d82-454">string</span><span class="sxs-lookup"><span data-stu-id="43d82-454">string</span></span> | <span data-ttu-id="43d82-455">The time the event is generated based on the provider's UTC time.</span><span class="sxs-lookup"><span data-stu-id="43d82-455">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="43d82-456">id</span><span class="sxs-lookup"><span data-stu-id="43d82-456">id</span></span> | <span data-ttu-id="43d82-457">string</span><span class="sxs-lookup"><span data-stu-id="43d82-457">string</span></span> | <span data-ttu-id="43d82-458">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="43d82-458">Unique identifier for the event.</span></span> |
| <span data-ttu-id="43d82-459">data</span><span class="sxs-lookup"><span data-stu-id="43d82-459">data</span></span> | <span data-ttu-id="43d82-460">object</span><span class="sxs-lookup"><span data-stu-id="43d82-460">object</span></span> | <span data-ttu-id="43d82-461">Media Services event data.</span><span class="sxs-lookup"><span data-stu-id="43d82-461">Media Services event data.</span></span> |
| <span data-ttu-id="43d82-462">dataVersion</span><span class="sxs-lookup"><span data-stu-id="43d82-462">dataVersion</span></span> | <span data-ttu-id="43d82-463">string</span><span class="sxs-lookup"><span data-stu-id="43d82-463">string</span></span> | <span data-ttu-id="43d82-464">The schema version of the data object.</span><span class="sxs-lookup"><span data-stu-id="43d82-464">The schema version of the data object.</span></span> <span data-ttu-id="43d82-465">The publisher defines the schema version.</span><span class="sxs-lookup"><span data-stu-id="43d82-465">The publisher defines the schema version.</span></span> |
| <span data-ttu-id="43d82-466">metadataVersion</span><span class="sxs-lookup"><span data-stu-id="43d82-466">metadataVersion</span></span> | <span data-ttu-id="43d82-467">string</span><span class="sxs-lookup"><span data-stu-id="43d82-467">string</span></span> | <span data-ttu-id="43d82-468">The schema version of the event metadata.</span><span class="sxs-lookup"><span data-stu-id="43d82-468">The schema version of the event metadata.</span></span> <span data-ttu-id="43d82-469">Event Grid defines the schema of the top-level properties.</span><span class="sxs-lookup"><span data-stu-id="43d82-469">Event Grid defines the schema of the top-level properties.</span></span> <span data-ttu-id="43d82-470">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="43d82-470">Event Grid provides this value.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43d82-471">Next steps</span><span class="sxs-lookup"><span data-stu-id="43d82-471">Next steps</span></span>

[<span data-ttu-id="43d82-472">Register for job state change events</span><span class="sxs-lookup"><span data-stu-id="43d82-472">Register for job state change events</span></span>](job-state-events-cli-how-to.md)