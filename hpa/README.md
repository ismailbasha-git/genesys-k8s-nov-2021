#### To perform the lab for this activity please follow the instrucion avaiable [here](https://github.com/kul-samples/genesys-k8s-nov-2021/discussions/17).
#### Manifest deloyment sequence
1. metrics-server.yml, once successfully deployed below commands will start generating output with information about COU & Memory status for PODS & Nodes
  - kubectl top pods -A
  - kubectl top nodes
2. application.yml
3. hpa.yml
#### Create short term pod to simulate load generation using below command, it will create the pod and open the POD terminal
`kubectl run -it --rm load-generator --image=busybox -- /bin/sh`
#### Run following command in POD terminal for load generation
`while true; do wget -q -O- http://webappsvc; done`
#### Check the change in CPU usage and POD replicas for `webap` deployment using
`kubectl get hpa` or `kubectl get pods`
