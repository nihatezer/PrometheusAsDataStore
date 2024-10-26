```
@nihatezer ➜ /workspaces/PrometheusAsDataStore (main) $ kubectl get pods -A
NAMESPACE     NAME                                                 READY   STATUS    RESTARTS        AGE
kube-system   coredns-6f6b679f8f-l4zvr                             1/1     Running   2 (4m30s ago)   7d
kube-system   etcd-minikube                                        1/1     Running   2 (4m30s ago)   7d
kube-system   kube-apiserver-minikube                              1/1     Running   2 (4m30s ago)   7d
kube-system   kube-controller-manager-minikube                     1/1     Running   2 (4m30s ago)   7d
kube-system   kube-proxy-vjkss                                     1/1     Running   2 (4m30s ago)   7d
kube-system   kube-scheduler-minikube                              1/1     Running   2 (4m30s ago)   7d
kube-system   storage-provisioner                                  1/1     Running   5 (3m42s ago)   7d
monitoring    prometheus-alertmanager-0                            1/1     Running   2 (4m30s ago)   7d
monitoring    prometheus-kube-state-metrics-75b5bb4bf8-q5s69       1/1     Running   2 (4m30s ago)   7d
monitoring    prometheus-prometheus-node-exporter-7dgrw            1/1     Running   2 (4m30s ago)   7d
monitoring    prometheus-prometheus-pushgateway-84557d6c79-z2tvx   1/1     Running   2 (4m30s ago)   7d
monitoring    prometheus-server-644d686bc6-7k22l                   2/2     Running   4 (4m30s ago)   7d
```
After minikube starts ...