
### Commandes

`Command` | Definition
--- | ---
general
`kubectl get componentstatuses` | list the components
`kubectl get nodes` | list the nodes (computers/workers links to our cluster)
`kubectl proxy` | locally start proxy web server (http://localhost:8001/ui)
pods
`kubectl get pods` | list the pods (group of running containers)
`kubectl get pods mon-pod -o jsonpath --template={.status.podIP}` | get only a specific pod status ip
`kubectl logs mon-pod` | logs the pod
`kubectl describe pods mon-pod` | who the state and setting of the pod 
`kubectl label pods mon-pod color=red` | apply label to a pod
`kubectl exec -it mon-pod` | exec something in a pod
`kubectl cp mon-pod:/home/homework/safe-video.mp4 /home/dude/video.mp4` | copy file from pod (works both ways)
`kubectl delete pods/mon-pod` | delete the pod
`kubectl port-forward mon-pod 8080:8080` | open a port from a pod container
yaml-objects
`kubectl create -f my-file.yaml` | create the ressources from the file
`kubectl apply -f my-file.yaml` | update the resources from the file
`kubectl delete -f my-file.yaml` | delete the ressources from the file
