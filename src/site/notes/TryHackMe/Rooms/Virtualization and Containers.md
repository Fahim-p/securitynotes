---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/virtualization-and-containers/","created":"2025-02-20T16:19:33.425-05:00","updated":"2025-02-20T18:37:22.555-05:00"}
---

# Task 2 - What is Virtualization

- Concept of encapsulating the capabilities and features of a physical machine in a virtual environment, known as a **virtual machine**.
	- **Decrease expenses** 
		- Physical servers can be expensive, and virtualization can decrease the number of servers or other hardware, or even completely remove physical hardware from a company's infrastructure.
	- **Scale** 
		- Hard for a company to scale resources as server usage increases. 
		- Virtualization makes this process easier and can delegate a server's resources to virtual machines as needed based on usage.
	- **Efficiency** 
		- Like scaling, virtualization can also make it easier to decrease the resources allocated to a virtual machine if there is reduced usage.
- **Virtualization Technology**  
	- Virtualization abstracts or creates an **abstraction layer** over computer hardware. 
		- Allows a single device to be divided into multiple virtual computers, 
		- Also known as virtual machines (VMs).  
		- Will have access to _logical resources_ that are abstracted away from the _physical resources_.
- **Virtualization Structure**
	- Implemented using an engine-machine format
		- Software or system creates an abstraction layer and allocates resources 
		- Operating system or application can then be installed on top of this virtualized environment. 
	- The operating system installed in a virtual machine is known as a **guest OS**
		- SAs opposed to the **host OS** on which the virtualization engine is running.  

> [!Question]
>  **Is scalability a primary benefit of virtualization? (Y/N)**

> [!Success] Answer
> Y

> [!Question]
>  **What is the operating system of a virtual machine often referred to as?**

> [!Success] Answer
> guest OS
# Task 3 - Hypervisors

- Provides the ability to create the abstraction layer between hardware and software. 
	- Includes some form of management application to provide an interface between the end user and the abstraction layer to create virtual machines.  
- Separated into two categories that are determined by their position relative to the hardware.
	- Create a lightweight operating system on top of the hardware that is the hypervisor
	- Add a hypervisor as an application on top of a pre-existing operating system.  
- **Type 1 Hypervisors**
	- Also known as **bare metal hypervisors**, create an abstraction layer directly between hardware and virtual machines without a common operating system between them. 
		- Hypervisor is the operating system and is often _headless_
	- Designed for scale and to deploy a large number of virtual machines at once. 
	- Lightweight to dedicate the most resources to virtual machines.
	- Examples include VMware ESXi, Proxmox, VMware vSphere, Xen, and KVM.  
- **Type 2 Hypervisors**
	- Also known as **hosted hypervisors**, create an abstraction layer from a software application built on top of a pre-existing operating system. 
		- Are managed directly from the application through a GUI. 
	- Designed for end-users or individuals such as developers and are not strictly designed to run a large number of virtual machines for scale
	- Examples include VMware Workstation, VMware Fusion, VirtualBox, Parallels, and QEMU.

> [!Question]
>  **What type of hypervisor is VirtualBox considered?**

> [!Success] Answer
> Type 2

> [!Question]
>  **What are type 1 hypervisors also known as?**

> [!Success] Answer
> Bare metal hypervisors

# Task 4 - Containers

- Hypervisors has issues when it comes to scaling lightweight applications. 
- _Microservices_ give us a good example of an application architecture that does not scale well with hypervisor. 
	- A microservice is an application structure that is broken up into smaller services that are scalable and use lightweight protocols and features. 
	- Requires a large number of virtual machines each with high resource usage.
- ****Containers**** are the current solution to the issues encountered with hypervisors at scale.
- **What are Containers**
	- Containers have a lot in common with virtual machines, but is not completely abstracted from the host operating system, shares some properties with them .
		- Containers have their own filesystem, a portion of computing resources (CPU, RAM), a process space, and more.   
		- Also _portable_ and _robust_ because they are not completely abstracted.
	- Container engines are our second type of virtualization. 
		- Containers use a container engine to create an abstraction layer using logical resources

> [!Question]
>  **Are containers completely abstracted from the host operating system? (Y/N)?**

> [!Success] Answer
> N
# Task 5 - Docker

- Docker is a container platform and engine that is used to run Docker "images" as containers.
	- Each Docker image is built of a base image, such Ubuntu, that is specifically built for use in containers and is lightweight. 
	- To build a Docker image, a Dockerfile must be created, which defines the base image for a container and any commands to be run.  
- **Running and Interacting with a Docker Container**
	- Docker Hub is a remote repository for Docker images, 
	- Can pull Docker images created by others or push our own.  

```bash
docker pull <user>/<image>
```

- A container image can be automatically pulled when running the container for the first time.
- Once a container is pulled for the first time, it will be cached locally
	- Docker will look for it locally before attempting to download it.  

```bash
docker run <user>/<image>
```

Once the image is started, we can verify that the Docker engine is running the container by listing the processes running in Docker using the below command.  

```bash
docker ps
```

From the above command, you may notice that the container will be assigned a random identifier, IP address, and network interface.

- **Hands-On Application**
	- Two flags that can be used with the `run` command 
		-  `-d` allows the container to detach from the current terminal 
		-  `-p` exposes ports externally.  
	- Below is the required syntax to start the example Flask app in a Docker container, exposing the webserver to port 5000.  

```bash
docker run -p 5000:5000 -d cryillic/thm_example_app 
```


> [!Question]
>  **What flag is obtained at [10.10.89.179:5000](http://10.10.245.105:5000) after running the container?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250220174735.png)

![](/img/user/TryHackMe/THM_Images/Pasted image 20250220174814.png)
![](/img/user/TryHackMe/THM_Images/1_XfXmmA2k7pLPjxu55HwXhg.webp)

> [!Success] Answer
> THM{this_is_running_in_docker}
# Task 6 - Kubernetes

- **Kubernetes**, also shortened to "**K8s**," is one such solution known as an **orchestration platform**. 
	- Aims to integrate into other products, such as Docker, and extend their capabilities or "synchronize" them with other products or applications.
	- Allows the resources or the number of instances allocated to the application or service to increase or decrease on the fly as needed.
	- Relies on models like hypervisors and containers and extends their uses, features, and capabilities.
		- **Horizontal scaling**
			- Adding devices or machines to handle increased workload, rather than adding logic resources such as CPU or RAM.
		- **Extensibility** 
			- Clusters can be modified dynamically without affecting containers outside of the intended group.
		- **Self-healing**
			- K8s can automatically restart, replace, reschedule, and kill containers that are not properly functioning based on user-defined health checks.
		- **Automated rollouts and rollbacks**
			- K8s can progressively roll out changes to containers. 
				- As changes are made, it will monitor the application's health and decide whether to continue the rollout or rollback. 
				- Ensures the constant uptime of your cluster even if some containers fail.
- **Hands-On** **Application**
	- Given you access to a pre-deployed cluster configured with _kubectl_. 
	- Because Kubernetes provides most of the basic automation by default, we want you to explore the differences between K8s and a traditional virtualization platform on your own.
	- Kubectl, you can use the online reference found [here](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

> [!Task]
>  **Before proceeding, ensure all clusters are started by running minikube start**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250220180019.png)

> [!Question]
>  **How many pods are running on the provided cluster?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250220180151.png)

> [!Success] Answer
> 1

> [!Question]
>  **How many system pods are running on the provided cluster?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250220182808.png)

> [!Success] Answer
> 7

> [!Question]
>  **What is the pod name on the provided cluster?**

Refer to previous screenshots

> [!Success] Answer
> hello-tryhackme-875767b84-sfk2c 

> [!Question]
>  **What is the deployment name on the provided cluster?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250220183019.png)

> [!Success] Answer
> hello-tryhackme

> [!Question]
>  **What port is exposed by the service in question 5?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250220183152.png)

> [!Success] Answer
> 8080

> [!Question]
>  **How many replica sets are deployed on the provided cluster?**

![](/img/user/TryHackMe/THM_Images/Pasted image 20250220183321.png)

> [!Success] Answer
> 1

> [!Question]
>  **What is the replica set name on the provided cluster?**

Refer to previous screenshot

> [!Success] Answer
> hello-tryhackme-875767b84 

> [!Question]
>  **What command would be used to delete the deployment from question 5?**

> [!Success] Answer
> kubectl delete deployment hello-tryhackme


