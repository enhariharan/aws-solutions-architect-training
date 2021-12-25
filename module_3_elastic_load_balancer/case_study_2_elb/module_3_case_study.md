# Module-3 Case Study

## Problem Statement:
You work for XYZ Corporation that uses on premise solutions and some limited number of systems. With the increase in requests in their application, the load also increases. So, to handle the load the corporation had to buy more systems almost on regular basis. Realizing the need to cut down the expenses on systems, they decided to move their infrastructure on AWS. Once migrated, you have been asked to:

1. Manage the scaling requirements of the company by:
   * Deploying multiple compute resources on the cloud as soon as the load increases and the CPU utilization exceeds 80%
   * Removing the resources when the CPU utilization goes under 60%
2. Create a Load balancer to distribute the load between compute resources
3. Route the traffic to the company’s domain

Note: You can get a free domain from [Freenom](https://www.freenom.com/en/index.html?lang=en)

## Answer

### 1. Create an EC2 instance.
* Follow the steps mentioned in the file _aws-solutions-architect-training/module_1_elastic_compute_and_storage_volumes/assignment_1_ec2/assignment_1_ec2.md_ to create an EC2 instance and install/configure nginx.
  * EC2 Instance: Ubuntu t2.micro EC2 instance, 64-bit (x86), new inbound HTTP rule on port 80 allowing all requests (0.0.0.0/0)
  * Create an AMI out of this EC2 instance and name it **module_3_case_study_1_ami**.


### 2. Create a Launch Template for the EC2 instance.
* Navigate to **Launch Templates** under "Instances" in "EC2 Management Console". Click on **Create launch template**.
* Name the launch template as **module_3_case_study_1_launch_template**.


### 3. Create an Auto-Scaling group and attach it to the EC2 instance.
* In the "EC2 Management Console", navigate to **Auto Scaling Groups** under "Auto Scaling".
* Click on **Create Auto Scaling group**.
* In "Auto Scaling group name"...
  * In "Auto Scaling group name", give the name as **module_3_case_study_1_auto_scaling_group**.
  * In "Launch Template", choose **module_3_case_study_1_launch_template** created above. Click **Next**.
  * In "Choose instance launch options", choose **us-east-1c** in "Availability Zones and subnets".
  * In "Configure group size and scaling policies", choose **Target tracking scaling policy**. Choose "Metric Tye" as **Average CPU utilization** and select 80. in the "Target Value" Click **Next** all the way until the Auto Scaling goup is created.


### 4. Transfer the company domain to AWS Route 53.
* This is described in the file _aws-solutions-architect-training/module_2_elastic_load_balancer/assignment_3_route_53/module_3_ assignment_3_route_53.md_. Please follow the same steps.


### 5. Create a new DNS record for the company's domain in AWS Route 53.
* This is described in the file _aws-solutions-architect-training/module_2_elastic_load_balancer/assignment_3_route_53/module_3_ assignment_3_route_53.md_. Please follow the same steps.

