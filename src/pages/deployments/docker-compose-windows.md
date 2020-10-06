---
title: Quick start with Hypertrace on windows
weight: 8
excerpt: Quickstart with Hypertrace using docker-compose on windows
template: docs
---

Hypertrace is an open-source distributed tracing and observability platform and it finds a lot of use-cases in the modern complex microservices world. If you live in a windows world and you want to try out Hypertrace, this blog post will help you understand how to get started quickly with Hypertrace on windows.

### System Requirements
- Windows 10 64-bit: Pro, Enterprise, or Education (Build 16299 or later).
- [Hyper-V and Containers Windows features must be enabled.](https://docs.docker.com/docker-for-windows/troubleshoot/#virtualization) (There are some requirements like the 64-bit processor and 4 GB Ram for Hyper-v including enabling BIOS-level virtualization. More details about it can be found [here](https://docs.docker.com/docker-for-windows/troubleshoot/#virtualization-must-be-enabled).)
- Docker Desktop
- We recommend you change the Docker Desktop memory to a minimum of `4 GB memory` and set CPUs to at least `4 CPUs` if it's not set to that by default. (Won't be an issue with fairly spec'd machine.)

Now, let's go step by step and see how we can get Hypertrace up and running with Docker desktop on windows. 

### Step 1: Make sure you have Docker desktop installed properly. 

You can skip this step completely if you have a docker-desktop installed with Hyper-V and Containers Windows features enabled. Otherwise, follow the below steps and refer [docker docs](https://docs.docker.com/docker-for-windows/install/) for more detailed instructions.

- Double-click `Docker Desktop Installer.exe` to run the installer.
If you haven’t already downloaded the installer (Docker Desktop Installer.exe), you can get it from Docker Hub. It typically downloads to your Downloads folder, or you can run it from the recent downloads bar at the bottom of your web browser.
- When prompted, ensure the `Enable Hyper-V Windows Features option` is selected on the Configuration page.
- Follow the instructions on the installation wizard to authorize the installer and proceed with the install.
- When the installation is successful, click Close to complete the installation process.
- If your admin account is different from your user account, you must add the user to the docker-users group. Run Computer Management as an administrator and navigate to `Local Users and Groups > Groups > docker-users`. Right-click to add the user to the group. Log out and log back in for the changes to take effect.

### Step 2: Enable linux containers
In order to run Linux containers, you need to make sure Docker is using the Linux daemon. You can toggle this by selecting Switch to Linux Containers from the action menu when clicking on the Docker whale icon in the system tray. If you see Switch to Windows Containers, then you are already targeting the Linux daemon. 

| ![space-1.jpg](https://docs.microsoft.com/en-us/virtualization/windowscontainers/quick-start/media/switchdaemon.png) | 
|:--:| 
| *Switch Daemons to use Linux containers* |

### Step 3: Clone Hypertrace repo

To clone the Hypertrace repo you have to run:
```
git clone https://github.com/hypertrace/hypertrace
cd hypertrace/docker
```
### Step 4: Run docker-compose 

To pull the images required for Hypertrace let's run

```
docker-compose pull
```
| ![space-1.jpg](https://hypertrace-docs.s3.amazonaws.com/dokcer-compose-pull.png) | 
|:--:| 
| *docker-compose pull* |

Okay! As we have all things in place now, let's start Hypertrace! 

```
docker-compose -f docker-compose.yml up
```

once you see the message `started Hypertrace UI service on port 2020` like below you can visit Hypertrace UI at http://localhost:2020.

| ![space-1.jpg](https://hypertrace-docs.s3.amazonaws.com/docker-compose-up.png) | 
|:--:| 
| *docker-compose up* |

### Step 5: Sending traces with sample app

It was pretty easy to get started with Hypertrace, wasn't it? So now let's just go ahead and send some traces so we can see Hypertrace in action and explore functionalities in real! If your application is already instrumented to send traces to Zipkin or Jaeger, it will work with Hypertrace out of the box. 

Even if you don't have an application instrumented you can get started quickly with our simple sample application. To run the sample app open another window of command prompt and run 

```
docker-compose -f docker-compose-zipkin-sample.yml up 
```

the sample app will run at http://localhost:8081. You should refresh the URL a few times to generate some sample trace requests!

Now, go back to http://localhost:2020 to see insights for your application using Hypertrace. 

| ![space-1.jpg](https://hypertrace-docs.s3.amazonaws.com/ht-home-post.png) | 
|:--:| 
| *Hypertrace Dashboard* |

If you need a platform and UI overview and want to understand what information each section serves, you can read the platform and UI overview [here](https://docs.hypertrace.org/platform-ui/). 

##### In a nutshell,

You can run Hypertrace on Windows in 4 easy steps (if you have docker desktop installed!) and start exploring it right away with your own instrumented application or our sample application! 


#### References
- Install docker desktop on windows: https://docs.docker.com/docker-for-windows/install/
- User manual for docker on windows:  https://docs.docker.com/docker-for-windows/
- How to use linux containers, Install docker on windows and step by step detailed guide by Ubuntu: https://ubuntu.com/tutorials/windows-ubuntu-hyperv-containers#1-overview
- Run linux containers on docker for desktop for windows by Microsoft: https://docs.microsoft.com/en-us/virtualization/windowscontainers/quick-start/quick-start-windows-10-linux 



