# **Deployment of Flask Application with Redis using Kubernetes**

## **1. Create a dockerfile using simple python app file**

`vim app.py `

Code: <https://github.com/kotianrakshith/otherprojects/blob/main/5.flask_redis_k8s/app.py>


![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.001.png)

`vim Dockerfile`

<https://github.com/kotianrakshith/otherprojects/blob/main/5.flask_redis_k8s/Dockerfile>

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.002.png)

Remember to create _requirements.txt_ in the same directory

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.003.png)

## **2. Build the docker image and push it to docker repository:**

`docker build -t flask_image .`

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.004.png)

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.005.png)

Now tag the image in the format it needs to be for it to send to dockerhub

`docker tag flask_image:latest kotianrakshith/flask-image:flask_image_for_redis`

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.006.png)

Now connect to your docker, Im using token for login (can be logged in throgh password too)

In password provide your personal access token

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.007.png)

Now to push use command: `docker push kotianrakshith/flask-image:flask_image_for_redis`

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.008.png)

## **3. Create the Redis and Flask deployment in kubernetes** 

Create redis.yaml file 

`vim redis.yaml`

[*https://github.com/kotianrakshith/otherprojects/blob/main/5.flask_redis_k8s/redis.yaml*](https://github.com/kotianrakshith/otherprojects/blob/main/5.flask_redis_k8s/redis.yaml "https://github.com/kotianrakshith/otherprojects/blob/main/5.flask_redis_k8s/redis.yaml")

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.009.png)

create redis deployment using command: 

`kubectl apply -f redis.yaml`

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.010.png)

Now we create simiarly flask deployment using the image created

`vim flask.yaml`

<https://github.com/kotianrakshith/otherprojects/blob/main/5.flask_redis_k8s/flask.yaml>

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.011.png)

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.012.png)

## **4. Create service for Redis and Flask Services:**

You can either create a yaml manifest file for service or you can use command kubectl expose deployment

`kubectl expose deployment redis --port=6379`

`kubectl expose deployment flask --port=5000`

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.013.png)

Now check the service using `kubectl get svc` command:

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.014.png)

## **5. Now verify if the application is correctly deployed using curl command:**

_curl clusterip:port (curl 10.97.210.176:5000)_

![](/5.flask_redis_k8s/readmeimages/Aspose.Words.cef84478-4759-4a50-9f94-1609ae52515c.015.png)

As you can see the count is displayed and increasing as we use it multiple times.


