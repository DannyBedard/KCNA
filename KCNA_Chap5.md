# Working with Kubernetes

[Retour](./README.md)

## Introduction

La pluspetite unité dans Kubernetes est un pod, une abstraction d'une charge de travail.

Kubernetes offre des outils pour gérer les problèmes d'orchestration, comme la configuration, le réseautage en les node, le routing du traffic externe l'équilabrage de charge ou la mise à l'échelle des pods.

## Kubernetes Objects

Kubernetes fourni des ressources abstraites (appelé objets) qui vont gérer les problèmes d'orchestrtions de conteneurs (self healing, scheduling etc...)

Nous pouvons décrire ces objets avec un fichier YAML

    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: nginx-deployment
    spec: 
    selector:
        matchLabels:
        app: nginx
    replicas: 2 # tells deployment to run 2 pods matching the template
    template:
        metadata:
        labels:
            app: nginx
        spec:
        containers:
        - name: nginx
            image: nginx:1.19
            ports:
            - containerPort: 80

## Interacting with Kubernetes

La ligne de commande officiel est 

    kubectl

Elle permet de contrôler le cluster Kubernetes

La commande suivante

    $ kubectl api-resources

Affiche ceci

    NAME                    SHORTNAMES  APIVERSION  NAMESPACED  KIND
    ...
    configmaps              cm          v1          true        ConfigMap
    ...
    namespaces              ns          v1          false       Namespace
    nodes                   no          v1          false       Node
    persistentvolumeclaims  pvc         v1          true        PersistentVolumeClaim
    ...
    pods                    po          v1          true        Pod
    ...
    services                svc         v1          true        Service

kubectl possède explain, que l'on peut itiliser pour se documenter

    kubectl explain pod

Ou plus précisément

    $ kubectl explain pod.spec

### Demo kubectl

Voir le fichier de config

    kubectl config view

create a pod

    kubectl create -f pod.yaml

Voir les pods

    kubectl get pod

Supprimer un pod

    kubectl delete pod nginx

## Pod concept

L'object le plus important dans Kubernetes est un pod. Ce dernier décrit une unité de un ou plusieurs conteneurs qui ont le même cgroup et namespace. Kubernetes intéragit avec les conteneurs VIA les pods. Tous les conteneurs à l'intérieur d'un pod partage la même adresse IP

![chrootdirectories](./res/Multiplecontainerssharenamespacestoformapod.png)

Son Yaml va ressembler à ça :

    apiVersion: v1
    kind: Pod
    metadata:
    name: nginx-with-sidecar
    spec:
    containers:
    - name: nginx
        image: nginx:1.19
        ports:
        - containerPort: 80
    - name: count
        image: busybox:1.34
        args: [/bin/sh, -c,
                'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done']
    initContainers:
    - name: init-myservice
        image: busybox
        command: ['sh', '-c', 'until nslookup myservice; do echo waiting for myservice; sleep 2; done;']

sidecar container : conteneur qui supporte l'application principal qui est dans un autre conteneur

initContainers: Le conteneur qui va démarrer avant les autres

### Demo Pods

Pour rouler un conteneurs nginx dans un pods

    kubectl run nginx --image=nginx:1.19

Pour apprendre plus sur notre nouveau pod

    kubectl explain pod nginx
    kubectl describe pod nginx

Créer un pod selon un fichier YAML (comme vue ci-haut)

    kubectl -f nomFichier.yaml

## Working Objects

Travailler juste avec des pods n'est pas assez flexible, par exemple, si un node échoue, le pod est perdu pour toujours. Pour être certain que nos pods roulent toujours, on va utiliser des controller objects, envoici une liste:

- ReplicaSet : S'assure qu'un certain nombre de pod roule. Peut être utilisé pour faire de la mise à l'échelle
- Deployment :  Peut gérer plusieurs ReplicaSet pour décrire l'entiereté du cycle de vie de l'application. Mets le tout à jours lorsqu'il y a une nouvelle image.
- StatefulSet : Utiliser pour rouler des application avec un état comme des BD. Ces applications ne se marient pas bien la nature courte des pods et des conteneurs. Il essaie également de retenir les adresse IP des pods et de leur garder le même nom/stockage.
- DaemonSet : S'assure qu'une copie d'un Pod roule sur les nodes désirés, comme des outils du monitoring ou des logs.
- Job : Créer un/plusieurs pods, exécute la tâche et se termine, bon pour les courts script
- CronJob : Pareil comme Job, mais périodiquement

### Demo Workload Objects

Kubeview : Bel outil pour visualiser ce qui se passe dans le cluster

Pour scaler, ajouter 10 copies

    kubectl scale --replicas=10 rs/nginx

