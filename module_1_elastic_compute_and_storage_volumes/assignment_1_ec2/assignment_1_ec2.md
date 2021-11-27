# Module-2: EC2 Assignment - 1

## You have been asked to: 
1. Create an Instance in us-east-1 (N. Virginia) region with an Ubuntu OS and install Nginx for making them web servers.
2. Change the default website with a hello world page

## Answer

### 1. Create an Instance in us-east-1 (N. Virginia) region with Ubuntu OS

* Login into https://aws.amazon.com.
* In the top status bar, just before the Login Name, click on the drop-down to choose the region. Choose US East (N. Virgina) us-east-1.
* Click on "services" in top-left and select EC2.
* In "Step 1: Choose an Amazon Machine Image (AMI)", choose an instance of Ubuntu Server on 64-bit (x86).
* In "Step 2: Choose an Instance Type" choose t2.micro.
  * If a default VPC is not available, then click on Create default VPC to create a new default VPC.
* In "Step 3: Configure Instance Details", select "Protect against accidental termination" to enable it.
* In "Step 4: Add Storage" leave the default "Root" volume as default.
* In "Step 5: Add Tags" Choose Add Tag and provide "assignment_1_ubuntu_vm" as a tag.
* In "Step 6: Configure Security Group" Click on Add Rule and select "HTTP" from drop-down.
  * Also, rename security group as "assignment_1_ubuntu_vm_sg" as an optional step.
* In "Step 7: Review Instance Launch", review the options chosed and finally click on Launch when satisfied.
* In "Select an existing key pair or create a new key pair", select on Create a new pair, select RSA, give "Key pair name" as "assignment_1_ubuntu_vm_key".
* Click on Download Key Pair and save the private key locally. Ensure that this file has limited permissions (in Linux, permission must be set to 400).
* Finally, click on Launch Instances.
* In "Launch Status", verify that the instance is launching. Click on View Instances. The instance should appear in the Instances dashboard as "Running".

### 2. Install Nginx
* Open an SSH instance into this instance. On my Ubuntu desktop, this was the command entered in a BASH terminal:
  ```bash
  $ ssh -i ~/.ssh/assignment_1_ubuntu_vm_key.pem ubuntu@ec2-3-83-242-220.compute-1.amazonaws.com
  ```
* Install nginx HTTP server with the following commands in the terminal.
  ```bash
  sudo apt install -y nginx
  ```
* Try opening the dns-name of the created VM in a browser.
  * For the above instance, I opened Firefox browser and pasted **ec2-3-83-242-220.compute-1.amazonaws.com** in the address bar.
  * If nginx installed correctly then you should see the default nginx page open in the browser.

### 3. Change the default website with a hello world page
* Create a nginx configuration file called **/etc/nginx/sites-enabled/ec2_assignment_1** and enter the following in it. The same file is attached to this directory for reference.
  ```
  server {
        listen 81;
        listen [::]:81;

        server_name ec1_assignment_1.hariharan.com;

        root /var/www/ec2_assignment_1;
        index index.html;

        location / {
                try_files $uri $uri/ = 404;
        }
  }
  ```

* Create an HTML landing page named **/var/www/ec2_assignment_1/index.html** and paste the following in it. The same file is attached to this directory for reference.
  ```HTML
  <!doctype html>
  <html>
    <head>
      <meta charset="utf-8">
      <title>EC2 Assignment 1</title>
    </head>
    <body>
      <h1>Submission for EC2 Assignment 1</h1>
      <p>This is the submission for EC2 Assigment 1.</P
      <p>Steps performed:
      <ol>
        <li> Created an Ubuntu VM on AWS.
        <li> Opened an SSH session to this VM.
        <li> Installed nginx server. </li>
        <li>Verified that default web-page openedfrom browser. </li>
        <li> Created a new virtual-site called ec2_assignment. </li>
        <li> Created a new index.html for this virtual-site. </li>
        <li> Opened this page in browser. </li>
      </ol>
      </p>
      <p> Thank you. <br>
      Hariharan Narayanan</p>
    </body>
  </html>
  ```
  * Restart nginx to take up the new configuration
    ```bash
    $ sudo nginx -s reload
    ```
  * Go to the EC2 Management Console and modify the Security Group linked to this EC2 instance. Create an inbound rule for TCP on port 81 that is open to 0.0.0.0/0
  * Finally, try opening the dns-name of the created VM in a browser with the post pointing to 81.
    * For the above instance, I opened Firefox browser and pasted **ec2-3-83-242-220.compute-1.amazonaws.com:81** in the address bar.
    * If nginx reloaded correctly then you should see the new index.html that we created above.

This finished the steps for the question asked above.
