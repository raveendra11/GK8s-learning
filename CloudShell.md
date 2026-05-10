
gcpfreetrail6@cloudshell:~/GK8s-learning/k8s-manifests (project-5f0d9702-ce65-4be7-ba2)$ kubectl create -f deploy-task-backend.yaml                                                                                
gcpfreetrail6@cloudshell:~/GK8s-learning/k8s-manifests (project-5f0d9702-ce65-4be7-ba2)$ kubectl get nodes
NAME                                      STATUS   ROLES    AGE     VERSION
gk3-dogood-cluster-pool-3-3ff5b544-5f7d   Ready    <none>   2m33s   v1.35.1-gke.1396002
gk3-dogood-cluster-pool-3-bd957097-jtbt   Ready    <none>   2m4s    v1.35.1-gke.1396002
gcpfreetrail6@cloudshell:~/GK8s-learning/k8s-manifests (project-5f0d9702-ce65-4be7-ba2)$ kubectl get deployments
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
deploy-task-backend   2/2     2            2           3m3s
dogood                0/0     0            0           9d
gcpfreetrail6@cloudshell:~/GK8s-learning/k8s-manifests (project-5f0d9702-ce65-4be7-ba2)$ kubectl get pods
NAME                                  READY   STATUS    RESTARTS   AGE
deploy-task-backend-f54c567d4-9vjhs   1/1     Running   0          4m20s
deploy-task-backend-f54c567d4-khdms   1/1     Running   0          4m20s
gcpfreetrail6@cloudshell:~/GK8s-learning/k8s-manifests (project-5f0d9702-ce65-4be7-ba2)$ kubectl get pods -o wide
NAME                                  READY   STATUS    RESTARTS   AGE     IP            NODE                                      NOMINATED NODE   READINESS GATES
deploy-task-backend-f54c567d4-9vjhs   1/1     Running   0          5m56s   10.103.0.16   gk3-dogood-cluster-pool-3-3ff5b544-5f7d   <none>           <none>
deploy-task-backend-f54c567d4-khdms   1/1     Running   0          5m56s   10.103.0.15   gk3-dogood-cluster-pool-3-3ff5b544-5f7d   <none>           <none>
gcpfreetrail6@cloudshell:~/GK8s-learning/k8s-manifests (project-5f0d9702-ce65-4be7-ba2)$ kubectl run -it --rm temp-pod --image nginx -- sh
Warning: autopilot-default-resources-mutator:Autopilot updated Pod default/temp-pod: defaulted unspecified 'cpu' resource for containers [temp-pod] (see http://g.co/gke/autopilot-defaults).
Warning: BCID failed open: BCID Constraint disabled by Giraffe
All commands and output from this session will be recorded in container logs, including credentials and sensitive information passed through the command prompt.
If you don't see a command prompt, try pressing enter.

# curl 10.103.0.16:8082/task/list
[{"taskId":"task1","taskName":"Task 1","taskPriority":"Critical"},{"taskId":"task2","taskName":"Task 2","taskPriority":"Normal"}]# 
# exit
Session ended, resume using 'kubectl attach temp-pod -c temp-pod -i -t' command when the pod is running
pod "temp-pod" deleted from default namespace
gcpfreetrail6@cloudshell:~/GK8s-learning/k8s-manifests (project-5f0d9702-ce65-4be7-ba2)$ 
