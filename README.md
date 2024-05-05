# Using Longhorn with EKS

### Deploy Longhorn via Helm

```sh

### Requirement...Install CSI 
helm repo add aws-ebs-csi-driver https://kubernetes-sigs.github.io/aws-ebs-csi-driver/
helm repo update

### 1. First, add the Longhorn Helm repository:
helm repo add longhorn https://charts.longhorn.io
helm repo update

### 2. Install 
### Install the OS package on the node, this DaemonSet will have privileged access rights.
kubectl apply -f iscsi-dependency.yaml

### 3. Next, install Longhorn with Helm:
helm install longhorn longhorn/longhorn --namespace longhorn-system --create-namespace

### 4. Verify the Installation
### Check the deployment status. All Longhorn components should be running:
kubectl -n longhorn-system get pod

### 5. Access the Longhorn UI
kubectl -n longhorn-system port-forward service/longhorn-frontend 8080:80

### Create a Persistent Volume Claim
kubectl apply -f Test/1_pvc.yaml

### Create a Deployment with Volume
kubectl apply -f Test/2_deployment.yaml