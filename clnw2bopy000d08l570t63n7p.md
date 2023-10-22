---
title: "Deploying and Resizing EBS Volumes on AWS: A Step-by-Step Guide for beginners"
seoTitle: "Deploying and Resizing EBS Volumes on AWS: A Step-by-Step Guide"
seoDescription: "Deploying and Resizing EBS Volumes on AWS: A Step-by-Step Guide for beginners"
datePublished: Wed Oct 18 2023 18:04:21 GMT+0000 (Coordinated Universal Time)
cuid: clnw2bopy000d08l570t63n7p
slug: deploying-and-resizing-ebs-volumes-on-aws-a-step-by-step-guide-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697652181160/586d36a9-18ed-4884-a67d-e4f584532af7.jpeg
tags: aws, ebs, aws-ebs, aws-ebs-introduction, aws-ebs-beginners

---

In the fast-paced world of cloud computing, AWS has emerged as a dominant force, offering a wide array of services and tools to cater to the ever-evolving needs of businesses. One such crucial feature is Elastic Block Store (EBS) volumes, which allow you to attach additional storage to your Amazon EC2 instances.

In this blog post, I'll walk you through the process of launching a Linux EC2 instance, creating an EBS volume (let's say 20 GiB), and resizing it (let's say 30 GiB).

### **Task 1: Launch a Linux EC2 Instance**

1. Log in to the AWS console and Click on EC2.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697644199842/54b27df8-a1a8-4af8-942b-2f042f5919be.png align="center")
    
2. There are no running instances. We’ll launch one. Click the **Launch Instance** button to start the EC2 instance creation process.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697644377176/6e7baa19-27be-40a2-b149-97ead577b519.png align="center")
    
3. Enter a name for the instance
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697644526843/19def079-829f-4349-8a9a-83aaedcdf210.png align="center")
    
4. Select the Linux AMI that best suits your needs. For example, you might choose "Amazon Linux 2" or "Ubuntu Server." I'm choosing Amazon Linux OS from the suggestions.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697644596417/2fbcf0bf-5d6e-4d1e-962f-19ca54a1fc0d.png align="center")
    
5. Select the instance type that matches your requirements in terms of CPU, memory, and other resources. You can choose the free tier-eligible options or scale up for more power. I keep the default instance type (t2.micro)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697644764423/5ab7be7a-343e-494b-8d0b-caf1a0f0297a.png align="center")
    
6. Select one of the key pairs from the suggestions.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697645434212/ca8a9644-99f3-4ca8-9d2a-f32dc18cb794.png align="center")
    
    Create a new one if no key pair is created for the current region.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697645495997/5feb2020-e80e-4c77-bcf9-d6a32b14eea4.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697645527314/cf29d238-c1d4-4cf7-93b8-e0e91dd0961f.png align="center")
    
    Click on Create key pair and download the .pem file. Later, we’ll use PuTTYgen to create a .ppk file to access the EC2 instance.
    
7. In the network settings, select the check boxes corresponding to SSH and HTTP Traffic.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697645779685/fd606aef-f035-47c3-a150-8cc2fe2de5e6.png align="center")
    
8. Configure the amount of storage you want for your instance. The default 8 GB of gp2 volume should be enough for a basic web server.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697645856907/30bf9ffb-bbee-4904-b374-954fdedcff82.png align="center")
    
9. Review the summary of the EC2 instance and click on the Launch Instance. It’ll take a moment to initiate the instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697645917269/b6a9d90f-5901-4c7d-a8d2-40fb107c47bb.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697645987800/5dbb7f9e-88ad-4c51-afb8-186391e51494.png align="center")
    
10. The newly created instance is launched in the availability zone in the US-East-1 Region. We’ll now open PuTTY & copy this Public IP to access the instance from PuTTY.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646236745/fd68dc16-9aa4-479d-ba20-62c7867e5bce.png align="center")
    
11. Open PuTTY & paste the copied Public IP in the Host Name (or IP address).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646309826/13bfa320-c319-483d-bae4-989a247fa9f0.png align="center")
    
12. Then go to, Connection -&gt; SSH -&gt; Auth -&gt; Credentials.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646365689/a839a4c5-d53a-4764-99df-4de9bbcd004c.png align="center")
    
    Now we need a putty private key file for authentication to access the instance. So we’ll now open PuTTYgen & generate the .ppk file from the .pem file.
    
    **<mark>Generating .ppk from .pem:</mark>**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646609242/7024a0c1-15b3-49e3-b676-330a8e329a9d.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646679926/be20a92e-f274-49e3-8943-ceaaec143605.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646716767/488f30b5-8052-440d-bea2-ac7dfc24ed89.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646747741/16de0141-4850-4125-a59f-54e9ab736a84.png align="center")
    
13. Select the generated .ppk file and then click on Open.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646821911/afc339b2-9a74-43b1-8adf-098560e08edd.png align="center")
    
14. It is successfully connected to the instance. Click on Accept.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697646939719/0a9ae031-4f2d-4037-89e8-83e0a20a6659.png align="center")
    
    Enter **ec2-user** to log in to the instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697647008279/d42428f4-9d3c-4ceb-b3b9-508b56274f99.png align="center")
    
    The instance is ready for use.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697647176041/9d5a2963-612d-448c-9745-58319e7f48be.png align="center")

---

### **Task 2: Create an EBS Volume and Attach It to the instance**

1. Now we’ll create an EBS volume with 20 GB of storage and attach it to the created EC2 instance. In this same EC2 page, scroll down to Elastic Block Store (EBS) and click on Volumes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697647431381/070aff36-2fed-4f64-8bd7-40e1c9fecf81.png align="center")
    
    Currently, it is showing the Root Volume Device of the instance launched in the previous task. Click on Create Volume.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697647570439/8f65330e-6c44-4124-ada6-4fcd50738901.png align="center")
    
2. Enter 20 GiB for the size and select the availability zone that our current instance is running from.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697647665890/51e01ffc-688e-4198-80d6-60f4885d3dad.png align="center")
    
    Keep the remaining options as it is and click on Create Volume.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697647731086/c537a3a2-58b4-4989-a2e3-083e0c6eaa5f.png align="center")
    
3. Volume is successfully created and is available for us to use.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697647823434/ac044fc8-0284-42b3-883b-93161168a982.png align="center")
    
4. Now, we’ll attach this volume to our instance. Go to Actions -&gt; Attach Volume
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697647892671/4e4a553e-ff48-4417-ad56-1d84e32c21bc.png align="center")
    
5. Select the instance to which we want to attach our newly created volume and click on attach volume.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697648020509/913faf44-1aa4-462e-b538-5f9569a666d7.png align="center")
    
6. Volume is successfully attached to our instance. Now we’ll go to our instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697648126778/cc8cb663-589c-4cd5-a67f-5accafa31a03.png align="center")
    
7. Type **lsblk** and see the available volumes and we can see that there is no mount point for **xvdf**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697648236191/3fd77d67-727e-4f16-abea-79f331774f78.png align="center")
    

<details data-node-type="hn-details-summary"><summary>LSBLK command</summary><div data-type="detailsContent">It lists information about all available or specified block devices. It reads the sysfs filesystem and udev db to gather the information.</div></details>

1. We'll run the **file** command. It detected the device **xvda** as a volume of root partition and **xvdf** as just data.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697648497826/2f3c78a0-c232-4df3-8591-6b7870e2479a.png align="center")

The output of the file command is different for both volumes (**xvda** & **xvdf**). So, we’ll make xvdf a file system.

<details data-node-type="hn-details-summary"><summary>FILE command</summary><div data-type="detailsContent">It determines the file type.</div></details>

1. Use **mkfs** to create a filesystem.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697648690599/a9735666-83d6-404f-9c8d-b24351cd598c.png align="center")
    
    <details data-node-type="hn-details-summary"><summary>The mkfs command</summary><div data-type="detailsContent">It builds a Linux filesystem on a device, usually a hard disk partition.</div></details>
2. We’ll make a new directory named **ebs** (mkdir ebs) and mount this file system.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697648824173/a906def0-9bcf-40c2-a659-f165c367e121.png align="center")
    
    Now, there is a mount point for **xvdf**.
    
    <details data-node-type="hn-details-summary"><summary>The mount command</summary><div data-type="detailsContent">It serves to attach the filesystem found on some devices to the big file tree.</div></details>

Go to the newly created directory **ebs** and create a new text file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697649026206/87f54f41-7bf6-4c55-a16f-17210922dff9.png align="center")

 1.txt is created. Now we have a new EBS volume attached to our EC2 instance.

---

### **Step 3: Resize the Attached Volume** and make sure it reflects in the connected instance

1. Go to AWS Console -&gt; EC2 -&gt; Elastic Block Storage -&gt; Volumes -&gt; Modify Volume. Change the size from 20 GiB to 30 GiB and click on Modify.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697649420800/7a8a243b-4187-4c4b-addb-77e73938d11b.png align="center")
    
2. Click on Modify.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697649481832/ee9ed9ae-6087-4ab2-8364-178eba9e5859.png align="center")
    
3. Modification is in progress and the size is still 20 GiB.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697649537704/bf91da4f-8414-430b-8637-3c29bc9e56ed.png align="center")
    
    After modification, the size is changed to 30 GiB.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697649596073/4d643d3d-24d1-4580-924a-e01d3133f209.png align="center")
    
4. Now, we’ll check the device information. Here **lsblk** is showing 30 GiB but **df** is still showing 20 GiB.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697649710908/598d6fdb-c6ac-41ab-aa90-b99ef3593f01.png align="center")
    
    <details data-node-type="hn-details-summary"><summary>The df command</summary><div data-type="detailsContent">It displays the amount of disk space available on the file system containing each file name argument.</div></details>
5. We’ll use the **resize2fs** command to reflect the changes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697649840031/638d1207-52fc-4d15-8ace-2962f385b623.png align="center")
    
    Now **df** is showing 30 GiB and we can also see the 1.txt that was created in the previous step.
    
    <details data-node-type="hn-details-summary"><summary>The resize2fs program</summary><div data-type="detailsContent">It will resize&nbsp;ext2,&nbsp;ext3 or ext4 file systems. It can be used to enlarge or shrink an unmounted file system located on a device. If the file system is mounted, it can be used to expand the size of the mounted file system, assuming the kernel and the file system support online resizing.</div></details>

---

And that's it! We've successfully launched a Linux EC2 instance, attached an EBS volume, and resized it to meet our requirements.

**Conclusion:**  
AWS provides a powerful and flexible platform for cloud computing, and understanding how to work with resources like EC2 instances and EBS volumes is essential for any AWS user. In this blog post, I've walked you through the process of launching an EC2 instance, creating an EBS volume, and resizing it when needed. With this knowledge, you can confidently deploy and manage resources in your AWS environment, ensuring that your infrastructure is always in line with your evolving requirements.