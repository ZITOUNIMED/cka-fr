# Pod
Les pods sont les plus petits déploiements des unités de calcul qu'on peut créer et gérer dans un cluster kubernetes.
Un pod est un groupe d'un ou plusiers containers qui partagent le même stockage et les même resources d'un réseau et il contient les spécifications d'exécution des containers.

- Le fichier de définiton YAML
```
apiVersion: v1
kind: Pod
metadata:
    name: my-sample-pod
    labels:
    app: myapp
    type: frontend
spec:
    containers:
    - name: my-container
        image: nginx:1.16
```
- Créer le pod à partir du fichier de définition:
```
$ kubectl create -f sample-pod-definition.yaml
```
- Lister tous les pods
```
$ kubectl get pods
```
- Supprimer un pod
```
$ kubectl delete pod my-sample-pod
```
- Afficher les logs d'un pod
```
$ kubectl logs my-sample-pod
```

- Créer un pod en utilisant la commande "run"
```
$ kubectl run demo-pod-1 --image=busybox:1.28 
$ kubectl get pods
```

- Générer le fichier de définition d'un pod sans le créer en utilisant l'option "--dry-run=client"
```
$ kubectl run demo-pod-2 --image=nginx --dry-run=client -o yaml > demo-pod-2.yaml 
$ cat demo-pod-2.yaml
$ kubectl create -f demo-pod-2.yaml
$ kubectl get pods
$ vim demo-pod-2.yaml
$ kubectl replace --force -f demo-pod-2.yaml
$ kubectl get pods
```

### Pod plus complexes
Un pod peut contenir plusiurs pods et une configuration plus complexe pour spécifier les volumes, les contexts de sécurité, les demandes des resources, les sélecteurs des nodes, les classes de priorité, etc. Nous verrons toutes ces notions lorsque nous avancerons dans ce cours.

```
$ k create -f cpmplex-pod-definition.yaml
```