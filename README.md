# terraform

<b>Getting started with terraform</b>

<b>What is Terraform</b>
<p>Terraform is an open source IAC(infra as code) tool written in golang for building, changing, and versioning infrastructure safely and efficiently. With Terraform we can provision infra through code/software to achieve consistent and predictable environments. With Terraform an organization is not locked with one cloud provider and can opt for hybrid cloud infra.</p>
<p>Terraform is created by HashiCorp</p>
<p>Terraform is declarative & it uses HCL(HashiCorp Configuration Language) to declare the desired state of your infra.</p>
<p>Documentation - https://www.terraform.io/intro/index.html </p>

<b>What is Terraform CLI</b> 
- It's command like tool written in golang to run terraform commands.
- Basic commands are init , plan , apply and destroy. 
- you can get it from https://www.terraform.io/downloads.html as per your operating system.

<b>How to run Terraform commands through CLI</b><br>
![alt Terraform CLI](./terraform.png)

<b>Building blocks of Terraform configuration files</b> 
<p>Terraform config files are written in HCL(Hashicorp configuration language). There are 5 frequently used terraform concepts explained in this getting started guide.</p>

- Provider - One of the cloud providers ( GCP , AWS , Docker , Azure etc)
    - This guide is designed for GCP. For other cloud providers please check terrafrom documentation at <a>https://learn.hashicorp.com/terraform.
    - Almost all the terraform providers are written in golang.
    - Providers are binaries. They work with terraform CLI to make respective API calls to provision the infra.
- Resource - The list of resources you like to create. In this guide we created a VPC network ,  a compute instance , a random number and a google storage bucket.
- Provisioner - They are executed after a resource a created or before a resource is destroyed.
    - In this sense provisioners are linked to a resource and declared under resource section.
    - Terraform advises to avoid provisioners as much as you can.
    - Provisioners are used to perform task like executing post creation scripts either locally or on remote machine.
- Output - output returns the values after creation of resources
- Module - module provides reusability to your code. you define it once like templates and then just pass values to get desired result.
    - Modules are of 2 types : local and global. We used a local module in this guide.
    - Local modules are the modules which reside on the same machine as your other terraform config files.
    - Global modules reside in a certral registry like terrafrom registry - https://registry.terraform.io/

<b>Prerequisite</b>
- Free GCP Account.
- Basic GCP understanding.

<b> how to use this guide? </b>

- Download terraform binary from terraform website <a>https://www.terraform.io/downloads.html.
- Add binary to classpath.
- git clone https://github.com/amitkumardube/terraform.git
- If there is any error while cloning the repo due to SSL certificate , please run `git config --global http.sslVerify false` and then run the above clone command again.
- git checkout release/1.0.0
- modify main.tf file to update the `GCP Project ID` and the `path of json file for the service account` which has required access to create resources as per config
- To create a service account if you don't already have one - please login to GCP account. Go to `IAM & ADMIN -> Service Accounts`. Check a new service account. For simplicity grant this service account `Editor` role and then `create a key` for this service account.
- Once you are done with above steps, you are all done to start with Terraform. Please follow below steps in sequence.
- terraform -chdir=DIR init (ignore -chdir flag if you are in the directory where your terraform config files are else enter the PATH of the directory which contains your terraform config files)
    - It downloads any modules being used in configuration.
    - It downloads any provider plugin used and put it in .terraform directly.
    - It initializes any backend to store your state data.
- terraform -chdir=DIR validate
    - It validates the configuration files as per the provider downloaded during the init step.
    - This step is optional and has to be run after terraform init. 
- terraform -chdir=DIR plan -out terraform.tfplan
    - It's not mandatory to run this step. However it's a best practice to do this.
    - This step captures your planning into a file so that any change done later doesn't impact your plan.
- terraform -chdir=DIR apply terraform.tfplan
    - This step actually triggers the creation of infra as per the config files.

Now grab a coffee and let terraform do all the magic. You will see your resources getting created in gcp console.

And this is all. Happy terraforming !!.

<b>Best Practices</b>
- Always give structure to your configuration files. Don't put everything in one file.
- Always write your code with reusability in mind. Try to write modules for each resource type.
- Write a variable file (.tfvars) for all the variables in the configuration.

<b> Terraform Associate Certification </b>
- https://www.hashicorp.com/certification/terraform-associate
- https://www.pluralsight.com/paths/hashicorp-certified-terraform-associate

<b>Documentation</b>
- Terraform Detailed documentation : https://www.terraform.io/docs/index.html
- Getting Started with GCP : https://learn.hashicorp.com/collections/terraform/gcp-get-started
- Google configuration reference with GCP ( detailed documentation ) : https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/provider_reference
