#LAB
Google Cloud Fundamentals: Getting Started with GKE

##OBJECTIVES


- In this lab, you learn how to perform the following tasks:



- Provision a Kubernetes cluster using Kubernetes Engine.



- Deploy and manage Docker containers using kubectl.


##STEP


1 .  **Confirm that needed APIs are enabled**

- View the list of enabled APIs

	-Kubernetes Engine API

	-Container Registry API
		
		gcloud services list --available

-If either API is missing:
	


- Run the code below to enable Kubernetes Engine API

		gcloud services enable container.googleapis.com



- Run the code below to enable Container Registry API

		gcloud services enable containerregistry.googleapis.com


2 . **Start a Kubernetes Engine cluster**





- For convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE.

	
		export MY_ZONE=

- Followed by the zone that Qwiklabs assigned to you. Your complete command will look similar to this:


		export MY_ZONE=us-central1-a


-  Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:

	
		gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

It takes several minutes to create a cluster as Kubernetes Engine provisions virtual machines for you



-  After the cluster is created, check your installed version of Kubernetes using the kubectl version command:

	
		kubectl version



- View your running nodes:

		gcloud compute instances list

3 . **Run and deploy a container**

	
- launch a single instance of the nginx container. (Nginx is a popular web server.)

	
		kubectl create deploy nginx --image=nginx:1.17.10

Note: If you see any deprecation warning about future version you can simply ignore it for now and can proceed further.

- View the pod running the nginx container:

		kubectl get pods



- Expose the nginx container to the Internet:

		kubectl expose deployment nginx --port 80 --type LoadBalancer


- View the services

		kubectl get services

It may take a few seconds before the External-IP field is populated for your service. This is normal. Just re-run the kubectl get services command every few seconds until the field is populated.

- Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

- Scale up the number of pods running on your service:


		kubectl scale deployment nginx --replicas 3

- Confirm that Kubernetes has updated the number of pods:

		kubectl get pods

- Confirm that your external IP address has not changed:

		kubectl get services	




- Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.

**Congratulations!**

In this lab, you configured a Kubernetes cluster in Kubernetes Engine. You populated the cluster with several pods containing an application, exposed the application, and scaled the application.

**End your lab**

















