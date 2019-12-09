Wordpress application on local machine in a kubernetes 

I use MacOs for Local Machine


STEP 1 : (First install Kubectl using CURL or Brew)


Download the latest release of kubectl:

	# curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl"


Make the kubectl binary executable.

	# chmod +x ./kubectl


Move the binary in to your PATH.

	# sudo mv ./kubectl /usr/local/bin/kubectl

Or 
	(
		 Run the kubectl installation command

 			# brew install kubectl 
  		or
   			# brew install kubernetes-cli

	)

 Check kubectl installed or not

    # kubectl version


STEP 2: (Install Minikube)


	1.	First we have to check for Virtulization is supported or not in Macbook. 
		For that run this command 

		# sysctl -a | grep -E --color 'machdep.cpu.features|VMX'    

		(output VMX should be coloured, if not then virtulization is not supported)
 
	2. Install a Hypervisor (I use VirtuaBox for Hypervisor)


	3. Install Minikube.

	  Using Homebrew

	   # brew install minikube

	   or

      Download using a stand-alone binary:

      # curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64 \
        && chmod +x minikube

      add the Minikube executable to your path:

	  # sudo mv minikube /usr/local/bin

	4. Confirm Installation.

	 1. ( minikube start --vm-driver=<driver_name> )   

	  i use virtuabox so i run above command by adding driver name VirtualBox : 

	  		# minikube start --vm-driver=virtualbox

	 2. confirm successful installation of both a hypervisor and Minikube

	 		# minikube status

	    (Output will be similar to this)

	    	host: Running
			kubelet: Running
			apiserver: Running
			kubeconfig: Configured


STEP 3: Set-up a Mysql DB Server in a POD and a Wordpress Application in another POD inside Minikube:


	     Create a folder (ex: wp-mysql)
	     # cd wp-mysql/

	     1. Create a kustomization.yaml  ("Secret" object that stores sensitive data like a password)

	     2. Create Mysql yaml file 

	         mysql-deployment.yaml

	     3. Create Wordpress yaml file 
	     
	     	wordpress-deployment.yaml 

	     4. Add both the MySql and Wordpress yaml file in kustomization.yaml file

	     	(kustomization.yaml contains all the resources for deploying a WordPress site and a MySQL database)


Step 4: Apply and Verify


			# kubectl apply -k ./      (Apply and verify all the yaml)

		Check that the Secret exists

			# kubectl get secrets

		Check that a PersistentVolume got dynamically provisioned

			# kubectl get pvc

		Check that the Pod is running

			# kubectl get pods

		Check that the Service is running
		
			# kubectl get services wordpress


Step 5: Check the application is working or not 
 
 		(This command shows the Url and you can copy paste that url in your browser to check if the application is working or not)

 		#   minikube service wordpress --url













	
