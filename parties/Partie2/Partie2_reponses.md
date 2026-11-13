❓ Les différentes ressources sont déployées dans le bon namespace ? Quelle commande utilisez-vous pour vérifier cela ?
kubectl get all --all-namespaces

PS C:\Users\etudiant\Documents\Cours\tp-kubernetes> kubectl get all --all-namespaces
NAMESPACE     NAME                                   READY   STATUS    RESTARTS      AGE
database      pod/mysql-0                            1/1     Running   0             24h
front         pod/nginx-5b9879f4f-25s4p              1/1     Running   0             24h
front         pod/nginx-5b9879f4f-lsxmg              1/1     Running   0             24h
kube-system   pod/coredns-559f6c778d-zbqvn           1/1     Running   1 (24h ago)   6d23h
kube-system   pod/etcd-minikube                      1/1     Running   1 (24h ago)   6d23h
kube-system   pod/kindnet-vl2sl                      1/1     Running   1 (24h ago)   6d23h
kube-system   pod/kube-apiserver-minikube            1/1     Running   1 (24h ago)   6d23h
kube-system   pod/kube-controller-manager-minikube   1/1     Running   1 (24h ago)   6d23h
kube-system   pod/kube-proxy-l8dxm                   1/1     Running   1 (24h ago)   6d23h
kube-system   pod/kube-scheduler-minikube            1/1     Running   1 (24h ago)   6d23h
kube-system   pod/storage-provisioner                1/1     Running   1 (24h ago)   6d23h
middle        pod/wordpress-58c769bdb5-4bfcw         1/1     Running   0             24h

NAMESPACE     NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                  AGE
database      service/mysql        ClusterIP   10.106.103.240   <none>        3306/TCP                 24h
default       service/kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP                  6d23h
front         service/nginx        ClusterIP   10.102.159.10    <none>        8383/TCP                 6d21h
kube-system   service/kube-dns     ClusterIP   10.96.0.10       <none>        53/UDP,53/TCP,9153/TCP   6d23h
middle        service/wordpress    ClusterIP   10.106.98.168    <none>        80/TCP                   24h

NAMESPACE     NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
kube-system   daemonset.apps/kindnet      1         1         1       1            1           <none>                   6d23h
kube-system   daemonset.apps/kube-proxy   1         1         1       1            1           kubernetes.io/os=linux   6d23h

NAMESPACE     NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
front         deployment.apps/nginx       2/2     2            2           6d21h
kube-system   deployment.apps/coredns     1/1     1            1           6d23h
middle        deployment.apps/wordpress   1/1     1            1           24h

NAMESPACE     NAME                                   DESIRED   CURRENT   READY   AGE
front         replicaset.apps/nginx-5b9879f4f        2         2         2       24h
front         replicaset.apps/nginx-5d68b47d97       0         0         0       6d21h
kube-system   replicaset.apps/coredns-559f6c778d     1         1         1       6d23h
middle        replicaset.apps/wordpress-58c769bdb5   1         1         1       24h

NAMESPACE   NAME                     READY   AGE
database    statefulset.apps/mysql   1/1     24h

❓ Les ressources MySQL ConfigMap et MySQL sont à déployer au sein des namespaces middle et database, pourquoi ?
Les ressources Kubernetes comme les ConfigMaps et les Secrets sont propres à leur namespace. Elles ne peuvent donc pas être directement utilisées depuis un autre namespace. Il faut donc créer une copie des ressources MySQL dans le namespace middle pour que Wordpress puisse accéder aux informations de connexion à la base de données.

❓ Les différentes pods sont-ils correctement démarrés ? Quelle commande utilisez-vous pour vérifier cela ?
kubectl get pods --all-namespaces

NAMESPACE     NAME                               READY   STATUS    RESTARTS      AGE
database      mysql-0                            1/1     Running   0             24h
front         nginx-5b9879f4f-25s4p              1/1     Running   0             24h
front         nginx-5b9879f4f-lsxmg              1/1     Running   0             24h
kube-system   coredns-559f6c778d-zbqvn           1/1     Running   1 (24h ago)   6d23h
kube-system   etcd-minikube                      1/1     Running   1 (24h ago)   6d23h
kube-system   kindnet-vl2sl                      1/1     Running   1 (24h ago)   6d23h
kube-system   kube-apiserver-minikube            1/1     Running   1 (24h ago)   6d23h
kube-system   kube-controller-manager-minikube   1/1     Running   1 (24h ago)   6d23h
kube-system   kube-proxy-l8dxm                   1/1     Running   1 (24h ago)   6d23h
kube-system   kube-scheduler-minikube            1/1     Running   1 (24h ago)   6d23h
kube-system   storage-provisioner                1/1     Running   1 (24h ago)   6d23h
middle        wordpress-58c769bdb5-4bfcw         1/1     Running   0             24h

❓ Lorsqu'un pod est en erreur comment accédez-vous aux events du namespace et aux logs du pod ? Quelles commandes utilisez-vous pour vérifier cela ?
kubectl get events -n database