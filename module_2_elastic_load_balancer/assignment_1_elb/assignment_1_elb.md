# Module-3: ELB Assignment - 1

## You have been asked to:
1. Create a Classic Load Balancer and register 3 EC2 instances with different web pages running in them.
2. Migrate the Classic Load Balancer into an Application Load Balancer

## Answer

### 1. Create 3 EC2 instances
* Follow the steps mentioned in the file _aws-solutions-architect-training/module_1_elastic_compute_and_storage_volumes/assignment_1_ec2/assignment_1_ec2.md_ to create an EC2 instance and install/configure nginx.
* Repeat the same steps to create 3 EC2 instances, as briefly described below.
  * Instance 1: Ubuntu t2.micro EC2 instance, 64-bit (x86), tag **module_1_assignment_1_ec2_vm1**, new inbound TCP rule on port 81 allowing TCP to 0.0.0.0/0
  * Instance 2: Ubuntu t2.micro EC2 instance, 64-bit (x86), tag **module_1_assignment_1_ec2_vm2**, new inbound TCP rule on port 81 allowing TCP to 0.0.0.0/0
  * Instance 3: Ubuntu t2.micro EC2 instance, 64-bit (x86), tag **module_1_assignment_1_ec2_vm3**, new inbound TCP rule on port 81 allowing TCP to 0.0.0.0/0
  * On all 3 EC2 instances, do the following steps:
    * Install nginx
    * Create a new nginx configuration file in /etc/nginx/sites-enabled/module_1_assignment_1_web_server_landing_site to listen on port 81.
    * Create a new index.html file in /var/www/module_1_assignment_1_web_server_landing_site/index.html
    * Verify that the new index.html can be accessed from the browser by providing the dnsname and port 81 in the address bar.


### 2. Create a Classic Load Balancer
* In the "EC2 Management Console", select **Load Balancers** under **Load Balancing**. Click on **Create Load Bakancer**.
* In the page "Select load balancer type", select **Classic Load Balancer - previous generation** and click on **Create**.
* In "Step 1: Define Load Balancer", give "Load Balancer name" as **module-1-assignment-1-classicelb** and select **Next: Assign Security Groups**.
* In " Step 2: Assign Security Groups", select all the security groups and select **Next: Configure Security Settings**.
* Keep clicking Next step until you reach **Step 6: Add Tags". Here, provide **module-1-assignment-1-classicelb** as a Tag.
* Click on **Review and Create**. In the next page, review all your settings and click on **Create** whne ready.
* Go back to the Load Balancers page in the EC2 console to verify that ELB is created.

### 3. Register the 3 EC2 instances to the Classic Load Balancer
* Option-1: During creation of a new Load Balancer
  * While creating a new load balancer, **Step 5: Add EC2 Instances** provides an opportunity to select EC2 instances to attach to the load balancer.

* Option-2: After creation of a new Load Balancer
  * In the "EC2 Management Console", select **Load Balancers** under **Load Balancing**. Select the load balancer created above, in this page.
  * Click on **Actions --> Edit instances**.
  * In the dialog "Add and Remove Instances", choose all the 3 EC2 instances shown. Select **Save**.
  * Back in the EC2 Management Console page for Load Balancers, click on **Instances** to verify that all 3 instances are selected.

### 4. Migrate the Classic Load Balancer into an Application Load Balancer
  * In the "EC2 Management Console", select **Load Balancers** under **Load Balancing**. Select the load balancer created above, in this page.
  * Under the tab "Description", note the entry called **Type Classic (Migrate Now)**. Click on **Migrate Now**.
  * In the "Migration" tab, click on **Launch ALB Migration Wizard**. This will take to **Step 6: Review**. Review and finally click on **Create**.
  * Go back to the "EC2 Management Console" and verify that there are now 2 load balancers. One id of Type **Classic** and a new ELB is of Type **Application**.

This finishes the steps asked in the question.
