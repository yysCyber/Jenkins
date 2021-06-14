# Task - Part 1



Name: Yuan Yueshun

Faculty: 503

Group: 555амнfj



Note: 

My blog (Language: Chinese) about Jenkins: [https://www.jianshu.com/nb/49941994](https://www.jianshu.com/nb/49941994)

GitHub: [https://github.com/yysCyber](https://github.com/yysCyber)



## 1. Environment

- Windows 10
- VMware Workstation 16 Pro
- CentOS 7
- MobaXterm
- etc.



## 2. Content

Part 1：

- 2.1. Preparation before installing Jenkins.
- 2.2. Install Jenkins.
- 2.3. Basic operations of Jenkins.
- 2.4. Plugins of Jenkins.

Part 2:

- 2.5. Job of Jenkins.
- 2.6. SSH of Jenkins.
- 2.7. Node of Jenkins.
- 2.8. Git of Jenkins.



### 2.1. Preparation before installing Jenkins

#### 2.1.1. Install JDK

Jenkins is an open-source software of CI&CD. It is based on Java. So we should install JDK at first.

According to the offical document, the best choice is JDK 8. Both Oracle JDK 8 and OpenJDK 8 are OK.

I select Oracle JDK 8 (JDK from Oracle offical website).

- Step 1: 

  Downlond JDK 8 from Oracle offical website and then upload to the Linux. Or just use `wget` command (Get `.tar.gz`package).

- Step 2:

  Unzip the package to the directory that you select. I select `/usr/local/jdk8`.

- Step 3:

  Use `vim` command to edit `/etc/profile`. Append the following at last:

  ```shell
  # Environment variables
  export JAVA_HOME=/usr/local/jdk8
  export PATH=$JAVA_HOME/bin:$PATH
  ```

- Step 4:

  Save and exit from `/etc/profile`, use `source /etc/profile` command to make the environment variables take effect.

- Step 5:

  Use `javac` and `java -version` command to verify that the installation is successful.



#### 2.1.2. Install Git

Git is very import and necessary in software development.

Jenkins can deploy automatically when you submit codes by Git.

- Step 1:

  Use `yum` command to install Git

  ```shell
  yum -y install git
  ```

- Step 2:

  Use `rpm` or `whereis` command to verify that the installation is successful.

  ```shell
  rpm -q -i git
  ```

  ![rpm](.\img\1.jpg)

  

  ```shell
  whereis git
  ```

  ![whereis](.\img\2.jpg)



#### 2.1.3. Install Tomcat

The target of installing Tomcat is helping us understand Jenkins CI&CD, installing *Apache HTTP Server* or other server softwares is also OK.

- Step 1: 

  Downlond Tomcat 8 (The version is suitable for JDK) from offical website and then upload to the Linux. Or just use `wget` command (Get `.tar.gz`package).

- Step 2:

  Unzip the package to the directory that you select. I select `/usr/local/tomcat8`.

- Step 3:

  Config the firewall. Open 8080 port to the public.

  ```shell
  # Open 8080 port
  firewall-cmd --zone=public --add-port=8080/tcp --permanent
  
  # Restart firewall
  systemctl restart firewalld
  ```

  ![firewall](.\img\3.jpg)

  

- Step 4:

  Start Tomcat server using `%TOMCAT_PATH%/bin/startup.sh`:

  ![Tomcat](.\img\4.jpg)

  

- Step 5:

  Open the browser and input `http://ip:8080`:

  ![Tomcat](.\img\5.jpg)

  

### 2.2.  Install Jenkins

There are many methods that install Jenkins in Linux ([https://www.jenkins.io/doc/book/installing](https://www.jenkins.io/doc/book/installing)). I select using WAR package because it is simple.

- Step 1:

  Downlond Jenkins war package (The best version is LTS) from offical website ([https://www.jenkins.io/download](https://www.jenkins.io/download)) and then upload to the Linux. Or just use `wget` command.

  

- Step 2:

  Use `java -jar` command to execute WAR package:

  ```shell
  # nohup: No hang up
  # --httpPort=port: Choose a free port
  # >: Output redirect
  # 2>&1: All output include error
  # &: Run as the background process
  
  nohup java -jar war_package_path --httpPort=port > log_file_path 2>&1 &
  
  # example
  nohup java -jar /usr/local/jenkins/jenkins.war --httpPort=8777 > /usr/local/jenkins/jenkins_open.log 2>&1 &
  ```

  ![Run Jenkins](.\img\6.jpg)

  

- Step 3:

  Wait a moment, open the log file. If it has error, you can see the information about errors in the log. If there is no error, find the initial password in the log:

  ![Log](.\img\7.jpg)

  

- Step 4:

  Config the firewall. Open the port that you choose to the public:
  
  ```shell
  # Open 8777 port
  firewall-cmd --zone=public --add-port=8777/tcp --permanent
  
  # Restart firewall
  systemctl restart firewalld
  ```
  
  
  
- Step 5:

  Open the browser and input `http://ip:port` (example: `http://192.168.3.43:8777`), input initial password, then click "Continue" button:

  ![](.\img\8.jpg)

  

- Step 6:

  The best choice is "Install suggest plugins", click it and wait for finishing installing plugins:

  ![](.\img\9.jpg)

  

  ![](.\img\10.jpg)

  

- Step 7:

  Cteate a user as administrator, then click the blue button at bottom:

  ![](.\img\11.jpg)

  

- Step 8:

  Config interface, default is OK, then click the blue button at bottom:

  ![](.\img\12.jpg)

  

- Step 9:

  Install successfully, click "Start using Jenkin":

  ![](.\img\13.jpg)

  

  ![](.\img\14.jpg)



### 2.3. Basic operations of Jenkins

#### 2.3.1. Start Jenkins

Use `java -jar` command:

```shell
java -jar war_package_path
```

```shell
# The best choice
nohup java -jar war_package_path --httpPort=port > log_file_path 2>&1 &
```



#### 2.3.2. Restart Jenkins

Input `http://ip:port/restart` (example: `http://192.168.3.43:8777/restart`), then ask you if Jenkins restarts, click "Yes" button:

![](.\img\15.jpg)



![](.\img\16.jpg)



#### 2.3.3. Stop Jenkins

Input `https://ip:port/exit`(example: `http://192.168.3.43:8777/exit`),  then click "RETRY USE POST" button in the page:

![](.\img\17.jpg)



### 2.4. Plugins of Jenkins

The plugins are powerful in Jenkins.



Install plugins:

- Step 1:

  Click "Manage Jenkins" in the main page of Jenkins, or input `http://ip:port/manage` (example: `http://192.168.3.43:8777/manage`):

  ![](.\img\18.jpg)

  

- Step 2:

  Click "Manage Plugins", or input `http://ip:port/pluginManager` (example: `http://192.168.3.43:8777/pluginManager`):

  ![](.\img\19.jpg)

  

- Step 3:

  Click "Available" tab, fill the name of plugins that you want to install in the *search* input:

  ![](.\img\20.jpg)

  

- For example, install "Green ball":

  ![](.\img\20.jpg)

  

  ![](.\img\22.jpg)