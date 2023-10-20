---
title: "Deploying Web Servers with AWS EC2: 
A Step-by-Step Guide for beginners"
seoTitle: "Deploying Web Servers with AWS EC2: A Step-by-Step Guide for beginners"
datePublished: Mon Oct 16 2023 16:29:58 GMT+0000 (Coordinated Universal Time)
cuid: clnt42lrh000009l4a1hrbayu
slug: deploying-web-servers-with-aws-ec2-a-step-by-step-guide-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697574783138/8928a3c3-104a-4e3c-89b9-3f00f666c9da.png
tags: aws, websever-nginix-aws, ec2-instance

---

In today's digital age, businesses are increasingly relying on cloud services to power their applications, websites, and more. Amazon Web Services (AWS) is a frontrunner in the cloud computing space, offering a plethora of services and features to cater to various needs. If you're looking to launch a new web-based application, AWS Virtual Machines (EC2), provides a flexible and scalable platform to get you started.

In this blog post, we'll embark on a journey through AWS, specifically the US East (N. Virginia) region, and explore how to configure resources to create web servers. Our goal is to set up an Ubuntu-based virtual machine and install the popular Nginx web server, culminating in a simple yet powerful "Hello World" web page. So, whether you're a seasoned cloud architect or a curious beginner, let's dive into the world of AWS and take your first steps towards web hosting mastery.

Before we delve into the steps, let's gain a better understanding of why this journey is important. AWS not only simplifies the process but also opens doors to an array of features that can enhance your web applications' performance, security, and scalability.

So, without further ado, let's roll up our sleeves and embark on this exciting adventure in AWS, where we'll transform a basic instance into a powerful web server capable of serving content to the world.

### **Step 1:** Creating an AWS Instance in us-east-1 with an Ubuntu OS

1. **Sign in to AWS Console:** To begin, you need to sign in to your AWS account. If you don't have an account, you can create one on the AWS website.
    
2. Navigate to **<mark>EC2</mark>**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697399797647/daccc0ac-617b-4ab8-8f12-2646660cc082.png align="center")
    
3. To set up your virtual machine in the **<mark>US-east-1</mark>** region, ensure that you have selected it from the AWS Management Console. This region is popular for its excellent availability and performance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697400570470/21c4bb03-f8e9-465a-ad69-f3eeb7a4ba29.png align="center")
    
4. On the left-hand side, you'll find the "**<mark>Instances</mark>**" option. Click on it to access the instances management panel.
    
    Once you're on the Instances page, look for the "**<mark>Launch Instances</mark>**" button. It's typically located at the top or prominently displayed on the page. Click on this button to initiate the instance creation process.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697400648296/0b34038a-d9a3-4528-910f-455a022bb398.png align="center")
    
5. Enter a descriptive name for your instance in the provided text field. This name will help you identify and manage your instances easily, especially when dealing with multiple instances. Make sure to choose a name that reflects the purpose or role of this instance, such as "WebServer" or "DevelopmentInstance."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697401156732/c4c223c6-4588-4e47-a7df-20cde7eb88e3.png align="center")
    
6. Choose an Ubuntu AMI for your virtual machine. You can search for "Ubuntu" in the AMI search bar.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697460569281/14dd3b0d-624d-4826-a25f-15d9876a85a4.png align="center")

1. Select an appropriate instance type based on your requirements. For a basic web server, a t2.micro instance is usually sufficient.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697460671657/253cdea5-f9ac-4686-b604-3e487ad1aac8.png align="center")

1. Select the key pair.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697460821866/45766f54-44cf-47fe-a353-e35bc0f14aa3.png align="center")

1. Create a new one if no key pair is created for the current region.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697460964045/8081dc9f-0c72-4f6d-9785-cd053d4ef2d9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461016004/9b9b4d17-f3ad-4f4e-bb9f-b2c9cac19716.png align="center")

Click on Create key pair and download the .pem file We’ll use PuTTY to create a .ppk file to access the EC2 instance.

1. In the network settings, select the check boxes corresponding to SSH and HTTP Traffic.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461101813/b1c9b30b-8a3a-43a7-98a2-636e07f821a6.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461195315/c6abebce-2e11-4ff7-b5c8-8cec5d347a72.png align="center")

1. Configure the amount of storage you want for your instance. The default 8 GB of gp2 volume should be enough for a basic web server.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461295286/92abd52c-e1f3-46ae-8525-7e1f3afbc30e.png align="center")

1. Review the summary of the EC2 instance and click on the Launch Instance. It’ll take a moment to initiate the instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461388840/711e444e-5a29-4e0e-9eb8-28c223e17b97.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461604204/d372722e-d4fd-439e-9613-9419ecb16ac2.png align="center")

1. A newly created instance is launched in the availability zone in the US-East-1 Region.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461703360/95745324-430e-447f-82dd-b315dc6ef976.png align="center")

1. We’ll now open PuTTY & copy this Public IP to access the instance from PuTTY.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461857380/8c0ff512-5d0d-4984-9215-6ffb194c53ff.png align="center")

1. Open PuTTY & paste the copied Public IP in the Host Name (or IP address).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697461936350/14b63d7a-6b4a-4916-9d35-7bdfa3a39f6f.png align="center")

1. Then go to, Connection -&gt; SSH -&gt; Auth -&gt; Credentials.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697462019274/81a51c5e-e8b7-42d9-a493-3a08c1de42b3.png align="center")

Now we need a putty private key file for authentication to access the instance. So we’ll now open PuTTYgen & generate the .ppk file from the .pem file.

**<mark>Generating .ppk from .pem:</mark>**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697462164687/135b254b-b34f-4645-b065-6ca540ed0a21.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697464671600/7fbb2b40-ea86-4882-8220-0916b49c9d84.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697464436229/393c8380-d241-418e-9a36-560ca384dac4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697464673390/1da33dba-05c8-4a44-ba15-e05ecf3f2d8d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697464556577/4406a095-2567-48f5-a72e-2476e43376bb.png align="center")

1. Select the generated .ppk file and then click on Open
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697462398153/3ae3ce7a-757d-45f7-abc2-33750c30c784.png align="center")

1. It is successfully connected to the instance. Click on Accept.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697464776370/e8bc8ace-a657-4a6b-9f8c-2ff8ba98b8fd.png align="center")

1. Enter **ubuntu** as username to log in to the instance.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697462580350/89184463-a50b-44d6-9a36-ec09db16ea41.png align="center")

Now our Ubuntu instance is ready for use.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697462657545/9d2d2140-3cba-4f15-b6b9-4ca9166fe34d.png align="center")

---

### **Step 2: Setting up the Nginx Web Server**

1. Now we’ll install NGINX for XYZ corporation to make web servers.
    
    Before installing **nginx**, we’ll first update the system packages using the command:
    
    **<mark>sudo apt-get update</mark>**
    
    • This command is used to resynchronize the package index files from their sources.
    
    • The indexes of available packages are fetched from the location(s) specified in /etc/apt/sources.list.
    
    • This command retrieves and scans the files, so that information about new and updated packages is available
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697462798482/67121008-b118-4abb-9fc4-b2a9c5b0831e.png align="center")
    
2. Installing NGINX using the command **<mark>sudo apt-get install nginx -y</mark>**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697462922609/ef7bc392-0041-4290-a819-fba4dc1a7640.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697462953864/f7a7e609-d8af-415c-9e7b-1eeea4480cff.png align="center")
    
    Now the nginx web server is successfully installed and is ready to be accessible from the internet. We can verify this by entering the public IP of this instance in the web browser.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697463073180/340c1922-a613-41db-b3cf-48d59a53bab7.png align="center")
    
    We can see that the default webpage of the nginx server is accessed successfully.
    

---

### **Step 3: Customizing the Default Website**

1. Our next task is to Change the default website with a page displaying the message: “Hello World”.
    
    For this, We’ll now change our directory to /var/www/html where the default webpage exists. Use the <mark>cd /var/www/html/</mark> command for this
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697463374702/06f00085-6e51-4bd8-a61b-46c1c62d1226.png align="center")
    
    We can see the file index.nginx-debain.html
    
2. We’ll now open the **vi editor** to modify this webpage to display the message **Hello World** using the command: **<mark>sudo vi index.nginx-debain.html</mark>**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697463459256/36834855-554f-4e8d-a02d-f444df2d2546.png align="center")
    
3. We’ll remove all paragraphs (**&lt;p&gt;**) except the last one. And we’ll change the text of &lt;title&gt; and  &lt;h1&gt; to **Hello World!**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697463519027/35c05fc0-60be-4899-87d7-ecebe341212c.png align="center")

All paragraphs (**&lt;p&gt;**) except the last one are removed and the text of &lt;title&gt; and  &lt;h1&gt; is changed to **Hello World!**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697463617734/f8ebae58-985c-47fc-a0b4-2fa2d3bf810d.png align="center")

You should see the "<mark>Hello World!</mark>" message displayed on the web page.

---

In this blog post, we've demonstrated how to create an AWS Virtual Machine in the US-east-1 region, install Nginx, and set up a basic "Hello World" web page. This is just the beginning of your AWS journey; from here, you can expand your web server capabilities, configure domain names, and scale your infrastructure as needed.

AWS offers a wide range of services and features to cater to various use cases. Whether you're hosting a personal blog or running a complex e-commerce website, AWS has you covered. Keep exploring and learning to make the most of AWS's cloud computing capabilities and enhance your online presence. Happy web serving!

---