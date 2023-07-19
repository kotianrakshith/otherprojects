# **Project: CI/CD Deployment Using Ansible CM Tool**

## **Steps Done:**

## **1. Configure Jenkins server as Ansible provisioning machine**
   
(This project was done in the lab provided simplilearn)

Considering the master in Configuration Management Lab as the Jenkins server

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.001.png)

Ansible is already installed in this machine.

Considering the worker1 in the lab as the node

In the /etc/ansible/hosts file adding this worker:

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.002.png)

Running ssh-keygen command and copying the file details to a file in node

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.003.png)

Now trying to ssh to the node

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.004.png)

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.005.png)

Trying to ping the node 

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.006.png)

We can see that it worked correctly and did not ask for any password.

## **2.  Install Ansible plugins in Jenkins CI server**

As Jenkins is not installed in this machine I’m following steps to install java jdk and jenkins from the ansible website : https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.007.png)

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.008.png)

After installing the jenkins we enabled and started the server:

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.009.png)

Now we can see that in our machine jenkins is running:

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.010.png)

Then go to jenkins portal by goining to localhost:8080 and setup the jenkins.

Once  jenkins portal opens and go to Manage jenkins and then go to manage plugins and search for Ansible plugin and install

Then go to Manage Jenkins and Global Tool Configuration so you can configure the ansible

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.011.png)

## **3. Prepare Ansible playbook to run Maven build on Jenkins CI server**

After making sure maven was insatlled I have forked a test repo required to create war file in the github from the internet. Then I prepared the Ansible playbook as below:

Playbook name: **mavenwarfile.yaml**

Link: <https://github.com/kotianrakshith/otherprojects/blob/main/1.ansibleproj/mavenwarfile.yaml>

We are not running this playbook as we have to create automated CI/CD pipeline using this playbook.

## **4. Prepare Ansible playbook to execute deployment steps on the remote web container with restart of the web container post deployment**

Before we automate the deployment for the WAR file we need to make sure that worker node is setup as tomcat web container, so we need to instal and setup tomcat in the node.


So creating playbook for that **tomcatinstall.yaml**

Link: <https://github.com/kotianrakshith/otherprojects/blob/main/1.ansibleproj/tomcatinstall.yaml>

We run this playbook to make sure that tomcat is installed and started:

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.012.png)

After this is successful let us create another playbook for deploy custom WAR files to a web container and then perform restart for the web container.

Playbook name: **deploywarfile.yaml**

Link: <https://github.com/kotianrakshith/otherprojects/blob/main/1.ansibleproj/deploywarfile.yaml>


Now that we have our two playbooks **mavenwarfile.yaml** and **deploywarfile.yaml** we can create a jenkins job to run both these playbook and automate creation of war file and also deployment of war file with restart for the web container.

First creating job for creating war file:

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.013.png)

In the build steps give the ansible command to execute in shell

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.014.png)

Now create the job for deploying and restarting;

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.015.png)

In build triggers make sure this runs after the previous job so we can automate it![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.016.png)

In build steps give invoke ansible command to execute the ansible playbook to deploy war file and restart the web container:

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.017.png)


Once the both the job are created, trigger it manually so the complete steps are performed![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.018.png)

To make sure jenkins can execute asnible commands in the shell you need to add the line 

`jenkins ALL= NOPASSWD: ALL` 

in file _/etc/sudoers_

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.019.png)

Then you run the jenkins job.  After solving any errors provided by jenkins run, it should provide the success output like this:

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.020.png)

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.021.png)

Once both the jobs are run check the webcontainer(worker node) to see if the war file is saved in the location or not.

![](/1.ansibleproj/readmeimages/Aspose.Words.92a2be4a-feb6-4e52-95c8-95e0112a1c40.022.png)

You can see that warfile has been sucessfully pasted. In the output of jenkins we can see tomcat has also been restarted and thus all the steps are completed.
