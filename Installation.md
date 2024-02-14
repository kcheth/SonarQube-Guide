## Step 1: Prerequisites

Before installing SonarQube, make sure your system meets the following requirements:
- Operating System: Linux
- Allocate a minimum of 2GB of RAM for SonarQube, with an additional 1GB of free RAM for the operating system. (If using AWS, consider a t2.medium instance.)
- Verify that the installed Java version meets the requirements. (This document was prepared with Java 17.)

For more detailed information about prerequisites, please refer to the [SonarQube Prerequisites](https://docs.sonarsource.com/sonarqube/latest/requirements/prerequisites-and-overview/)

## Step 2: Installation

1. Download and Extract SonarQube:
   Open a terminal and execute the following commands:
   ```
   sudo su -
   cd /opt
   yum install wget unzip -y
   wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.3.79811.zip_gl=1*19ipoye*_gcl_au*Nzc2NTAxNTg3LjE3MDUwNDQ2NTg.*_ga*MTI3NjA1MjQ1NS4xNzA1MDQ0NjU4*_ga_9JZ0GZ5TC6*MTcwNTA1Mzc4Mi4yLjEuMTcwNTA1NjA0OS40Ny4wLjA.
   unzip sonarqube-9.9.3.79811.zip
   ```
2. Create a New User for SonarQube:
   ```
   useradd sonar
   visudo
   ```
3. Change Permissions:
   ```
   chown -R sonar:sonar /opt/sonarqube-9.9.3.79811.zip/
   chmod -R 775 /opt/sonarqube-9.9.3.79811.zip/
   ```
4. Start SonarQube:
   ```
   su - sonar
   cd /opt/sonarqube-7.8/bin/linux-x86-64/
   ./sonar.sh start
   ./sonar.sh status
   ```
### Troubleshooting:
If you encounter issues while setting up SonarQube, consider these solutions:

- Ensure the /opt/sonarqube-9.9.3.79811/ directory's ownership and permissions are set for the sonar user.
- Make sure you start the SonarQube service using the sonar user.
- Ensure the correct version of Java is installed as per the requirements. 

### Access SonarQube
Once SonarQube is running, access it through your web browser by visiting <http://your-server-ip:9000.> If you're using AWS EC2, make sure port 9000 is open in your security group settings.

## Step 3: Configure SonarQube as a Service
1. Create a Symbolic Link:
   ```
   ln /opt/sonarqube-9.9.3.79811.zip/bin/linux-x86-64/sonar.sh /etc/init.d/sonar
   ```
2. Edit the Service File:
   ```
   vi /etc/init.d/sonar
   ```
Insert the following lines into the file. These lines are designed to define environment variables and configurations for running SonarQube as a service. Please add these lines immediately after the shebang `(#!/bin/bash)`, and the rest of the code will remain unchanged.
  ```
SONAR_HOME=/opt/sonarqube-9.9.3.79811
PLATFORM=linux-x86-64

WRAPPER_CMD="${SONAR_HOME}/bin/${PLATFORM}/wrapper"
WRAPPER_CONF="${SONAR_HOME}/conf/wrapper.conf"
PIDDIR="/opt/sonarqube-9.9.3.79811/"
```

After completing this step, when attempting to enable/start the service, you may encounter an issue related to systemd while trying to run SonarQube as a system service using a service manager like systemd. In such a scenario, please refer to the document [Running SonarQube as a service on Linux with systemd ](https://docs.sonarsource.com/sonarqube/9.9/setup-and-upgrade/configure-and-operate-a-server/operating-the-server/)

On a Unix system using systemd, you can install SonarQube as a service. You cannot run SonarQube as root in Unix systems. Ideally, you will have created a new account dedicated to the purpose of running SonarQube. Let's suppose:
- The user used to start the service is `sonar`
- The group used to start the service is `sonar`
- The Java Virtual Machine is installed in `/opt/java/`
- SonarQube has been unzipped into `/opt/sonarqube/`

Then create the file `/etc/systemd/system/sonarqube.service` based on the following:
```
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=simple
User=sonar
Group=sonar
PermissionsStartOnly=true
ExecStart=/bin/nohup /opt/java/bin/java -Xms32m -Xmx32m -Djava.net.preferIPv4Stack=true -jar /opt/sonarqube/lib/sonar-application-sonarqube-9.9.3.79811.jar
StandardOutput=journal
LimitNOFILE=131072
LimitNPROC=8192
TimeoutStartSec=5
Restart=always
SuccessExitStatus=143

[Install]
WantedBy=multi-user.target
```
Ensure to modify the 'User' and 'Group' names, and set the accurate path for the .jar file in the 'ExecStart' parameter.

### Enable and Start the Service:
```
sudo systemctl daemon-reload  # Reload systemd manager configuration to apply changes in unit files
sudo systemctl enable sonar
sudo systemctl start sonar
```

### Check Service Status:

```
sudo systemctl status sonar
```

## NOTE:
Running SonarQube "as a service" using a service manager (like systemd) and starting/stopping it using `./sonar.sh` are different approaches to managing the SonarQube application.

- #### Running as a service:
  This typically involves creating a systemd service unit  that defines how SonarQube should be started, stopped, and managed by the system. The service manager takes care of starting SonarQube during system boot, stopping it during shutdown, and managing its lifecycle.

- #### Starting/Stopping with ./sonar.sh:
  This approach involves manually running the `sonar.sh` script, which is provided by SonarQube, to start and stop the SonarQube application. When you run `./sonar.sh` start, it starts the application, and when you run `./sonar.sh` stop, it stops the application.

The former method is generally preferred for production environments, as it allows for better integration with the system and provides more control and automation. The latter method is useful for development and testing environments, where you might want to start and stop SonarQube manually for specific purposes.

If you're having issues with the service configuration, ensure that the paths and configurations in your systemd unit file are correctly set to match your SonarQube installation.

### Conclusion:
By following this guide, you've successfully installed and configured SonarQube to manage code quality efficiently. SonarQube helps you identify code issues, enforce best practices, and maintain a high level of code quality throughout your development process. This foundation will empower your team to deliver robust and reliable software.







