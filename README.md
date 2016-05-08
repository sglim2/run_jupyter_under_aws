# Embedding Examples using Amazon's Free Tier service
How to run a Jupyter Notebook under Amazon Web Services (AWS) using Amazon's [Free Tier](http://aws.amazon.com/free/). 
*(Please be aware that Amazon's free tier for new users is limited, and if you extend usage beyond their free tier, you will be charged)*

# What you'll need?
- You will need an activce AWS account. If you are a first-time user of AWS, check out their [free service](http://aws.amazon.com/free/)
  - This author advises you to set up a billing notification, just in case you do get close to reaching your Free Tier limit. Amazon will desribe how this is done during their sign-up process.
- We will use the EC2 to spin up a Virtual Machine (VM)
- Once the VM is up and running you will og into it, install and required packages, download the Embedding Notebook, and the run the Jupyter console
- Once the Jupyter console is running, you will then point your browser at your VM's IP address, and you will see the live Notebook.

# Getting Started
Once you have set up your AWS account, head over to the [Amazon Console] (https://console.aws.amazon.com/console). We will be launching a Virtual Server in the Cloud, so click on the [EC2 link](https://console.aws.amazon.com/ec2/v2/). Once under the EC2 Dashboard, we will want to launch an instance, so click on the big blue button that says 'Launch Instance'.

![Launch Instance](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Launch_Instance.png)

There are a lot of instances to choose from - If you are using the free tier service, you could just click the 'Free tier only' option, which will limit your choices slightly. For our demonstration, we will be using the 'Amazon Linux' image, which is a RHEL-based distribution. Of course, you are welcome to use any image you like (though I would recommend to keep with a flavour of Linux), but usage will differ to varying degrees to instructions that follow.

![Choose_an_image](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Choose_an_Image.png)

You will then be prompted to choose the size of the instance you would like to launch. If you are using the free tier service, the choice is simple (there is probably only one option elligible). The *t2.micro* image is sufficient for our purposes (a single vCPU and 1 GB RAM), so go ahead and make that selection and click on the 'Review and Launch' button to continue.

![Choose_an_Instance_Type](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Choose_an_Instance_Type.png)


You will now be asked to review your instance before lauching. It is likely that Amazon will show you a warning about securing your instance. _You are strongly advised to heed this warning_. When you run your *Jupyter* notebook, you want to make sure that no-one other than yourself has access to it. When you launch a VM on EC2, your virtual server will be given a public IP address. If you do not restrict access to this VM then anyone will be able to connect to your Jupyter notebook and start running their own (perhaps malicious) code from your server.

In order to secure your VM, select the option to 'Edit security groups'.

![Edit_Security_Groups](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Edit_Security_Groups.png)

If you are new to AWS, then you will not have set up any security groups yet. Here you will need to set up a new security group to allow access to port 8080 to your VM, and restrcit access to your IP address only. Click on the 'Add Rule' button and add a rule with the following settings to your instance launch:
- Type: Custom TCP Rule
- Protocol: TCP
- Port Range: 8080
- Source: 'My IP'
While we're here, it is good practice to restrict the current SSH setting to your IP address only too.

![Configure_Security_Group](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Configure_Security_Group.png)

Continue with the 'Review and Launch' process. There are a few more options available to you before you launch, but for the purpose of this demonstration, we're ready to 'Launch' (again, press the big blue button.

Before Amazon actually launches your VM, you will need to select (or create a new) key pair. (If you are not sure what a key pair is, you can think of them as a password replacement). Let's assume you want to create a new key pair - select the 'Create a new key pair' option, and give it a name. I'll call mine 'amazon-aws-homekey' (because this is a key for use with amazon-aws and I'll be downloading the key to my home computer). You will need to downlaod the key before you can launch the instance, so do that now. Keep this key safe, it is the only way that will allow you to log into the VM you are about to launch. In addition, (for Linux and OSX users), edit the downloaded key's file permissions to make it user-accessible only. (I also keep all my keys in the standard *.ssh* directory. In a terminal, run:
'''bash
mv ~/Downloads/amazon-aws-homekey.pem ~/.ssh
chmod 600 ~/.ssh/amazon-aws-homekey.pem
'''

You may now lauch the install (big blue button time again). Phew!!











