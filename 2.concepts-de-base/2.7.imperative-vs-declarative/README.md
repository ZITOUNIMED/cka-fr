# Imerative 
```
$ kubectl run nginx --image=nginx:1.16
$ kuebectl create deployment my-deploy --image=busybox --replicas=3
$ kubectl edit deployment my-deploy 
$ kubectl scale deployment my-deploy --replicas=4
$ kubectl set image deployment my-deploy busybox=busybox:1.28
$ kubectl create -f nginx.yaml
$ kubectl delete deployment my-deploy
$ kubectl delete -f nginx.yaml
$ kubectl replace -f nginx.yaml
```
Les commandes impérative permetent des créer des objets, les supprimer, mais la modification n'est pas toujours garantie. En fait, dans des cas particulier on ne peut par modifier des propriétés spécifiques d'un objets déjà créer avec les commandes "edit" ou "replace". Par example le changement de l'image d'un container n'est pas possible sauf si on force la commande.

- Exemple: modifier la version de l'image nginx et executer la commande suivante:
```
$ kubectl replace -f nginx.yaml
# Erreur
```
- Utiliser l'option "--force" pour forcer la modification:
```
$ kubectl replace --force -f nginx.yaml
```

# Declarative
La commande "apply" permet d'appliquer toutes modifications aporter à un fichier de définition d'une façon optimisée et sécurisée.
```
$ kubectl apply -f nginx.yaml
```