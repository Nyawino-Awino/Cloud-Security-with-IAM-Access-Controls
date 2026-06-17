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

### Step 2: Set Up Permission Policy
Create **IAM Policy** to give access to our instances.
- On the AWS Console, Search **IAM**.
- On the Left navigation panel, choose **Policies**.
*A policy is an object in AWS that, when associated with an identity or resource, defines their permissions. Permissions in the policies determine whether the request is allowed or denied. Most policies are stored in AWS as JSON documents. AWS supports various types of policies: permission boundaries, identity-based policies, resource-based policies, AWS Organizations service control policies (SCPs), AWS Organizations resource control policies (RCPS), Session Policies and Access Control Lists (ACLs)*
- Choose Create **Policy**
Specify the Permissions. Switch your Policy editor tab to JSON

'''json
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Effect": "Allow",
   "Action": "ec2:*",
   "Resource": "*",
   "Condition": {
    "StringEquals": {
     "ec2:ResourceTag/Environment": "Chrome"
    }
   }
  },
  {
   "Effect": "Allow",
   "Action": "ec2:Describe*",
   "Resource": "*"
  },
  {
  
   "Effect": "Allow",
   "Action": [
       "ec2:DeleteTags",
       "ec2:CreateTags"
       ],
   "Resource": "*"
  }
 ]
}

**Lets understand what a Policy is?**
The policy that we have created allows some Permissions. 
It allows the user to start, stop and describe the various instances with the tag "Environment=Chrome" as it denies the ability to create and delete tags for all the instances.

**Structure of a JSON Policy.**
- Version
‍This means 2012-10-17 is the date of the latest policy version. 
This tells you whether the policy is up to date and if it complies with the standards.

- Statement
‍The main part or element of the policy structure.
It defines a list of permissions.
A statement can be a single statement or an array of statements. In an array of statements, each individual is contained in a curly brace {}.
For multiple statement we us [{...},{...},{...}]

- Effect
‍This can have two values - either Allow or Deny - to specify whether the 
policy allows or denies a certain action. 
Deny has priority. 
In the first statement, "Effect": "Allow" means this statement is trying to allow for an action.

- Action
‍Specifies actions that will be allowed or denied.
As for the above case, "Action": "ec2:*" means all actions that you could possibly take on EC2 instances are allowed.

- Resource
D‍efines the objects that the policy apply to? Using "*" means all resources within the defined scope.

- Condition Block (optional)
‍The circumstances under which the policy is in action. 
Conditions have 3 parts:Codition-operator, Condition-Key, Condition-Value.
In this case, the condition is that the resource is tagged Environment - Chrome. 
This means specifying "Resource": "*" in the line above means all resources with the Env - Chrome tag are impacted by your statement.
