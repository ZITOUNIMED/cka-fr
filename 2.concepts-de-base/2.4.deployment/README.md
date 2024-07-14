# Déploiment
  
#### Fichier de définition YAML

```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: demo-deployment
      labels:
        app: webapp
        tier: frontend
    spec:
     template:
        metadata:
          name: demo-app
          labels:
            app: webapp
            tier: frontend
        spec:
         containers:
         - name: nginx
           image: nginx
     replicas: 4
     selector:
       matchLabels:
        tier: frontend
 ```
- Créer le déploiment à partir du fichier de définition YAML
  ```
  $ kubectl create -f demo-deployment-definition.yaml
  ```
- Lister les déploiments
  ```
  $ kubectl get deployment
  ```
- Le déploiment crée automatiquement une **`ReplicaSet`**. 
  ```
  $ kubectl get replicaset
  ```
- Et la ReplicaSet crée les **`PODs`**.
  ```
  $ kubectl get pods
  ```
    
  ![deployment1](../../images/deployment1.PNG)
  

Documentation Kubernetes:
- https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
