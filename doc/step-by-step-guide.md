### Step 1: Create an EC2 Instances.
Amazon EC2(Elastic Compute Cloud) allows you to launch and manage your virtual servers - called EC2 Instances in the cloud. These instances are like computers that you can use to run applications, host websites, or perform computations.

**Elastic Compute Cloud:**
**Elastic**: Can easily increase or decrease the number of servers (instances) 
depending on your workloads.
**Compute**: provides the processing power needed to run your applications.
**Cloud**: Available over the internet, can be accessed from anywhere.

- Choose the **Region** closest to you.
- In Your EC2 Console, Click **Launch Instances**.
- Press **enter** or click to view image in full size
- Under **Name & Tags**:
*Tags are labels that you assign to your AWS resources to helps you assign to your resources to help you organize, identify, and manage them.*
*Tags are made up of two parts: 
 **Key**: The name of the tag e.g. Environment.
**Value**: The identifier for that key e.g. Chrome*

 - **Name**: Provide a name e.g. *ChromeInstances*
 - **Tags**: Choose Additional Tags under the Name
- Proceed Down to the **AMI and OS Images**, select **Amazon Linux 2023**.
- Under **Instance Types**, Choose **t2micro or t3micro** as they are *free tier eligible*.
- For **Key pair** (login), select **Proceed without a key pair**.
*A key pair to securely connect to your instance.*


Next, Configure your **Network Settings**. *Network settings define how your instances interact with the internet and other AWS resources, determining factors like IP addresses and network routing*. 
Select the **VPC** to Launch your Instance in. Under Subnets, choose a subnet. On the Firewalls, choose Security Group. Security Groups control the traffic for your Instance.
The rest remain as default, then Click **Launch Instances**.

Now let’s create one more EC2 instance for the **ICT environment**.
