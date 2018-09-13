---
title: Smooth Streaming Windows Store App Tutorial | Microsoft Docs
description: Learn how to use Azure Media Services to create a C# Windows Store application with a XML MediaElement control to playback Smooth Stream content.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 96416ca866d0a7dfdb1280d5be711b9278aeb27b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662570"
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="ccbc7-103">How to Build a Smooth Streaming Windows Store Application</span><span class="sxs-lookup"><span data-stu-id="ccbc7-103">How to Build a Smooth Streaming Windows Store Application</span></span>
<span data-ttu-id="ccbc7-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="ccbc7-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="ccbc7-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="ccbc7-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="ccbc7-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="ccbc7-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="ccbc7-108">This tutorial contains four lessons:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="ccbc7-109">Create a Basic Smooth Streaming Store Application</span><span class="sxs-lookup"><span data-stu-id="ccbc7-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="ccbc7-110">Add a Slider Bar to Control the Media Progress</span><span class="sxs-lookup"><span data-stu-id="ccbc7-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="ccbc7-111">Select Smooth Streaming Streams</span><span class="sxs-lookup"><span data-stu-id="ccbc7-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="ccbc7-112">Select Smooth Streaming Tracks</span><span class="sxs-lookup"><span data-stu-id="ccbc7-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccbc7-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ccbc7-113">Prerequisites</span></span>
* <span data-ttu-id="ccbc7-114">Windows 8 32-bit or 64-bit.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="ccbc7-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="ccbc7-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span><span class="sxs-lookup"><span data-stu-id="ccbc7-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="ccbc7-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="ccbc7-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="ccbc7-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="ccbc7-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="ccbc7-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span><span class="sxs-lookup"><span data-stu-id="ccbc7-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="ccbc7-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span><span class="sxs-lookup"><span data-stu-id="ccbc7-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="ccbc7-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span><span class="sxs-lookup"><span data-stu-id="ccbc7-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="ccbc7-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span><span class="sxs-lookup"><span data-stu-id="ccbc7-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="ccbc7-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="ccbc7-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span><span class="sxs-lookup"><span data-stu-id="ccbc7-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>
<span data-ttu-id="ccbc7-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="ccbc7-126">The running application looks like:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-126">The running application looks like:</span></span>

![Smooth Streaming Windows Store application example][PlayerApplication]

<span data-ttu-id="ccbc7-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccbc7-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="ccbc7-129">This lesson contains the following procedures:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="ccbc7-130">Create a Windows Store project</span><span class="sxs-lookup"><span data-stu-id="ccbc7-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="ccbc7-131">Design the user interface (XAML)</span><span class="sxs-lookup"><span data-stu-id="ccbc7-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="ccbc7-132">Modify the code behind file</span><span class="sxs-lookup"><span data-stu-id="ccbc7-132">Modify the code behind file</span></span>
4. <span data-ttu-id="ccbc7-133">Compile and test the application</span><span class="sxs-lookup"><span data-stu-id="ccbc7-133">Compile and test the application</span></span>

<span data-ttu-id="ccbc7-134">**To create a Windows Store project**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="ccbc7-135">Run Visual Studio 2012 or later.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="ccbc7-136">From the **FILE** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="ccbc7-137">From the New Project dialog, type or select  the following values:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="ccbc7-138">Name</span><span class="sxs-lookup"><span data-stu-id="ccbc7-138">Name</span></span> | <span data-ttu-id="ccbc7-139">Value</span><span class="sxs-lookup"><span data-stu-id="ccbc7-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ccbc7-140">Template group</span><span class="sxs-lookup"><span data-stu-id="ccbc7-140">Template group</span></span> |<span data-ttu-id="ccbc7-141">Installed/Templates/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="ccbc7-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="ccbc7-142">Template</span><span class="sxs-lookup"><span data-stu-id="ccbc7-142">Template</span></span> |<span data-ttu-id="ccbc7-143">Blank App (XAML)</span><span class="sxs-lookup"><span data-stu-id="ccbc7-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="ccbc7-144">Name</span><span class="sxs-lookup"><span data-stu-id="ccbc7-144">Name</span></span> |<span data-ttu-id="ccbc7-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="ccbc7-145">SSPlayer</span></span> |
| <span data-ttu-id="ccbc7-146">Location</span><span class="sxs-lookup"><span data-stu-id="ccbc7-146">Location</span></span> |<span data-ttu-id="ccbc7-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="ccbc7-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="ccbc7-148">Solution Name</span><span class="sxs-lookup"><span data-stu-id="ccbc7-148">Solution Name</span></span> |<span data-ttu-id="ccbc7-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="ccbc7-149">SSPlayer</span></span> |
| <span data-ttu-id="ccbc7-150">Create directory for solution</span><span class="sxs-lookup"><span data-stu-id="ccbc7-150">Create directory for solution</span></span> |<span data-ttu-id="ccbc7-151">(selected)</span><span class="sxs-lookup"><span data-stu-id="ccbc7-151">(selected)</span></span> |

1. <span data-ttu-id="ccbc7-152">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-152">Click **OK**.</span></span>

<span data-ttu-id="ccbc7-153">**To add a reference to the Smooth Streaming Client SDK**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="ccbc7-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="ccbc7-155">Type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-155">Type or select the following values:</span></span>

| <span data-ttu-id="ccbc7-156">Name</span><span class="sxs-lookup"><span data-stu-id="ccbc7-156">Name</span></span> | <span data-ttu-id="ccbc7-157">Value</span><span class="sxs-lookup"><span data-stu-id="ccbc7-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ccbc7-158">Reference group</span><span class="sxs-lookup"><span data-stu-id="ccbc7-158">Reference group</span></span> |<span data-ttu-id="ccbc7-159">Windows/Extensions</span><span class="sxs-lookup"><span data-stu-id="ccbc7-159">Windows/Extensions</span></span> |
| <span data-ttu-id="ccbc7-160">Reference</span><span class="sxs-lookup"><span data-stu-id="ccbc7-160">Reference</span></span> |<span data-ttu-id="ccbc7-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span><span class="sxs-lookup"><span data-stu-id="ccbc7-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="ccbc7-162">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-162">Click **OK**.</span></span> 

<span data-ttu-id="ccbc7-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="ccbc7-164">In solution explorer, you will see yellow warning mark for these added references.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="ccbc7-165">**To design the player user interface**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="ccbc7-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="ccbc7-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>
   
     <span data-ttu-id="ccbc7-168"><Grid.RowDefinitions></span><span class="sxs-lookup"><span data-stu-id="ccbc7-168"><Grid.RowDefinitions></span></span>
   
         <RowDefinition Height="20"/>    <!-- spacer -->
         <RowDefinition Height="50"/>    <!-- media controls -->
         <RowDefinition Height="100*"/>  <!-- media element -->
         <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
         <RowDefinition Height="50"/>    <!-- status bar -->
     <span data-ttu-id="ccbc7-169"></Grid.RowDefinitions></span><span class="sxs-lookup"><span data-stu-id="ccbc7-169"></Grid.RowDefinitions></span></span>
   
     <span data-ttu-id="ccbc7-170"><StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal"> <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" /> <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" /> <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/> <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/> <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/> <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/> <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/> <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/> </StackPanel></span><span class="sxs-lookup"><span data-stu-id="ccbc7-170"><StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal"> <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" /> <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" /> <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/> <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/> <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/> <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/> <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/> <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/> </StackPanel></span></span>
   
     <span data-ttu-id="ccbc7-171"><StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                 HorizontalAlignment="Center" VerticalAlignment="Center"> <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                       HorizontalAlignment="Center" VerticalAlignment="Center" 
                       AudioCategory="BackgroundCapableMedia" /> <StackPanel Orientation="Horizontal"> <Slider x:Name="sliderProgress" Width="924" Height="44"
                     HorizontalAlignment="Center" VerticalAlignment="Center"
                     PointerPressed="sliderProgress_PointerPressed"/> <Slider x:Name="sliderVolume" 
                     HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                     Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                     Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                     ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/> </StackPanel> </StackPanel></span><span class="sxs-lookup"><span data-stu-id="ccbc7-171"><StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                 HorizontalAlignment="Center" VerticalAlignment="Center"> <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                       HorizontalAlignment="Center" VerticalAlignment="Center" 
                       AudioCategory="BackgroundCapableMedia" /> <StackPanel Orientation="Horizontal"> <Slider x:Name="sliderProgress" Width="924" Height="44"
                     HorizontalAlignment="Center" VerticalAlignment="Center"
                     PointerPressed="sliderProgress_PointerPressed"/> <Slider x:Name="sliderVolume" 
                     HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                  Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                  Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                  ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/> </StackPanel> </StackPanel></span></span>
   
     <span data-ttu-id="ccbc7-172"><StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal"> <TextBlock x:Name="tbStatus" Text="Status :  " 
            FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" /> <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/> </StackPanel></span><span class="sxs-lookup"><span data-stu-id="ccbc7-172"><StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal"> <TextBlock x:Name="tbStatus" Text="Status :  " 
            FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" /> <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/> </StackPanel></span></span>
   
   <span data-ttu-id="ccbc7-173">The MediaElement control is used to playback media.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-173">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="ccbc7-174">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-174">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="ccbc7-175">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-175">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="ccbc7-176">The MediaElement control does not support Smooth Streaming content out-of-box.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-176">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="ccbc7-177">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-177">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="ccbc7-178">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-178">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="ccbc7-179">In this XAML file, some event handlers are associated with the controls.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-179">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="ccbc7-180">You must define those event handlers.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-180">You must define those event handlers.</span></span>

<span data-ttu-id="ccbc7-181">**To modify the code behind file**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-181">**To modify the code behind file**</span></span>

1. <span data-ttu-id="ccbc7-182">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-182">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ccbc7-183">At the top of the file, add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-183">At the top of the file, add the following using statement:</span></span>
   
     <span data-ttu-id="ccbc7-184">using Windows.Media;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-184">using Windows.Media;</span></span>
3. <span data-ttu-id="ccbc7-185">At the beginning of the **MainPage** class, add the following data member:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-185">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="ccbc7-186">private MediaExtensionManager extensions = new MediaExtensionManager();</span><span class="sxs-lookup"><span data-stu-id="ccbc7-186">private MediaExtensionManager extensions = new MediaExtensionManager();</span></span>
4. <span data-ttu-id="ccbc7-187">At the end of the **MainPage** constructor, add the following two lines:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-187">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
     <span data-ttu-id="ccbc7-188">extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");   extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");</span><span class="sxs-lookup"><span data-stu-id="ccbc7-188">extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");   extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");</span></span>
5. <span data-ttu-id="ccbc7-189">At the end of the **MainPage** class, past the following code:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-189">At the end of the **MainPage** class, past the following code:</span></span>
   
   # <a name="region-ui-button-click-events"></a><span data-ttu-id="ccbc7-190">region UI Button Click Events</span><span class="sxs-lookup"><span data-stu-id="ccbc7-190">region UI Button Click Events</span></span>
     <span data-ttu-id="ccbc7-191">private void btnPlay_Click(object sender, RoutedEventArgs e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-191">private void btnPlay_Click(object sender, RoutedEventArgs e)   {</span></span>
   
         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
     <span data-ttu-id="ccbc7-192">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-192">}</span></span>
   
     <span data-ttu-id="ccbc7-193">private void btnPause_Click(object sender, RoutedEventArgs e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-193">private void btnPause_Click(object sender, RoutedEventArgs e)   {</span></span>
   
         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
     <span data-ttu-id="ccbc7-194">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-194">}</span></span>
   
     <span data-ttu-id="ccbc7-195">private void btnSetSource_Click(object sender, RoutedEventArgs e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-195">private void btnSetSource_Click(object sender, RoutedEventArgs e)   {</span></span>
   
         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);
   
         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click the Play button to play the media source.";
         }
     <span data-ttu-id="ccbc7-196">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-196">}</span></span>
   
     <span data-ttu-id="ccbc7-197">private void btnStop_Click(object sender, RoutedEventArgs e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-197">private void btnStop_Click(object sender, RoutedEventArgs e)   {</span></span>
   
         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
     <span data-ttu-id="ccbc7-198">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-198">}</span></span>
   
     <span data-ttu-id="ccbc7-199">private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-199">private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)   {</span></span>
   
         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
     <span data-ttu-id="ccbc7-200">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-200">}</span></span>
   
   # <a name="endregion"></a><span data-ttu-id="ccbc7-201">endregion</span><span class="sxs-lookup"><span data-stu-id="ccbc7-201">endregion</span></span>
   <span data-ttu-id="ccbc7-202">The sliderProgress_PointerPressed event handler is defined here.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-202">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="ccbc7-203">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-203">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="ccbc7-204">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-204">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="ccbc7-205">The finished the code behind file shall look like this:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-205">The finished the code behind file shall look like this:</span></span>

![Codeview in Visual Studio of Smooth Streaming Windows Store application][CodeViewPic]

<span data-ttu-id="ccbc7-207">**To compile and test the application**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-207">**To compile and test the application**</span></span>

1. <span data-ttu-id="ccbc7-208">From the **BUILD** menu, click **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-208">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="ccbc7-209">Change **Active solution platform** to match your development platform.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-209">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="ccbc7-210">Press **F6** to compile the project.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-210">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="ccbc7-211">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-211">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="ccbc7-212">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-212">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="ccbc7-213">Click **Set Source**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-213">Click **Set Source**.</span></span> <span data-ttu-id="ccbc7-214">Because **Auto Play** is enabled by default, the media shall play automatically.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-214">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="ccbc7-215">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-215">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="ccbc7-216">You can control the media volume using the vertical slider.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-216">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="ccbc7-217">However the horizontal slider for controlling the media progress is not fully implemented yet.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-217">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="ccbc7-218">You have completed lesson1.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-218">You have completed lesson1.</span></span>  <span data-ttu-id="ccbc7-219">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-219">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="ccbc7-220">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-220">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="ccbc7-221">Lesson 2: Add a Slider Bar to Control the Media Progress</span><span class="sxs-lookup"><span data-stu-id="ccbc7-221">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>
<span data-ttu-id="ccbc7-222">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-222">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="ccbc7-223">It comes some basic media functions like start, stop and pause.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-223">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="ccbc7-224">In this lesson, you will add a slider bar control to the application.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-224">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="ccbc7-225">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-225">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="ccbc7-226">The slider start and end time also need to be updated in case of live content.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-226">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="ccbc7-227">This can be better handled in the adaptive source update event.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-227">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="ccbc7-228">Media sources are objects that generate media data.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-228">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="ccbc7-229">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-229">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="ccbc7-230">The source resolver is the standard way for the applications to create media sources.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-230">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="ccbc7-231">This lesson contains the following procedures:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-231">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="ccbc7-232">Register the Smooth Streaming handler</span><span class="sxs-lookup"><span data-stu-id="ccbc7-232">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="ccbc7-233">Add the adaptive source manager level event handlers</span><span class="sxs-lookup"><span data-stu-id="ccbc7-233">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="ccbc7-234">Add the adaptive source level event handlers</span><span class="sxs-lookup"><span data-stu-id="ccbc7-234">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="ccbc7-235">Add MediaElement event handlers</span><span class="sxs-lookup"><span data-stu-id="ccbc7-235">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="ccbc7-236">Add slider bar related code</span><span class="sxs-lookup"><span data-stu-id="ccbc7-236">Add slider bar related code</span></span>
6. <span data-ttu-id="ccbc7-237">Compile and test the application</span><span class="sxs-lookup"><span data-stu-id="ccbc7-237">Compile and test the application</span></span>

<span data-ttu-id="ccbc7-238">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-238">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="ccbc7-239">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-239">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ccbc7-240">At the beginning of the file, add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-240">At the beginning of the file, add the following using statement:</span></span>
   
     <span data-ttu-id="ccbc7-241">using Microsoft.Media.AdaptiveStreaming;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-241">using Microsoft.Media.AdaptiveStreaming;</span></span>
3. <span data-ttu-id="ccbc7-242">At the beginning of the MainPage class, add the following data members:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-242">At the beginning of the MainPage class, add the following data members:</span></span>
   
     <span data-ttu-id="ccbc7-243">private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();</span><span class="sxs-lookup"><span data-stu-id="ccbc7-243">private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();</span></span>             
     <span data-ttu-id="ccbc7-244">private IAdaptiveSourceManager adaptiveSourceManager;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-244">private IAdaptiveSourceManager adaptiveSourceManager;</span></span>
4. <span data-ttu-id="ccbc7-245">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-245">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>
   
     <span data-ttu-id="ccbc7-246">// Gets the default instance of AdaptiveSourceManager which manages Smooth //Streaming media sources.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-246">// Gets the default instance of AdaptiveSourceManager which manages Smooth //Streaming media sources.</span></span>
     <span data-ttu-id="ccbc7-247">adaptiveSourceManager = AdaptiveSourceManager.GetDefault(); // Sets property key value to AdaptiveSourceManager default instance.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-247">adaptiveSourceManager = AdaptiveSourceManager.GetDefault(); // Sets property key value to AdaptiveSourceManager default instance.</span></span>
     <span data-ttu-id="ccbc7-248">// {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-248">// {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.</span></span>
     <span data-ttu-id="ccbc7-249">propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-249">propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;</span></span>
5. <span data-ttu-id="ccbc7-250">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-250">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>
   
     <span data-ttu-id="ccbc7-251">// Registers Smooth Streaming byte-stream handler for ".ism" extension and, // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-251">// Registers Smooth Streaming byte-stream handler for ".ism" extension and, // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset.</span></span> 
     <span data-ttu-id="ccbc7-252">// http://\*.ism/manifest URI resources will be resolved by Byte-stream handler.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-252">// http://\*.ism/manifest URI resources will be resolved by Byte-stream handler.</span></span>
     <span data-ttu-id="ccbc7-253">extensions.RegisterByteStreamHandler(</span><span class="sxs-lookup"><span data-stu-id="ccbc7-253">extensions.RegisterByteStreamHandler(</span></span>
   
         "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
         ".ism", 
         "text/xml", 
         propertySet );
     <span data-ttu-id="ccbc7-254">extensions.RegisterByteStreamHandler(</span><span class="sxs-lookup"><span data-stu-id="ccbc7-254">extensions.RegisterByteStreamHandler(</span></span>
   
         "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
         ".ism", 
         "application/vnd.ms-sstr+xml", 
     <span data-ttu-id="ccbc7-255">propertySet);</span><span class="sxs-lookup"><span data-stu-id="ccbc7-255">propertySet);</span></span>
6. <span data-ttu-id="ccbc7-256">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-256">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="ccbc7-257">**To add the adaptive source manager level event handler**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-257">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="ccbc7-258">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-258">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ccbc7-259">Inside the **MainPage** class, add the following data member:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-259">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="ccbc7-260">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-260">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="ccbc7-261">At the end of the **MainPage** class, add the following event handler:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-261">At the end of the **MainPage** class, add the following event handler:</span></span>
   
   # <a name="region-adaptive-source-manager-level-events"></a><span data-ttu-id="ccbc7-262">region Adaptive Source Manager Level Events</span><span class="sxs-lookup"><span data-stu-id="ccbc7-262">region Adaptive Source Manager Level Events</span></span>
     <span data-ttu-id="ccbc7-263">private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-263">private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)   {</span></span>
   
         adaptiveSource = args.AdaptiveSource;
     <span data-ttu-id="ccbc7-264">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-264">}</span></span>
   
   # <a name="endregion-adaptive-source-manager-level-events"></a><span data-ttu-id="ccbc7-265">endregion Adaptive Source Manager Level Events</span><span class="sxs-lookup"><span data-stu-id="ccbc7-265">endregion Adaptive Source Manager Level Events</span></span>
4. <span data-ttu-id="ccbc7-266">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-266">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
   <span data-ttu-id="ccbc7-267">adaptiveSourceManager.AdaptiveSourceOpenedEvent +=   new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);</span><span class="sxs-lookup"><span data-stu-id="ccbc7-267">adaptiveSourceManager.AdaptiveSourceOpenedEvent +=   new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);</span></span>
5. <span data-ttu-id="ccbc7-268">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-268">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="ccbc7-269">**To add adaptive source level event handlers**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-269">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="ccbc7-270">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-270">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ccbc7-271">Inside the **MainPage** class, add the following data member:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-271">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="ccbc7-272">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-272">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="ccbc7-273">At the end of the **MainPage** class, add the following event handlers:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-273">At the end of the **MainPage** class, add the following event handlers:</span></span>
   
   # <a name="region-adaptive-source-level-events"></a><span data-ttu-id="ccbc7-274">region Adaptive Source Level Events</span><span class="sxs-lookup"><span data-stu-id="ccbc7-274">region Adaptive Source Level Events</span></span>
     <span data-ttu-id="ccbc7-275">private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-275">private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)   {</span></span>
   
         adaptiveSource = args.AdaptiveSource;
         manifestObject = args.AdaptiveSource.Manifest;
     <span data-ttu-id="ccbc7-276">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-276">}</span></span>
   
     <span data-ttu-id="ccbc7-277">private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-277">private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)   {</span></span>
   
         adaptiveSourceStatusUpdate = args;
     <span data-ttu-id="ccbc7-278">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-278">}</span></span>
   
     <span data-ttu-id="ccbc7-279">private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-279">private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)   {</span></span>
   
         txtStatus.Text = "Error: " + args.HttpResponse;
     <span data-ttu-id="ccbc7-280">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-280">}</span></span>
   
   # <a name="endregion-adaptive-source-level-events"></a><span data-ttu-id="ccbc7-281">endregion Adaptive Source Level Events</span><span class="sxs-lookup"><span data-stu-id="ccbc7-281">endregion Adaptive Source Level Events</span></span>
4. <span data-ttu-id="ccbc7-282">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-282">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
     <span data-ttu-id="ccbc7-283">adaptiveSource.ManifestReadyEvent +=</span><span class="sxs-lookup"><span data-stu-id="ccbc7-283">adaptiveSource.ManifestReadyEvent +=</span></span>
   
                 mediaElement_ManifestReady;
     <span data-ttu-id="ccbc7-284">adaptiveSource.AdaptiveSourceStatusUpdatedEvent +=</span><span class="sxs-lookup"><span data-stu-id="ccbc7-284">adaptiveSource.AdaptiveSourceStatusUpdatedEvent +=</span></span> 
   
         mediaElement_AdaptiveSourceStatusUpdated;
     <span data-ttu-id="ccbc7-285">adaptiveSource.AdaptiveSourceFailedEvent +=</span><span class="sxs-lookup"><span data-stu-id="ccbc7-285">adaptiveSource.AdaptiveSourceFailedEvent +=</span></span> 
   
         mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="ccbc7-286">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-286">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="ccbc7-287">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-287">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="ccbc7-288">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-288">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="ccbc7-289">**To add Media Element event handlers**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-289">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="ccbc7-290">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-290">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ccbc7-291">At the end of the **MainPage** class, add the following event handlers:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-291">At the end of the **MainPage** class, add the following event handlers:</span></span>
   
   # <a name="region-media-element-event-handlers"></a><span data-ttu-id="ccbc7-292">region Media Element Event Handlers</span><span class="sxs-lookup"><span data-stu-id="ccbc7-292">region Media Element Event Handlers</span></span>
     <span data-ttu-id="ccbc7-293">private void MediaOpened(object sender, RoutedEventArgs e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-293">private void MediaOpened(object sender, RoutedEventArgs e)   {</span></span>
   
         txtStatus.Text = "MediaElement opened";
     <span data-ttu-id="ccbc7-294">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-294">}</span></span>
   
     <span data-ttu-id="ccbc7-295">private void MediaFailed(object sender, ExceptionRoutedEventArgs e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-295">private void MediaFailed(object sender, ExceptionRoutedEventArgs e)   {</span></span>
   
         txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
     <span data-ttu-id="ccbc7-296">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-296">}</span></span>
   
     <span data-ttu-id="ccbc7-297">private void MediaEnded(object sender, RoutedEventArgs e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-297">private void MediaEnded(object sender, RoutedEventArgs e)   {</span></span>
   
         txtStatus.Text ="MediaElement ended.";
     <span data-ttu-id="ccbc7-298">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-298">}</span></span>
   
   # <a name="endregion-media-element-event-handlers"></a><span data-ttu-id="ccbc7-299">endregion Media Element Event Handlers</span><span class="sxs-lookup"><span data-stu-id="ccbc7-299">endregion Media Element Event Handlers</span></span>
3. <span data-ttu-id="ccbc7-300">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-300">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>
   
     <span data-ttu-id="ccbc7-301">mediaElement.MediaOpened += MediaOpened;   mediaElement.MediaEnded += MediaEnded;   mediaElement.MediaFailed += MediaFailed;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-301">mediaElement.MediaOpened += MediaOpened;   mediaElement.MediaEnded += MediaEnded;   mediaElement.MediaFailed += MediaFailed;</span></span>
4. <span data-ttu-id="ccbc7-302">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-302">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="ccbc7-303">**To add slider bar related code**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-303">**To add slider bar related code**</span></span>

1. <span data-ttu-id="ccbc7-304">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-304">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ccbc7-305">At the beginning of the file, add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-305">At the beginning of the file, add the following using statement:</span></span>
   
     <span data-ttu-id="ccbc7-306">using Windows.UI.Core;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-306">using Windows.UI.Core;</span></span>
3. <span data-ttu-id="ccbc7-307">Inside the **MainPage** class, add the following data members:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-307">Inside the **MainPage** class, add the following data members:</span></span>
   
     <span data-ttu-id="ccbc7-308">public static CoreDispatcher _dispatcher;   private DispatcherTimer sliderPositionUpdateDispatcher;</span><span class="sxs-lookup"><span data-stu-id="ccbc7-308">public static CoreDispatcher _dispatcher;   private DispatcherTimer sliderPositionUpdateDispatcher;</span></span>
4. <span data-ttu-id="ccbc7-309">At the end of the **MainPage** constructor, add the following code:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-309">At the end of the **MainPage** constructor, add the following code:</span></span>
   
     <span data-ttu-id="ccbc7-310">_dispatcher = Window.Current.Dispatcher;   PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);   sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);</span><span class="sxs-lookup"><span data-stu-id="ccbc7-310">_dispatcher = Window.Current.Dispatcher;   PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);   sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);</span></span>    
5. <span data-ttu-id="ccbc7-311">At the end of the **MainPage** class, add the following code:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-311">At the end of the **MainPage** class, add the following code:</span></span>
   
   # <a name="region-slidermediaplayer"></a><span data-ttu-id="ccbc7-312">region sliderMediaPlayer</span><span class="sxs-lookup"><span data-stu-id="ccbc7-312">region sliderMediaPlayer</span></span>
     <span data-ttu-id="ccbc7-313">private double SliderFrequency(TimeSpan timevalue)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-313">private double SliderFrequency(TimeSpan timevalue)   {</span></span>
   
         long absvalue = 0;
         double stepfrequency = -1;
   
         if (manifestObject != null)
         {
             absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
         }
         else
         {
             absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
         }
   
         TimeSpan totalDVRDuration = new TimeSpan(absvalue);
   
         if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
         {
            stepfrequency = 10;
         }
         else if (totalDVRDuration.TotalMinutes >= 30 
                  && totalDVRDuration.TotalMinutes < 60)
         {
             stepfrequency = 30;
         }
         else if (totalDVRDuration.TotalHours >= 1)
         {
             stepfrequency = 60;
         }
   
         return stepfrequency;
     <span data-ttu-id="ccbc7-314">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-314">}</span></span>
   
     <span data-ttu-id="ccbc7-315">void updateSliderPositionoNTicks(object sender, object e)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-315">void updateSliderPositionoNTicks(object sender, object e)   {</span></span>
   
         sliderProgress.Value = mediaElement.Position.TotalSeconds;
     <span data-ttu-id="ccbc7-316">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-316">}</span></span>
   
     <span data-ttu-id="ccbc7-317">public void setupTimer()   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-317">public void setupTimer()   {</span></span>
   
         sliderPositionUpdateDispatcher = new DispatcherTimer();
         sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
         startTimer();
     <span data-ttu-id="ccbc7-318">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-318">}</span></span>
   
     <span data-ttu-id="ccbc7-319">public void startTimer()   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-319">public void startTimer()   {</span></span>
   
         sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
         sliderPositionUpdateDispatcher.Start();
     <span data-ttu-id="ccbc7-320">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-320">}</span></span>
   
     <span data-ttu-id="ccbc7-321">// Slider start and end time must be updated in case of live content   public async void setSliderStartTime(long startTime)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-321">// Slider start and end time must be updated in case of live content   public async void setSliderStartTime(long startTime)   {</span></span>
   
         await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
         {
             TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
             double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
             sliderProgress.Minimum = absvalue;
         });
     <span data-ttu-id="ccbc7-322">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-322">}</span></span>
   
     <span data-ttu-id="ccbc7-323">// Slider start and end time must be updated in case of live content   public async void setSliderEndTime(long startTime)   {</span><span class="sxs-lookup"><span data-stu-id="ccbc7-323">// Slider start and end time must be updated in case of live content   public async void setSliderEndTime(long startTime)   {</span></span>
   
         await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
         {
             TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
             double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
             sliderProgress.Maximum = absvalue;
         });
     <span data-ttu-id="ccbc7-324">}</span><span class="sxs-lookup"><span data-stu-id="ccbc7-324">}</span></span>
   
   # <a name="endregion-slidermediaplayer"></a><span data-ttu-id="ccbc7-325">endregion sliderMediaPlayer</span><span class="sxs-lookup"><span data-stu-id="ccbc7-325">endregion sliderMediaPlayer</span></span>
   <span data-ttu-id="ccbc7-326">**Note:** CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-326">**Note:** CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="ccbc7-327">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-327">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="ccbc7-328">For example:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-328">For example:</span></span>
   
     <span data-ttu-id="ccbc7-329">await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ccbc7-329">await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan</span></span> 
   
       timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
     <span data-ttu-id="ccbc7-330">double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);</span><span class="sxs-lookup"><span data-stu-id="ccbc7-330">double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);</span></span> 
   
       sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="ccbc7-331">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-331">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>
   
     <span data-ttu-id="ccbc7-332">setSliderStartTime(args.StartTime);   setSliderEndTime(args.EndTime);</span><span class="sxs-lookup"><span data-stu-id="ccbc7-332">setSliderStartTime(args.StartTime);   setSliderEndTime(args.EndTime);</span></span>
7. <span data-ttu-id="ccbc7-333">At the end of the **MediaOpened** method, add the following code:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-333">At the end of the **MediaOpened** method, add the following code:</span></span>
   
   <span data-ttu-id="ccbc7-334">sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan); sliderProgress.Width = mediaElement.Width; setupTimer();</span><span class="sxs-lookup"><span data-stu-id="ccbc7-334">sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan); sliderProgress.Width = mediaElement.Width; setupTimer();</span></span>
8. <span data-ttu-id="ccbc7-335">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-335">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="ccbc7-336">**To compile and test the application**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-336">**To compile and test the application**</span></span>

1. <span data-ttu-id="ccbc7-337">Press **F6** to compile the project.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-337">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="ccbc7-338">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-338">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="ccbc7-339">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-339">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="ccbc7-340">Click **Set Source**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-340">Click **Set Source**.</span></span> 
5. <span data-ttu-id="ccbc7-341">Test the slider bar.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-341">Test the slider bar.</span></span>

<span data-ttu-id="ccbc7-342">You have completed lesson 2.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-342">You have completed lesson 2.</span></span>  <span data-ttu-id="ccbc7-343">In this lesson you added a slider to application.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-343">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="ccbc7-344">Lesson 3: Select Smooth Streaming Streams</span><span class="sxs-lookup"><span data-stu-id="ccbc7-344">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="ccbc7-345">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-345">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="ccbc7-346">In this lesson, you will enable viewers to select streams.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-346">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="ccbc7-347">This lesson contains the following procedures:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-347">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="ccbc7-348">Modify the XAML file</span><span class="sxs-lookup"><span data-stu-id="ccbc7-348">Modify the XAML file</span></span>
2. <span data-ttu-id="ccbc7-349">Modify the code behand file</span><span class="sxs-lookup"><span data-stu-id="ccbc7-349">Modify the code behand file</span></span>
3. <span data-ttu-id="ccbc7-350">Compile and test the application</span><span class="sxs-lookup"><span data-stu-id="ccbc7-350">Compile and test the application</span></span>

<span data-ttu-id="ccbc7-351">**To modify the XAML file**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-351">**To modify the XAML file**</span></span>

1. <span data-ttu-id="ccbc7-352">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-352">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="ccbc7-353">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-353">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
        <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
        </Grid.RowDefinitions>
3. <span data-ttu-id="ccbc7-354">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-354">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>
   
        <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
        </Grid>
4. <span data-ttu-id="ccbc7-355">Press **CTRL+S** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-355">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="ccbc7-356">**To modify the code behind file**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-356">**To modify the code behind file**</span></span>

1. <span data-ttu-id="ccbc7-357">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-357">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ccbc7-358">Inside the SSPlayer namespace, add a new class:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-358">Inside the SSPlayer namespace, add a new class:</span></span>
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke the video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. <span data-ttu-id="ccbc7-359">At the beginning of the MainPage class, add the following variable definitions:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-359">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Stream> availableStreams;
        private List<Stream> availableAudioStreams;
        private List<Stream> availableTextStreams;
        private List<Stream> availableVideoStreams;
4. <span data-ttu-id="ccbc7-360">Inside the MainPage class, add the following region:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-360">Inside the MainPage class, add the following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality to select streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from the mediaElement_ManifestReady event handler 
        // to retrieve the streams and populate them to the local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate the stream lists based on the types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select the default selected streams from the manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set the list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update the stream check box list on the UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select the frist video stream from the list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "The audio stream is changed to " + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select the frist audio stream from the list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. <span data-ttu-id="ccbc7-361">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-361">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="ccbc7-362">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-362">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="ccbc7-363">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-363">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="ccbc7-364">**To compile and test the application**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-364">**To compile and test the application**</span></span>

1. <span data-ttu-id="ccbc7-365">Press **F6** to compile the project.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-365">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="ccbc7-366">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-366">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="ccbc7-367">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-367">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="ccbc7-368">Click **Set Source**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-368">Click **Set Source**.</span></span> 
5. <span data-ttu-id="ccbc7-369">The default language is audio_eng.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-369">The default language is audio_eng.</span></span> <span data-ttu-id="ccbc7-370">Try to switch between audio_eng and audio_es.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-370">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="ccbc7-371">Everytime, you select a new stream, you must click the Submit button.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-371">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="ccbc7-372">You have completed lesson 3.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-372">You have completed lesson 3.</span></span>  <span data-ttu-id="ccbc7-373">In this lesson, you add the functionality to choose streams.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-373">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="ccbc7-374">Lesson 4: Select Smooth Streaming Tracks</span><span class="sxs-lookup"><span data-stu-id="ccbc7-374">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="ccbc7-375">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-375">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="ccbc7-376">In this lesson, you will enable users to select tracks.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-376">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="ccbc7-377">This lesson contains the following procedures:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-377">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="ccbc7-378">Modify the XAML file</span><span class="sxs-lookup"><span data-stu-id="ccbc7-378">Modify the XAML file</span></span>
2. <span data-ttu-id="ccbc7-379">Modify the code behand file</span><span class="sxs-lookup"><span data-stu-id="ccbc7-379">Modify the code behand file</span></span>
3. <span data-ttu-id="ccbc7-380">Compile and test the application</span><span class="sxs-lookup"><span data-stu-id="ccbc7-380">Compile and test the application</span></span>

<span data-ttu-id="ccbc7-381">**To modify the XAML file**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-381">**To modify the XAML file**</span></span>

1. <span data-ttu-id="ccbc7-382">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-382">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="ccbc7-383">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-383">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
        <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
        </StackPanel>
3. <span data-ttu-id="ccbc7-384">Press **CTRL+S** to save he changes</span><span class="sxs-lookup"><span data-stu-id="ccbc7-384">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="ccbc7-385">**To modify the code behind file**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-385">**To modify the code behind file**</span></span>

1. <span data-ttu-id="ccbc7-386">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-386">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="ccbc7-387">Inside the SSPlayer namespace, add a new class:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-387">Inside the SSPlayer namespace, add a new class:</span></span>
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. <span data-ttu-id="ccbc7-388">At the beginning of the MainPage class, add the following variable definitions:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-388">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="ccbc7-389">Inside the MainPage class, add the following region:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-389">Inside the MainPage class, add the following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality to select video streams
        /// </summary>
   
        /// This Function gets the tracks for the selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets the video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set the UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update the track check box list on the UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of the selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects the tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. <span data-ttu-id="ccbc7-390">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-390">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getTracks(manifestObject);
        refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="ccbc7-391">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-391">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="ccbc7-392">**To compile and test the application**</span><span class="sxs-lookup"><span data-stu-id="ccbc7-392">**To compile and test the application**</span></span>

1. <span data-ttu-id="ccbc7-393">Press **F6** to compile the project.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-393">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="ccbc7-394">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-394">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="ccbc7-395">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-395">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="ccbc7-396">Click **Set Source**.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-396">Click **Set Source**.</span></span> 
5. <span data-ttu-id="ccbc7-397">By default, all of the tracks of the video stream are selected.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-397">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="ccbc7-398">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-398">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="ccbc7-399">You must click Submit after each change.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-399">You must click Submit after each change.</span></span>  <span data-ttu-id="ccbc7-400">You can see the video quality changes.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-400">You can see the video quality changes.</span></span>

<span data-ttu-id="ccbc7-401">You have completed lesson 4.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-401">You have completed lesson 4.</span></span>  <span data-ttu-id="ccbc7-402">In this lesson, you add the functionality to choose tracks.</span><span class="sxs-lookup"><span data-stu-id="ccbc7-402">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ccbc7-403">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="ccbc7-403">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ccbc7-404">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="ccbc7-404">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="ccbc7-405">Other Resources:</span><span class="sxs-lookup"><span data-stu-id="ccbc7-405">Other Resources:</span></span>
* [<span data-ttu-id="ccbc7-406">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span><span class="sxs-lookup"><span data-stu-id="ccbc7-406">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="ccbc7-407">Smooth Streaming Technical Overview</span><span class="sxs-lookup"><span data-stu-id="ccbc7-407">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png



