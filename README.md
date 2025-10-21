# Homelab-Guide
A project based guide to building out your very own homelab! 

Building a Homelab to suite your needs.
* **Introduction: What is a Homelab and Why Build One?**
    * [Benefits of a Homelab](#benefits-of-a-homelab) (Learning, Privacy, Control, Experimentation)
    * [Understanding the Core Components](#understanding-the-core-components) (The "Why" behind the technologies)

* **Planning Your Homelab: Essential Recommendations**
    * [Resource Assessment](#resource-assessment)
    * [The Folly of Estimating Your Current and Future Needs](#the-folly-of-estimating-your-current-and-future-needs)
    * [Power](#power)
    * [Routers, Switches, and Network Addressing](#routers-switches-and-network-addressing)

* **Core Technologies for Your Homelab**
    * [Virtualization (Hypervisor)](#virtualization-hypervisor)
    * [Operating System (Server OS)](#operating-system-server-os)
    * [Containerization (Docker Compose)](#containerization-docker-compose)
    * [Network Attached Storage (NAS)](#network-attached-storage-nas)
    * [Remote Access Tools](#remote-access-tools)


* **Accessing Your Homelab Remotely and Securely**
    * **[Remote Access Solutions](#remote-access-solutions):**
    * **[Mobile Access (Termux)](#mobile-access-optional):**

* **Homelab Projects: Practical Applications**
    * **[Home Automation](#home-automation):**
    * **[Media Streaming](#media-streaming):**
    * **[Photo Management](#photo-management):**

* **Maintaining Your Homelab**
    * **[Monitoring](#monitoring):**
    * **[Backups](#backups):**
    * **[Security](#security):**
    * **[Automation and Orchestration](#automation-and-orchestration):**
* **[Homelab: A Never-Ending Journey](#homelab-a-never-ending-journey)**

## Introduction: What is a Homelab and Why Build One?

In its simplest form, a homelab is a practice environment built using servers, networking equipment, and software, usually set up at home. Unlike relying on cloud services or large corporations, a homelab gives you complete control over your data and applications.
But it's more than just a collection of hardware; it's a space for learning, experimentation, and self-sufficiency. You can use a homelab to:

*   **Learn Real-World Skills:** Gain practical experience with technologies used in professional IT environments, making you more employable.
*   **Self-Host Services:** Host your own website, email server, media server (like Plex or Jellyfin), file storage (NAS), or home automation system.
*   **Take Control of Your Data:** Host your own files, photos, and videos, keeping them private and secure.
*   **Protect Your Privacy:** Control your data and avoid relying on cloud services that may track your activity.
*   **Experiment Safely:** Test new software, configurations, or network setups without risking your production environment (if you have one).
*   **Become More Self-Reliant:** Learn how to troubleshoot issues, configure servers, and manage your own digital infrastructure.

Whether you're a software developer, sysadmin, cybersecurity enthusiast, or simply someone who wants to learn more about technology, a homelab is an invaluable tool. It's a place to break things, fix them, and grow your skills in a low-stakes, highly rewarding environment.

### Understanding the Core Components

Let's explore the fundamental building blocks of a typical homelab. While the specific technologies you choose will depend on your goals, most homelabs rely on these core components:

*   **Hardware:** The physical foundation of your homelab, including servers, networking equipment, and storage devices.  We will discuss hardware considerations in general terms, but this guide focuses on *what* software you'll need rather than *what* to purchase.
*   **Hypervisor (Virtualization):** Software that allows you to run multiple virtual machines (VMs) on a single physical server. This is a crucial component for maximizing resource utilization and isolating different applications.
*   **Operating System (Server OS):** The foundation upon which your applications and services run. You'll need a server OS for both your physical server (if you're using a bare-metal hypervisor) and your VMs.
*   **Containerization (Docker):** A technology that allows you to package applications and their dependencies into isolated containers, making them easy to deploy and manage. Docker is a popular choice for self-hosting applications.
*   **Networking:** The infrastructure that connects your servers, VMs, and containers, allowing them to communicate with each other and the outside world. This includes routers, switches, and firewalls.
*   **Remote Access Tools:** Allowing you to connect to your homelab remotely, even when you aren't on the same local network.

Don't worry if you're not familiar with all of these components yet. We'll dive into each of them in more detail in the following sections. The important thing to understand is that these components work together to create a powerful and flexible environment for learning, experimentation, and self-hosting.  Knowing the purpose of each component will help you better understand its function within your homelab.

## Planning Your Homelab: Essential Recommendations

### Resource Assessment
What do you really need? - I would suggest starting with what you already have. Do you have an old PC that is not being used? IS your current gaming PC starting to show its age? Use that as an excuse to buy yourself a new one and give your old machine new life as your new server!

### The Folly of Estimating Your Current and Future Requirements
Before you can really know what you need now and what you might need in the future, my suggestion would be to start small and build out only when your projects or goals require you to. Trying to "future proof" your homelab will only lead to buyer's remorse as your understanding of what you really need become apparent through actual use.

### Power
If you ware serious about your data and want to keep everything safe from hardware failures due to power outages. I would highly recommend getting a UPS. Having an uninterruptible power supply will help ensure that your hardware has time to gracefully shout down in the event of a power outage and will help prevent your data from becoming corrupted. 

### Routers, Switches, and Network Addressing
There is nothing wrong with using the default router that you rent from your ISP, but if you want better control over your network and functionality, then I would highly recommend buying your own router and modem. This will allow you to create VLANs, maintain your own DNS records, as well as get the most out of your internet speeds.

## Core Technology for Your Homelab

### Virtualization (Hypervisor)
The hypervisor will be the baremetal operation system that you will want to install on most all of your heardware. This will allow you to get more out of the hardware that you already have and will give you the flexability to test, deploy, backup and destroy your software across all of oyu machines. 
### Operating System (Server OS)
The operating system is the software that bridges the hardware and the software together. For your homelab, you will install your chosen hypervisor onto your servers and then create virtual machines (VMs) to install your software onto. 
### Containerization (Docker Compose)
  *  What are Containers and Why Use Them?
Think of them as lightweight, isolated environments for running applications. Unlike virtual machines (VMs), which virtualize the entire hardware, containers virtualize the operating system.
They package up an application along with all its dependencies: code, runtime, system tools, system libraries, and settings. This ensures that the application runs reliably across different computing environments.
They are based on OS-level virtualization. The container engine (like Docker) leverages features in the kernel of the operating system to isolate processes.
The same container image runs the same way regardless of where it's deployed: developer's laptop, test environment, or production server. Eliminates the "works on my machine" problem.They easily scale applications by creating multiple instances of the same container. Container orchestration tools (like Kubernetes) make this even easier.
  * Docker Fundamentals: Images, Containers, Networks, Volumes
     * Images: Read-only templates used to create containers. Think of them like a blueprint for your application's environment. Images are built from a Dockerfile: A text file containing instructions for building the image. These instructions typically include base image, copying files, installing dependencies, and setting environment variables. Images are layered: Each instruction in the Dockerfile creates a new layer. This layering helps optimize image size and sharing. Images are stored in registries: Docker Hub is the most common public registry, but you can also use private registries. Example: An image might contain a specific version of Python, your application code, and any libraries it needs.
  * Containers: Running instances of Docker images. They are the actual, executable environments for your application. Each container is isolated from other containers and the host operating system. Containers have their own file system, networking, and process space. You can start, stop, restart, and remove containers. Containers are ephemeral (by default): Changes made inside a container are lost when the container is stopped or removed, unless you use volumes (see below).
  * Networks: Containers need to communicate with each other and the outside world. Docker networks provide a way to connect containers. 
  * Volumes:
     * Mechanism for persisting data generated or used by containers.
     * Provide a way to share data between containers and the host operating system.
     * Data in volumes persists even after the container is stopped or removed.
  * Types of Volumes:
     * Named Volumes: Managed by Docker. Stored in a specific location on the host. Preferred way to persist data.
     * Bind Mounts: Mount a directory from the host's file system into the container. More flexible, but less portable.
     * tmpfs Mounts: Stored in the host's memory. Data is lost when the container is stopped. Useful for temporary data that doesn't need to be persisted. Use cases: Persisting database data, sharing code between the host and the container, storing logs.
  *  Docker Compose: Defining and Managing Multi-Container Applications
     *  Installing Docker and Docker Compose [Guide](https://github.com/gorect/Docker)
### Network Attached Storage (NAS)
  *  NAS Concepts: File Sharing, RAID, Data Redundancy
  *  To access your files, you will need to set up a basic NAS Share
### Remote Access Tools:
* Allowing you to connect to your homelab remotely, even when you aren't on the same local network.

Don't worry if you're not familiar with all of these components yet. We'll dive into each of them in more detail in the following sections. The important thing to understand is that these components work together to create a powerful and flexible environment for learning, experimentation, and self-hosting.  Knowing the purpose of each component will help you better understand its function within your homelab.

## Accessing Your Homelab Remotely and Securely
### Remote Access Solutions
  *  [Tailscale](https://tailscale.com): A simple zero-config solution.
The first thing you should do is create a tailscale account. Tailscale is a free VPN service that is based on Wireguard and allows you to create a flat, mesh network where all of your tailscale devices and connect and communicate to each other securely. 
  *  SSH (Secure Shell): Securely accessing the command line.
For servers and services that you wish to remotely access, SSH is an excellent choice for accessing and troubleshooting you Linux servers and containers.
### Mobile Access (Optional)
  * Termux on Android
In combinate with Tailscale, you can use you phone to access and administer your homelab from your phone, anywhere in the world!

### Homelab Projects: Practical Applications
Now that we have the basics, your homelab journey is ready to begin. With unlimited possibilities, it can be very overwhelming and difficult to know where to start. My suggestion for you is to take small steps and think of one or two projects or technologies that you would like to implement. Do you want to control your lights or check on automations while you are away from home? Be able to watch your DVDs or listen to your CDs from anywhere in the world? Make sure that you have complete data sovereignty over your pictures?
### Home Automation
  *  Home Assistant: The free and opensource home automation platform.
### Media Streaming
  *  **Video Streaming
     *  Jellyfin: A free and opensource option for presenting your personal movie and tv show collection.
  *  **Music Streaming
     *  Navidrome:  Lightweight and focused on music. Pairs well with the Symfonium app.
     *  Azuracast:  For setting up your own internet radio station.
### Photo Management
  *  Immich:  Self-hosted photo and video backup solution (Google Photos replacement). 
Know that these are just a few of the many options that you can choose to selfhost!

### Maintaining Your Homelab**
Now that you have a few projects under your belt, you might now want to start fleshing out your homelab infrastructure with monitoring, backups and automation!
### Monitoring
  *  System Monitoring Tools
You can use services like Grafana and Prometheus to track your VMs, docker containers and services.
### Backups
  *  Backup Strategies (Full, Incremental, Differential)
Since we went with Proxmox for our hypervisor, a good first option would be to create an instance of Proxmox Backup Server (PBS). This can either be implemented as a VM on one of your existing Proxmox servers or you can get a separate bare metal host (or CSP) host to install PBS on to. This works well with Proxmox as it is easily integrated into your cluster.
  *  Backup Solutions
Besides backing up full VMs, you can also use technology like rsync or BorgBackup to sync files from across your homelab to a cerntalized location (your previously setup NAS solution).
### Security

Security can be something easily overlooked, the best first defense is to ensure that your operating systems are kept up to date. This can be maintained through the unattended updates tool available in most Linux operating systems or by using services like Ansible (see the next section for more). Next making sure that you are not opening up services or hosts to the open internet. Tailscale will mostly prevent this from being needed, however, know that sometimes services like docker containers can open ports if you are not careful. Additionally there are other services like fail2ban can be implemented to catch intrusion attempts and automatically ban them based on your ruleset. 
### Automation and Orchestration
  *  Ansible:  Automating server configuration and application deployment
Ansible can be used to provision servers based on roles that you create and can be used to automatically update servers to keep them secure.
  *  Watchtower:  
Assuming that youre containers are set to `latest` or `stable`, watchtower can automatically update predefined Docker containers on your docker server(s).

## Homelab: A Never-Ending Journey

Congratulations on taking the first steps on your homelab journey! As you build and maintain your homelab, you'll quickly realize that it's a never-ending process of learning and adaptation. New technologies emerge, your needs change, and there's always something new to explore. Embrace this constant evolution. Don't be afraid to try new things, experiment with different configurations, and challenge yourself to learn new skills. Your homelab is a reflection of your curiosity and your commitment to continuous growth.
