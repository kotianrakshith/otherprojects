# **Deploying a Voting Application using Kubernetes**

**For this pracitce we can create a new namespace :**

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.001.png)

The source code is available in a pub;ic github repository and so we are cloning it: 

`git clone https://github.com/dockersamples/example-voting-app.git`

 Once you clone you can go to the directory and view the files in it:

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.002.png)

If you see the folder k8s-specifications you can see that it has several yaml file for several component needed for this app to run.

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.003.png)

By running comand *`kubectl create -f k8s-specifications/`* you can create several deployment, service based on the yaml files inside the folder:

(we are using `–n vote` for it to be created in newly created namespace)

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.004.png)

**Now check all the pods in the new namspace:**

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.005.png)

**You can also see deployments**

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.006.png)

**You can also see services:**

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.007.png)

Now since our deployment is done, we can check where the result pod is running and use the IP to access this in our web browser:

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.008.png)

As result is in node 2, we can use 172.31.52.153:31001

**As you can see we can access the app:**

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.009.png)

We can also see voting app in 172.31.55.232:31000

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.010.png)

**When we vote here we should see it reflected in result page:**

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.011.png)

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.012.png)

**This means voting application has been successfully deployed and the code from github was correct.**

**Now we can delete all the deployment using command:**

`kubectl delete -n vote -f k8s-specifications/`

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.013.png)

Now you see that there is no pod, deployment, service

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.014.png)

**When you refresh in the browser you can see its not accessible anymore:**

![](/4.votingapp_k8s/readmeimages/Aspose.Words.954a6ea4-03a0-4374-acac-f8bcf514e8e3.015.png)






