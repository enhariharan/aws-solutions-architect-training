# Module-2: Auto Scaling Assignment - 2

## You have been asked to:
1. Create a Web Server AMI with Apache 2 server running in it.
2. Create a Launch Configuration with this AMI. 
3. Use this Launch Configuration to create an Auto Scaling group with 1 minimum and 3 maximum instances.

## Answer

### 1. Create an EC2 instance
* Follow the steps mentioned in the file aws-solutions-architect-training/module_1_elastic_compute_and_storage_volumes/assignment_1_ec2/assignment_1_ec2.md to create an EC2 instance and install/configure nginx.
* Instance 1: Ubuntu t2.micro EC2 instance, 64-bit (x86), tag **module_2_assignment_2_ec2_vm1**, new inbound HTTP rule on port 80 allowing all requests (0.0.0.0/0)


### 2. Install Apache 2 in this EC2 instance
* Open an SSH session to the EC2 instance created above.
* Install Apache2 HTTP server using the below commands
  ```bash
  $ sudo apt update
  $ sudo apt install -y apache2
  ```
* Verify that Apache2 HTTP server is running. As a result of this command, the status of Apache2 HTTP server must show up as **Active: active (running)**
  ```bash
  $ sudo service apache2 status
  ```
* Verify that Apache2 HTTP server is serving pages correctly. Open a browser and go to the external IP address for the EC2 instance (using http://) as pointed in the EC2 management console. If correctly configured, then the default **Apache2 Ubuntu Default Page** must show up.
* Now, save this EC2 instance as an AMI image with name **module_2_assignment_2_ec2_vm1_ami**.

### 3. Create a launch configuration with this AMI
* In the "EC2 Management Console", open **Launch Configurations** under **Auto Scaling** in the navigation pane. Click on **Create Launch Configuration**.
* In the page "Create launch configuration"...
  * In the field "Name", type **module_2_assignment_2_ec2_vm1_launch_configuration**.
  * In the field "AMI", choose the same AMI that was created above with name **module_2_assignment_2_ec2_vm1_ami**.
  * In the field "Instance Type", choose **m1.small**
  * Leave all other fields as it were with default values.
  * In the field "Key pair (login)", give the Key pair name as **module_2_assignment_2_ec2_vm1_launch_config_key**.
  * Finally click on **Create launch configuration**.
* In the "Launch Configurations" page, verify that the launch configuration is visible.

### 4. Create an Auto Scaling group with this launch configuration
* In the "Launch configurations" page, select the launch confioguration created above with name **module_2_assignment_2_ec2_vm1_launch_configuration**.
* Now click on **Actions --> Create Auto Scaling group**.
* In the page "Choose launch template or configuration"...
  * In the field "Auto Scaling group name", provide the name as **module_2_assignment_2_ec2_vm1_auto_scaling_config**. Click on **Next**.
  * In the field "Availability Zones and subnets", choose **use-east-1c** which is the same zone in which the EC2 instance was created above. Click on **Next**.
* In the page "Configure advanced options", leave the fields as they are. CLick **Next**.
* In the page "Configure group size and scaling policies"...
  * Set "Minimum capacity" to **1**, and "Maximum Capacity" to **5**. CLick **Next**.
* In the page "Add tags", leave the fields as they are. CLick **Next**.
* Now, review the settings and click on **Create Auto Scaling group**.

This finishes the steps asked in the question.
