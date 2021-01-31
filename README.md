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

 # Known issues 

```
vagrant@master:~/app1$ k exec -it try1-5558cbcc-95gl2 -- /bin/bash
error: unable to upgrade connection: pod does not exist
```

```
agrant@master:~/app1$ k get nodes -o wide
NAME     STATUS   ROLES    AGE   VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION       CONTAINER-RUNTIME
master   Ready    master   42h   v1.19.0   10.0.2.15     <none>        Ubuntu 18.04.5 LTS   4.15.0-135-generic   docker://19.3.6
node1    Ready    <none>   42h   v1.19.0   10.0.2.15     <none>        Ubuntu 18.04.5 LTS   4.15.0-132-generic   docker://19.3.6
```

Add *--node-ip* flag to the file */etc/systemd/system/kubelet.service.d/10-kubeadm.conf*

```
# Note: This dropin only works with kubeadm and kubelet v1.11+
[Service]
Environment="KUBELET_KUBECONFIG_ARGS=--bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --node-ip=192.168.0.100"
Environment="KUBELET_CONFIG_ARGS=--config=/var/lib/kubelet/config.yaml"
# This is a file that "kubeadm init" and "kubeadm join" generates at runtime, populating the KUBELET_KUBEADM_ARGS variable dynamically
EnvironmentFile=-/var/lib/kubelet/kubeadm-flags.env
# This is a file that the user can use for overrides of the kubelet args as a last resort. Preferably, the user should use
# the .NodeRegistration.KubeletExtraArgs object in the configuration files instead. KUBELET_EXTRA_ARGS should be sourced from this file.
EnvironmentFile=-/etc/default/kubelet
ExecStart=
ExecStart=/usr/bin/kubelet $KUBELET_KUBECONFIG_ARGS $KUBELET_CONFIG_ARGS $KUBELET_KUBEADM_ARGS $KUBELET_EXTRA_ARGS                                                                                                                    
```
 
