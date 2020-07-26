### Aim:

Installation and Configuration of Jenkins

### Procedure and Screenshots.

Jenkins is an open source automation server that has become a crucial component in the likes of Kubernetes and GitOps. Jenkins enables the continuous integration and delivery of software. Jenkins includes a number of plugins to help the automation of building and deploying your applications.

Steps for Installation:

1. First of all, jenkins **needs** jdk, so on ubuntu vm of ours go ahead and issue:

```

sudo apt update && sudo apt install default-jdk

#if on ubuntu server, default-jdk-headless

#Once the installation finishes check the java version by,

java -version.
```

![Java Installation](Devops-Study.Cheese_Thu-16Apr20_06.56.png)

2. Download and install the necessary GPG key with the command

```

wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
```

3. Add the necessary repository with the command

```

sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

4. Add the universe repository with the command

```

sudo add-apt-repository universe
```

5. Update apt with the command ```sudo apt-get update```

6. Install Jenkins with the command

```

sudo apt-get install jenkins -y
```

Allow the installation to complete.

![Jenkins installation](Devops-Study.Cheese_Thu-16Apr20_07.04.png)

#### How to access Jenkins?

1. Open a web browser and point it to http://SERVER_IP:8080 (where SERVER_IP is the IP address of the hosting server).

2. You will then be prompted to copy and paste a password that was created during the Jenkins installation. To retrieve that password, go back to the terminal window and issue the command:

```

sudo less /var/lib/jenkins/secrets/initialAdminPassword
```

![Getting the password](Devops-Study.Cheese_Thu-16Apr20_07.24.png)

![jenkins Unlock page](Devops-Study.Cheese_Thu-16Apr20_07.26.png)

![Cat password pewpew](Devops-Study.Cheese_Thu-16Apr20_07.31.png)

![jenkins Start Page](Devops-Study.Cheese_Thu-16Apr20_07.27.png)

Choose suggested plugins and then

Create the first user

![Creation of user.](Devops-Study.Cheese_Thu-16Apr20_07.41.png)

Set the deafult path and you will be set to roll with jenkins.

![First page](Devops-Study.Cheese_Thu-16Apr20_07.42.png)

### Testing java applications on jenkins.

![Java Application testing](Devops-Study.Cheese_Thu-16Apr20_07.44.png)

After correct configuration and proper build information

![Hello.java using Jenkins](Devops-Study.Cheese_Thu-16Apr20_09.05.png)

### Executing python programs using jenkins.

![Python code](Devops-Study.Cheese_Thu-16Apr20_09.28.png)

![Python Jenkins](Devops-Study.Cheese_Thu-16Apr20_09.30.png)

![python code running](Devops-Study.Cheese_Thu-16Apr20_09.31.png)

![Success](Devops-Study.Cheese_Thu-16Apr20_09.32.png)
