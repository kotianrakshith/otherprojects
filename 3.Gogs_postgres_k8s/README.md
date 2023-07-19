# **Deploying Multitier Application Postgres and Gogs using Kubernetes**


Please note that steps are all personally done by me, steps and templates may have been referenced from training and other sources.

## 1. Creating yaml file for postgres deployment:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.001.png)

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.002.png)

Code:

<https://github.com/kotianrakshith/otherprojects/blob/main/3.Gogs_postgres_k8s/postgres.yaml>

## 2. Create the deployment:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.003.png)

## 3. When verfying you can see the deployment and the pods created:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.004.png)

## 4. Simiary creating yaml file for gogs

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.005.png)

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.006.png)

Code: <https://github.com/kotianrakshith/otherprojects/blob/main/3.Gogs_postgres_k8s/gogs.yaml>

## 5. Creating the deployment:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.007.png)

## 6. Now verfifying the deplotment and pods:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.008.png)

## 7. Now we have to expose a service for Postgres and Gogs deployment:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.009.png) 	

## 8. Now we have to change the service type  from ClusterIP to Nodeport.(ClusterIP services expose pods to internal network traffic. NodePort services expose pods internally the same way a ClusterIP service does. In addition, a NodePort service allows external clients to access pods via network ports opened on the Kubernetes nodes. These ports are typically in the range 30000-32768, although that range is customizable.)

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.010.png)

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.011.png)

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.012.png)

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.013.png)

## 9. Verify the changes:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.014.png)

## 10. Now we check for the IP so we can chek the deployments:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.015.png)

## 11. Now we enter the IP in the browser to check the if the deployment was sucessfull:

_Internal-IP:port_ (you can also use service nodeport)

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.016.png)

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.017.png)

Then changing required fileds and click install gogs:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.018.png)

## 12. Once the installation is done, reload in fresh page and we can see that Gogs application is successfully installed and deployed.

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.019.png)

## 13. Incase you want to delete the deployment you can use the command: Kubectl delete

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.020.png)

## 14. Now if you refresh you can see that application is no more running:

![](/3.Gogs_postgres_k8s/readmeimages/Aspose.Words.aa22601a-268b-46c5-9027-2dad84deb50a.021.png)

