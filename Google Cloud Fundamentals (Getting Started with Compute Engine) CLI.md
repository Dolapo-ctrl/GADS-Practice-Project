#LAB
Google Cloud Fundamentals:Getting Started With Compute Engine

##OBJECTIVES

In this lab, you will learn how to perform the following tasks:

- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

- Create a Compute Engine virtual machine using the gcloud command-line interface.

- Connect between the two instances.

##STEPS

**1. Create a virtual machine using the GCP Console**


		gcloud compute instances create my-vm-1 --zone=us-central1-a --image-project=debian-cloud --image=debian-9-stretch-v20200902 --tags=http
		
		gcloud compute firewall-rules create allow-http --action=ALLOW --direction=INGRESS --rules=tcp:80 --target-tags=http

**2. Create a virtual machine using the gcloud command line**
	


- Display the list of zones in us-central1:

		gcloud compute zones list | grep us-central1


- Set the default zone to us-central1-b:
		
			gcloud config set compute/zone us-central1-b
 

- Create a VM instance called my-vm-2:
		
			gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

	(Note: The VM can take about two minutes to launch and be fully available for use.)

- Exit the cloud shell
		
		exit
   
**3. Connect between VM instances**
	
- Open a command prompt on my-vm-2 instance:
		
			gcloud compute ssh my-vm-2 --zone us-central1-b
- Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
		
			ping my-vm-1
- Press Ctrl+C to abort the ping command
	
- Use the ssh command to open a command prompt on my-vm-1:
		
			ssh my-vm-1
	(Result:If you are prompted about whether you want to continue connecting to a host with unknown authenticity, enter yes to confirm that you do.)

- At the command prompt on my-vm-1, install the Nginx web server:
		
			sudo apt-get install nginx-light -y

- Use the nano text editor to add a custom message to the home page of the web server:

			sudo nano /var/www/html/index.nginx-debian.html

- Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
		
			Hi from <YOUR_NAME>

- Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.
	
- Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
		
			curl http://localhost/
	(Result:The response will be the HTML source of the web server's home page, including your line of custom text.)

- Exit the command prompt on my-vm-1

		exit
	
- Confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
			
			curl http://my-vm-1/

	(Result:The response will again be the HTML source of the web server's home page, including your line of custom text.)
	
- Display the information on my-vm-1 to get and copy the external I.P address 

			gcloud compute instances list

 

- Paste it into the address bar of a new browser tab to see your web server's homepage including your custom text 

**Congratulations!**

In this lab, you created virtual machine (VM) instances in two different zones and connected to them using ping, ssh, and HTTP.

**End your lab**
		