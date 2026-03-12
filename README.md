# Minikube-website-deployment

This repository describes how I deployed a website using minikube

## Install software

### Install a VM manager
I used Virtual Machine Manager which can be installed by doing the following:
- Update system packages
  - `sudo apt update`
- install the required packages
  - `sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients virt-manager -y`
- Add your user or whichever user will be using the software to the groups libvirt and kvm
  - `sudo adduser $USER libvirt`
  - `sudo adduser $USER kvm`
- Log out and log back in if you were added to either of the groups above
- Search Virtual Machine Manager or run virt-manager in the terminal to start managing your VMs

### Install the latest kubectl release
- `curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"`
- `sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl`

### Install the latest minikube release
- `curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64`
- `sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64`

---

### Deploy and expose the service
- Using the files in this repository, run:
  - `kubectl apply -f deployment.yaml`
  - `kubectl apply -f service.yaml`

### Create configmap
- The service will use the configmap to retrieve the index.html file and serve it:
  - `kubectl create configmap nginx-html --from-file=index.html`
  
### Access the service
- `minikube service nginx-service`
