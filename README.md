Are you looking forward to learn Jenkins right from Zero(installation) to Hero(Build end to end pipelines)? then you are at the right place.

Installation on EC2 Instance
Install Jenkins, configure Docker as agent, set up cicd, deploy applications to k8s and much more.

AWS EC2 Instance
Go to AWS Console
Instances(running)
Launch instances

![image](https://github.com/rnagargoje27/NewRepository/assets/138219884/585ed332-b979-4cc0-80d2-d31f7d69e563)

Install Jenkins.
Pre-Requisites:

Java (JDK)
Run the below commands to install Java and Jenkins
Install Java

sudo apt update
sudo apt install openjdk-11-jre
Verify Java is Installed

java -version
Now, you can proceed with installing Jenkins

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

EC2 > Instances > Click on
In the bottom tabs -> Click on Security
Security groups
Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).
![image](https://github.com/rnagargoje27/NewRepository/assets/138219884/bc89c363-b7d6-422e-96d0-252eb3c89127)


Login to Jenkins using the below URL:
http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password

![image](https://github.com/rnagargoje27/NewRepository/assets/138219884/1633e7f5-0279-4a6f-8abe-16b6928325ce)


Click on Install suggested plugins
![image](https://github.com/rnagargoje27/NewRepository/assets/138219884/58b2ddb6-9b4d-44ad-9c89-a32c5d9ff7ab)


Wait for the Jenkins to Install suggested plugins

![image](https://github.com/rnagargoje27/NewRepository/assets/138219884/55d70023-24ab-4266-8b45-98c9b5bb4175)


Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

![image](https://github.com/rnagargoje27/NewRepository/assets/138219884/02d94beb-21c2-4f78-bd70-a7d65d52e42b)


Jenkins Installation is Successful. You can now starting using the Jenkins

![image](https://github.com/rnagargoje27/NewRepository/assets/138219884/f2ddef83-b06c-4169-a39c-345a7faed208)


Install the Docker Pipeline plugin in Jenkins:
Log in to Jenkins.
Go to Manage Jenkins > Manage Plugins.
In the Available tab, search for "Docker Pipeline".
Select the plugin and click the Install button.
Restart Jenkins after the plugin is installed.
![image](https://github.com/rnagargoje27/NewRepository/assets/138219884/5aadc1a0-31b6-4128-93aa-da85ba43739c)


Wait for the Jenkins to be restarted.

Docker Slave Configuration
Run the below command to Install Docker

sudo apt update
sudo apt install docker.io
Grant Jenkins user and Ubuntu user permission to docker deamon.
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
Once you are done with the above steps, it is better to restart Jenkins.

http://<ec2-instance-public-ip>:8080/restart
The docker agent configuration is now successful.


