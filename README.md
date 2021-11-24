# Google Cloud Platform - App Dev - Setting up a Development Environment: Node.js, Java, Python
### Google Cloud Platform
Google Cloud Platform (GCP) consists of a set of physical assets, such as computers and hard disk drives, and virtual resources, such as virtual machines (VMs), that are contained in Google's data centers around the globe. Each data center location is in a global region. Regions include Central US, Western Europe, and East Asia. Each region is a collection of zones, which are isolated from each other within the region. Each zone is identified by a name that combines a letter identifier with the name of the region. For example, zone a in the East Asia region is named asia-east1-a.</br>
This distribution of resources provides several benefits, including redundancy in case of failure and reduced latency by locating resources closer to clients. This distribution also introduces some rules about how resources can be used together.
### Projects
Any GCP resources that you allocate and use must belong to a project. You can think of a project as the organizing entity for what you're building. A project is made up of the settings, permissions, and other metadata that describe your applications. Resources within a single project can work together easily, for example by communicating through an internal network, subject to the regions-and-zones rules. The resources that each project contains remain separate across project boundaries; you can only interconnect them through an external network connection.</br>
Each GCP project has: A project name, which you provide. A project ID, which you can provide or GCP can provide for you. A project number, which GCP provides. As you work with GCP, you'll use these identifiers in certain command lines and API calls.</br>
The Google Cloud Platform Console displays project name, ID and number under Home > Dashboard.</br>
Each project ID is unique across GCP. Once you have created a project, you can delete the project but its ID can never be used again.</br>
When billing is enabled, each project is associated with one billing account. Multiple projects can have their resource usage billed to the same account.</br>
A project serves as a namespace. This means every resource within each project must have a unique name, but you can usually reuse resource names if they are in separate projects. Some resource names must be globally unique. Refer to the documentation for the resource for details.</br>
### Ways to interact with the services
GCP gives you three basic ways to interact with the services and resources.
- Google Cloud Platform Console: a web-based, graphical user interface that you can use to manage your GCP projects and resources.
- Command-line interface
    - Google Cloud SDK: provides the gcloud command-line tool, which gives you access to the commands you need.
    - Cloud Shell: a browser-based, interactive shell environment for GCP. You can access Cloud Shell from the GCP console. If you prefer to work in a terminal window, the Google Cloud SDK provides the gcloud command-line tool, which gives you access to the commands you need. The gcloud tool can be used to manage both your development workflow and your GCP resources. See the gcloud reference for the complete list of available commands.
- Client libraries: The Cloud SDK includes client libraries that enable you to easily create and manage resources. GCP client libraries expose APIs to provide access to services and resource management functions. You also can use the Google API client libraries to access APIs for products such as Google Maps, Google Drive, and YouTube.

## Setting up a Development Environment: Node.js
We will
- Provision a Google Compute Engine instance.
- Connect to the instance using SSH.
- Install software on the instance.
- Verify the software installation.

### Task 1: Create a Compute Engine Virtual Machine instance
In this section, you use the Google Cloud Platform Console to provision a new Google Compute Engine virtual machine (VM) instance.
- In the **Cloud Platform Console**, on the **Navigation menu**, select **Compute Engine > VM instances**.
- On the **VM Instances** dialog, click **Create**.

![a1](https://user-images.githubusercontent.com/73010204/143005717-5aef8a4e-33b9-46b8-9e2a-fcdf52805c51.png)
- On the **Create an instance** dialog:
    - Name the instance _dev-instance_.
    - Set the **Region** to _us-central1_.
    - Set the **Zone** to _us-central1-a_.
     GCP Regions and Zones: Google Cloud Platform offers products and services in multiple distinct geographic locations, called regions.
    Each region has multiple distinct zones. Each zone is isolated from other zones in terms of power and internet connectivity.
- In the **Identity and API access > Access Scopes** section, select **Allow full access to all Cloud APIs**.
- In the **Firewall** section, enable **Allow HTTP traffic**.
- Leave the remaining settings as their defaults, and click **Create**.

![a2](https://user-images.githubusercontent.com/73010204/143005966-bd7d925a-1284-4dc8-8076-d3ff95a34801.png)
- On the **VM instances** dialog, in the row for the **dev-instance**, click **SSH** (in the Connect column).
This launches a browser-hosted SSH session. If you have a popup blocker, you may need to click twice.
There's no need to configure or manage SSH keys.
![a3](https://user-images.githubusercontent.com/73010204/143006282-215b35ba-7a48-4927-ae85-45dc1fa2ebd3.png)

### Task 2: Install software on the VM instance
In this section, you use the SSH session to install software on your VM instance.</br>
In the SSH session, to update the Debian package list, execute the following command:
```sh
sudo apt-get update
```
To install Git, execute the following command:
```sh
sudo apt-get install git
```
If prompted, press _Y_ then **Enter** to continue.</br>
To download the Node.js setup script, execute the following command:
```sh
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
```
To install Node Package Manager (npm) and Node.js, execute the following command:
```sh
sudo apt install nodejs
```
### Task 3: Configure the VM to Run application software
In this section, you verify the software installation and run some sample codes.</br>
To check the version of Node.js, execute the following command:
```sh
node -v
```
You should see the Node.js version 12.x.x.</br>
![a4](https://user-images.githubusercontent.com/73010204/143006698-54ec7671-6b6a-4575-ac65-f4ca3c2b809e.PNG)</br>
To clone the class repository, execute the following command:
```sh
git clone https://github.com/GoogleCloudPlatform/training-data-analyst
```
Create a soft link as a shortcut to the working directory.
```sh
ln -s ~/training-data-analyst/courses/developingapps/v1.2/nodejs/devenv ~/devenv
```
Navigate to the directory that contains the sample files for this lab, execute the following command:
```sh
cd ~/devenv
```
To run a simple web server, execute the following command:
```sh
sudo node server/app.js
```
Return to the Cloud Console VM instances list, and click on the External IP address for the dev-instance.</br>
![a5](https://user-images.githubusercontent.com/73010204/143007035-b3617590-2d61-4b65-96a2-7047994e551a.png)</br>
A browser tab opens to display a Hello GCP dev! message from Node.js.</br>
![a6](https://user-images.githubusercontent.com/73010204/143007227-8ac911af-03d7-457c-902c-956f2c3189c3.png)</br>
Return to the SSH window and stop the application by pressing **Ctrl+C**.</br>
To install the Node.js library for Compute Engine, execute the following command:
```sh
npm install
```
To run a simple Node.js application that lists Compute Engine instances, execute the following command:
```sh
node list-gce-instances.js
```

Many details about your machine should appear in the terminal window.</br>

![a7](https://user-images.githubusercontent.com/73010204/143007616-29fa0b76-a387-4bec-ba0b-72b790ec6a7e.png)</br>
</br>
**Warning**: If you try to do this on your own machine, it will not work if credentials have not been set up to access GCP on your machine.

--------------------------------------------
## Setting up a Development Environment: Java
We will
- Provision a Google Compute Engine instance.
- Connect to the instance using SSH.
- Install a Java library on the instance.
- Verify the software installation.

### Create a Compute Engine virtual machine instance
Same as Create a Compute Engine virtual machine instance with Node.js
### Install software and configure the VM instance
In the SSH session, to update the Debian package list, enter the following command:
```sh
sudo apt-get update
```
Install Java 11:
```sh
sudo apt-get install -yq openjdk-11-jdk
```
Apply workaround for certificate issue in OpenJDK 11:
```sh
sudo sed -i 's/^\(keystore\.type\s*=\s*\).*$/\1jks/' /etc/java-11-openjdk/security/java.security; sudo rm /etc/ssl/certs/java/cacerts; sudo /usr/sbin/update-ca-certificates -f
```
Install Git:
```sh
sudo apt-get install git -y
```
Install Maven:
```sh
sudo apt-get install -yq maven
```
Configure IP tables:
```sh
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
```
This command (above) to configure the IP tables redirects requests on Port 80 to Port 8080 - the Java Web application listens on Port 8080.</br<
Export the Project ID as an environment variable:
```sh
export GCLOUD_PROJECT="$(curl -H Metadata-Flavor:Google http://metadata/computeMetadata/v1/project/project-id)"
```
### Configure the VM to run application software
To check the version of Java, enter the following command:
```sh
java -version
```
Example output:
> openjdk version "11.0.6" 2020-01-14</br>
OpenJDK Runtime Environment (build 11.0.6+10-post-Debian-1bpo91)</br>
OpenJDK 64-Bit Server VM (build 11.0.6+10-post-Debian-1bpo91, mixed mode, sharing)</br>

Clone the class repository:
```sh
git clone https://github.com/GoogleCloudPlatform/training-data-analyst
```
To keep the navigation simple, create a soft link as a shortcut to the working directory:
```sh
ln -s ~/training-data-analyst/courses/developingapps/v1.2/java/devenv ~/devenv
```
Change to the directory that contains the sample files:
```sh
cd ~/devenv
```
Run a simple web application:
```sh
mvn clean install
```
Wait for the project to build. When the project successfully finishes you will see output similar to this:
> [INFO] -------------------------------------------------------</br>
[INFO] BUILD SUCCESS</br>
[INFO] -------------------------------------------------------</br>
[INFO] Total time: 24.586 s</br>
[INFO] Finished at: 2020-08-18T20:30:04+00:00</br>
[INFO] Final Memory: 34M/179M</br>
[INFO] -------------------------------------------------------</br>

Run the application.
```sh
mvn spring-boot:run
```
You may see a number of warnings, but the project is running when you can see an INFO message in the output similar to the following:
> 01:11:05.274 [restartedMain] INFO  c.g.training.appdev.DemoApplication - Started DemoApplication in 3 seconds (JVM running for 4.863)

Return to the Cloud Console VM instances list, and click on the **External IP** address for the _dev-instance_.</br>
A browser opens to display a _Hello GCP dev!_ message from Java.</br>
Return to the SSH window, and stop the application by pressing **Ctrl+C**.</br>
To run a simple Java application that lists Compute Engine instances, execute the following command:
```sh
mvn exec:java@list-gce
```
The terminal window outputs VM details.

--------------------------------------------
## Setting up a Development Environment: Python
We will
- Provision a Compute Engine instance
- Connect to the instance using SSH
- Install a Python library on the instance
- Verify the software installation

### Create a Compute Engine virtual machine instance
Same as Create a Compute Engine virtual machine instance with Node.js
### Install software on the VM instance
In the SSH session, update the Debian package list:
```sh
sudo apt-get update
```
Install Git:
```sh
sudo apt-get install git
```
When prompted, enter _Y_ to continue, accepting the use of additional disk space.
Install Python:
```sh
sudo apt-get install python3-setuptools python3-dev build-essential
```
Again, when prompted, enter _Y_ to continue, accepting the use of additional disk space.
Install pip:
```sh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
```
```sh
sudo python3 get-pip.py
```
### Configure the VM to run application software
Still in the SSH window, verify the installation by checking the Python and pip version:
```sh
python3 --version
```
```sh
pip3 --version
```
The output provides the version of Python and pip that you installed.</br>
Clone the class repository:
```sh
git clone https://github.com/GoogleCloudPlatform/training-data-analyst
```
Crete a soft link as a shortcut to hte working directory:
```sh
ln -s ~/training-data-analyst/courses/developingapps/v1.3/python/devenv ~/devenv
```
Change the directory that contains the sample files for this lab:
```sh
cd ~/devenv/
```
Run a simple web server:
```sh
sudo python3 server.py
```
Return to the Cloud Console VM instances list (**Navigation menu > Compute Engine > Virtual Instances**), and click on the **External IP address** for the dev-instance.</br>
A browser opens and displays a _Hello GCP dev!_ message from Python.</br>
Return to the SSH window, and stop the application by pressing **Ctrl+c**.</br>
Install the Python packages needed to enumerate Compute Engine VM instances:
```sh
sudo pip3 install -r requirements.txt
```
Install the Python packages needed to enumerate Compute Engine VM instances:
```sh
sudo pip3 install -r requirements.txt
```
Now list your instance in Cloud Shell. Enter the following command to run a simple Python application that lists Compute Engine instances. Replace _<PROJECT_ID>_ with your Google Cloud Project ID and _<YOUR_VM_ZONE>_ is the region you specified when you created your VM. Find these values on the VM instances dialog of the console:
```sh
python3 list-gce-instances.py <PROJECT_ID> --zone=<YOUR_VM_ZONE>
```
Your instance name shows in the SSH terminal window.

--------------------------------------------
## Congratulations!
You learned how to provision a Google Compute Engine virtual machine and install software libraries for Node.js, Java, Python software development on Google Cloud Platform.

## Reference
**Google Cloud Fundamentals: Getting Started With Application Development** course
https://www.coursera.org/learn/getting-started-app-development/home/welcome
