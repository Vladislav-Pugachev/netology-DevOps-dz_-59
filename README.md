### Задание 1: установить в кластер CNI плагин Calico
- установка производится через ansible/kubespray
```commandline
vlad@home:~/Documents/Netology/DevOps/dz_№59$ kubectl get pods -n kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-56fd7b8dc-d8mzv   1/1     Running   0             75m
calico-node-jtcw4                         1/1     Running   0             77m
calico-node-p789m                         1/1     Running   0             77m
calico-node-wdjv5                         1/1     Running   0             77m
```

- после применения следует настроить политику доступа к hello-world извне.
- - До применения политики [denyall.yml](./denyall.yml)
```commandline
vlad@master1:~/kubespray$ curl http://10.233.105.131:8080
Hello World!vlad@master1:~/kubespray$ 
```
- - После применения политики [denyall.yml](./denyall.yml)
```commandline
url http://10.233.105.131:8080
curl: (28) Failed to connect to 10.233.105.131 port 8080: Connection timed out
```
- - После примения политки [allowTCP8080.yml](./allowTCP8080.yml)
```commandline
curl http://10.233.105.131:8080
Hello World!vlad@master1:~/kubespray$ 
```

### Задание 2. изучить, что запущено по умолчанию
```commandline
vlad@master1:~/kubespray$ calicoctl get nodes
NAME      
master1   
worker1   
worker2   

vlad@master1:~/kubespray$ calicoctl get ipPool
NAME           CIDR             SELECTOR   
default-pool   10.233.64.0/18   all()      

vlad@master1:~/kubespray$ calicoctl get profile
NAME                                                 
projectcalico-default-allow                          
kns.default                                          
kns.kube-node-lease                                  
kns.kube-public                                      
kns.kube-system                                      
kns.tigera-operator                                  
ksa.default.default                                  
ksa.kube-node-lease.default                          
ksa.kube-public.default                              
ksa.kube-system.attachdetach-controller              
ksa.kube-system.bootstrap-signer                     
ksa.kube-system.calico-kube-controllers              
ksa.kube-system.calico-node                          
ksa.kube-system.certificate-controller               
ksa.kube-system.clusterrole-aggregation-controller   
ksa.kube-system.coredns                              
ksa.kube-system.cronjob-controller                   
ksa.kube-system.daemon-set-controller                
ksa.kube-system.default                              
ksa.kube-system.deployment-controller                
ksa.kube-system.disruption-controller                
ksa.kube-system.dns-autoscaler                       
ksa.kube-system.endpoint-controller                  
ksa.kube-system.endpointslice-controller             
ksa.kube-system.endpointslicemirroring-controller    
ksa.kube-system.ephemeral-volume-controller          
ksa.kube-system.expand-controller                    
ksa.kube-system.generic-garbage-collector            
ksa.kube-system.horizontal-pod-autoscaler            
ksa.kube-system.job-controller                       
ksa.kube-system.kube-proxy                           
ksa.kube-system.namespace-controller                 
ksa.kube-system.node-controller                      
ksa.kube-system.nodelocaldns                         
ksa.kube-system.persistent-volume-binder             
ksa.kube-system.pod-garbage-collector                
ksa.kube-system.pv-protection-controller             
ksa.kube-system.pvc-protection-controller            
ksa.kube-system.replicaset-controller                
ksa.kube-system.replication-controller               
ksa.kube-system.resourcequota-controller             
ksa.kube-system.root-ca-cert-publisher               
ksa.kube-system.service-account-controller           
ksa.kube-system.service-controller                   
ksa.kube-system.statefulset-controller               
ksa.kube-system.token-cleaner                        
ksa.kube-system.ttl-after-finished-controller        
ksa.kube-system.ttl-controller                       
ksa.tigera-operator.default                          
ksa.tigera-operator.tigera-operator                  

vlad@master1:~/kubespray$ 

```