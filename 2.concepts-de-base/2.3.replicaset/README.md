# ReplicaSet
 **`ReplicaSet`** c'est une nouvelle manière pour mettre en place une réplication.
   ![rs](../../images/rs.PNG)

## Fichier de définition YAML
```
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
      name: demo-replicaset
      labels:
        app: webapp
    spec:
     template:
        metadata:
          name: webapp
          labels:
            app: webapp
            tier: frontend
        spec:
         containers:
         - name: nginx
           image: nginx
     replicas: 3
     selector:
       matchLabels:
        tier: frontend
 ```   
  - Créer la "replicaset"
    ```
    $ kubectl create -f demo-replicaset-definition.yaml
    ```
  - Lister toutes les "replicaset"
    ```
    $ kubectl get replicaset
    ```
  - Lister tous les "pods" lancés par la "replicaset"
    ```
    $ kubectl get pods
    ```
   
    ![rs1](../../images/rs1.PNG)
   
## Noter bien
 - La "ReplicaSet" nécessite un "selector". Ce qui n'est pas le cas de "Replication Controller".

  ![labels](../../images/labels.PNG)
  
## Comment mettre à l'échelle une "ReplicaSet"
Il y a trois façons pour mettre à l'échelle une "ReplicaSet"
1. modifier le nombre des "replicas" dans le fichier de définition YAML.
 ```
   apiVersion: apps/v1
       kind: ReplicaSet
       metadata:
         name: demo-replicaset
         labels:
           app: webapp
       spec:
        template:
           metadata:
             name: webapp
             labels:
               app: webapp
               tier: frontend
           spec:
            containers:
            - name: nginx
              image: nginx
        replicas: 6
        selector:
          matchLabels:
           tier: frontend
```

  ```
  $ kubectl apply -f demo-replicaset-definition.yaml
  ```
2. Deuxième façon c'est d'utiliser la commande **`kubectl scale`** et avec le nom du fichier de définition.
  ```
  $ kubectl scale --replicas=6 -f demo-replicaset-definition.yaml
  ```
3. Troixième façon c'est d'utiliser la commande **`kubectl scale`** avec le nom de la "ReplicaSet".
  ```
  $ kubectl scale --replicas=6 replicaset demo-replicaset
  ```
  ![rs2](../../images/rs2.PNG)

#### Documentation Kubernetes:
- https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/
- https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/
