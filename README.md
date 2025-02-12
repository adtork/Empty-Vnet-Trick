# Empty-Vnet-Trick

# Intro
This article explains a quick hack and trick in order to advertise an address space to a remote branch in order to make it reachable on both sides. In the below topology, on-premise has no idea how to reach the Spoke2 Vnet, and this cannot be solved with static routes etc. If we use remote gateway on the hub vnet and allow gateway transit, on-prem can reach Spoke1, but it cannot reach Spoke2, since it's an indirect spoke!. This can be solved by vnet peering a "dummy vnet" to the hub vnet, with the same address space as Spoke2 and using a NVA or AzFW in Spoke1 to make all sides reachable. Here is the simple architecture below!

> [!NOTE]
> This should not be used at scale and is something that can be done in a pinch to get the routes advertised! Ideally, the better option is to have an NVA/VM that supports BGP, and then you can BGP peer with Azure Route Server in Spoke1 or Spoke2 and use that to inject (advertise) the 10.2.0.0/16 down to the remote branch!

# Simple Topology
![image](https://github.com/user-attachments/assets/174814cf-f494-4e99-a723-323ae6af4431)
