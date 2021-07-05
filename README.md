# vagrant-k3s

## Deploy k3s server cluster using Vagrant

[k3s](https://rancher.com/products/k3s/) is lightweighted kubernets cluster for edge computing.

## Requirements

- Vagrant
- VirtualBox
- Minimum system requirements
    - 2 cpu core, 3GB memory

### macOS

```sh
% brew install --cask vagrant virtualbox vagrant-manager

# % VBoxManage -v
# 6.1.22r144080

# % vagrant --version
# Vagrant 2.2.16
```

## How to deploy

`cd k3s && vagrant up`

## How to connect k3s cluster

```sh
vagrant ssh k3s-m
# ssh root@127.0.0.1 -p 60010
# qwe123

vagrant ssh k3s-w1
# ssh root@127.0.0.1 -p 60011
# qwe123

vagrant ssh k3s-w2
# ssh root@127.0.0.1 -p 60012
# qwe123
```

### Check k3s cluster installing success

```sh
kubectl get nodes -o wide
[root@k3s-m ~ ]# kubectl get nodes -o wide
NAME     STATUS   ROLES                  AGE   VERSION        INTERNAL-IP       EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION     CONTAINER-RUNTIME
k3s-m    Ready    control-plane,master   15d   v1.21.1+k3s1   192.168.200.10    <none>        Ubuntu 20.04.2 LTS   5.4.0-74-generic   docker://20.10.7
k3s-w1   Ready    <none>                 15d   v1.21.1+k3s1   192.168.200.101   <none>        Ubuntu 20.04.2 LTS   5.4.0-74-generic   docker://20.10.7
k3s-w2   Ready    <none>                 15d   v1.21.1+k3s1   192.168.200.102   <none>        Ubuntu 20.04.2 LTS   5.4.0-74-generic   docker://20.10.7

kubectl get pod -n kube-system
kubectl describe node k3s-m
kubectl describe node k3s-w1
kubectl describe node k3s-w2
kubectl get pod -A
```

### Halt virtual machine (stop vm)

- `vagrant halt`

### Destory virtual machine and remove config files

- `vagrant destroy -f && rm -rf .vagrant share`
