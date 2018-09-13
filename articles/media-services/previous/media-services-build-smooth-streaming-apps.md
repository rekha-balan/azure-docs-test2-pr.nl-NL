---
title: Smooth Streaming Windows Store App Tutorial | Microsoft Docs
description: Learn how to use Azure Media Services to create a C# Windows Store application with a XML MediaElement control to playback Smooth Stream content.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: f55e8aa652d65ea751a77742fa5823b09d9ee87b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855825"
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="928df-103">How to Build a Smooth Streaming Windows Store Application</span><span class="sxs-lookup"><span data-stu-id="928df-103">How to Build a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="928df-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span><span class="sxs-lookup"><span data-stu-id="928df-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="928df-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span><span class="sxs-lookup"><span data-stu-id="928df-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="928df-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="928df-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="928df-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="928df-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="928df-108">This tutorial contains four lessons:</span><span class="sxs-lookup"><span data-stu-id="928df-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="928df-109">Create a Basic Smooth Streaming Store Application</span><span class="sxs-lookup"><span data-stu-id="928df-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="928df-110">Add a Slider Bar to Control the Media Progress</span><span class="sxs-lookup"><span data-stu-id="928df-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="928df-111">Select Smooth Streaming Streams</span><span class="sxs-lookup"><span data-stu-id="928df-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="928df-112">Select Smooth Streaming Tracks</span><span class="sxs-lookup"><span data-stu-id="928df-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="928df-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="928df-113">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="928df-114">Windows Store projects version 8.1 and earlier are not supported in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="928df-114">Windows Store projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="928df-115">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="928df-115">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

* <span data-ttu-id="928df-116">Windows 8 32-bit or 64-bit.</span><span class="sxs-lookup"><span data-stu-id="928df-116">Windows 8 32-bit or 64-bit.</span></span>
* <span data-ttu-id="928df-117">Visual Studio versions 2012 through 2015.</span><span class="sxs-lookup"><span data-stu-id="928df-117">Visual Studio versions 2012 through 2015.</span></span>
* <span data-ttu-id="928df-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="928df-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="928df-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span><span class="sxs-lookup"><span data-stu-id="928df-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="928df-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span><span class="sxs-lookup"><span data-stu-id="928df-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="928df-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span><span class="sxs-lookup"><span data-stu-id="928df-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="928df-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span><span class="sxs-lookup"><span data-stu-id="928df-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="928df-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span><span class="sxs-lookup"><span data-stu-id="928df-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="928df-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span><span class="sxs-lookup"><span data-stu-id="928df-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="928df-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span><span class="sxs-lookup"><span data-stu-id="928df-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="928df-126">The running application looks like:</span><span class="sxs-lookup"><span data-stu-id="928df-126">The running application looks like:</span></span>

![Smooth Streaming Windows Store application example][PlayerApplication]

<span data-ttu-id="928df-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="928df-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="928df-129">This lesson contains the following procedures:</span><span class="sxs-lookup"><span data-stu-id="928df-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="928df-130">Create a Windows Store project</span><span class="sxs-lookup"><span data-stu-id="928df-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="928df-131">Design the user interface (XAML)</span><span class="sxs-lookup"><span data-stu-id="928df-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="928df-132">Modify the code behind file</span><span class="sxs-lookup"><span data-stu-id="928df-132">Modify the code behind file</span></span>
4. <span data-ttu-id="928df-133">Compile and test the application</span><span class="sxs-lookup"><span data-stu-id="928df-133">Compile and test the application</span></span>

<span data-ttu-id="928df-134">**To create a Windows Store project**</span><span class="sxs-lookup"><span data-stu-id="928df-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="928df-135">Run Visual Studio; versions 2012 through 2015 are supported.</span><span class="sxs-lookup"><span data-stu-id="928df-135">Run Visual Studio; versions 2012 through 2015 are supported.</span></span>
2. <span data-ttu-id="928df-136">From the **FILE** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="928df-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="928df-137">From the New Project dialog, type or select  the following values:</span><span class="sxs-lookup"><span data-stu-id="928df-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="928df-138">Name</span><span class="sxs-lookup"><span data-stu-id="928df-138">Name</span></span> | <span data-ttu-id="928df-139">Value</span><span class="sxs-lookup"><span data-stu-id="928df-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="928df-140">Template group</span><span class="sxs-lookup"><span data-stu-id="928df-140">Template group</span></span> |<span data-ttu-id="928df-141">Installed/Templates/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="928df-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="928df-142">Template</span><span class="sxs-lookup"><span data-stu-id="928df-142">Template</span></span> |<span data-ttu-id="928df-143">Blank App (XAML)</span><span class="sxs-lookup"><span data-stu-id="928df-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="928df-144">Name</span><span class="sxs-lookup"><span data-stu-id="928df-144">Name</span></span> |<span data-ttu-id="928df-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="928df-145">SSPlayer</span></span> |
| <span data-ttu-id="928df-146">Location</span><span class="sxs-lookup"><span data-stu-id="928df-146">Location</span></span> |<span data-ttu-id="928df-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="928df-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="928df-148">Solution Name</span><span class="sxs-lookup"><span data-stu-id="928df-148">Solution Name</span></span> |<span data-ttu-id="928df-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="928df-149">SSPlayer</span></span> |
| <span data-ttu-id="928df-150">Create directory for solution</span><span class="sxs-lookup"><span data-stu-id="928df-150">Create directory for solution</span></span> |<span data-ttu-id="928df-151">(selected)</span><span class="sxs-lookup"><span data-stu-id="928df-151">(selected)</span></span> |

1. <span data-ttu-id="928df-152">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="928df-152">Click **OK**.</span></span>

<span data-ttu-id="928df-153">**To add a reference to the Smooth Streaming Client SDK**</span><span class="sxs-lookup"><span data-stu-id="928df-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="928df-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="928df-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="928df-155">Type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="928df-155">Type or select the following values:</span></span>

| <span data-ttu-id="928df-156">Name</span><span class="sxs-lookup"><span data-stu-id="928df-156">Name</span></span> | <span data-ttu-id="928df-157">Value</span><span class="sxs-lookup"><span data-stu-id="928df-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="928df-158">Reference group</span><span class="sxs-lookup"><span data-stu-id="928df-158">Reference group</span></span> |<span data-ttu-id="928df-159">Windows/Extensions</span><span class="sxs-lookup"><span data-stu-id="928df-159">Windows/Extensions</span></span> |
| <span data-ttu-id="928df-160">Reference</span><span class="sxs-lookup"><span data-stu-id="928df-160">Reference</span></span> |<span data-ttu-id="928df-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span><span class="sxs-lookup"><span data-stu-id="928df-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="928df-162">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="928df-162">Click **OK**.</span></span> 

<span data-ttu-id="928df-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span><span class="sxs-lookup"><span data-stu-id="928df-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="928df-164">In solution explorer, you will see yellow warning mark for these added references.</span><span class="sxs-lookup"><span data-stu-id="928df-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="928df-165">**To design the player user interface**</span><span class="sxs-lookup"><span data-stu-id="928df-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="928df-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span><span class="sxs-lookup"><span data-stu-id="928df-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="928df-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span><span class="sxs-lookup"><span data-stu-id="928df-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   <span data-ttu-id="928df-168">The MediaElement control is used to playback media.</span><span class="sxs-lookup"><span data-stu-id="928df-168">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="928df-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span><span class="sxs-lookup"><span data-stu-id="928df-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="928df-170">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="928df-170">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="928df-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span><span class="sxs-lookup"><span data-stu-id="928df-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="928df-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span><span class="sxs-lookup"><span data-stu-id="928df-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="928df-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span><span class="sxs-lookup"><span data-stu-id="928df-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="928df-174">In this XAML file, some event handlers are associated with the controls.</span><span class="sxs-lookup"><span data-stu-id="928df-174">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="928df-175">You must define those event handlers.</span><span class="sxs-lookup"><span data-stu-id="928df-175">You must define those event handlers.</span></span>

<span data-ttu-id="928df-176">**To modify the code behind file**</span><span class="sxs-lookup"><span data-stu-id="928df-176">**To modify the code behind file**</span></span>

1. <span data-ttu-id="928df-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="928df-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="928df-178">At the top of the file, add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="928df-178">At the top of the file, add the following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="928df-179">At the beginning of the **MainPage** class, add the following data member:</span><span class="sxs-lookup"><span data-stu-id="928df-179">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="928df-180">At the end of the **MainPage** constructor, add the following two lines:</span><span class="sxs-lookup"><span data-stu-id="928df-180">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="928df-181">At the end of the **MainPage** class, paste the following code:</span><span class="sxs-lookup"><span data-stu-id="928df-181">At the end of the **MainPage** class, paste the following code:</span></span>
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

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
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="928df-182">The sliderProgress_PointerPressed event handler is defined here.</span><span class="sxs-lookup"><span data-stu-id="928df-182">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="928df-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="928df-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="928df-184">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="928df-184">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="928df-185">The finished the code behind file shall look like this:</span><span class="sxs-lookup"><span data-stu-id="928df-185">The finished the code behind file shall look like this:</span></span>

![Codeview in Visual Studio of Smooth Streaming Windows Store application][CodeViewPic]

<span data-ttu-id="928df-187">**To compile and test the application**</span><span class="sxs-lookup"><span data-stu-id="928df-187">**To compile and test the application**</span></span>

1. <span data-ttu-id="928df-188">From the **BUILD** menu, click **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="928df-188">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="928df-189">Change **Active solution platform** to match your development platform.</span><span class="sxs-lookup"><span data-stu-id="928df-189">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="928df-190">Press **F6** to compile the project.</span><span class="sxs-lookup"><span data-stu-id="928df-190">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="928df-191">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="928df-191">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="928df-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span><span class="sxs-lookup"><span data-stu-id="928df-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="928df-193">Click **Set Source**.</span><span class="sxs-lookup"><span data-stu-id="928df-193">Click **Set Source**.</span></span> <span data-ttu-id="928df-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span><span class="sxs-lookup"><span data-stu-id="928df-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="928df-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span><span class="sxs-lookup"><span data-stu-id="928df-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="928df-196">You can control the media volume using the vertical slider.</span><span class="sxs-lookup"><span data-stu-id="928df-196">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="928df-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span><span class="sxs-lookup"><span data-stu-id="928df-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="928df-198">You have completed lesson1.</span><span class="sxs-lookup"><span data-stu-id="928df-198">You have completed lesson1.</span></span>  <span data-ttu-id="928df-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span><span class="sxs-lookup"><span data-stu-id="928df-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="928df-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span><span class="sxs-lookup"><span data-stu-id="928df-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="928df-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span><span class="sxs-lookup"><span data-stu-id="928df-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>

<span data-ttu-id="928df-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span><span class="sxs-lookup"><span data-stu-id="928df-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="928df-203">It comes some basic media functions like start, stop and pause.</span><span class="sxs-lookup"><span data-stu-id="928df-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="928df-204">In this lesson, you will add a slider bar control to the application.</span><span class="sxs-lookup"><span data-stu-id="928df-204">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="928df-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span><span class="sxs-lookup"><span data-stu-id="928df-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="928df-206">The slider start and end time also need to be updated in case of live content.</span><span class="sxs-lookup"><span data-stu-id="928df-206">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="928df-207">This can be better handled in the adaptive source update event.</span><span class="sxs-lookup"><span data-stu-id="928df-207">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="928df-208">Media sources are objects that generate media data.</span><span class="sxs-lookup"><span data-stu-id="928df-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="928df-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span><span class="sxs-lookup"><span data-stu-id="928df-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="928df-210">The source resolver is the standard way for the applications to create media sources.</span><span class="sxs-lookup"><span data-stu-id="928df-210">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="928df-211">This lesson contains the following procedures:</span><span class="sxs-lookup"><span data-stu-id="928df-211">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="928df-212">Register the Smooth Streaming handler</span><span class="sxs-lookup"><span data-stu-id="928df-212">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="928df-213">Add the adaptive source manager level event handlers</span><span class="sxs-lookup"><span data-stu-id="928df-213">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="928df-214">Add the adaptive source level event handlers</span><span class="sxs-lookup"><span data-stu-id="928df-214">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="928df-215">Add MediaElement event handlers</span><span class="sxs-lookup"><span data-stu-id="928df-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="928df-216">Add slider bar related code</span><span class="sxs-lookup"><span data-stu-id="928df-216">Add slider bar related code</span></span>
6. <span data-ttu-id="928df-217">Compile and test the application</span><span class="sxs-lookup"><span data-stu-id="928df-217">Compile and test the application</span></span>

<span data-ttu-id="928df-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span><span class="sxs-lookup"><span data-stu-id="928df-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="928df-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="928df-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="928df-220">At the beginning of the file, add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="928df-220">At the beginning of the file, add the following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="928df-221">At the beginning of the MainPage class, add the following data members:</span><span class="sxs-lookup"><span data-stu-id="928df-221">At the beginning of the MainPage class, add the following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="928df-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span><span class="sxs-lookup"><span data-stu-id="928df-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>

        // Gets the default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value to AdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="928df-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span><span class="sxs-lookup"><span data-stu-id="928df-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. <span data-ttu-id="928df-224">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="928df-224">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="928df-225">**To add the adaptive source manager level event handler**</span><span class="sxs-lookup"><span data-stu-id="928df-225">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="928df-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="928df-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="928df-227">Inside the **MainPage** class, add the following data member:</span><span class="sxs-lookup"><span data-stu-id="928df-227">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="928df-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="928df-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="928df-229">At the end of the **MainPage** class, add the following event handler:</span><span class="sxs-lookup"><span data-stu-id="928df-229">At the end of the **MainPage** class, add the following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="928df-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span><span class="sxs-lookup"><span data-stu-id="928df-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="928df-231">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="928df-231">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="928df-232">**To add adaptive source level event handlers**</span><span class="sxs-lookup"><span data-stu-id="928df-232">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="928df-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="928df-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="928df-234">Inside the **MainPage** class, add the following data member:</span><span class="sxs-lookup"><span data-stu-id="928df-234">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="928df-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="928df-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="928df-236">At the end of the **MainPage** class, add the following event handlers:</span><span class="sxs-lookup"><span data-stu-id="928df-236">At the end of the **MainPage** class, add the following event handlers:</span></span>

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. <span data-ttu-id="928df-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span><span class="sxs-lookup"><span data-stu-id="928df-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="928df-238">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="928df-238">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="928df-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span><span class="sxs-lookup"><span data-stu-id="928df-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="928df-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="928df-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="928df-241">**To add Media Element event handlers**</span><span class="sxs-lookup"><span data-stu-id="928df-241">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="928df-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="928df-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="928df-243">At the end of the **MainPage** class, add the following event handlers:</span><span class="sxs-lookup"><span data-stu-id="928df-243">At the end of the **MainPage** class, add the following event handlers:</span></span>

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. <span data-ttu-id="928df-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span><span class="sxs-lookup"><span data-stu-id="928df-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="928df-245">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="928df-245">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="928df-246">**To add slider bar related code**</span><span class="sxs-lookup"><span data-stu-id="928df-246">**To add slider bar related code**</span></span>

1. <span data-ttu-id="928df-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="928df-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="928df-248">At the beginning of the file, add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="928df-248">At the beginning of the file, add the following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="928df-249">Inside the **MainPage** class, add the following data members:</span><span class="sxs-lookup"><span data-stu-id="928df-249">Inside the **MainPage** class, add the following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="928df-250">At the end of the **MainPage** constructor, add the following code:</span><span class="sxs-lookup"><span data-stu-id="928df-250">At the end of the **MainPage** constructor, add the following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="928df-251">At the end of the **MainPage** class, add the following code:</span><span class="sxs-lookup"><span data-stu-id="928df-251">At the end of the **MainPage** class, add the following code:</span></span>

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

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
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
><span data-ttu-id="928df-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span><span class="sxs-lookup"><span data-stu-id="928df-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="928df-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span><span class="sxs-lookup"><span data-stu-id="928df-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="928df-254">For example:</span><span class="sxs-lookup"><span data-stu-id="928df-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="928df-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span><span class="sxs-lookup"><span data-stu-id="928df-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="928df-256">At the end of the **MediaOpened** method, add the following code:</span><span class="sxs-lookup"><span data-stu-id="928df-256">At the end of the **MediaOpened** method, add the following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="928df-257">Press **CTRL+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="928df-257">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="928df-258">**To compile and test the application**</span><span class="sxs-lookup"><span data-stu-id="928df-258">**To compile and test the application**</span></span>

1. <span data-ttu-id="928df-259">Press **F6** to compile the project.</span><span class="sxs-lookup"><span data-stu-id="928df-259">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="928df-260">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="928df-260">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="928df-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span><span class="sxs-lookup"><span data-stu-id="928df-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="928df-262">Click **Set Source**.</span><span class="sxs-lookup"><span data-stu-id="928df-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="928df-263">Test the slider bar.</span><span class="sxs-lookup"><span data-stu-id="928df-263">Test the slider bar.</span></span>

<span data-ttu-id="928df-264">You have completed lesson 2.</span><span class="sxs-lookup"><span data-stu-id="928df-264">You have completed lesson 2.</span></span>  <span data-ttu-id="928df-265">In this lesson you added a slider to application.</span><span class="sxs-lookup"><span data-stu-id="928df-265">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="928df-266">Lesson 3: Select Smooth Streaming Streams</span><span class="sxs-lookup"><span data-stu-id="928df-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="928df-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span><span class="sxs-lookup"><span data-stu-id="928df-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="928df-268">In this lesson, you will enable viewers to select streams.</span><span class="sxs-lookup"><span data-stu-id="928df-268">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="928df-269">This lesson contains the following procedures:</span><span class="sxs-lookup"><span data-stu-id="928df-269">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="928df-270">Modify the XAML file</span><span class="sxs-lookup"><span data-stu-id="928df-270">Modify the XAML file</span></span>
2. <span data-ttu-id="928df-271">Modify the code behand file</span><span class="sxs-lookup"><span data-stu-id="928df-271">Modify the code behand file</span></span>
3. <span data-ttu-id="928df-272">Compile and test the application</span><span class="sxs-lookup"><span data-stu-id="928df-272">Compile and test the application</span></span>

<span data-ttu-id="928df-273">**To modify the XAML file**</span><span class="sxs-lookup"><span data-stu-id="928df-273">**To modify the XAML file**</span></span>

1. <span data-ttu-id="928df-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span><span class="sxs-lookup"><span data-stu-id="928df-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="928df-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span><span class="sxs-lookup"><span data-stu-id="928df-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="928df-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span><span class="sxs-lookup"><span data-stu-id="928df-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="928df-277">Press **CTRL+S** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="928df-277">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="928df-278">**To modify the code behind file**</span><span class="sxs-lookup"><span data-stu-id="928df-278">**To modify the code behind file**</span></span>

1. <span data-ttu-id="928df-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="928df-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="928df-280">Inside the SSPlayer namespace, add a new class:</span><span class="sxs-lookup"><span data-stu-id="928df-280">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="928df-281">At the beginning of the MainPage class, add the following variable definitions:</span><span class="sxs-lookup"><span data-stu-id="928df-281">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="928df-282">Inside the MainPage class, add the following region:</span><span class="sxs-lookup"><span data-stu-id="928df-282">Inside the MainPage class, add the following region:</span></span>
   
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
5. <span data-ttu-id="928df-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span><span class="sxs-lookup"><span data-stu-id="928df-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="928df-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span><span class="sxs-lookup"><span data-stu-id="928df-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="928df-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span><span class="sxs-lookup"><span data-stu-id="928df-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="928df-286">**To compile and test the application**</span><span class="sxs-lookup"><span data-stu-id="928df-286">**To compile and test the application**</span></span>

1. <span data-ttu-id="928df-287">Press **F6** to compile the project.</span><span class="sxs-lookup"><span data-stu-id="928df-287">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="928df-288">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="928df-288">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="928df-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span><span class="sxs-lookup"><span data-stu-id="928df-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="928df-290">Click **Set Source**.</span><span class="sxs-lookup"><span data-stu-id="928df-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="928df-291">The default language is audio_eng.</span><span class="sxs-lookup"><span data-stu-id="928df-291">The default language is audio_eng.</span></span> <span data-ttu-id="928df-292">Try to switch between audio_eng and audio_es.</span><span class="sxs-lookup"><span data-stu-id="928df-292">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="928df-293">Everytime, you select a new stream, you must click the Submit button.</span><span class="sxs-lookup"><span data-stu-id="928df-293">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="928df-294">You have completed lesson 3.</span><span class="sxs-lookup"><span data-stu-id="928df-294">You have completed lesson 3.</span></span>  <span data-ttu-id="928df-295">In this lesson, you add the functionality to choose streams.</span><span class="sxs-lookup"><span data-stu-id="928df-295">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="928df-296">Lesson 4: Select Smooth Streaming Tracks</span><span class="sxs-lookup"><span data-stu-id="928df-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="928df-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span><span class="sxs-lookup"><span data-stu-id="928df-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="928df-298">In this lesson, you will enable users to select tracks.</span><span class="sxs-lookup"><span data-stu-id="928df-298">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="928df-299">This lesson contains the following procedures:</span><span class="sxs-lookup"><span data-stu-id="928df-299">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="928df-300">Modify the XAML file</span><span class="sxs-lookup"><span data-stu-id="928df-300">Modify the XAML file</span></span>
2. <span data-ttu-id="928df-301">Modify the code behand file</span><span class="sxs-lookup"><span data-stu-id="928df-301">Modify the code behand file</span></span>
3. <span data-ttu-id="928df-302">Compile and test the application</span><span class="sxs-lookup"><span data-stu-id="928df-302">Compile and test the application</span></span>

<span data-ttu-id="928df-303">**To modify the XAML file**</span><span class="sxs-lookup"><span data-stu-id="928df-303">**To modify the XAML file**</span></span>

1. <span data-ttu-id="928df-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span><span class="sxs-lookup"><span data-stu-id="928df-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="928df-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span><span class="sxs-lookup"><span data-stu-id="928df-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
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
3. <span data-ttu-id="928df-306">Press **CTRL+S** to save he changes</span><span class="sxs-lookup"><span data-stu-id="928df-306">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="928df-307">**To modify the code behind file**</span><span class="sxs-lookup"><span data-stu-id="928df-307">**To modify the code behind file**</span></span>

1. <span data-ttu-id="928df-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span><span class="sxs-lookup"><span data-stu-id="928df-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="928df-309">Inside the SSPlayer namespace, add a new class:</span><span class="sxs-lookup"><span data-stu-id="928df-309">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="928df-310">At the beginning of the MainPage class, add the following variable definitions:</span><span class="sxs-lookup"><span data-stu-id="928df-310">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="928df-311">Inside the MainPage class, add the following region:</span><span class="sxs-lookup"><span data-stu-id="928df-311">Inside the MainPage class, add the following region:</span></span>
   
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
5. <span data-ttu-id="928df-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span><span class="sxs-lookup"><span data-stu-id="928df-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="928df-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span><span class="sxs-lookup"><span data-stu-id="928df-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on the presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="928df-314">**To compile and test the application**</span><span class="sxs-lookup"><span data-stu-id="928df-314">**To compile and test the application**</span></span>

1. <span data-ttu-id="928df-315">Press **F6** to compile the project.</span><span class="sxs-lookup"><span data-stu-id="928df-315">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="928df-316">Press **F5** to run the application.</span><span class="sxs-lookup"><span data-stu-id="928df-316">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="928df-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span><span class="sxs-lookup"><span data-stu-id="928df-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="928df-318">Click **Set Source**.</span><span class="sxs-lookup"><span data-stu-id="928df-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="928df-319">By default, all of the tracks of the video stream are selected.</span><span class="sxs-lookup"><span data-stu-id="928df-319">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="928df-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span><span class="sxs-lookup"><span data-stu-id="928df-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="928df-321">You must click Submit after each change.</span><span class="sxs-lookup"><span data-stu-id="928df-321">You must click Submit after each change.</span></span>  <span data-ttu-id="928df-322">You can see the video quality changes.</span><span class="sxs-lookup"><span data-stu-id="928df-322">You can see the video quality changes.</span></span>

<span data-ttu-id="928df-323">You have completed lesson 4.</span><span class="sxs-lookup"><span data-stu-id="928df-323">You have completed lesson 4.</span></span>  <span data-ttu-id="928df-324">In this lesson, you add the functionality to choose tracks.</span><span class="sxs-lookup"><span data-stu-id="928df-324">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="928df-325">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="928df-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="928df-326">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="928df-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="928df-327">Other Resources:</span><span class="sxs-lookup"><span data-stu-id="928df-327">Other Resources:</span></span>
* [<span data-ttu-id="928df-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span><span class="sxs-lookup"><span data-stu-id="928df-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="928df-329">Smooth Streaming Technical Overview</span><span class="sxs-lookup"><span data-stu-id="928df-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

