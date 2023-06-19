# INSTALL KUBERNETES USING KUBEADM

* [Pre-Requisites](#pre-requisites-official-documentation)
* [Install Container Runtime](#install-container-runtime-containerd--centos--rhel-)
* [Install kubeadm kubectl kubelet](#install-kubeadm-kubectl-kubelet)
* [Initialize cluster using `kubeadm`](#initialize-cluster-using-kubeadm)
* [Install CNI](#install-cni-container-network-interface-for-the-cluser)
* [Verify Installation](#verify-the-kubernetes-cluster-installation)



## Pre-Requisites [(Official Documentation)](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)
1. Compatible Linux host(s).
2. First identify how many Leader nodes and How many Follower nodes are to be deployed.
3. Ensure you are having `root` user access for these nodes.
4. Ensure you are having internet access from these nodes.
5. 2 GB or more of RAM per machine and 2 CPUs or more. (any less will leave little room for your apps).
7. Unique hostname, MAC address, and product_uuid for every node.
8. Certain [ports](#ports-need-to-be-available-by-default) are open on your machines.
9. Swap disabled. You MUST disable swap in order for the kubelet to work properly.

## Ports Need to be available by default across cluster nodes.
Leader Nodes:
| Protocol    | Direction | Port Range  | Purpose                 | Used By             |
| --------    | --------  | --------    | ---------------------   | ---------------     |
| TCP         | Inbound   | 6443        | Kubernetes API server   | All                 |
| TCP         | Inbound   | 2379-2380   | etcd server client API  | kube-apiserver, etcd|
| TCP         | Inbound   | 10250       | Kubelet API             | Self, Control plane |
| TCP         | Inbound   | 10259       | kube-scheduler          | Self                |
| TCP         | Inbound   | 10257       | kube-controller-manager | Self                |

Follower Nodes:
| Protocol    | Direction | Port Range  | Purpose                 | Used By             |
| --------    | --------  | --------    | ---------------------   | ---------------     |
| TCP         | Inbound   | 10250       | Kubelet API             | Self, Leader        |
| TCP         | Inbound   | 30000-32767 | NodePort Services       | All                 |



## Install Container Runtime (containerd) [ CentOS / RHEL ]
**This step needs to be followed on all nodes [Leader and Follower]**
* Steps to install containerd in [CentOS/RHEL]

```
dnf install -y  yum-utils device-mapper-persistent-data lvm2

dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

dnf update -y && dnf install -y containerd.io

mkdir -p /etc/containerd

containerd config default > /etc/containerd/config.toml# Restart containerd 

systemctl restart containerd

systemctl enable containerd

systemctl status containerd
```

* Download `crictl` executable for checking the successfull status of containerd | [Official Documentation](https://github.com/kubernetes-sigs/cri-tools/blob/master/docs/crictl.md)
```
VERSION="v1.26.0" 
wget https://github.com/kubernetes-sigs/cri-tools/releases/download/$VERSION/crictl-$VERSION-linux-amd64.tar.gz
sudo tar zxvf crictl-$VERSION-linux-amd64.tar.gz -C /usr/local/bin
rm -f crictl-$VERSION-linux-amd64.tar.gz
```

* Add the below lines in the file: `/etc/crictl.yaml`
```
runtime-endpoint: unix:///var/run/containerd/containerd.sock
image-endpoint: unix:///var/run/containerd/containerd.sock
timeout: 2
```
* Run `crictl images` and  `crictl ps -a` to ensure containerd is successfully runing.

## Install Kubeadm ,Kubectl ,Kubelet

```
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
EOF
```

## Set SELinux in permissive mode (effectively disabling it)
```
sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
```
* **Run the Below Command in Leader Node**
```
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
sudo systemctl enable --now kubelet
```
* **Run the Below Command in Follower Node**
```
sudo yum install -y kubelet kubeadm --disableexcludes=kubernetes
sudo systemctl enable --now kubelet
```

## Initialize cluster using `kubeadm`
* **Get The Leader Node IP Address** using the command `ifconfig -a` or `hostname -i`
* Use the IP Address in `--apiserver-advertise-address` flag
```
kubeadm init --apiserver-advertise-address=10.184.42.29 --pod-network-cidr=192.168.0.0/16  --service-cidr=192.168.0.0/17
```
* The above command will output a command like `kubeadm join ......` Collect the same command and run it in `Follower` Nodes.

## Install CNI (Container Network Interface) for the cluser 

* We are going to install Calico as a CNI in the cluster
**Run the Below Command in Leader Node**
```
kubectl apply -f https://docs.projectcalico.org/v3.8/manifests/calico.yaml
```

## Verify the Kubernetes Cluster Installation

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
* Verify the cluster is working fine by using the below command.
`kubectl get nodes` `kubectl get pods --all-namespaces`