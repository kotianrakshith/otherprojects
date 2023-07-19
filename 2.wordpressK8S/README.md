# **Deploy wordpress with MySQL using Kubernetes(using NFS server, Persistent volumes, ConfigMap, Secrets)**

Steps:

## **1.Configure and setting up  the NFS-server :**

First we create required directories:

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.001.png)

Then we install the server :

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.002.png)

Then we edit the /etc/exports file to modify and add the file systems that can be exported:

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.003.png)

Then we change the required group and permission for these file directories:

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.004.png)

Then we restart the server:

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.005.png)

In one of the worker node we install the nfs-common

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.006.png)

## **2.Creating and verifying the PV :**

Let create PV :

For the pv we will use below yaml code: _**pv.yaml**_

<https://github.com/kotianrakshith/otherprojects/blob/main/2.wordpressK8S/pv.yaml>

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.007.png)

Create another pv:_ **pv2.yaml**_

<https://github.com/kotianrakshith/otherprojects/blob/main/2.wordpressK8S/pv2.yaml>

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.008.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.009.png)

## **3. Create pvc for both mysql and wordpress:**

Before that first lets create the namespace for our new deployment

`kubectl create ns cep-project1`

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.010.png)

Lets create pvc for mysql: _**mysqlpvc.yaml**_

<https://github.com/kotianrakshith/otherprojects/blob/main/2.wordpressK8S/mysqlpvc.yaml>

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.011.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.012.png)

Similarly for Wordpress

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.013.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.014.png)

Lets check the pvc

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.015.png)

Now check the pv:

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.016.png)

## **4. Creating a secret for MySQL deployment:**

Now lets create secret: _**secret.yaml**_

<https://github.com/kotianrakshith/otherprojects/blob/main/2.wordpressK8S/secret.yaml>

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.017.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.018.png)

Now create  msql deployment file : _**mysql.yaml**_

<https://github.com/kotianrakshith/otherprojects/blob/main/2.wordpressK8S/mysql.yaml>

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.019.png)

## **5.Creating a configmap for WordPress Deployment**

Let create the Yaml file: _**config.yaml**_

<https://github.com/kotianrakshith/otherprojects/blob/main/2.wordpressK8S/config.yaml>

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.020.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.021.png)

Now create wordpress deployment using configmap: _**wp.yaml**_

<https://github.com/kotianrakshith/otherprojects/blob/main/2.wordpressK8S/wp.yaml>

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.022.png)

## **6. Deploy the application and test the application:**

Deploy mysql:

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.023.png)

Now also deploy wordpress

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.024.png)

Now we need to expose both the deployment to create service

`kubectl expose deployment mysql --port=3306 -n cep-project1`

`kubectl expose deployment wordpress --port=80 -n cep-project1`

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.025.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.026.png)

Change the Service type for both MySQL and WordPress from ClusterIP to Nodeport.

`kubectl edit svc mysql -n cep-project1`

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.027.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.028.png)

`kubectl edit svc wordpress -n cep-project1`

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.029.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.030.png)

Now check all the resorce under the namespace cep-project1

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.031.png)

Now we enter the IP in the browser to check the if the deployment was successful:

_Internal-IP:port_

[*http://172.31.62.159:32500*](http://172.31.62.159:30817 "http://172.31.62.159:30817")

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.032.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.033.png)

![](/2.wordpressK8S/readmeimages/Aspose.Words.991ba115-e2d5-4505-8a72-19a359411fd9.034.png)

As you can see the wordpress service is accessible and working correctly.


