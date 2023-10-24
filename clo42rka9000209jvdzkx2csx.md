---
title: "Accelerating File Sharing and Data Replication with AWS FSx: A Comprehensive Guide for beginners"
datePublished: Tue Oct 24 2023 08:38:52 GMT+0000 (Coordinated Universal Time)
cuid: clo42rka9000209jvdzkx2csx
slug: accelerating-file-sharing-and-data-replication-with-aws-fsx-a-comprehensive-guide-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698136039818/ffb98c25-c508-42ce-aa92-61466a4acf13.jpeg
tags: aws, ec2-instance, fsx, fsx-for-lustre, fsx-for-windows

---

In today's fast-paced business environment, the need for faster file sharing and efficient data replication has become paramount. Companies are continually looking for ways to streamline these processes and make them more robust. One solution that stands out in this regard is Amazon Web Services (AWS) FSx, a managed file storage service that offers two powerful file systems, Windows File Server and Lustre. In this blog post, we'll look into the process of setting up these file systems to meet your organization's requirements for faster file sharing and data replication.

### Section 1: Creating an FSx File System for Windows File Server

It is a fully managed Windows file system that is accessible from both Windows and Linux instances. Here's how you can create this file system:

1. Log in to the AWS Management Console.
    
2. Navigate to the FSx service and click on "Create file system".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698124719681/cc05747d-7c71-458a-884f-621f5b251754.png align="center")
    
3. Choose "Windows file server" as the file system type.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698124890373/c717f2f0-662c-44ba-a16e-896712774988.png align="center")
    
4. Configure the storage capacity, network settings, and other options according to your needs. For the sake of this demo, I'm choosing the default values for VPC & Subnet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698125131317/f3640dcc-9f74-4c1b-aa42-cc0b8a58d18d.png align="center")
    
    *Note here that the minimum SSD capacity required for FSx windows is 32 GiB.*
    
5. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698125204251/8c151708-799f-4f94-959b-3f66ea702e16.png align="center")
    
    To proceed further, you need to ensure that you have AWS Managed Active Directory with a valid domain name. AWS Managed <mark>Active Directory</mark> is a managed Microsoft Active Directory service provided by AWS. It's a crucial component for integrating with your Windows FSx file system. We don’t have any Active Directory, so let’s create one.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698125616866/5d8abc3b-8aec-41aa-9272-d20b2ec12ee2.png align="center")
    
    Click on Create a new directory.
    
6. Keep AWS Managed Microsoft AD and Click on Next.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698125780261/5fbd6e4a-16aa-4773-8ead-e981682527cd.png align="center")
    
7. Select the standard edition.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698125881199/c5240454-e83e-4811-a8d1-851f6136aeaa.png align="center")
    
8. Enter your domain name and a short name for the domain name. Then enter a password for the admin user and click on Next.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698125988574/366f1c1c-7ab6-43e1-834e-dc302eea5181.png align="center")
    
9. Choose the default values for networking.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698126570479/717bb125-c539-4fb2-9d3b-7c28b5df8c6f.png align="center")
    
10. Review the settings and click on Create Directory.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698126992874/689839e4-58de-4dec-9f7b-f4e333244146.png align="center")
    
11. It’ll take some time to create the Active Directory.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698127049798/adc200fc-4247-44e3-9b8c-577c1d01e7e5.png align="center")
    
12. Now, we'll go back to the FSx creation. Select the Active Directory that we created just now.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698136368080/6b5b4e0b-ace1-489a-b30b-1df381fd8e82.png align="center")
    
    Keep the default values for other options and click on Next.
    
13. Review the settings.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698136578265/b86cecbc-1ffa-4917-a299-17108fa16fc0.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698127387802/f8f6e740-0061-4b8a-ad46-5f0268ce8d9a.png align="center")
    
    Click on Create file system.
    
14. The file system is being created and it'll take some time.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698136447134/ef9df3d7-43ab-4309-a23a-484543c26634.png align="center")
    
    Also, We'll go and check if our directory is active.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698136498320/3141ccf0-965c-4bad-9680-e22e8279aa60.png align="center")
    
    Now our directory is active.
    
15. Our file system is getting created. Meanwhile, we’ll create an EC2 instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698131324998/4ca54afb-bda5-4c66-a602-177391268eda.png align="center")

1. EC2 instance is created. In security groups, we’ll add the following to the inbound rules,
    
      RDP - to allow access to the Windows instance and
    
      SMB – to allow access to the FSx file system.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698131439104/38355119-a2b8-49f0-8f59-7d5b4c3111e0.png align="center")

1. Use the RDP application in Windows to access the Windows EC2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698131612175/3aee73bb-082a-4a15-acb6-dc08b5d0e460.png align="center")
    
    Successfully connected to our Windows instance.
    
2. Now, to access the FSx file system,
    
    •Change the DNS address in the network settings.
    
    •Add this instance to our Active directory domain.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698131824849/dbe4b7f1-f547-4725-a803-3d99c0b24857.png align="center")
    
    Copy these addresses to the Windows EC2 DNS settings.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698131899413/c3b92bf5-005b-4e2d-8e7c-4c0fd6e51975.png align="center")
    
3. Go to the System properties, and add it to the domain.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698132191803/d4b050d3-8630-4323-b076-bcc3ebd565c3.png align="center")
    
    The instance is successfully connected to the domain. Now, restart the PC to apply these changes.
    
4. After rebooting the instance, go to the FSx file system and Click on attach.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698132351422/3e39de80-4de1-4b67-872a-ada9d599e244.png align="center")
    
5. Open the command prompt and execute this command.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698132462007/0083eb29-f8d4-41e4-832d-62e4fabd17a0.png align="center")
    
6. ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698132616194/e8682f9e-a248-48f1-8bb4-48c36dbb2b82.png align="center")
    
    The command is successfully executed and the file system is visible under network locations. You can now access the files on the FSx file system as the normal disk. We'll now see how to create an FSx file system for Lustre.
    

### Section 2: Creating an FSx File System for Lustre

1. Navigate to the FSx service as shown in step 2 of the previous section and click on "Create file system".
    
2. Choose Amazon FSx for Lustre.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133086163/9c0a406c-4cef-44a3-824f-02846589d2ef.png align="center")
    
3. Enter the basic details. Please note that Lustre requires at least 1.2 TiB or storage capacity. For the sake of this demo, I'm creating a size of 1.2 TiB. You can choose a greater value.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133158922/d52e0fd3-80cf-4667-81df-a52c6933f07f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133420318/0afba009-854b-4b59-b4dd-9896a2fff87b.png align="center")
    
    **Add port numbers 988 and 1018 - 1023 as custom ports in the inbound rules of this security group to allow access to Lustre.**
    
4. Keep the default values for the remaining options and click on Next.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133501103/3dcbe17d-8afa-4045-9cd6-b77a8bd0ab3d.png align="center")
    
5. Review the settings and click on Create.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133599253/2ebdf79c-faf0-4a68-9c7d-cbed7b950794.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133612744/d0e8c68b-a17c-4274-a2e1-961157fb9bd3.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133641123/dcab7004-5971-4d98-bb3c-56322ec82087.png align="center")
    
6. The file system is getting created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133762721/7ed3b9ae-46af-4e83-9730-813ca94a6ec4.png align="center")
    
    The Lusture File system is ready for use.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698133867054/854022e7-67a1-4709-b6a1-eb2668d65cd7.png align="center")
    
7. Now, we’ll create an Amazon Linux 2 EC2 instance to attach this file system.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698134045435/46ed3533-f074-44eb-831b-b1136657741f.png align="center")
    
    Amazon Linux 2 EC2 instance was created. We’ll connect to it.
    
8. Click on Attach.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698134123991/42c3e626-fcf3-42d4-b510-109c3c3318ec.png align="center")
    
    Go to the EC2 instance and follow these steps to continue.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698134212885/2c9ec426-6763-498d-9dbe-c647ddf007d8.png align="center")
    

The file system is attached successfully.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698134294308/95768188-e80e-4998-8c7f-ec1700f1550d.png align="center")

You can start utilizing it for your data-intensive tasks.

---

By following these steps, you can successfully set up FSx file systems to accelerate file sharing and data replication in your organization. AWS's managed file storage services, Windows File Server and Lustre, provide you with the robust solutions you need to meet the demands of today's data-driven world. With AWS FSx, you'll be able to ensure efficient, high-speed data handling, and enable your organization to thrive in the digital age.

Remember, AWS's extensive documentation and support resources are always available to assist you in case you encounter any issues during this setup process. Happy file sharing and data replication!