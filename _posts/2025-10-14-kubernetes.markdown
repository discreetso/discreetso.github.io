---
layout: post
title:  "Kubernetes"
author: "discreetso (M.Huzaifa)"
date:   2025-10-14 16:00:04 +0500
categories: kubernetes tutorial
---
# Kubernetes: The Container Orchestrator

## What is Kubernetes?

Kubernetes (often abbreviated as K8s) is an open-source platform designed to automate deploying, scaling, and operating application containers. It groups containers that make up an application into logical units for easy management and discovery.

In simple terms, it's a system for running and coordinating applications across a cluster of machines. It's the brain that manages your containerized applications.

> **Fun Fact:** "Kubernetes" is Greek for helmsman or pilot, hence the helm in the community logo. K8s is a numeronym, where the "8" stands for the eight letters between the "K" and the "s".

---

## Core Concepts

To understand Kubernetes, you need to grasp its fundamental building blocks.

### 1. Pod
The smallest and simplest Kubernetes object. A Pod represents a single instance of a running process in your cluster and can contain one or more containers (like Docker containers). Containers within a Pod share storage and network resources.

### 2. Node
A worker machine in Kubernetes, which can be a virtual or physical machine. Each Node is managed by the Control Plane. Pods run on Nodes.

### 3. Cluster
A set of Nodes grouped together. This is the foundation of Kubernetes. If one Node fails, the workload is automatically moved to another Node in the cluster.

### 4. Deployment
A Deployment provides declarative updates for Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. It's the most common way to manage stateless applications.

### 5. Service
An abstract way to expose an application running on a set of Pods as a network service. Pods are ephemeral (they can come and go), so a Service provides a stable IP address and DNS name to access them, acting as a built-in load balancer.

### 6. ConfigMap & Secret
*   **ConfigMap:** Allows you to decouple configuration artifacts from container images, keeping your applications portable.
*   **Secret:** Similar to a ConfigMap but intended for storing sensitive information, like passwords or API keys, in an encoded format.

---

## Key Features & Benefits

*   **Service Discovery and Load Balancing:** Kubernetes can expose a container using a DNS name or its own IP address. If traffic to a container is high, Kubernetes can load balance and distribute the network traffic.
*   **Storage Orchestration:** Automatically mount storage systems of your choice, such as local storage, public cloud providers, or network storage systems.
*   **Automated Rollouts and Rollbacks:** You can describe the desired state for your deployed containers, and Kubernetes can change the actual state to the desired state at a controlled rate (e.g., performing a rolling update).
*   **Automatic Bin Packing:** You provide Kubernetes with a cluster of nodes, and it automatically fits containers onto your nodes to make the best use of resources.
*   **Self-Healing:** Kubernetes restarts containers that fail, replaces and reschedules containers when nodes die, and kills containers that don't respond to your user-defined health check.
*   **Secret and Configuration Management:** Lets you store and manage sensitive information without rebuilding your container images.

---

## A Simple Example: Deploying a Web App

Let's deploy a simple Nginx web server.

### 1. Create a Deployment
This YAML file defines a Deployment that will create 3 replicas (copies) of an Nginx Pod.

```yaml
# nginx-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80