# Setting Up GKE Cluster and Deploying Next.js App

## Prerequisites

### 1. Install Google Cloud SDK (gcloud CLI)
Download and install the Google Cloud SDK from the [official website](https://cloud.google.com/sdk/docs/install).

### 2. Install kubectl(Optional)
Install `kubectl`, the Kubernetes command-line tool:
```bash
gcloud components install kubectl
```

### 3. Authenticate gcloud
Log in to your Google Cloud account:
```bash
gcloud auth login
```

### 4. Set Your Project
Specify the GCP project you want to use: Assuming you have already created a Cluster in GCP you can paste the command present in the dashboard under the connect option.

In our WBL  case we have created the cluster so we can directly paste the link given below in the gcloud cli.

```bash
gcloud container clusters get-credentials wbl-cluster --region us-central1 --project wbl-new
```

---

## Preparing Your App

### 1. Create a Dockerfile and push it to Docker hub
Create a `Dockerfile` in your project root:
```dockerfile
# Use the Node.js image as the base
FROM node:18-alpine
.......
```
---

## Deploying Your App to GKE

### 1. Create a Kubernetes Deployment
Create a `deployment.yaml` file:
```yaml
apiVersion: apps/v1
kind: Deployment
......
```

### 2. Create a Kubernetes Service
Add a `service.yaml` file:
```yaml
apiVersion: v1
kind: Service
.....
```

### 3. Apply the Deployment and Service
Apply the YAML files to your cluster:
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

## Managing Multiple Accounts in gcloud CLI

### 1. Login to Multiple Accounts
#### Login to an Account:
```bash
gcloud auth login
```
#### Add Another Account:
```bash
gcloud auth login --activate
```

### 2. List All Accounts
View all accounts authenticated with `gcloud`:
```bash
gcloud auth list
```
Example output:
```
Credentialed Accounts
ACTIVE  ACCOUNT
        hemantkd2402@gmail.com
*       sampath.velupula@gmail.com
```

### 3. Switch Between Accounts
Set a specific account as active:
```bash
gcloud config set account [ACCOUNT_EMAIL]
```
Example:
```bash
gcloud config set account hemantkd2402@gmail.com
```

### 4. Verify the Active Account
Confirm the currently active account:
```bash
gcloud auth list
```

### 5. Remove an Account (Optional)
If you no longer need an account:
```bash
gcloud auth revoke [ACCOUNT_EMAIL]
```

---

## Resolving GKE Auth Plugin Issues

If you encounter errors related to `gke-gcloud-auth-plugin` while using `kubectl`, follow these steps:

### 1. Install the GKE Auth Plugin
Run the following command to install the `gke-gcloud-auth-plugin` using the Google Cloud SDK:
```bash
gcloud components install gke-gcloud-auth-plugin
```

### 2. Update Your kubeconfig to Use the Plugin
Update the `kubeconfig` to ensure it uses the plugin for authentication:
```bash
gcloud container clusters get-credentials [CLUSTER_NAME] --zone [ZONE]
```

### 3. Verify the Installation
Confirm that the plugin is working by running a simple `kubectl` command:
```bash
kubectl get pods
```

### Monitor Cluster Status
```bash
kubectl get pods
kubectl get services
kubectl get nodes
```
