
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
`kubectl describe pods mon-pod` | show the state and setting of the pod 
`kubectl exec -it mon-pod` | exec something in a pod
`kubectl cp mon-pod:/home/homework/safe-video.mp4 /home/dude/video.mp4` | copy file from pod (works both ways)
`kubectl delete pods/mon-pod` | delete the pod
`kubectl delete pods --all` | delete all pods
`kubectl port-forward mon-pod 8080:8080` | open a port from a pod container
deployments
`kubectl get deployments` | list deployments
`kubectl edit deployments/<dep-name>` | open editor to modify deployment yaml
replicaset
`kubectl scale replicasets <rs> --replicas=<n>` | scale the number of replicaset pod
`kubectl autoscale rs <rs> --min=<nmin> --max=<nmax> --cpu-percent=<[0-100]>` | auto scale with values
yaml-objects
`kubectl create -f my-file.yaml` | create the ressources from the file
`kubectl apply -f my-file.yaml` | update the resources from the file
`kubectl delete -f my-file.yaml` | delete the ressources from the file
labels
`kubectl label pods mon-pod color=red` | apply label to a pod
`kubectl label pods mon-pod color-` | remove the label to a pod
`kubectl get <object> --show-labels` | list objects of type and show attributed labels
`kubectl get <object> -L <label>` | list object of type and a column for the value of the label
`kubectl get <object> --selector="<label>=<value>"` | list object filter with exact match label/value
`kubectl get <object> --selector="<label>"` | list object having given label defined with any value
`kubectl get <object> --selector="<label1>=<value1>,<label2>=<value2>,..."` | list object filter with exact match label/value of multiple labels  (AND)
`kubectl get <object> --selector="<label> in (<value1>,<value2>,<value3>)"` | filter label that has any of given value (OR)
services
`kubectl expose pods mon-pod` | expose a pod to put a service with an ip and a load balancer (can work with other objects)
`kubectl get services` | list current services and their ip addresses



When we expose something with a service, it has a load balancer with a static address. The value of the ip is sent to all other pods as environment variable with the name `{SERVICE_UPPERCASED}_SERVICE_HOST` and the port as `{SERVICE_UPPERCASED}_SERVICE_PORT`
