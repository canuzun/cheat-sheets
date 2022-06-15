[Official Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
[Pod DNS Stuff](https://unofficial-kubernetes.readthedocs.io/en/latest/concepts/services-networking/dns-pod-service/)

````
kubectl cluster-info

kubectl apply -f twx-pod.yml
kubectl delete -f twx-pod.yml

kubectl get svc

kubectl get pods --watch
kubectl get pods -o wide

###LOGS###
kubectl logs my-pod                   #pod logs, maybe not all container logs
kubectl logs my-pod mssql-init        #container logs, container name from yaml 
kubectl describe pods
````
