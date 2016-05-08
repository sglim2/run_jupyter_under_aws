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
Once you have set up your AWS account, hed over to the [Amazon Console] (https://console.aws.amazon.com/console). We will be launching an Virtual Server in the Cloud, so click on the EC2 link. Once under the EC2 Dashboard, we will want to launch an instance, so click on the big blue button that says ' Launch Instance'.

![Launch Instance](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Launch_Instance.png)

There are a lot of instances to choose from - If you are using the free tier service, you could just click the 'Free tier only' option, which willlimit your choices slightly. For our demonstration, we will be using the 'Amazon Linux' image, which is a RHEL-based distribution. Of course, you are welcome to use any image you like (though I would recommend to keep with a flavour of Linux), but usage will differ to varying degrees to instructions that follow.

![Choose_an_image](https://raw.githubusercontent.com/sglim2/run_jupyter_under_aws/master/Choose_an_Image.png)
