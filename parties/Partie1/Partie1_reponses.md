4. Vérifier les events du namespace et le bon démarrage des pods et de leurs conteneurs ❓ Quelles sont les 2 commandes utilisées ?

 **kubectl get pods -n front**

 NAME                              READY   STATUS    RESTARTS   AGE
nginx-deployment-9cd4455d-2j7cn   1/1     Running   0          3m19s
nginx-deployment-9cd4455d-lg47z   1/1     Running   0          3m19s
nginx-deployment-9cd4455d-mtfsb   1/1     Running   0          3m19s

**kubectl get events -n front**

LAST SEEN   TYPE      REASON                         OBJECT                                 MESSAGE
2m53s       Normal    Scheduled                      pod/nginx-deployment-9cd4455d-2j7cn    Successfully assigned front/nginx-deployment-9cd4455d-2j7cn to minikube
2m52s       Normal    Pulling                        pod/nginx-deployment-9cd4455d-2j7cn    Pulling image "nginx:1.14.2"
2m46s       Normal    Pulled                         pod/nginx-deployment-9cd4455d-2j7cn    Successfully pulled image "nginx:1.14.2" in 698ms (6.684s including waiting). Image size: 44710204 bytes.
2m46s       Normal    Created                        pod/nginx-deployment-9cd4455d-2j7cn    Container created
2m46s       Normal    Started                        pod/nginx-deployment-9cd4455d-2j7cn    Container started
2m53s       Normal    Scheduled                      pod/nginx-deployment-9cd4455d-lg47z    Successfully assigned front/nginx-deployment-9cd4455d-lg47z to minikube
2m52s       Normal    Pulling                        pod/nginx-deployment-9cd4455d-lg47z    Pulling image "nginx:1.14.2"
2m47s       Normal    Pulled                         pod/nginx-deployment-9cd4455d-lg47z    Successfully pulled image "nginx:1.14.2" in 5.341s (5.342s including waiting). Image size: 44710204 bytes.
2m47s       Normal    Created                        pod/nginx-deployment-9cd4455d-lg47z    Container created
2m47s       Normal    Started                        pod/nginx-deployment-9cd4455d-lg47z    Container started
2m53s       Normal    Scheduled                      pod/nginx-deployment-9cd4455d-mtfsb    Successfully assigned front/nginx-deployment-9cd4455d-mtfsb to minikube
2m52s       Normal    Pulling                        pod/nginx-deployment-9cd4455d-mtfsb    Pulling image "nginx:1.14.2"
2m46s       Normal    Pulled                         pod/nginx-deployment-9cd4455d-mtfsb    Successfully pulled image "nginx:1.14.2" in 717ms (6.057s including waiting). Image size: 44710204 bytes.
2m46s       Normal    Created                        pod/nginx-deployment-9cd4455d-mtfsb    Container created
2m46s       Normal    Started                        pod/nginx-deployment-9cd4455d-mtfsb    Container started
2m53s       Warning   FailedCreate                   replicaset/nginx-deployment-9cd4455d   Error creating: Unauthorized
2m53s       Normal    SuccessfulCreate               replicaset/nginx-deployment-9cd4455d   Created pod: nginx-deployment-9cd4455d-2j7cn
2m53s       Normal    SuccessfulCreate               replicaset/nginx-deployment-9cd4455d   Created pod: nginx-deployment-9cd4455d-lg47z
2m53s       Normal    SuccessfulCreate               replicaset/nginx-deployment-9cd4455d   Created pod: nginx-deployment-9cd4455d-mtfsb
2m53s       Warning   ReplicaSetCreateError          deployment/nginx-deployment            Failed to create new replica set "nginx-deployment-9cd4455d": Unauthorized
2m53s       Normal    ScalingReplicaSet              deployment/nginx-deployment            Scaled up replica set nginx-deployment-9cd4455d from 0 to 3
97s         Warning   FailedToUpdateEndpointSlices   service/nginx                          Error updating Endpoint Slices for Service front/nginx: failed to create EndpointSlice for Service front/nginx: Unauthorized

7. ❓ A quoi correspond les pointillés violet ? 
Les pointillés violets représentent la ressource Deployment nginx. Elle gère les 2 pods (replicas) qui portent le label app: reverse-proxy et s’assure qu’ils tournent en permanence. C’est le développeur / DevOps qui la définit (nginx-deployment.yml).

8. ❓ A quoi correspond les pointillés ?
Les pointillés rouges représentent le namespace front. Il regroupe et isole toutes les ressources du reverse proxy (le Service nginx et les pods gérés par le Deployment) à l’intérieur du cluster. Sa gestion revient à l’administrateur du cluster.