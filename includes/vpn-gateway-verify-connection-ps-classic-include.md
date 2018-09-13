<span data-ttu-id="feaa2-101">You can use the **Get-AzureVNetConnection** to verify the connection for a classic virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="feaa2-101">You can use the **Get-AzureVNetConnection** to verify the connection for a classic virtual network gateway.</span></span> 

1. <span data-ttu-id="feaa2-102">Use the following cmdlet example, configuring the values to match your own.</span><span class="sxs-lookup"><span data-stu-id="feaa2-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="feaa2-103">The name of the virtual network must be in quotes if it contains spaces.</span><span class="sxs-lookup"><span data-stu-id="feaa2-103">The name of the virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="feaa2-104">After the cmdlet has finished, view the values.</span><span class="sxs-lookup"><span data-stu-id="feaa2-104">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="feaa2-105">In the example below, the Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span><span class="sxs-lookup"><span data-stu-id="feaa2-105">In the example below, the Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : The connectivity state for the local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal
