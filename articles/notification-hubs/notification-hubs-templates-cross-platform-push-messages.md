---
title: Templates
description: This topic explains Templates for Azure notification hubs.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: ''
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5434bc8b5b915d8cc0a4965372fa04d5e98d5e28
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564576"
---
# <a name="templates"></a><span data-ttu-id="41df4-103">Templates</span><span class="sxs-lookup"><span data-stu-id="41df4-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="41df4-104">Overview</span><span class="sxs-lookup"><span data-stu-id="41df4-104">Overview</span></span>
<span data-ttu-id="41df4-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span><span class="sxs-lookup"><span data-stu-id="41df4-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="41df4-106">Using templates, an app can realize several different benefits, including the following :</span><span class="sxs-lookup"><span data-stu-id="41df4-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="41df4-107">A platform-agnostic backend</span><span class="sxs-lookup"><span data-stu-id="41df4-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="41df4-108">Personalized notifications</span><span class="sxs-lookup"><span data-stu-id="41df4-108">Personalized notifications</span></span>
* <span data-ttu-id="41df4-109">Client-version independence</span><span class="sxs-lookup"><span data-stu-id="41df4-109">Client-version independence</span></span>
* <span data-ttu-id="41df4-110">Easy localization</span><span class="sxs-lookup"><span data-stu-id="41df4-110">Easy localization</span></span>

<span data-ttu-id="41df4-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span><span class="sxs-lookup"><span data-stu-id="41df4-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="41df4-112">Using templates cross-platform</span><span class="sxs-lookup"><span data-stu-id="41df4-112">Using templates cross-platform</span></span>
<span data-ttu-id="41df4-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="41df4-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="41df4-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span><span class="sxs-lookup"><span data-stu-id="41df4-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="41df4-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span><span class="sxs-lookup"><span data-stu-id="41df4-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="41df4-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span><span class="sxs-lookup"><span data-stu-id="41df4-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="41df4-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span><span class="sxs-lookup"><span data-stu-id="41df4-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="41df4-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span><span class="sxs-lookup"><span data-stu-id="41df4-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="41df4-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span><span class="sxs-lookup"><span data-stu-id="41df4-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="41df4-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span><span class="sxs-lookup"><span data-stu-id="41df4-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="41df4-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span><span class="sxs-lookup"><span data-stu-id="41df4-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="41df4-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span><span class="sxs-lookup"><span data-stu-id="41df4-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="41df4-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span><span class="sxs-lookup"><span data-stu-id="41df4-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="41df4-124">The following picture illustrates the above process:</span><span class="sxs-lookup"><span data-stu-id="41df4-124">The following picture illustrates the above process:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="41df4-125">The template for the iOS client app registration is as follows:</span><span class="sxs-lookup"><span data-stu-id="41df4-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="41df4-126">The corresponding template for the Windows Store client app is:</span><span class="sxs-lookup"><span data-stu-id="41df4-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="41df4-127">Notice that the actual message is substituted for the expression $(message).</span><span class="sxs-lookup"><span data-stu-id="41df4-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="41df4-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span><span class="sxs-lookup"><span data-stu-id="41df4-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="41df4-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span><span class="sxs-lookup"><span data-stu-id="41df4-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="41df4-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span><span class="sxs-lookup"><span data-stu-id="41df4-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="41df4-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span><span class="sxs-lookup"><span data-stu-id="41df4-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="41df4-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span><span class="sxs-lookup"><span data-stu-id="41df4-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="41df4-133">This behavior can be used to translate platform-independent notifications into more notifications.</span><span class="sxs-lookup"><span data-stu-id="41df4-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="41df4-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span><span class="sxs-lookup"><span data-stu-id="41df4-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="41df4-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span><span class="sxs-lookup"><span data-stu-id="41df4-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="41df4-136">Using templates for personalization</span><span class="sxs-lookup"><span data-stu-id="41df4-136">Using templates for personalization</span></span>
<span data-ttu-id="41df4-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span><span class="sxs-lookup"><span data-stu-id="41df4-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="41df4-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span><span class="sxs-lookup"><span data-stu-id="41df4-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="41df4-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span><span class="sxs-lookup"><span data-stu-id="41df4-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="41df4-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span><span class="sxs-lookup"><span data-stu-id="41df4-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="41df4-141">The template for the one-day forecast with Celsius temperatures is as follows:</span><span class="sxs-lookup"><span data-stu-id="41df4-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="41df4-142">The message sent to the Notification Hub contains all the following properties:</span><span class="sxs-lookup"><span data-stu-id="41df4-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="41df4-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="41df4-143">day1_image</span></span></td><td><span data-ttu-id="41df4-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="41df4-144">day2_image</span></span></td><td><span data-ttu-id="41df4-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="41df4-145">day3_image</span></span></td><td><span data-ttu-id="41df4-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="41df4-146">day4_image</span></span></td><td><span data-ttu-id="41df4-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="41df4-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="41df4-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="41df4-148">day1_tempC</span></span></td><td><span data-ttu-id="41df4-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="41df4-149">day2_tempC</span></span></td><td><span data-ttu-id="41df4-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="41df4-150">day3_tempC</span></span></td><td><span data-ttu-id="41df4-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="41df4-151">day4_tempC</span></span></td><td><span data-ttu-id="41df4-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="41df4-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="41df4-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="41df4-153">day1_tempF</span></span></td><td><span data-ttu-id="41df4-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="41df4-154">day2_tempF</span></span></td><td><span data-ttu-id="41df4-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="41df4-155">day3_tempF</span></span></td><td><span data-ttu-id="41df4-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="41df4-156">day4_tempF</span></span></td><td><span data-ttu-id="41df4-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="41df4-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="41df4-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span><span class="sxs-lookup"><span data-stu-id="41df4-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="41df4-159">The following picture illustrates this scenario:</span><span class="sxs-lookup"><span data-stu-id="41df4-159">The following picture illustrates this scenario:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="41df4-160">How to register templates</span><span class="sxs-lookup"><span data-stu-id="41df4-160">How to register templates</span></span>
<span data-ttu-id="41df4-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="41df4-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="41df4-162">Template expression language</span><span class="sxs-lookup"><span data-stu-id="41df4-162">Template expression language</span></span>
<span data-ttu-id="41df4-163">Templates are limited to XML or JSON document formats.</span><span class="sxs-lookup"><span data-stu-id="41df4-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="41df4-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span><span class="sxs-lookup"><span data-stu-id="41df4-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="41df4-165">The following table shows the language allowed in templates:</span><span class="sxs-lookup"><span data-stu-id="41df4-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="41df4-166">Expression</span><span class="sxs-lookup"><span data-stu-id="41df4-166">Expression</span></span> | <span data-ttu-id="41df4-167">Description</span><span class="sxs-lookup"><span data-stu-id="41df4-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41df4-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="41df4-168">$(prop)</span></span> |<span data-ttu-id="41df4-169">Reference to an event property with the given name.</span><span class="sxs-lookup"><span data-stu-id="41df4-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="41df4-170">Property names are not case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="41df4-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="41df4-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span><span class="sxs-lookup"><span data-stu-id="41df4-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="41df4-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="41df4-172">$(prop, n)</span></span> |<span data-ttu-id="41df4-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span><span class="sxs-lookup"><span data-stu-id="41df4-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="41df4-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="41df4-174">.(prop, n)</span></span> |<span data-ttu-id="41df4-175">As above, but the text is suffixed with three dots as it is clipped.</span><span class="sxs-lookup"><span data-stu-id="41df4-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="41df4-176">The total size of the clipped string and the suffix does not exceed n characters.</span><span class="sxs-lookup"><span data-stu-id="41df4-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="41df4-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span><span class="sxs-lookup"><span data-stu-id="41df4-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="41df4-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="41df4-178">%(prop)</span></span> |<span data-ttu-id="41df4-179">Similar to $(name) except that the output is URI-encoded.</span><span class="sxs-lookup"><span data-stu-id="41df4-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="41df4-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="41df4-180">#(prop)</span></span> |<span data-ttu-id="41df4-181">Used in JSON templates (for example, for iOS and Android templates).</span><span class="sxs-lookup"><span data-stu-id="41df4-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="41df4-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span><span class="sxs-lookup"><span data-stu-id="41df4-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="41df4-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;\*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span><span class="sxs-lookup"><span data-stu-id="41df4-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;\*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="41df4-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span><span class="sxs-lookup"><span data-stu-id="41df4-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="41df4-185">‘text’ or “text”</span><span class="sxs-lookup"><span data-stu-id="41df4-185">‘text’ or “text”</span></span> |<span data-ttu-id="41df4-186">A literal.</span><span class="sxs-lookup"><span data-stu-id="41df4-186">A literal.</span></span> <span data-ttu-id="41df4-187">Literals contain arbitrary text enclosed in single or double quotes.</span><span class="sxs-lookup"><span data-stu-id="41df4-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="41df4-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="41df4-188">expr1 + expr2</span></span> |<span data-ttu-id="41df4-189">The concatenation operator joining two expressions into a single string.</span><span class="sxs-lookup"><span data-stu-id="41df4-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="41df4-190">The expressions can be any of the preceding forms.</span><span class="sxs-lookup"><span data-stu-id="41df4-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="41df4-191">When using concatenation, the entire expression must be surrounded with {}.</span><span class="sxs-lookup"><span data-stu-id="41df4-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="41df4-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="41df4-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="41df4-193">For example, the following is not a valid XML template:</span><span class="sxs-lookup"><span data-stu-id="41df4-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="41df4-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span><span class="sxs-lookup"><span data-stu-id="41df4-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="41df4-195">For example:</span><span class="sxs-lookup"><span data-stu-id="41df4-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>



