These are my extra side notes of curiosity while learning Kubernetes


# Q. How is kubernetes setup?

## kubectl - the client/remote control
kubectl is a **CLI tool that talks to any Kubernetes cluster's API server**.  It doesn't create clusters,
it just sends commands and reads state

you point at:
- A **kind** cluster on your laptop
- A **kubeadm** cluster you built by hand
- An **EKS** cluster in **AWS**
- A **GKE** or **AKS** cluster

## kind - the cluster builder (for local/dev use)

I'll be setting up **kind** (Kubernetes **IN Docker**)  for my CKA study..  This creates a **real, functioning Kubernetes cluster**, using Docker containers to simulate nodes

**Setups steps in WSL2**
```
# 1. Install kubectl (the CLI to talk to any cluster)
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl && sudo mv kubectl /usr/local/bin/

# 2. Install kind
curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64
chmod +x ./kind && sudo mv ./kind /usr/local/bin/

# 3. Write a kind-config.yaml defining 1 control-plane + 2 workers (matches your diagram)
# 4. Run:
kind create cluster --config kind-config.yaml --name cka-lab
```

### Kubernetes manifests 
(YAML files) go to the cluster via kubectl. A manifest doesn't contain your app — it's a reference to an image sitting in a registry, plus instructions for how to run it:

### The full flow, end to end

1. docker build → build your image locally
2. docker push architectn/my-flask-app → image lands in Docker Hub (or ECR)
3. Write a Deployment YAML referencing that image
4. ```kubectl apply -f deployment.yaml``` → sent to AWS's managed API server
5. AWS's scheduler decides which of your worker nodes should run it
6. That worker node's kubelet pulls the image and starts the container




### Made an EKS to test
EKS cost 10 cents/Hr 
- even if the cluster is empty

EKS will handle the control plane and scale it automatically

You can also change the configuration to have it reserve extra headroom to spin up the control plane faster (cost $$$)


#### Pullling from Private Docker Hub 
to point to it will need the Docker Hub token stored
I realized I can use Parameter Store to store the username and password 
```
DOCKER_TOKEN=$(aws ssm get-parameter --name /dockerhub/token --with-decryption --query 'Parameter.Value' --output text)

kubectl create secret docker-registry dockerhub-creds \
  --docker-username=architectn \
  --docker-password=$DOCKER_TOKEN \
  --docker-server=https://index.docker.io/v1/
```