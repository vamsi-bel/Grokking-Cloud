---
title: "Streamlining VPC Connectivity with AWS Transit Gateway"
seoTitle: "Streamlining VPC Connectivity with AWS Transit Gateway"
seoDescription: "Hands-on tutorial on Streamlining VPC Connectivity with AWS Transit Gateway"
datePublished: Sat Apr 06 2024 20:00:23 GMT+0000 (Coordinated Universal Time)
cuid: cluoirkna000r08jv4uyp3nfk
slug: streamlining-vpc-connectivity-with-aws-transit-gateway
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712433569274/0cb1be85-693a-45c5-a4d4-a78c823505c0.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1712433518396/7b17fc35-3486-4725-a58d-b35a917ecf1f.png
tags: aws, aws-vpc, aws-transit-gateway

---

### **Introduction:**

Efficient networking solutions are vital for seamless communication between services and resources in cloud environments. Amazon Web Services (AWS) offers AWS Transit Gateway, a scalable and centralized solution for connecting multiple Virtual Private Clouds (VPCs) and on-premises networks. In this article, we'll explore how to set up and utilize AWS **Transit Gateway** (TGW) to establish connectivity between multiple VPCs within the same region, eliminating the time-consuming process of manually accepting peering connections.

We'll understand this in 5 steps.

### **Step 1:Provisioning VPCs**

Begin by creating four VPCs within any region. For this lab, I've selected Singapore region. Ensure that each VPC has a unique CIDR block assigned to it, and also allocate a common CIDR block to all the VPCs. This setup ensures that there is no overlapping CIDR and allows for seamless communication within the VPCs.

CIDRs for each VPC:  
VPC-A - 10.0.0.0/24  
VPC-B - 10.1.0.0/24  
VPC-C - 10.2.0.0/24  
VPC-D - 10.3.0.0/24  
Common CIDR - 10.0.0.0/8

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712427585715/d0e1983e-b505-4b7d-9b08-0ac8d465a15e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712468031886/7852086c-e125-4e57-ad36-8777343f7333.png align="center")

Select **None** for VPC endpoints, keep the other settings as it is and Click on Create VPC. It create our first VPC (VPC-A). Similarly create the other 3 VPCs (VPC-B, VPC-C and VPC-D).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712427932859/d89785a4-097e-45e1-836c-ce7cec501dbf.png align="center")

### **Step 2: Setting up AWS Transit Gateway**

Next, create an AWS Transit Gateway in the Singapore region. Provide a name and description for the Transit Gateway, and leave all other options as default. This Transit Gateway will serve as the central hub for routing traffic between the VPCs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712428637992/e5ff11a2-9757-44dc-b968-3f6f583c2bb9.png align="center")

I named it as MyTGW and the same is given as Description. Keep the default settings and click on Create.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712428759438/ef263021-4cf4-4117-9482-8564b8091fd0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712428901491/c37b178e-ef50-48aa-8efe-aef7148abd60.png align="center")

This will take some time to create the TGW.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712428958233/77165e8e-dadf-4b5b-a7d7-0ee65a5b7c21.png align="center")

The state is changed to Available. Now we'll go to **transit gateway attachments** and create attachments.

### **Step 3: Creating Transit Gateway Attachments**

Once the TGW is set up, create TGW attachments for each VPC. Specify the TGW ID and choose the attachment type as "VPC." Select the respective VPC and subnets for each attachment. This establishes the connectivity between the TGW and the VPCs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712429084645/1db06afd-ed63-469a-bebc-c8b2f2330e87.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712429247035/9a67ff76-b109-4779-9960-c18e1214a387.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712429294749/c45bb9f2-92a5-4b25-a5f1-c9d511d9085a.png align="center")

We've to do this step carefully. I chose VPC-A. For this, we need to select the 2 subnets of explicit association. In my case one subnet is ending with 497 and another with 0df.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712429601936/dbdceb12-30bf-48c8-8261-3867373398c9.png align="center")

Similarly do association for the other VPCs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712429848190/5bde92af-ee59-443a-9f17-f78af4404274.png align="center")

Wait until the state for all the attachments is changed to **Available**. Meanwhile, configure the route entries.

### **Step 4: Configuring Route Entries**

Now, configure route entries in the route tables associated with the VPC subnets. Add a route entry for the common CIDR block (10.0.0.0/8) with the TGW as the target. This ensures that traffic destined for the common CIDR block is routed through the TGW.

We'll now go to Route Tables, and select those Route Tables where there are 2 explicit subnet associations are present as shown below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712428189814/55b75911-b169-4615-8174-c33a9ddde399.png align="center")

I've renamed them as RT for TGW. For each of this RT, we've to add a route to the TGW to route the traffic.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712430209084/0ac5fc8d-5e2e-48a0-b5ec-5a87f50bb3ad.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712430307614/6ce18abb-d7fb-42ab-93fe-7e3035ea0426.png align="center")

Click on Add route -&gt; Enter the common CIDR in the destination field, select the transit gateway and save it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712430388899/73fff06f-c9a7-4f29-a46b-188080083fec.png align="center")

Route is added. Similarly, repeat this process for the remaining 3 RTs.

### **Step 5: Testing Connectivity**

To test the setup, launch EC2 instances in two different VPCs. Ensure that the instances are launched in subnets associated with the route tables containing the Transit Gateway route entry. Attempt to communicate between the EC2 instances using their private IP addresses. For this test purpose, I'll create a Windows EC2 instance in VPC-A and an Amazon Linux EC2 in VPC-D. Let's test this.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712430787616/b9e58989-1398-4bf5-8fc6-bc7aeb2ad560.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712430929518/9530adfe-5fab-4588-b5f6-eb0ae8d1ad00.png align="center")

First let's connect to Windows EC2 using RDP. From Windows, we'll connect to Linux via SSH using MobaXterm.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712431630099/1108a9ca-de08-47fb-997c-4ab1cf9e9bf8.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712431645852/ba030719-a752-4d81-a1dc-c67174b674fc.png align="center")

Successful communication indicates that the Transit Gateway is functioning correctly.  
This communication is no longer possible, If we delete the TGW.

### **Step 6: Cleanup**

After testing, clean up the resources in the following order  
1\. Delete the Transit Gateway attachments,  
2\. Delete the Transit Gateway, and  
3\. Delete the routes explicitly added in the RTs.

Verify that connectivity is disrupted after cleanup, ensuring that resources are no longer accessible across VPCs. Finally, Terminate the EC2 instances.

### **Conclusion:**

AWS Transit Gateway offers a scalable and efficient solution for interconnecting multiple VPCs within the same region. By following the steps outlined in this article, users can establish a robust network architecture that enables seamless communication between VPCs while maintaining security and scalability. Embracing AWS Transit Gateway empowers organizations to streamline their networking infrastructure and drive innovation in the cloud computing space.