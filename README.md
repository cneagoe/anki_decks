# anki_decks

<!-- 
sample:
##

```console

```

todo: 
gpg certs
tls certs

reserve:
## How do you upgrade a master node configured with kubeadm?
upgrade kubeadm itself
upgrade all the components (except kubelet)
drain the node
upgrade kubelet on the master node
restart service
uncordon node
```console
apt-get upgrade -y kubeadm=1.12.0-00
kubeadm upgrade plan
kubeadm upgrade apply
apt-get upgrade -y kubelet=1.12.0-00
systemctl restart kubelet
```
## How do you upgrade a worker node configured with kubeadm?
drain the node
upgrade kubeadm itself
upgrade kubelet on the master node
update config
restart service
uncordon node
```console
kubectl drain node-1
apt-get upgrade -y kubeadm=1.12.0-00
apt-get upgrade -y kubelet=1.12.0-00
kubeadm upgrade node config --kubelet-version v1.12.0
systemctl restart kubelet
kubectl uncordon node-1

to move to linux:
what does apt-cache madison do
```
-->