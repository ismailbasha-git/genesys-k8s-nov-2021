#### To perform the lab for this activity please follow the instrucion avaiable [here](https://github.com/kul-samples/genesys-k8s-nov-2021/discussions/17).
#### Manifest deloyment sequence
1. metrics-server.yml, once successfully deployed below commands will start generating output with information about COU & Memory status for PODS & Nodes

`kubectl top pods -A`
```
NAMESPACE       NAME                                       CPU(cores)   MEMORY(bytes)
kube-system     calico-kube-controllers-75f8f6cc59-s7mjz   3m           16Mi
kube-system     calico-node-5ljlj                          21m          119Mi
kube-system     calico-node-5m6nd                          27m          119Mi
kube-system     calico-node-j7bbf                          37m          121Mi
kube-system     coredns-78fcd69978-mdw5h                   2m           11Mi
kube-system     coredns-78fcd69978-tx9qh                   2m           11Mi
kube-system     etcd-master                                13m          101Mi
kube-system     kube-apiserver-master                      58m          371Mi
kube-system     kube-controller-manager-master             14m          53Mi
kube-system     kube-proxy-cfb2x                           1m           14Mi
kube-system     kube-proxy-qmknl                           1m           15Mi
kube-system     kube-proxy-tsznq                           1m           15Mi
kube-system     kube-scheduler-master                      3m           17Mi
kube-system     metrics-server-5d564864d4-ntqxk            4m           13Mi
nginx-ingress   nginx-ingress-5654b9bc84-7mdsf             1m           22Mi
voting-app      coffee-6f4b79b975-8hvxb                    0m           3Mi
voting-app      coffee-6f4b79b975-t8cmd                    0m           1Mi
voting-app      load-generator                             0m           0Mi
voting-app      tea-6fb46d899f-bp46d                       0m           3Mi
voting-app      tea-6fb46d899f-mzjhg                       0m           1Mi
voting-app      tea-6fb46d899f-txzgs                       0m           1Mi
voting-app      webapp-794c9d5db4-cl84h                    1m           82Mi
```
`kubectl top nodes`
```
NAME     CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
master   224m         11%    1553Mi          40%
w1       69m          6%     777Mi           41%
w2       74m          7%     748Mi           39%
```
2. application.yml
`kubectl get all`
3. hpa.yml
`kubectl get hpa`
```
NAME     REFERENCE           TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
webapp   Deployment/webapp   2%/30%    1         5         5          14h
```
#### Create short term pod to simulate load generation using below command, it will create the pod and open the POD terminal
`kubectl run -it --rm load-generator --image=busybox -- /bin/sh`
#### Run following command in POD terminal for load generation
`while true; do wget -q -O- http://webappsvc; done`
#### Check the change in CPU usage and POD replicas for `webap` deployment using
`kubectl get hpa` or `kubectl get pods`
