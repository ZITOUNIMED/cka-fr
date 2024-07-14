# Namespaces
Les objets de kubernetes (PODs, Deployments, Services, ...) sont organisés par des **`Namespaces`**.
Le "Namespace" par défault c'est **`default`**. Il est crée automatiquement quand on met on place un cluster kubernetes.

  ![ns](../../images/ns.PNG)
 
- Afficher tous les pods dans le namespace par défaut:
  ```
  $ kubectl get pods
  ```
- Afficher les pods dans un autre namespace. Dans ce cas le namespace kube-system.
  ```
  $ kubectl get pods --namespace=kube-system
  ```
  ![ns8](../../images/ns8.PNG)
  
- Sans spécifier le namespace la command **`kubectl create`** va créer le pod dans le namespace par défaut:
  ```
  $ kubectl create -f pod-definition.yaml
  ```
- Créer un pod dans le namespace "dev":
  ```
  $ kubectl create -f pod-definition.yaml --namespace=dev
  ```
  ![ns9](../../images/ns9.PNG)

- Pour être sur de créer le pod dans un namespace spécifique on peut le spécifier explicitement dans le fichier de définition YAML.
```
apiVersion: v1
kind: Pod
metadata:
  name: demo-pod
  namespace: dev
  labels:
     app: webapp
     tier: frontend
spec:
  containers:
  - name: nginx
    image: nginx
 ```
  
  ![ns10](../../images/ns10.PNG)
  
- Créer un nouveau namespace à partir d'un fichier de définiton
```
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

  ```
  $ kubectl create -f dev-namespace-definition.yaml
  ```
  Ou juste avec la commande create:
  ```
  $ kubectl create namespace dev
  ```
  ![ns11](../../images/ns11.PNG)
  
- Pour changer le namespace par défaut on peut utiliser la commande suivante:
  ```
  $ kubectl config set-context $(kubectl config current-context) --namespace=dev
  ```
- Afficher tous les pods dans tous les namespaces du cluster:
  ```
  $ kubectl get pods --all-namespaces
  ```
  ![ns12](../../images/ns12.PNG)

  
Documentation Kubernetes
- https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
  
