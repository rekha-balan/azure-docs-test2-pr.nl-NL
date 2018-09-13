<span data-ttu-id="8d484-101">You can verify that your connection succeeded by using the **Get-AzureRmVirtualNetworkGatewayConnection** cmdlet, with or without **-Debug**.</span><span class="sxs-lookup"><span data-stu-id="8d484-101">You can verify that your connection succeeded by using the **Get-AzureRmVirtualNetworkGatewayConnection** cmdlet, with or without **-Debug**.</span></span> 

1. <span data-ttu-id="8d484-102">Use the following cmdlet example, configuring the values to match your own.</span><span class="sxs-lookup"><span data-stu-id="8d484-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="8d484-103">If prompted, select 'A' in order to run 'All'.</span><span class="sxs-lookup"><span data-stu-id="8d484-103">If prompted, select 'A' in order to run 'All'.</span></span> <span data-ttu-id="8d484-104">In the example, **-Name** refers to the name of the connection that you created and want to test.</span><span class="sxs-lookup"><span data-stu-id="8d484-104">In the example, **-Name** refers to the name of the connection that you created and want to test.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="8d484-105">After the cmdlet has finished, view the values.</span><span class="sxs-lookup"><span data-stu-id="8d484-105">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="8d484-106">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span><span class="sxs-lookup"><span data-stu-id="8d484-106">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```
  