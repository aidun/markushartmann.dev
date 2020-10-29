---
title: "Elastic Cloud on RaspberryPi 4"
date: 2020-10-27T15:14:41+01:00
description: "How to setup Elastic-Stack on RaspberryPi 4"
featured: true 
draft: true
toc: true
codeMaxLines: 10
codeLineNumbers: false
categories:
  - cloud
tags:
  - k3s
  - k3sup
  - elastic
  - elastic cloud
  - elk
  - eck
  - raspi
  - raspberry pi
---


# Introduction

# Requirements

You need a **Raspberry Pi 4** and a proper SD-Card. As OS I recommend Ubuntu Server 20.10 with ARM64 support. You can download it on the [Offical Download Page](https://ubuntu.com/download/raspberry-pi/thank-you?version=20.10&architecture=server-arm64+raspi) and install it by following the steps 1-4 of the [tutorial from Ubuntu](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi).

We will install k3s with *k3sup*. You can download k3sup from the [Github-Page of Alex Ellis](https://github.com/alexellis/k3sup).

To configure and install the Elastic-Stack you need [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) and [helm](https://helm.sh/docs/intro/install/).

# Installation of k3s with k3sup

1. Check if we can connect to the maschine with the username and ip from the ubuntu tutorial.

```
# IP from the tutorial
export IPOFTHEPI=192.168.178.50

# Connect with user and password from the tutorial
ssh ubuntu@$IPOFTHEPI
```

2. Setup key based authentication
```
# generate a new ssh-key if needed
ssh-keygen

# Connect with user and password from the tutorial
ssh-copy-id ubuntu@$IPOFTHEPI

# Check if the login without password works
ssh ubuntu@$IPOFTHEPI
```

3. Install k3s

```
# Install k3s master without
k3sup install --ip $IPOFTHEPI --user ubuntu

# Wait for the installation to be finished

# Point KUBECONFIG to the new config, so kubectl and helm can use it
export KUBECONFIG=`pwd`/kubeconfig

# Check if k3s is running
kubectl get nodes
```

# Installation of the Elastic-Stack on k3s
