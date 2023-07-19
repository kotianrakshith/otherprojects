# **Deploy Kubernetes Dashboard**

Steps:

## **Deploying the kubernetes dashboard and verifying the service:**

To deploy the dashboard we use the below command:

`kubectl apply -f  https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml`

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.001.png)

Once the installation is done, check the resources that it deployed, like pods, service and deployment

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.002.png)

Now change the service type to Nodeport:

`kubectl edit svc -n kubernetes-dashboard kubernetes-dashboard`

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.003.png)

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.004.png)

Now when you check if will be changed in the service:

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.005.png)

You can check that pods are running now :

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.006.png)


## **Creating a token and working on dashboard :**

Now you can go to master node and open the desktop

Here if we open in the browser _https://localhost:NodePort_ 

For me in the node port , port number is  31535, so i will use _https://localhost:31535_

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.007.png)

Once you proceed with as suggested, it will ask for a token.

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.008.png)

You can generate token with below command

```
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | awk '/^deployment-controller-token-/{print $1}') | awk '$1=="token:"{print $2}'
```

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.009.png)

Once you paste this command you will be able to access:

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.010.png)

Add new cluster role bindig:

`kubectl get sa -n kubernetes-dashboard`

`kubectl get clusterrolebindings`

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.011.png)

Now delete the old one and create a new one :

![](/6.k8s_dashboard/readmeimages/Aspose.Words.127c8a51-c8f0-4ecc-8e5d-bd861e9df0c5.012.png)

Now you can see new one is created. This shoud be sufficient for you to start working in the dashboard.

