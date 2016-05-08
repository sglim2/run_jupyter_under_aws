# Embedding Examples using Amazon's Free Tier service
How to run a Jupyter Notebook under Amazon Web Services (AWS) using Amazon's [Free Tier](http://aws.amazon.com/free/). 
*(Please be aware that Amazon's free tier for new users is limited, and if you extend usage beyond their free tier usage limit, you will be charged)*

# What you'll need?
- You will need an activce AWS account. If you are a first-time user of AWS, check out their [free service](http://aws.amazon.com/free/)
  - This author advises you to set up a billing notification, just in case you do get close to reaching your Free Tier limit. Amazon will desribe how this is done during their sign-up process.

# What we'll do
- We will use the EC2 to spin up a Virtual Machine (VM)
- Once the VM is up and running you will log into it, install any required packages, download the Embedding Notebook, and the run the Jupyter console.
- Once the Jupyter console is running, you will then point your browser at your VM's IP address, and you will see the live Notebook.

# Spinning Up an EC2 Virtual Machine
Once you have set up your AWS account, head over to the [Amazon Console] (https://console.aws.amazon.com/console). We will be launching a Virtual Server in the Cloud, so click on the [EC2 link](https://console.aws.amazon.com/ec2/v2/). Once under the EC2 Dashboard, we will want to launch an instance, so click on the big blue button that says 'Launch Instance'.

![Launch Instance](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Launch_Instance.png)

There are a lot of instances to choose from - If you are using the free tier service, you could just click the 'Free tier only' option, which will limit your choices slightly. For our demonstration, we will be using the 'Amazon Linux' image, which is a RHEL-based distribution. Of course, you are welcome to use any image you like (though I would recommend to keep with a flavour of Linux), but usage will differ to varying degrees to instructions that follow.

![Choose_an_image](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Choose_an_Image.png)

You will now be prompted to choose the size of the instance you would like to launch. If you are using the free tier service, the choice is simple (there is probably only one option elligible). The *t2.micro* image is sufficient for our purposes (a single vCPU and 1 GB RAM), so go ahead and make that selection and click on the 'Review and Launch' button to continue.

![Choose_an_Instance_Type](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Choose_an_Instance_Type.png)


You will now be asked to review your instance before lauching. It is likely that Amazon will show you a warning about securing your instance. _You are strongly advised to heed this warning_. When you run your *Jupyter* notebook, you want to make sure that no-one other than yourself has access to it. When you launch a VM on EC2, your virtual server will be given a public IP address. If you do not restrict access to this VM then anyone will be able to connect to your Jupyter notebook and start running their own (perhaps malicious) code from your server.

In order to secure your VM, select the option to 'Edit security groups'.

![Edit_Security_Groups](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Edit_Security_Groups.png)

If you are new to AWS, then you will not have set up any security groups yet. Here you will need to set up a new security group to allow access to port 8888 to your VM (this is the port the Jupyter notebook will listen on by default), and restrcit access to your current IP address only. Click on the 'Add Rule' button and add a rule with the following settings to your instance:
- Type: Custom TCP Rule
- Protocol: TCP
- Port Range: 88880
         iso_url": "http://www.mirrorservice.org/sites/mirror.centos.org/7/isos/x86_64/CentOS-7-x86_64-Minimal-1503-01.iso",
- Source: 'My IP'
While we're here, it is good practice to restrict the current SSH setting to your IP address only as well.

![Configure_Security_Group](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Configure_Security_Group.png)

Continue with the 'Review and Launch' process. There are a few more options available to you before you launch, but for the purpose of this demonstration, we're ready to 'Launch' (again, press the big blue button).

Before Amazon actually launches your VM, you will need to select (or create a new) key pair. (If you are not sure what a key pair is, you can think of them as a password replacement). Let's assume you want to create a new key pair - select the 'Create a new key pair' option, and give it a name. I'll call mine 'amazon-aws-homekey' (because this is a key for use with amazon-aws and I'll be downloading the key to my home computer). You will need to downlaod the key before you can launch the instance, so do that now. Keep this key safe, it is the only way that will allow you to log into the VM you are about to launch. In addition, (for Linux and OSX users), edit the downloaded key's file permissions to make it user-accessible only. (I also keep all my keys in the standard *.ssh* directory). In a terminal, run:
'''bash
mv ~/Downloads/amazon-aws-homekey.pem ~/.ssh
chmod 600 ~/.ssh/amazon-aws-homekey.pem
'''

You may now lauch the install (big blue button time again). Phew!!

Head on back over to the [EC2 dashboard](https://console.aws.amazon.com/ec2/v2), and select the 'Instances' link. You will see that an instance is in a 'running' state, and you will also find it's public hostname and IP address.

![Running_Instance](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Running_Instance.png)

you are now ready to log in to your server in the cloud.

# Provisioning your Server

From a terminal (assuming you're a linux or mac user), log on to the VM you have just provisioned:

'''bash
ssh -i ~/.ssh/amazon-aws-homekey.pem ec2-user@52.90.238.194 
'''

The '-i' option will point to your key file you have just set up for this VM instance, and the user (*ec2-user*) is the standard username you will need to use to log in as. 

You will now need to install a few packages in order to run the embedding methos examples. At the very least you will need to install
- gcc
- git
- lapack-devel
- blas-devel
- python-numpy
- python-matplotlib
- pyhton-scipy
- jupyter
The Amazon Linux Instance uses the *yum* package manager, so we'll use that to install most packages:
'''bash
sudo yum group install -y "Development tools"
sudo yum install -y lapack-devel blas-devel python27-numpy python27-matplotlib python27-scipy
'''
The *Jupyter* package isn't available as part of the standard yum packages, so we'll use python's pip to install it:
'''bash
sudo pip install jupyter
'''

Colne the Embedding Method notebook examples 
'''bash
git clone https://github.org/............
'''
and run the notebook, making sure to set the notebook to listen on all ports (the security group you set up eariler will actually limit the IP addresses allowed to connect to only your current IP.
'''bash
jupyter notebook Notebook_1/Embedding\ Notebook\ 1.ipynb --ip='\*'
''')

# Accessing the Notebook

Now from your local machine, point your favourite browser at the cloud VM's IP address, port 8888, for example
'''bash
IP.ADD.RE.SS:8888
'''










