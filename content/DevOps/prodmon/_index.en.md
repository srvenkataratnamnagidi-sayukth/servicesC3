---
title: ProdMon Installation
tags : ["Composing"]
---

## ProdMon Setup


## OS Details
Oracle linux 8.4 https://linux.oracle.com/switch/centos/

## Application Stack
|Application Name|Reference Links|
|----------------|---------------|
|Kubernaetes| Latest Version |
|MiniO| Latest Version |
|Cortex|Latest Version|
|Percona XtraDB|Latest Version|
|Grafana|Latest Version|

### Prerequisites

#### Disable selinux
Follow the default process

#### First setup the hostnames

```
hostnamectl set-hostname gsts1ship04
hostnamectl set-hostname gsts2ship04
```

Update the Hostnames to IP Address resolutions in the /etc/hosts file
```
172.16.119.24	gsts1ship04
172.17.135.229	gsts2ship04
```

#### Configure the Firewall Ports
Configure the firewall rules on the ports.

```
firewall-cmd --permanent --add-port=6443/tcp
firewall-cmd --permanent --add-port=2379-2380/tcp
firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=10251/tcp
firewall-cmd --permanent --add-port=10252/tcp
firewall-cmd --permanent --add-port=10255/tcp
firewall-cmd --reload
modprobe br_netfilter
echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables
```

### Install Docker-CE on CentOS 8
You will need to add the Docker repository first as it is no longer in the default package list using the following dnf config-manager command

```
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```

Also install containerd.io package which is available as a daemon that manages the complete container lifecycle of its host system, from image transfer and storage to container execution and supervision to low-level storage to network attachments and beyond.

```
dnf install https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm
```
The podman and buildah packages conflict with docker-ce. Remove them first:
```
dnf erase podman buildah
```

Now install the latest version of a docker-ce package.
```
dnf install docker-ce
```

You can now enable and start the docker service.
```
systemctl enable docker
systemctl start docker
```

### Install Kubernetes (Kubeadm) on CentOS 8
Next, you will need to add Kubernetes repositories manually as they do not come installed by default on CentOS 8.
```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

+ Kubeadm helps you bootstrap a minimum viable Kubernetes cluster that conforms to best practices. With kubeadm, your cluster should pass the Kubernetes Conformance tests.

+ Kubeadm also supports other cluster lifecycle functions, such as upgrades, downgrade, and managing bootstrap tokens.

+ With the package repo now ready, you can go ahead and install kubeadm package.
```
dnf install kubeadm -y 
```

When the installation completes successfully, enable and start the service.

```
systemctl enable kubelet
systemctl start kubelet
```

The Kubernetes master which acts as the control plane for the cluster runs a few critical services necessary for the cluster. As such, the initialization process will do a series of prechecks to ensure that the machine is ready to run Kubernetes. These prechecks expose warnings and exit on errors. kubeadm init then downloads and installs the cluster control plane components.

Now it’s time to initialize Kubernetes master, but before that, you must disable swap in order to run “kubeadm init“ command
```
swapoff -a
```
Initializing Kubernetes master is a completely automated process that is controlled by the “kubeadm init“ command as shown.

```
dnf install -y iproute-tc
sudo usermod -aG docker $USER
```

There was a problem with cgroup driver. Kubernetes cgroup driver was set to systems but docker was set to systemd. So we created '/etc/docker/daemon.json' and added below:
```
{
"exec-opts": ["native.cgroupdriver=systemd"],
"default-address-pools": [{"base":"10.11.0.0/16","size":24}]
}
```

Then
```
 systemctl daemon-reload
 systemctl restart docker
 systemctl restart kubelet
```

```
kubeadm config images pull
```

#### Create a control-plane Master with kubeadm (Strictly not for worker-nodes)

```
kubeadm init
```

Incase of issues, run the following command for reset
```
kubeadm reset
```

After successful initialization, you should see the below output
```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 172.16.119.24:6443 --token rtm2my.g9mxp3984kp1cwfl \
	--discovery-token-ca-cert-hash sha256:cfbc2be9e612d01b56b80adfa0766a97f29401285f66372a9446a89c39389c3e
```

To use root, to kubernetes do the following
```
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
```	

Now confirm that the kubectl command is activated.
```
kubectl get nodes
```
Now you should see the following output
```
[root@gsts1ship04 ~]# kubectl get nodes
NAME          STATUS     ROLES                  AGE     VERSION
gsts1ship04   NotReady   control-plane,master   5m31s   v1.22.2
```

At this moment, you will see the status of the master-node is ‘NotReady’. This is because we are yet to deploy the pod network to the cluster.

The pod Network is the overlay network for the cluster, that is deployed on top of the present node network. It is designed to allow connectivity across the pod.

##### Setup Your Pod Network
Deploying the network cluster is a highly flexible process depending on your needs and there are many options available. Since we want to keep our installation as simple as possible, we will use Weavenet plugin which does not require any configuration or extra code and it provides one IP address per pod which is great for us.

These commands will be important to get the pod network setup.
```
export kubever=$(kubectl version | base64 | tr -d '\n')
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$kubever"
```

On successful creation, the output is as follows
```
[root@gsts1ship04 ~]# kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$kubever"
serviceaccount/weave-net created
clusterrole.rbac.authorization.k8s.io/weave-net created
clusterrolebinding.rbac.authorization.k8s.io/weave-net created
role.rbac.authorization.k8s.io/weave-net created
rolebinding.rbac.authorization.k8s.io/weave-net created
daemonset.apps/weave-net created
```
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Now if you check the status of your master-node, it should be ‘Ready’.

```
[root@gsts1ship04 ~]# kubectl get nodes
NAME          STATUS   ROLES                  AGE   VERSION
gsts1ship04   Ready    control-plane,master   27m   v1.22.2
```

Next, we add the worker nodes to the cluster.

### Adding Worker Nodes to Kubernetes Cluster

Install the Kubernetes by following the above steps. Dont install the contol panel

Need different Network for each host docker '/etc/docker/daemon.json' and added below:
```
{
"exec-opts": ["native.cgroupdriver=systemd"],
"default-address-pools": [{"base":"10.10.0.0/16","size":24}]
}
```

We now require the token that kubeadm init generated, to join the cluster. You can copy and paste it to your nodes
```
kubeadm join 172.16.119.24:6443 --token rtm2my.g9mxp3984kp1cwfl \
	--discovery-token-ca-cert-hash sha256:cfbc2be9e612d01b56b80adfa0766a97f29401285f66372a9446a89c39389c3e
```	

On successfull node addition, you should see the following output
```
[root@gsts1ship04 ~]# kubectl get nodes
NAME          STATUS   ROLES                  AGE     VERSION
gsts1ship04   Ready    control-plane,master   4h52m   v1.22.2
gsts2ship04   Ready    <none>                 28s     v1.22.2
[root@gsts1ship04 ~]#
```

## Install Helm

{{% notice info %}}
		Make sure the namespace name
{{% /notice %}}


```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

```
apiVersion: minio.min.io/v2
kind: Tenant
metadata:
  name: storage
  namespace: minio-operator
spec:
  ## Specification for MinIO Pool(s) in this Tenant.
  pools:
    ## Servers specifies the number of MinIO Tenant Pods / Servers in this pool.
    ## For standalone mode, supply 1. For distributed mode, supply 4 or more.
    ## Note that the operator does not support upgrading from standalone to distributed mode.
    - servers: 4
      ## volumesPerServer specifies the number of volumes attached per MinIO Tenant Pod / Server.
      volumesPerServer: 2
      ## This VolumeClaimTemplate is used across all the volumes provisioned for MinIO Tenant in this Pool.
      volumeClaimTemplate:
        metadata:
          name: data
        spec:
          accessModes:
            - ReadWriteOnce
          resources:
            requests:
              storage: 4Gi
```



## MiniO CLuster on K8s

Ref: https://github.com/minio/operator/blob/master/README.md

This procedure assumes the host machine has kubectl installed and configured with access to the target Kubernetes cluster.

MinIO supports no more than one MinIO Tenant per Namespace. The following kubectl command creates a new namespace for the MinIO Tenant.
```
kubectl create namespace minio-metric
```



useradd -r minio-user -s /sbin/nologin



{{% children  %}}
