# Module-2: Case Study
## Problem Statement
You work for XYZ Corporation. Your corporation is working on an application and they require secured web servers on Linux to launch the application.

### You have been asked to:
1. Create an Instance in us-east-1 (N. Virginia) region with Linux OS and manage the requirement of web servers of your company using AMI.
2. Replicate the instance in us-west-2 (Oregon) region.
3. Build two EBS volumes and attach them to the instance in us-east-1 (N. Virginia) region.
4. Delete one volume after detaching it and extend the size of other volume. 
5. Take backup of this EBS volume.

## Answer
### 1. Create an Instance in us-east-1 (N. Virginia) region with Linux OS and manage the requirement of web servers of your company using AMI.
* Login into https://as/amazon.com.
* In the top status bar, just before the Login Name, click on the drop-down to choose the region. Choose **US East (N. Virgina) us-east-1**.
* Click on "services" in top-left and select **EC2**.
  * In "Step 1: Choose an Amazon Machine Image (AMI)", choose an instance of **Ubuntu Server** on **64-bit (x86)**.
  * In "Step 2: Choose an Instance Type" choose **t2.micro**.
    * If a default VPC is not available, then click on **Create default VPC** to create a new default VPC.
  * In "Step 3: Configure Instance Details", select "Protect against accidental termination" to enable it
  * In "Step 4: Add Storage" leave the default "Root" volume as default.
  * In "Step 5: Add Tags" Choose **Add Tag** and provide "assignment_1_ubuntu_vm" as a tag
  * In "Step 6: Configure Security Group" Click on **Add Rule** and select "HTTP" from drop-down.
    * Also, rename security group as "assignment_1_ubuntu_vm_sg" as an optional step.
  * In "Step 7: Review Instance Launch", review the options chosed and finally click on **Launch** when satisfied.
  * In "Select an existing key pair or create a new key pair", select on **Create a new pair**, select **RSA**, give "Key pair name" as "assignment_1_ubuntu_vm_key"
    * Click on **Download Key Pair** and save the private key locally. Ensure that this file has limited permissions (in Linux, permission must be set to 400)
    * Finally, click on **Launch Instances**
  * In "Launch Status", verify that the instance is launching. Click on **View Instances**. The instance should appear in the Instances dashboard as "Running".
  * Now open an SSH instance into this instance and install nginx HTTP server with the following commands in a terminal.
    * sudo apt install -y nginx
    * try opening the dns-name of the created VM in a browser. If nginx installed correctly then you should see the default nginx page open in the browser.
 

### 2. Replicate the instance in us-west-2 (Oregon) region.
* In the EC2 dashboard, select the EC2 instance ID created in Step 1.
* Now, Select **Actions --> Image and templates --> Create image".
* In the "Create image" page, type "Image name" as "case_study_1_image".
* In "Image description - optional", type "case_study_1_image"
* Click on **Add tag** and select "case_study_1_vm_image" as a new tag.
* CLick on **Create image**.
* Select **AMIs** in the "EC2 Management Console" and verify that an AMI with AMI name **case_study_1_vm_image** is created.
* Now selet this AMI and then click on **Actions --> Copy AMI**
  * In "AMI copy name" paste **case_study_1_vm_image_copy**
  * In Destination region, select **US West (Oregon)**
  * Select **Copy AMI**
  * Now, in the "EC2 Management Console", Select **Oregon** as the AWS region.
  * Open **AMIs** in the dashboard and wait until the AMI instance state is converted to **available**

### 3. Build two EBS volumes and attach them to the instance in us-east-1 (N. Virginia) region.
* In the "EC2 Management Console", choose  **US East (N. Virgina) us-east-1**.
* Under "Elastic Block Store", choose **Volumes** and select **Create volume**.
* In the "Create volume" page, ensure that the "Availability Zone" is exactly the same as that for the EC2 instance created above.
* Choose **Add tag** and provide a new tag **case_study_1_ebs_volume_1**. Leave other options as it is. Finally, select **Create volume**
* In the **Volumes** dashboard, varify that the "volume-state" changes from **Creating** to **Available**.
* Now select this newly created volume and select **Actions --> Attach volume**
* In the "Attach volume" page, select the same instance of EC2 that was created above. Then choose **Attach volume**.
* Login to the EC2 instance through SSH and unmount the volume with tag "case_study_1_ebs_volume_2".
  * Execute the command **lsblk** to verify that the EBS volume is listed as the device **/dev/xvdf**.
  * Execute the command **sudo file -s /dev/xvdf** to verify that there is no file system on this device (Output must be **/dev/xvdf: data**)
  * Create a file system with the command **sudo mkfs -t xfs /dev/xvdf** and then execute **sudo file -s /dev/xvdf** to confirm that an XFS file-sytem was created.
  * Create a directory to work as a mount point - **sudo mkdir -p /data/case_study_1_volume_1**
  * Finally, mount this volume - **sudo mount /dev/xvdf /data/case_study_1_volume_1**
* Repeat the same steps as above to attach a new volume with tag **case_study_1_ebs_volume_2**.
  * Execute the command **lsblk** to verify that the EBS volume is listed as the device **/dev/xvdg**.
  * Execute the command **sudo file -s /dev/xvdg** to verify that there is no file system on this device (Output must be **/dev/xvdg: data**)
  * Create a file system with the command **sudo mkfs -t xfs /dev/xvdg** and then execute **sudo file -s /dev/xvdg** to confirm that an XFS file-sytem was created.
  * Create a directory to work as a mount point - **sudo mkdir -p /data/case_study_1_volume_2**
  * Finally, mount this volume - **sudo mount /dev/xvdg /data/case_study_1_volume_2**

### 4. Delete one volume after detaching it and extend the size of other volume.
* In the "EC2 Management Console", choose  **US East (N. Virgina) us-east-1** and select **Volumes** under "Elastic Block Store".
* Login to the EC2 instance through SSH and unmount the volume with tag "case_study_1_ebs_volume_2".
  * Now unmount the volume - **sudo umount -d /dev/xvdg**
  * In the "EC2 Management Console" choose the volume with tag "case_study_1_ebs_volume_2" and then select **Actions --> Detach volume**. Choose **Detach** in the message box.
* In the "Volumes" dashboard, verify that there is no instance shown under "Attached instances".
* Now, choose the volume with tag "case_study_1_ebs_volume_1". Now, select **Actions --> Modify volume**.
* In the "Modify volume" page box, change the "Size" field to **125** GiB and click on **Modify**.
* In the "Modify ..." dialog box, click on **Modify**.
* In the "Volumes" dashboard, verify that "Volume state" value changes from **in-use - modifying (0%)** to **in-use - optimizing** to finally **in-use**.

### 5. Take backup of this EBS volume.
* Option-1: Using Snapshots.
  * In the "EC2 Management Console", choose  **US East (N. Virgina) us-east-1**.
  * Under "Elastic Block Store" choose **Snapshots** and click on **Create snapshot**.
  * Under "Volume ID" choose the EBS ID corresponding to "case_study_1_ebs_volume_1"
  * In "Description" enter **case_study_1_ebs_volume_1_snapshot**.
  * In "Tags" add a new tag **case_study_1_ebs_volume_1_snapshot**.
  * Finally, select **Create snapshot**.
  * Come back to "Snapshots" page and verify that the snapsot is created and it's "Progress" column has the value **Available (100%)**.
  
* Option-2: Using AWS Backup
  * In the "EC2 Management Console", choose **US East (N. Virgina) us-east-1**.
  * In the search bar type **AWS Backup**. Under the listed services select **AWS Backup**.
  * Select **Create Backup plan**. In "Choose template" choose an appropriate template. In Backup plan name" give a name. Finally select **Create plan**.
  * A plan was not actually created since this appears to be a paid service.


This finishes the steps done to address all aspects of the Case study.
