Learning Kubernetes through taking the CKA.  This will give me guidance on how to proficiently navigate and troubleshoot Kubernetes 















Realized making all these folders is causing unnecessary bloat and too many README files so i'll put them all under the main README

# Day 6 notes
## Kubernetes scaling
so far we only learned how to setup a single container using Docker.  this is great for local development but what if I python application gets popular.  what if 100 users want to access your application?  we need to utilize auto-scaling.

### Here is where Kubernetes (k8s) comes to play



#Day 7 notes
## What is Kubernetes

### Kubernetes pod
A Pod is the smallest and most basic deployable unit in Kubernetes.  
Pod can have multiple containers which mainly share:
- Networking (Network Namespaces)
- Storage

Why multiple container?
Sidecar pattern (Logging, monitoring, proxy, reverse proxy)


### Deployment
It ensures that the desired nuber of Pods are running.
Key features:
- Replica Management
- Rolling Updates and Rollbacks
- Declarative Configuration

Even if you have a single Pod in the Deployment.  The Deployment will try to restart the Pod incase it fails

If I want to update my application, Deployment can update the Pods section by section (rolling update) ensuring no downtime

Declarative Configuration
when I tell the deployment to run 10 Pods.  I dont have to manage that 10 Pods will run

![Kubernetes Cluster diagram](stored-images/image.png)

### How is the control plane setup?
kubelet




