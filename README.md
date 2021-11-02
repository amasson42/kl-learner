
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

DaemonSets are like replicaset but with exactly one pod running one each node

To start a job:
`kubectl run [-i for interactive] <jobname> --image=gcr.io/kuar-demo/kuard-amd64:1 --restart=OnFailure -- [args...]`
After execution, the job still exist as terminated pod and we should delete it

Create a ConfigMap:
`kubectl create configmap my-config --from-file=my-config.txt --from-literal=param=value`
This creates a configmap with a file and an environment variable. We can stack as much as we want
Environment variable from configmap are also small files

Create a secret:
`kubectl create secret generic kuard-tls --from-file=my-secret.txt`
This creates a generic secret as a mountable directory

`kubectl create secret docker-registry my-image-pull-secret --docker-username=<username> --docker-password=<password> --docker-email=<email>`
In the `kuard-config.yaml` file, the parameter `imagePullSecrets` is the name of the docker-registry secret used to pull private docker images
```
  imagePullSecrets:
    - name: my-image-pull-secret
```

`Param` | Definition
--- | ---
`--from-file=<file>` | use name of the file `file` as key and the content as value
`--from-file=<key>=<file>` | use `key` as key and content of file `file` as value
`--from-file=<directory>` | like `--from-file=<file>` but for each file in the directory `directory`
`--from-literal=<key>=<value>` | too obvious to take time to explain