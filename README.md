# kubernetes-labs

## kubeadm init

```
sudo kubeadm init --kubernetes-version 1.19.0 --apiserver-advertise-address 192.168.0.100 --pod-network-cidr 172.16.0.0/16
```

## kubectl configuration
```
mkdir ~/.kube/
sudo cp /etc/kubernetes/admin.conf ~/.kube/config
sudo chown $(id -u):$(id -g) ~/.kube/config
```

## Cluster network
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

# Links to bookmark

 [https://kubernetes.io/docs/reference/kubectl/cheatsheet/]

 
