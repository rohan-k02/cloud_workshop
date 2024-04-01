- [Workshop](#workshop)
- [Introduction](#introduction)
- [Where did I begin?](#where-did-i-begin)
- [What you’ll learn](#what-youll-learn)
- [Actual Steps](#actual-steps)
  - [1. Set up your VM on GCP](#1-set-up-your-vm-on-gcp)
    - [a. Enable the free tier](#a-enable-the-free-tier)
    - [b. Create a free VM instance](#b-create-a-free-vm-instance)
  - [2. Install Docker on the VM](#2-install-docker-on-the-vm)
  - [What is Docker?](#what-is-docker)


# Workshop

- Basic Introduction
- Where did I begin?
- What you’ll learn

- Set up VM on GCP
- Install docker
- Explain docker concepts
- Install authelia
- Install code server
- Install nginx
- Explain what is a reverse proxy
- Set up a custom domain
- Explain what is SSL
- Set up NGINX and HTTPS
- Set up authelia
- Show iPad

# Introduction

Hey everyone, welcome to our Cloud Hosting Workshop! I'm absolutely thrilled to see such a fantastic turnout today. We've got a jam-packed agenda ahead, and I promise  it's going to be super interesting..

Today, we're diving deep into the world of cloud hosting. Over the next couple of hours, you're going to learn about many new things and by the end of this workshop, you’ll have your own VSCode server that you can access from anywhere.

But hey, this workshop isn't just going to be a lecture. Since this is a workshop, we’ll actually be implementing things as we learn and its essential for you to ask questions about anything you’re confused about. Don’t be afraid to ask me if you get stuck at any point. So let's make the most of this awesome opportunity to learn and grow together!

# Where did I begin?

So, a lot of you might be wondering how did I get started with this whole thing? Well, I didn’t begin with GCP, but I started hosting on my own spare laptop at home. Since I had a spare laptop, I thought a good use for it would be to act as a server for my family’s media.  I started by just hosting simple and small apps, but then turned it into a full fledged server as i went deeper into the rabbit hole.

Thus, I ended up hosting tons of apps and services on my own domain and server.

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled.png)

   

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%201.png)

Ofcourse, my cat Minki isnt part of the server installation, she  just likes the warmth from the computer.

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled.jpeg)

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%201.jpeg)

Now, since a lot of you don’t have spare laptops and live in hostels where you don’t have access to your routers, I thought a better option would be to teach you how to host your own apps on the cloud instead.

# What you’ll learn

logos of

- Docker
- Linux
- GCP
- SSL
- DNS
- Authentication
- Nginx

# Actual Steps

## 1. Set up your VM on GCP

### a. Enable the free tier

- Visit [https://cloud.google.com/](https://console.cloud.google.com/)
- Enable the free tier by searching for it or visiting [https://console.cloud.google.com/freetrial/signup](https://console.cloud.google.com/freetrial/signup)

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%202.png)

```
Start your free trial with $300 in credit. Don't worry – you won't be charged if you run out of credit.
```

- Enter your card details.

Now, google cloud requires you to add your card details if you want to use their free tier. Just like any app with a free trial asks you to. Let me make it clear that you will NOT be charged a single rupee if you are only using the free tier. You don’t have to worry about any expenses. This is completely free.

### b. Create a free VM instance

Follow these steps exactly to create a VM that qualifies for the free tier. You can keep using it as long as you want without being charged.

- Search for ‘Add VM Instance’ or visit this link: [https://console.cloud.google.com/compute/instancesAdd](https://console.cloud.google.com/compute/instancesAdd)

```
1. Name your VM
2. Select only these regions: us-west1, us-central1 and us-east1
3. Any zone within these regions is fine
4. Under 'Machine Configuration', select the E2 series.
5. Select the e2-micro Machine Type.
6. Change the boot disk size to 30 GB (only if your account has 1 VM!)
7. Enable HTTP and HTTPS Traffic under 'Firewall'
8. Expand 'Advanced Options' and under 'Networking' expand the default interface.
9. Click 'Reserve Static External IP address' in the 'External IPv4 address' option.
10. Enter a name for the IP address and click 'DONE' to save the IP.
11. Create the VM

```

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%203.png)

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%204.png)

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%205.png)

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%206.png)

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%207.png)

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%208.png)

![Untitled](Workshop%205f6488780f41413c8e8ca534cbd70224/Untitled%209.png)

## 2. Install Docker on the VM

- View all your VMs by visiting [https://console.cloud.google.com/compute/instances](https://console.cloud.google.com/compute/instances) or by searching ‘VM instances’ in the search bar
- Click SSH under the Connect column.
- Refer [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/) to install docker engine or just copy-paste this block in the terminal. This will install the docker repository to allow you to get the latest version of docker.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

- To install the latest version, run:

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

- Verify that the Docker Engine installation is successful by running the `hello-world` image.

```bash
sudo docker run hello-world
```

You have now successfully installed and started Docker Engine.

## What is Docker?