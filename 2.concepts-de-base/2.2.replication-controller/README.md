# Replication Controller
**`Replication Controller`** c'est une ancienne technologie et qui maintenant replacée par **`ReplicaSet`**.

   ![rc2](../../images/rc2.PNG)
## Fichier de définition yaml
```
    apiVersion: v1
    kind: ReplicationController
    metadata:
      name: demo-rc
      labels:
        app: webapp
    spec:
     template:
        metadata:
          name: webapp
          labels:
            app: webapp
        spec:
         containers:
         - name: nginx
           image: nginx
     replicas: 2
```
  - Créer une "replication controller"
    ```
    $ kubectl create -f demo-rc-definition.yaml
    ```
  - Afficher toutes les "replication controllers"
    ```
    $ kubectl get replicationcontroller
    ```
  - Afficher tous les "pods" lancés par la "replication controller"
    ```
    $ kubectl get pods
    ```
    ![rc3](../../images/rc3.PNG)