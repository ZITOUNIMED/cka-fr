# Services
- Les services de kubernetes permettent de communiquer les composants du cluster kubernetes entre eux et avec l'exterieur.

  ![srv1](../../images/srv1.PNG)
  
    
## Les types des services de kubernetes
 
#### Il y a 3 types des services kubernetes
 
 
1. NodePort
    - Le service de type NodePort permet de rendre une application accessible à travers un port d'un Node du cluster.
    Dans cette exemple, on crée le service demo-service-nodeport dans le namespace par défaut pour rendre l'application "webapp" frontend accessible via le port 30010 du node où les pods qui hébergent l'application s'exécutent.
      ```
      apiVersion: v1
      kind: Service
      metadata:
       name: demo-service-nodeport
      spec:
       types: NodePort
       ports:
       - targetPort: 80
         port: 80
         nodePort: 30010
       selector:
         app: webapp
         tier: frontend
      ```
    - Créer le service:
      ```
      $ kubectl create -f demo-service-nodeport.yaml
      ```
    - Lister les services:
      ```
      $ kubectl get services
      ```
      
      #### Accéder à l'application
      Maintenant on peut utiliser l'adresse IP du node et le port qu'on a spécifié pour accéder à l'application avec la commande "curl" ou à partir d'un browser.
      ```
      # Node IP is 192.168.1.2
      $ curl http://192.168.1.2:30010
      ```
      
      ![srvnp2](../../images/srvnp2.PNG)

      
      #### Quand les pods sont distribués sur plusieurs nodes dans ce cas le port reste le même mais on bascule entre les adresses IP des différents nodes.
     
      ```
      # Node 1 IP is 192.168.1.2
      # Node 2 IP is 192.168.2.2

      $ curl http://192.168.1.2:30010
      $ curl http://192.168.2.2:30010
      ```
     
            
 2. ClusterIP
    - Ce le type par défaut des service et qui permet de créer une adresse IP virtuelle **`Virtual IP`** à l'intérieur du cluster kubernetes pour permettre aux différents composants du cluster de communiquer entre eux. Commepar exemple une application avec deux tiers frontend et backend. On crée un service pour le tier backend pour permettre au tier frontend d'avoir une distination backend unique et inchangeable. Le tier frontend va tjrs utiliser le nom du service du backend même si les pods du backend changent.
    ```
      apiVersion: v1
      kind: Service
      metadata:
       name: demo-service-clusterip
      spec:
       types: ClusterIp
       ports:
       - targetPort: 80
         port: 80
       selector:
         app: webapp
         tier: frontend
      ```
    
 3. LoadBalancer
    - Ce type des service permet surtout les applications en production qui nécessitent un répartiteur de charge "load balancer" pour distribuer le traffic correctement sur les différents serveurs de l'applications.
    
Documentation Kubernetes
- https://kubernetes.io/docs/concepts/services-networking/service/

