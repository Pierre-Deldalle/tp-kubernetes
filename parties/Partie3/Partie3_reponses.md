PS C:\Users\etudiant\Documents\Cours\tp-kubernetes\TP> kubectl logs -l job-name=date-29909595  
Fri Nov 13 13:15:03 UTC 2026


4. ❓ Avant de poursuivre, expliquez le résultat souhaité.
L'objectif est de configurer un système qui ajuste automatiquement le nombre de Pods NGINX en fonction de leur utilisation du processeur. Au démarrage, un seul Pod est utilisé. Si le nombre de requêtes augmente et que la consommation CPU dépasse le seuil de 20 %, Kubernetes ajoute automatiquement des Pods, jusqu'à un maximum de 5. À l'inverse, lorsque le trafic diminue, le nombre de Pods est progressivement réduit jusqu'à revenir à un minimum de 1.

6. Vérifiez le HPA. Quelle commande avez-vous utilisé ? 
PS C:\Users\etudiant\Documents\Cours\tp-kubernetes\TP> kubectl get hpa
NAME              REFERENCE                    TARGETS       MINPODS   MAXPODS   REPLICAS   AGE
mon-application   Deployment/mon-application   cpu: 0%/20%   1         5         1          75m

NAME :Nom du HPA, REFERENCE: Ressource Kubernetes surveillée, ici le Deployment mon-application, TARGETS: Utilisation CPU actuellement mesurée / utilisation CPU ciblée, MINPODS: Nombre minimum de Pods autorisé, MAXPODS: Nombre maximum de Pods autorisé, REPLICAS: Nombre actuel de réplicas gérés par le Deployment, AGE: Temps écoulé depuis la création du HPA.

9. ❓ Votre HPA fonctionne-t-il comme souhaité ? Ajustez le si nécessaire

Le HPA fonctionne correctement. Pendant le test de charge, l'utilisation du CPU a dépassé le seuil de 20 % configuré. Kubernetes a alors automatiquement augmenté le nombre de réplicas du Deployment en créant de nouveaux Pods. Cela permet à l'application de s'adapter automatiquement à l'augmentation de la charge.