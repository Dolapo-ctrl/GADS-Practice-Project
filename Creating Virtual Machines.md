#LAB
CREATING VIRTUAL MACHINES

##OBJECTIVES
In this lab, you explore the available options for VMs and see the differences between locations.

In this lab, you learn how to perform the following tasks:



- Create several standard VMs



- Create advanced VMs

##STEPS

**1. Create a utility virtual machine using the cloud console**



- Examine the different machine type options:

		gcloud compute machine-types list

- Create vm with specifications on Region,Zone,Machine type, External I.P address:



		gcloud compute instances create <YOUR_VM_NAME> --zone=us-central1-c --machine-type=n1-standard-1 --subnet=default --no-address
	Replace < YOUR_VM_NAME > with a desired name for your instance. 
	Example:

		gcloud compute instances create utility-vm --zone=us-central1-c --machine-type=n1-standard-1 --subnet=default --no-address

- Explore the VM details:

		gcloud compute instances describe utility-vm --zone us-central1-c

- Explore the VM Logs:

		gcloud logging read utility-vm 

**2. Create a Windows virtual machine**

- Create vm with specifications on Region,Zone,Machine type,BootDisk:

		gcloud compute instances create windows-vm --zone=europe-west2-a --machine-type=n1-standard-2 --subnet=default --boot-disk-size=100GB --boot-disk-type=pd-standard --image=windows-server-2016-dc-core-v20200813 --image-project=windows-cloud --tags=http,https

		gcloud compute firewall-rules create default-allow-http --action=ALLOW --direction=INGRESS --rules=tcp:80 --target-tags=http

		gcloud compute firewall-rules create default-allow-https --action=ALLOW --direction=INGRESS --rules=tcp:443 --target-tags=https

	When the VM is running, notice that the connection option in the far right column is RDP, not SSH. RDP is the Remote Desktop Protocol. You would need the RDP client installed on your local machine to connect to the Windows desktop.

	you will not be connecting to the Windows VM during this lab. However, you will step through the usual procedures up to the point of requiring the RDP client.


- **Set the password for the VM**

	Access the windows VM instance details:

		gcloud compute instances describe windows-vm --zone europe-west2-a


	Set windows password to log in to the windows vm:

		gcloud compute reset-windows-password windows-vm --zone europe-west2-a

	You will not connect to the Windows VM during this lab.However, the process would look something like the following
	
	
	On the VM instances page, you would click RDP for your Windows VM and connect with the password copied earlier.
		
3. **Create a custom virtual machine**

	Create vm with specifications on Region,Zone,Machine type,cores,memory:

		gcloud compute instances create custom-vm --zone "us-west1-b" --machine-type "custom-6-32768"


	Connect via SSH to your custom VM:

		gcloud compute ssh custom-vm --zone us-west1-b

	To see information about unused and used memory and swap space on your custom VM,tun the following command:

		free

	To see details about the RAM installed on your VM, run the following command:

		sudo dmidecode -t 17		

	To verify the number of processors, run the following command:

		nproc

	To see details about the CPUs installed on your VM, run the following command:

		lscpu

	To exit the SSH terminal, run the following command:

		exit

4. In this lab, you created several virtual machine instances of different types with different characteristics. One was a small utility VM for administration purposes. You also created a standard VM and a custom VM. You launched both Windows and Linux VMs and deleted VMs.

**End your lab**