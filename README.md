# Kubsernetes-with-minikube

Minikube System Requirements:
2 GB RAM or more
2 CPU / vCPU or more
20 GB free hard disk space or more
Docker / Virtual Machine Manager – KVM & VirtualBox


Prerequisites for minikube:
Minimal Ubuntu 
Sudo User with root privilegesStable Internet Connection


Step 1) Apply updates:

Command:
sudo apt update -y
sudo apt upgrade -y

Step 2) Install Minikube dependencies:
Command:
 sudo apt install -y curl wget apt-transport-https
 
 Step 3) Download Minikube Binary:
Command:
 wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
 
 Once the binary is downloaded, copy it to the path /usr/local/bin and set the executable permissions on it
Command:
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
sudo chmod +x /usr/local/bin/minikube

Verify the minikube version
Command:
minikube version
Output:
minikube version: v1.28.0
commit: 986b1ebd987211ed16f8cc10aed7d2c42fc8392f


Step 4) Install Kubectl utility
Kubectl is a command line utility which is used to interact with Kubernetes cluster. It is used for managing deployments, service and pods etc. Use below curl command to download latest version of kubectl.
Command:
 curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl


Once kubectl is downloaded then set the executable permissions on kubectl binary and move it to the path /usr/local/bin.
Command:
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

Now verify the kubectl version:
Command:
kubectl version -o yaml

Output:
clientVersion:
  buildDate: "2023-01-18T15:58:16Z"
  compiler: gc
  gitCommit: 8f94681cd294aa8cfd3407b8191f6c70214973a4
  gitTreeState: clean
  gitVersion: v1.26.1
  goVersion: go1.19.5
  major: "1"
  minor: "26"
  platform: linux/amd64
kustomizeVersion: v4.5.7


Step 5) Start minikube:
Command:
minikube start

In case you want to start minikube with customize resources and want installer to automatically select the driver then you can run following command,
Command:
 minikube start --addons=ingress --cpus=2 --cni=flannel --install-addons=true --kubernetes-version=stable --memory=6g
Output:
minikube v1.28.0 on Ubuntu 22.04
✨  Automatically selected the kvm2 driver. Other choices: virtualbox, ssh, qemu2 (experimental)
👍  Starting control plane node minikube in cluster minikube
💾  Downloading Kubernetes v1.25.3 preload ...
    > preloaded-images-k8s-v18-v1...:  385.44 MiB / 385.44 MiB  100.00% 4.24 Mi
🔥  Creating kvm2 VM (CPUs=2, Memory=2200MB, Disk=20000MB) ...
🐳  Preparing Kubernetes v1.25.3 on Docker 20.10.20 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default


Run below minikube command to check status,
Command:
minikube status
Output:

minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

Run following kubectl command to verify the Kubernetes version, node status and cluster info.
Command:
kubectl cluster-info
Output:
Kubernetes control plane is running at https://192.168.39.243:8443
CoreDNS is running at https://192.168.39.243:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

Command:
kubectl get nodes

Output:
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   14m   v1.25.3




Step 6) Managing Addons on minikube
Command:
minikube addons list
Output:
|-----------------------------|----------|--------------|--------------------------------|
|         ADDON NAME          | PROFILE  |    STATUS    |           MAINTAINER           |
|-----------------------------|----------|--------------|--------------------------------|
| ambassador                  | minikube | disabled     | 3rd party (Ambassador)         |
| auto-pause                  | minikube | disabled     | Google                         |
| cloud-spanner               | minikube | disabled     | Google                         |
| csi-hostpath-driver         | minikube | disabled     | Kubernetes                     |
| dashboard                   | minikube | disabled     | Kubernetes                     |
| default-storageclass        | minikube | enabled ✅   | Kubernetes                     |
| efk                         | minikube | disabled     | 3rd party (Elastic)            |
| freshpod                    | minikube | disabled     | Google                         |
| gcp-auth                    | minikube | disabled     | Google                         |
| gvisor                      | minikube | disabled     | Google                         |
| headlamp                    | minikube | disabled     | 3rd party (kinvolk.io)         |
| helm-tiller                 | minikube | disabled     | 3rd party (Helm)               |
| inaccel                     | minikube | disabled     | 3rd party (InAccel             |
|                             |          |              | [info@inaccel.com])            |
| ingress                     | minikube | enabled ✅   | Kubernetes                     |
| ingress-dns                 | minikube | disabled     | Google                         |
| istio                       | minikube | disabled     | 3rd party (Istio)              |
| istio-provisioner           | minikube | disabled     | 3rd party (Istio)              |
| kong                        | minikube | disabled     | 3rd party (Kong HQ)            |
| kubevirt                    | minikube | disabled     | 3rd party (KubeVirt)           |
| logviewer                   | minikube | disabled     | 3rd party (unknown)            |
| metallb                     | minikube | disabled     | 3rd party (MetalLB)            |
| metrics-server              | minikube | disabled     | Kubernetes                     |
| nvidia-driver-installer     | minikube | disabled     | Google                         |
| nvidia-gpu-device-plugin    | minikube | disabled     | 3rd party (Nvidia)             |
| olm                         | minikube | disabled     | 3rd party (Operator Framework) |
| pod-security-policy         | minikube | disabled     | 3rd party (unknown)            |
| portainer                   | minikube | disabled     | 3rd party (Portainer.io)       |
| registry                    | minikube | disabled     | Google                         |
| registry-aliases            | minikube | disabled     | 3rd party (unknown)            |
| registry-creds              | minikube | disabled     | 3rd party (UPMC Enterprises)   |
| storage-provisioner         | minikube | enabled ✅   | Google                         |
| storage-provisioner-gluster | minikube | disabled     | 3rd party (Gluster)            |
| volumesnapshots             | minikube | disabled     | Kubernetes                     |
|-----------------------------|----------|--------------|--------------------------------|













Let’s assume we want to enable and access kubernetes dashboard , run
Command:
 minikube dashboard

Output:

 


 



















































