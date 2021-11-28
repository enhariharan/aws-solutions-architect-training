# Module-3: Route 53 Assignment - 3


## You have been asked to:
1. Use the Route 53 Hosted Zone created in the Assignment
2. Route the traffic to an EC2 instance with an Apache web server running in it using it’s IP address


## Answer

### 1. Create an EC2 instance with Apache web server running in it.
* The steps for this were already provided in the file _aws-solutions-architect-training/module_2_elastic_load_balancer/assignment_2_auto_scaling/module_2_assignment_2_auto_scaling.md_
* Follow the same steps to create an EC2 instance named **module_2_assignment_3_ec2_vm1** and install and configure apache2 in it.
* Verify from a browser that typing the dns name of the EC2 instance in the address bar will take to the **Apache2 Ubuntu Default Page**.


### 2. Use Route 53 to register a DNS name called _hariharan.link_.
* Open the AWS Route 53 console - https://console.aws.amazon.com/route53
* In "Route 53 Dashboard", enter **hariharan.link** in the text box under "Register Domain".
* Finish the purchase of this domain.


### 2. Use Route 53 to route traffic to awsassignment.hariharan.link to open the default apache page in the EC2 instance created above.
* Open the AWS Route 53 console - https://console.aws.amazon.com/route53
* Navigate to **Hosted zones** and select **hariharan.link**. Click on **View details**.
* In the "hariharan.link" page, click on **Create record**.
* In the "Quick create record" page...
  * In the field "Record name", enter **awsassignment** so that the full DNS name reads as **awsassignment.hariharan.link**.
  * In the field "Routing policy", choose **Simple routing**.
  * In the field "Value", paste the value of **IPv4 Public IP** copied from the EC2 console of the EC2 instance created above. Finally click on **Create records**.
* In the "hariharan.link" page, verify that a record for _awsassignment.hariharan.link_ is now added.
* Finally, open the link http://awsassignment.hariharan.link in a browser to verify that the **Apache2 Ubuntu Default Page** is opened. This confirms that the DNS record in Route 53 created correctly.


This finishes all the steps asked in the question.
